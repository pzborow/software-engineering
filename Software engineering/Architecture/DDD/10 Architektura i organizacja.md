# Architektura i organizacja

DDD nie narzuca architektury aplikacji ani struktury zespołów, ale ma na nie silny wpływ. Model domeny potrzebuje ochrony przed technologią, a granice kontekstów muszą się zgadzać z tym, jak ludzie ze sobą pracują. Ten rozdział łączy DDD z architekturami z tutoriali [hexagonal](../Hexagonal/), [onion](../Onion/) i [clean](../Clean/) oraz z organizacją zespołów.

```text
organizacja            ──►  zespoły (Team Topologies)
     │                              │
     ▼                              ▼
strategia (subdomeny)  ──►  bounded contexts  ──►  moduły lub serwisy
                                    │
                                    ▼
                         architektura wewnątrz kontekstu
                         (hexagonal / onion / clean)
                                    │
                                    ▼
                         model domeny w środku
```

## Model w środku architektury

Wzorce taktyczne DDD opisują, co jest w modelu domeny. Nie mówią, jak odizolować go od bazy, frameworka i API. To zadanie architektury aplikacji. <a id="term-hexagonal-architecture"></a>[Architektura heksagonalna](00%20Glossary%20DDD.md#hexagonal-architecture) i jej krewne, Onion i Clean, dają dokładnie tę izolację: model w środku, technologia na zewnątrz, zależności tylko do środka.

| Element DDD | Hexagonal | Onion | Clean |
|---|---|---|---|
| encje, value objects, agregaty, zdarzenia domenowe | domena w rdzeniu | Domain Model | Entities |
| serwisy domenowe | domena w rdzeniu | Domain Services | Entities |
| serwisy aplikacyjne (przypadki użycia) | use case'y, porty wejściowe | Application Services | Use Cases |
| interfejs repozytorium | port wyjściowy | interfejs w Domain Services | gateway |
| implementacja repozytorium, ACL, publikacja zdarzeń | adaptery wyjściowe | pierścień zewnętrzny | Interface Adapters |
| API, konsumenci zdarzeń | adaptery wejściowe | pierścień zewnętrzny | Interface Adapters, Frameworks |

W środku jest więc cała taktyczna część DDD: agregaty z niezmiennikami, value objects, serwisy domenowe i zdarzenia domenowe. Serwisy aplikacyjne orkiestrują przypadki użycia wokół nich. Repozytoria są interfejsami zdefiniowanymi przy modelu, a ich implementacje, podobnie jak ACL i tłumaczenie zdarzeń integracyjnych, są na zewnątrz.

```text
rental/                         ← jeden bounded context
├── domain/                     agregaty, VO, serwisy domenowe, zdarzenia, interfejsy repozytoriów
├── application/                przypadki użycia, polityki, publikacja zdarzeń integracyjnych
└── adapters/
    ├── inbound/                REST, konsumenci zdarzeń z innych kontekstów
    └── outbound/               repozytoria SQL, ACL do legacy fleet, outbox
```

Taka architektura dotyczy jednego kontekstu. Różne konteksty mogą mieć różną architekturę. Core domain z bogatym modelem uzasadnia hexagonal z pełnym zestawem portów. Supporting subdomain z prostym CRUD-em może być zwykłą aplikacją warstwową albo nawet gotowym panelem administracyjnym.

## Zespoły kształtują system

<a id="term-conways-law"></a>[Prawo Conwaya](00%20Glossary%20DDD.md#conways-law) Melvina Conwaya z 1968 roku mówi, że organizacje projektują systemy, które odwzorowują ich strukturę komunikacji. Jeśli trzy zespoły budują jeden system, powstanie system z trzech części, niezależnie od tego, co zakłada projekt.

Dla DDD ma to dwie konsekwencje:

- granice kontekstów, które nie pokrywają się z granicami zespołów, z czasem się rozmywają. Kontekst rozwijany przez dwa zespoły zaczyna mieć dwa języki, a dwa konteksty jednego zespołu zaczynają się zlewać,
- relacje na mapie kontekstów (rozdział 05) wynikają z relacji między zespołami. Customer–Supplier działa tylko wtedy, gdy zespół dostawcy ma powód słuchać klienta.

Świadome wykorzystanie tego prawa to <a id="term-inverse-conway"></a>[odwrotny manewr Conwaya](00%20Glossary%20DDD.md#inverse-conway) (inverse Conway maneuver): najpierw projektuje się pożądane granice systemu, a potem kształtuje zespoły tak, żeby im odpowiadały. Jeśli wycena ma być osobnym kontekstem core, potrzebuje osobnego zespołu z własnymi ekspertami.

<a id="term-team-topologies"></a>[Team Topologies](00%20Glossary%20DDD.md#team-topologies) Matthew Skeltona i Manuela Paisa z 2019 roku opisuje cztery typy zespołów, które dobrze pasują do DDD:

| Typ zespołu | Rola | Związek z DDD |
|---|---|---|
| stream-aligned | dostarcza wartość w jednym strumieniu biznesowym, od końca do końca | właściciel jednego lub kilku bounded contextów, zwykle core i supporting |
| platform | dostarcza wewnętrzne usługi, z których korzystają inne zespoły | broker, outbox, obserwowalność, generic subdomains jako usługi |
| enabling | pomaga innym zespołom zdobyć nowe umiejętności | coaching DDD, prowadzenie Event Stormingu |
| complicated-subsystem | utrzymuje część wymagającą specjalistycznej wiedzy | np. silnik optymalizacji floty jako cohesive mechanism |

Team Topologies wprowadza też pojęcie obciążenia poznawczego zespołu. Jeden zespół nie powinien odpowiadać za więcej kontekstów, niż potrafi zrozumieć. To praktyczne ograniczenie rozmiaru i liczby kontekstów: jeśli zespół ma za dużo kontekstów, zaczyna je traktować powierzchownie, a model w każdym z nich się degeneruje.

W wypożyczalni może to wyglądać tak: zespół wyceny (stream-aligned, kontekst `Pricing`), zespół rezerwacji i najmu (stream-aligned, `Reservations` i `Rental`), zespół floty (stream-aligned, `Fleet` i `Claims`), zespół platformy (broker, `Identity`, integracja z `Billing`) oraz zespół optymalizacji (complicated-subsystem, model prognozy popytu używany przez wycenę).

## Jedno wdrożenie czy wiele

DDD bywa utożsamiane z <a id="term-microservice"></a>[mikroserwisami](00%20Glossary%20DDD.md#microservice), czyli kontekstami wdrażanymi jako osobne procesy z własnymi bazami, bo bounded context wydaje się naturalną granicą serwisu. To dobra heurystyka, ale nie reguła. <a id="term-modular-monolith"></a>[Modularny monolit](00%20Glossary%20DDD.md#modular-monolith) z kontekstami jako modułami jest pełnoprawną realizacją DDD, tak samo jak mikroserwisy.

| | Modularny monolit | Mikroserwisy |
|---|---|---|
| Granice kontekstów | moduły pilnowane testami architektury | procesy i sieć |
| Komunikacja | wywołania w procesie, zdarzenia w pamięci lub przez outbox | HTTP, gRPC, broker |
| Transakcje | możliwe lokalnie w obrębie modułu, pokusa przekraczania granic | tylko w obrębie serwisu |
| Wdrożenie | jedno, prostsze | niezależne per serwis, wymaga platformy |
| Koszt błędnych granic | refaktoryzacja w jednym repozytorium | zmiany kontraktów sieciowych, migracje danych |
| Kiedy | nowy system, niepewne granice, mały zespół | stabilne granice, wiele zespołów, różne wymagania skalowania |

Od czego zacząć w nowym systemie? Najczęstsza rekomendacja brzmi: od modularnego monolitu z wyraźnymi granicami kontekstów. Granice na początku projektu są niepewne, bo wiedza o domenie dopiero rośnie. Przesunięcie granicy w monolicie to refaktoryzacja, a w mikroserwisach migracja danych i zmiana kontraktów sieciowych. Gdy granica okaże się stabilna, a kontekst potrzebuje niezależnego wdrożenia, skalowania albo osobnego zespołu, wydziela się go do serwisu. Dzięki izolacji modułu jest to decyzja wdrożeniowa, a nie przeprojektowanie.

```toml
# pyproject.toml: granice kontekstów w modularnym monolicie
[[tool.importlinter.contracts]]
name = "Konteksty są niezależne"
type = "independence"
modules = ["carrental.pricing", "carrental.reservations", "carrental.rental", "carrental.fleet"]

[[tool.importlinter.contracts]]
name = "Komunikacja tylko przez publiczne API kontekstu"
type = "forbidden"
source_modules = ["carrental.reservations"]
forbidden_modules = ["carrental.pricing.domain", "carrental.pricing.adapters"]
```

Mikroserwisy od początku mają sens, gdy granice są dobrze znane (np. system budowany ponownie po latach doświadczeń), kilka niezależnych zespołów zaczyna pracę równolegle albo konteksty mają skrajnie różne wymagania technologiczne lub wydajnościowe.

## Co zapamiętać

- DDD opisuje model domeny, a hexagonal, onion i clean izolują go od technologii. Model jest w środku.
- Architekturę wybiera się per kontekst: bogaty model w core, prostsze rozwiązania w supporting i generic.
- Prawo Conwaya sprawia, że granice kontekstów muszą odpowiadać granicom zespołów.
- Odwrotny manewr Conwaya kształtuje zespoły pod pożądane granice systemu.
- Team Topologies: zespoły stream-aligned są właścicielami kontekstów, platform dostarcza usług wspólnych, enabling uczy, complicated-subsystem utrzymuje specjalistyczne mechanizmy. Obciążenie poznawcze ogranicza liczbę kontekstów na zespół.
- Nowy system zwykle zaczyna się od modularnego monolitu, a konteksty wydziela do serwisów, gdy ich granice są stabilne.

## Pytania sprawdzające

### 45. Jak DDD łączy się z architekturą heksagonalną, onion i clean? Która część DDD jest „w środku”?

<details>
<summary>Odpowiedź</summary>

DDD opisuje zawartość modelu, a te architektury izolują go od technologii przez zależności skierowane do środka. W środku są agregaty, value objects, serwisy domenowe i zdarzenia domenowe (w hexagonal domena w rdzeniu, w Onion Domain Model i Domain Services, w Clean Entities). Wokół nich są serwisy aplikacyjne (use case'y, Application Services, Use Cases), interfejsy repozytoriów przy modelu, a implementacje repozytoriów, ACL i publikacja zdarzeń integracyjnych na zewnątrz w adapterach. Architekturę wybiera się per kontekst.

Zobacz: sekcja „Model w środku architektury”.

</details>

### 46. Jak prawo Conwaya i Team Topologies (stream-aligned, platform, enabling) wpływają na granice kontekstów?

<details>
<summary>Odpowiedź</summary>

Prawo Conwaya mówi, że system odwzorowuje strukturę komunikacji organizacji. Granice kontekstów niezgodne z granicami zespołów się rozmywają, a relacje na mapie kontekstów wynikają z relacji między zespołami. Odwrotny manewr Conwaya kształtuje zespoły pod pożądane granice. W Team Topologies zespoły stream-aligned są właścicielami kontekstów core i supporting, platform dostarcza usług wspólnych i generic, enabling uczy DDD i prowadzi warsztaty, a complicated-subsystem utrzymuje mechanizmy specjalistyczne. Obciążenie poznawcze ogranicza liczbę kontekstów na zespół.

Zobacz: sekcja „Zespoły kształtują system”.

</details>

### 47. Jak DDD odnosi się do mikroserwisów i modularnego monolitu? Od czego zacząć w nowym systemie?

<details>
<summary>Odpowiedź</summary>

Bounded context jest dobrą heurystyką granicy serwisu, ale modularny monolit z kontekstami jako modułami też jest pełnoprawnym DDD. Monolit daje prostsze wdrożenie i tańsze poprawianie granic, a mikroserwisy niezależne wdrożenie i skalowanie kosztem sieci i kosztownych zmian kontraktów. W nowym systemie zwykle zaczyna się od modularnego monolitu z granicami pilnowanymi testami architektury, a konteksty wydziela się, gdy granice są stabilne i potrzeba niezależności. Mikroserwisy od początku mają sens przy znanych granicach, wielu zespołach albo skrajnie różnych wymaganiach.

Zobacz: sekcja „Jedno wdrożenie czy wiele”.

</details>
