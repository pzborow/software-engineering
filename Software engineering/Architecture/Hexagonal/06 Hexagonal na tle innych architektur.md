# Hexagonal na tle innych architektur

Architektura heksagonalna ma dwie bliskie krewne, które pojawiają się w każdej rozmowie o niej, i jedno podejście, z którym często jest mylona. Dobrze znać różnice, ale ważniejsze jest zrozumienie, że te trzy architektury opisują ten sam pomysł.

```text
2005  Hexagonal (Cockburn)      rdzeń + porty + adaptery
2008  Onion (Palermo)           koncentryczne warstwy, domena w środku
2012  Clean (Martin)            koncentryczne kręgi + reguła zależności
2003  DDD (Evans)               jak modelować to, co jest w środku
```

## Trzy nazwy, jedna idea

<a id="term-onion-architecture"></a>[Onion Architecture](00%20Glossary%20Hexagonal.md#onion-architecture) Jeffreya Palermo rysuje aplikację jak cebulę: w środku model domeny, wokół serwisy domenowe, dalej serwisy aplikacyjne, a na zewnątrz UI, testy i infrastruktura. Zależności wskazują do środka.

<a id="term-clean-architecture"></a>[Clean Architecture](00%20Glossary%20Hexagonal.md#clean-architecture) Roberta C. Martina rysuje koncentryczne kręgi: Entities, Use Cases, Interface Adapters, Frameworks & Drivers. Martin nazwał wprost regułę zależności i uznał hexagonal oraz onion za przykłady tej samej idei.

```text
Hexagonal                 Onion                        Clean
─────────                 ─────                        ─────
adaptery                  infrastruktura / UI / testy  Frameworks & Drivers
porty                     interfejsy w warstwach       Interface Adapters (granice)
application / use case    Application Services         Use Cases
domena                    Domain Services + Model      Entities
```

## Co je różni

Różnice dotyczą głównie tego, jak szczegółowo opisany jest środek:

| | Hexagonal | Onion | Clean |
|---|---|---|---|
| Główna metafora | wnętrze i zewnętrze, porty | warstwy cebuli | koncentryczne kręgi |
| Podział rdzenia | nie narzuca | model, serwisy domenowe, serwisy aplikacyjne | Entities, Use Cases |
| Nacisk | symetria stron driving/driven | domena w samym centrum | use case'y jako centrum projektu |
| Słownik | port, adapter | warstwa, interfejs | boundary, interactor, presenter |

Hexagonal mówi najmniej o wnętrzu, a najwięcej o granicy. Onion i Clean dzielą wnętrze na nazwane warstwy. W praktyce projekt opisany jako „clean” i projekt opisany jako „hexagonal” zwykle wyglądają prawie tak samo: `domain`, `application`, `adapters`, zależności do środka.

## Co je łączy

Wszystkie trzy opierają się na tych samych zasadach:

- logika biznesowa nie zależy od frameworka, bazy ani UI,
- zależności w kodzie wskazują do środka,
- rdzeń definiuje interfejsy, infrastruktura je implementuje,
- rdzeń da się testować bez infrastruktury.

Na rozmowie dobrze to powiedzieć wprost: różnice są w metaforze i poziomie szczegółu, a mechanizm jest wspólny. To odwrócenie zależności zastosowane do całej aplikacji.

## Czym jest DDD

<a id="term-ddd"></a>[Domain-Driven Design](00%20Glossary%20Hexagonal.md#ddd) Erica Evansa jest podejściem do modelowania złożonej logiki biznesowej. Nie mówi, jak podłączyć bazę, tylko jak zbudować model, który odzwierciedla język i reguły ekspertów.

DDD ma dwie części. Strategiczna dzieli duży system na części z własnym modelem i językiem. Taka część to <a id="term-bounded-context"></a>[bounded context](00%20Glossary%20Hexagonal.md#bounded-context), na przykład „Sprzedaż”, „Magazyn”, „Fakturowanie”. Słowo „produkt” może znaczyć coś innego w każdym z nich.

Taktyczna część daje cegiełki do budowania modelu wewnątrz kontekstu:

<a id="term-entity"></a>[Encja](00%20Glossary%20Hexagonal.md#entity) ma tożsamość, która trwa mimo zmian stanu. Zamówienie `o-42` pozostaje tym samym zamówieniem po dodaniu pozycji.

<a id="term-value-object"></a>[Value object](00%20Glossary%20Hexagonal.md#value-object) nie ma tożsamości i jest porównywany po wartości. `Money(50, "PLN")` jest równe każdemu innemu `Money(50, "PLN")`. Jest niezmienny.

<a id="term-aggregate"></a>[Agregat](00%20Glossary%20Hexagonal.md#aggregate) to grupa obiektów pilnowana przez jeden korzeń. `Order` jest korzeniem, a `OrderLine` można zmieniać tylko przez metody zamówienia. Agregat jest jednostką spójności: zapisuje się go w całości, w jednej transakcji.

```python
@dataclass(frozen=True)
class Money:                        # value object
    amount: Decimal
    currency: str


@dataclass
class Order:                        # encja i korzeń agregatu
    id: str
    lines: list[OrderLine]          # część agregatu, zmieniana tylko przez Order

    def add_line(self, sku: str, quantity: int, unit_price: Money) -> None:
        ...                         # pilnuje niezmienników całego agregatu
```

## Jak hexagonal i DDD się uzupełniają

Hexagonal odpowiada na pytanie „jak odizolować rdzeń”. DDD odpowiada na pytanie „co włożyć do rdzenia”. Dlatego często występują razem:

```text
DDD strategiczne    bounded context      ≈ jeden heksagon
DDD taktyczne       encje, agregaty      = zawartość katalogu domain
Hexagonal           porty, adaptery      = granica wokół kontekstu
Oba                 repozytorium         = port wyjściowy per agregat
```

Repozytorium w DDD operuje na całych agregatach: `OrderRepository.save(order)` zapisuje zamówienie razem z pozycjami. Nie ma osobnego `OrderLineRepository`.

## Czy jedno wymaga drugiego

Nie. Hexagonal bez DDD jest w pełni poprawny. Rdzeń może zawierać proste obiekty i funkcje, bo ważna jest izolacja, a nie słownik DDD. Tak wygląda wiele mniejszych serwisów.

DDD bez hexagonal też jest możliwe, na przykład w klasycznych warstwach. Jest jednak trudniejsze, bo model domeny łatwo zostaje zanieczyszczony adnotacjami ORM i szczegółami frameworka. Izolacja z hexagonal chroni model, który DDD pieczołowicie buduje.

| Połączenie | Kiedy ma sens |
|---|---|
| Hexagonal bez DDD | średnia złożoność, potrzeba testowalności i wymienności adapterów |
| DDD bez hexagonal | rzadko, zwykle w starszych systemach warstwowych |
| Hexagonal i DDD | złożona domena, wiele reguł, długie życie systemu |
| Żadne | prosty CRUD, prototyp |

## Co zapamiętać

- Hexagonal, Onion i Clean to ta sama idea: rdzeń niezależny od technologii i zależności do środka.
- Hexagonal opisuje głównie granicę, Onion i Clean dodatkowo dzielą wnętrze na warstwy.
- DDD opisuje, jak modelować logikę wewnątrz rdzenia.
- Bounded context często odpowiada jednemu heksagonowi.
- Encja ma tożsamość, value object jest porównywany po wartości, agregat jest jednostką spójności.
- Repozytorium to port wyjściowy operujący na całych agregatach.
- Hexagonal nie wymaga DDD, ale bardzo dobrze chroni model DDD.

## Pytania sprawdzające

### 29. Czym hexagonal różni się od Clean Architecture i Onion Architecture? Co je łączy?

<details>
<summary>Odpowiedź</summary>

Łączy je ta sama idea: rdzeń niezależny od frameworka i bazy, zależności wskazujące do środka, interfejsy definiowane przez rdzeń i implementowane przez infrastrukturę. Różnią się metaforą i szczegółowością. Hexagonal opisuje granicę (porty, adaptery, strony driving i driven) i nie narzuca podziału wnętrza. Onion dzieli wnętrze na model domeny, serwisy domenowe i aplikacyjne. Clean nazywa kręgi (Entities, Use Cases, Interface Adapters, Frameworks & Drivers) i formułuje regułę zależności wprost.

Zobacz: sekcje „Trzy nazwy, jedna idea”, „Co je różni”, „Co je łączy”.

</details>

### 30. Jak hexagonal ma się do DDD? Czy jedno wymaga drugiego?

<details>
<summary>Odpowiedź</summary>

Uzupełniają się: hexagonal odpowiada na pytanie, jak odizolować rdzeń, a DDD na pytanie, co w nim umieścić (encje, value objects, agregaty). Bounded context często odpowiada jednemu heksagonowi, a repozytorium agregatu jest portem wyjściowym. Żadne nie wymaga drugiego. Hexagonal bez DDD jest normalny w prostszych serwisach, DDD bez hexagonal jest możliwe, ale model łatwiej wtedy zanieczyścić szczegółami ORM i frameworka.

Zobacz: sekcje „Jak hexagonal i DDD się uzupełniają” i „Czy jedno wymaga drugiego”.

</details>
