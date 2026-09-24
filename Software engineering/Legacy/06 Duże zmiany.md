# Duże zmiany

Techniki z rozdziałów 04 i 05 poprawiają kod w małej skali: funkcję, klasę, moduł. Czasem trzeba jednak wymienić coś dużego: cały moduł fakturowania, bibliotekę ORM, framework albo sposób integracji z KSeF. Robienie tego na długiej gałęzi, którą scala się po trzech miesiącach, kończy się konfliktami i ryzykownym wdrożeniem. Ten rozdział opisuje techniki, dzięki którym duża zmiana składa się z wielu małych, a każda z nich trafia na produkcję.

```text
technika                 odpowiada na pytanie
strangler fig            jak zastąpić cały moduł, fragment po fragmencie?
branch by abstraction    jak wymienić komponent używany w wielu miejscach bez długiej gałęzi?
Mikado Method            od czego zacząć, gdy nie wiadomo, co jeszcze trzeba zmienić?
feature toggles          jak wdrożyć nowy kod, ale włączyć go później i dla wybranych?
parallel run             skąd wiadomo, że nowa implementacja daje te same wyniki co stara?
```

## Nowe obrasta stare

<a id="term-strangler-fig"></a>[Strangler fig](00%20Glossary%20Legacy.md#strangler-fig) to wzorzec opisany przez Martina Fowlera w 2004 roku, nazwany od figowca dusiciela. Roślina kiełkuje na starym drzewie, stopniowo je obrasta i w końcu całkowicie zastępuje. W oprogramowaniu nowy system powstaje obok starego i przejmuje kolejne funkcje, aż stary można wyłączyć.

Kluczowy element to <a id="term-interception-point"></a>[punkt przechwycenia](00%20Glossary%20Legacy.md#interception-point): miejsce, w którym decyduje się, czy żądanie obsłuży stary, czy nowy kod. Może to być funkcja-fasada w kodzie, router HTTP, reverse proxy albo konsument kolejki.

```python
# billing/invoices.py: fasada w miejscu starej funkcji
def generate_invoice(order_id):
    order = order_summary(order_id)                         # lekki odczyt: kraj, typ klienta, kategorie
    if new_billing_handles(order):
        return new_billing.InvoiceService.default().generate(order_id)
    return _legacy_generate_invoice(order_id)               # 400 starych linii, bez zmian


def new_billing_handles(order) -> bool:
    # przejmowanie etapami: najpierw najprostsze przypadki, potem kolejne
    return (
        order.customer_country == "PL"
        and order.customer_type == "B2C"
        and order.categories <= {"electronics", "books"}
    )
```

Etapy wymiany modułu fakturowania:

```text
etap 1  fasada przed starym kodem                   generate_invoice → _legacy_generate_invoice (100%)
etap 2  nowy moduł obsługuje klientów B2C z Polski  nowy: 60% faktur, stary: 40%
etap 3  nowy moduł obsługuje też żywność            nowy: 75%, stary: 25%
etap 4  nowy moduł obsługuje B2B i UE               nowy: 100%, stary: 0% (nadal w kodzie)
etap 5  usunięcie starego kodu i fasady             tylko nowy moduł
```

Każdy etap to osobne wdrożenie, które można cofnąć, zmieniając warunek w fasadzie. Najczęstszym błędem jest pominięcie etapu 5: stary kod zostaje „na wszelki wypadek” i system ma na stałe dwie implementacje. Warto zaplanować usunięcie starego kodu jako osobne zadanie z terminem od samego początku.

## Wymiana pod abstrakcją

<a id="term-branch-by-abstraction"></a>[Branch by abstraction](00%20Glossary%20Legacy.md#branch-by-abstraction) to technika opisana przez Paula Hammanta i spopularyzowana przez Jeza Humble'a w kontekście ciągłego dostarczania. Pozwala wymienić komponent używany w wielu miejscach bez tworzenia długiej gałęzi w gicie. „Gałąź” powstaje w kodzie, jako abstrakcja z dwiema implementacjami, a nie w systemie kontroli wersji.

Przykład: stare obliczanie podatku jest wywoływane z faktur, z koszyka, z raportów i z eksportu do księgowości. Nowe ma obsłużyć stawki VAT z zewnętrznego serwisu, a nie z kodu.

```python
# krok 1: abstrakcja nad tym, czego używają wywołujący
class TaxCalculator(Protocol):
    def vat_rate(self, category: str, customer: dict, on: date) -> Decimal: ...


# krok 2: stara logika za abstrakcją, bez zmian w działaniu
class LegacyTaxCalculator:
    def vat_rate(self, category, customer, on):
        return Decimal(str(vat_rate_for(category, customer)))        # stara funkcja


# krok 3: wszyscy wywołujący przechodzą na abstrakcję, jeden po drugim, każdy w osobnym wdrożeniu
tax: TaxCalculator = LegacyTaxCalculator()


# krok 4: nowa implementacja, rozwijana w głównej gałęzi, nieużywana na produkcji
class RatesServiceTaxCalculator:
    def __init__(self, client: RatesClient):
        self._client = client

    def vat_rate(self, category, customer, on):
        if customer["type"] == "B2B" and customer["country"] != "PL":
            return Decimal("0")
        return self._client.rate(category=category, country="PL", on=on)


# krok 5: przełączenie (flaga), krok 6: usunięcie starej implementacji, krok 7: ewentualnie abstrakcji
tax = RatesServiceTaxCalculator(RatesClient(settings.RATES_URL)) if flags.enabled("new_tax") else LegacyTaxCalculator()
```

| | Długa gałąź w gicie | Branch by abstraction |
|---|---|---|
| Gdzie żyje nowy kod | na osobnej gałęzi przez tygodnie | w głównej gałęzi, od pierwszego dnia |
| Konflikty | narastają, scalenie na końcu jest bolesne | brak, bo wszyscy pracują na tym samym kodzie |
| Wdrażanie | jedno duże na końcu | wiele małych, nowy kod wyłączony |
| Cofnięcie | rewert dużego scalenia | przełączenie flagi |
| Koszt | niski na starcie, wysoki na końcu | abstrakcja i dwie implementacje przez jakiś czas |

## Graf zależności zmiany

Duża zmiana często wygląda prosto, dopóki się jej nie zacznie. „Zamieńmy bibliotekę do PDF” okazuje się wymagać zmiany szablonów, które wymagają nowej wersji Pythona, która wymaga aktualizacji Django, która psuje trzy inne moduły. Zespół po tygodniu ma gałąź z setkami zmian, które się nie kompilują i których nie da się wdrożyć.

<a id="term-mikado-method"></a>[Mikado Method](00%20Glossary%20Legacy.md#mikado-method), opisana przez Olę Ellnestama i Daniela Brolunda, odpowiada na ten problem prostą procedurą:

1. Zapisz cel na środku kartki, np. „PDF generowany przez WeasyPrint”.
2. Spróbuj zrobić zmianę wprost, w najprostszy sposób.
3. Gdy coś się psuje, zapisz na kartce, co trzeba by zrobić wcześniej (warunek wstępny), i połącz to z celem.
4. Cofnij wszystkie zmiany (`git reset --hard`). To najważniejszy krok.
5. Wybierz liść grafu, czyli warunek bez własnych warunków, i powtórz próbę dla niego.
6. Gdy liść da się zrobić bez psucia czegokolwiek, zrób go, zatwierdź, wdróż i skreśl na grafie.
7. Powtarzaj, aż cel stanie się liściem.

```text
CEL: PDF generowany przez WeasyPrint
├── szablony faktur w HTML zamiast RML
│   └── Jinja2 w module billing                          ✓ zrobione i wdrożone
└── render_pdf przyjmuje dane, a nie obiekty z bazy
    └── wydziel InvoiceDocument jako DTO                 ← liść, następny krok
```

Cofanie zmian po każdej nieudanej próbie wydaje się marnotrawstwem, ale jest istotą metody. Kod zawsze pozostaje w stanie gotowym do wdrożenia, a wiedza o zależnościach zostaje na grafie. Każdy liść to mała, bezpieczna zmiana, którą można wdrożyć od razu.

## Wdrożenie osobno od włączenia

<a id="term-feature-toggle"></a>[Feature toggle](00%20Glossary%20Legacy.md#feature-toggle) (flaga funkcji) to przełącznik w konfiguracji albo w serwisie flag, który decyduje w czasie działania, czy nowy kod jest aktywny. Dzięki niemu wdrożenie (kod trafia na produkcję) jest oddzielone od włączenia (użytkownicy zaczynają go używać).

Pete Hodgson opisał cztery rodzaje flag, które różnią się czasem życia:

| Rodzaj | Cel | Czas życia |
|---|---|---|
| release toggle | ukrycie niedokończonej funkcji, stopniowe włączanie | dni lub tygodnie |
| experiment toggle | test A/B | tygodnie |
| ops toggle | wyłącznik awaryjny, np. wyłączenie KSeF przy awarii | długo, czasem na stałe |
| permission toggle | funkcja dla wybranych klientów lub planów | długo |

Przy wymianie legacy używa się głównie release toggles: nowy moduł fakturowania włącza się najpierw dla zespołu, potem dla 5 procent zamówień, potem dla wszystkich.

```python
def generate_invoice(order_id):
    if flags.enabled("new_billing", key=order_id, percent=5):     # stały podział po order_id
        return new_billing.InvoiceService.default().generate(order_id)
    return _legacy_generate_invoice(order_id)
```

Flagi łatwo stają się długiem. Każda flaga podwaja liczbę ścieżek w kodzie, a zapomniane flagi zostają na lata. Knight Capital w 2012 roku stracił 440 milionów dolarów w 45 minut, między innymi przez ponowne użycie nazwy starej flagi, która uruchomiła martwy kod na jednym z serwerów. Zasady, które ograniczają ryzyko:

- każda flaga release ma właściciela i datę usunięcia, zapisaną w kodzie albo w serwisie flag,
- usunięcie flagi to zadanie planowane razem z jej dodaniem,
- test w CI albo linter ostrzega o flagach po terminie,
- liczba aktywnych flag jest monitorowana i ma limit,
- nazw flag nie używa się ponownie.

```python
FLAGS = {
    "new_billing": Flag(owner="team-billing", kind="release", remove_by=date(2026, 12, 31)),
}

def test_no_expired_release_flags():
    expired = [n for n, f in FLAGS.items() if f.kind == "release" and f.remove_by < date.today()]
    assert not expired, f"Flagi po terminie: {expired}"
```

## Stara i nowa naraz

Testy charakteryzujące sprawdzają przypadki, które ktoś przygotował. Produkcja ma przypadki, o których nikt nie pomyślał. <a id="term-parallel-run"></a>[Parallel run](00%20Glossary%20Legacy.md#parallel-run) polega na tym, że dla prawdziwych żądań uruchamia się obie implementacje, porównuje wyniki, a użytkownikowi zwraca wynik starej. Różnice trafiają do logów i metryk.

GitHub opisał ten wzorzec w bibliotece Scientist dla Rubiego. W Pythonie istnieje jej odpowiednik `laboratory`, ale prosta wersja mieści się w kilkunastu liniach:

```python
def invoice_total(order) -> Decimal:
    old = legacy_invoice_total(order)
    try:
        new = new_billing.total(order)
        if new != old:
            log.warning("invoice_total mismatch", extra={"order_id": order.id, "old": str(old), "new": str(new)})
            MISMATCHES.labels(experiment="invoice_total").inc()
        else:
            MATCHES.labels(experiment="invoice_total").inc()
    except Exception:
        log.exception("new invoice_total failed", extra={"order_id": order.id})
        ERRORS.labels(experiment="invoice_total").inc()
    return old                                       # użytkownik zawsze dostaje wynik starej implementacji
```

Zasady:

- porównuje się tylko funkcje bez efektów ubocznych albo uruchamia nową w trybie bez zapisu. Nie wolno dwa razy wysłać faktury do KSeF ani dwa razy obciążyć karty,
- błąd lub wolne działanie nowej implementacji nie może wpływać na użytkownika: wyjątki są łapane, a przy dużym ruchu nową wywołuje się asynchronicznie albo dla próbki żądań,
- porównanie musi uwzględniać różnice, które nie są błędami: kolejność elementów, formatowanie, zaokrąglenia o ułamki grosza, uzgodnione jako dopuszczalne,
- eksperyment kończy się, gdy przez ustalony okres (np. dwa tygodnie i jedno zamknięcie miesiąca) nie ma różnic. Wtedy przełącza się flagę.

Odmianą parallel run na poziomie infrastruktury jest shadow traffic: kopia ruchu produkcyjnego jest wysyłana do nowego serwisu, którego odpowiedzi są porównywane, ale nie wracają do użytkownika. Wspiera to wiele proxy i service meshy, np. mirroring w Envoy albo Istio.

## Co zapamiętać

- Strangler fig zastępuje moduł fragment po fragmencie przez punkt przechwycenia. Usunięcie starego kodu planuje się od początku.
- Branch by abstraction tworzy gałąź w kodzie, a nie w gicie: abstrakcja, stara implementacja za nią, nowa obok, przełączenie, usunięcie.
- Mikado Method buduje graf warunków wstępnych dużej zmiany, cofa nieudane próby i realizuje liście jako małe, wdrażalne kroki.
- Feature toggles oddzielają wdrożenie od włączenia. Każda flaga release ma właściciela i datę usunięcia, bo inaczej staje się długiem.
- Parallel run porównuje starą i nową implementację na prawdziwym ruchu, zwracając wynik starej, bez podwójnych efektów ubocznych.

## Pytania sprawdzające

### 23. Czym jest strangler fig i jak krok po kroku zastępować stary moduł nowym?

<details>
<summary>Odpowiedź</summary>

To wzorzec Martina Fowlera nazwany od figowca dusiciela: nowy system powstaje obok starego i przejmuje kolejne funkcje, aż stary można wyłączyć. Kluczowy jest punkt przechwycenia (fasada w kodzie, router, proxy), który decyduje, czy żądanie obsłuży stary, czy nowy kod. Kolejne kroki to fasada przed starym kodem, przejmowanie przypadków od najprostszych (np. B2C z Polski), rozszerzanie zakresu etapami, każdy jako osobne, odwracalne wdrożenie, i na końcu usunięcie starego kodu i fasady, zaplanowane od początku.

Zobacz: sekcja „Nowe obrasta stare”.

</details>

### 24. Czym jest branch by abstraction i czym różni się od długiej gałęzi w gicie?

<details>
<summary>Odpowiedź</summary>

To technika (Paul Hammant, Jez Humble) wymiany komponentu używanego w wielu miejscach: wprowadza się abstrakcję (np. `TaxCalculator`), przenosi za nią starą implementację, przełącza wywołujących na abstrakcję jeden po drugim, rozwija nową implementację w głównej gałęzi, przełącza flagą, a na końcu usuwa starą. W odróżnieniu od długiej gałęzi w gicie nowy kod żyje w głównej gałęzi od pierwszego dnia, nie ma narastających konfliktów, wdrożenia są małe, a cofnięcie to przełączenie flagi. Kosztem jest utrzymywanie abstrakcji i dwóch implementacji przez pewien czas.

Zobacz: sekcja „Wymiana pod abstrakcją”.

</details>

### 25. Czym jest Mikado Method i jak pomaga zaplanować zmianę, której zależności nie są znane?

<details>
<summary>Odpowiedź</summary>

To metoda Ellnestama i Brolunda: zapisujesz cel, próbujesz zrobić zmianę wprost, a gdy coś się psuje, zapisujesz warunek wstępny na grafie i cofasz wszystkie zmiany. Potem powtarzasz próbę dla liści grafu. Liść, który da się zrobić bez psucia czegokolwiek, realizujesz, wdrażasz i skreślasz, aż cel stanie się liściem. Cofanie jest istotą metody: kod zawsze nadaje się do wdrożenia, wiedza o zależnościach zostaje na grafie, a duża zmiana rozpada się na małe, bezpieczne kroki.

Zobacz: sekcja „Graf zależności zmiany”.

</details>

### 26. Jak używać feature toggles przy wymianie starego kodu i jak nie pozwolić, żeby same stały się długiem?

<details>
<summary>Odpowiedź</summary>

Flagi oddzielają wdrożenie od włączenia: nowy kod trafia na produkcję wyłączony, potem włącza się go dla zespołu, części ruchu (stabilnie po ID) i wszystkich. Przy legacy używa się głównie release toggles (według Hodgsona są też experiment, ops i permission). Żeby nie stały się długiem, każda flaga release ma właściciela i datę usunięcia, usunięcie jest planowane razem z dodaniem, CI ostrzega o flagach po terminie, liczba flag jest monitorowana, a nazw nie używa się ponownie. Przestrogą jest Knight Capital z 2012 roku.

Zobacz: sekcja „Wdrożenie osobno od włączenia”.

</details>

### 27. Czym jest równoległe uruchamianie (parallel run, shadow traffic) i jak porównać wyniki starej i nowej implementacji na produkcji?

<details>
<summary>Odpowiedź</summary>

Parallel run uruchamia obie implementacje dla prawdziwych żądań, porównuje wyniki, loguje i zlicza różnice, a użytkownikowi zwraca wynik starej (wzorzec biblioteki Scientist GitHuba, w Pythonie `laboratory`). Zasady: tylko funkcje bez efektów ubocznych albo nowa w trybie bez zapisu, błędy i opóźnienia nowej nie mogą dotknąć użytkownika, dopuszczalne różnice (kolejność, zaokrąglenia) są uzgodnione, a eksperyment kończy się po okresie bez różnic. Shadow traffic to wersja infrastrukturalna: kopia ruchu idzie do nowego serwisu przez proxy (mirroring w Envoy lub Istio).

Zobacz: sekcja „Stara i nowa naraz”.

</details>
