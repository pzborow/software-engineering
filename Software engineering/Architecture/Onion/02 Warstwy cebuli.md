# Warstwy cebuli

Palermo opisał cztery pierścienie. Każdy ma jedną odpowiedzialność i może korzystać tylko z pierścieni leżących bliżej środka. Ten rozdział przechodzi przez nie od środka na zewnątrz na przykładzie wypożyczalni książek.

```text
pierścień              przykładowe klasy                      zależy od
─────────────────────  ─────────────────────────────────────  ──────────────────
Domain Model           Book, Member, Loan                     nikogo
Domain Services        LoanPolicy, FineCalculator,            Domain Model
                       interfejs LoanRepository
Application Services   BorrowBookService, ReturnBookService   obu powyższych
UI, infra, testy       router FastAPI, SqlLoanRepository,     wszystkich powyższych
                       pytest
```

## Pierwsza warstwa: obiekty biznesowe

Najgłębiej leży <a id="term-domain-model"></a>[model domeny](00%20Glossary%20Onion.md#domain-model) (Domain Model). Są tu obiekty, które mają stan i zachowanie: książka wie, czy jest dostępna, a wypożyczenie wie, czy jest przeterminowane.

```python
# domain/model.py
from dataclasses import dataclass
from datetime import date, timedelta


class LoanError(Exception):
    pass


@dataclass
class Book:
    id: str
    title: str
    available: bool = True

    def lend(self) -> None:
        if not self.available:
            raise LoanError(f"Książka {self.title} jest już wypożyczona")
        self.available = False

    def give_back(self) -> None:
        self.available = True


@dataclass
class Loan:
    id: str
    book_id: str
    member_id: str
    borrowed_on: date
    returned_on: date | None = None

    LOAN_DAYS = 30

    @property
    def due_date(self) -> date:
        return self.borrowed_on + timedelta(days=self.LOAN_DAYS)

    def is_overdue(self, today: date) -> bool:
        return self.returned_on is None and today > self.due_date

    def close(self, today: date) -> None:
        if self.returned_on is not None:
            raise LoanError("Wypożyczenie jest już zamknięte")
        self.returned_on = today
```

Do modelu domeny nie należą: adnotacje ORM, serializacja do JSON, obiekty `Request`, logowanie techniczne, konfiguracja, zapytania SQL. Nie należą tu też reguły, które wymagają wiedzy o wielu obiektach naraz. Te trafiają pierścień wyżej.

## Druga warstwa: reguły ponad obiektami

Warstwa <a id="term-domain-services"></a>[Domain Services](00%20Glossary%20Onion.md#domain-services) zawiera logikę biznesową, która nie pasuje do jednego obiektu. Reguła „członek z przeterminowanym wypożyczeniem albo z trzema aktywnymi wypożyczeniami nie może pożyczyć kolejnej książki” dotyczy członka i wszystkich jego wypożyczeń naraz:

```python
# domain/services.py
from datetime import date
from decimal import Decimal

from library.domain.model import Loan


class LoanPolicy:
    MAX_ACTIVE_LOANS = 3

    def can_borrow(self, active_loans: list[Loan], today: date) -> bool:
        if len(active_loans) >= self.MAX_ACTIVE_LOANS:
            return False
        return not any(loan.is_overdue(today) for loan in active_loans)


class FineCalculator:
    DAILY_FINE = Decimal("0.50")

    def fine_for(self, loan: Loan, today: date) -> Decimal:
        if not loan.is_overdue(today):
            return Decimal("0")
        return (today - loan.due_date).days * self.DAILY_FINE
```

W oryginalnym opisie Palermo w tej warstwie leżą też interfejsy repozytoriów, bo to reguły domenowe decydują, jakie dane są potrzebne. Szczegóły opisuje rozdział 03.

Serwis domenowy nie wie o transakcjach, HTTP ani powiadomieniach. Przyjmuje obiekty domeny i zwraca decyzję albo wynik obliczenia. Da się go przetestować bez żadnego dublera.

## Trzecia warstwa: scenariusze

Warstwa <a id="term-application-services"></a>[Application Services](00%20Glossary%20Onion.md#application-services) realizuje przypadki użycia: „wypożycz książkę”, „zwróć książkę”. Pobiera dane przez interfejsy repozytoriów, pyta domenę o decyzję, zapisuje wynik.

```python
# application/borrow_book.py
from datetime import date
from uuid import uuid4

from library.domain.model import Loan, LoanError
from library.domain.repositories import BookRepository, Clock, LoanRepository
from library.domain.services import LoanPolicy


class BorrowBookService:
    def __init__(self, books: BookRepository, loans: LoanRepository,
                 policy: LoanPolicy, clock: Clock):
        self._books = books
        self._loans = loans
        self._policy = policy
        self._clock = clock

    def borrow(self, member_id: str, book_id: str) -> str:
        today = self._clock.today()
        active = self._loans.active_for(member_id)
        if not self._policy.can_borrow(active, today):
            raise LoanError("Członek nie może teraz wypożyczyć książki")

        book = self._books.get(book_id)
        book.lend()
        loan = Loan(id=str(uuid4()), book_id=book.id, member_id=member_id, borrowed_on=today)

        self._books.save(book)
        self._loans.add(loan)
        return loan.id
```

Application Service nie zawiera reguł biznesowych. Nie wie, ile wypożyczeń wolno mieć i kiedy jest przeterminowanie. Wie tylko, w jakiej kolejności wykonać kroki. Dzięki temu reguła zmienia się w jednym miejscu, nawet jeśli korzysta z niej kilka scenariuszy.

| | Domain Services | Application Services |
|---|---|---|
| Pytanie | czy wolno? ile kosztuje? | co zrobić i w jakiej kolejności? |
| Zna repozytoria | definiuje ich interfejsy | wywołuje je |
| Zna transakcje | nie | wyznacza ich granice |
| Wywoływany przez | Application Services | UI, API, CLI, testy |

## Czwarta warstwa: styk ze światem

<a id="term-outer-ring"></a>[Pierścień zewnętrzny](00%20Glossary%20Onion.md#outer-ring) zawiera wszystko, co łączy rdzeń ze światem: UI i API, implementacje repozytoriów, klientów zewnętrznych usług, a także testy.

```python
# infrastructure/web.py
@router.post("/loans", status_code=201)
def borrow(body: BorrowRequest, service: BorrowBookService = Depends(get_borrow_service)):
    loan_id = service.borrow(body.member_id, body.book_id)
    return {"loan_id": loan_id}


# infrastructure/sql_loans.py
class SqlLoanRepository:
    def active_for(self, member_id: str) -> list[Loan]:
        rows = self._session.scalars(
            select(LoanRow).where(LoanRow.member_id == member_id, LoanRow.returned_on.is_(None))
        )
        return [to_domain(row) for row in rows]
```

Palermo celowo stawia UI, infrastrukturę i testy w tym samym pierścieniu. Każde z nich jest klientem albo dostawcą rdzenia i każde można wymienić. Test jest po prostu kolejnym „UI”, które wywołuje Application Services, a baza jest kolejnym dostawcą danych. Żadne z nich nie jest ważniejsze od pozostałych i żadne nie jest fundamentem.

## Przeskakiwanie warstw

Czy kontroler może wywołać `LoanPolicy` bezpośrednio, pomijając Application Services? W <a id="term-strict-layering"></a>[ścisłym warstwowaniu](00%20Glossary%20Onion.md#strict-layering) każda warstwa rozmawia tylko z warstwą leżącą bezpośrednio pod nią. W <a id="term-relaxed-layering"></a>[luźnym warstwowaniu](00%20Glossary%20Onion.md#relaxed-layering) warstwa może korzystać z każdej warstwy bliższej środka.

Onion w wersji Palermo jest luźny: kod może zależeć od dowolnej warstwy bardziej wewnętrznej. Zakazany jest tylko kierunek na zewnątrz.

```text
dozwolone:  kontroler ──► BorrowBookService ──► LoanPolicy ──► Loan
dozwolone:  kontroler ──► Loan                (odczyt prostego pola do widoku)
zakazane:   Loan ──► SqlLoanRepository
zakazane:   LoanPolicy ──► BorrowBookService
```

W praktyce wiele zespołów przyjmuje umowę bliższą ścisłej: UI woła tylko Application Services. Powód jest prosty. Jeśli kontroler sam złoży `LoanPolicy` i repozytoria, scenariusz rozjedzie się na dwie wersje, jedną w serwisie aplikacyjnym i drugą w kontrolerze. Luźne warstwowanie jest dopuszczalne, ale ścisłe dla zapisu zwykle jest bezpieczniejsze.

## Co zapamiętać

- Cztery pierścienie: Domain Model, Domain Services, Application Services, pierścień zewnętrzny.
- Model domeny zawiera obiekty z zachowaniem i nie zawiera niczego technicznego.
- Domain Services zawierają reguły dotyczące wielu obiektów i interfejsy repozytoriów.
- Application Services orkiestrują scenariusz, ale nie podejmują decyzji biznesowych.
- UI, infrastruktura i testy leżą w tym samym zewnętrznym pierścieniu.
- Onion Palermo jest luźny: wolno zależeć od każdej warstwy bliższej środka.
- Dla operacji zapisu bezpieczniej jest, gdy UI woła tylko Application Services.

## Pytania sprawdzające

### 6. Wymień typowe warstwy Onion od środka i opisz rolę każdej z nich.

<details>
<summary>Odpowiedź</summary>

Domain Model to obiekty biznesowe ze stanem i zachowaniem. Domain Services to reguły obejmujące wiele obiektów oraz interfejsy repozytoriów. Application Services to przypadki użycia, które orkiestrują kroki. Pierścień zewnętrzny to UI, infrastruktura (implementacje repozytoriów, klienci usług) i testy. Każda warstwa może zależeć tylko od warstw bliższych środka.

Zobacz: tabela na początku rozdziału i kolejne sekcje o warstwach.

</details>

### 7. Co należy do Domain Model, a co już nie?

<details>
<summary>Odpowiedź</summary>

Należą obiekty biznesowe z zachowaniem i własnymi regułami, np. `Book.lend()` czy `Loan.is_overdue()`. Nie należą adnotacje ORM, serializacja JSON, obiekty `Request`, logowanie techniczne, konfiguracja i SQL. Nie należą też reguły wymagające wiedzy o wielu obiektach naraz, bo te trafiają do Domain Services.

Zobacz: sekcja „Pierwsza warstwa: obiekty biznesowe”.

</details>

### 8. Czym jest warstwa Domain Services i czym różni się od Application Services?

<details>
<summary>Odpowiedź</summary>

Domain Services zawierają logikę biznesową, która nie pasuje do jednego obiektu, np. `LoanPolicy` (limit wypożyczeń, blokada przy przeterminowaniu) albo `FineCalculator`. Nie znają transakcji, HTTP ani powiadomień, tylko przyjmują obiekty domeny i zwracają decyzję. Application Services odpowiadają na pytanie „co zrobić i w jakiej kolejności”: pobierają dane, pytają domenę o decyzję, zapisują wynik i wyznaczają granice transakcji.

Zobacz: sekcje „Druga warstwa: reguły ponad obiektami” i „Trzecia warstwa: scenariusze”.

</details>

### 9. Co robią Application Services i dlaczego nie powinny zawierać reguł biznesowych?

<details>
<summary>Odpowiedź</summary>

Realizują przypadki użycia: pobierają obiekty przez repozytoria, wywołują domenę, zapisują zmiany. Nie zawierają reguł, bo reguła wpisana w jeden serwis nie obowiązuje w innym scenariuszu, który powinien jej przestrzegać. Wtedy ta sama reguła rozjeżdża się na kilka kopii. Reguła w domenie zmienia się w jednym miejscu.

Zobacz: sekcja „Trzecia warstwa: scenariusze”.

</details>

### 10. Co trafia do najbardziej zewnętrznej warstwy (UI, infrastruktura, testy) i dlaczego są one „na tym samym poziomie”?

<details>
<summary>Odpowiedź</summary>

UI i API, implementacje repozytoriów, klienci zewnętrznych usług oraz testy. Leżą na jednym poziomie, bo każde z nich jest wymiennym klientem albo dostawcą rdzenia. Test wywołuje Application Services tak samo jak kontroler, a baza dostarcza danych tak samo jak fake. Żadne z nich nie jest fundamentem aplikacji.

Zobacz: sekcja „Czwarta warstwa: styk ze światem”.

</details>

### 11. Czy warstwa może wywołać warstwę położoną dwa poziomy głębiej, pomijając pośrednią (strict vs relaxed layering)?

<details>
<summary>Odpowiedź</summary>

W wersji Palermo tak. Onion jest luźny, więc kod może zależeć od każdej warstwy bliższej środka, a zakazany jest tylko kierunek na zewnątrz. W ścisłym warstwowaniu wolno rozmawiać tylko z warstwą bezpośrednio niżej. W praktyce dla operacji zapisu dobrze jest umówić się, że UI woła tylko Application Services, bo inaczej scenariusz rozjedzie się między kontroler a serwis.

Zobacz: sekcja „Przeskakiwanie warstw”.

</details>
