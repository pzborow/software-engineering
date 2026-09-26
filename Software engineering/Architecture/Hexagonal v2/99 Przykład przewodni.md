# Przykład przewodni: Wypożyczalnia rowerów „Rowerek”

Miejska wypożyczalnia rowerów: użytkownicy rezerwują i wypożyczają rowery na stacjach, zwracają je i płacą za czas jazdy. Reguły: limit jednego aktywnego wypożyczenia, blokada przy zaległej płatności, cennik z darmowymi pierwszymi 20 minutami, opłata kary za zwrot poza stacją. Integracje: baza SQL, bramka płatności, powiadomienia SMS/e-mail, kolejka wiadomości z IoT zamków rowerowych.

**Dokąd zmierza:** Zaczynamy od prostego, sprzężonego z ORM kodu wypożyczania i wyodrębniamy z niego rdzeń: encje, porty i use case'y. Potem dokładamy adaptery (FastAPI, SQLAlchemy, bramka płatności), okablowanie w composition root i testy na fake'ach z testami kontraktowymi. Na końcu dodajemy Unit of Work, zdarzenia z Outboxem, konsumenta wiadomości z zamków oraz import-linter i strategię migracji monolitu.

## Plan przyrostów

| Dział | Co przybywa |
|---|---|
| [01. Podstawy i motywacja](01%20Podstawy%20i%20motywacja.md) | Pokazujemy początkowy, sprzężony kod wypożyczania (widok FastAPI + model ORM + wywołanie Stripe) jako motywację i szkicujemy heksagon z Rental, Bike, User i PricingPolicy w środku. |
| [02. Porty](02%20Porty.md) | Definiujemy porty: wejściowy StartRental oraz wyjściowe RentalRepository i PaymentGateway, raz jako ABC i raz jako Protocol, z własnością w rdzeniu. |
| [03. Adaptery](03%20Adaptery.md) | Dodajemy adaptery: rentals_router, SqlAlchemyRentalRepository z mapowaniem RentalRow na Rental oraz StripePaymentGateway z tłumaczeniem wyjątków na błędy rdzenia. |
| [04. Domena i warstwa aplikacji](04%20Domena%20i%20warstwa%20aplikacji.md) | Wypełniamy rdzeń: reguły w encjach i PricingPolicy oraz use case'y StartRental i FinishRental zwracające wyniki domenowe zamiast odpowiedzi HTTP. |
| [05. Wstrzykiwanie zależności i kompozycja](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md) | Wiążemy całość w composition root (ręczny konstruktor, potem FastAPI Depends i opcjonalnie kontener DI) z zarządzaniem cyklem życia sesji SQL. |
| [06. Testowanie](06%20Testowanie.md) | Testujemy StartRental i FinishRental na fake'ach, dodajemy testy kontraktowe RentalRepository uruchamiane na fake'u i SQL oraz test endpointu z podmienionym use case'em. |
| [07. Transakcje, zdarzenia i asynchroniczność](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md) | Wprowadzamy UnitOfWork, zdarzenia domenowe (RentalFinished) z Outboxem oraz idempotentny LockEventConsumer i asynchroniczne porty bez async w domenie. |
| [08. Praktyka i kompromisy](08%20Praktyka%20i%20kompromisy.md) | Układamy pakiety domain/application/adapters, wymuszamy kierunek zależności import-linterem i omawiamy migrację monolitu oraz odczyty CQRS omijające porty domeny. |

## Stan kodu po ostatnim dziale

Szkic, nie działający kod: nazwy i sygnatury, których trzymają się przykłady w tekście.

### `app/composition.py`

```python
def build_finish_rental(session: Session) -> FinishRental: ...

def get_finish_rental(session: Session = Depends(get_session)) -> FinishRental: ...

def get_start_rental(session: Session = Depends(get_session)) -> StartRental: ...
```

