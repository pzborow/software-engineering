# Cztery kręgi

Diagram Martina ma cztery kręgi. Każdy zawiera inny rodzaj kodu i może zależeć tylko od kręgów leżących bliżej środka. Ten rozdział przechodzi przez nie od środka na zewnątrz na przykładzie rezerwacji sal.

```text
krąg          przykładowe klasy                              rodzaj reguł
────────────  ─────────────────────────────────────────────  ───────────────────────
1 (środek)    Room, Reservation, TimeSlot                    reguły przedsiębiorstwa
2             ReserveRoomInteractor, ReservationGateway      reguły aplikacji
3             ReservationController, ReservationPresenter    tłumaczenie formatów
4 (zewnątrz)  FastAPI, SQLAlchemy, PostgreSQL                narzędzia i urządzenia
```

## Pierwszy krąg: reguły przedsiębiorstwa

Środkowy krąg nazywa się <a id="term-entities"></a>[Entities](00%20Glossary%20Clean.md#entities). Martin rozumie przez to obiekty z krytycznymi regułami biznesowymi, czyli regułami, które obowiązywałyby także wtedy, gdyby nie było żadnego systemu. Firma nie pozwalała na podwójną rezerwację sali także wtedy, gdy rezerwacje zapisywano w zeszycie w recepcji.

```python
# entities/reservation.py
from dataclasses import dataclass
from datetime import datetime, timedelta


class ReservationError(Exception):
    pass


@dataclass(frozen=True)
class TimeSlot:
    start: datetime
    end: datetime

    def __post_init__(self):
        if self.end <= self.start:
            raise ReservationError("Koniec musi być po początku")

    def overlaps(self, other: "TimeSlot") -> bool:
        return self.start < other.end and other.start < self.end


@dataclass
class Reservation:
    id: str
    room_id: str
    organizer_id: str
    slot: TimeSlot
    cancelled: bool = False

    CANCELLATION_NOTICE = timedelta(hours=24)

    def conflicts_with(self, other: "Reservation") -> bool:
        return (not self.cancelled and not other.cancelled
                and self.room_id == other.room_id and self.slot.overlaps(other.slot))

    def cancel(self, now: datetime) -> None:
        if self.slot.start - now < self.CANCELLATION_NOTICE:
            raise ReservationError("Za późno na anulowanie")
        self.cancelled = True
```

Encja w rozumieniu Martina nie musi być klasą. Może to być zbiór funkcji i struktur danych. Ważne jest, że zawiera najbardziej ogólne i najstabilniejsze reguły, których nie zmieni żadna zmiana w UI, bazie czy sposobie wdrożenia. W systemie z wieloma aplikacjami Entities mogą być współdzielone przez wszystkie.

## Drugi krąg: reguły aplikacji

Krąg <a id="term-use-cases"></a>[Use Cases](00%20Glossary%20Clean.md#use-cases) zawiera reguły specyficzne dla tej konkretnej aplikacji. Opisują, jak system automatyzuje pracę: w jakiej kolejności pobrać dane, kiedy wywołać encje, co zapisać.

Pojedynczy przypadek użycia realizuje <a id="term-interactor"></a>[interactor](00%20Glossary%20Clean.md#interactor). Przyjmuje dane wejściowe, wywołuje reguły encji i przygotowuje wynik:

```python
# use_cases/reserve_room.py
from dataclasses import dataclass
from datetime import datetime, timedelta
from uuid import uuid4

from rooms.entities.reservation import Reservation, ReservationError, TimeSlot
from rooms.use_cases.gateways import Clock, ReservationGateway


@dataclass(frozen=True)
class ReserveRoomRequest:
    room_id: str
    organizer_id: str
    start: datetime
    end: datetime


class ReserveRoomInteractor:
    MAX_DAYS_AHEAD = 14                     # reguła aplikacji, nie przedsiębiorstwa

    def __init__(self, reservations: ReservationGateway, clock: Clock):
        self._reservations = reservations
        self._clock = clock

    def execute(self, request: ReserveRoomRequest) -> str:
        if request.start - self._clock.now() > timedelta(days=self.MAX_DAYS_AHEAD):
            raise ReservationError("Można rezerwować najwyżej 14 dni do przodu")

        candidate = Reservation(
            id=str(uuid4()),
            room_id=request.room_id,
            organizer_id=request.organizer_id,
            slot=TimeSlot(request.start, request.end),
        )
        for existing in self._reservations.for_room(request.room_id):
            if candidate.conflicts_with(existing):
                raise ReservationError("Sala jest zajęta w tym czasie")

        self._reservations.add(candidate)
        return candidate.id
```

Różnica między regułą przedsiębiorstwa a regułą aplikacji jest tu widoczna. Zakaz nakładania się rezerwacji jest w encji, bo obowiązuje zawsze. Limit 14 dni do przodu jest w interactorze, bo to decyzja tej konkretnej aplikacji. Aplikacja recepcji może mieć inny limit albo żadnego.

Interactor nie wie, skąd przyszło żądanie ani gdzie trafi wynik. Nie zna HTTP, JSON-a ani SQL-a. W rozdziale 03 zobaczysz pełną wersję z interfejsami wejścia i wyjścia oraz presenterem.

## Interfejsy danych w kręgu przypadków użycia

Interactor potrzebuje danych, ale nie może importować bazy. Martin rozwiązuje to przez <a id="term-gateway"></a>[gateway](00%20Glossary%20Clean.md#gateway): polimorficzny interfejs z operacjami na danych, zdefiniowany w kręgu Use Cases i zaimplementowany na zewnątrz.

```python
# use_cases/gateways.py
from datetime import datetime
from typing import Protocol

from rooms.entities.reservation import Reservation


class ReservationGateway(Protocol):
    def for_room(self, room_id: str) -> list[Reservation]: ...
    def get(self, reservation_id: str) -> Reservation: ...
    def add(self, reservation: Reservation) -> None: ...
    def save(self, reservation: Reservation) -> None: ...


class Clock(Protocol):
    def now(self) -> datetime: ...
```

Gateway to w praktyce to samo co repozytorium w DDD. Martin używa słowa „gateway”, bo interfejs może ukrywać nie tylko bazę, ale też dowolne zewnętrzne źródło danych.

## Trzeci krąg: tłumacze formatów

Krąg <a id="term-interface-adapters"></a>[Interface Adapters](00%20Glossary%20Clean.md#interface-adapters) tłumaczy dane z formatu wygodnego dla przypadków użycia na format wygodny dla narzędzi zewnętrznych i z powrotem. Są tu trzy rodzaje klas:

- kontrolery, które zamieniają żądanie z frameworka na strukturę wejściową interactora,
- presentery, które zamieniają wynik interactora na dane gotowe do wyświetlenia,
- implementacje gateway'ów, które zamieniają encje na wiersze bazy i z powrotem.

```python
# interface_adapters/sql_reservation_gateway.py
class SqlReservationGateway:
    def __init__(self, session):
        self._session = session

    def for_room(self, room_id: str) -> list[Reservation]:
        rows = self._session.scalars(select(ReservationRow).where(ReservationRow.room_id == room_id))
        return [self._to_entity(row) for row in rows]

    def add(self, reservation: Reservation) -> None:
        self._session.add(ReservationRow(
            id=reservation.id,
            room_id=reservation.room_id,
            organizer_id=reservation.organizer_id,
            starts_at=reservation.slot.start,
            ends_at=reservation.slot.end,
            cancelled=reservation.cancelled,
        ))

    # get i save wyglądają analogicznie

    @staticmethod
    def _to_entity(row) -> Reservation:
        return Reservation(row.id, row.room_id, row.organizer_id,
                           TimeSlot(row.starts_at, row.ends_at), row.cancelled)
```

W tym kręgu kończy się wiedza o SQL. Kręgi wewnętrzne nie wiedzą, że baza jest relacyjna. Martin mówi wprost: jeśli baza jest SQL-owa, cały SQL powinien być ograniczony do tej warstwy.

## Czwarty krąg: narzędzia

Najbardziej zewnętrzny krąg to <a id="term-frameworks-and-drivers"></a>[Frameworks & Drivers](00%20Glossary%20Clean.md#frameworks-and-drivers): framework webowy, silnik bazy, sterowniki, biblioteki klienckie. Zwykle jest tu niewiele własnego kodu, głównie konfiguracja i „klej”, który łączy narzędzie z kręgiem niżej.

```python
# frameworks/web.py
app = FastAPI()
engine = create_engine(settings.database_url)
SessionLocal = sessionmaker(bind=engine)


@app.post("/reservations", status_code=201)
def reserve(body: dict, controller: ReservationController = Depends(get_controller)):
    return controller.reserve(body)
```

Kodu jest tu mało celowo. Wszystko, co jest w tym kręgu, jest związane z konkretnym narzędziem i przepada przy jego wymianie.

## Kręgi to schemat, nie przepis

Martin pisze wprost, że cztery kręgi są schematem. Aplikacja może mieć ich więcej albo mniej. Stała jest tylko Dependency Rule i to, że im bliżej środka, tym wyższy poziom polityki.

Przykłady odstępstw:

- mała aplikacja łączy Entities i Use Cases w jeden moduł `core`,
- duży system dzieli Interface Adapters na osobne kręgi dla web i dla persystencji,
- system z wieloma aplikacjami ma dodatkowy krąg dla reguł wspólnych kilku aplikacjom.

## Co przechodzi przez granice

Dane przekraczające granicę kręgu powinny być prostymi strukturami: dataclassami, krotkami, słownikami o znanym kształcie. Powinny mieć postać wygodną dla kręgu wewnętrznego.

Przez granicę nie powinny przechodzić:

- encje, bo zewnętrzny krąg zacząłby zależeć od ich struktury i mógłby wywołać metody zmieniające stan,
- wiersze bazy (`ReservationRow`) ani obiekty ORM, bo wtedy wewnętrzny krąg znałby format zewnętrznego,
- obiekty frameworka (`Request`, `QuerySet`), z tego samego powodu.

```text
HTTP JSON ──► dict ──► ReserveRoomRequest (dataclass) ──► interactor ──► Reservation (encja)
Reservation ──► ReservationRow ──► PostgreSQL
```

Strukturę wejściową i wyjściową definiuje krąg wewnętrzny, a tłumaczeniem zajmuje się krąg zewnętrzny. Dzięki temu kierunek zależności nie odwraca się przy przekazywaniu danych.

## Co zapamiętać

- Entities zawierają krytyczne reguły przedsiębiorstwa, które obowiązywałyby także bez systemu.
- Use Cases zawierają reguły tej konkretnej aplikacji i orkiestrują encje.
- Interactor realizuje jeden przypadek użycia i nie zna HTTP, JSON-a ani SQL-a.
- Gateway to interfejs danych zdefiniowany w kręgu Use Cases.
- Interface Adapters tłumaczą formaty: kontrolery, presentery, implementacje gateway'ów.
- Frameworks & Drivers zawierają narzędzia i jak najmniej własnego kodu.
- Liczba kręgów jest umowna, stała jest tylko Dependency Rule.
- Przez granice przechodzą proste struktury danych, a nie encje i wiersze bazy.

## Pytania sprawdzające

### 7. Wymień kręgi Clean Architecture od środka i opisz rolę każdego z nich.

<details>
<summary>Odpowiedź</summary>

Entities to krytyczne reguły przedsiębiorstwa (np. zakaz nakładania się rezerwacji). Use Cases to reguły tej konkretnej aplikacji, realizowane przez interactory. Interface Adapters to tłumacze formatów: kontrolery, presentery i implementacje gateway'ów. Frameworks & Drivers to narzędzia: framework webowy, baza, sterowniki. Każdy krąg może zależeć tylko od kręgów bliższych środka.

Zobacz: tabela na początku rozdziału i sekcje o kolejnych kręgach.

</details>

### 8. Czym są Entities i czym „reguły przedsiębiorstwa” różnią się od reguł aplikacji?

<details>
<summary>Odpowiedź</summary>

Entities to obiekty albo funkcje z krytycznymi regułami biznesowymi, które obowiązywałyby także bez systemu, np. zakaz podwójnej rezerwacji sali. Reguły aplikacji dotyczą sposobu, w jaki konkretna aplikacja automatyzuje pracę, np. limit 14 dni do przodu w aplikacji dla pracowników. Reguły przedsiębiorstwa mogą być współdzielone przez wiele aplikacji, a reguły aplikacji nie.

Zobacz: sekcje „Pierwszy krąg: reguły przedsiębiorstwa” i „Drugi krąg: reguły aplikacji”.

</details>

### 9. Czym są Use Cases (Interactors) i co powinny, a czego nie powinny zawierać?

<details>
<summary>Odpowiedź</summary>

Interactor realizuje jeden przypadek użycia: przyjmuje prostą strukturę wejściową, pobiera dane przez gateway, wywołuje reguły encji, stosuje reguły specyficzne dla aplikacji i zapisuje wynik. Nie powinien znać HTTP, JSON-a, SQL-a, frameworka ani formatu wyświetlania. Nie powinien też powielać reguł przedsiębiorstwa, które należą do encji.

Zobacz: sekcja „Drugi krąg: reguły aplikacji”.

</details>

### 10. Co należy do warstwy Interface Adapters (kontrolery, presentery, gateway'e)?

<details>
<summary>Odpowiedź</summary>

Kod tłumaczący formaty między przypadkami użycia a narzędziami zewnętrznymi. Kontrolery zamieniają żądanie frameworka na strukturę wejściową interactora. Presentery zamieniają wynik interactora na dane do wyświetlenia. Implementacje gateway'ów zamieniają encje na wiersze bazy i z powrotem. Cały SQL powinien być ograniczony do tej warstwy.

Zobacz: sekcja „Trzeci krąg: tłumacze formatów”.

</details>

### 11. Co należy do warstwy Frameworks & Drivers i dlaczego ma być w niej jak najmniej kodu?

<details>
<summary>Odpowiedź</summary>

Framework webowy, silnik bazy, sterowniki i biblioteki klienckie oraz konfiguracja i „klej”, który łączy je z kręgiem Interface Adapters. Kodu ma być mało, bo wszystko w tym kręgu jest związane z konkretnym narzędziem i przepada przy jego wymianie.

Zobacz: sekcja „Czwarty krąg: narzędzia”.

</details>

### 12. Czy kręgów zawsze muszą być cztery? Co mówi o tym Martin?

<details>
<summary>Odpowiedź</summary>

Nie. Martin pisze, że kręgi są schematem i może ich być więcej lub mniej. Stała jest tylko Dependency Rule i to, że poziom polityki rośnie w stronę środka. Mała aplikacja może połączyć Entities i Use Cases w jeden moduł, a duży system może rozbić adaptery na kilka kręgów.

Zobacz: sekcja „Kręgi to schemat, nie przepis”.

</details>

### 13. Jak dane przekraczają granice kręgów i dlaczego nie powinny to być encje ani wiersze bazy?

<details>
<summary>Odpowiedź</summary>

Jako proste struktury danych (dataclassy, krotki) w postaci wygodnej dla kręgu wewnętrznego, który je definiuje. Encje nie powinny wychodzić na zewnątrz, bo zewnętrzny kod zacząłby zależeć od ich struktury i mógłby zmieniać ich stan. Wiersze bazy i obiekty frameworka nie powinny wchodzić do środka, bo wewnętrzny krąg zależałby wtedy od formatu zewnętrznego, co łamie Dependency Rule.

Zobacz: sekcja „Co przechodzi przez granice”.

</details>
