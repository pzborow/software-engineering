# Projektowanie agregatów

<a id="term-aggregate"></a>[Agregat](00%20Glossary%20DDD.md#aggregate) to wzorzec taktyczny, który najczęściej projektuje się źle. Za duży powoduje konflikty współbieżności i wolne ładowanie. Za mały nie chroni reguł biznesowych. Zbyt powiązany z innymi agregatami wymusza transakcje obejmujące pół systemu. Ten rozdział opisuje zasady, które pomagają znaleźć właściwy rozmiar, i techniki na reguły obejmujące wiele agregatów.

```text
┌──────────── agregat RentalAgreement ────────────┐
│  RentalAgreement (korzeń)                       │   ← jedyny punkt wejścia
│   ├── period: RentalPeriod          (VO)        │
│   ├── driver: Driver                (encja)     │
│   ├── extensions: [Extension]       (encje)     │
│   └── return_protocol: ReturnProtocol | None    │
│                                                 │
│  reservation_id ──► Reservation   (tylko ID)    │   ← inne agregaty przez identyfikator
│  vin            ──► Vehicle       (tylko ID)    │
└─────────────────────────────────────────────────┘
          jedna transakcja = jeden agregat
```

## Granica spójności

Agregat to grupa powiązanych obiektów (encji i value objectów) traktowana jako jedna całość przy zmianach danych. Każdy agregat ma <a id="term-aggregate-root"></a>[korzeń](00%20Glossary%20DDD.md#aggregate-root), czyli encję, która jest jedynym punktem wejścia. Kod spoza agregatu może trzymać referencję tylko do korzenia, a wszystkie zmiany przechodzą przez jego metody.

Po co ta granica? Agregat chroni <a id="term-invariant"></a>[niezmienniki](00%20Glossary%20DDD.md#invariant), czyli reguły, które muszą być prawdziwe po każdej operacji. Dla umowy najmu:

- łączna liczba przedłużeń nie przekracza trzech,
- nie można przedłużyć umowy po zwrocie auta,
- data zwrotu po przedłużeniu nie może być wcześniejsza niż obecna,
- kaucja nie może być zwolniona, dopóki protokół zwrotu nie jest zamknięty.

Żeby niezmienniki były zawsze prawdziwe, agregat musi być zmieniany w całości w jednej transakcji. Dlatego agregat jest granicą spójności transakcyjnej: wszystko w środku jest spójne natychmiast, a wszystko na zewnątrz może być spójne ostatecznie.

```python
class RentalAgreement:
    MAX_EXTENSIONS = 3

    def extend(self, new_end: datetime, availability: VehicleAvailability) -> None:
        if self.return_protocol is not None:
            raise RentalError("Nie można przedłużyć zwróconego najmu")
        if len(self.extensions) >= self.MAX_EXTENSIONS:
            raise RentalError("Przekroczono limit przedłużeń")
        if new_end <= self.period.end:
            raise RentalError("Nowa data zwrotu musi być późniejsza")
        if not availability.is_free(self.vin, RentalPeriod(self.period.end, new_end)):
            raise RentalError("Auto jest zarezerwowane w nowym terminie")
        self.extensions.append(Extension(previous_end=self.period.end, new_end=new_end))
        self.period = self.period.extended_to(new_end)
        self._record(RentalExtended(self.id, new_end))
```

Nie da się dodać przedłużenia z pominięciem korzenia (`agreement.extensions.append(...)` z zewnątrz), bo wtedy nikt nie sprawdziłby limitu.

## Cztery reguły Vernona

Vaughn Vernon w serii artykułów „Effective Aggregate Design” (2011) i w książce „Implementing Domain-Driven Design” sformułował cztery reguły, które stały się standardem.

1. Modeluj prawdziwe niezmienniki w granicach spójności. Do agregatu należy tylko to, co musi być natychmiast spójne z powodu reguły biznesowej. Samo to, że obiekty są „powiązane” albo „wyświetlane razem”, nie wystarcza.
2. Projektuj małe agregaty. Mały agregat szybko się ładuje, rzadko wchodzi w konflikt współbieżności i łatwo go zrozumieć. Wiele agregatów to korzeń i kilka value objectów.
3. Odwołuj się do innych agregatów przez identyfikator. Umowa trzyma `vin: Vin`, a nie `vehicle: Vehicle`. Dzięki temu nie da się przypadkiem zmienić dwóch agregatów w jednej transakcji, a agregaty mogą żyć w różnych bazach i serwisach.
4. Poza granicą agregatu używaj spójności ostatecznej. Jeśli zmiana jednego agregatu ma wpłynąć na inny, publikuje się zdarzenie, a drugi agregat reaguje w osobnej transakcji.

```python
# źle: referencje obiektowe, jedna transakcja zmienia trzy agregaty
agreement.vehicle.status = VehicleStatus.RENTED
agreement.reservation.status = ReservationStatus.FULFILLED

# dobrze: identyfikatory i zdarzenia
agreement = RentalAgreement.from_reservation(reservation, vehicle_snapshot, driver, now)
# zdarzenie AgreementSigned → Fleet oznacza auto jako wynajęte
#                            → Reservations oznacza rezerwację jako zrealizowaną
```

<a id="term-eventual-consistency"></a>[Spójność ostateczna](00%20Glossary%20DDD.md#eventual-consistency) oznacza, że inne agregaty zobaczą skutek zmiany z opóźnieniem. Vernon proponuje prosty test: zapytaj eksperta, czy biznes zaakceptuje, że status auta zmieni się kilka sekund po podpisaniu umowy. Zwykle odpowiedź brzmi „tak”, bo w świecie przed komputerami te informacje i tak przepływały z opóźnieniem.

## Za duży agregat

Najczęstszy błąd to agregat zbudowany według struktury danych albo UI: „auto ze wszystkimi rezerwacjami”, „klient ze wszystkimi umowami”, „oddział ze wszystkimi autami”.

```python
# za duży: Vehicle z całą historią i przyszłością
class Vehicle:
    vin: str
    reservations: list[Reservation]         # setki, rosną z czasem
    agreements: list[RentalAgreement]       # cała historia
    service_records: list[ServiceRecord]
    damages: list[Damage]
```

Objawy:

- konflikty współbieżności: dwóch pracowników rezerwuje różne terminy tego samego auta i jeden dostaje błąd, choć terminy się nie pokrywają,
- wolne ładowanie: żeby dodać wpis serwisowy, trzeba wczytać setki rezerwacji,
- blokady w bazie przy każdej zmianie,
- w metodach agregatu większość kodu nie dotyczy żadnego niezmiennika, tylko przenosi dane.

Podział zaczyna się od pytania: które reguły naprawdę wymagają natychmiastowej spójności między tymi obiektami? Dla `Vehicle` okazuje się, że:

- rezerwacje nie mogą się nakładać, ale to reguła dotycząca dostępności w czasie, a nie auta jako całości,
- historia umów nie ma niezmiennika wspólnego z serwisem,
- szkody są rozpatrywane osobno i mają własny cykl życia.

Wynik to kilka małych agregatów: `Vehicle` (dane pojazdu i status), `RentalAgreement`, `ServiceRecord`, `DamageClaim`, a dostępnością zajmuje się osobny agregat opisany w następnej sekcji.

## Reguła ponad agregatami

Niektóre reguły dotyczą wielu agregatów naraz: „e-mail klienta jest unikalny”, „klient może mieć najwyżej dwa aktywne najmy”, „w oddziale nie można zarezerwować więcej aut klasy SUV, niż jest dostępnych”. Jedna transakcja na wszystkich agregatach łamie czwartą regułę Vernona i zasadę „jedna transakcja, jeden agregat”. Są cztery techniki.

Pierwsza technika to agregat wokół reguły. Jeśli reguła jest ważna, zasługuje na własny agregat, którego jedynym zadaniem jest jej pilnowanie. Przepełnienie oddziału chroni agregat dostępności per oddział, klasa i dzień:

```python
class ClassCapacity:                                       # agregat: oddział × klasa × dzień
    def __init__(self, branch: BranchId, vehicle_class: VehicleClassCode, day: date,
                 fleet_size: int, reserved: int, version: int):
        ...

    def reserve(self, reservation_id: ReservationId) -> None:
        if self.reserved >= self.fleet_size:
            raise NoCapacity(self.branch, self.vehicle_class, self.day)
        self.reserved += 1
        self._record(CapacityReserved(self.branch, self.vehicle_class, self.day, reservation_id))
```

Agregat jest mały, więc konflikty dotyczą tylko rezerwacji tej samej klasy w tym samym oddziale i dniu, a nie całego auta.

Druga technika to ograniczenie w bazie jako część implementacji repozytorium. Unikalność e-maila najprościej wymusić indeksem `UNIQUE`, a naruszenie zamienić na wyjątek domenowy. To pragmatyczne i poprawne, jeśli regułę dokumentuje test kontraktowy repozytorium.

Trzecia technika to wzorzec rezerwacji: najpierw zarezerwuj zasób w osobnym agregacie (np. `EmailClaim`), potem utwórz właściwy agregat, a po niepowodzeniu zwolnij rezerwację. Przydaje się, gdy agregaty żyją w różnych bazach.

Czwarta technika to wykrywanie i kompensacja. Jeśli naruszenie jest rzadkie i nieszkodliwe, można je dopuścić, wykryć po fakcie (zdarzenie, raport) i naprawić procesem biznesowym. Wypożyczalnie robią tak z overbookingiem od dziesięcioleci: gdy auta brakuje, klient dostaje wyższą klasę.

| Technika | Siła gwarancji | Koszt | Kiedy |
|---|---|---|---|
| agregat wokół reguły | pełna | nowy agregat, więcej konfliktów w jego obrębie | reguła ważna, mieści się w jednej bazie |
| ograniczenie bazy | pełna | wiedza w schemacie | unikalność, prosta reguła |
| wzorzec rezerwacji | pełna, z kompensacją | dodatkowe kroki i sprzątanie | różne bazy lub serwisy |
| wykrywanie i kompensacja | ostateczna | proces naprawczy | naruszenia rzadkie i tanie do naprawy |

Wybór to decyzja biznesowa: ile kosztuje naruszenie reguły, a ile kosztuje pełna gwarancja.

## Jedna transakcja, jeden agregat

Zasada „jedna transakcja zmienia jeden agregat” wynika bezpośrednio z granicy spójności. Jeśli transakcja zmienia dwa agregaty, to albo są one w rzeczywistości jednym agregatem, albo zespół próbuje uzyskać natychmiastową spójność tam, gdzie wystarczy ostateczna.

Konsekwencje przestrzegania zasady:

- agregaty można trzymać w różnych bazach i serwisach bez przeprojektowania,
- konflikty współbieżności dotyczą tylko jednego agregatu naraz,
- procesy obejmujące wiele agregatów stają się jawne: zdarzenie, polityka, kolejna komenda,
- testy agregatu nie wymagają innych agregatów.

Vernon wymienia sytuacje, w których można świadomie złamać zasadę:

- wygoda interfejsu użytkownika: tworzenie kilku agregatów tego samego typu naraz, np. import listy aut, gdy nie ma między nimi niezmienników,
- brak infrastruktury do spójności ostatecznej (brak brokera, brak outboxa) w małym systemie,
- globalne transakcje wymagane przez technologię lub regulacje,
- wydajność, gdy zmierzony koszt osobnych transakcji jest nieakceptowalny.

W każdym z tych przypadków decyzję warto zapisać, na przykład w ADR, bo przy przejściu na osobne bazy lub serwisy trzeba będzie do niej wrócić.

## Długie listy w agregacie

Czasem naturalny agregat ma kolekcję, która rośnie bez końca: zamówienie flotowe na tysiąc aut, konto rozliczeniowe firmy z historią transakcji, auto z historią przebiegów. Ładowanie całej kolekcji przy każdej zmianie jest nie do przyjęcia.

Techniki:

- wyciągnij elementy do osobnych agregatów, jeśli niezmienniki ich nie łączą. Pozycja zamówienia flotowego może być osobnym agregatem z referencją do zamówienia, a korzeń trzyma tylko liczniki potrzebne do niezmienników (np. łączna liczba aut i limit kredytowy),
- trzymaj w agregacie tylko to, czego potrzebują niezmienniki. Konto rozliczeniowe potrzebuje salda i limitu, a nie wszystkich transakcji. Transakcje to osobne zdarzenia albo osobny model odczytu,
- dziel w czasie: zamiast jednego konta na całe życie, agregat per okres rozliczeniowy (`BillingPeriod`), który zamyka się i przenosi saldo do następnego,
- nie ukrywaj problemu lazy loadingiem ORM-a. Pozornie działa, ale każda metoda agregatu może wtedy nieoczekiwanie wczytać tysiące wierszy, a niezmienniki liczone na częściowo wczytanej kolekcji są błędne.

```python
class FleetOrder:                                          # korzeń bez listy pozycji
    def __init__(self, id: FleetOrderId, credit_limit: Money, committed: Money, line_count: int): ...

    def add_line(self, line_id: FleetOrderLineId, price: Money) -> None:
        if self.committed + price > self.credit_limit:
            raise CreditLimitExceeded(self.id)
        self.committed = self.committed + price
        self.line_count += 1
        self._record(FleetOrderLineAdded(self.id, line_id, price))
        # pozycja FleetOrderLine to osobny agregat, tworzony w reakcji na zdarzenie
```

## Co zapamiętać

- Agregat to granica spójności transakcyjnej z jednym korzeniem, przez który przechodzą wszystkie zmiany.
- Do agregatu należy tylko to, co wymaga natychmiastowej spójności z powodu prawdziwego niezmiennika.
- Reguły Vernona: prawdziwe niezmienniki, małe agregaty, referencje przez ID, spójność ostateczna poza granicą.
- Za duży agregat widać po konfliktach współbieżności, wolnym ładowaniu i kodzie niezwiązanym z niezmiennikami.
- Reguły między agregatami wymusza się agregatem wokół reguły, ograniczeniem bazy, wzorcem rezerwacji albo wykrywaniem i kompensacją.
- Jedna transakcja zmienia jeden agregat. Wyjątki są świadome i udokumentowane.
- Długie listy wyciąga się do osobnych agregatów, redukuje do potrzeb niezmienników albo dzieli w czasie. Lazy loading niczego nie rozwiązuje.

## Pytania sprawdzające

### 35. Czym jest agregat i jego korzeń? Dlaczego agregat jest granicą spójności transakcyjnej?

<details>
<summary>Odpowiedź</summary>

Agregat to grupa encji i value objectów traktowana jako całość przy zmianach. Korzeń to encja będąca jedynym punktem wejścia: z zewnątrz trzyma się referencję tylko do niego, a wszystkie zmiany przechodzą przez jego metody. Agregat chroni niezmienniki, które muszą być prawdziwe po każdej operacji, więc musi być zmieniany w całości w jednej transakcji. Wewnątrz spójność jest natychmiastowa, a na zewnątrz ostateczna.

Zobacz: sekcja „Granica spójności”.

</details>

### 36. Jakie są reguły projektowania agregatów według Vaughna Vernona (prawdziwe niezmienniki, małe agregaty, referencje przez ID, spójność ostateczna poza granicą)?

<details>
<summary>Odpowiedź</summary>

Pierwsza: modeluj w granicy tylko prawdziwe niezmienniki, a nie powiązania czy to, co wyświetla się razem. Druga: projektuj małe agregaty, bo szybko się ładują i rzadko wchodzą w konflikty. Trzecia: odwołuj się do innych agregatów przez ID, co uniemożliwia zmianę kilku w jednej transakcji i pozwala trzymać je w różnych bazach. Czwarta: poza granicą używaj spójności ostatecznej przez zdarzenia. Test: czy biznes zaakceptuje opóźnienie, co zwykle jest prawdą.

Zobacz: sekcja „Cztery reguły Vernona”.

</details>

### 37. Jak rozpoznać, że agregat jest za duży (konflikty współbieżności, wydajność ładowania), i jak go podzielić?

<details>
<summary>Odpowiedź</summary>

Objawy to konflikty współbieżności przy niezależnych zmianach (dwie rezerwacje różnych terminów tego samego auta), wolne ładowanie niepotrzebnych kolekcji, blokady w bazie i metody, które nie dotyczą żadnego niezmiennika. Zwykle powstaje z modelowania według danych lub UI. Dzieli się go, pytając, które reguły naprawdę wymagają natychmiastowej spójności: `Vehicle` z rezerwacjami, umowami, serwisem i szkodami rozpada się na kilka małych agregatów i osobny agregat dostępności.

Zobacz: sekcja „Za duży agregat”.

</details>

### 38. Jak egzekwować regułę obejmującą wiele agregatów (np. unikalność e-maila, limit na klienta) bez jednej transakcji?

<details>
<summary>Odpowiedź</summary>

Są cztery techniki. Agregat wokół reguły, np. `ClassCapacity` per oddział, klasa i dzień. Ograniczenie w bazie jako część implementacji repozytorium, np. `UNIQUE` dla e-maila zamieniony na wyjątek domenowy i opisany testem kontraktowym. Wzorzec rezerwacji, czyli najpierw rezerwacja zasobu, potem utworzenie agregatu, przy błędzie zwolnienie. Wykrywanie i kompensacja przy rzadkich, tanich naruszeniach, jak overbooking z upgrade'em klasy. Wybór zależy od kosztu naruszenia wobec kosztu gwarancji i jest decyzją biznesową.

Zobacz: sekcja „Reguła ponad agregatami”.

</details>

### 39. Dlaczego jedna transakcja powinna zmieniać jeden agregat i kiedy można świadomie złamać tę zasadę?

<details>
<summary>Odpowiedź</summary>

Bo agregat jest granicą spójności. Zmiana dwóch w jednej transakcji oznacza, że są w rzeczywistości jednym agregatem albo wymusza się niepotrzebną natychmiastową spójność. Przestrzeganie zasady pozwala trzymać agregaty w różnych bazach, ogranicza konflikty i czyni procesy jawnymi. Świadome wyjątki według Vernona to wygoda UI przy tworzeniu wielu agregatów bez wspólnych niezmienników, brak infrastruktury do spójności ostatecznej, wymogi technologii lub regulacji oraz zmierzona wydajność. Decyzję warto zapisać w ADR.

Zobacz: sekcja „Jedna transakcja, jeden agregat”.

</details>

### 40. Jak modelować agregaty z długą listą elementów (np. zamówienie z tysiącem pozycji, konto z historią operacji)?

<details>
<summary>Odpowiedź</summary>

Wyciągnąć elementy do osobnych agregatów, jeśli niezmienniki ich nie łączą, a w korzeniu trzymać tylko liczniki i sumy potrzebne do reguł (np. limit kredytowy i suma zamówienia). Trzymać w agregacie tylko to, czego potrzebują niezmienniki (saldo zamiast historii transakcji, z historią jako zdarzeniami lub modelem odczytu). Dzielić w czasie, np. agregat per okres rozliczeniowy. Nie polegać na lazy loadingu ORM, bo ukrywa koszt i prowadzi do niezmienników liczonych na częściowych danych.

Zobacz: sekcja „Długie listy w agregacie”.

</details>
