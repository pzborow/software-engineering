# Porty i adaptery

Port jest kontraktem na granicy rdzenia, a adapter tłumaczy ten kontrakt na konkretną technologię. Porty i adaptery występują po dwóch stronach aplikacji: po stronie, która aplikację wywołuje, i po stronie, którą aplikacja sama wywołuje.

```text
strona wywołująca (driving)          strona wywoływana (driven)

HTTP controller ──► port wejściowy ─► rdzeń ─► port wyjściowy ◄── SQL repository
CLI command     ──►                            port wyjściowy ◄── SMTP notifier
```

## Dwie strony heksagonu

<a id="term-driving-port"></a>[Port wejściowy](00%20Glossary%20Hexagonal.md#driving-port) (driving, primary) opisuje, co aplikacja potrafi zrobić: złożyć zamówienie, anulować zamówienie, pobrać szczegóły. To API rdzenia dla świata zewnętrznego.

<a id="term-driven-port"></a>[Port wyjściowy](00%20Glossary%20Hexagonal.md#driven-port) (driven, secondary) opisuje, czego aplikacja potrzebuje od świata: zapisać zamówienie, obciążyć kartę, wysłać powiadomienie. Rdzeń go wywołuje, ale nie implementuje.

Kierunek wywołania jest przeciwny po obu stronach, a kierunek zależności w kodzie jest zawsze ten sam: do środka.

| Strona | Kto inicjuje | Kto definiuje interfejs | Kto implementuje |
|---|---|---|---|
| Driving | świat zewnętrzny | rdzeń | rdzeń (scenariusz) |
| Driven | rdzeń | rdzeń | adapter |

## Scenariusz jako port wejściowy

Port wejściowy jest najczęściej realizowany przez <a id="term-use-case"></a>[use case](00%20Glossary%20Hexagonal.md#use-case), czyli klasę albo funkcję opisującą jeden scenariusz biznesowy. Wejściem jest komenda z danymi, wyjściem prosty wynik:

```python
from dataclasses import dataclass
from typing import Protocol


@dataclass(frozen=True)
class PlaceOrderCommand:
    customer_id: str
    items: list[tuple[str, int]]      # (sku, quantity)


class PlaceOrder(Protocol):           # port wejściowy
    def __call__(self, command: PlaceOrderCommand) -> str: ...
```

Czy port wejściowy musi być osobnym interfejsem? Nie zawsze. W wielu projektach klasa use case'u sama jest portem: kontroler zależy od `PlaceOrderHandler` bez pośredniego `Protocol`. Osobny interfejs ma sens, gdy chcesz podmienić implementację w testach adaptera HTTP albo gdy rdzeń jest publikowany jako biblioteka.

## Port wyjściowy należy do rdzenia

Interfejs portu wyjściowego definiuje rdzeń, bo to rdzeń wie, czego potrzebuje. Gdyby interfejs pochodził z infrastruktury, rdzeń musiałby ją importować i reguła zależności byłaby złamana.

Najczęstszy port wyjściowy to <a id="term-repository"></a>[repozytorium](00%20Glossary%20Hexagonal.md#repository), które udaje kolekcję obiektów domenowych:

```python
class OrderRepository(Protocol):
    def get(self, order_id: str) -> "Order": ...
    def save(self, order: "Order") -> None: ...


class PaymentGateway(Protocol):
    def charge(self, customer_id: str, amount: "Money") -> str: ...


class Notifier(Protocol):
    def order_placed(self, order: "Order") -> None: ...
```

Parametry i typy zwracane są pojęciami domeny (`Order`, `Money`), a nie typami technologii (`Row`, `Response`, `dict` z JSON-a).

## Nazwy wyrażają intencję

Nazwa portu powinna odpowiadać na pytanie „czego potrzebuje biznes”, a nie „czego używamy”:

| Źle: nazwa technologii | Dobrze: nazwa potrzeby |
|---|---|
| `PostgresOrderDao` | `OrderRepository` |
| `StripeClient` | `PaymentGateway` |
| `SmtpSender` | `Notifier` albo `CustomerNotifications` |
| `RedisCache.get_json()` | `ExchangeRates.current()` |

Nazwa technologii jest dobra dla adaptera, bo adapter jest z nią związany: `PostgresOrderRepository`, `StripePaymentGateway`.

## Adaptery po obu stronach

<a id="term-driving-adapter"></a>[Adapter wejściowy](00%20Glossary%20Hexagonal.md#driving-adapter) tłumaczy żądanie z zewnątrz na wywołanie portu. Kontroler HTTP odczytuje JSON, buduje komendę i woła use case:

```python
from fastapi import APIRouter, Depends

router = APIRouter()


@router.post("/orders", status_code=201)
def place_order(body: PlaceOrderRequest, place: PlaceOrder = Depends(get_place_order)):
    command = PlaceOrderCommand(
        customer_id=body.customer_id,
        items=[(i.sku, i.quantity) for i in body.items],
    )
    order_id = place(command)
    return {"id": order_id}
```

<a id="term-driven-adapter"></a>[Adapter wyjściowy](00%20Glossary%20Hexagonal.md#driven-adapter) implementuje port wyjściowy przy użyciu konkretnej technologii:

```python
class StripePaymentGateway:
    def __init__(self, client: "stripe.StripeClient"):
        self._client = client

    def charge(self, customer_id: str, amount: Money) -> str:
        intent = self._client.payment_intents.create(
            amount=int(amount.amount * 100),
            currency=amount.currency.lower(),
            customer=customer_id,
        )
        return intent.id
```

Typowe przykłady w serwisie webowym:

- wejściowe: kontroler REST, handler GraphQL, komenda CLI, konsument kolejki, zadanie cron, test,
- wyjściowe: repozytorium SQL, klient zewnętrznego API, wysyłka e-maili, publikacja na Kafkę, zapis pliku do S3.

## Jeden port, wiele adapterów

Jeden port może mieć dowolnie wiele implementacji. To główne źródło elastyczności:

```text
OrderRepository
├── PostgresOrderRepository     produkcja
├── InMemoryOrderRepository     testy i prototyp
└── DynamoOrderRepository       migracja na inną bazę

PlaceOrder
├── HTTP controller             aplikacja webowa
├── CLI command                 import z pliku
└── Kafka consumer              zamówienia z innego systemu
```

Po stronie wyjściowej zwykle aktywny jest jeden adapter na raz, wybrany przy starcie. Po stronie wejściowej wiele adapterów może działać równocześnie i wołać ten sam use case.

## Mapowanie na granicy

Adapter pracuje na formatach technologii, rdzeń na obiektach domeny. Między nimi potrzebne jest mapowanie. Do przenoszenia danych przez granicę służy <a id="term-dto"></a>[DTO](00%20Glossary%20Hexagonal.md#dto), czyli prosty obiekt bez zachowania, a za przepisywanie pól odpowiada <a id="term-mapper"></a>[mapper](00%20Glossary%20Hexagonal.md#mapper).

```text
JSON ─► PlaceOrderRequest (DTO HTTP) ─► PlaceOrderCommand ─► Order (domena)
Order (domena) ─► OrderRow (model ORM) ─► wiersz w tabeli
```

Mapowanie odbywa się w adapterze, nie w domenie. Domena nie zna `PlaceOrderRequest` ani `OrderRow`:

```python
class PostgresOrderRepository:
    def save(self, order: Order) -> None:
        row = OrderRow(
            id=order.id,
            customer_id=order.customer_id,
            status=order.status.value,
            total_cents=int(order.total().amount * 100),
        )
        self._session.merge(row)

    def get(self, order_id: str) -> Order:
        row = self._session.get(OrderRow, order_id)
        return Order.restore(id=row.id, customer_id=row.customer_id, status=row.status)
```

Dzięki temu zmiana kolumny w bazie albo pola w JSON-ie zmienia tylko adapter.

## Co zapamiętać

- Port wejściowy mówi, co aplikacja potrafi, port wyjściowy mówi, czego potrzebuje.
- Oba rodzaje portów definiuje rdzeń, zależności w kodzie wskazują do środka.
- Port wejściowy najczęściej realizuje use case, osobny interfejs jest opcjonalny.
- Nazwa portu opisuje potrzebę biznesową, nazwa adaptera może zawierać technologię.
- Jeden port może mieć wiele adapterów, na przykład produkcyjny i w pamięci.
- Mapowanie DTO ↔ domena odbywa się w adapterze, na granicy.

## Pytania sprawdzające

### 8. Czym jest port? Czym jest adapter?

<details>
<summary>Odpowiedź</summary>

Port to interfejs na granicy rdzenia, zdefiniowany przez rdzeń i wyrażony w pojęciach domeny. Opisuje, co aplikacja oferuje albo czego potrzebuje. Adapter to konkretna klasa, która tłumaczy ten kontrakt na technologię: wywołuje port wejściowy (np. kontroler HTTP) albo implementuje port wyjściowy (np. repozytorium SQL).

Zobacz: wstęp rozdziału i sekcja „Adaptery po obu stronach”.

</details>

### 9. Czym różni się port wejściowy (driving/primary) od wyjściowego (driven/secondary)?

<details>
<summary>Odpowiedź</summary>

Port wejściowy opisuje, co aplikacja potrafi zrobić, i jest wywoływany przez świat zewnętrzny. Port wyjściowy opisuje, czego aplikacja potrzebuje, i jest wywoływany przez rdzeń, a implementowany przez adapter. Kierunek wywołań jest przeciwny, ale oba interfejsy należą do rdzenia i zależności w kodzie wskazują do środka.

Zobacz: sekcja „Dwie strony heksagonu”.

</details>

### 10. Podaj przykłady adapterów driving i driven w typowym serwisie webowym.

<details>
<summary>Odpowiedź</summary>

Driving: kontroler REST, handler GraphQL, komenda CLI, konsument kolejki, zadanie cron, test. Driven: repozytorium SQL, klient zewnętrznego API (np. płatności), wysyłka e-maili, publikacja wiadomości na Kafkę, zapis plików do S3.

Zobacz: sekcja „Adaptery po obu stronach”.

</details>

### 11. Kto definiuje interfejs portu wyjściowego: domena czy infrastruktura? Dlaczego?

<details>
<summary>Odpowiedź</summary>

Rdzeń. To rdzeń wie, czego potrzebuje, i opisuje to w swoich pojęciach (`Order`, `Money`). Gdyby interfejs pochodził z infrastruktury, rdzeń musiałby ją importować, co łamie regułę zależności.

Zobacz: sekcja „Port wyjściowy należy do rdzenia”.

</details>

### 12. Jak nazwać port, żeby wyrażał intencję biznesową, a nie technologię?

<details>
<summary>Odpowiedź</summary>

Nazwa portu odpowiada na pytanie „czego potrzebuje biznes”: `OrderRepository`, `PaymentGateway`, `Notifier`, `ExchangeRates`. Nazwy technologii, takie jak `PostgresOrderDao` czy `StripeClient`, są właściwe dla adapterów, np. `PostgresOrderRepository`, `StripePaymentGateway`.

Zobacz: sekcja „Nazwy wyrażają intencję”.

</details>

### 13. Czy port wejściowy musi być interfejsem? Czy może nim być klasa use case'u?

<details>
<summary>Odpowiedź</summary>

Nie musi. Często klasa use case'u sama pełni rolę portu, a kontroler zależy bezpośrednio od niej. Osobny interfejs ma sens, gdy chcesz podmienić implementację w testach adaptera wejściowego albo gdy rdzeń jest publikowany jako biblioteka dla innych modułów.

Zobacz: sekcja „Scenariusz jako port wejściowy”.

</details>

### 14. Ile adapterów może mieć jeden port? Podaj przykład.

<details>
<summary>Odpowiedź</summary>

Dowolnie wiele. `OrderRepository` może mieć implementację Postgres na produkcji, w pamięci do testów i DynamoDB na czas migracji. Port wejściowy `PlaceOrder` może być wywoływany równocześnie przez kontroler HTTP, komendę CLI i konsumenta Kafki. Po stronie wyjściowej zwykle jeden adapter jest aktywny, wybrany przy starcie.

Zobacz: sekcja „Jeden port, wiele adapterów”.

</details>

### 15. Jak mapować dane między adapterem a domeną (DTO ↔ model domenowy)? Gdzie ma się dziać mapowanie?

<details>
<summary>Odpowiedź</summary>

Mapowanie robi adapter, na granicy. Adapter wejściowy zamienia DTO (np. JSON → `PlaceOrderRequest`) na komendę rdzenia, a adapter wyjściowy zamienia obiekt domeny na model persystencji (`Order` → `OrderRow`) i z powrotem. Domena nie zna DTO ani modeli ORM, więc zmiana kolumny albo pola JSON zmienia tylko adapter.

Zobacz: sekcja „Mapowanie na granicy”.

</details>
