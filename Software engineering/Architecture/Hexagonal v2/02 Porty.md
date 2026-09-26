# Porty

Skoro importy wskazują do rdzenia, czas zobaczyć, jak rdzeń wyraża swoje potrzeby: przez porty. Zdefiniujemy je dla „Rowerka”: wejściowy StartRental oraz wyjściowe RentalRepository i PaymentGateway, raz jako ABC, raz jako Protocol, z interfejsami należącymi do rdzenia.

```text
Adapter HTTP --> [StartRental] RDZEŃ [RentalRepository] <-- Adapter SQL
                                 [PaymentGateway]  <-- Adapter płatności
```

## Czym jest port

[Port](00%20Glosariusz.md#port) to interfejs należący do [rdzenia](00%20Glosariusz.md#rdzeń), który opisuje jedną rozmowę rdzenia ze światem zewnętrznym, w języku domeny i bez śladu technologii. Rdzeń mówi, czego potrzebuje albo co oferuje; adapter decyduje, jak to zrobić.

Port ma dwa końce. Po jednej stronie stoi rdzeń, po drugiej adapter, a który z nich wywołuje, a który implementuje, zależy od kierunku rozmowy. Importy i tak wskazują do środka, zgodnie z [zasadą odwrócenia zależności](00%20Glosariusz.md#zasada-odwrócenia-zależności).

W „Rowerku” porty są trzy. `StartRental` to port wejściowy (świat wywołuje rdzeń), a jego rolę pełni sam [przypadek użycia](00%20Glosariusz.md#przypadek-użycia). `RentalRepository` i nowy `PaymentGateway` to porty wyjściowe: to rdzeń woła bazę i bramkę płatności.

```python
# core/ports.py
class PaymentGateway(Protocol):
    def charge(self, user_id: str, amount: Money) -> None: ...
```

Sygnatura nie wspomina Stripe'a, HTTP ani tokenów karty. Mówi tylko: „obciąż użytkownika kwotą”. Typy w portach są typami rdzenia (`Money`, `Rental`), nigdy modelami ORM czy DTO dostawcy.

```text
router → StartRental → RentalRepository ← SqlAlchemyRentalRepository

(osobno) przypadek użycia zwrotu → PaymentGateway ← adapter bramki
```

Opłatę pobiera dopiero zwrot roweru, więc z `PaymentGateway` skorzysta późniejszy przypadek użycia, nie `StartRental`.

Konsekwencja: port jest granicą, którą można podstawić fake'iem w teście albo wymienić adapter bez ruszania logiki. Kształt portu wyznacza potrzeba rdzenia, a nie możliwości technologii.

## Porty wejściowe i wyjściowe

[Port wejściowy](00%20Glosariusz.md#port-wejściowy-driving) (driving) służy do sterowania rdzeniem: adapter po stronie świata (router, konsument kolejki, CLI) wywołuje go, a implementuje go rdzeń. [Port wyjściowy](00%20Glosariusz.md#port-wyjściowy-driven) (driven) działa odwrotnie: to rdzeń woła port, a implementuje go adapter, który rozmawia z bazą, bramką płatności czy SMS-ami.

W „Rowerku” wygląda to tak: `StartRental` jest portem wejściowym i implementuje go sam przypadek użycia. `RentalRepository` i `PaymentGateway` są portami wyjściowymi, więc implementują je adaptery, np. `SqlAlchemyRentalRepository`.

```text
wejście:  adapter (router) ───▶ StartRental (port + implementacja w rdzeniu)
wyjście:  StartRental ───▶ RentalRepository ◀─── SqlAlchemyRentalRepository
```

Strzałki wywołań w obu przypadkach biegną „od inicjatora”, ale zależności importów zawsze wskazują do rdzenia. Adapter wejściowy importuje port rdzenia; adapter wyjściowy importuje port, by go zaimplementować.

| | wejściowy (driving) | wyjściowy (driven) |
|---|---|---|
| Kto wywołuje | adapter | rdzeń |
| Kto implementuje | rdzeń | adapter |
| Przykład | `StartRental` | `RentalRepository` |
| W teście | wywołujesz go wprost | podstawiasz fake |

Konsekwencja: te dwie strony testuje się inaczej. Port wejściowy wywołujesz z testu jak zwykły obiekt, a porty wyjściowe zastępujesz fake'ami wstrzykniętymi do konstruktora.

## Port jako klasa ABC

Port w wersji ABC to [klasa abstrakcyjna](00%20Glosariusz.md#klasa-abstrakcyjna-abc) (dziedziczy po `abc.ABC`, a jej operacje to metody z `@abstractmethod`) bez stanu i bez logiki. Leży w rdzeniu i opisuje rozmowę językiem domeny.

```python
# core/ports.py
class RentalRepository(ABC):
    @abstractmethod
    def add(self, rental: Rental) -> None: ...

    @abstractmethod
    def active_for_user(self, user_id: str) -> Rental | None: ...

# infra/sqlalchemy_rentals.py
class SqlAlchemyRentalRepository(RentalRepository):
    def __init__(self, session: Session) -> None: ...
    def add(self, rental: Rental) -> None: ...
```

Mechanizm: adapter jawnie dziedziczy po porcie, czyli stosuje [typowanie nominalne](00%20Glosariusz.md#typowanie-nominalne) (zgodność wynika z deklaracji w kodzie, nie z kształtu klasy). Próba `RentalRepository()` albo instancjonowania adaptera z pominiętą metodą kończy się `TypeError` już przy tworzeniu obiektu, a nie dopiero przy pierwszym wywołaniu.

Zasady: metody portu przyjmują i zwracają typy domeny (`Rental`, `Money`), nigdy `Session` czy wiersze ORM. Nie dodawaj konstruktora ani stanu; port jest kontraktem, nie klasą bazową do współdzielenia kodu.

Konsekwencja: import `SqlAlchemyRentalRepository` wskazuje na `core.ports`, więc kierunek zależności zostaje zachowany. Ceną jest jawne sprzężenie adaptera z klasą rdzenia; alternatywę bez niego omawia sekcja o zaletach `Protocol`.

## Protocol zamiast ABC

`typing.Protocol` pozwala zdefiniować port bez zmuszania adaptera do dziedziczenia: wystarczy, że klasa ma metody o pasujących sygnaturach. Główna zaleta to brak sprzężenia adaptera z samym portem, a cena to późniejsze wykrywanie błędów.

Mechanizm to [typowanie strukturalne](00%20Glosariusz.md#typowanie-strukturalne): zgodność klasy z interfejsem wynika z jej kształtu, a nie z deklaracji w kodzie. Sprawdza ją type checker (mypy, pyright), nie interpreter. Dlatego `StripePaymentGateway` jest poprawnym `PaymentGateway`, choć nie importuje portu ani po nim nie dziedziczy. Nadal importuje `Money` z rdzenia, bo tego typu wymaga sygnatura.

```python
# core/ports.py
class PaymentGateway(Protocol):
    def charge(self, user_id: str, amount: Money) -> None: ...

# infra/stripe_gateway.py  (bez dziedziczenia po porcie)
class StripePaymentGateway:
    def charge(self, user_id: str, amount: Money) -> None: ...
```

Zyskujesz trzy rzeczy:

- Adapter nie zależy od klasy portu, więc port można zmienić lub podzielić bez edycji nagłówków adapterów; zależność od typów domenowych zostaje.
- Istniejące klasy, także z bibliotek, pasują do portu bez klasy pośredniczącej, o ile mają zgodne sygnatury.
- Fake w teście to zwykła klasa bez dziedziczenia. Musi mieć wszystkie metody portu, więc port powinien być wąski: `PaymentGateway` ma jedną metodę, a fake to trzy linie.

| | ABC | Protocol |
|---|---|---|
| Zgodność | nominalna (dziedziczenie) | strukturalna (kształt) |
| Błąd niepełnej implementacji | `TypeError` przy tworzeniu obiektu | raport type checkera |
| Sprzężenie adaptera z portem | jawny import i dziedziczenie | brak |

Konsekwencja: bez type checkera w CI `Protocol` nie chroni przed niczym, bo literówka w nazwie metody wyjdzie dopiero w czasie działania. `@runtime_checkable` sprawdza tylko obecność nazw metod, nie sygnatury.

## Właściciel interfejsu portu

Właścicielem portu jest rdzeń. Interfejs leży w pakiecie rdzenia, jest pisany w języku domeny i zmienia się, gdy rdzeń potrzebuje czegoś nowego, a nie gdy zmienia się technologia.

Mechanizm to odwrócenie zależności. Własność oznacza tu dwie rzeczy: gdzie plik leży i czyja potrzeba kształtuje sygnatury. Gdy port leży w `core/ports.py`, adapter importuje rdzeń, a rdzeń nie zna adaptera. Gdy interfejs należy do adaptera, rdzeń musi go importować i znów zależy od infrastruktury.

```text
# poza kanonem: własność interfejsu
źle:   core/use_cases.py  -->  infra/stripe_gateway.py   (interfejs w adapterze)
dobrze: infra/stripe_gateway.py  -->  core/ports.py       (interfejs w rdzeniu)
```

Drugi wymiar to kształt. Interfejs wyprowadzony z SDK dostawcy wymusza jego typy i słownictwo w rdzeniu. Dlatego `PaymentGateway.charge` przyjmuje `Money` i `user_id`, a nie obiekt `PaymentIntent` z Stripe. To adapter tłumaczy język domeny na język dostawcy.

| | Port w rdzeniu | Interfejs w adapterze |
|---|---|---|
| Kierunek importów | adapter → rdzeń | rdzeń → adapter |
| Kształt wyznacza | potrzeba przypadku użycia | API dostawcy |
| Wymiana technologii | nowy adapter, rdzeń bez zmian | zmiana także w rdzeniu |

Konsekwencja: to samo dotyczy `Protocol`. Nawet jeśli adapter go nie importuje, definicja zostaje w `core/ports.py`, bo własność nie zależy od sposobu sprawdzania zgodności. Gotowa biblioteka z własnym interfejsem nie staje się portem. Opakowujesz ją adapterem, który spełnia port rdzenia.

## Co zapamiętać

- Port to interfejs rdzenia opisujący jedną rozmowę ze światem w języku domeny; jego kształt wyznacza potrzeba rdzenia, nie technologia.
- Port wejściowy jest wywoływany przez świat i implementowany przez rdzeń; port wyjściowy jest wywoływany przez rdzeń i implementowany przez adapter.
- Port jako ABC to bezstanowa klasa w rdzeniu z metodami @abstractmethod, po której adapter jawnie dziedziczy, a Python odmawia utworzenia adaptera z niepełną implementacją.
- Protocol usuwa z adaptera import i dziedziczenie po porcie oraz upraszcza fake'i, ale kontrolę zgodności przenosi z interpretera na type checker.
- Port należy do rdzenia, zarówno lokalizacją pliku, jak i kształtem, a adapter tłumaczy go na język technologii.

## Pytania sprawdzające

### 6. Czym jest port w architekturze heksagonalnej?

<details>
<summary>Odpowiedź</summary>

Port to interfejs należący do rdzenia, który opisuje jedną rozmowę rdzenia ze światem zewnętrznym w języku domeny, bez szczegółów technologii. Rdzeń określa, czego potrzebuje lub co oferuje, a adapter po drugiej stronie portu decyduje, jak to zrealizować. Dzięki temu zależności wskazują do rdzenia, a adapter można wymienić lub zastąpić fake'iem w teście bez zmian w logice.

Zobacz: [sekcja „Czym jest port”](#czym-jest-port).

</details>

### 7. Czym różnią się porty wejściowe (driving) od wyjściowych (driven)?

<details>
<summary>Odpowiedź</summary>

Port wejściowy (driving) to interfejs, przez który świat zewnętrzny wywołuje rdzeń; implementuje go rdzeń (przypadek użycia), a woła adapter, np. router HTTP. Port wyjściowy (driven) to interfejs, przez który rdzeń wywołuje świat zewnętrzny; definiuje go rdzeń, a implementuje adapter, np. repozytorium SQL. Różni je więc kierunek wywołania i to, kto implementuje interfejs, a nie położenie w kodzie: oba należą do rdzenia.

Zobacz: [sekcja „Porty wejściowe i wyjściowe”](#porty-wejściowe-i-wyjściowe), [sekcja „Czym jest port”](#czym-jest-port).

</details>

### 8. Jak zdefiniować port w Pythonie za pomocą abc.ABC?

<details>
<summary>Odpowiedź</summary>

Port definiujesz jako klasę dziedziczącą po abc.ABC, w której każda operację oznaczasz dekoratorem @abstractmethod, a całość umieszczasz w module rdzenia (core/ports.py). Adapter jawnie dziedziczy po takiej klasie i musi zaimplementować wszystkie metody abstrakcyjne, inaczej Python nie pozwoli utworzyć jego instancji. Kontrakt jest więc egzekwowany w czasie wykonania, a nazwa portu jest widoczna w hierarchii klas adaptera.

Zobacz: [sekcja „Port jako klasa ABC”](#port-jako-klasa-abc).

</details>

### 9. Jakie zalety ma typing.Protocol względem ABC przy definiowaniu portów?

<details>
<summary>Odpowiedź</summary>

Protocol pozwala adapterowi spełnić port samym kształtem metod, bez importu portu i dziedziczenia po nim. Dzięki temu istniejące klasy i fake'i pasują do portu bez klas pośredniczących, a port można zmieniać bez edycji deklaracji adapterów. Adapter nadal zależy od typów domenowych użytych w sygnaturach. Ceną jest to, że niezgodność wykrywa type checker, a nie interpreter przy tworzeniu obiektu, więc potrzebny jest mypy lub pyright w CI.

Zobacz: [sekcja „Protocol zamiast ABC”](#protocol-zamiast-abc).

</details>

### 10. Kto powinien być właścicielem interfejsu portu: rdzeń czy adapter?

<details>
<summary>Odpowiedź</summary>

Właścicielem portu powinien być rdzeń. Interfejs leży w pakiecie rdzenia i jest pisany w języku domeny, więc adaptery importują rdzeń, a nie odwrotnie. Kształt portu wyznacza potrzeba przypadku użycia, nie API dostawcy technologii. Dzięki temu wymiana technologii oznacza nowy adapter, a nie zmianę w rdzeniu.

Zobacz: [sekcja „Właściciel interfejsu portu”](#właściciel-interfejsu-portu).

</details>
