# Struktura kodu

Architektura heksagonalna nie narzuca jednego układu katalogów. Narzuca tylko kierunek zależności. Poniższy układ jest jednym z najczęstszych i dobrze pasuje do projektu w Pythonie.

```text
shop/
├── domain/                     reguły biznesowe, zero zależności technicznych
│   ├── money.py
│   ├── order.py
│   └── pricing.py
├── application/                scenariusze i porty
│   ├── ports.py                porty wyjściowe
│   └── place_order.py          use case = port wejściowy
├── adapters/
│   ├── inbound/                wywołują aplikację
│   │   ├── http.py
│   │   └── cli.py
│   └── outbound/               są wywoływane przez aplikację
│       ├── sql_orders.py
│       ├── stripe_payments.py
│       └── email_notifier.py
└── main.py                     składanie całości
```

Kierunek importów jest jeden:

```text
adapters ──► application ──► domain
main.py  ──► wszystko
```

## Domena: czysty Python

W katalogu `domain` są obiekty biznesowe z zachowaniem. Nie importują niczego spoza biblioteki standardowej. Najpierw kwota, która pilnuje waluty i zaokrągleń:

```python
# domain/money.py
from dataclasses import dataclass
from decimal import Decimal


@dataclass(frozen=True)
class Money:
    amount: Decimal
    currency: str

    @classmethod
    def zero(cls, currency: str) -> "Money":
        return cls(Decimal("0"), currency)

    def __add__(self, other: "Money") -> "Money":
        if other.currency != self.currency:
            raise ValueError("Nie można dodać kwot w różnych walutach")
        return Money(self.amount + other.amount, self.currency)

    def __mul__(self, factor: int | Decimal) -> "Money":
        return Money((self.amount * factor).quantize(Decimal("0.01")), self.currency)
```

Potem zamówienie:

```python
# domain/order.py
from dataclasses import dataclass, field
from enum import Enum
from uuid import uuid4

from shop.domain.money import Money


class OrderStatus(Enum):
    DRAFT = "draft"
    PLACED = "placed"
    CANCELLED = "cancelled"


class OrderError(Exception):
    pass


@dataclass
class OrderLine:
    sku: str
    quantity: int
    unit_price: Money


@dataclass
class Order:
    customer_id: str
    id: str = field(default_factory=lambda: str(uuid4()))
    lines: list[OrderLine] = field(default_factory=list)
    status: OrderStatus = OrderStatus.DRAFT

    def add_line(self, sku: str, quantity: int, unit_price: Money) -> None:
        if self.status is not OrderStatus.DRAFT:
            raise OrderError("Można edytować tylko szkic zamówienia")
        if quantity <= 0:
            raise OrderError("Ilość musi być dodatnia")
        self.lines.append(OrderLine(sku, quantity, unit_price))

    def total(self) -> Money:
        return sum((l.unit_price * l.quantity for l in self.lines), Money.zero("PLN"))

    def place(self) -> None:
        if not self.lines:
            raise OrderError("Puste zamówienie")
        self.status = OrderStatus.PLACED
```

Reguły biznesowe siedzą w obiektach domeny: nie można dodać pozycji do złożonego zamówienia i nie można złożyć pustego zamówienia.

## Porty jako interfejsy

