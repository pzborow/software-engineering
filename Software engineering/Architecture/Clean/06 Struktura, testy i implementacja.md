# Struktura, testy i implementacja

Kręgi i boundaries trzeba zamienić na katalogi, reguły importów i testy. Ten rozdział odpowiada na praktyczne pytania: jak ułożyć pakiety, jak pilnować Dependency Rule, jak testować każdy krąg i gdzie umieścić walidację, transakcje i błędy.

```text
decyzja                 opcje
──────────────────────  ───────────────────────────────────────────────
układ pakietów          warstwami · funkcjami · porty i adaptery · komponentami
pilnowanie granic       konwencja · import-linter · osobne paczki
testy                   encje · interactory · presentery · kontrolery · całość
granice techniczne      walidacja · transakcje · błędy
```

## Cztery sposoby układania pakietów

W książce Martina jest rozdział „The Missing Chapter”, który napisał Simon Brown. Porównuje w nim cztery sposoby organizacji kodu na tym samym przykładzie.

<a id="term-package-by-layer"></a>[Package by layer](00%20Glossary%20Clean.md#package-by-layer) dzieli kod według warstw technicznych. Jest prosty na start, ale nic nie mówi o domenie, a przy wzroście projektu każda funkcja jest rozsmarowana po wszystkich katalogach:

```text
rooms/
├── controllers/     reservation_controller.py, room_controller.py
├── services/        reservation_service.py, room_service.py
└── repositories/    reservation_repository.py, room_repository.py
```

<a id="term-package-by-feature"></a>[Package by feature](00%20Glossary%20Clean.md#package-by-feature) dzieli kod według funkcji biznesowej. Struktura krzyczy o domenie, ale w obrębie funkcji nic nie pilnuje granic między warstwami:

```text
rooms/
├── reservations/    controller.py, service.py, repository.py
└── rooms/           controller.py, service.py, repository.py
```

Porty i adaptery dzielą kod na wnętrze (domena) i zewnętrze (web, persystencja). To układ najbliższy diagramowi kręgów:

```text
rooms/
├── domain/          reservations/, rooms/          encje, interactory, interfejsy gateway'ów
└── infrastructure/  web/, persistence/             kontrolery, presentery, implementacje
```

<a id="term-package-by-component"></a>[Package by component](00%20Glossary%20Clean.md#package-by-component) to propozycja Browna. Logika biznesowa i dostęp do danych jednej funkcji są w jednym komponencie za wąskim publicznym interfejsem, a UI jest osobno. W Pythonie publiczny interfejs komponentu to jego `__init__.py`, a wszystko inne jest wewnętrzne:

```text
rooms/
├── web/                          kontrolery, presentery (osobno)
└── reservations/                 komponent
    ├── __init__.py               publiczne API: ReserveRoom, CancelReservation, DTO
    ├── _entities.py              wewnętrzne
    ├── _interactors.py           wewnętrzne
    └── _sql_gateway.py           wewnętrzne
```

| Układ | Czytelność domeny | Pilnowanie granic | Koszt |
|---|---|---|---|
| Package by layer | słaba | słabe, każdy widzi wszystko | najniższy |
| Package by feature | dobra | słabe wewnątrz funkcji | niski |
| Porty i adaptery | średnia | dobre, jeśli pilnowane narzędziem | średni |
| Package by component | dobra | dobre, publiczne API komponentu | średni |

Brown podkreśla, że każdy z tych układów może zostać złamany, jeśli język nie wymusza granic. W Javie pomaga modyfikator dostępu pakietowego. W Pythonie nic nie jest naprawdę prywatne, więc potrzebne jest narzędzie.

## Pilnowanie Dependency Rule

Dependency Rule zapisana tylko w dokumentacji szybko się rozmywa. Trzeba zamienić ją w <a id="term-architecture-test"></a>[test architektury](00%20Glossary%20Clean.md#architecture-test), który pada w CI, gdy ktoś zaimportuje coś z kręgu zewnętrznego:

```toml
# pyproject.toml
[tool.importlinter]
root_package = "rooms"

[[tool.importlinter.contracts]]
name = "Kręgi Clean Architecture"
type = "layers"
layers = [
    "rooms.frameworks",
    "rooms.interface_adapters",
    "rooms.use_cases",
    "rooms.entities",
]

[[tool.importlinter.contracts]]
name = "Środek bez bibliotek technicznych"
type = "forbidden"
source_modules = ["rooms.entities", "rooms.use_cases"]
forbidden_modules = ["fastapi", "sqlalchemy", "django", "requests", "pydantic"]
```

Dla package by component dodaje się kontrakt, który zabrania importowania modułów wewnętrznych innego komponentu:

```toml
[[tool.importlinter.contracts]]
name = "Tylko publiczne API komponentów"
type = "forbidden"
source_modules = ["rooms.web"]
forbidden_modules = ["rooms.reservations._entities", "rooms.reservations._sql_gateway"]
```

Najmocniejszy wariant to osobne paczki z własnym `pyproject.toml`. Paczka `rooms-entities` nie ma w zależnościach FastAPI ani SQLAlchemy, więc zakazany import po prostu się nie powiedzie. W Javie tę samą rolę pełnią moduły Maven lub Gradle i ArchUnit, w .NET osobne projekty i NetArchTest.

## Testy w każdym kręgu

Każdy krąg testuje się inaczej:

| Krąg | Co testujemy | Dublery | Koszt |
|---|---|---|---|
| Entities | reguły przedsiębiorstwa | brak | najniższy |
| Use Cases | scenariusze, reguły aplikacji | fake gateway'ów, zegara, fake presenter | niski |
| Interface Adapters | presenter, kontroler, gateway SQL | presenter i kontroler bez dublerów, gateway z prawdziwą bazą | średni |
| Frameworks & Drivers | czy całość jest złożona poprawnie | brak, prawdziwe wszystko | wysoki |

Test interactora używa fake'owego presentera, który zapamiętuje, co dostał:

```python
class SpyOutput:
    def __init__(self):
        self.calls = []

    def success(self, response): self.calls.append(("success", response))
    def room_taken(self, room_id): self.calls.append(("room_taken", room_id))
    def rejected(self, reason): self.calls.append(("rejected", reason))


def test_overlapping_reservation_is_reported_as_room_taken():
    gateway = InMemoryReservations(existing_reservation("sala-A", "09:00", "10:00"))
    output = SpyOutput()
    interactor = ReserveRoomInteractor(gateway, FixedClock(MONDAY_8AM), output)

    interactor.execute(ReserveRoomRequest("sala-A", "u-1", at("09:30"), at("10:30")))

    assert output.calls == [("room_taken", "sala-A")]
```

Presenter i kontroler testuje się bez żadnej infrastruktury, bo są zwykłymi klasami. Widok, jako Humble Object, nie potrzebuje testów.

## Testy jako część systemu

Martin pisze, że testy są częścią systemu i leżą w najbardziej zewnętrznym kręgu. Zależą od wszystkiego, a nic nie zależy od nich. To niesie ryzyko: jeśli każdy test wywołuje wiele konkretnych klas, zmiana struktury kodu psuje setki testów, choć zachowanie się nie zmieniło. Martin nazywa to problemem kruchych testów (Fragile Tests Problem).

Rozwiązaniem jest <a id="term-test-api"></a>[testowe API](00%20Glossary%20Clean.md#test-api): warstwa, przez którą testy komunikują się z systemem. Testy zależą od tego API, a nie od szczegółów struktury. Refaktoryzacja wnętrza zmienia implementację testowego API, a nie same testy.

```python
# tests/api.py: testowe API
class ReservationSystem:
    def __init__(self, now: datetime):
        self.clock = FixedClock(now)
        self.reservations = InMemoryReservations()

    def reserve(self, room: str, start: str, end: str) -> list:
        output = SpyOutput()
        ReserveRoomInteractor(self.reservations, self.clock, output).execute(
            ReserveRoomRequest(room, "u-1", at(start), at(end)))
        return output.calls


# tests/test_reservations.py
def test_back_to_back_reservations_are_allowed():
    system = ReservationSystem(now=MONDAY_8AM)
    system.reserve("sala-A", "09:00", "10:00")
    assert system.reserve("sala-A", "10:00", "11:00")[0][0] == "success"
```

Testowe API może też mieć uprawnienia, których nie ma produkcja: ustawiać stan bazy, podmieniać zegar, pomijać autoryzację. Nie powinno jednak trafiać do kodu produkcyjnego.

## Walidacja, transakcje i błędy

Walidacja ma trzy poziomy, jak w innych architekturach:

- format sprawdza krąg zewnętrzny, na przykład Pydantic w kontrolerze,
- reguły aplikacji sprawdza interactor, na przykład limit 14 dni do przodu,
- <a id="term-invariant"></a>[niezmienniki](00%20Glossary%20Clean.md#invariant) pilnują encje, na przykład `TimeSlot` nie pozwala, żeby koniec był przed początkiem.

Transakcję wyznacza interactor, ale nie może importować sesji bazy. Służy do tego <a id="term-unit-of-work"></a>[Unit of Work](00%20Glossary%20Clean.md#unit-of-work): interfejs zdefiniowany w kręgu Use Cases obok gateway'ów, a zaimplementowany w Interface Adapters.

```python
class UnitOfWork(Protocol):
    reservations: ReservationGateway

    def __enter__(self) -> "UnitOfWork": ...
    def __exit__(self, *exc) -> None: ...
    def commit(self) -> None: ...


class CancelReservationInteractor:
    def execute(self, request: CancelReservationRequest) -> None:
        with self._uow as uow:
            reservation = uow.reservations.get(request.reservation_id)
            try:
                reservation.cancel(self._clock.now())
            except ReservationError as e:
                return self._output.rejected(str(e))
            uow.reservations.save(reservation)
            uow.commit()
        self._output.success(CancelReservationResponse(reservation.id))
```

Błędy w wariancie z presenterem to osobne metody Output Boundary (`room_taken`, `rejected`). Presenter zamienia je na kody statusu. W wariancie, w którym interactor zwraca Response Model, błędy są wyjątkami zdefiniowanymi w Use Cases albo Entities, a kontroler lub handler w kręgu zewnętrznym mapuje je na kody HTTP. W obu przypadkach wyjątki bibliotek, na przykład `IntegrityError` z SQLAlchemy, są tłumaczone w implementacji gateway'a i nie trafiają do środka.

## Co zapamiętać

- Brown opisuje cztery układy: package by layer, by feature, porty i adaptery oraz by component.
- Package by component ukrywa szczegóły funkcji za publicznym API komponentu.
- W Pythonie żaden układ nie pilnuje granic sam, potrzebny jest `import-linter` albo osobne paczki.
- Interactory testuje się z fake'ami gateway'ów i presenterem-szpiegiem, a widok nie potrzebuje testów.
- Testy leżą w zewnętrznym kręgu. Testowe API chroni je przed kruchością przy refaktoryzacji.
- Walidacja ma trzy poziomy, transakcję wyznacza interactor przez Unit of Work, a błędy technologii tłumaczy gateway.

## Pytania sprawdzające

### 32. Jak zorganizować projekt Clean Architecture w Pythonie: package by layer, package by feature czy package by component?

<details>
<summary>Odpowiedź</summary>

Package by layer jest najprostszy, ale nie mówi nic o domenie i rozsmarowuje funkcje po katalogach. Package by feature pokazuje domenę, ale nie pilnuje granic wewnątrz funkcji. Porty i adaptery są najbliższe diagramowi kręgów. Package by component (Simon Brown) zamyka logikę i dostęp do danych funkcji w komponencie z publicznym API (w Pythonie `__init__.py`), a UI trzyma osobno. W Pythonie każdy układ wymaga narzędzia do pilnowania granic, więc wybór zależy od rozmiaru projektu. Package by component albo porty i adaptery z `import-linter` to rozsądne domyślne wybory.

Zobacz: sekcja „Cztery sposoby układania pakietów”.

</details>

### 33. Jak wymusić Dependency Rule w kodzie (import-linter, osobne paczki, ArchUnit)?

<details>
<summary>Odpowiedź</summary>

Zamienić regułę w test architektury uruchamiany w CI. W Pythonie `import-linter` z kontraktem `layers` (frameworks → interface_adapters → use_cases → entities) i `forbidden` (środek bez `fastapi`, `sqlalchemy`, `pydantic`), a dla komponentów dodatkowo zakaz importu modułów wewnętrznych. Najmocniejsze są osobne paczki bez technicznych zależności. W Javie to ArchUnit i moduły Maven lub Gradle, w .NET NetArchTest i osobne projekty.

Zobacz: sekcja „Pilnowanie Dependency Rule”.

</details>

### 34. Jak testować interactory, presentery i kontrolery? Czym jest „testowe API” u Martina?

<details>
<summary>Odpowiedź</summary>

Interactory testuje się z fake'ami gateway'ów i zegara oraz z presenterem-szpiegiem, który zapamiętuje wywołania Output Boundary. Presentery i kontrolery to zwykłe klasy, testowane bez infrastruktury, a widok jako Humble Object nie wymaga testów. Testowe API to warstwa, przez którą testy komunikują się z systemem. Testy zależą od niej, a nie od szczegółów struktury, więc refaktoryzacja wnętrza nie psuje setek testów (Fragile Tests Problem). Może mieć dodatkowe uprawnienia, np. podmianę zegara.

Zobacz: sekcje „Testy w każdym kręgu” i „Testy jako część systemu”.

</details>

### 35. Gdzie umieścić walidację, transakcje i obsługę błędów w modelu kręgów?

<details>
<summary>Odpowiedź</summary>

Walidacja: format w kręgu zewnętrznym (Pydantic), reguły aplikacji w interactorze, niezmienniki w encjach. Transakcje: interactor wyznacza granice przez interfejs Unit of Work z kręgu Use Cases, a implementacja leży w Interface Adapters. Błędy: w wariancie z presenterem są to metody Output Boundary, w wariancie zwracającym Response Model są to wyjątki z Use Cases lub Entities mapowane na HTTP na zewnątrz. Wyjątki bibliotek tłumaczy implementacja gateway'a.

Zobacz: sekcja „Walidacja, transakcje i błędy”.

</details>
