# Przepływ przez granicę

Najbardziej charakterystyczny element Clean Architecture to sposób, w jaki żądanie przechodzi przez granicę przypadku użycia i wraca jako odpowiedź. Martin narysował go w prawym dolnym rogu słynnego diagramu. Ten rozdział rozkłada ten rysunek na klasy.

```text
Interface Adapters      Use Cases                                     Interface Adapters
──────────────────      ─────────────────────────────────────────     ──────────────────
Controller ──woła──►    «interface» ReserveRoomInput
                                ▲ implementuje
                        ReserveRoomInteractor ──woła──► «interface» ReserveRoomOutput
                                                                ▲ implementuje
                                                        Presenter ──► ViewModel ──► View
```

## Wejście do przypadku użycia

<a id="term-input-boundary"></a>[Input Boundary](00%20Glossary%20Clean.md#input-boundary) to interfejs, przez który świat zewnętrzny wywołuje przypadek użycia. Definiuje go krąg Use Cases, a implementuje interactor.

<a id="term-request-model"></a>[Request Model](00%20Glossary%20Clean.md#request-model) to prosta struktura danych wejściowych. Nie jest obiektem frameworka ani słownikiem z JSON-a. Zawiera tylko pola potrzebne przypadkowi użycia, w typach wygodnych dla niego:

```python
# use_cases/reserve_room/boundaries.py
from dataclasses import dataclass
from datetime import datetime
from typing import Protocol


@dataclass(frozen=True)
class ReserveRoomRequest:                   # Request Model
    room_id: str
    organizer_id: str
    start: datetime
    end: datetime


class ReserveRoomInput(Protocol):           # Input Boundary
    def execute(self, request: ReserveRoomRequest) -> None: ...
```

Różnica wobec DTO frameworka jest istotna. `BaseModel` z Pydantic albo serializer DRF należą do frameworka i leżą na zewnątrz. Request Model to zwykła dataclassa z kręgu Use Cases. Przypadek użycia można wywołać z testu, CLI albo kolejki bez importowania czegokolwiek z frameworka.

## Wyjście z przypadku użycia

<a id="term-output-boundary"></a>[Output Boundary](00%20Glossary%20Clean.md#output-boundary) to interfejs, przez który interactor przekazuje wynik. Też definiuje go krąg Use Cases, ale implementuje go klasa z zewnątrz.

<a id="term-response-model"></a>[Response Model](00%20Glossary%20Clean.md#response-model) to prosta struktura z wynikiem przypadku użycia. Zawiera dane w postaci biznesowej: daty jako `datetime`, a nie sformatowane napisy.

```python
@dataclass(frozen=True)
class ReserveRoomResponse:                  # Response Model
    reservation_id: str
    room_id: str
    start: datetime
    end: datetime


class ReserveRoomOutput(Protocol):          # Output Boundary
    def success(self, response: ReserveRoomResponse) -> None: ...
    def room_taken(self, room_id: str) -> None: ...
    def rejected(self, reason: str) -> None: ...
```

Interactor implementuje wejście i wywołuje wyjście:

```python
# use_cases/reserve_room/interactor.py
class ReserveRoomInteractor:                # implementuje ReserveRoomInput
    MAX_DAYS_AHEAD = 14

    def __init__(self, reservations: ReservationGateway, clock: Clock, output: ReserveRoomOutput):
        self._reservations = reservations
        self._clock = clock
        self._output = output

    def execute(self, request: ReserveRoomRequest) -> None:
        if request.start - self._clock.now() > timedelta(days=self.MAX_DAYS_AHEAD):
            return self._output.rejected("Można rezerwować najwyżej 14 dni do przodu")

        candidate = Reservation(str(uuid4()), request.room_id, request.organizer_id,
                                TimeSlot(request.start, request.end))
        if any(candidate.conflicts_with(r) for r in self._reservations.for_room(request.room_id)):
            return self._output.room_taken(request.room_id)

        self._reservations.add(candidate)
        self._output.success(ReserveRoomResponse(candidate.id, candidate.room_id,
                                                 candidate.slot.start, candidate.slot.end))
```

## Tłumacz wejścia

<a id="term-controller"></a>[Kontroler](00%20Glossary%20Clean.md#controller) leży w kręgu Interface Adapters. Bierze dane w formacie frameworka, buduje Request Model i wywołuje Input Boundary. Nie podejmuje decyzji i nie formatuje odpowiedzi.

```python
# interface_adapters/reservation_controller.py
from datetime import datetime


class ReservationController:
    def __init__(self, reserve_room: ReserveRoomInput):
        self._reserve_room = reserve_room

    def reserve(self, body: dict, user_id: str) -> None:
        self._reserve_room.execute(ReserveRoomRequest(
            room_id=body["room_id"],
            organizer_id=user_id,
            start=datetime.fromisoformat(body["start"]),
            end=datetime.fromisoformat(body["end"]),
        ))
```

## Tłumacz wyjścia i model widoku

<a id="term-presenter"></a>[Presenter](00%20Glossary%20Clean.md#presenter) implementuje Output Boundary. Dostaje Response Model i zamienia go na <a id="term-view-model"></a>[View Model](00%20Glossary%20Clean.md#view-model), czyli strukturę, w której wszystko jest już gotowe do wyświetlenia: napisy, sformatowane daty, kody statusu, flagi dla przycisków.

```python
# interface_adapters/reservation_presenter.py
from dataclasses import dataclass


@dataclass
class ReservationViewModel:
    status_code: int = 500
    body: dict | None = None


class ReserveRoomJsonPresenter:             # implementuje ReserveRoomOutput
    def __init__(self):
        self.view_model = ReservationViewModel()

    def success(self, response: ReserveRoomResponse) -> None:
        self.view_model = ReservationViewModel(201, {
            "id": response.reservation_id,
            "room": response.room_id,
            "when": f"{response.start:%d.%m.%Y %H:%M}–{response.end:%H:%M}",
        })

    def room_taken(self, room_id: str) -> None:
        self.view_model = ReservationViewModel(409, {"error": f"Sala {room_id} jest zajęta"})

    def rejected(self, reason: str) -> None:
        self.view_model = ReservationViewModel(422, {"error": reason})
```

Widok w kręgu Frameworks & Drivers tylko przepisuje View Model do odpowiedzi. Nie ma w nim żadnej logiki, więc nie trzeba go testować:

```python
# frameworks/web.py
@app.post("/reservations")
def reserve(body: dict, user=Depends(current_user)):
    presenter = ReserveRoomJsonPresenter()
    controller = ReservationController(build_reserve_room(output=presenter))
    controller.reserve(body, user.id)
    vm = presenter.view_model
    return JSONResponse(status_code=vm.status_code, content=vm.body)
```

Ta sama logika może mieć drugi presenter, na przykład `ReserveRoomHtmlPresenter` dla panelu administracyjnego albo `ReserveRoomCliPresenter` dla terminala. Interactor się nie zmienia.

## Pełny przepływ i odwrócenie zależności

Po złożeniu wszystkich części widać różnicę między <a id="term-flow-of-control"></a>[przepływem sterowania](00%20Glossary%20Clean.md#flow-of-control) a kierunkiem zależności w kodzie:

```text
Przepływ sterowania (kto kogo woła w czasie działania):
Controller ──► Interactor ──► Presenter ──► View

Zależności w kodzie (kto kogo importuje):
Controller ──► ReserveRoomInput      ◄── Interactor
Interactor ──► ReserveRoomOutput     ◄── Presenter
Presenter  ──► ReserveRoomResponse   (zdefiniowany w Use Cases)
```

Sterowanie przechodzi z interactora do presentera, czyli z kręgu wewnętrznego do zewnętrznego. Gdyby interactor importował presenter, Dependency Rule byłaby złamana. Dlatego interactor zna tylko interfejs `ReserveRoomOutput`, który sam definiuje. Presenter ten interfejs implementuje. Zależność w kodzie wskazuje do środka, choć sterowanie płynie na zewnątrz. Na tym polega odwrócenie zależności na granicy.

## Zwracać czy prezentować

Dlaczego interactor woła presenter zamiast po prostu zwrócić wynik? Martin podaje kilka powodów:

- interactor nie decyduje o formacie wyniku, więc ta sama logika obsłuży JSON, HTML i CLI,
- różne wyniki (sukces, sala zajęta, odrzucenie) są osobnymi metodami, a nie flagami do sprawdzania w kontrolerze,
- interactor może przekazać wynik asynchronicznie albo kilka razy, na przykład postęp długiej operacji,
- kontroler i widok nie muszą rozumieć wyniku, bo presenter już go przetłumaczył.

W typowym API REST, gdzie żądanie i odpowiedź są synchroniczne, wiele zespołów wybiera prostszy wariant: interactor zwraca Response Model, a kontroler przekazuje go do presentera albo sam mapuje na JSON.

```python
class ReserveRoomInteractor:
    def execute(self, request: ReserveRoomRequest) -> ReserveRoomResponse:
        ...
        return ReserveRoomResponse(...)
```

Ten wariant nie łamie Dependency Rule, bo Response Model jest zdefiniowany w kręgu Use Cases, a kontroler zależy od niego, czyli do środka. Traci się elastyczność wielu wyników i asynchroniczności, ale zyskuje prostotę. Błędy przekazuje się wtedy wyjątkami zdefiniowanymi w Use Cases. Rozdział 08 wraca do tego kompromisu.

## Dostęp do danych przez granicę

Dostęp do danych przechodzi przez granicę tak samo jak wynik, tylko w drugą stronę. Interactor woła <a id="term-gateway"></a>[gateway](00%20Glossary%20Clean.md#gateway), którego interfejs leży w kręgu Use Cases, a implementacja w Interface Adapters:

```text
Przepływ sterowania:  Interactor ──► SqlReservationGateway ──► PostgreSQL
Zależności w kodzie:  Interactor ──► ReservationGateway ◄── SqlReservationGateway
```

Martin opisuje gateway jako interfejs z metodą dla każdej operacji, której potrzebuje aplikacja. W praktyce jest to repozytorium z DDD. Metody zwracają encje albo proste struktury i są nazwane językiem przypadków użycia (`for_room`), a nie językiem bazy. Cały SQL, ORM i wiedza o tabelach zostają w implementacji.

Gateway nie musi dotyczyć bazy. Ten sam wzorzec obsługuje zewnętrzne API (`CalendarGateway` dla synchronizacji z Google Calendar), wysyłkę e-maili czy system plików.

## Co zapamiętać

- Input Boundary to interfejs wejścia do przypadku użycia, implementuje go interactor.
- Output Boundary to interfejs wyjścia, implementuje go presenter.
- Request i Response Model to proste struktury z kręgu Use Cases, a nie DTO frameworka.
- Kontroler tłumaczy format frameworka na Request Model i wywołuje interactor.
- Presenter zamienia Response Model na View Model, a widok tylko go wyświetla.
- Sterowanie płynie z interactora do presentera, ale zależność w kodzie wskazuje do środka.
- Zwracanie Response Model zamiast wołania presentera jest dozwolonym uproszczeniem w synchronicznym API.
- Gateway to interfejs danych w kręgu Use Cases, zwykle odpowiednik repozytorium.

## Pytania sprawdzające

### 14. Czym są Input Boundary i Output Boundary i kto definiuje te interfejsy?

<details>
<summary>Odpowiedź</summary>

Input Boundary to interfejs, przez który świat zewnętrzny wywołuje przypadek użycia. Implementuje go interactor, a woła kontroler. Output Boundary to interfejs, przez który interactor przekazuje wynik. Implementuje go presenter. Oba definiuje krąg Use Cases, bo tylko wtedy zależności w kodzie wskazują do środka.

Zobacz: sekcje „Wejście do przypadku użycia” i „Wyjście z przypadku użycia”.

</details>

### 15. Czym są Request Model i Response Model? Czym różnią się od DTO frameworka?

<details>
<summary>Odpowiedź</summary>

To proste struktury danych (np. dataclassy) zdefiniowane w kręgu Use Cases: Request Model z danymi wejściowymi, Response Model z wynikiem w postaci biznesowej (np. `datetime`, a nie sformatowany napis). DTO frameworka, jak `BaseModel` z Pydantic czy serializer DRF, należą do frameworka i leżą na zewnątrz. Request i Response Model nie zależą od żadnego frameworka, więc przypadek użycia można wywołać z testu, CLI albo kolejki.

Zobacz: sekcje „Wejście do przypadku użycia” i „Wyjście z przypadku użycia”.

</details>

### 16. Jaką rolę pełni Presenter i czym różni się od kontrolera?

<details>
<summary>Odpowiedź</summary>

Kontroler obsługuje wejście: tłumaczy dane frameworka na Request Model i wywołuje Input Boundary. Presenter obsługuje wyjście: implementuje Output Boundary, dostaje Response Model i zamienia go na View Model gotowy do wyświetlenia (napisy, sformatowane daty, kody statusu). Oba leżą w Interface Adapters i żaden nie podejmuje decyzji biznesowych.

Zobacz: sekcje „Tłumacz wejścia” i „Tłumacz wyjścia i model widoku”.

</details>

### 17. Czym jest View Model w Clean Architecture i kto go tworzy?

<details>
<summary>Odpowiedź</summary>

To struktura, w której wszystko jest gotowe do wyświetlenia: napisy, sformatowane daty, kody statusu, flagi dla przycisków. Tworzy go presenter na podstawie Response Model. Widok tylko przepisuje View Model do odpowiedzi, bez logiki, dzięki czemu nie trzeba go testować.

Zobacz: sekcja „Tłumacz wyjścia i model widoku”.

</details>

### 18. Opisz pełny przepływ żądania: kontroler → interactor → presenter → widok. Gdzie odwraca się zależność?

<details>
<summary>Odpowiedź</summary>

Kontroler tłumaczy żądanie na Request Model i woła Input Boundary. Interactor wykonuje logikę i woła Output Boundary. Presenter tworzy View Model, a widok go wyświetla. Zależność odwraca się na wyjściu: sterowanie płynie z interactora (krąg wewnętrzny) do presentera (krąg zewnętrzny), ale interactor zna tylko interfejs Output Boundary, który sam definiuje, a presenter go implementuje. Zależność w kodzie wskazuje więc do środka.

Zobacz: sekcja „Pełny przepływ i odwrócenie zależności”.

</details>

### 19. Dlaczego use case przekazuje wynik do presentera zamiast go zwrócić? Kiedy zwracanie wyniku jest akceptowalne?

<details>
<summary>Odpowiedź</summary>

Bo interactor nie powinien decydować o formacie wyniku. Ta sama logika obsłuży wtedy JSON, HTML i CLI. Różne wyniki są osobnymi metodami, a nie flagami, i można je przekazać asynchronicznie albo kilka razy. W synchronicznym API REST akceptowalne jest zwracanie Response Model. Nie łamie to Dependency Rule, bo Response Model jest zdefiniowany w Use Cases. Traci się elastyczność, a zyskuje prostotę, a błędy przekazuje się wtedy wyjątkami.

Zobacz: sekcja „Zwracać czy prezentować”.

</details>

### 20. Jak Clean Architecture podchodzi do repozytoriów i gateway'ów danych?

<details>
<summary>Odpowiedź</summary>

Dostęp do danych idzie przez gateway: interfejs zdefiniowany w kręgu Use Cases, z metodą dla każdej potrzebnej operacji, nazwaną językiem przypadków użycia. Implementacja leży w Interface Adapters i zawiera cały SQL i ORM. Praktycznie jest to repozytorium z DDD. Ten sam wzorzec obsługuje zewnętrzne API, e-maile czy pliki.

Zobacz: sekcja „Dostęp do danych przez granicę”.

</details>
