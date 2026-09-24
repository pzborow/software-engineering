# Bounded contexts

Rozdział 02 pokazał, że „klient” znaczy co innego w rezerwacjach, rozliczeniach i marketingu. Ten rozdział odpowiada na pytanie, co z tym zrobić w oprogramowaniu: jak podzielić system na części, w których każde słowo ma jedno znaczenie, jak wyznaczać granice tych części i jak je zmieniać, gdy okażą się złe.

```text
┌─ Reservations ─────────┐  ┌─ Rental ──────────────┐  ┌─ Billing ─────────────┐
│ Reservation            │  │ RentalAgreement       │  │ Invoice               │
│ Booker                 │  │ Driver                │  │ Payer                 │
│ VehicleClass           │  │ Vehicle (VIN, stan)   │  │ BillingAccount        │
│ „klient” = rezerwujący │  │ „klient” = kierowca   │  │ „klient” = płatnik    │
└────────────────────────┘  └───────────────────────┘  └───────────────────────┘
```

## Granica jednego modelu

<a id="term-bounded-context"></a>[Bounded context](00%20Glossary%20DDD.md#bounded-context) to jawna granica, wewnątrz której obowiązuje jeden model i jeden język. W jej obrębie każde pojęcie ma dokładnie jedno znaczenie. Poza nią to samo słowo może oznaczać coś innego i to jest w porządku.

Bounded context ma kilka wymiarów naraz:

- językowy: słownik pojęć, w którym „klient” znaczy jedno,
- modelowy: klasy, reguły i niezmienniki spójne ze sobą,
- techniczny: zwykle osobny moduł lub serwis, z własnym schematem danych,
- organizacyjny: najlepiej jeden zespół odpowiedzialny za cały kontekst.

Dlaczego nie jeden model dla całej firmy? Takie podejście, czyli <a id="term-enterprise-model"></a>[model korporacyjny](00%20Glossary%20DDD.md#enterprise-model), próbowano wdrażać w latach 90. i 2000. jako „jeden kanoniczny model danych”. Przegrywa z kilku powodów:

- każdy dział potrzebuje innych atrybutów i reguł, więc wspólna klasa rośnie do dziesiątek pól, z których każdy używa kilku,
- reguły jednego działu blokują zmiany w innych: rozliczenia wymagają NIP, a rezerwacja przez aplikację mobilną go nie ma,
- zmiana wymaga zgody wszystkich zespołów, więc system przestaje się rozwijać,
- nie da się utrzymać jednego języka w organizacji, w której różne działy naprawdę myślą o świecie inaczej.

Evans odwraca to podejście: zamiast walczyć o jeden model, jawnie wyznacza się granice, w których modele mogą się różnić, i jawnie projektuje się tłumaczenie między nimi.

## Jak wyznaczyć granice

Nie ma algorytmu wyznaczania kontekstów. Są heurystyki, które warto stosować razem:

| Heurystyka | Pytanie | Przykład w wypożyczalni |
|---|---|---|
| Język | Gdzie to samo słowo zmienia znaczenie? | „klient” w rezerwacjach i rozliczeniach |
| Eksperci | Kto jest ekspertem od tej części? | kierownik oddziału a analityk cen |
| Proces biznesowy | Gdzie kończy się jeden etap i zaczyna drugi? | rezerwacja kończy się wydaniem auta |
| Zmiany | Co zmienia się razem, a co niezależnie? | cennik zmienia się co tydzień, proces wydania raz na rok |
| Dane | Kto jest właścicielem danych i ich cyklu życia? | stan techniczny auta należy do floty |
| Zespoły | Kto będzie to rozwijał? | zespół wyceny, zespół operacji w oddziałach |
| Zdarzenia przełomowe | Po jakim zdarzeniu zmienia się odpowiedzialność? | `VehicleHandedOver`, `VehicleReturned` |

<a id="term-pivotal-event"></a>[Zdarzenie przełomowe](00%20Glossary%20DDD.md#pivotal-event) (pivotal event) to pojęcie Alberta Brandoliniego z Event Stormingu. Oznacza zdarzenie, po którym proces przechodzi do innej fazy, często obsługiwanej przez innych ludzi. `ReservationConfirmed`, `VehicleHandedOver` i `VehicleReturned` dzielą wynajem na fazy: przed wydaniem (rezerwacje), w trakcie (umowa najmu), po zwrocie (rozliczenie i szkody). Takie zdarzenia są dobrymi kandydatami na granice kontekstów.

W wypożyczalni wynik może wyglądać tak:

| Kontekst | Odpowiada za | Subdomena |
|---|---|---|
| `Pricing` | wycena najmu, reguły cenowe, prognoza popytu | core |
| `Reservations` | rezerwacje, dostępność klas aut | core i supporting |
| `Rental` | wydanie, umowa najmu, zwrot | supporting |
| `Fleet` | ewidencja, serwis, przesunięcia aut | supporting, planowanie w core |
| `Claims` | szkody, protokoły, likwidacja | supporting |
| `Billing` | faktury, płatności, kaucje | generic (integracja) |
| `Identity` | konta, logowanie | generic (gotowe rozwiązanie) |

## Rozmiar kontekstu

Nie ma właściwej liczby klas ani linii kodu. Rozmiar ocenia się po objawach.

Kontekst za duży:

- to samo słowo ma w nim kilka znaczeń, a klasy mają pola używane tylko przez część kodu,
- kilka zespołów wchodzi sobie w drogę w tym samym kodzie,
- zmiana w jednej części wymaga testowania niezwiązanych części,
- eksperci z różnych działów nie rozumieją nawzajem swoich części modelu.

Kontekst za mały:

- prosty proces biznesowy wymaga współpracy kilku kontekstów i zdarzeń między nimi,
- większość zmian obejmuje dwa lub trzy konteksty naraz,
- konteksty współdzielą dużo danych i często o nie się pytają,
- pojawia się potrzeba transakcji między kontekstami.

Lepiej zacząć od kontekstów nieco za dużych i dzielić je, gdy pojawią się objawy. Połączenie dwóch źle podzielonych kontekstów jest trudniejsze niż podział jednego.

## Kontekst a jednostka wdrożenia

<a id="term-microservice"></a>[Mikroserwis](00%20Glossary%20DDD.md#microservice) to osobno wdrażana jednostka z własną bazą danych. Bounded context to granica modelu i języka. Często się pokrywają, ale nie są tym samym. Kilka kontekstów może też żyć w jednym wdrożeniu jako moduły, co nazywa się <a id="term-modular-monolith"></a>[modularnym monolitem](00%20Glossary%20DDD.md#modular-monolith):

| Relacja | Kiedy |
|---|---|
| 1 kontekst : 1 serwis | typowa i dobra relacja w systemie mikroserwisowym |
| 1 kontekst : wiele serwisów | kontekst ma części o różnych wymaganiach wdrożeniowych, np. API i worker obliczeń cenowych |
| wiele kontekstów : 1 wdrożenie | modularny monolit z kontekstami jako modułami |
| 1 serwis obejmujący kawałki wielu kontekstów | objaw problemu: serwis bez spójnego modelu |

```text
jednostka wdrożenia    ⊇  serwis   ⊇  bounded context   ⊇  moduł   ⊇  agregat
(kontener, proces)                    (model, język)
```

Mikroserwis nie może być mniejszy niż agregat, bo agregat jest granicą transakcji. Nie powinien też być mniejszy niż kontekst, jeśli wymaga to rozbijania jednego modelu na serwisy, które muszą się ciągle synchronizować. Częsty błąd to serwis per encja (`CustomerService`, `VehicleService`, `ReservationService`), który daje rozproszony monolit z transakcjami rozłożonymi na sieć.

Modularny monolit z kontekstami jako modułami to dobry punkt startu. Granice kontekstów pilnuje się w nim testami architektury, a wydzielenie modułu do serwisu jest później decyzją wdrożeniową, a nie przeprojektowaniem modelu. Rozdział 10 wraca do tej decyzji.

## Ten sam obiekt w wielu kontekstach

Samochód w wypożyczalni istnieje w kilku kontekstach, za każdym razem w innej postaci:

```python
# Fleet: fizyczny pojazd, jego stan i historia
@dataclass
class Vehicle:
    vin: str
    registration: str
    model: str
    mileage: int
    service_due_at: int
    status: VehicleStatus                 # AVAILABLE, IN_SERVICE, RENTED, RETIRED


# Reservations: rezerwuje się klasę, a nie konkretne auto
@dataclass(frozen=True)
class VehicleClass:
    code: str                             # „C”, „SUV”, „VAN”
    seats: int
    transmission: str


# Rental: konkretne auto przypisane do umowy, stan przy wydaniu i zwrocie
@dataclass(frozen=True)
class RentedVehicle:
    vin: str
    registration: str
    fuel_at_pickup: FuelLevel
    mileage_at_pickup: int
```

Identyfikacja między kontekstami odbywa się przez wspólny identyfikator, a nie przez wspólną klasę. VIN łączy `Vehicle` we flocie z `RentedVehicle` w umowie. Każdy kontekst przechowuje tylko to, czego potrzebuje, i aktualizuje swoje dane przez zdarzenia z kontekstu, który jest ich właścicielem (`VehicleRetired` z floty usuwa auto z dostępności w rezerwacjach).

Kilka zasad:

- identyfikator nadaje kontekst będący właścicielem obiektu, a inne go tylko przechowują,
- identyfikatory powinny być stabilne i niezależne od technologii (VIN, UUID), a nie autoinkrementowane klucze bazy,
- kopia danych w innym kontekście jest świadomą decyzją: jest nieaktualna przez chwilę, ale kontekst działa, gdy właściciel jest niedostępny.

## Przesuwanie granic

Granice kontekstów wyznacza się na podstawie ówczesnej wiedzy, a ta się zmienia. Objawy źle wyznaczonych granic:

- większość funkcji wymaga zmian w dwóch kontekstach i wspólnego wdrożenia,
- dwa konteksty wymieniają ogromną liczbę zdarzeń albo zapytań synchronicznych,
- jeden kontekst odpytuje drugi o dane przy każdej operacji,
- zespoły ciągle negocjują zmiany kontraktów,
- w jednym kontekście pojawiają się dwa języki, bo trafiły do niego pojęcia z dwóch działów.

Przesuwanie granic w działającym systemie robi się stopniowo:

1. Nazwij problem na mapie kontekstów (rozdział 05) i uzgodnij docelowe granice z zespołami.
2. W kontekście docelowym zbuduj nowy model i nowe API obok starego.
3. Przełączaj konsumentów po kolei, a przez okres przejściowy utrzymuj oba kontrakty.
4. Przenieś dane: jednorazowa migracja plus synchronizacja zdarzeniami, aż stary kontekst przestanie być źródłem prawdy.
5. Usuń stary kod i dane.

To ten sam wzorzec strangler fig, który opisuje rozdział 11 przy migracji z legacy. Przesunięcie granicy to operacja na miesiące, więc warto jej unikać przez dobre wstępne rozpoznanie. Nie należy jednak utrzymywać złych granic tylko dlatego, że kiedyś je wyznaczono.

## Co zapamiętać

- Bounded context to granica jednego modelu i języka, z wymiarem językowym, modelowym, technicznym i organizacyjnym.
- Jeden model dla całej firmy nie działa, bo działy myślą różnie, a wspólny model blokuje zmiany.
- Granice wyznacza się heurystykami: język, eksperci, proces, zmiany, dane, zespoły, zdarzenia przełomowe.
- Rozmiar ocenia się po objawach. Lepiej zacząć od większych kontekstów i dzielić je.
- Kontekst i mikroserwis często się pokrywają, ale nie są tym samym. Serwis per encja to błąd.
- Ten sam obiekt ma w różnych kontekstach różne modele połączone stabilnym identyfikatorem.
- Złe granice przesuwa się stopniowo, jak przy migracji strangler fig.

## Pytania sprawdzające

### 14. Czym jest bounded context i dlaczego jeden model dla całej firmy się nie sprawdza?

<details>
<summary>Odpowiedź</summary>

To jawna granica, w której obowiązuje jeden model i jeden język, a każde pojęcie ma jedno znaczenie. Ma wymiar językowy, modelowy, techniczny i organizacyjny. Jeden model korporacyjny zawodzi, bo działy potrzebują różnych atrybutów i reguł, więc wspólne klasy puchną. Reguły jednego działu blokują inne, zmiany wymagają zgody wszystkich, a organizacja naprawdę myśli różnymi językami. DDD zamiast walczyć o jeden model wyznacza granice i jawne tłumaczenie między nimi.

Zobacz: sekcja „Granica jednego modelu”.

</details>

### 15. Jakie heurystyki pomagają wyznaczyć granice kontekstów (język, przepływ, zmiany, zespoły, pivotal events)?

<details>
<summary>Odpowiedź</summary>

Język (gdzie słowo zmienia znaczenie), eksperci (kto zna daną część), proces biznesowy (gdzie kończy się etap), zmiany (co zmienia się razem), dane (kto jest właścicielem i zarządza cyklem życia), zespoły (kto rozwija) oraz zdarzenia przełomowe z Event Stormingu, po których proces przechodzi w inną fazę, np. `VehicleHandedOver`, `VehicleReturned`. Heurystyki stosuje się razem, bo nie ma algorytmu.

Zobacz: sekcja „Jak wyznaczyć granice”.

</details>

### 16. Jak duży powinien być bounded context? Jakie są objawy kontekstu za dużego i za małego?

<details>
<summary>Odpowiedź</summary>

Nie ma miary w liczbie klas. Ocenia się po objawach. Za duży: słowa z wieloma znaczeniami, klasy z polami dla części kodu, zespoły wchodzące sobie w drogę, zmiany wymagające testowania niezwiązanych części. Za mały: prosty proces wymaga kilku kontekstów, zmiany dotykają kilku kontekstów naraz, dużo współdzielonych danych i zapytań, potrzeba transakcji między kontekstami. Lepiej zacząć od większych kontekstów i dzielić je, bo łączenie jest trudniejsze.

Zobacz: sekcja „Rozmiar kontekstu”.

</details>

### 17. Czy bounded context to mikroserwis? Jak się mają do siebie kontekst, moduł, serwis i jednostka wdrożenia?

<details>
<summary>Odpowiedź</summary>

Nie zawsze. Kontekst to granica modelu i języka, a mikroserwis to osobno wdrażana jednostka z własną bazą. Typowo 1 kontekst to 1 serwis, ale kontekst może mieć kilka serwisów (API i worker), a kilka kontekstów może żyć w jednym wdrożeniu jako moduły modularnego monolitu. Serwis nie powinien być mniejszy niż agregat. Serwis per encja albo serwis z kawałkami wielu kontekstów to błąd prowadzący do rozproszonego monolitu. Dobry start to modularny monolit.

Zobacz: sekcja „Kontekst a jednostka wdrożenia”.

</details>

### 18. Jak ten sam obiekt biznesowy (np. „produkt”) wygląda w różnych kontekstach i jak identyfikować go między nimi?

<details>
<summary>Odpowiedź</summary>

W każdym kontekście ma inny model z innymi atrybutami: we flocie pojazd z przebiegiem i serwisem, w rezerwacjach klasa auta, a w umowie najmu konkretne auto ze stanem przy wydaniu. Łączy je stabilny identyfikator (VIN, UUID) nadany przez kontekst będący właścicielem, a nie wspólna klasa. Inne konteksty przechowują tylko potrzebne dane i aktualizują je zdarzeniami właściciela, świadomie akceptując chwilową nieaktualność.

Zobacz: sekcja „Ten sam obiekt w wielu kontekstach”.

</details>

### 19. Jak rozpoznać, że granice kontekstów są źle wyznaczone, i jak je przesunąć w działającym systemie?

<details>
<summary>Odpowiedź</summary>

Objawy to zmiany i wdrożenia prawie zawsze w dwóch kontekstach naraz, ogromna liczba zdarzeń lub zapytań między nimi, odpytywanie innego kontekstu przy każdej operacji, ciągłe negocjacje kontraktów i dwa języki w jednym kontekście. Przesunięcie robi się stopniowo: uzgodnienie docelowych granic, nowy model i API obok starego, przełączanie konsumentów z okresem przejściowym, migracja danych z synchronizacją, na końcu usunięcie starego kodu. To strangler fig i praca na miesiące.

Zobacz: sekcja „Przesuwanie granic”.

</details>
