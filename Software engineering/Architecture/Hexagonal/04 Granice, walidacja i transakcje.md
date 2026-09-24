# Granice, walidacja i transakcje

Granica między rdzeniem a adapterami istnieje tylko wtedy, gdy ktoś jej pilnuje. Ten rozdział opisuje, jak utrzymać ją w kodzie i jak rozwiązać trzy praktyczne problemy, które pojawiają się na każdej granicy: walidację, transakcje i błędy.

```text
żądanie HTTP
    ↓
adapter: format i typy          → 422 przy złym JSON-ie
    ↓
use case: transakcja            → commit albo rollback
    ↓
domena: reguły biznesowe        → wyjątek domenowy
    ↓
adapter: tłumaczenie błędu      → 409 / 404 / 400
```

## Automatyczne pilnowanie importów

Reguła zależności zapisana tylko w README szybko się rozmywa. Lepiej zamienić ją w <a id="term-architecture-test"></a>[test architektury](00%20Glossary%20Hexagonal.md#architecture-test), który uruchamia się w CI i pada, gdy ktoś zaimportuje adapter w domenie.

W Pythonie służy do tego `import-linter`. Kontrakt zapisuje się w `pyproject.toml`:

```toml
[tool.importlinter]
root_package = "shop"

[[tool.importlinter.contracts]]
name = "Warstwy heksagonu"
type = "layers"
layers = [
    "shop.adapters",
    "shop.application",
    "shop.domain",
]

[[tool.importlinter.contracts]]
name = "Domena bez bibliotek technicznych"
type = "forbidden"
source_modules = ["shop.domain", "shop.application"]
forbidden_modules = ["sqlalchemy", "fastapi", "stripe", "requests"]
```

```bash
lint-imports
```

W Javie tę samą rolę pełni ArchUnit, w .NET NetArchTest. Najmocniejszym wariantem są osobne paczki: `shop-domain` nie ma w zależnościach `sqlalchemy`, więc import po prostu się nie powiedzie.

| Sposób | Siła | Koszt |
|---|---|---|
| Konwencja w README | słaba | zerowy |
| `import-linter` / ArchUnit w CI | dobra | mały |
| Osobne paczki lub moduły budowania | pełna | większy narzut projektu |

## Trzy poziomy walidacji

Pytanie „gdzie walidować” ma trzy odpowiedzi, bo są trzy rodzaje sprawdzeń.

Walidacja formatu należy do adaptera wejściowego. Sprawdza, czy JSON ma pola, czy `quantity` jest liczbą, czy e-mail ma poprawną składnię. W FastAPI robi to Pydantic:

```python
from pydantic import BaseModel, Field


class ItemRequest(BaseModel):
    sku: str = Field(min_length=1)
    quantity: int = Field(gt=0)


class PlaceOrderRequest(BaseModel):
    customer_id: str
    items: list[ItemRequest] = Field(min_length=1)
```

Walidacja aplikacyjna należy do use case'u. Sprawdza rzeczy, które wymagają portów: czy klient istnieje, czy produkt jest w cenniku.

Reguły biznesowe należą do domeny. Są to <a id="term-invariant"></a>[niezmienniki](00%20Glossary%20Hexagonal.md#invariant), czyli warunki, które obiekt musi spełniać zawsze, niezależnie od tego, kto go wywołał:

```python
def add_line(self, sku: str, quantity: int, unit_price: Money) -> None:
    if self.status is not OrderStatus.DRAFT:
        raise OrderError("Można edytować tylko szkic zamówienia")
    if quantity <= 0:
        raise OrderError("Ilość musi być dodatnia")
    self.lines.append(OrderLine(sku, quantity, unit_price))
```

Sprawdzenie `quantity > 0` występuje w adapterze i w domenie. To nie jest błąd. Adapter daje szybką, czytelną odpowiedź 422 dla HTTP, a domena chroni regułę także przed wywołaniem z CLI albo kolejki, które nie przechodzą przez Pydantic.

| Rodzaj | Przykład | Miejsce |
|---|---|---|
| Format | pole jest liczbą, JSON ma `items` | adapter wejściowy |
| Aplikacyjna | klient istnieje, SKU jest w cenniku | use case |
| Biznesowa | nie można edytować złożonego zamówienia | domena |

## Transakcja bez wiedzy o bazie

Use case musi zapisać zamówienie atomowo, ale nie może importować sesji SQLAlchemy. Rozwiązaniem jest <a id="term-unit-of-work"></a>[Unit of Work](00%20Glossary%20Hexagonal.md#unit-of-work): port wyjściowy, który grupuje zmiany i zatwierdza je razem.

```python
# application/ports.py
from typing import Protocol


class UnitOfWork(Protocol):
    orders: OrderRepository

    def __enter__(self) -> "UnitOfWork": ...
    def __exit__(self, *exc) -> None: ...
    def commit(self) -> None: ...
```

Use case określa granicę transakcji, ale nie wie, jak jest realizowana:

```python
class PlaceOrderHandler:
    def __init__(self, uow: UnitOfWork, prices: PriceList):
        self._uow = uow
        self._prices = prices

    def __call__(self, command: PlaceOrderCommand) -> str:
        with self._uow as uow:
            order = Order(customer_id=command.customer_id)
            for sku, quantity in command.items:
                order.add_line(sku, quantity, self._prices.price_of(sku))
            order.place()
            uow.orders.save(order)
            uow.commit()
        return order.id
```

Adapter dla SQLAlchemy otwiera sesję, podaje repozytorium i wycofuje zmiany, jeśli `commit()` nie zostało wywołane:

```python
class SqlUnitOfWork:
    def __init__(self, session_factory):
        self._session_factory = session_factory

    def __enter__(self):
        self._session = self._session_factory()
        self.orders = SqlOrderRepository(self._session)
        return self

    def __exit__(self, *exc):
        self._session.rollback()      # no-op po udanym commit
        self._session.close()

    def commit(self):
        self._session.commit()
```

Transakcja obejmuje tylko bazę. Płatność w Stripe albo e-mail nie wycofają się razem z rollbackiem. Dlatego takie efekty uboczne wykonuje się po commicie albo przez zdarzenia, co opisuje rozdział 07.

## Błędy na granicy

Domena zgłasza problem przez <a id="term-domain-exception"></a>[wyjątek domenowy](00%20Glossary%20Hexagonal.md#domain-exception), nazwany w języku biznesu. Nie zwraca kodów HTTP i nie rzuca wyjątków bibliotek technicznych:

```python
# domain/errors.py
class DomainError(Exception):
    pass


class OrderError(DomainError):        # z rozdziału 03, teraz ze wspólną bazą
    pass


class OrderNotFound(DomainError):
    def __init__(self, order_id: str):
        super().__init__(f"Zamówienie {order_id} nie istnieje")
        self.order_id = order_id


class OrderAlreadyPlaced(OrderError):
    pass
```

Wspólna klasa bazowa `DomainError` pozwala adapterowi obsłużyć wszystkie błędy rdzenia w jednym miejscu.

Adapter wyjściowy tłumaczy błędy technologii na błędy rdzenia. Brak wiersza nie może wypłynąć do use case'u jako `None` ani jako `NoResultFound` z SQLAlchemy:

```python
def get(self, order_id: str) -> Order:
    row = self._session.get(OrderRow, order_id)
    if row is None:
        raise OrderNotFound(order_id)
    return to_domain(row)
```

Adapter wejściowy tłumaczy błędy rdzenia na protokół. W FastAPI wystarczy jeden handler na typ wyjątku:

```python
ERROR_STATUS = {
    OrderNotFound: 404,
    OrderAlreadyPlaced: 409,
    OrderError: 400,
}


@app.exception_handler(DomainError)
def handle_domain_error(request, exc: DomainError):
    status = ERROR_STATUS.get(type(exc), 400)
    return JSONResponse(status_code=status, content={"error": type(exc).__name__, "message": str(exc)})
```

Wyjątki domenowe mogą przejść przez granicę rdzenia, ale nie przez granicę protokołu. Klient HTTP dostaje kod statusu i czytelny komunikat, a nie traceback z nazwą klasy SQLAlchemy.

## Co zapamiętać

- Regułę zależności utrzymuje test architektury w CI albo podział na osobne paczki.
- Format waliduje adapter, fakty wymagające portów sprawdza use case, niezmienniki pilnuje domena.
- Powtórzona walidacja w adapterze i domenie jest celowa.
- Unit of Work pozwala use case'owi wyznaczyć transakcję bez znajomości bazy.
- Efekty zewnętrzne, jak płatność czy e-mail, nie wycofują się rollbackiem.
- Adapter wyjściowy tłumaczy wyjątki technologii na wyjątki domenowe.
- Adapter wejściowy tłumaczy wyjątki domenowe na kody protokołu.

## Pytania sprawdzające

### 20. Jak wymusić granice architektoniczne w kodzie (ArchUnit, import-linter, osobne moduły lub paczki)?

<details>
<summary>Odpowiedź</summary>

Zamienić konwencję w automatyczny test architektury uruchamiany w CI. W Pythonie `import-linter` z kontraktem `layers` (adapters → application → domain) i `forbidden` (domena nie importuje `sqlalchemy`, `fastapi` itd.), w Javie ArchUnit. Najmocniejszy wariant to osobne paczki lub moduły budowania: jeśli paczka domeny nie ma biblioteki w zależnościach, zakazany import się nie powiedzie.

Zobacz: sekcja „Automatyczne pilnowanie importów”.

</details>

### 21. Gdzie umieścić walidację: w adapterze, w use case czy w domenie?

<details>
<summary>Odpowiedź</summary>

W każdym z tych miejsc, ale każdy poziom sprawdza co innego. Adapter waliduje format (typy, wymagane pola). Use case sprawdza fakty, które wymagają portów (czy klient istnieje). Domena pilnuje niezmienników, czyli reguł, które muszą być prawdziwe zawsze. Częściowe powtórzenie jest celowe: adapter daje czytelną odpowiedź 422, a domena chroni regułę także przed wywołaniem z CLI czy kolejki.

Zobacz: sekcja „Trzy poziomy walidacji”.

</details>

### 22. Jak obsługiwać transakcje, skoro domena nie powinna wiedzieć o bazie danych?

<details>
<summary>Odpowiedź</summary>

Przez port Unit of Work. Use case wyznacza granicę transakcji (`with uow:` … `uow.commit()`), a adapter, np. `SqlUnitOfWork`, realizuje ją na sesji bazy i wycofuje zmiany, jeśli commit nie nastąpił. Transakcja obejmuje tylko bazę, więc zewnętrzne efekty, jak płatność czy e-mail, trzeba wykonywać po commicie albo przez zdarzenia.

Zobacz: sekcja „Transakcja bez wiedzy o bazie”.

</details>

### 23. Jak obsługiwać wyjątki i błędy na granicy portów? Czy wyjątki domenowe mogą przeciekać do HTTP?

<details>
<summary>Odpowiedź</summary>

Domena rzuca wyjątki domenowe nazwane w języku biznesu (`OrderNotFound`, `OrderAlreadyPlaced`). Adapter wyjściowy tłumaczy wyjątki technologii (np. brak wiersza w SQLAlchemy) na wyjątki domenowe. Adapter wejściowy mapuje wyjątki domenowe na kody protokołu (404, 409, 400). Wyjątek domenowy może więc dotrzeć do adaptera HTTP, ale do klienta trafia kod statusu i komunikat, a nie wyjątek czy traceback.

Zobacz: sekcja „Błędy na granicy”.

</details>
