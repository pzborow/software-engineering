# Pułapki i decyzje

Clean Architecture ma więcej nazwanych elementów niż Hexagonal czy Onion, więc łatwiej ją przesadzić. Zespół, który dosłownie odwzoruje diagram Martina dla każdego endpointu, dostanie osiem plików na prosty odczyt. Zespół, który uprości za mocno, straci ochronę reguł. Ten rozdział opisuje typowe problemy i rozsądne kompromisy.

## Pełny zestaw w API REST

Przepływ z rozdziału 03 (Input Boundary, Request Model, interactor, Output Boundary, Response Model, presenter, View Model) został zaprojektowany z myślą o UI, który może wyświetlać wynik na wiele sposobów. W typowym API REST żądanie i odpowiedź są synchroniczne, a framework oczekuje, że funkcja obsługi zwróci odpowiedź. Presenter trzymający stan i widok, który go odczytuje, stają się wtedy <a id="term-ceremony"></a>[ceremonią](00%20Glossary%20Clean.md#ceremony), czyli kodem, który spełnia formę wzorca, ale nie wnosi korzyści.

Rozsądne uproszczenie zachowuje Dependency Rule i usuwa to, co w API nic nie daje:

```python
# use_cases/reserve_room.py: jeden moduł na przypadek użycia
@dataclass(frozen=True)
class ReserveRoomRequest:
    room_id: str
    organizer_id: str
    start: datetime
    end: datetime


@dataclass(frozen=True)
class ReserveRoomResponse:
    reservation_id: str
    start: datetime
    end: datetime


class RoomTaken(ReservationError):
    pass


class ReserveRoom:
    def __init__(self, reservations: ReservationGateway, clock: Clock):
        self._reservations = reservations
        self._clock = clock

    def __call__(self, request: ReserveRoomRequest) -> ReserveRoomResponse:
        ...                                           # ta sama logika, zwraca wynik albo rzuca wyjątek
```

```python
# frameworks/web.py: kontroler i presenter w jednej funkcji
@app.post("/reservations", status_code=201)
def reserve(body: ReserveBody, user=Depends(current_user), reserve_room=Depends(get_reserve_room)):
    result = reserve_room(ReserveRoomRequest(body.room_id, user.id, body.start, body.end))
    return {"id": result.reservation_id, "when": f"{result.start:%d.%m %H:%M}–{result.end:%H:%M}"}


@app.exception_handler(RoomTaken)
def room_taken(request, exc):
    return JSONResponse(status_code=409, content={"error": str(exc)})
```

| Element | Pełna wersja | Uproszczenie dla API |
|---|---|---|
| Input Boundary | osobny `Protocol` | klasa use case'u jest interfejsem |
| Output Boundary i presenter | interfejs, klasa ze stanem | zwracany Response Model, mapowanie w endpoincie |
| View Model | osobna klasa | słownik JSON albo model Pydantic w endpoincie |
| Błędy | metody Output Boundary | wyjątki z Use Cases, handler w frameworku |
| Request i Response Model | zostają | zostają |
| Gateway'e i Dependency Rule | zostają | zostają |

Pełny presenter warto zostawić tam, gdzie ten sam przypadek użycia ma kilka różnych wyjść (API, panel HTML, eksport CSV) albo gdzie wynik jest przekazywany asynchronicznie.

## Logika w złym kręgu

<a id="term-logic-leak"></a>[Wyciek logiki](00%20Glossary%20Clean.md#logic-leak) to reguła biznesowa, która trafiła do kontrolera, presentera albo zapytania SQL. Interactor staje się wtedy cienką rurką przekazującą dane, a reguły są rozsiane po krawędziach systemu.

```python
# kontroler zna regułę 14 dni
def reserve(self, body: dict, user_id: str) -> None:
    start = datetime.fromisoformat(body["start"])
    if start - datetime.now() > timedelta(days=14):     # reguła aplikacji w kontrolerze
        raise HTTPException(422, "Za daleko")
    self._reserve_room.execute(...)


# presenter zna regułę anulowania
def success(self, response):
    can_cancel = response.start - datetime.now() > timedelta(hours=24)   # reguła encji w presenterze
    self.view_model = ReservationViewModel(201, {"cancellable": can_cancel})
```

Objawy są przewidywalne. Reguła działa w API, ale nie działa w CLI. Presenter HTML pokazuje przycisk „Anuluj”, a presenter JSON pokazuje co innego. Testy interactora przechodzą, choć system zachowuje się niezgodnie z wymaganiami.

Naprawa polega na przeniesieniu reguły do właściwego kręgu i przekazaniu wyniku w Response Model:

```python
# encja zna regułę
class Reservation:
    def can_be_cancelled(self, now: datetime) -> bool:
        return self.slot.start - now >= self.CANCELLATION_NOTICE


# interactor przekazuje decyzję
ReserveRoomResponse(..., cancellable=reservation.can_be_cancelled(self._clock.now()))


# presenter tylko ją formatuje
body = {"id": response.reservation_id, "cancellable": response.cancellable}
```

Pomaga prosty test: każdy `if`, który porównuje daty, kwoty albo statusy, powinien być w kręgu Entities albo Use Cases. W kontrolerze i presenterze mogą być tylko `if`-y dotyczące formatu.

## Za dużo plików na jeden przypadek użycia

Dosłowne odwzorowanie diagramu prowadzi do <a id="term-interface-explosion"></a>[eksplozji interfejsów](00%20Glossary%20Clean.md#interface-explosion). Na każdy przypadek użycia przypada osiem elementów: Input Boundary, Output Boundary, Request Model, Response Model, interactor, presenter, View Model i kontroler, często każdy w osobnym pliku. Przy 50 przypadkach użycia daje to 400 plików, z których większość ma po kilka linii.

Sposoby ograniczenia:

- jeden moduł na przypadek użycia, zawierający Request Model, Response Model i interactor,
- Input Boundary tylko wtedy, gdy są dwie implementacje albo interactor jest publikowany jako biblioteka,
- wspólny presenter dla grupy przypadków użycia, jeśli formatują dane w ten sam sposób,
- brak osobnego View Model, gdy odpowiada 1:1 formatowi JSON,
- granice częściowe z rozdziału 05 zamiast pełnych tam, gdzie granica jest tylko prawdopodobna,
- `Protocol` zamiast klas abstrakcyjnych, bo nie wymaga dziedziczenia i kosztuje kilka linii.

```text
Dosłownie (8 plików):                  Rozsądnie (2 pliki):
reserve_room/                          use_cases/reserve_room.py
├── input_boundary.py                      ReserveRoomRequest, ReserveRoomResponse,
├── output_boundary.py                     RoomTaken, ReserveRoom
├── request_model.py                   web/reservations.py
├── response_model.py                      endpoint + mapowanie na JSON
├── interactor.py
├── presenter.py
├── view_model.py
└── controller.py
```

Pytanie kontrolne dla każdego elementu: czy ma albo realnie będzie miał drugą implementację lub drugiego klienta? Jeśli nie, jest kandydatem do połączenia z sąsiednim elementem.

## Migracja istniejącej aplikacji

Przepisanie aplikacji Django albo FastAPI od zera rzadko się udaje. Bezpieczniej przechodzić stopniowo, według wzorca <a id="term-strangler-fig"></a>[strangler fig](00%20Glossary%20Clean.md#strangler-fig): nowa struktura otacza stary kod i przejmuje kolejne funkcje, aż stary kod można usunąć.

Przed pierwszą zmianą zamroź obecne zachowanie <a id="term-characterization-test"></a>[testami charakteryzującymi](00%20Glossary%20Clean.md#characterization-test). Takie testy wywołują API i sprawdzają to, co system zwraca dziś, łącznie z dziwactwami.

```text
krok 1  testy charakteryzujące     zamroź zachowanie endpointów
krok 2  nowy pakiet rooms.core     z import-linterem od pierwszego dnia
krok 3  jeden przypadek użycia     najlepiej często zmieniany i bogaty w reguły
krok 4  encje                      czyste dataclassy obok modeli Django
krok 5  gateway                    interfejs w core, implementacja na Django ORM
krok 6  widok Django               staje się kontrolerem i presenterem, woła interactor
krok 7  powtarzaj                  aż stare serwisy i „grube modele” znikną
```

W Django modele `models.Model` nie znikają. Stają się modelem persystencji w kręgu Interface Adapters, a implementacja gateway'a tłumaczy je na encje:

```python
# interface_adapters/django_reservation_gateway.py
from rooms.web.models import ReservationModel          # model Django zostaje na zewnątrz


class DjangoReservationGateway:
    def for_room(self, room_id: str) -> list[Reservation]:
        return [self._to_entity(m) for m in ReservationModel.objects.filter(room_id=room_id)]

    def add(self, reservation: Reservation) -> None:
        ReservationModel.objects.create(
            id=reservation.id, room_id=reservation.room_id,
            organizer_id=reservation.organizer_id,
            starts_at=reservation.slot.start, ends_at=reservation.slot.end,
        )
```

Gdy nowy kod musi korzystać ze starego modelu danych z innymi pojęciami, stosuje się <a id="term-anti-corruption-layer"></a>[anti-corruption layer](00%20Glossary%20Clean.md#anti-corruption-layer): implementację gateway'a, która tłumaczy stare pojęcia na język nowych encji. Nowy kod widzi `Reservation` z `TimeSlot`, a nie tabelę `SALE_REZ` z kolumnami `DT_OD`, `DT_DO` i `FLAGA_ANUL`.

## Co zapamiętać

- W synchronicznym API REST pełny presenter i View Model to często ceremonia.
- Uproszczenie: klasa use case'u zwraca Response Model, błędy są wyjątkami, a Dependency Rule i gateway'e zostają.
- Reguły w kontrolerach i presenterach to wyciek logiki, a jego objawem jest różne zachowanie w różnych interfejsach.
- W kontrolerze i presenterze mogą być tylko warunki dotyczące formatu.
- Eksplozję plików ogranicza się, łącząc elementy, które nie mają drugiej implementacji ani drugiego klienta.
- Migracja idzie przypadek po przypadku: testy charakteryzujące, nowy pakiet z `import-linter`, gateway na starym ORM.
- Modele Django zostają jako model persystencji na zewnątrz, a anti-corruption layer tłumaczy stare pojęcia.

## Pytania sprawdzające

### 39. Dlaczego pełny zestaw boundaries, Request i Response Models oraz presenterów bywa przesadą w API REST? Jak to uprościć?

<details>
<summary>Odpowiedź</summary>

Pełny przepływ zaprojektowano z myślą o UI z wieloma formami prezentacji i asynchronicznym wyjściem. W synchronicznym API framework oczekuje, że funkcja zwróci odpowiedź, więc presenter ze stanem i odczyt View Model to ceremonia. Uproszczenie: klasa use case'u pełni rolę Input Boundary, zwraca Response Model, błędy są wyjątkami z Use Cases obsługiwanymi przez handler frameworka, a mapowanie na JSON odbywa się w endpoincie. Request i Response Model, gateway'e i Dependency Rule zostają. Pełny presenter warto zostawić, gdy jest kilka wyjść albo wynik idzie asynchronicznie.

Zobacz: sekcja „Pełny zestaw w API REST”.

</details>

### 40. Co zrobić, gdy interactory stają się anemiczne, a logika ląduje w kontrolerach albo presenterach?

<details>
<summary>Odpowiedź</summary>

To wyciek logiki. Objawy to reguła działająca w API, ale nie w CLI, oraz różne zachowanie presenterów. Trzeba przenieść reguły przedsiębiorstwa do encji (np. `can_be_cancelled`), reguły aplikacji do interactora, a decyzje przekazywać w Response Model, żeby presenter tylko je formatował. Test: każdy `if` porównujący daty, kwoty lub statusy należy do Entities albo Use Cases. W kontrolerze i presenterze zostają tylko warunki dotyczące formatu.

Zobacz: sekcja „Logika w złym kręgu”.

</details>

### 41. Jak uniknąć eksplozji plików (osobny interfejs, model wejścia i wyjścia oraz presenter dla każdego use case'u)?

<details>
<summary>Odpowiedź</summary>

Trzymać Request Model, Response Model i interactor w jednym module na przypadek użycia. Input Boundary tworzyć tylko przy dwóch implementacjach lub publikowaniu biblioteki. Używać wspólnego presentera dla podobnych przypadków, pomijać View Model, gdy odpowiada JSON-owi 1:1, stosować granice częściowe i `Protocol` zamiast klas abstrakcyjnych. Kryterium: element bez drugiej implementacji i bez drugiego klienta jest kandydatem do połączenia.

Zobacz: sekcja „Za dużo plików na jeden przypadek użycia”.

</details>

### 42. Jak stopniowo zmigrować istniejącą aplikację (np. Django albo FastAPI) do Clean Architecture?

<details>
<summary>Odpowiedź</summary>

Stopniowo, wzorcem strangler fig. Najpierw testy charakteryzujące zamrażają zachowanie endpointów. Potem powstaje nowy pakiet `core` z `import-linter` od pierwszego dnia. Następnie jeden przypadek użycia na raz: encje jako czyste dataclassy, gateway z interfejsem w `core` i implementacją na starym ORM, widok przerobiony na kontroler i presenter wołający interactor. Modele Django zostają jako model persystencji na zewnątrz, a stary model danych o innych pojęciach obsługuje anti-corruption layer.

Zobacz: sekcja „Migracja istniejącej aplikacji”.

</details>
