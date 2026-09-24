# Struktura projektu i granice

Pierścienie z diagramu trzeba zamienić na katalogi, pakiety albo projekty. Od tego wyboru zależy, czy reguła zależności będzie tylko umową w głowach zespołu, czy ograniczeniem, którego nie da się złamać przypadkiem. Ten rozdział pokazuje też, gdzie w cebuli trafiają walidacja, transakcje i wyjątki.

```text
Library.Domain          ◄── Library.Application ◄── Library.Infrastructure
(model + interfejsy)        (Application Services)   (SQL, zegar, e-mail)
      ▲                            ▲                          │
      └──────────── Library.Web ───┴──────────────────────────┘
                   (API + composition root)
```

## Pierścienie jako projekty w .NET

W .NET każdy pierścień to zwykle osobny projekt `.csproj`. Projekt może używać innego tylko wtedy, gdy ma do niego <a id="term-project-reference"></a>[referencję projektu](00%20Glossary%20Onion.md#project-reference). Kompilator nie pozwoli użyć klasy z projektu, do którego referencji nie ma.

```text
Library.sln
├── src/
│   ├── Library.Domain/            brak referencji do innych projektów
│   ├── Library.Application/       → Library.Domain
│   ├── Library.Infrastructure/    → Library.Domain, Library.Application
│   └── Library.Web/               → wszystkie (composition root)
└── tests/
    ├── Library.Domain.Tests/
    └── Library.Application.Tests/
```

```xml
<!-- Library.Application.csproj -->
<ItemGroup>
  <ProjectReference Include="..\Library.Domain\Library.Domain.csproj" />
</ItemGroup>
```

Jeśli ktoś w `Library.Domain` spróbuje użyć `DbContext` z Entity Framework, kod się nie skompiluje, bo projekt domeny nie ma tego pakietu. To najmocniejsza forma ochrony granic.

## Pierścienie jako pakiety w Pythonie

W Pythonie nie ma referencji projektów. Każdy moduł może zaimportować każdy inny, więc układ katalogów sam niczego nie gwarantuje:

```text
library/
├── domain/
│   ├── model.py               Book, Member, Loan
│   ├── services.py            LoanPolicy, FineCalculator
│   ├── repositories.py        interfejsy repozytoriów i Clock
│   └── errors.py
├── application/
│   ├── borrow_book.py
│   ├── return_book.py
│   └── dto.py
├── infrastructure/
│   ├── sql_repositories.py
│   ├── clock.py
│   └── bootstrap.py           composition root
└── web/
    └── api.py
```

Granicę trzeba więc pilnować narzędziem. Takie narzędzie uruchamia <a id="term-architecture-test"></a>[test architektury](00%20Glossary%20Onion.md#architecture-test) w CI. Dla Pythona służy do tego `import-linter`:

```toml
# pyproject.toml
[tool.importlinter]
root_package = "library"

[[tool.importlinter.contracts]]
name = "Pierścienie cebuli"
type = "layers"
layers = [
    "library.web | library.infrastructure",
    "library.application",
    "library.domain",
]

[[tool.importlinter.contracts]]
name = "Rdzeń bez bibliotek technicznych"
type = "forbidden"
source_modules = ["library.domain", "library.application"]
forbidden_modules = ["sqlalchemy", "fastapi", "django", "requests"]
```

Zapis `library.web | library.infrastructure` oznacza, że oba pakiety leżą w tym samym, zewnętrznym pierścieniu. Najmocniejszym wariantem w Pythonie są osobne paczki instalowane przez `pip` z własnym `pyproject.toml`. Paczka `library-domain` nie ma SQLAlchemy w zależnościach, więc import się nie powiedzie.

| Sposób | Język | Siła |
|---|---|---|
| Referencje projektów | .NET, Maven, Gradle | kompilator blokuje złamanie reguły |
| ArchUnit, NetArchTest | Java, .NET | test w CI |
| `import-linter` | Python | test w CI |
| Osobne paczki | Python | import się nie powiedzie |
| Konwencja w README | każdy | tylko dyscyplina zespołu |

## Walidacja w trzech pierścieniach

Każda warstwa sprawdza co innego. Walidacja formatu należy do pierścienia zewnętrznego: czy JSON ma pole `book_id`, czy to niepusty napis. W FastAPI robi to Pydantic:

```python
class BorrowRequest(BaseModel):
    member_id: str = Field(min_length=1)
    book_id: str = Field(min_length=1)
```

Application Services sprawdzają fakty, które wymagają repozytoriów: czy członek istnieje, czy książka jest w katalogu.

Domena pilnuje <a id="term-invariant"></a>[niezmienników](00%20Glossary%20Onion.md#invariant), czyli warunków, które muszą być prawdziwe zawsze, niezależnie od tego, kto wywołał kod. Książki wypożyczonej nie można wypożyczyć drugi raz. Tego pilnuje `Book.lend()`, a nie kontroler, bo scenariusz może przyjść także z CLI albo z kolejki.

| Rodzaj | Przykład | Pierścień |
|---|---|---|
| Format | pole jest napisem, JSON jest poprawny | zewnętrzny |
| Aplikacyjna | członek istnieje | Application Services |
| Biznesowa | książka nie jest już wypożyczona, limit wypożyczeń | Domain Model, Domain Services |

## Transakcje bez wiedzy o bazie

Wypożyczenie zmienia dwie rzeczy: książkę (`available = False`) i listę wypożyczeń. Obie zmiany muszą się zapisać razem albo wcale. Application Service nie może jednak importować sesji SQLAlchemy.

Rozwiązaniem jest <a id="term-unit-of-work"></a>[Unit of Work](00%20Glossary%20Onion.md#unit-of-work): interfejs w rdzeniu, który grupuje repozytoria i zatwierdza zmiany jedną operacją.

```python
# domain/repositories.py
class UnitOfWork(Protocol):
    books: BookRepository
    loans: LoanRepository

    def __enter__(self) -> "UnitOfWork": ...
    def __exit__(self, *exc) -> None: ...
    def commit(self) -> None: ...
```

```python
# application/borrow_book.py
class BorrowBookService:
    def __init__(self, uow: UnitOfWork, policy: LoanPolicy, clock: Clock):
        self._uow = uow
        self._policy = policy
        self._clock = clock

    def borrow(self, member_id: str, book_id: str) -> str:
        today = self._clock.today()
        with self._uow as uow:
            if not self._policy.can_borrow(uow.loans.active_for(member_id), today):
                raise BorrowingBlocked(member_id)
            book = uow.books.get(book_id)
            book.lend()
            loan = Loan(id=str(uuid4()), book_id=book.id, member_id=member_id, borrowed_on=today)
            uow.books.save(book)
            uow.loans.add(loan)
            uow.commit()
        return loan.id
```

Application Service wyznacza granicę transakcji, a implementacja w infrastrukturze realizuje ją na sesji bazy. Domain Model i Domain Services nie wiedzą, że transakcje istnieją.

```python
# infrastructure/sql_uow.py
class SqlUnitOfWork:
    def __init__(self, session_factory):
        self._session_factory = session_factory

    def __enter__(self):
        self._session = self._session_factory()
        self.books = SqlBookRepository(self._session)
        self.loans = SqlLoanRepository(self._session)
        return self

    def __exit__(self, *exc):
        self._session.rollback()       # bez efektu po udanym commit
        self._session.close()

    def commit(self):
        self._session.commit()
```

## Wyjątki i ich tłumaczenie

Domena zgłasza problemy przez <a id="term-domain-exception"></a>[wyjątki domenowe](00%20Glossary%20Onion.md#domain-exception) nazwane językiem biznesu. Nie zna kodów HTTP ani wyjątków bibliotek:

```python
# domain/errors.py
class LibraryError(Exception):
    pass


class BookNotFound(LibraryError):
    pass


class BookAlreadyLent(LibraryError):
    pass


class BorrowingBlocked(LibraryError):
    def __init__(self, member_id: str):
        super().__init__(f"Członek {member_id} ma zablokowane wypożyczenia")
```

W pierścieniu zewnętrznym zachodzą dwa tłumaczenia. Implementacja repozytorium zamienia problemy technologii na wyjątki domenowe, na przykład brak wiersza na `BookNotFound`. API zamienia wyjątki domenowe na kody protokołu:

```python
STATUS = {BookNotFound: 404, BookAlreadyLent: 409, BorrowingBlocked: 403}


@app.exception_handler(LibraryError)
def library_error(request, exc: LibraryError):
    return JSONResponse(
        status_code=STATUS.get(type(exc), 400),
        content={"error": type(exc).__name__, "message": str(exc)},
    )
```

Wyjątek domenowy przechodzi z rdzenia do pierścienia zewnętrznego, bo to zgodne z kierunkiem zależności: zewnętrzny kod zna typy z rdzenia. Klient HTTP nie widzi jednak ani wyjątku, ani tracebacku, tylko kod statusu i komunikat.

## Co zapamiętać

- W .NET pierścienie to projekty, a referencje projektów wymuszają regułę zależności w kompilatorze.
- W Pythonie granice pilnuje `import-linter` w CI albo podział na osobne paczki.
- UI i infrastruktura to jeden zewnętrzny pierścień, który może zależeć od wszystkiego.
- Format waliduje pierścień zewnętrzny, istnienie danych sprawdzają Application Services, niezmienników pilnuje domena.
- Unit of Work to interfejs w rdzeniu, dzięki któremu Application Service wyznacza transakcję bez wiedzy o bazie.
- Repozytoria tłumaczą błędy technologii na wyjątki domenowe, a API tłumaczy je na kody protokołu.

## Pytania sprawdzające

### 17. Jak odwzorować warstwy Onion w strukturze katalogów lub projektów (np. osobne projekty w .NET, pakiety w Pythonie)?

<details>
<summary>Odpowiedź</summary>

W .NET każdy pierścień to osobny projekt: `Domain` bez referencji, `Application` z referencją do `Domain`, `Infrastructure` z referencjami do obu i `Web` jako composition root, który widzi wszystko. W Pythonie są to pakiety `domain` (model, serwisy domenowe, interfejsy repozytoriów), `application`, `infrastructure` i `web`, a dla najmocniejszej izolacji osobne paczki instalowalne.

Zobacz: sekcje „Pierścienie jako projekty w .NET” i „Pierścienie jako pakiety w Pythonie”.

</details>

### 18. Jak wymusić, żeby wewnętrzne warstwy nie importowały zewnętrznych (referencje projektów, import-linter, ArchUnit)?

<details>
<summary>Odpowiedź</summary>

Najmocniej przez referencje projektów w .NET, Mavenie lub Gradle, bo wtedy kompilator nie pozwoli użyć klasy z projektu bez referencji. W Javie i .NET można dodać testy ArchUnit albo NetArchTest. W Pythonie `import-linter` w CI z kontraktem `layers` (web i infrastruktura → application → domain) oraz `forbidden` (rdzeń bez `sqlalchemy`, `fastapi` itd.), albo osobne paczki bez technicznych zależności. Sama konwencja w README to za mało.

Zobacz: sekcja „Pierścienie jako pakiety w Pythonie” i tabela na jej końcu.

</details>

### 19. Gdzie umieścić walidację, transakcje i obsługę wyjątków w modelu warstw Onion?

<details>
<summary>Odpowiedź</summary>

Walidacja ma trzy poziomy: format w pierścieniu zewnętrznym (Pydantic), fakty wymagające repozytoriów w Application Services, niezmienniki w Domain Model i Domain Services. Transakcje wyznacza Application Service przez interfejs Unit of Work z rdzenia, a realizuje je implementacja w infrastrukturze. Wyjątki domenowe powstają w rdzeniu. Infrastruktura tłumaczy błędy technologii na wyjątki domenowe, a API tłumaczy wyjątki domenowe na kody HTTP.

Zobacz: sekcje „Walidacja w trzech pierścieniach”, „Transakcje bez wiedzy o bazie” i „Wyjątki i ich tłumaczenie”.

</details>
