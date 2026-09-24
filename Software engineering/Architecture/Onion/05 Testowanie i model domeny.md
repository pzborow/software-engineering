# Testowanie i model domeny

Czwarta zasada Palermo mówi, że rdzeń da się uruchomić bez infrastruktury. Najbardziej odczuwalnie wykorzystują to testy. Ten rozdział pokazuje, jak testować każdy pierścień osobno, a potem jak wypełnić środek cebuli pojęciami z DDD.

```text
pierścień              czym testujemy                           koszt testu
Domain Model           zwykły pytest, bez żadnych dublerów      najtańszy
Domain Services        zwykły pytest, obiekty domeny na wejściu tani
Application Services   fake'i repozytoriów i zegara             tani
zewnętrzny             prawdziwa baza, klient HTTP              najdroższy
```

## Najtańsze testy są w środku

Model domeny i serwisy domenowe to czysty Python. Test tworzy obiekty, wywołuje metodę i sprawdza wynik. Nie ma bazy, sieci ani przygotowywania danych:

```python
from datetime import date


def test_loan_is_overdue_after_30_days():
    loan = Loan(id="l-1", book_id="b-1", member_id="m-1", borrowed_on=date(2026, 9, 1))

    assert not loan.is_overdue(date(2026, 10, 1))
    assert loan.is_overdue(date(2026, 10, 2))


def test_member_with_overdue_loan_cannot_borrow():
    overdue = Loan(id="l-1", book_id="b-1", member_id="m-1", borrowed_on=date(2026, 1, 1))

    assert not LoanPolicy().can_borrow([overdue], today=date(2026, 9, 23))


def test_fine_is_half_zloty_per_day():
    loan = Loan(id="l-1", book_id="b-1", member_id="m-1", borrowed_on=date(2026, 9, 1))

    assert FineCalculator().fine_for(loan, date(2026, 10, 5)) == Decimal("2.00")
```

Takie testy trwają milisekundy, więc może ich być setki. Każda reguła biznesowa powinna mieć test właśnie tutaj.

## Application Services z dublerami