- **build_finish_rental** (inne): Funkcja w composition root składająca FinishRental z adapterów SQLAlchemy i Stripe. Wprowadzony: [05 › Composition root: gdzie go umieścić](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#composition-root-gdzie-go-umieścić).
- **get_finish_rental** (inne): Provider FastAPI delegujący do build_finish_rental, używany w Depends przez router. Wprowadzony: [05 › FastAPI Depends w okablowaniu](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#fastapi-depends-w-okablowaniu).
- **get_start_rental** (inne): Dependency budujące StartRental, które test endpointu podmienia przez dependency_overrides. Wprowadzony: [06 › Testowanie endpointu HTTP](06%20Testowanie.md#testowanie-endpointu-http).

### `app/queries.py`

```python
class RentalHistoryQuery:
    def __init__(self, session: Session) -> None: ...
    def __call__(self, user_id: str) -> list[RentalSummary]: ...
```

- **RentalHistoryQuery** (przypadek użycia): Zapytanie czytające historię wypożyczeń wprost SQL-em, z pominięciem encji i portów. Wprowadzony: [08 › Odczyty CQRS a porty domeny](08%20Praktyka%20i%20kompromisy.md#odczyty-cqrs-a-porty-domeny).

### `core/entities.py`

```python
@dataclass
class Rental:
    id: str
    bike_id: str
    user_id: str

@dataclass
class Bike:
    id: str
    station_id: str | None

@dataclass
class User:
    id: str
    has_overdue_payment: bool
```

- **Rental** (encja): Wypożyczenie; szkic wnętrza heksagonu, rozwijany w kolejnych sekcjach. Wprowadzony: [01 › Problem: logika uwięziona w infrastrukturze](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze).
- **Bike** (encja): Rower; element rdzenia. Wprowadzony: [01 › Problem: logika uwięziona w infrastrukturze](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze).
- **User** (encja): Użytkownik; element rdzenia. Wprowadzony: [01 › Problem: logika uwięziona w infrastrukturze](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze).

### `core/events.py`

```python
@dataclass(frozen=True)
class RentalFinished:
    rental_id: str
    user_id: str
    fee: Money
```

- **RentalFinished** (obiekt wartości): Zdarzenie domenowe: fakt zakończenia wypożyczenia wraz z naliczoną opłatą. Wprowadzony: [07 › Zdarzenia domenowe i port publikacji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji).

### `core/ports.py`

```python
class RentalRepository(ABC):
    @abstractmethod
    def add(self, rental: Rental) -> None: ...
    @abstractmethod
    def active_for_user(self, user_id: str) -> Rental | None: ...

class PaymentGateway(Protocol):
    def charge(self, user_id: str, amount: Money) -> None: ...

class UnitOfWork(ABC):
    rentals: RentalRepository
    @abstractmethod
    def publish(self, event: DomainEvent) -> None: ...
    @abstractmethod
    def commit(self) -> None: ...

class PaymentDeclined(Exception): ...

class PaymentUnavailable(Exception): ...
```

- **RentalRepository** (port): Port, przez który rdzeń zapisuje i odczytuje wypożyczenia, nie znając bazy. Wprowadzony: [01 › Wnętrze i zewnętrze heksagonu](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu).
  - zmiana w [02 › Port jako klasa ABC](02%20Porty.md#port-jako-klasa-abc): Pokazujemy wariant ABC (jawne dziedziczenie); sygnatury metod bez zmian, zmienia się tylko baza klasy z Protocol na ABC.
- **PaymentGateway** (port): Port wyjściowy: rdzeń prosi o obciążenie użytkownika, nie znając dostawcy płatności. Wprowadzony: [02 › Czym jest port](02%20Porty.md#czym-jest-port).
- **UnitOfWork** (port): Port granicy spójności: udostępnia repozytoria, zatwierdza lub cofa zmiany scenariusza. Wprowadzony: [07 › Unit of Work jako port](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#unit-of-work-jako-port).
  - zmiana w [07 › Zdarzenia domenowe i port publikacji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji): Zdarzenie ma być częścią scenariusza, więc UoW przyjmuje je przed commit i przekazuje adapterowi.
- **PaymentDeclined** (inne): Błąd rdzenia: płatność odrzucona, nie ponawiać. Wprowadzony: [03 › Tłumaczenie wyjątków w adapterze](03%20Adaptery.md#tłumaczenie-wyjątków-w-adapterze).
- **PaymentUnavailable** (inne): Błąd rdzenia: awaria przejściowa bramki, można ponowić. Wprowadzony: [03 › Tłumaczenie wyjątków w adapterze](03%20Adaptery.md#tłumaczenie-wyjątków-w-adapterze).

### `core/pricing.py`

```python
@dataclass(frozen=True)
class Money:
    amount: Decimal
    currency: str

@dataclass(frozen=True)
class PricingPolicy:
    free_minutes: int = 20
    def fee(self, minutes: int) -> Money: ...
```

- **Money** (obiekt wartości): Kwota w typach rdzenia, używana w sygnaturze portu zamiast typu dostawcy. Wprowadzony: [02 › Czym jest port](02%20Porty.md#czym-jest-port).
- **PricingPolicy** (obiekt wartości): Cennik z darmowymi 20 minutami; element rdzenia. Wprowadzony: [01 › Problem: logika uwięziona w infrastrukturze](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze).
  - zmiana w [04 › Logika domenowa a aplikacyjna](04%20Domena%20i%20warstwa%20aplikacji.md#logika-domenowa-a-aplikacyjna): Dodajemy metodę fee, by reguła cennika była logiką domenową wywoływaną przez FinishRental.

### `core/use_cases.py`

```python
class StartRental:
    def __init__(self, uow: UnitOfWork) -> None: ...
    def __call__(self, user_id: str, bike_id: str) -> Rental: ...

class FinishRental:
    def __init__(self, uow: UnitOfWork, payments: PaymentGateway) -> None: ...
    def __call__(self, rental_id: str) -> Money: ...
```

- **StartRental** (przypadek użycia): Scenariusz rozpoczęcia wypożyczenia, który egzekwuje reguły i korzysta wyłącznie z portów. Wprowadzony: [01 › Wnętrze i zewnętrze heksagonu](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu).
  - zmiana w [07 › Unit of Work jako port](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#unit-of-work-jako-port): Scenariusz potrzebuje granicy spójności, więc konstruktor przyjmuje UnitOfWork zamiast RentalRepository.
- **FinishRental** (przypadek użycia): Kończy wypożyczenie i wywołuje charge, więc obsługuje błędy płatności. Wprowadzony: [03 › Tłumaczenie wyjątków w adapterze](03%20Adaptery.md#tłumaczenie-wyjątków-w-adapterze).
  - zmiana w [07 › Granica transakcji: use case czy adapter](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#granica-transakcji-use-case-czy-adapter): Zamiast RentalRepository przyjmuje UnitOfWork, by use case, a nie adapter, decydował o commit i rollback.

### `infra/async_payment_gateway.py`

```python
class AsyncStripePaymentGateway:
    def __init__(self, client, loop: asyncio.AbstractEventLoop) -> None: ...
    def charge(self, user_id: str, amount: Money) -> None: ...
```

- **AsyncStripePaymentGateway** (adapter): Synchroniczny PaymentGateway mostkujący klienta async przez run_coroutine_threadsafe. Wprowadzony: [07 › Asynchroniczność na brzegu, nie w domenie](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#asynchroniczność-na-brzegu-nie-w-domenie).

### `infra/lock_consumer.py`

```python
class LockEventConsumer:
    def __init__(self, session_factory, build_finish_rental) -> None: ...
    def handle(self, message: bytes) -> None: ...

class ProcessedMessageRow(Base):
    message_id: str  # klucz główny, unikalny
```

- **LockEventConsumer** (adapter): Adapter wejściowy: odbiera wiadomość z zamka IoT i wywołuje przypadek użycia. Wprowadzony: [03 › Adaptery wejściowe w Pythonie](03%20Adaptery.md#adaptery-wejściowe-w-pythonie).
  - zmiana w [07 › Idempotentny konsument wiadomości](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#idempotentny-konsument-wiadomości): Konkretyzuje konstruktor z kanonu (`...`) o zależności potrzebne do deduplikacji na jednej sesji.
- **ProcessedMessageRow** (inne): Znacznik przetworzonej wiadomości; unikalny klucz wykrywa duplikat. Wprowadzony: [07 › Idempotentny konsument wiadomości](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#idempotentny-konsument-wiadomości).

### `infra/rentals_router.py`

```python
router = APIRouter()

@router.post("/rentals")
def start_rental(body: StartRentalRequest, use_case: StartRental = Depends(...)) -> RentalResponse: ...

@router.post("/rentals")
def start_rental(body: StartRentalRequest, user: AuthUser = Depends(current_user), use_case: StartRental = Depends(...)) -> RentalResponse: ...
```

- **rentals_router** (adapter): Adapter wejściowy: przyjmuje HTTP i wywołuje przypadek użycia StartRental. Wprowadzony: [03 › Czym jest adapter](03%20Adaptery.md#czym-jest-adapter).
- **start_rental** (adapter): Cienki handler: tożsamość z uwierzytelnienia, jedno wywołanie przypadku użycia, mapowanie na DTO. Wprowadzony: [03 › Zakres adaptera wejściowego](03%20Adaptery.md#zakres-adaptera-wejściowego).

### `infra/sqlalchemy_rentals.py`

```python
class SqlAlchemyRentalRepository(RentalRepository):
    def __init__(self, session: Session) -> None: ...
    def add(self, rental: Rental) -> None: ...
    def active_for_user(self, user_id: str) -> Rental | None: ...
    @staticmethod
    def _to_domain(row: RentalRow) -> Rental: ...
```

- **SqlAlchemyRentalRepository** (adapter): Implementuje RentalRepository w SQL, importuje z rdzenia, a nie odwrotnie. Wprowadzony: [01 › Kierunek zależności: do rdzenia](01%20Podstawy%20i%20motywacja.md#kierunek-zależności-do-rdzenia).
  - zmiana w [02 › Port jako klasa ABC](02%20Porty.md#port-jako-klasa-abc): W wariancie ABC adapter musi jawnie dziedziczyć po porcie; pozostałe sygnatury bez zmian.
  - zmiana w [03 › Mapowanie modeli zewnętrznych](03%20Adaptery.md#mapowanie-modeli-zewnętrznych): Dodano prywatną metodę mapującą _to_domain; sygnatury portu bez zmian.

### `infra/sqlalchemy_uow.py`

```python
class SqlAlchemyUnitOfWork(UnitOfWork):
    def publish(self, event: DomainEvent) -> None: ...

class OutboxRow(Base):
    type: str
    payload: str
    sent_at: datetime | None
```

- **SqlAlchemyUnitOfWork.publish** (adapter): Zapisuje zdarzenie do tabeli outbox w bieżącej sesji, więc trafia do tej samej transakcji co zmiana stanu. Wprowadzony: [07 › Outbox: zdarzenia w tej samej transakcji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#outbox-zdarzenia-w-tej-samej-transakcji).
- **OutboxRow** (inne): Model trwałości wiersza outboxa czytany przez relay. Wprowadzony: [07 › Outbox: zdarzenia w tej samej transakcji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#outbox-zdarzenia-w-tej-samej-transakcji).

### `infra/stripe_gateway.py`

```python
class StripePaymentGateway:
    def charge(self, user_id: str, amount: Money) -> None: ...
```

- **StripePaymentGateway** (adapter): Adapter bramki płatności bez dziedziczenia po porcie. Wprowadzony: [02 › Protocol zamiast ABC](02%20Porty.md#protocol-zamiast-abc).

### `tests/fakes.py`

```python
class InMemoryRentalRepository(RentalRepository):
    def __init__(self) -> None: ...
    def add(self, rental: Rental) -> None: ...
    def active_for_user(self, user_id: str) -> Rental | None: ...

class FakePaymentGateway:
    def __init__(self, fail_with: Exception | None = None) -> None: ...
    def charge(self, user_id: str, amount: Money) -> None: ...
    charged: list[tuple[str, Money]]
```

- **InMemoryRentalRepository** (adapter): Fake repozytorium w pamięci, którym testy podmieniają SqlAlchemyRentalRepository. Wprowadzony: [06 › Testy use case'ów bez infrastruktury](06%20Testowanie.md#testy-use-caseów-bez-infrastruktury).
- **FakePaymentGateway** (adapter): Fake bramki płatności zapamiętujący obciążenia i zgłaszający wstrzyknięty błąd, np. PaymentDeclined. Wprowadzony: [06 › Kiedy fake, a kiedy mock](06%20Testowanie.md#kiedy-fake-a-kiedy-mock).
