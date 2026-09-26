# Domena i warstwa aplikacji

Porty i adaptery już znamy, więc teraz wypełniamy rdzeń treścią: reguły trafiają do encji i PricingPolicy, a use case'y StartRental i FinishRental orkiestrują je przez porty wyjściowe i zwracają wyniki domenowe, nie odpowiedzi HTTP.

```text
adapter wejściowy --> [ use case ] --> port wyjściowy <-- adapter
                        |
                        v
                encje, PricingPolicy
                (logika domenowa)
```

## Rola use case'u w heksagonie

[Przypadek użycia](00%20Glosariusz.md#przypadek-użycia) (serwis aplikacyjny) to jedna operacja, którą rdzeń oferuje światu: koordynuje encje i [porty wyjściowe](00%20Glosariusz.md#port-wyjściowy-driven), by zrealizować cel użytkownika, np. „rozpocznij wypożyczenie”. Sam nie zawiera szczegółów technologii, a reguły biznesowe deleguje do encji i obiektów wartości.

### Mechanizm

Use case to punkt wejścia do rdzenia, czyli konkretna realizacja [portu wejściowego](00%20Glosariusz.md#port-wejściowy-driving). Adapter wejściowy wywołuje go z danymi domenowymi, a on wykonuje stały scenariusz: pobiera dane przez porty, każe encjom sprawdzić reguły, zapisuje wynik i zwraca rezultat domenowy.

```text
router (adapter) → StartRental → User / Bike / Rental (reguły)
                       │
                       └→ RentalRepository (port) → SQLAlchemy (adapter)
```

W przykładzie `StartRental` dostaje `RentalRepository`, sprawdza przez `active_for_user`, czy użytkownik nie ma aktywnego wypożyczenia, i zapisuje nowe `Rental` przez `add`. `FinishRental` liczy opłatę przez `PricingPolicy` i wywołuje `PaymentGateway.charge`.

```python
class StartRental:
    def __init__(self, rentals: RentalRepository) -> None: ...
    def __call__(self, user_id: str, bike_id: str) -> Rental: ...
```

### Konsekwencja

Use case jest jedynym miejscem, które zna kolejność kroków, więc każdy kanał wejścia (HTTP, CLI, konsument kolejki) powtarza ten sam scenariusz bez kopiowania go. Testujesz go na fake'ach portów, bez bazy i HTTP.

## Logika domenowa a aplikacyjna

[Logika domenowa](00%20Glosariusz.md#logika-domenowa) to reguły biznesu, które obowiązywałyby także bez komputera, np. „pierwsze 20 minut jest darmowe”. [Logika aplikacyjna](00%20Glosariusz.md#logika-aplikacyjna) to koordynacja jednego scenariusza: skąd wziąć dane, w jakiej kolejności wywołać kroki i co zapisać lub wysłać. Pierwsza odpowiada na pytanie „co wolno i ile to kosztuje?”, druga na „co po kolei zrobić, by zrealizować żądanie?”.

| | Domenowa | Aplikacyjna |
|---|---|---|
| Miejsce | [[entity\|encje]], [[value-object\|obiekty wartości]] | [[use-case\|przypadki użycia]] |
| Przykład | cennik, blokada przy zaległej płatności | pobierz wypożyczenie, policz, obciąż, zapisz |
| Zna porty? | nie | tak |
| Test | zwykłe wywołanie, bez fake'ów | fake'i portów |

Praktyczny test: jeśli zasada zmieni się, bo zmieni się regulamin, to logika domenowa. Jeśli zmieni się, bo dodajesz krok, retry albo kanał wejścia, to aplikacyjna.

```python
# core/pricing.py · domenowa: sama reguła, bez portów
def fee(self, minutes: int) -> Money:
    billable = max(0, minutes - self.free_minutes)
    ...

# core/use_cases.py · aplikacyjna: kolejność kroków
def __call__(self, rental_id: str) -> Money:
    ...  # wczytaj Rental, ustal minutes
    fee = PricingPolicy().fee(minutes)
    self._payments.charge(rental.user_id, fee)
    return fee
```

### Konsekwencja

Gdy reguła trafi do use case'u, każdy nowy use case musi ją skopiować albo o niej pamiętać. Gdy zaś orkiestracja trafi do encji, encja zacznie wołać porty i przestanie być testowalna bez fake'ów. Trzymanie granicy sprawia, że cennik testujesz jednym wywołaniem, a `FinishRental` tylko pod kątem kolejności kroków.

## Use case i porty wyjściowe

Use case zależy od portów wyjściowych przez konstruktor: dostaje je jako argumenty typowane abstrakcją z rdzenia i nigdy sam nie tworzy adapterów. To praktyczne zastosowanie [zasady odwrócenia zależności](00%20Glosariusz.md#zasada-odwrócenia-zależności): kod wysokiego poziomu zależy od interfejsu, który sam zdefiniował.

```python
# core/use_cases.py
class FinishRental:
    def __init__(self, rentals: RentalRepository,
                 payments: PaymentGateway) -> None:
        self._rentals = rentals
        self._payments = payments

    def __call__(self, rental_id: str) -> Money:
        ...  # wczytaj Rental, policz fee
        self._payments.charge(rental.user_id, fee)
        return fee
```

Importy w `core/use_cases.py` sięgają tylko do `core/ports.py` i `core/pricing.py`. Nie ma tam `sqlalchemy` ani `stripe`. Zależności są jawne: sygnatura konstruktora mówi, z czym use case rozmawia ze światem.

Use case nie wie, jaki adapter dostał. Może to być `StripePaymentGateway` albo [fake](00%20Glosariusz.md#fake), czyli prosta, działająca implementacja portu (np. w pamięci), podstawiana w testach zamiast prawdziwego adaptera. Liczy się kształt portu. Wybór należy do composition root, czyli miejsca składania aplikacji, które omawiamy w dziale o okablowaniu.

### Konsekwencja

Test `FinishRental` nie wymaga bazy ani sieci: podajesz fake'i i sprawdzasz kolejność kroków. Dodanie nowej zależności widać od razu w konstruktorze, a zmiana dostawcy płatności nie dotyka pliku z use case'em.

## Encje bez dziedziczenia po ORM

Encja dziedzicząca po modelu ORM przestaje być [encją](00%20Glosariusz.md#encja) domeny i staje się [modelem trwałości](00%20Glosariusz.md#model-trwałości): klasą opisującą tabelę, z kolumnami, sesją i cyklem życia zarządzanym przez bibliotekę. Rdzeń zaczyna wtedy zależeć od `sqlalchemy`, czyli zależność wskazuje na zewnątrz, wbrew temu, co ustaliliśmy w sekcji o kierunku zależności.

Mechanizm jest prosty: klasa bazowa ORM wnosi do encji instrumentację atrybutów, powiązanie z sesją i metadane tabeli. Reguły domenowe zaczynają być zależne od tego, czy obiekt jest podpięty do sesji, czy atrybut jest załadowany leniwie i kiedy nastąpi `flush`. Zmiana schematu (np. rozbicie tabeli) wymusza wtedy zmianę encji, choć reguły biznesowe się nie zmieniły.

```python
# poza kanonem: źle, encja jest wierszem tabeli
class Rental(Base):
    __tablename__ = "rentals"
    id = Column(String, primary_key=True)
    bike_id = Column(ForeignKey("bikes.id"))
    user_id = Column(ForeignKey("users.id"))
```

Test takiej encji wymaga metadanych i zwykle bazy, a nie zwykłego wywołania konstruktora. Rozwiązaniem jest zostawienie `Rental` zwykłym dataclassem z `core/entities.py`, a `RentalRow` w `infra`. Tłumaczy je adapter, jak w `SqlAlchemyRentalRepository._to_domain`.

### Konsekwencja

Koszt to kod mapowania i jedna klasa więcej na tabelę. W zamian rdzeń testujesz bez bazy, a schemat i model domeny zmieniasz niezależnie.

## Port repozytorium a DAO

[Port repozytorium](00%20Glosariusz.md#port-repozytorium) to port wyjściowy, który dla rdzenia wygląda jak kolekcja encji w pamięci: dodajesz obiekt, pytasz o obiekt, a o tabelach nic nie wiesz. [DAO](00%20Glosariusz.md#dao-data-access-object) (Data Access Object) to obiekt opakowujący dostęp do jednej tabeli lub źródła danych, więc jego kształt wyznacza schemat, a nie domena.

Różnica leży w właścicielu i języku. `RentalRepository` mieszka w `core/ports.py`, przyjmuje i zwraca `Rental`, a jego metody odpowiadają na pytania domeny, np. `active_for_user`. DAO mieszka przy bazie, operuje na wierszach i zwykle odzwierciedla operacje na tabeli:

```python
# poza kanonem: DAO, język tabeli
class RentalDao:
    def insert(self, row: RentalRow) -> None: ...
    def select_by_id(self, row_id: str) -> RentalRow | None: ...
    def select_where_returned_at_is_null(self, user_id: str) -> list[RentalRow]: ...
    def update(self, row: RentalRow) -> None: ...
    def delete(self, row_id: str) -> None: ...
```

| | Port repozytorium | DAO |
|---|---|---|
| Właściciel | rdzeń | warstwa danych |
| Typy | encje domeny | wiersze, modele trwałości |
| Nazwy metod | pytania domeny | operacje na tabeli |
| Kształt wyznacza | potrzeba use case'u | schemat bazy |

### Konsekwencja

Use case pyta „czy użytkownik ma aktywne wypożyczenie”, a nie „które wiersze mają `returned_at IS NULL`”. Dzięki temu `StartRental` nie zmienia się przy przebudowie schematu, a port łatwo zastąpić fake'iem w pamięci. Repozytorium ma też tylko metody, których rdzeń faktycznie potrzebuje, a nie pełny zestaw CRUD.

## Use case zwraca wynik, nie HTTP

Use case powinien zwracać obiekty domenowe lub dedykowane wyniki, bo odpowiedź HTTP jest językiem jednego portu wejściowego i wciągnęłaby protokół do rdzenia. Rdzeń mówi językiem domeny: `StartRental` zwraca `Rental`, a `FinishRental` zwraca `Money`.

Mechanizm jest prosty. Kod statusu, nagłówki i kształt JSON to decyzje adaptera. Ten sam use case wywołuje router FastAPI, `LockEventConsumer` i zadanie cykliczne, a żaden z nich nie chce `JSONResponse`. Każdy tłumaczy wynik po swojemu: router na `RentalResponse` i 201, konsument na potwierdzenie wiadomości.

```python
# poza kanonem: źle, use case zna HTTP
class FinishRental:
    def __call__(self, rental_id: str) -> JSONResponse:
        ...
        return JSONResponse({"fee": str(fee.amount)}, status_code=200)
```

Gdy wynik nie mieści się w jednej encji, użyj dedykowanego wyniku, czyli małego [obiektu wyniku](00%20Glosariusz.md#obiekt-wyniku): niezmiennej struktury w rdzeniu, opisującej rezultat scenariusza w języku domeny. Może np. zawierać `Money` i minuty jazdy. Nie zawiera pól wymyślonych pod jeden ekran ani pod jeden format.

Błędy działają tak samo: use case zgłasza [błąd rdzenia](00%20Glosariusz.md#błąd-rdzenia), np. `PaymentDeclined`, a nie `HTTPException(402)`. Adapter mapuje go na status.

### Konsekwencja

Test use case'u sprawdza `Money`, a nie treść odpowiedzi. Zmiana formatu API, dodanie CLI czy gRPC nie dotyka rdzenia, a importy nadal wskazują do środka.

## Port repozytorium a DAO (uzupełnienie)

Port repozytorium to port wyjściowy należący do rdzenia, który udaje kolekcję encji: dodajesz i wyszukujesz obiekty domenowe, nie wiedząc nic o tabelach. DAO (Data Access Object) to obiekt opakowujący dostęp do jednej tabeli lub źródła danych, więc jego kształt wyznacza schemat bazy, a nie potrzeba domeny.

| | Port repozytorium | DAO |
|---|---|---|
| Właściciel | rdzeń | infrastruktura |
| Język | pojęcia domeny (`Rental`) | wiersze i CRUD |
| Kształt wyznacza | scenariusz use case'u | schemat tabeli |
| Zwraca | encje | wiersze lub słowniki |

`RentalRepository.active_for_user` nazywa pytanie biznesowe. DAO miałby raczej `select_by_user_and_status`, bo mówi językiem SQL.

### Adapter może użyć DAO

Oba pojęcia nie wykluczają się, tylko leżą w różnych miejscach. [Adapter](00%20Glosariusz.md#adapter) repozytorium może w środku sięgać do tabeli przez DAO, a potem tłumaczyć wiersze na encje:

```text
StartRental → RentalRepository (port, rdzeń)
                   ↑ implementuje
SqlAlchemyRentalRepository (adapter)
                   → RentalDao → tabela rentals
```

Rdzeń widzi tylko port. To, że pod spodem jest DAO, sesja SQLAlchemy czy plik, jest szczegółem adaptera, który można zmienić bez dotykania use case'ów.

Konsekwencja: DAO wystawione wprost use case'owi przenosi schemat bazy do rdzenia. Wtedy zmiana tabeli wymusza zmianę reguł biznesowych, czyli dokładnie to, czemu port miał zapobiec.

## Co zapamiętać

- Use case jest punktem wejścia do rdzenia: orkiestruje encje i porty w jednym scenariuszu, a reguły i technologię zostawia innym.
- Reguły biznesu (co wolno i ile kosztuje) należą do encji i obiektów wartości, a use case tylko układa kroki scenariusza i wywołuje te reguły.
- Use case przyjmuje porty wyjściowe w konstruktorze i zna tylko ich abstrakcje z rdzenia, więc adapter można podmienić bez zmiany use case'u.
- Encja domenowa to zwykła klasa w rdzeniu, a model ORM żyje w adapterze, bo dziedziczenie po ORM wciąga bibliotekę i schemat bazy do reguł biznesowych.
- Port repozytorium jest kolekcją encji w języku domeny i należy do rdzenia, a DAO jest opakowaniem tabeli w języku bazy i należy do infrastruktury.
- Use case zwraca wartości domenowe lub dedykowany wynik i zgłasza błędy rdzenia; kody statusu i JSON to zadanie adaptera.
- Port repozytorium to kolekcja encji w języku domeny w rdzeniu, a DAO to opakowanie tabeli przy technologii; adapter repozytorium może w środku używać DAO, o czym rdzeń nie wie.

## Pytania sprawdzające

### 17. Jaką rolę pełni use case (serwis aplikacyjny) w heksagonie?

<details>
<summary>Odpowiedź</summary>

Use case to jedna operacja oferowana przez rdzeń: orkiestruje encje i porty wyjściowe, by zrealizować cel użytkownika. Pobiera dane, wywołuje reguły zawarte w encjach i obiektach wartości, zapisuje wynik i zwraca rezultat domenowy. Jest punktem wejścia do rdzenia dla wszystkich adapterów wejściowych, więc scenariusz istnieje w jednym miejscu i daje się testować na fake'ach.

Zobacz: [sekcja „Rola use case'u w heksagonie”](#rola-use-caseu-w-heksagonie).

</details>

### 18. Czym różni się logika domenowa od logiki aplikacyjnej?

<details>
<summary>Odpowiedź</summary>

Logika domenowa to reguły biznesu niezależne od aplikacji (cennik, limity, blokady), żyjące w encjach i obiektach wartości i nieznające portów. Logika aplikacyjna to koordynacja jednego scenariusza: pobranie danych przez porty, wywołanie reguł domenowych w odpowiedniej kolejności, zapis i skutki uboczne. Pierwsza zmienia się wraz z regulaminem, druga wraz ze scenariuszami i kanałami użycia.

Zobacz: [sekcja „Logika domenowa a aplikacyjna”](#logika-domenowa-a-aplikacyjna).

</details>

### 19. Jak use case zależy od portów wyjściowych?

<details>
<summary>Odpowiedź</summary>

Use case dostaje porty wyjściowe przez konstruktor, jako argumenty typowane abstrakcjami zdefiniowanymi w rdzeniu, i nigdy sam nie tworzy adapterów. Dzięki temu importuje tylko porty i obiekty domeny, a nie biblioteki technologiczne. Konkretny adapter, na przykład Stripe albo fake w testach, wybiera composition root. Zależności use case'u są jawne w sygnaturze konstruktora, a ich wymiana nie wymaga zmian w use case'ie.

Zobacz: [sekcja „Use case i porty wyjściowe”](#use-case-i-porty-wyjściowe).

</details>

### 20. Dlaczego encje domenowe nie powinny dziedziczyć po modelach ORM?

<details>
<summary>Odpowiedź</summary>

Encja dziedzicząca po modelu ORM staje się modelem trwałości: rdzeń zależy wtedy od biblioteki bazodanowej, wbrew kierunkowi zależności do rdzenia. Reguły domenowe wiążą się ze stanem sesji, ładowaniem leniwym i schematem tabel, więc zmiana schematu wymusza zmianę encji, a testy wymagają metadanych lub bazy. Lepiej trzymać encję jako zwykły dataclass w rdzeniu, a model ORM w adapterze, który tłumaczy między nimi. Kosztem jest dodatkowy kod mapowania.

Zobacz: [sekcja „Encje bez dziedziczenia po ORM”](#encje-bez-dziedziczenia-po-orm).

</details>

### 21. Czym jest port repozytorium i czym różni się od DAO?

<details>
<summary>Odpowiedź</summary>

Port repozytorium to port wyjściowy należący do rdzenia, który udaje kolekcję encji: dodajesz i wyszukujesz obiekty domenowe, nie wiedząc nic o tabelach. DAO opakowuje konkretną tabelę lub źródło danych, więc jego kształt wyznacza schemat bazy, a nie potrzeba domeny. Różnią się właścicielem i językiem: repozytorium mówi pojęciami domeny i leży w rdzeniu, DAO mówi wierszami i operacjami CRUD i leży przy technologii. Adapter repozytorium może w środku użyć DAO do dostępu do tabeli i tłumaczyć wiersze na encje, ale rdzeń o tym nie wie i widzi tylko port.

Zobacz: [sekcja „Port repozytorium a DAO”](#port-repozytorium-a-dao), [sekcja „Port repozytorium a DAO (uzupełnienie)”](#port-repozytorium-a-dao-uzupełnienie).

</details>

### 22. Dlaczego use case powinien zwracać obiekty domenowe lub dedykowane wyniki, a nie odpowiedzi HTTP?

<details>
<summary>Odpowiedź</summary>

Odpowiedź HTTP jest językiem jednego adaptera wejściowego, więc jej zwracanie wciągałoby protokół do rdzenia i wiązało use case z jednym kanałem. Use case zwraca obiekty domenowe (`Rental`, `Money`) albo dedykowany wynik w języku domeny, a błędy zgłasza jako błędy rdzenia. Adapter tłumaczy to na status, nagłówki i JSON. Dzięki temu ten sam use case obsłuży router, konsumenta kolejki i CLI, a testy sprawdzają wartości domenowe.

Zobacz: [sekcja „Use case zwraca wynik, nie HTTP”](#use-case-zwraca-wynik-nie-http).

</details>
