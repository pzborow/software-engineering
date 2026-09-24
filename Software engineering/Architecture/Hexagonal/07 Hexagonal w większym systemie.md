# Hexagonal w większym systemie

Dotąd heksagon był jeden: aplikacja sklepu z zamówieniami. W większym systemie pojawiają się nowe pytania. Jak obsłużyć ciężkie odczyty, jak powiadamiać inne części systemu o zmianach i ile heksagonów potrzeba, gdy kodu jest dużo.

```text
             ┌──────────── system ────────────┐
             │                                │
HTTP ──►  [ Sprzedaż ] ──zdarzenie──► [ Magazyn ]
             │    │                           │
             │    └──zdarzenie──► [ Fakturowanie ]
             │                                │
             └────────────────────────────────┘
```

## Rozdzielenie zapisu i odczytu

<a id="term-cqrs"></a>[CQRS](00%20Glossary%20Hexagonal.md#cqrs) (Command Query Responsibility Segregation) rozdziela operacje zmieniające stan (komendy) od operacji zwracających dane (zapytania). W hexagonal oznacza to dwa rodzaje portów wejściowych:

```python
class PlaceOrder(Protocol):                    # komenda: zmienia stan, zwraca ID
    def __call__(self, command: PlaceOrderCommand) -> str: ...


class GetOrderSummaries(Protocol):             # zapytanie: nic nie zmienia
    def __call__(self, customer_id: str) -> list[OrderSummary]: ...
```

Strona zapisu przechodzi przez domenę, bo tam są niezmienniki do pilnowania. Strona odczytu nie musi. Ładowanie całych agregatów tylko po to, żeby zbudować listę z trzema kolumnami, jest kosztowne i niczego nie chroni.

## Odczyt obok domeny

Strona odczytu zwraca <a id="term-read-model"></a>[model odczytu](00%20Glossary%20Hexagonal.md#read-model): płaskie DTO przygotowane pod konkretny ekran lub endpoint. Port odczytu jest nadal portem, ale jego adapter może użyć prostego SQL-a:

```python
@dataclass(frozen=True)
class OrderSummary:
    order_id: str
    placed_at: datetime
    total: Decimal
    status: str


class OrderSummaries(Protocol):                # port wyjściowy strony odczytu
    def for_customer(self, customer_id: str) -> list[OrderSummary]: ...


class SqlOrderSummaries:                       # adapter: jedno zapytanie, bez ORM-owych agregatów
    def for_customer(self, customer_id: str) -> list[OrderSummary]:
        rows = self._conn.execute(
            text("SELECT id, placed_at, total, status FROM orders "
                 "WHERE customer_id = :c ORDER BY placed_at DESC"),
            {"c": customer_id},
        )
        return [OrderSummary(*row) for row in rows]
```

```text
komenda  ──► use case ──► domena ──► OrderRepository ──► tabela orders
zapytanie ──► query handler ──────► OrderSummaries  ──► tabela / widok / Elasticsearch
```

Granica nadal obowiązuje: handler zapytania nie zna SQL-a, zna tylko port `OrderSummaries`. Pomijana jest tylko domena. Model odczytu może też leżeć w innym magazynie, na przykład w Elasticsearch jako projekcja danych.

## Zdarzenia jako wynik domeny

<a id="term-domain-event"></a>[Zdarzenie domenowe](00%20Glossary%20Hexagonal.md#domain-event) to fakt biznesowy zapisany w czasie przeszłym: `OrderPlaced`, `PaymentDeclined`. Domena je tworzy, ale nie wie, kto je odbierze.

```python
@dataclass(frozen=True)
class OrderPlaced:
    order_id: str
    customer_id: str
    total: Money


@dataclass
class Order:
    ...
    events: list = field(default_factory=list)

    def place(self) -> None:
        if not self.lines:
            raise OrderError("Puste zamówienie")
        self.status = OrderStatus.PLACED
        self.events.append(OrderPlaced(self.id, self.customer_id, self.total()))
```

Wysyłka zdarzenia na zewnątrz to kolejny port wyjściowy. Adapter publikuje je na <a id="term-message-broker"></a>[broker wiadomości](00%20Glossary%20Hexagonal.md#message-broker), na przykład Kafkę albo RabbitMQ:

```python
class EventPublisher(Protocol):
    def publish(self, event: object) -> None: ...


class KafkaEventPublisher:
    def publish(self, event: object) -> None:
        self._producer.send(
            topic=type(event).__name__,
            value=json.dumps(asdict(event), default=str).encode(),
        )
```

Po drugiej stronie konsument Kafki jest adapterem wejściowym innego heksagonu. Odbiera wiadomość, mapuje ją na komendę i wywołuje use case, na przykład `ReserveStock`.

## Zapis i publikacja razem

Use case zapisuje zamówienie w bazie i publikuje zdarzenie na brokerze. To dwie różne technologie bez wspólnej transakcji. Jeśli publikacja się nie uda po commicie, inne systemy nie dowiedzą się o zamówieniu. Jeśli publikacja pójdzie przed commitem, a commit się nie uda, wyślesz zdarzenie o czymś, co nie istnieje.

Rozwiązaniem jest <a id="term-outbox"></a>[transactional outbox](00%20Glossary%20Hexagonal.md#outbox). Zdarzenia zapisuje się do tabeli `outbox` w tej samej transakcji co agregat. Osobny proces czyta tabelę i publikuje na broker.

```python
class SqlUnitOfWork:
    def commit(self):
        for order in self.orders.seen:
            for event in order.events:
                self._session.add(OutboxRow.from_event(event))
            order.events.clear()
        self._session.commit()        # zamówienie i zdarzenia atomowo
```

```text
use case ──► UoW.commit ──► [orders + outbox] w jednej transakcji
                                    ↓
                     relay (worker) czyta outbox ──► Kafka
```

Repozytorium zapamiętuje w `seen` agregaty wczytane i zapisane w tej transakcji, więc Unit of Work wie, skąd zebrać zdarzenia. Rdzeń nie wie o outboxie. To szczegół adaptera Unit of Work. Broker może dostarczyć wiadomość więcej niż raz, więc konsumenci powinni być idempotentni.

## Każdy serwis to heksagon

<a id="term-microservice"></a>[Mikroserwis](00%20Glossary%20Hexagonal.md#microservice) to osobno wdrażana aplikacja z własną bazą. Każdy mikroserwis może mieć wewnętrzną strukturę heksagonalną, a komunikacja z innymi serwisami odbywa się przez adaptery: klienta HTTP, producenta i konsumenta wiadomości.

```text
serwis Sprzedaż                          serwis Magazyn
┌──────────────────────┐                ┌──────────────────────┐
│ HTTP ─► rdzeń ─► DB  │                │ Kafka ─► rdzeń ─► DB │
│           └─► Kafka ─┼── OrderPlaced ─┼─► konsument          │
└──────────────────────┘                └──────────────────────┘
```

Czy każdy serwis musi być heksagonem? Nie. Serwis, który tylko tłumaczy formaty albo przekazuje dane dalej, nie ma rdzenia do ochrony. Hexagonal stosuje się tam, gdzie są reguły biznesowe.

## Wiele heksagonów w jednym procesie

<a id="term-modular-monolith"></a>[Modularny monolit](00%20Glossary%20Hexagonal.md#modular-monolith) to jedna wdrażana aplikacja podzielona na moduły o wyraźnych granicach. Każdy moduł, zwykle jeden bounded context, może być osobnym heksagonem.

```text
shop/
├── sales/          domain, application, adapters
├── inventory/      domain, application, adapters
└── billing/        domain, application, adapters
```

Moduły komunikują się tak samo jak serwisy, tylko bez sieci:

- synchronicznie: moduł `sales` ma port wyjściowy `StockAvailability`, a adapter wywołuje publiczny port wejściowy modułu `inventory`,
- asynchronicznie: zdarzenia przez szynę w pamięci albo outbox, gdy potrzebna jest trwałość.

Zasada jest ta sama co między serwisami: moduł nie importuje domeny innego modułu i nie czyta jego tabel. Taki podział można pilnować testem architektury. Dzięki temu moduł da się później wydzielić do osobnego serwisu, wymieniając tylko adapter.

## Co zapamiętać

- CQRS rozdziela porty komend i zapytań. Komendy przechodzą przez domenę, zapytania nie muszą.
- Model odczytu to płaskie DTO dostarczane przez port odczytu, na przykład z prostego SQL-a.
- Zdarzenie domenowe to fakt w czasie przeszłym tworzony przez domenę.
- Publikacja zdarzeń to port wyjściowy, a konsument wiadomości to adapter wejściowy.
- Outbox zapewnia atomowość zapisu agregatu i zdarzeń.
- Mikroserwis z regułami biznesowymi może być heksagonem, prosty serwis przekaźnikowy nie musi.
- Modularny monolit to wiele heksagonów w jednym procesie, połączonych portami i zdarzeniami.

## Pytania sprawdzające

### 31. Jak połączyć hexagonal z CQRS? Czy strona odczytu też musi przechodzić przez domenę?

<details>
<summary>Odpowiedź</summary>

Komendy i zapytania stają się osobnymi portami wejściowymi. Komendy przechodzą przez domenę, bo tam są niezmienniki. Zapytania nie muszą: handler zapytania korzysta z portu odczytu, a jego adapter zwraca płaski model odczytu, np. z prostego SQL-a, widoku albo Elasticsearch. Granica nadal obowiązuje, bo handler zna tylko port, a nie SQL. Pomijana jest tylko domena.

Zobacz: sekcje „Rozdzielenie zapisu i odczytu” i „Odczyt obok domeny”.

</details>

### 32. Jak hexagonal wygląda w mikroserwisach? Czy każdy serwis powinien być heksagonem?

<details>
<summary>Odpowiedź</summary>

Każdy mikroserwis z regułami biznesowymi może mieć wewnętrzną strukturę heksagonalną. Komunikacja z innymi serwisami to adaptery: klient HTTP i producent wiadomości po stronie wyjściowej, konsument wiadomości i kontroler po stronie wejściowej. Nie każdy serwis tego potrzebuje. Serwis, który tylko tłumaczy formaty albo przekazuje dane, nie ma rdzenia do ochrony.

Zobacz: sekcja „Każdy serwis to heksagon”.

</details>

### 33. Jak zdarzenia domenowe i messaging (Kafka, RabbitMQ) wpisują się w porty i adaptery?

<details>
<summary>Odpowiedź</summary>

Domena tworzy zdarzenia (`OrderPlaced`) jako fakty biznesowe, nie wiedząc, kto je odbierze. Publikacja to port wyjściowy (`EventPublisher`) z adapterem Kafki lub RabbitMQ. Konsument wiadomości w innym heksagonie jest adapterem wejściowym, który mapuje wiadomość na komendę. Żeby zapis agregatu i publikacja były spójne, używa się transactional outbox, czyli zapisu zdarzeń w tej samej transakcji i osobnego procesu publikującego. Konsumenci powinni być idempotentni.

Zobacz: sekcje „Zdarzenia jako wynik domeny” i „Zapis i publikacja razem”.

</details>

### 34. Czy modularny monolit może składać się z wielu heksagonów? Jak się komunikują?

<details>
<summary>Odpowiedź</summary>

Tak. Każdy moduł, zwykle jeden bounded context, ma własne `domain`, `application` i `adapters`. Moduły komunikują się synchronicznie przez porty (port wyjściowy jednego modułu, adapter wywołujący publiczny port wejściowy drugiego) albo asynchronicznie przez zdarzenia. Moduł nie importuje domeny innego modułu i nie czyta jego tabel. Dzięki temu moduł można później wydzielić do osobnego serwisu, wymieniając adapter.

Zobacz: sekcja „Wiele heksagonów w jednym procesie”.

</details>