W Pythonie porty wygodnie opisuje <a id="term-protocol"></a>[`Protocol`](00%20Glossary%20Hexagonal.md#protocol) z modułu `typing`. Adapter nie musi dziedziczyć po porcie, wystarczy, że ma pasujące metody. Mypy albo Pyright sprawdzą zgodność statycznie.

```python
# application/ports.py
from typing import Protocol

from shop.domain.money import Money
from shop.domain.order import Order


class OrderRepository(Protocol):
    def get(self, order_id: str) -> Order: ...
    def save(self, order: Order) -> None: ...


class PriceList(Protocol):
    def price_of(self, sku: str) -> Money: ...


class PaymentGateway(Protocol):
    def charge(self, customer_id: str, amount: Money) -> str: ...


class Notifier(Protocol):
    def order_placed(self, order: Order) -> None: ...
```

Alternatywą jest `abc.ABC` z `@abstractmethod`. Daje błąd już przy tworzeniu niekompletnego adaptera, ale wymaga dziedziczenia, czyli adapter musi importować port. W obu wariantach zależność i tak wskazuje do środka.

## Use case: scenariusz krok po kroku

<a id="term-application-service"></a>[Serwis aplikacyjny](00%20Glossary%20Hexagonal.md#application-service), czyli use case, orkiestruje scenariusz: pobiera dane przez porty, wywołuje domenę, zapisuje wynik. Sam nie podejmuje decyzji biznesowych.

```python
# application/place_order.py
from dataclasses import dataclass

from shop.application.ports import Notifier, OrderRepository, PaymentGateway, PriceList
from shop.domain.order import Order


@dataclass(frozen=True)
class PlaceOrderCommand:
    customer_id: str
    items: list[tuple[str, int]]


class PlaceOrderHandler:
    def __init__(self, orders: OrderRepository, prices: PriceList,
                 payments: PaymentGateway, notifier: Notifier):
        self._orders = orders
        self._prices = prices
        self._payments = payments
        self._notifier = notifier

    def __call__(self, command: PlaceOrderCommand) -> str:
        order = Order(customer_id=command.customer_id)
        for sku, quantity in command.items:
            order.add_line(sku, quantity, self._prices.price_of(sku))
        order.place()
        self._payments.charge(order.customer_id, order.total())
        self._orders.save(order)
        self._notifier.order_placed(order)
        return order.id
```

## Reguła czy orkiestracja

<a id="term-domain-service"></a>[Serwis domenowy](00%20Glossary%20Hexagonal.md#domain-service) zawiera regułę biznesową, która nie pasuje do jednego obiektu, na przykład naliczenie rabatu zależnego od historii klienta i zawartości koszyka. Leży w `domain` i nie używa portów.

```python
# domain/pricing.py
from decimal import Decimal

from shop.domain.money import Money
from shop.domain.order import Order


class LoyaltyDiscount:
    def apply(self, order: Order, previous_orders: int) -> Money:
        if previous_orders >= 10:
            return order.total() * Decimal("0.9")
        return order.total()
```

| | Serwis aplikacyjny | Serwis domenowy |
|---|---|---|
| Gdzie leży | `application` | `domain` |
| Co robi | orkiestruje kroki scenariusza | liczy regułę biznesową |
| Używa portów | tak | nie |
| Zna transakcje, powiadomienia | tak, przez porty | nie |
| Test | z fake'ami portów | czysty test jednostkowy |

Prosta heurystyka: jeśli ekspert biznesowy rozpoznałby kod jako regułę, to domena. Jeśli opisuje „najpierw pobierz, potem zapisz, na końcu wyślij”, to aplikacja.

## Wywołanie na zewnątrz, zależność do środka

Use case wywołuje `PaymentGateway`, ale nie importuje `StripePaymentGateway`. To jest <a id="term-dependency-inversion"></a>[odwrócenie zależności](00%20Glossary%20Hexagonal.md#dependency-inversion) (Dependency Inversion Principle): moduł wysokiego poziomu i moduł niskiego poziomu zależą od wspólnej abstrakcji, którą posiada moduł wysokiego poziomu.

```text
Przepływ wywołania:    PlaceOrderHandler ──► StripePaymentGateway
Zależność w kodzie:    PlaceOrderHandler ──► PaymentGateway ◄── StripePaymentGateway
```

Wywołanie płynie na zewnątrz, zależność płynie do środka. Na tym polega cały mechanizm hexagonal.

## Kto składa całość

Skoro rdzeń nie tworzy adapterów, ktoś musi to zrobić. Tym miejscem jest <a id="term-composition-root"></a>[composition root](00%20Glossary%20Hexagonal.md#composition-root): jedno miejsce przy starcie aplikacji, które zna wszystkie klasy i łączy je ze sobą.

```python
# main.py
import stripe
from fastapi import FastAPI
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

from shop.adapters.inbound import http
from shop.adapters.outbound.email_notifier import SmtpNotifier
from shop.adapters.outbound.sql_orders import SqlOrderRepository, SqlPriceList
from shop.adapters.outbound.stripe_payments import StripePaymentGateway
from shop.application.place_order import PlaceOrderHandler


def build_app(settings) -> FastAPI:
    session = sessionmaker(bind=create_engine(settings.database_url))()
    place_order = PlaceOrderHandler(
        orders=SqlOrderRepository(session),
        prices=SqlPriceList(session),
        payments=StripePaymentGateway(stripe.StripeClient(settings.stripe_key)),
        notifier=SmtpNotifier(settings.smtp_host),
    )
    app = FastAPI()
    app.include_router(http.build_router(place_order))
    return app
```

Composition root jest jedynym plikiem, który wolno uzależnić od wszystkiego. Dla testów, CLI i workera można mieć osobne funkcje `build_*`, które składają ten sam rdzeń z innymi adapterami.

## Kontenery i frameworki

<a id="term-di-container"></a>[Kontener DI](00%20Glossary%20Hexagonal.md#di-container) automatyzuje składanie obiektów: rejestrujesz, która klasa implementuje który port, a kontener tworzy graf zależności. W Pythonie popularne są `dependency-injector`, `punq`, `lagom`, a w FastAPI mechanizm `Depends`.

Kontener jest wygodny przy dużej liczbie zależności, ale nie jest wymagany. Ręczne składanie w `main.py` jest czytelne i wystarcza w większości serwisów.

Framework może żyć w adapterach i composition root, ale nie w rdzeniu. Sygnały ostrzegawcze:

- dekoratory frameworka na klasach domeny (`@inject`, `@Entity`, `models.Model`),
- use case przyjmujący `Request` albo zwracający `JSONResponse`,
- domena dziedzicząca po modelu ORM, na przykład Django `models.Model`.

Jeśli rdzeń da się zaimportować i uruchomić w czystym interpreterze bez zainstalowanego frameworka, granica jest szczelna.

## Co zapamiętać

- Typowy układ to `domain`, `application`, `adapters/inbound`, `adapters/outbound` i `main.py`.
- Domena zawiera reguły i nie importuje niczego technicznego.
- W Pythonie porty wygodnie opisuje `Protocol`, alternatywą jest `ABC`.
- Serwis aplikacyjny orkiestruje kroki, serwis domenowy liczy regułę.
- Wywołanie płynie na zewnątrz, zależność w kodzie do środka.
- Composition root jako jedyne miejsce zna wszystkie klasy i je łączy.
- Kontener DI jest opcjonalny, framework nie może wejść do rdzenia.

## Pytania sprawdzające

### 16. Jak zorganizować pakiety/moduły projektu w stylu hexagonal?

<details>
<summary>Odpowiedź</summary>

Typowy układ: `domain` (reguły biznesowe bez zależności technicznych), `application` (use case'y i porty wyjściowe), `adapters/inbound` (HTTP, CLI), `adapters/outbound` (SQL, płatności, e-mail) oraz `main.py` jako composition root. Układ katalogów jest umowny, ważny jest kierunek importów: `adapters → application → domain`.

Zobacz: początek rozdziału.

</details>

### 17. Gdzie leżą use case'y (application services) i czym różnią się od domain services?

<details>
<summary>Odpowiedź</summary>

Use case'y leżą w `application`. Orkiestrują scenariusz: pobierają dane przez porty, wołają domenę, zapisują wynik i wysyłają powiadomienia. Serwis domenowy leży w `domain`, zawiera regułę biznesową, która nie pasuje do jednego obiektu (np. rabat lojalnościowy), i nie używa portów. Heurystyka: regułę rozpozna ekspert biznesowy, orkiestracja brzmi jak „pobierz, zapisz, wyślij”.

Zobacz: sekcje „Use case: scenariusz krok po kroku” i „Reguła czy orkiestracja”.

</details>

### 18. Jak realizuje się Dependency Inversion w tej architekturze i kto „skleja” całość?

<details>
<summary>Odpowiedź</summary>

Use case zależy od abstrakcji (`PaymentGateway`), którą sam posiada, a adapter (`StripePaymentGateway`) ją implementuje. Wywołanie płynie na zewnątrz, zależność w kodzie do środka. Całość składa composition root, czyli jedno miejsce przy starcie (np. `main.py`), które tworzy adaptery i wstrzykuje je do use case'ów.

Zobacz: sekcje „Wywołanie na zewnątrz, zależność do środka” i „Kto składa całość”.

</details>

### 19. Jaką rolę pełni kontener DI? Czy framework (Spring, FastAPI, Django) może wejść do rdzenia?

<details>
<summary>Odpowiedź</summary>

Kontener DI automatyzuje składanie grafu obiektów, ale jest opcjonalny, bo ręczne składanie w `main.py` zwykle wystarcza. Framework może żyć w adapterach i w composition root, ale nie w rdzeniu. Sygnały ostrzegawcze to dekoratory frameworka na klasach domeny, use case przyjmujący `Request` albo domena dziedzicząca po `models.Model`. Test: rdzeń da się uruchomić bez zainstalowanego frameworka.

Zobacz: sekcja „Kontenery i frameworki”.

</details>
