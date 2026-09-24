# Clean na tle innych architektur

Martin nie twierdził, że wymyślił coś nowego. W artykule z 2012 roku wymienia kilka wcześniejszych architektur i pokazuje, że wszystkie dzielą system na warstwy z regułami biznesowymi w środku. Clean Architecture próbuje połączyć je w jeden spójny obraz. Ten rozdział pokazuje, co z nich wzięła i jak łączy się z rozdzieleniem zapisu od odczytu oraz z modelowaniem domeny.

```text
1992  BCE (Jacobson)            Boundary, Control, Entity w przypadkach użycia
2003  DDD (Evans)               jak modelować wnętrze
2005  Hexagonal (Cockburn)      porty i adaptery na granicy
2008  Onion (Palermo)           koncentryczne warstwy z nazwanym wnętrzem
2009  DCI (Reenskaug, Coplien)  dane, kontekst, interakcje
2012  Clean (Martin)            synteza z jawną Dependency Rule
```

## Co Martin wziął od innych

Od <a id="term-hexagonal-architecture"></a>[architektury heksagonalnej](00%20Glossary%20Clean.md#hexagonal-architecture) Alistaira Cockburna Clean wzięła pomysł granicy, przez którą aplikacja komunikuje się ze światem. U Cockburna granica składa się z <a id="term-port"></a>[portów](00%20Glossary%20Clean.md#port), czyli interfejsów należących do aplikacji, i <a id="term-adapter"></a>[adapterów](00%20Glossary%20Clean.md#adapter), czyli ich implementacji dla konkretnej technologii. Nazwa kręgu Interface Adapters nawiązuje do tego słownika.

Od <a id="term-onion-architecture"></a>[architektury cebulowej](00%20Glossary%20Clean.md#onion-architecture) Jeffreya Palermo wzięła koncentryczne warstwy z nazwanym wnętrzem i zasadę, że infrastruktura, UI i testy leżą razem na zewnątrz.

Od BCE Ivara Jacobsona wzięła przypadki użycia jako centralny element architektury. Interactor to w praktyce obiekt Control z BCE, a boundaries to jego obiekty Boundary.

Dodała od siebie:

- jawnie nazwaną Dependency Rule jako jedną zasadę, z której wynika reszta,
- podział zewnętrza na dwa kręgi: Interface Adapters i Frameworks & Drivers,
- nazwany przepływ przez granicę: Input i Output Boundary, Request i Response Model, Presenter i View Model,
- zasady komponentów (rozdział 04) i wzorce Humble Object, Main Component oraz granice częściowe (rozdział 05).

## Jak odpowiadają sobie warstwy

| Clean | Onion | Hexagonal |
|---|---|---|
| Entities | Domain Model (+ część Domain Services) | domena w rdzeniu |
| Use Cases (Interactors) | Application Services | use case'y w rdzeniu, realizacja portów wejściowych |
| Input Boundary | interfejs serwisu aplikacyjnego (opcjonalny) | port wejściowy |
| Gateway (interfejs) | interfejs repozytorium w Domain Services | port wyjściowy |
| Output Boundary | brak odpowiednika | port wyjściowy w stronę UI |
| Interface Adapters | część pierścienia zewnętrznego | adaptery wejściowe i wyjściowe |
| Frameworks & Drivers | część pierścienia zewnętrznego | technologia za adapterami |

Najważniejsza różnica dotyczy Output Boundary. W Hexagonal i Onion wynik zwykle wraca z use case'u jako wartość. Clean formalizuje wyjście jako osobny interfejs z presenterem. W Hexagonal można to zapisać jako port wyjściowy, którego adapterem jest presenter, ale w praktyce rzadko się to robi.

Druga różnica to akcent. Hexagonal najwięcej mówi o granicy i symetrii jej stron. Onion najwięcej mówi o warstwach wewnątrz. Clean opisuje jedno i drugie, a do tego zasady podziału na komponenty.

Na rozmowie dobrze powiedzieć wprost, że mechanizm jest wspólny: odwrócenie zależności zastosowane do całej aplikacji. Różnice dotyczą nazw, metafory i poziomu szczegółowości. Szczegółowe porównania są w tutorialach [hexagonal](../Hexagonal/) i [onion](../Onion/).

## Zapis i odczyt osobno

<a id="term-cqrs"></a>[CQRS](00%20Glossary%20Clean.md#cqrs) (Command Query Responsibility Segregation) rozdziela operacje zmieniające stan od operacji odczytu. W Clean Architecture oznacza to dwa rodzaje interactorów.

Interactory komend (`ReserveRoom`, `CancelReservation`) ładują encje przez gateway'e, wywołują ich reguły i zapisują zmiany. Interactory zapytań (`ShowRoomSchedule`) nie potrzebują encji, bo nie ma czego chronić. Korzystają z gateway'a odczytu, który zwraca gotowy <a id="term-read-model"></a>[model odczytu](00%20Glossary%20Clean.md#read-model):

```python
# use_cases/show_room_schedule.py
@dataclass(frozen=True)
class ScheduleEntry:                           # model odczytu
    reservation_id: str
    organizer_name: str
    start: datetime
    end: datetime


class ScheduleQueryGateway(Protocol):         # gateway odczytu
    def for_day(self, room_id: str, day: date) -> list[ScheduleEntry]: ...


class ShowRoomScheduleInteractor:
    def execute(self, request: ShowRoomScheduleRequest) -> None:
        entries = self._schedule.for_day(request.room_id, request.day)
        self._output.present(ShowRoomScheduleResponse(request.room_id, entries))
```

```text
komenda:   Controller ──► Interactor ──► Entities ──► Gateway (zapis) ──► tabele
zapytanie: Controller ──► Interactor ──────────────► Gateway (odczyt) ──► widok SQL / Elasticsearch
```

Dependency Rule obowiązuje po obu stronach. Interactor zapytania nadal zna tylko interfejs z kręgu Use Cases. Implementacja gateway'a odczytu może użyć surowego SQL-a z JOIN-ami albo osobnej bazy do odczytu, bo to szczegół. Interactor zapytania bywa bardzo cienki, co jest w porządku, bo pilnuje granicy, a nie logiki.

## Model domeny według DDD

<a id="term-ddd"></a>[Domain-Driven Design](00%20Glossary%20Clean.md#ddd) Erica Evansa opisuje, jak modelować złożoną logikę biznesową. Clean Architecture mówi, gdzie ten model mieszka i jak go chronić. Oba podejścia dobrze się uzupełniają:

| Element DDD | Krąg Clean |
|---|---|
| encje, value objects, agregaty, zdarzenia domenowe | Entities |
| serwisy domenowe | Entities (reguły przedsiębiorstwa) |
| serwisy aplikacyjne | Use Cases (interactory) |
| interfejs repozytorium | gateway w Use Cases |
| implementacja repozytorium, anti-corruption layer | Interface Adapters |
| bounded context | osobny zestaw kręgów lub osobny komponent |

Jest jedna różnica w słownictwie, o którą warto zadbać na rozmowie. Entities w Clean to cały krąg reguł przedsiębiorstwa, w tym funkcje i serwisy. Encja w DDD to konkretny obiekt z tożsamością. `TimeSlot` jest w kręgu Entities, ale w DDD jest value objectem, a nie encją.

Clean nie wymaga DDD. Przy prostej domenie krąg Entities może zawierać kilka funkcji i dataclass. DDD bez izolacji z Clean jest możliwe, ale model łatwiej zanieczyścić ORM-em i frameworkiem.

## Co zapamiętać

- Clean to synteza Hexagonal, Onion, BCE i DCI z jawną Dependency Rule.
- Od Hexagonal pochodzi idea portów i adapterów, od Onion koncentryczne warstwy, od BCE przypadki użycia w centrum.
- Gateway odpowiada portowi wyjściowemu i interfejsowi repozytorium, Input Boundary odpowiada portowi wejściowemu.
- Output Boundary z presenterem to element, którego w tej formie nie mają Hexagonal ani Onion.
- W CQRS interactory zapytań korzystają z gateway'a odczytu i pomijają encje.
- DDD wypełnia krąg Entities, ale „Entities” w Clean to szersze pojęcie niż encja w DDD.

## Pytania sprawdzające

### 36. Czym Clean Architecture różni się od Hexagonal i Onion? Co Martin z nich wziął?

<details>
<summary>Odpowiedź</summary>

Z Hexagonal wziął granicę z portami i adapterami (do niej nawiązuje nazwa Interface Adapters), z Onion koncentryczne warstwy z nazwanym wnętrzem i infrastrukturę na zewnątrz, a z BCE przypadki użycia w centrum. Dodał jawną Dependency Rule, podział zewnętrza na dwa kręgi, nazwany przepływ przez granicę (boundaries, Request i Response Model, Presenter, View Model), zasady komponentów oraz wzorce Humble Object i Main Component. Mechanizm odwrócenia zależności jest we wszystkich trzech ten sam.

Zobacz: sekcja „Co Martin wziął od innych”.

</details>

### 37. Jak odpowiadają sobie kręgi Clean, pierścienie Onion i porty oraz adaptery Hexagonal?

<details>
<summary>Odpowiedź</summary>

Entities odpowiadają Domain Model (i części Domain Services) w Onion oraz domenie w rdzeniu hexagonal. Use Cases odpowiadają Application Services oraz use case'om realizującym porty wejściowe. Input Boundary to port wejściowy, gateway to port wyjściowy lub interfejs repozytorium, Interface Adapters to adaptery, a Frameworks & Drivers to technologia za nimi (w Onion oba ostatnie to jeden pierścień zewnętrzny). Output Boundary z presenterem nie ma bezpośredniego odpowiednika.

Zobacz: sekcja „Jak odpowiadają sobie warstwy”.

</details>

### 38. Jak Clean Architecture łączy się z CQRS i DDD?

<details>
<summary>Odpowiedź</summary>

CQRS: interactory komend ładują encje i zapisują zmiany, a interactory zapytań korzystają z gateway'a odczytu zwracającego płaski model odczytu, z pominięciem encji. Dependency Rule obowiązuje po obu stronach. DDD: encje, value objects, agregaty i serwisy domenowe trafiają do kręgu Entities, serwisy aplikacyjne do Use Cases, interfejs repozytorium to gateway, a implementacja leży w Interface Adapters. Uwaga: „Entities” w Clean to cały krąg reguł, a encja w DDD to obiekt z tożsamością.

Zobacz: sekcje „Zapis i odczyt osobno” i „Model domeny według DDD”.

</details>
