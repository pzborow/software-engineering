# Podstawy

Bezpieczeństwo aplikacji nie jest osobną warstwą, którą dokleja się na końcu projektu. To sposób myślenia przy każdej funkcji: kto może jej użyć, co może pójść źle i co się stanie, jeśli ktoś celowo użyje jej inaczej, niż zakładaliśmy. Ten rozdział wprowadza pojęcia, na których opierają się pozostałe, i pokazuje, jak Django realizuje je w swoich domyślnych ustawieniach.

Przykładem przewodnim tego tutorialu jest API sklepu internetowego w Django i Django REST Framework: klienci zakładają konta, składają zamówienia, wgrywają awatary, używają kuponów, a sklep przyjmuje webhooki od operatora płatności i importuje produkty z plików dostawców.

```text
każdy temat w tym tutorialu:

zasada ogólna          ──►  jak to rozwiązuje Django / DRF  ──►  gdzie ochrona się kończy
(niezależna od          (mechanizm, ustawienia,               (typowe obejścia, błędy
 frameworka)             co trzeba włączyć samemu)             konfiguracji, test lub review)
```

## Myślenie o zagrożeniach

<a id="term-threat-modeling"></a>[Modelowanie zagrożeń](00%20Glossary%20Security.md#threat-modeling) (threat modeling) to systematyczne zastanowienie się, co może pójść źle w projektowanej funkcji, zanim powstanie kod. Nie wymaga specjalistów ani narzędzi. Wystarczą cztery pytania, które spopularyzował Adam Shostack:

1. Co budujemy? Szkic przepływu danych: kto wysyła, co, dokąd i gdzie to jest zapisywane.
2. Co może pójść źle? Tu pomaga lista kontrolna.
3. Co z tym zrobimy? Zabezpieczenie, akceptacja ryzyka albo rezygnacja z funkcji.
4. Czy zrobiliśmy to dobrze? Testy, przegląd, sprawdzenie po wdrożeniu.

Popularną listą kontrolną do pytania drugiego jest <a id="term-stride"></a>[STRIDE](00%20Glossary%20Security.md#stride), opracowane w Microsofcie. Każda litera to kategoria zagrożenia i odpowiadająca jej właściwość bezpieczeństwa:

| Litera | Zagrożenie | Chroniona właściwość | Przykład w sklepie |
|---|---|---|---|
| S | Spoofing, podszywanie się | uwierzytelnienie | ktoś loguje się jako inny klient |
| T | Tampering, modyfikacja danych | integralność | zmiana ceny w żądaniu zamówienia |
| R | Repudiation, wypieranie się | niezaprzeczalność | klient twierdzi, że nie złożył zamówienia, a brak logów |
| I | Information disclosure, ujawnienie | poufność | API zwraca zamówienia innych klientów |
| D | Denial of service, odmowa usługi | dostępność | masowe żądania do wyszukiwarki zatrzymują bazę |
| E | Elevation of privilege, podniesienie uprawnień | autoryzacja | klient nadaje sobie flagę `is_staff` |

Przykład dla nowej funkcji „import produktów z adresu URL podanego przez dostawcę”:

```text
dostawca ──URL──► API sklepu ──GET──► serwer pod URL ──CSV──► parser ──► baza produktów

S: czy tylko zweryfikowany dostawca może zlecić import?          → uprawnienie supplier
T: czy dostawca może zmienić ceny cudzych produktów?             → import tylko jego SKU
I: czy URL może wskazywać na serwer wewnętrzny (SSRF)?           → rozdział 03
D: co, jeśli plik ma 5 GB albo serwer odpowiada bardzo wolno?    → limit rozmiaru i timeout
E: czy CSV może zawierać formuły wykonywane w Excelu księgowości? → escapowanie komórek
```

Pół godziny takiej rozmowy przy planowaniu funkcji znajduje więcej problemów niż tydzień testów po wdrożeniu.

## Zasady projektowe

Trzy zasady wracają w każdym rozdziale.

<a id="term-defense-in-depth"></a>[Defense in depth](00%20Glossary%20Security.md#defense-in-depth) (obrona w głąb): nie polegaj na jednym zabezpieczeniu. Każda warstwa zakłada, że poprzednia może zawieść. Walidacja w formularzu, ograniczenie w bazie, uprawnienia na poziomie obiektu i monitoring działają razem.

<a id="term-least-privilege"></a>[Least privilege](00%20Glossary%20Security.md#least-privilege) (najmniejsze uprawnienia): każdy użytkownik, proces i token ma tylko te uprawnienia, których potrzebuje. Konto bazy aplikacji nie ma prawa `DROP TABLE`, token do webhooków nie ma dostępu do panelu admina, a pracownik obsługi klienta nie widzi danych kart.

<a id="term-secure-by-default"></a>[Secure by default](00%20Glossary%20Security.md#secure-by-default) (bezpieczne ustawienia domyślne): najprostsza droga ma być bezpieczna, a wyłączenie ochrony wymaga świadomej decyzji.

Django jest dobrym przykładem tej ostatniej zasady:

| Ochrona | Domyślnie w Django | Co trzeba zrobić, żeby ją wyłączyć |
|---|---|---|
| escapowanie w szablonach | włączone | `mark_safe`, `\|safe`, `{% autoescape off %}` |
| parametryzacja SQL | każde zapytanie ORM | `raw()`, `extra()`, łączenie tekstu w SQL |
| ochrona CSRF | middleware w nowym projekcie | `@csrf_exempt`, usunięcie middleware |
| ochrona przed clickjackingiem | `X-Frame-Options: DENY` | `@xframe_options_exempt` |
| hashowanie haseł | PBKDF2 z dużą liczbą iteracji | własny hasher albo zapis hasła wprost do pola |
| ciasteczko sesji niedostępne z JS | `SESSION_COOKIE_HTTPONLY = True` | zmiana ustawienia |

Nie wszystko jest jednak bezpieczne domyślnie. `DEBUG = True` w nowym projekcie, `SESSION_COOKIE_SECURE = False`, HSTS wyłączony, a w DRF domyślne uprawnienie to `AllowAny`. Te wartości są wygodne w developmencie, więc na produkcji trzeba je zmienić świadomie. Rozdział 07 omawia je szczegółowo.

## Co może zaatakować napastnik

<a id="term-attack-surface"></a>[Powierzchnia ataku](00%20Glossary%20Security.md#attack-surface) (attack surface) to suma miejsc, przez które napastnik może wprowadzić dane albo wywołać działanie systemu. Im mniejsza, tym mniej trzeba bronić.

W aplikacji Django składają się na nią:

- wszystkie endpointy HTTP, także te zapomniane: stare wersje API, endpointy testowe, `/api/debug/`,
- panel administracyjny pod domyślnym adresem `/admin/`,
- strona błędu z `DEBUG = True`, która pokazuje ustawienia, zmienne i fragmenty kodu,
- upload plików i miejsca, z których te pliki są serwowane,
- webhooki od partnerów i zadania uruchamiane z zewnątrz,
- zależności, czyli cały kod bibliotek, który wykonuje się w procesie aplikacji,
- dostęp do infrastruktury: SSH, konsola chmury, pipeline CI/CD.

Sposoby zmniejszania powierzchni ataku:

```python
# urls.py: tylko to, co potrzebne, i nic więcej na produkcji
urlpatterns = [
    path("api/v2/", include("shop.api.urls")),
    path(env("ADMIN_URL", default="staff-7f3a/"), admin.site.urls),   # nie /admin/
]
if settings.DEBUG:
    urlpatterns += [path("__debug__/", include("debug_toolbar.urls"))]
```

- usuwaj nieużywane endpointy i wersje API, zamiast je „ukrywać”,
- przenieś panel admina pod niestandardowy adres i ogranicz go do VPN albo listy adresów IP na poziomie proxy,
- wyłącz funkcje, których nie używasz: DRF browsable API na produkcji, niepotrzebne formaty odpowiedzi,
- dodawaj zależności świadomie, bo każda poszerza powierzchnię ataku.

## Błąd, który działa dla złej osoby

<a id="term-vulnerability"></a>[Podatność](00%20Glossary%20Security.md#vulnerability) (vulnerability) to błąd, który pozwala komuś osiągnąć coś, na co nie powinien mieć pozwolenia: odczytać cudze dane, zmienić je, wykonać kod albo zablokować usługę. Różnica wobec błędu funkcjonalnego polega na tym, kto go wywołuje i jak:

| | Błąd funkcjonalny | Podatność |
|---|---|---|
| Kto go wywołuje | zwykły użytkownik, przypadkiem | napastnik, celowo |
| Jak jest znajdowany | użytkownicy go zgłaszają | napastnik go szuka i nie zgłasza |
| Skutek | coś nie działa | coś działa, ale dla niewłaściwej osoby |
| Testy | sprawdzają ścieżki szczęśliwe i brzegowe | muszą sprawdzać złośliwe dane i nieuprawnionych użytkowników |

Przykład: endpoint `GET /api/orders/42/` zwraca zamówienie. Działa poprawnie dla właściciela, więc testy funkcjonalne przechodzą. Jeśli zwraca je także każdemu innemu zalogowanemu użytkownikowi, to nie jest usterka, którą ktoś zauważy. To podatność, której nikt nie zgłosi, dopóki ktoś jej nie wykorzysta.

Za bezpieczeństwo odpowiada cały zespół, a nie tylko „ktoś od security”. Programista odpowiada za kod, który pisze i przegląda. Senior dodatkowo za to, żeby bezpieczne rozwiązania były łatwiejsze niż niebezpieczne: wspólne klasy bazowe widoków z poprawnymi uprawnieniami, gotowe helpery, testy w CI. Zespół bezpieczeństwa, jeśli istnieje, wspiera i audytuje, ale nie jest w stanie przejrzeć każdej zmiany.

## Listy najczęstszych problemów

<a id="term-owasp-top-10"></a>[OWASP Top 10](00%20Glossary%20Security.md#owasp-top-10) to publikowana przez fundację OWASP lista najczęstszych i najpoważniejszych kategorii ryzyka w aplikacjach webowych. Wydanie z 2021 roku jest najczęściej cytowane na rozmowach. W 2025 roku ukazała się aktualizacja, w której wyżej znalazły się błędy konfiguracji i łańcuch dostaw. Dla API istnieje osobna lista, OWASP API Security Top 10 (wydanie 2023), bo API mają inne typowe problemy niż strony renderowane po stronie serwera.

Jak Django odnosi się do kategorii OWASP Top 10 (2021):

| Kategoria | Co robi Django | Co zostaje po stronie programisty |
|---|---|---|
| A01 Broken Access Control | `login_required`, uprawnienia, DRF `permission_classes` | uprawnienia na poziomie obiektu, filtrowanie querysetów (rozdział 05) |
| A02 Cryptographic Failures | hashowanie haseł, `signing`, HTTPS przez ustawienia | szyfrowanie wrażliwych pól, zarządzanie kluczami (rozdział 06) |
| A03 Injection | ORM, escapowanie szablonów | surowy SQL, `mark_safe`, `subprocess` (rozdziały 02 i 03) |
| A04 Insecure Design | nic | modelowanie zagrożeń, limity biznesowe |
| A05 Security Misconfiguration | `check --deploy` | `DEBUG`, `ALLOWED_HOSTS`, nagłówki, CORS (rozdział 07) |
| A06 Vulnerable Components | szybkie wydania łatek | aktualizacje, skanowanie zależności (rozdział 08) |
| A07 Authentication Failures | sesje, walidatory haseł, reset hasła | limity logowania, MFA, JWT (rozdział 04) |
| A08 Integrity Failures | JSON zamiast pickle w sesjach | deserializacja, bezpieczeństwo CI/CD (rozdziały 08 i 09) |
| A09 Logging Failures | `logging`, filtry danych wrażliwych | co logować, alerty (rozdziały 09 i 10) |
| A10 SSRF | nic | walidacja adresów wychodzących (rozdział 03) |

Lista API Security Top 10 (2023) przesuwa akcenty. Na pierwszym miejscu jest BOLA, czyli brak autoryzacji na poziomie obiektu, na trzecim autoryzacja na poziomie właściwości (mass assignment i nadmiarowe dane w odpowiedziach), a na czwartym nieograniczone zużycie zasobów. To dokładnie te miejsca, w których DRF nie chroni automatycznie i które omawiają rozdziały 05 i 09.

## Co zapamiętać

- Modelowanie zagrożeń to cztery pytania zadane przed napisaniem kodu, a STRIDE to lista kontrolna do pytania „co może pójść źle”.
- Defense in depth, least privilege i secure by default wracają w każdym temacie.
- Django jest w dużej mierze bezpieczne domyślnie, ale `DEBUG`, ciasteczka `Secure`, HSTS i `AllowAny` w DRF trzeba zmienić świadomie.
- Powierzchnię ataku zmniejsza się, usuwając nieużywane endpointy, ukrywając i ograniczając admina oraz ostrożnie dodając zależności.
- Podatność to błąd, który działa dla niewłaściwej osoby. Testy muszą sprawdzać napastnika, a nie tylko użytkownika.
- OWASP Top 10 i API Security Top 10 pokazują, gdzie kończy się ochrona frameworka: autoryzacja, konfiguracja, SSRF, zużycie zasobów.

## Pytania sprawdzające

### 1. Czym jest modelowanie zagrożeń i jak używać STRIDE przy projektowaniu nowej funkcji?

<details>
<summary>Odpowiedź</summary>

To systematyczne zastanowienie się przed napisaniem kodu, co może pójść źle. Opiera się na czterech pytaniach: co budujemy, co może pójść źle, co z tym zrobimy i czy zrobiliśmy to dobrze. STRIDE to lista kontrolna do drugiego pytania: podszywanie się, modyfikacja danych, wypieranie się, ujawnienie informacji, odmowa usługi i podniesienie uprawnień. Każdą kategorię sprawdza się dla przepływu danych funkcji, np. przy imporcie z URL: kto może zlecić import, czy URL może wskazać serwer wewnętrzny, co przy pliku 5 GB.

Zobacz: sekcja „Myślenie o zagrożeniach”.

</details>

### 2. Co oznaczają defense in depth, least privilege i secure by default? Jak te zasady widać w domyślnych ustawieniach Django?

<details>
<summary>Odpowiedź</summary>

Defense in depth oznacza wiele niezależnych warstw zabezpieczeń, z których każda zakłada, że poprzednia może zawieść. Least privilege to minimalne uprawnienia dla użytkowników, procesów i tokenów. Secure by default to bezpieczna najprostsza droga, a wyłączenie ochrony wymaga świadomej decyzji. W Django domyślnie włączone są escapowanie szablonów, parametryzacja ORM, CSRF, `X-Frame-Options: DENY`, PBKDF2 i `HttpOnly` dla sesji. Wyjątkami są `DEBUG = True`, `SESSION_COOKIE_SECURE = False`, wyłączony HSTS i `AllowAny` w DRF.

Zobacz: sekcja „Zasady projektowe”.

</details>

### 3. Czym jest powierzchnia ataku i jak ją zmniejszać w aplikacji webowej (endpointy, panel admina, tryb debug)?

<details>
<summary>Odpowiedź</summary>

To suma miejsc, przez które napastnik może wprowadzić dane lub wywołać działanie: endpointy (także zapomniane), panel admina, strona błędu w trybie debug, upload, webhooki, zależności i infrastruktura. Zmniejsza się ją, usuwając nieużywane endpointy i stare wersje API, przenosząc admina pod niestandardowy adres i ograniczając go do VPN lub listy IP, wyłączając na produkcji `DEBUG`, debug toolbar i browsable API oraz ostrożnie dodając zależności.

Zobacz: sekcja „Co może zaatakować napastnik”.

</details>

### 4. Czym różni się podatność od błędu funkcjonalnego i kto w zespole odpowiada za bezpieczeństwo?

<details>
<summary>Odpowiedź</summary>

Błąd funkcjonalny wywołuje przypadkiem zwykły użytkownik i zwykle go zgłasza. Podatność napastnik szuka celowo i wykorzystuje: coś działa, ale dla niewłaściwej osoby, np. endpoint zwraca zamówienie każdemu zalogowanemu. Testy muszą więc sprawdzać złośliwe dane i nieuprawnionych użytkowników. Za bezpieczeństwo odpowiada cały zespół: programista za kod i review, senior za to, żeby bezpieczne rozwiązania były najłatwiejsze (wspólne klasy bazowe, helpery, testy w CI), a zespół bezpieczeństwa wspiera i audytuje.

Zobacz: sekcja „Błąd, który działa dla złej osoby”.

</details>

### 5. Czym jest OWASP Top 10 i OWASP API Security Top 10? Które kategorie Django łagodzi domyślnie, a które zostają po stronie programisty?

<details>
<summary>Odpowiedź</summary>

To publikowane przez OWASP listy najczęstszych kategorii ryzyka: dla aplikacji webowych (najczęściej cytowane wydanie 2021, aktualizacja 2025) i dla API (2023). Django domyślnie łagodzi wstrzykiwanie (ORM, escapowanie), część problemów kryptograficznych (hashowanie haseł), część błędów uwierzytelniania i konfiguracji (`check --deploy`). Po stronie programisty zostają autoryzacja na poziomie obiektu (BOLA, pierwsze miejsce w liście API), mass assignment, niebezpieczny projekt, SSRF, zależności, zużycie zasobów i logowanie.

Zobacz: sekcja „Listy najczęstszych problemów”.

</details>
