# Pułapki i decyzje

Architekturę heksagonalną łatwo wdrożyć w formie, a trudniej w treści. Katalogi `domain`, `ports` i `adapters` mogą istnieć, a mimo to logika może leżeć w złym miejscu, interfejsów może być za dużo, a wydajność może spaść. Ten rozdział opisuje najczęstsze problemy i decyzje, które trzeba podjąć świadomie.

## Pusty środek

<a id="term-anemic-domain-model"></a>[Anemiczny model domeny](00%20Glossary%20Hexagonal.md#anemic-domain-model) to obiekty domeny, które mają tylko pola, a cała logika siedzi w use case'ach. Struktura jest heksagonalna, ale rdzeń nie chroni żadnych reguł.

```python
# anemiczny: zamówienie to worek na dane
@dataclass
class Order:
    status: str
    lines: list


class PlaceOrderHandler:
    def __call__(self, command):
        order = self._orders.get(command.order_id)
        if order.status != "draft":                  # reguła w use case
            raise ValueError("...")
        if not order.lines:                          # reguła w use case
            raise ValueError("...")
        order.status = "placed"                      # każdy może ustawić dowolny status
        self._orders.save(order)
```

```python
# bogaty: zamówienie pilnuje własnych reguł
class PlaceOrderHandler:
    def __call__(self, command):
        order = self._orders.get(command.order_id)
        order.place()                                # reguły są w Order.place()
        self._orders.save(order)
```

Anemia pojawia się, bo zespół przenosi strukturę z CRUD-a: encja ORM z getterami i serwis z logiką. Druga przyczyna to pośpiech: łatwiej dopisać `if` w handlerze niż dodać metodę do domeny. Sygnały ostrzegawcze to publiczne settery statusu, use case'y dłuższe niż obiekty domeny i te same `if`-y powtórzone w kilku handlerach.

Anemia nie zawsze jest błędem. Jeśli domena naprawdę jest prosta, anemiczny rdzeń jest uczciwym sygnałem, że hexagonal może być na wyrost.

## Jeden model czy dwa

Domenę trzeba jakoś zapisać. Są dwie drogi, a każda ma koszt.

Pierwsza to jeden model: klasa domeny jest jednocześnie encją ORM, na przykład przez mapowanie imperatywne SQLAlchemy, w którym klasa domeny nie dziedziczy po niczym, a mapowanie jest zdefiniowane w adapterze:

```python
# adapters/outbound/orm.py
from sqlalchemy.orm import registry

mapper_registry = registry()
mapper_registry.map_imperatively(Order, orders_table, properties={
    "lines": relationship(OrderLine),
})
```

Druga to osobny <a id="term-persistence-model"></a>[model persystencji](00%20Glossary%20Hexagonal.md#persistence-model): klasa `OrderRow` odwzorowuje tabelę, a mapper w adapterze tłumaczy ją na `Order` i z powrotem (rozdział 02).

| | Jeden model | Osobny model persystencji |
|---|---|---|
| Ilość kodu | mniej | mapper dla każdego agregatu |
| Czystość domeny | ORM wpływa na kształt klas (lazy loading, puste konstruktory) | pełna |
| Zmiana schematu bazy | może wymusić zmianę domeny | zmienia tylko adapter |
| Ryzyko | przeciekanie zachowań ORM do rdzenia | rozjazd mapperów z modelem |

Rozsądna reguła: zacznij od osobnego modelu tam, gdzie domena jest bogata. Zostań przy jednym modelu z mapowaniem imperatywnym, gdy klasy domeny są proste, a mapper tylko przepisywałby pola.

## Za dużo abstrakcji

<a id="term-interface-explosion"></a>[Eksplozja interfejsów](00%20Glossary%20Hexagonal.md#interface-explosion) to sytuacja, w której każda klasa ma swój interfejs, każda metoda swój port, a każda warstwa swój DTO. Dodanie jednego pola wymaga zmiany w ośmiu plikach.

Kilka zasad ogranicza ceremonię:

- port wyjściowy twórz dla rzeczy zewnętrznych i zmiennych: bazy, API, kolejki, zegara, a nie dla każdej klasy domeny,
- port wejściowy może być po prostu klasą use case'u, bez osobnego interfejsu,
- grupuj metody w portach według potrzeby rdzenia (`OrderRepository` z `get` i `save`), a nie „jeden interfejs na metodę”,
- nie twórz DTO dla każdej warstwy, jeśli komenda może przejść z adaptera wprost do use case'u,
- w Pythonie `Protocol` nie wymaga dziedziczenia, więc interfejs kosztuje jedną krótką definicję.

Pytanie kontrolne dla każdej abstrakcji: czy istnieje albo realnie powstanie druga implementacja, choćby fake w testach? Jeśli nie, abstrakcja jest prawdopodobnie zbędna.

## Logika w złym miejscu

<a id="term-logic-leak"></a>[Wyciek logiki](00%20Glossary%20Hexagonal.md#logic-leak) to reguła biznesowa, która trafiła do adaptera: do kontrolera, zapytania SQL, szablonu albo konsumenta kolejki.

```python
# kontroler zna regułę rabatu
@router.post("/orders")
def place_order(body: PlaceOrderRequest, place: PlaceOrder = Depends(get_place_order)):
    if body.customer_tier == "gold":
        body.discount = 0.1
    ...

# repozytorium zna regułę „aktywnego zamówienia”
def active_orders(self):
    return self._session.execute(
        text("SELECT * FROM orders WHERE status = 'placed' AND created_at > now() - interval '30 days'")
    )
```

Objawy są przewidywalne: ta sama reguła działa w HTTP, ale nie działa w CLI, a zmiana reguły wymaga szukania po zapytaniach SQL.

Naprawa polega na przeniesieniu reguły do domeny i nazwaniu jej. Filtr w SQL może zostać ze względu na wydajność, ale jego definicja powinna mieć nazwę i pochodzić z rdzenia, na przykład jako metoda portu `orders.active_for(customer_id)` opisana testem kontraktowym. Pomagają też code review z pytaniem „czy ekspert biznesowy nazwałby ten `if`?” oraz testy use case'ów, które wywołują rdzeń bez HTTP. Jeśli reguła nie działa bez kontrolera, jest w kontrolerze.

## Wydajność bez łamania granic

Repozytorium zwracające całe agregaty jest wygodne dla zapisu, ale bywa kosztowne przy odczytach. Typowy problem to <a id="term-n-plus-one"></a>[N+1](00%20Glossary%20Hexagonal.md#n-plus-one): jedno zapytanie po listę zamówień i osobne zapytanie po pozycje każdego z nich.

```python
# N+1: 1 zapytanie + po jednym na każde zamówienie
for order_id in order_ids:
    order = repo.get(order_id)
    ...
```

Rozwiązania, które nie łamią granic:

| Problem | Rozwiązanie |
|---|---|
| Pętla `get` po ID | metoda portu `get_many(ids)`, adapter robi jedno zapytanie |
| Lazy loading pozycji | adapter ładuje agregat w całości (`selectinload`, JOIN) |
| Raport z agregacjami | osobny port odczytu z modelem odczytu i surowym SQL-em (rozdział 07) |
| Lista na ekran | model odczytu zamiast agregatów, ewentualnie projekcja w innym magazynie |
| Wolne zewnętrzne API | adapter z cache za tym samym portem |

Zasada: optymalizacja siedzi w adapterze albo w dedykowanym porcie odczytu. Domena nie dostaje `session` ani `joinedload`, a use case nie buduje SQL-a.

## Migracja istniejącego systemu

Przepisanie monolitu od zera rzadko się udaje. Bezpieczniej jest przejść do hexagonal stopniowo, wzorcem <a id="term-strangler-fig"></a>[strangler fig](00%20Glossary%20Hexagonal.md#strangler-fig): nowy kod stopniowo otacza stary i przejmuje jego funkcje, aż stary kod można usunąć.

```text
krok 1  test charakteryzujący    zamroź obecne zachowanie testami end-to-end
krok 2  wybierz jeden scenariusz  najlepiej często zmieniany i bogaty w reguły
krok 3  wyciągnij rdzeń           use case + domena w nowym pakiecie
krok 4  dodaj porty               dla bazy i API, którego używa scenariusz
krok 5  adapter do starego kodu   port implementowany przez istniejący kod
krok 6  przełącz ruch             kontroler woła nowy use case
krok 7  usuń stare ścieżki        i powtórz dla kolejnego scenariusza
```

Nowy rdzeń często musi rozmawiać ze starym modelem, który ma inne pojęcia, dziwne nazwy i przeciążone tabele. Żeby stary model nie przeciekł do nowej domeny, stosuje się <a id="term-anti-corruption-layer"></a>[anti-corruption layer](00%20Glossary%20Hexagonal.md#anti-corruption-layer): adapter, który tłumaczy pojęcia starego systemu na język nowego rdzenia.

```python
class LegacyCustomerAdapter:                 # implementuje port CustomerDirectory
    def get(self, customer_id: str) -> Customer:
        row = self._legacy_db.query("SELECT * FROM KLIENCI_T WHERE ID_KL = %s", customer_id)
        return Customer(
            id=str(row["ID_KL"]),
            tier=Tier.GOLD if row["FLAG_VIP"] == "T" else Tier.STANDARD,
            blocked=row["STATUS_KL"] in ("Z", "W"),
        )
```

W hexagonal anti-corruption layer jest po prostu adapterem wyjściowym z bogatszym mapowaniem. Nowa domena zna `Tier.GOLD`, a nie `FLAG_VIP == "T"`.

## Co zapamiętać

- Anemiczny model to struktura heksagonalna bez reguł w domenie.
- Jeden model czy osobny model persystencji to świadomy kompromis między ilością kodu a czystością domeny.
- Abstrakcja ma sens, gdy istnieje druga implementacja, choćby fake.
- Reguła w kontrolerze albo SQL-u to wyciek logiki, a jego objawem jest różne zachowanie w różnych adapterach.
- Problemy wydajności rozwiązuje się w adapterach i portach odczytu, nie w domenie.
- Migracja odbywa się scenariusz po scenariuszu, według wzorca strangler fig.
- Anti-corruption layer chroni nową domenę przed pojęciami starego systemu.

## Pytania sprawdzające

### 35. Co to jest „anemiczny rdzeń” i dlaczego często pojawia się w źle wdrożonym hexagonal?

<details>
<summary>Odpowiedź</summary>

To domena złożona z obiektów z samymi polami, w której cała logika siedzi w use case'ach. Katalogi są heksagonalne, ale rdzeń nie chroni reguł: każdy może ustawić dowolny status, a te same `if`-y powtarzają się w handlerach. Powstaje przez przeniesienie nawyków z CRUD-a (encja z getterami i serwis z logiką) oraz przez pośpiech. Naprawa: przenieść reguły do metod domeny, np. `order.place()`. Jeśli domena jest naprawdę prosta, anemia może oznaczać, że hexagonal jest na wyrost.

Zobacz: sekcja „Pusty środek”.

</details>

### 36. Model domenowy a encje ORM: jeden model czy dwa? Jakie są koszty każdego podejścia?

<details>
<summary>Odpowiedź</summary>

Jeden model, np. klasa domeny zmapowana imperatywnie przez SQLAlchemy, to mniej kodu, ale ORM wpływa na kształt klas (lazy loading, wymagania konstruktora), a zmiany schematu mogą dotknąć domeny. Osobny model persystencji (`OrderRow` i mapper) daje czystą domenę i izoluje schemat, ale kosztuje mapper dla każdego agregatu i ryzyko rozjazdu. Przy bogatej domenie lepszy jest osobny model, przy prostych klasach jeden model z mapowaniem w adapterze.

Zobacz: sekcja „Jeden model czy dwa”.

</details>

### 37. Jak uniknąć eksplozji interfejsów i boilerplate'u (port na każdą metodę)?

<details>
<summary>Odpowiedź</summary>

Porty wyjściowe tworzyć tylko dla rzeczy zewnętrznych i zmiennych (baza, API, kolejka, zegar). Port wejściowy może być po prostu klasą use case'u. Metody grupować według potrzeby rdzenia, a nie tworzyć interfejsu na każdą metodę. Nie mnożyć DTO dla każdej warstwy. Test dla każdej abstrakcji: czy istnieje albo realnie powstanie druga implementacja, choćby fake w testach.

Zobacz: sekcja „Za dużo abstrakcji”.

</details>

### 38. Co zrobić, gdy logika biznesowa „wycieka” do kontrolerów albo zapytań SQL?

<details>
<summary>Odpowiedź</summary>

Przenieść regułę do domeny i nadać jej nazwę. Jeśli filtr w SQL musi zostać ze względów wydajności, powinien być nazwaną metodą portu (np. `active_for(customer_id)`) opisaną testem kontraktowym, a nie anonimowym warunkiem w zapytaniu. Zapobiegają temu testy use case'ów bez HTTP (reguła, która nie działa bez kontrolera, siedzi w kontrolerze) i code review z pytaniem, czy ekspert biznesowy nazwałby dany `if`.

Zobacz: sekcja „Logika w złym miejscu”.

</details>

### 39. Jak radzić sobie z wydajnością (N+1, lazy loading, złożone raporty) bez łamania granic?

<details>
<summary>Odpowiedź</summary>

Optymalizować w adapterach i portach odczytu, nie w domenie. Pętlę `get` zastąpić metodą portu `get_many`, agregat ładować w całości (`selectinload`, JOIN) zamiast polegać na lazy loadingu, raporty i listy obsługiwać osobnym portem odczytu z płaskim modelem i surowym SQL-em (CQRS), a wolne API ukryć za cache w adapterze. Domena nie dostaje sesji ORM, a use case nie buduje SQL-a.

Zobacz: sekcja „Wydajność bez łamania granic”.

</details>

### 40. Jak stopniowo zmigrować istniejący monolit warstwowy do hexagonal (strangler, anti-corruption layer)?

<details>
<summary>Odpowiedź</summary>

Nie przepisywać całości, tylko iść scenariusz po scenariuszu według wzorca strangler fig: zamrozić zachowanie testami charakteryzującymi, wybrać jeden często zmieniany scenariusz, wyciągnąć use case i domenę, dodać porty, zaimplementować je adapterami do istniejącego kodu, przełączyć kontroler na nowy use case i usunąć starą ścieżkę. Kontakt ze starym modelem odbywa się przez anti-corruption layer, czyli adapter tłumaczący pojęcia starego systemu (`FLAG_VIP == "T"`) na język nowej domeny (`Tier.GOLD`).

Zobacz: sekcja „Migracja istniejącego systemu”.

</details>