Application Service używa interfejsów, więc w teście każdą zależność zastępuje <a id="term-test-double"></a>[dubler testowy](00%20Glossary%20Onion.md#test-double). Najczęściej jest to <a id="term-fake"></a>[fake](00%20Glossary%20Onion.md#fake), czyli działająca, uproszczona implementacja interfejsu, która trzyma dane w pamięci:

```python
class InMemoryBooks:
    def __init__(self, *books: Book):
        self._books = {b.id: b for b in books}

    def get(self, book_id: str) -> Book:
        try:
            return self._books[book_id]
        except KeyError:
            raise BookNotFound(book_id)

    def save(self, book: Book) -> None:
        self._books[book.id] = book


class InMemoryLoans:
    def __init__(self, *loans: Loan):
        self._loans = {l.id: l for l in loans}

    def active_for(self, member_id: str) -> list[Loan]:
        return [l for l in self._loans.values() if l.member_id == member_id and l.returned_on is None]

    def add(self, loan: Loan) -> None:
        self._loans[loan.id] = loan


class FixedClock:
    def __init__(self, today: date):
        self._today = today

    def today(self) -> date:
        return self._today
```

Test używa prostszej wersji `BorrowBookService` z rozdziału 02, która przyjmuje repozytoria bezpośrednio. Wersja z Unit of Work z rozdziału 04 testuje się tak samo, z fake'owym `InMemoryUnitOfWork`, który trzyma oba repozytoria.

```python
def an_active_loan(member_id: str, n: int) -> Loan:
    return Loan(id=f"l-{n}", book_id=f"b-{n}", member_id=member_id, borrowed_on=date(2026, 9, 20))


def test_borrowing_marks_book_as_lent():
    books = InMemoryBooks(Book(id="b-1", title="Cebula"))
    loans = InMemoryLoans()
    service = BorrowBookService(books, loans, LoanPolicy(), FixedClock(date(2026, 9, 23)))

    service.borrow("m-1", "b-1")

    assert books.get("b-1").available is False
    assert len(loans.active_for("m-1")) == 1


def test_fourth_loan_is_refused():
    loans = InMemoryLoans(*[an_active_loan("m-1", n) for n in range(3)])
    service = BorrowBookService(InMemoryBooks(Book("b-9", "X")), loans, LoanPolicy(), FixedClock(date(2026, 9, 23)))

    with pytest.raises(LoanError):
        service.borrow("m-1", "b-9")
```

`FixedClock` pokazuje, dlaczego zegar był interfejsem w rozdziale 03. Test przeterminowania ustawia dowolną datę jednym argumentem.

Fake jest lepszy niż mock, bo test sprawdza stan po operacji („książka jest wypożyczona”), a nie to, które metody zostały wywołane. Refaktoryzacja serwisu nie psuje takich testów.

## Czy fake mówi prawdę

Fake jest użyteczny tylko wtedy, gdy zachowuje się jak prawdziwa implementacja. Pilnuje tego <a id="term-contract-test"></a>[test kontraktowy](00%20Glossary%20Onion.md#contract-test): jeden zestaw testów uruchamiany na fake'u i na implementacji SQL.

```python
@pytest.fixture(params=["memory", "sql"])
def books(request, db_session):
    if request.param == "memory":
        return InMemoryBooks()
    return SqlBookRepository(db_session)


def test_missing_book_raises_domain_error(books):
    with pytest.raises(BookNotFound):
        books.get("nope")


def test_saved_book_keeps_availability(books):
    book = Book(id="b-1", title="Cebula")
    book.lend()
    books.save(book)
    assert books.get("b-1").available is False
```

Wariant `sql` uruchamia się na prawdziwej bazie, na przykład w Testcontainers. Jest to jednocześnie test integracyjny infrastruktury.

## Koszt testów w każdym pierścieniu

| Pierścień | Co testujemy | Zależności | Ile testów |
|---|---|---|---|
| Domain Model | niezmienniki, obliczenia | brak | najwięcej |
| Domain Services | reguły między obiektami | brak | dużo |
| Application Services | scenariusze, kolejność, błędy | fake'i | dużo |
| Zewnętrzny | SQL, mapowanie, HTTP, konfiguracja | prawdziwa technologia | umiarkowanie |
| Całość end-to-end | czy composition root poprawnie łączy obiekty | wszystko | kilka |

Najtańsze testy są w środku cebuli, najdroższe na zewnątrz. Rozkład testów powinien to odzwierciedlać.

## Wypełnianie środka

Onion mówi, gdzie leży model domeny, ale nie mówi, jak go zbudować. Tę lukę wypełnia <a id="term-ddd"></a>[Domain-Driven Design](00%20Glossary%20Onion.md#ddd) Erica Evansa. Palermo pisał swoje artykuły z myślą o DDD, dlatego oba podejścia pasują do siebie naturalnie.

DDD zaczyna od <a id="term-ubiquitous-language"></a>[języka wszechobecnego](00%20Glossary%20Onion.md#ubiquitous-language): wspólnego słownika zespołu i ekspertów. Jeśli bibliotekarz mówi „wypożyczenie” i „kara za przetrzymanie”, w kodzie są `Loan` i `FineCalculator`, a nie `Transaction` i `PenaltyHelper`.

Taktyczne cegiełki DDD trafiają do warstwy Domain Model:

<a id="term-entity"></a>[Encja](00%20Glossary%20Onion.md#entity) ma tożsamość, która trwa mimo zmian stanu. `Loan` o ID `l-1` pozostaje tym samym wypożyczeniem po zwrocie książki.

<a id="term-value-object"></a>[Value object](00%20Glossary%20Onion.md#value-object) nie ma tożsamości i jest porównywany po wartości. Jest niezmienny. Dobrym przykładem jest okres wypożyczenia:

```python
@dataclass(frozen=True)
class LoanPeriod:
    start: date
    days: int = 30

    @property
    def end(self) -> date:
        return self.start + timedelta(days=self.days)

    def extended(self, extra_days: int) -> "LoanPeriod":
        return LoanPeriod(self.start, self.days + extra_days)
```

<a id="term-aggregate"></a>[Agregat](00%20Glossary%20Onion.md#aggregate) to grupa obiektów zmienianych tylko przez korzeń. Agregat jest jednostką spójności, więc zapisuje się go w całości, a repozytorium istnieje dla korzenia, nie dla każdej klasy. W wypożyczalni `Member` może być korzeniem agregatu, który pilnuje własnych wypożyczeń:

```python
@dataclass
class Member:
    id: str
    loans: list[Loan] = field(default_factory=list)

    def borrow(self, book: Book, today: date, policy: LoanPolicy) -> Loan:
        active = [l for l in self.loans if l.returned_on is None]
        if not policy.can_borrow(active, today):
            raise BorrowingBlocked(self.id)
        book.lend()
        loan = Loan(id=str(uuid4()), book_id=book.id, member_id=self.id, borrowed_on=today)
        self.loans.append(loan)
        return loan
```

Mapowanie DDD na pierścienie:

| Element DDD | Pierścień Onion |
|---|---|
| encje, value objects, agregaty, zdarzenia domenowe | Domain Model |
| serwisy domenowe, interfejsy repozytoriów | Domain Services |
| serwisy aplikacyjne | Application Services |
| implementacje repozytoriów, anti-corruption layer | pierścień zewnętrzny |

Onion bez DDD też działa, bo środek może zawierać proste klasy i funkcje. DDD bez izolacji z cebuli jest trudniejsze, bo model łatwo zanieczyścić adnotacjami ORM.

## Co zapamiętać

- Testy Domain Model i Domain Services nie potrzebują żadnych dublerów i są najtańsze.
- Application Services testuje się z fake'ami repozytoriów i zegara.
- Fake jest zwykle lepszy od mocka, bo test sprawdza stan, a nie wywołania.
- Test kontraktowy uruchamia te same asercje na fake'u i implementacji SQL.
- DDD wypełnia środek cebuli: encje, value objects i agregaty trafiają do Domain Model.
- Język wszechobecny sprawia, że nazwy w kodzie odpowiadają słowom ekspertów.

## Pytania sprawdzające

### 20. Jak testować każdą warstwę osobno i której warstwy testy są najtańsze?

<details>
<summary>Odpowiedź</summary>

Domain Model i Domain Services testuje się zwykłymi testami jednostkowymi bez dublerów: tworzysz obiekty, wywołujesz metodę, sprawdzasz wynik. To najtańsze testy i powinno ich być najwięcej. Application Services testuje się z fake'ami repozytoriów i zegara (np. `InMemoryBooks`, `FixedClock`), sprawdzając stan po operacji. Pierścień zewnętrzny testuje się z prawdziwą technologią, a zgodność fake'ów z implementacjami pilnują testy kontraktowe. Kilka testów end-to-end sprawdza composition root.

Zobacz: sekcje „Najtańsze testy są w środku”, „Application Services z dublerami”, „Czy fake mówi prawdę” i „Koszt testów w każdym pierścieniu”.

</details>

### 21. Jak Onion współpracuje z DDD (encje, value objects, agregaty) w warstwie Domain Model?

<details>
<summary>Odpowiedź</summary>

Onion mówi, gdzie jest model domeny, a DDD mówi, jak go zbudować. Encje (tożsamość, np. `Loan`), value objects (niezmienne, porównywane po wartości, np. `LoanPeriod`) i agregaty (grupa zmieniana przez korzeń, np. `Member` z wypożyczeniami) trafiają do Domain Model. Serwisy domenowe i interfejsy repozytoriów trafiają do Domain Services, serwisy aplikacyjne do Application Services, a implementacje repozytoriów na zewnątrz. Nazwy wynikają z języka wszechobecnego. Onion nie wymaga DDD, ale bardzo dobrze chroni model DDD.

Zobacz: sekcja „Wypełnianie środka”.

</details>
