# Interfejsy i odwrócenie zależności

Rdzeń cebuli potrzebuje danych z bazy, aktualnej daty i czasem zewnętrznych usług. Nie może jednak importować niczego z pierścienia zewnętrznego. Rozwiązaniem jest para: interfejs w środku i implementacja na zewnątrz. Ten rozdział pokazuje, gdzie leży każda część i kto je ze sobą łączy.

```text
środek:     BorrowBookService ──używa──► LoanRepository (interfejs)
                                                ▲
zewnątrz:                      SqlLoanRepository ┘ implementuje
```

## Interfejs w środku, implementacja na zewnątrz

<a id="term-repository"></a>[Repozytorium](00%20Glossary%20Onion.md#repository) daje rdzeniowi dostęp do obiektów domeny tak, jakby były kolekcją w pamięci. Jego interfejs leży w rdzeniu, w warstwie Domain Services albo w osobnym module domeny. Implementacja leży w infrastrukturze.

W Pythonie interfejs najwygodniej opisać przez <a id="term-protocol"></a>[`Protocol`](00%20Glossary%20Onion.md#protocol) z modułu `typing`. Klasa spełnia protokół, jeśli ma pasujące metody, bez dziedziczenia:

```python
# domain/repositories.py
from datetime import date
from typing import Protocol

from library.domain.model import Book, Loan, Member


class BookRepository(Protocol):
    def get(self, book_id: str) -> Book: ...
    def save(self, book: Book) -> None: ...


class LoanRepository(Protocol):
    def get(self, loan_id: str) -> Loan: ...
    def active_for(self, member_id: str) -> list[Loan]: ...
    def add(self, loan: Loan) -> None: ...


class MemberRepository(Protocol):
    def get(self, member_id: str) -> Member: ...


class Clock(Protocol):
    def today(self) -> date: ...
```

Dlaczego interfejs leży w środku? Bo to rdzeń wie, jakich danych potrzebuje i w jakiej postaci. Gdyby interfejs pochodził z infrastruktury, rdzeń musiałby ją importować i reguła zależności byłaby złamana. Metody są więc nazwane językiem domeny (`active_for`), a nie językiem bazy (`select_where_returned_is_null`).

Implementacja w infrastrukturze zna SQLAlchemy i tłumaczy wiersze na obiekty domeny:

```python
# infrastructure/sql_repositories.py
from sqlalchemy import select
from sqlalchemy.orm import Session

from library.domain.model import Loan


class SqlLoanRepository:
    def __init__(self, session: Session):
        self._session = session

    def active_for(self, member_id: str) -> list[Loan]:
        rows = self._session.scalars(
            select(LoanRow).where(LoanRow.member_id == member_id, LoanRow.returned_on.is_(None))
        )
        return [to_domain(row) for row in rows]

    def add(self, loan: Loan) -> None:
        self._session.add(from_domain(loan))
```

Nawet `Clock` jest interfejsem. Data systemowa to też zależność od świata zewnętrznego. Bez niej test reguły o przeterminowaniu musiałby czekać 30 dni albo podmieniać funkcje biblioteki standardowej.

## Zasada odwrócenia zależności

Opisany mechanizm to <a id="term-dependency-inversion"></a>[Dependency Inversion Principle](00%20Glossary%20Onion.md#dependency-inversion), czyli zasada odwrócenia zależności: moduł wysokiego poziomu i moduł niskiego poziomu zależą od wspólnej abstrakcji, a abstrakcja należy do modułu wysokiego poziomu.

```text
Przepływ wywołania:   BorrowBookService ──► SqlLoanRepository ──► PostgreSQL
Zależność w kodzie:   BorrowBookService ──► LoanRepository ◄── SqlLoanRepository
```

Wywołanie płynie na zewnątrz, zależność w kodzie wskazuje do środka. Cała architektura cebulowa to ta sama zasada SOLID zastosowana do całej aplikacji, a nie do jednej klasy.

## Kto tworzy obiekty

Skoro rdzeń nie tworzy `SqlLoanRepository`, ktoś musi to zrobić. Tym miejscem jest <a id="term-composition-root"></a>[composition root](00%20Glossary%20Onion.md#composition-root): jedno miejsce przy starcie aplikacji, w pierścieniu zewnętrznym, które zna wszystkie klasy i łączy je ze sobą.

```python
# infrastructure/bootstrap.py
from datetime import date

from library.application.borrow_book import BorrowBookService
from library.domain.services import LoanPolicy
from library.infrastructure.sql_repositories import SqlBookRepository, SqlLoanRepository


class SystemClock:
    def today(self) -> date:
        return date.today()


def build_borrow_service(session) -> BorrowBookService:
    return BorrowBookService(
        books=SqlBookRepository(session),
        loans=SqlLoanRepository(session),
        policy=LoanPolicy(),
        clock=SystemClock(),
    )
```

Composition root to jedyny moduł, który wolno uzależnić od wszystkiego. Dla testów, CLI i workera można mieć osobne funkcje `build_*`, które składają ten sam rdzeń z innymi implementacjami.

## Kontener i framework

<a id="term-di-container"></a>[Kontener DI](00%20Glossary%20Onion.md#di-container) automatyzuje składanie obiektów: rejestrujesz, która klasa implementuje który interfejs, a kontener tworzy graf zależności. W .NET, skąd pochodzi Onion, jest to wbudowany `IServiceCollection`. W Pythonie popularne są `dependency-injector`, `punq` i `lagom`, a w FastAPI mechanizm `Depends`.

```python
# infrastructure/web.py (FastAPI jako prosty kontener)
def get_session():
    with SessionLocal() as session:
        yield session


def get_borrow_service(session=Depends(get_session)) -> BorrowBookService:
    return build_borrow_service(session)
```

Kontener jest opcjonalny. W małym i średnim serwisie ręczne składanie w jednej funkcji jest czytelniejsze i łatwiej je debugować.

Framework (Django, FastAPI, Spring, ASP.NET) może żyć tylko w pierścieniu zewnętrznym. Sygnały, że wszedł do środka:

- klasy domeny dziedziczą po `models.Model` albo mają adnotacje ORM,
- Application Service przyjmuje `Request` albo zwraca `JSONResponse`,
- domena używa `settings` frameworka albo jego mechanizmu logowania,
- dekoratory wstrzykiwania zależności na klasach domeny.

Test szczelności jest ten sam co w rozdziale 01: rdzeń musi dać się zaimportować i uruchomić bez zainstalowanego frameworka.

## Dane na granicach warstw

Czym przekazywać dane między pierścieniami? Są trzy rodzaje obiektów:

<a id="term-dto"></a>[DTO](00%20Glossary%20Onion.md#dto) (Data Transfer Object) to prosty obiekt bez zachowania, który przenosi dane przez granicę, na przykład wynik Application Service dla API.

<a id="term-view-model"></a>[View model](00%20Glossary%20Onion.md#view-model) to DTO przygotowane pod konkretny ekran: sformatowane daty, etykiety, flagi dla przycisków.

Obiekty domeny mogą przepływać do środka i w obrębie rdzenia, ale nie powinny wychodzić do UI. Inaczej widok zaczyna zależeć od kształtu domeny, a ktoś wcześniej czy później wywoła w szablonie metodę zmieniającą stan.

```python
# application/dto.py
from dataclasses import dataclass
from datetime import date
from decimal import Decimal


@dataclass(frozen=True)
class LoanSummary:                 # DTO zwracane przez Application Services
    loan_id: str
    book_title: str
    due_date: date
    fine: Decimal
```

```python
# infrastructure/web.py
class LoanView(BaseModel):         # view model dla API
    title: str
    due: str                       # "12.10.2026"
    overdue: bool
    fine_label: str                # "2,50 zł"
```

```text
HTTP JSON ──► BorrowRequest ──► argumenty serwisu ──► obiekty domeny
obiekty domeny ──► LoanSummary (DTO) ──► LoanView (view model) ──► HTTP JSON
```

Tłumaczenie między tymi obiektami to zadanie <a id="term-mapper"></a>[mappera](00%20Glossary%20Onion.md#mapper). Mapper z domeny do DTO leży w Application Services. Mapper z DTO do view modelu i z wiersza bazy do domeny leży w pierścieniu zewnętrznym. Zasada jest prosta: mapowanie robi ta warstwa, która zna oba formaty.

## Co zapamiętać

- Interfejs repozytorium leży w rdzeniu, implementacja w infrastrukturze.
- Interfejs mówi językiem domeny, bo definiuje go rdzeń według własnych potrzeb.
- W Pythonie interfejsy wygodnie opisuje `Protocol`.
- Nawet zegar systemowy powinien być interfejsem, jeśli reguły zależą od daty.
- Wywołanie płynie na zewnątrz, zależność w kodzie do środka.
- Composition root w pierścieniu zewnętrznym tworzy i łączy wszystkie obiekty.
- Kontener DI jest opcjonalny, framework nie może wejść do rdzenia.
- Do UI wychodzą DTO i view modele, nie obiekty domeny.

## Pytania sprawdzające

### 12. W której warstwie definiuje się interfejs repozytorium, a w której jego implementację? Dlaczego?

<details>
<summary>Odpowiedź</summary>

Interfejs leży w rdzeniu: w warstwie Domain Services, jak u Palermo, albo w module domeny. Implementacja leży w infrastrukturze, w pierścieniu zewnętrznym. Rdzeń wie, jakich danych potrzebuje, więc to on definiuje kontrakt w swoim języku (`active_for`). Gdyby interfejs pochodził z infrastruktury, rdzeń musiałby ją importować i złamałby regułę zależności.

Zobacz: sekcja „Interfejs w środku, implementacja na zewnątrz”.

</details>

### 13. Jak w Onion realizowana jest zasada Dependency Inversion?

<details>
<summary>Odpowiedź</summary>

Application Service zależy od interfejsu `LoanRepository`, który należy do rdzenia, a `SqlLoanRepository` w infrastrukturze ten interfejs implementuje. Wywołanie w czasie działania płynie na zewnątrz (serwis → SQL → baza), a zależność w kodzie wskazuje do środka (implementacja → interfejs). Onion to DIP zastosowany do całej aplikacji.

Zobacz: sekcja „Zasada odwrócenia zależności”.

</details>

### 14. Gdzie w Onion jest composition root i kto tworzy obiekty infrastruktury?

<details>
<summary>Odpowiedź</summary>

W pierścieniu zewnętrznym, zwykle w module startowym (np. `bootstrap.py` albo `main.py`). Jest to jedyne miejsce, które zna wszystkie klasy. Tworzy implementacje repozytoriów, zegar i klientów usług, a potem wstrzykuje je do Application Services. Rdzeń nigdy sam nie tworzy obiektów infrastruktury. Dla testów i CLI można mieć osobne funkcje składające.

Zobacz: sekcja „Kto tworzy obiekty”.

</details>

### 15. Czy framework (Django, FastAPI, Spring, ASP.NET) może być zależnością wewnętrznych warstw?

<details>
<summary>Odpowiedź</summary>

Nie. Framework żyje wyłącznie w pierścieniu zewnętrznym: kontrolery, konfiguracja, kontener DI, implementacje repozytoriów. Sygnały przecieku to domena dziedzicząca po `models.Model`, adnotacje ORM, Application Service przyjmujący `Request`, użycie `settings` frameworka w domenie. Test: rdzeń da się uruchomić bez zainstalowanego frameworka.

Zobacz: sekcja „Kontener i framework”.

</details>

### 16. Jak przekazywać dane między warstwami: obiekty domeny, DTO czy view modele?

<details>
<summary>Odpowiedź</summary>

Obiekty domeny krążą wewnątrz rdzenia. Application Services zwracają na zewnątrz DTO (np. `LoanSummary`), a pierścień zewnętrzny zamienia je na view modele pod konkretny ekran lub API. Obiekty domeny nie powinny wychodzić do UI, bo widok zaczyna wtedy zależeć od kształtu domeny i może wywołać metody zmieniające stan. Mapowanie robi warstwa, która zna oba formaty.

Zobacz: sekcja „Dane na granicach warstw”.

</details>
