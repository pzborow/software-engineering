# Testowanie

Testowalność to najczęściej wymieniana zaleta architektury heksagonalnej. Wynika wprost z portów: jeśli rdzeń rozmawia ze światem wyłącznie przez interfejsy, w teście można podłączyć do nich cokolwiek, co te interfejsy spełnia.

```text
produkcja:  HTTP ──► rdzeń ──► Postgres, Stripe, SMTP
test:       pytest ──► rdzeń ──► lista w pamięci, fake płatności, fake powiadomień
```

Rdzeń jest ten sam. Zmieniają się tylko adaptery.

## Dlaczego jest łatwiej

W architekturze warstwowej test logiki zamówień wymaga bazy, bo serwis importuje ORM. Trzeba postawić kontener, wykonać migracje i sprzątać dane. Test trwa sekundy, a nie milisekundy.

W hexagonal test rdzenia jest zwykłym testem Pythona. Każdą zależność zastępuje <a id="term-test-double"></a>[dubler testowy](00%20Glossary%20Hexagonal.md#test-double), czyli obiekt, który w teście zajmuje miejsce prawdziwej implementacji portu. Przypadki brzegowe, takie jak odmowa płatności, można wywołać jedną linijką, bez konfiguracji zewnętrznej usługi.

## Rodzaje dublerów

<a id="term-stub"></a>[Stub](00%20Glossary%20Hexagonal.md#stub) zwraca przygotowane odpowiedzi i nic nie zapamiętuje. Dobrze pasuje do portów, z których rdzeń tylko czyta:

```python
class FixedPriceList:
    def __init__(self, prices: dict[str, Money]):
        self._prices = prices

    def price_of(self, sku: str) -> Money:
        return self._prices[sku]
```

<a id="term-fake"></a>[Fake](00%20Glossary%20Hexagonal.md#fake) to działająca, uproszczona implementacja portu. Zachowuje się jak prawdziwa, ale trzyma dane w pamięci. Fake repozytorium to <a id="term-in-memory-adapter"></a>[adapter w pamięci](00%20Glossary%20Hexagonal.md#in-memory-adapter):

```python
class InMemoryOrderRepository:
    def __init__(self):
        self._orders: dict[str, Order] = {}

    def get(self, order_id: str) -> Order:
        try:
            return self._orders[order_id]
        except KeyError:
            raise OrderNotFound(order_id)

    def save(self, order: Order) -> None:
        self._orders[order.id] = order

    def all(self) -> list[Order]:          # pomocnicze, tylko dla testów
        return list(self._orders.values())


class FakePaymentGateway:
    def __init__(self, decline: bool = False):
        self.charges: list[tuple[str, Money]] = []
        self._decline = decline

    def charge(self, customer_id: str, amount: Money) -> str:
        if self._decline:
            raise PaymentDeclined(customer_id)
        self.charges.append((customer_id, amount))
        return f"pay-{len(self.charges)}"
```

<a id="term-mock"></a>[Mock](00%20Glossary%20Hexagonal.md#mock) nagrywa wywołania i pozwala sprawdzić, czy konkretna metoda została wywołana z konkretnymi argumentami. W Pythonie zwykle jest to `unittest.mock.Mock`.

| Dubler | Zwraca dane | Ma stan | Sprawdzasz |
|---|---|---|---|
| Stub | tak, stałe | nie | wynik rdzenia |
| Fake | tak, jak prawdziwy | tak | stan po operacji |
| Mock | opcjonalnie | nagrania wywołań | czy i jak wywołano metodę |

## Test rdzenia bez infrastruktury

Z fake'ami test use case'u jest krótki i czyta się go jak specyfikację:

```python
def build(decline=False):
    orders = InMemoryOrderRepository()
    payments = FakePaymentGateway(decline=decline)
    handler = PlaceOrderHandler(
        orders=orders,
        prices=FixedPriceList({"BOOK": Money(Decimal("50"), "PLN")}),
        payments=payments,
        notifier=FakeNotifier(),
    )
    return handler, orders, payments


def test_places_order_and_charges_customer():
    handler, orders, payments = build()

    order_id = handler(PlaceOrderCommand("c-1", [("BOOK", 2)]))

    assert orders.get(order_id).status is OrderStatus.PLACED
    assert payments.charges == [("c-1", Money(Decimal("100"), "PLN"))]


def test_declined_payment_does_not_save_order():
    handler, orders, _ = build(decline=True)

    with pytest.raises(PaymentDeclined):
        handler(PlaceOrderCommand("c-1", [("BOOK", 1)]))

    assert orders.all() == []
```

Test nie wie, czy rdzeń woła `save` przed czy po `charge`. Sprawdza tylko wynik: zamówienie istnieje albo nie istnieje. Dzięki temu refaktoryzacja use case'u nie psuje testów.

## Fake czy mock dla portów wyjściowych

Dla portów wyjściowych zwykle lepszy jest fake. Mock sprawdza, jak rdzeń jest zbudowany (`save` wywołane raz z tym obiektem). Fake sprawdza, co rdzeń osiągnął (zamówienie jest w repozytorium). Testy oparte na mockach łamią się przy każdej zmianie implementacji, nawet gdy zachowanie jest poprawne.

Mock ma sens tam, gdzie wywołanie jest samym efektem i nie ma stanu do odczytania, na przykład „wysłano dokładnie jedno powiadomienie”. Nawet wtedy prosty fake z listą wysłanych wiadomości bywa czytelniejszy.

```python
# mock: test zna szczegół implementacji
repo = Mock()
handler(command)
repo.save.assert_called_once()

# fake: test zna tylko wynik
repo = InMemoryOrderRepository()
order_id = handler(command)
assert repo.get(order_id).status is OrderStatus.PLACED
```

## Czy fake mówi prawdę

Fake jest użyteczny tylko wtedy, gdy zachowuje się jak prawdziwy adapter. Jeśli `InMemoryOrderRepository.get` zwraca `None`, a `SqlOrderRepository.get` rzuca `OrderNotFound`, testy rdzenia przechodzą, a produkcja się wywraca.

Rozwiązaniem jest <a id="term-contract-test"></a>[test kontraktowy](00%20Glossary%20Hexagonal.md#contract-test): jeden zestaw testów opisujący zachowanie portu, uruchamiany na każdej implementacji.

```python
import pytest


@pytest.fixture(params=["memory", "sql"])
def repo(request, db_session):
    if request.param == "memory":
        return InMemoryOrderRepository()
    return SqlOrderRepository(db_session)


def test_saved_order_can_be_read_back(repo):
    order = an_order()
    repo.save(order)
    assert repo.get(order.id).total() == order.total()


def test_missing_order_raises_domain_error(repo):
    with pytest.raises(OrderNotFound):
        repo.get("missing")
```

Wariant `sql` łączy się z prawdziwą bazą, na przykład przez Testcontainers. Test kontraktowy jest więc zarazem testem integracyjnym adaptera i gwarancją, że fake nie kłamie.

## Piramida testów

W projekcie heksagonalnym piramida testów układa się według granic:

```text
            ▲  kilka testów end-to-end
           ▲▲▲  HTTP → rdzeń → prawdziwa baza
          ▲▲▲▲▲  testy adapterów i kontraktów
         ▲▲▲▲▲▲▲  Testcontainers, klient HTTP w teście
        ▲▲▲▲▲▲▲▲▲  testy use case'ów z fake'ami
       ▲▲▲▲▲▲▲▲▲▲▲  testy domeny: czyste funkcje i obiekty
```

| Poziom | Co testuje | Zależności | Liczba |
|---|---|---|---|
| Domena | niezmienniki, obliczenia | brak | najwięcej |
| Use case | scenariusze, obsługa błędów | fake'i portów | dużo |
| Adapter | mapowanie, SQL, HTTP | prawdziwa technologia | umiarkowanie |
| End-to-end | czy całość jest poprawnie złożona | wszystko | kilka |

Testy end-to-end nie muszą sprawdzać każdej reguły, bo reguły są pokryte niżej. Sprawdzają głównie composition root: czy właściwe adaptery są podłączone i czy konfiguracja działa.

## Co zapamiętać

- Porty pozwalają testować rdzeń bez bazy, sieci i frameworka.
- Stub zwraca stałe dane, fake działa jak uproszczona implementacja, mock nagrywa wywołania.
- Dla portów wyjściowych zwykle lepszy jest fake, bo test sprawdza wynik, a nie implementację.
- Adapter w pamięci jest najczęstszym fake'iem repozytorium.
- Test kontraktowy uruchamia te same asercje na fake'u i prawdziwym adapterze.
- Najwięcej testów jest na poziomie domeny i use case'ów, najmniej end-to-end.

## Pytania sprawdzające

### 24. Dlaczego mówi się, że hexagonal ułatwia testowanie?

<details>
<summary>Odpowiedź</summary>

Rdzeń komunikuje się ze światem wyłącznie przez porty, więc w teście każdą zależność można zastąpić dublerem. Test logiki nie potrzebuje bazy, sieci ani frameworka, działa w milisekundach, a przypadki brzegowe (np. odmowę płatności) wywołuje się jedną linijką.

Zobacz: sekcja „Dlaczego jest łatwiej”.

</details>

### 25. Jak testować rdzeń aplikacji bez bazy danych i HTTP (fake, stub, in-memory adapter)?

<details>
<summary>Odpowiedź</summary>

Use case wywołuje się bezpośrednio z testu, z komendą jako wejściem. Porty wyjściowe zastępuje się dublerami: stub dla portów tylko do odczytu (`FixedPriceList`), fake dla portów ze stanem (`InMemoryOrderRepository`, `FakePaymentGateway`). Asercje sprawdzają stan po operacji, np. status zamówienia w repozytorium i listę obciążeń.

Zobacz: sekcje „Rodzaje dublerów” i „Test rdzenia bez infrastruktury”.

</details>

### 26. Czym jest test kontraktowy adaptera i po co go pisać dla każdej implementacji portu?

<details>
<summary>Odpowiedź</summary>

To jeden zestaw testów opisujący zachowanie portu, uruchamiany na każdej implementacji, np. przez sparametryzowaną fixturę `memory` / `sql`. Gwarantuje, że fake zachowuje się jak prawdziwy adapter, więc testy rdzenia oparte na fake'u mówią prawdę. Wariant z prawdziwą technologią jest jednocześnie testem integracyjnym adaptera.

Zobacz: sekcja „Czy fake mówi prawdę”.

</details>

### 27. Jak wygląda piramida testów w projekcie heksagonalnym?

<details>
<summary>Odpowiedź</summary>

Najwięcej testów domeny (czyste obiekty, bez zależności), dużo testów use case'ów z fake'ami portów, umiarkowanie testów adapterów i kontraktów z prawdziwą technologią (np. Testcontainers) oraz kilka testów end-to-end. Te ostatnie sprawdzają głównie, czy composition root poprawnie złożył całość, a nie każdą regułę.

Zobacz: sekcja „Piramida testów”.

</details>

### 28. Mock czy fake: co wybierzesz do portów wyjściowych i dlaczego?

<details>
<summary>Odpowiedź</summary>

Zwykle fake. Test z fake'iem sprawdza wynik (zamówienie jest zapisane), a test z mockiem sprawdza implementację (`save` wywołane raz), więc łamie się przy refaktoryzacji mimo poprawnego zachowania. Mock ma sens, gdy samo wywołanie jest efektem i nie ma stanu do odczytania, ale nawet wtedy fake z listą wywołań bywa czytelniejszy.

Zobacz: sekcja „Fake czy mock dla portów wyjściowych”.

</details>
