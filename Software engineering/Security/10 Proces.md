# Proces

Pojedyncze techniki z poprzednich rozdziałów działają tylko wtedy, gdy zespół stosuje je regularnie, a nie od przypadku do przypadku. Ten rozdział opisuje, jak wbudować bezpieczeństwo w codzienną pracę: narzędzia w CI, przegląd kodu z listą kontrolną i przygotowanie na sytuację, w której mimo wszystko coś pójdzie źle.

```text
pomysł ──► projekt ──► kod ──► review ──► CI ──► staging ──► produkcja ──► monitoring
           STRIDE      pre-commit  lista    SAST,     DAST        check       alerty,
           (rozdz. 01) gitleaks    kontrolna SCA,      (ZAP)       --deploy    reakcja na
                                            testy                              incydent
```

## Bezpieczeństwo w każdym kroku

Bezpieczeństwo w cyklu wytwarzania (secure SDLC, shift left) oznacza szukanie problemów jak najwcześniej, bo błąd znaleziony przy projektowaniu kosztuje minuty, a na produkcji dni i reputację. Automaty w CI sprawdzają to, co da się sprawdzić mechanicznie, a ludzie resztę.

<a id="term-sast"></a>[SAST](00%20Glossary%20Security.md#sast) (Static Application Security Testing) analizuje kod bez uruchamiania go i szuka wzorców typowych dla podatności:

- `bandit` wykrywa niebezpieczne wywołania w Pythonie: `pickle.loads`, `yaml.load`, `subprocess` z `shell=True`, `verify=False`, `random` w kontekście tokenów, zakodowane hasła,
- `semgrep` pozwala pisać własne reguły i ma gotowe zestawy dla Django (`p/django`): `mark_safe` z f-stringiem, `csrf_exempt`, `raw()` z formatowaniem, `fields = "__all__"`,
- CodeQL (GitHub) śledzi przepływ danych od źródła (np. `request.GET`) do niebezpiecznego miejsca (np. `cursor.execute`).

```yaml
# fragment pipeline'u
- run: bandit -r shop -ll                             # tylko średnia i wysoka waga
- run: semgrep scan --config p/django --config p/python --error
- run: pip-audit -r requirements.txt                  # SCA, rozdział 08
- run: python manage.py check --deploy --fail-level WARNING
```

<a id="term-dast"></a>[DAST](00%20Glossary%20Security.md#dast) (Dynamic Application Security Testing) testuje działającą aplikację z zewnątrz, jak napastnik. OWASP ZAP w trybie baseline przegląda środowisko testowe i zgłasza brakujące nagłówki, ciasteczka bez flag, błędy konfiguracji i część podatności XSS. Pełny skan aktywny uruchamia się rzadziej, bo trwa długo i modyfikuje dane.

| | SAST | DAST |
|---|---|---|
| Co bada | kod źródłowy | działającą aplikację |
| Kiedy | przy każdym commicie | na stagingu, np. nocą |
| Mocne strony | szybko, wskazuje linię kodu | widzi konfigurację, nagłówki, rzeczywiste odpowiedzi |
| Słabe strony | fałszywe alarmy, nie zna kontekstu biznesowego | wolniej, nie wskazuje miejsca w kodzie, słabo widzi autoryzację |
| Przykłady | bandit, semgrep, CodeQL | OWASP ZAP, Burp Suite |

Żadne narzędzie nie znajdzie błędów autoryzacji, bo nie wie, kto powinien widzieć które zamówienie. Te sprawdzają testy bezpieczeństwa pisane przez zespół, jak zwykłe testy:

```python
@pytest.mark.parametrize("method,url", [
    ("get", "/api/orders/{pk}/"),
    ("patch", "/api/orders/{pk}/"),
    ("delete", "/api/orders/{pk}/"),
    ("get", "/api/orders/{pk}/invoice/"),
])
def test_other_customers_order_is_not_accessible(api_client, customer, other_order, method, url):
    api_client.force_authenticate(customer)
    response = getattr(api_client, method)(url.format(pk=other_order.pk))
    assert response.status_code == 404


def test_every_api_view_has_explicit_permissions():
    for pattern in get_resolver().url_patterns:
        view = getattr(pattern.callback, "cls", None)
        if view and issubclass(view, APIView):
            assert AllowAny not in view.permission_classes or view in PUBLIC_VIEWS, view
```

Dobrze działa też cykliczny test penetracyjny wykonywany przez zewnętrzną firmę, np. raz w roku i przed dużymi zmianami. Narzędzia i testy zespołu znajdują rzeczy powtarzalne, a pentester błędy logiki i nietypowe ścieżki.

Narzędzia trzeba dostroić. SAST z setkami fałszywych alarmów szybko przestaje być czytany. Lepiej zacząć od reguł o wysokiej wadze i blokować build tylko dla nowych problemów, a stare zapisać jako dług do spłaty.

## Przegląd kodu z myślą o napastniku

Automaty nie zastąpią review. Przegląd kodu pod kątem bezpieczeństwa to nie osobny proces, tylko kilka pytań zadawanych przy każdej zmianie, która dotyka danych, uprawnień albo granic systemu. Lista kontrolna dla projektu Django:

Autoryzacja (rozdział 05):

- czy nowy widok ma jawne `permission_classes` i czy `get_queryset` filtruje po właścicielu lub najemcy,
- czy akcje `@action` i widoki funkcyjne pobierają obiekty przez `get_object()` albo z filtrem po użytkowniku,
- czy identyfikatory w treści żądania są sprawdzane względem użytkownika,
- czy jest test z cudzym obiektem.

Dane wejściowe i wyjściowe (rozdziały 02, 03, 05 i 09):

- czy serializer ma jawną listę `fields` i `read_only_fields`, a nie `"__all__"`,
- czy surowy SQL używa parametrów, a nazwy pól z żądania są na liście dozwolonych,
- czy pojawia się `mark_safe`, `|safe`, `format_html` z f-stringiem albo `innerHTML` we frontendzie,
- czy nowy upload waliduje typ po zawartości, rozmiar i nazwę,
- czy kod pobiera URL podany przez użytkownika (SSRF),
- czy `subprocess`, `pickle`, `yaml.load` albo `eval` dotykają danych z zewnątrz.

Uwierzytelnianie, sekrety i konfiguracja (rozdziały 04, 06 i 07):

- czy pojawił się `@csrf_exempt` i czym jest zastąpiony,
- czy tokeny są generowane przez `secrets` i porównywane przez `compare_digest`,
- czy nie ma sekretów w kodzie, testach i fixture'ach,
- czy zmiany w `settings` nie osłabiają ustawień produkcyjnych,
- czy logi nie zapisują danych osobowych, haseł ani tokenów.

Zależności (rozdział 08):

- czy nowa zależność jest potrzebna, ma poprawną nazwę i jest utrzymywana,
- czy lockfile zaktualizowano z hashami.

Lista nie musi być przechodzona w całości przy każdym PR. Szablon pull requesta z kilkoma pytaniami („czy zmiana dotyka uprawnień, danych osobowych, uploadu, zewnętrznych URL-i?”) kieruje uwagę tam, gdzie jest potrzebna. Zmiany w obszarach wrażliwych (uwierzytelnianie, płatności, uprawnienia) mogą wymagać review osoby z większym doświadczeniem w bezpieczeństwie, przez `CODEOWNERS`.

## Gdy coś się wydarzy

<a id="term-incident-response"></a>[Reakcja na incydent](00%20Glossary%20Security.md#incident-response) to zaplanowany sposób postępowania po wykryciu podatności albo naruszenia. Plan przygotowany zawczasu jest ważny, bo w czasie incydentu nie ma czasu na ustalanie, kto decyduje i kogo powiadomić.

Etapy według NIST (SP 800-61):

1. Przygotowanie: kontakt do osoby odpowiedzialnej, dostęp do logów, możliwość szybkiego wyłączenia funkcji (flagi), procedura rotacji sekretów, kanał zgłoszeń od badaczy (`security.txt`, adres `security@`).
2. Wykrycie i analiza: potwierdzenie, że problem jest prawdziwy, ustalenie zakresu (które dane, którzy użytkownicy, od kiedy) i zabezpieczenie dowodów, czyli logów i stanu systemu, zanim zostaną nadpisane.
3. Powstrzymanie, usunięcie i przywrócenie: najpierw zatrzymanie szkód (wyłączenie podatnej funkcji flagą, unieważnienie sesji i tokenów, rotacja sekretów, blokada adresów), potem poprawka i wdrożenie, na końcu przywrócenie normalnego działania i obserwacja.
4. Działania po incydencie: analiza przyczyn i usprawnienia.

Przykład: badacz zgłasza, że `GET /api/orders/{id}/invoice/` zwraca faktury dowolnych klientów.

```text
godz. 0   potwierdzenie zgłoszenia w środowisku testowym, powołanie osoby prowadzącej
godz. 1   flaga: endpoint faktur wyłączony, zamiast niego komunikat „chwilowo niedostępne”
godz. 2   analiza logów dostępu: które faktury pobrali użytkownicy inni niż właściciele, od kiedy
godz. 4   poprawka (get_queryset + test z cudzym obiektem), review, wdrożenie, włączenie flagi
godz. 8   ocena: faktury zawierają dane osobowe, pobrano 312 cudzych faktur przez 3 konta
godz. 24  decyzja o zgłoszeniu do organu nadzorczego i powiadomieniu klientów
tydzień   analiza po incydencie, test z cudzym obiektem dla wszystkich endpointów w CI
```

Obowiązki prawne mają konkretne terminy. RODO (art. 33) wymaga zgłoszenia naruszenia ochrony danych osobowych do organu nadzorczego, w Polsce do Prezesa UODO, w ciągu 72 godzin od jego stwierdzenia, chyba że naruszenie prawdopodobnie nie powoduje ryzyka. Jeśli ryzyko dla osób jest wysokie, trzeba je też powiadomić (art. 34). Decyzję podejmuje się z inspektorem ochrony danych i działem prawnym, ale programista dostarcza fakty: jakie dane, ilu osób, od kiedy.

Zgłoszenia od zewnętrznych badaczy warto ułatwić. Plik `/.well-known/security.txt` z adresem kontaktowym i zasadami odpowiedzialnego ujawniania (responsible disclosure) sprawia, że podatność trafi do zespołu, a nie na forum.

<a id="term-blameless-postmortem"></a>[Analiza po incydencie bez szukania winnych](00%20Glossary%20Security.md#blameless-postmortem) (blameless postmortem) kończy każdy incydent. Pytanie nie brzmi „kto popełnił błąd?”, tylko „dlaczego system i proces pozwoliły, żeby błąd trafił na produkcję i pozostał niezauważony?”. W przykładzie odpowiedzią nie jest „programista zapomniał o filtrze”, tylko brak testów autoryzacji w CI i klasa bazowa widoku, która nie wymuszała filtrowania. Wynikiem są konkretne działania z właścicielami i terminami: test dla wszystkich endpointów, zmiana klasy bazowej, reguła semgrep. Dzięki temu ten sam błąd nie powtórzy się w innym miejscu.

## Co zapamiętać

- Shift left: problemy szuka się jak najwcześniej, od modelowania zagrożeń, przez pre-commit, po CI.
- SAST (bandit, semgrep z regułami Django, CodeQL) sprawdza kod, DAST (OWASP ZAP) działającą aplikację. Narzędzia dostraja się, żeby nie zalewały fałszywymi alarmami.
- Błędów autoryzacji nie znajdzie żadne narzędzie. Potrzebne są testy z cudzym obiektem dla wszystkich endpointów i test wymuszający jawne uprawnienia.
- Review z listą kontrolną: autoryzacja, dane wejściowe i wyjściowe, CSRF, sekrety, konfiguracja, logi i zależności. Obszary wrażliwe obsługuje `CODEOWNERS`.
- Reakcja na incydent: przygotowanie, analiza z zabezpieczeniem dowodów, powstrzymanie (flaga, unieważnienie, rotacja), poprawka i analiza po incydencie. RODO daje 72 godziny na zgłoszenie do UODO.
- `security.txt` ułatwia zgłoszenia badaczom. Analiza bez szukania winnych szuka przyczyn w systemie i procesie, a nie w ludziach.

## Pytania sprawdzające

### 43. Jak wbudować bezpieczeństwo w cykl wytwarzania (SAST jak `bandit` i `semgrep`, DAST, testy bezpieczeństwa w CI)?

<details>
<summary>Odpowiedź</summary>

Przez shift left, czyli szukanie problemów jak najwcześniej: modelowanie zagrożeń przy projekcie, pre-commit (gitleaks), w CI SAST (`bandit` dla niebezpiecznych wywołań Pythona, `semgrep` z regułami `p/django`, CodeQL dla przepływu danych), SCA (`pip-audit`) i `check --deploy`, a na stagingu DAST (OWASP ZAP baseline, rzadziej pełny skan). Błędów autoryzacji nie znajdą narzędzia, więc potrzebne są własne testy: cudzy obiekt dla każdego endpointu i test wymuszający jawne uprawnienia. Do tego cykliczny pentest. Narzędzia dostraja się i blokuje build tylko przy nowych problemach wysokiej wagi.

Zobacz: sekcja „Bezpieczeństwo w każdym kroku”.

</details>

### 44. Na co patrzeć w code review pod kątem bezpieczeństwa w projekcie Django (lista kontrolna)?

<details>
<summary>Odpowiedź</summary>

Autoryzacja: jawne `permission_classes`, `get_queryset` filtrujący po właścicielu lub najemcy, `@action` przez `get_object()`, sprawdzone identyfikatory z treści żądania, test z cudzym obiektem. Dane: jawne `fields` i `read_only_fields`, parametryzowany SQL i lista dozwolonych nazw pól, `mark_safe` i `|safe`, walidacja uploadu, pobieranie URL-i od użytkownika (SSRF), `subprocess`, `pickle`, `yaml.load` i `eval`. Uwierzytelnianie i konfiguracja: `@csrf_exempt`, `secrets` i `compare_digest`, sekrety w kodzie i testach, osłabione ustawienia, dane osobowe w logach. Zależności: potrzeba, nazwa, lockfile z hashami. Pomagają szablon PR z pytaniami i `CODEOWNERS` dla obszarów wrażliwych.

Zobacz: sekcja „Przegląd kodu z myślą o napastniku”.

</details>

### 45. Co zrobić, gdy w produkcji wykryto podatność albo wyciek (reakcja na incydent, komunikacja, analiza po incydencie)?

<details>
<summary>Odpowiedź</summary>

Postępować według planu (NIST SP 800-61). Przygotowanie: osoba odpowiedzialna, logi, flagi, procedura rotacji, `security.txt`. Analiza: potwierdzenie, zakres, zabezpieczenie dowodów. Powstrzymanie: wyłączenie funkcji flagą, unieważnienie sesji i tokenów, rotacja sekretów, blokady. Potem poprawka z testem, wdrożenie i obserwacja. Przy danych osobowych: zgłoszenie do organu nadzorczego (w Polsce UODO) w ciągu 72 godzin (art. 33 RODO), a przy wysokim ryzyku powiadomienie osób (art. 34), decyzję podejmuje się z IOD i działem prawnym na podstawie faktów od zespołu. Na końcu analiza bez szukania winnych z konkretnymi działaniami (testy, klasy bazowe, reguły SAST).

Zobacz: sekcja „Gdy coś się wydarzy”.

</details>
