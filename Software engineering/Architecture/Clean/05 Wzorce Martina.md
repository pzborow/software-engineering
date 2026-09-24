# Wzorce Martina

Książka „Clean Architecture” wprowadza kilka wzorców, których nie ma w opisach Hexagonal i Onion. Odpowiadają na praktyczne pytania: jak testować kod na granicy, gdzie tworzyć obiekty, co zrobić, gdy pełna granica jest za droga, i jak powinna wyglądać struktura katalogów.

```text
Humble Object          kod trudny do testowania zredukuj do minimum
Main Component         jedno miejsce, które zna wszystko i wszystko tworzy
Partial Boundaries     tańsze granice na zapas
Screaming Architecture struktura mówi, co robi system, a nie jakiego używa frameworka
```

## Skromny obiekt na granicy

<a id="term-humble-object"></a>[Humble Object](00%20Glossary%20Clean.md#humble-object) to wzorzec, który dzieli zachowanie na dwie części: trudną do testowania i łatwą do testowania. Część trudna, „skromna”, jest ograniczona do absolutnego minimum. Część łatwa zawiera całą logikę.

Najlepszym przykładem jest para presenter i widok z rozdziału 03. Widok jest skromnym obiektem: przepisuje View Model do odpowiedzi HTTP albo szablonu i nie robi nic więcej. Presenter zawiera całą logikę formatowania i daje się przetestować zwykłym testem jednostkowym.

```python
# presenter: cała logika, łatwy test
def test_presenter_formats_time_range():
    p = ReserveRoomJsonPresenter()
    p.success(ReserveRoomResponse("r-1", "sala-A",
                                  datetime(2026, 10, 5, 9, 0), datetime(2026, 10, 5, 10, 30)))
    assert p.view_model.status_code == 201
    assert p.view_model.body["when"] == "05.10.2026 09:00–10:30"


# widok: skromny obiekt, nie ma czego testować
def render(vm: ReservationViewModel) -> JSONResponse:
    return JSONResponse(status_code=vm.status_code, content=vm.body)
```

Martin wskazuje, że wzorzec pojawia się na każdej granicy architektury:

| Granica | Skromny obiekt | Testowalna część |
|---|---|---|
| UI | widok, szablon | presenter |
| Baza danych | kod SQL, ORM, sterownik | interactor i gateway jako interfejs |
| Usługi zewnętrzne | klient HTTP, listener wiadomości | kod tłumaczący dane usługi na struktury aplikacji |

Dzięki temu granica architektoniczna jest jednocześnie granicą testowalności. Po jednej stronie leży kod, który wymaga prawdziwej technologii, i jest go mało. Po drugiej jest logika, którą testuje się szybko.

## Najbrudniejsze miejsce w systemie

<a id="term-main-component"></a>[Main Component](00%20Glossary%20Clean.md#main-component) to komponent, który tworzy, konfiguruje i łączy wszystkie inne. Martin nazywa go „ostatecznym szczegółem” i „najbrudniejszym” komponentem systemu. Zna wszystkie klasy, czyta konfigurację, tworzy fabryki i strategie, a potem oddaje sterowanie do wysokopoziomowej części systemu.

```python
# main.py
def main() -> None:
    settings = Settings.from_env()
    engine = create_engine(settings.database_url)
    session_factory = sessionmaker(bind=engine)

    def build_reserve_room(output: ReserveRoomOutput) -> ReserveRoomInteractor:
        session = session_factory()
        return ReserveRoomInteractor(
            reservations=SqlReservationGateway(session),
            clock=SystemClock(),
            output=output,
        )

    app = create_web_app(build_reserve_room)
    uvicorn.run(app, host="0.0.0.0", port=settings.port)


if __name__ == "__main__":
    main()
```

Dependency Rule obowiązuje także tutaj: nic nie zależy od Main, a Main zależy od wszystkiego. Dzięki temu Main jest wtyczką do reszty aplikacji. Można mieć kilka takich komponentów, na przykład `main_dev.py` z repozytoriami w pamięci, `main_prod.py` z PostgreSQL i `main_test.py` dla testów end-to-end. Aplikacja się nie zmienia, zmienia się tylko sposób jej złożenia.

## Tańsze granice

Pełna granica architektoniczna jest droga: interfejsy wejścia i wyjścia, osobne struktury danych, osobne komponenty wydawane niezależnie. Czasem zespół przewiduje, że granica może się przydać, ale nie chce płacić za nią od razu. Martin opisuje wtedy <a id="term-partial-boundary"></a>[granice częściowe](00%20Glossary%20Clean.md#partial-boundary) w trzech wariantach.

Pierwszy wariant to pominięcie ostatniego kroku. Kod jest podzielony tak, jakby miał trafić do dwóch komponentów, z interfejsami i własnymi strukturami danych, ale całość jest budowana i wydawana jako jeden komponent. Oszczędza to koszt zarządzania wersjami, a zachowuje możliwość rozdzielenia.

Drugi wariant to granica jednowymiarowa, czyli wzorzec Strategy. Zamiast pary Input i Output Boundary jest jeden interfejs, przez który klient woła implementację. Zabezpiecza to tylko jeden kierunek i łatwo go obejść, ale kosztuje jeden `Protocol`:

```python
class NotificationSender(Protocol):          # jedyny interfejs na granicy
    def reservation_confirmed(self, reservation_id: str, email: str) -> None: ...


class SmtpNotificationSender:
    def reservation_confirmed(self, reservation_id: str, email: str) -> None:
        ...
```

Trzeci wariant to fasada. Klasa fasady udostępnia wszystkie usługi jako metody i przekazuje wywołania do klas, których klient nie powinien widzieć. Nie ma tu odwrócenia zależności, bo klient zależy od fasady, a fasada od klas usług. Jest to najtańszy i najsłabszy wariant:

```python
class ReservationsFacade:
    def reserve(self, room_id: str, start: datetime, end: datetime) -> str: ...
    def cancel(self, reservation_id: str) -> None: ...
    def list_for_room(self, room_id: str) -> list[ReservationSummary]: ...
```

| Wariant | Koszt | Siła ochrony | Kiedy |
|---|---|---|---|
| Pełna granica | wysoki | pełna | granica jest pewna i ważna |
| Pominięcie ostatniego kroku | średni | dobra, dopóki dyscyplina trzyma | granica prawdopodobna, jeden zespół |
| Strategy | niski | jeden kierunek | wymienny dostawca, np. powiadomienia |
| Fasada | najniższy | słaba | uporządkowanie dostępu bez odwracania zależności |

Martin podkreśla, że decyzja o granicy nie jest jednorazowa. Architekt obserwuje system i dodaje granicę wtedy, gdy koszt jej braku zaczyna przewyższać koszt jej wprowadzenia.

## Struktura, która mówi o domenie

<a id="term-screaming-architecture"></a>[Screaming Architecture](00%20Glossary%20Clean.md#screaming-architecture) to zasada, że struktura projektu powinna „krzyczeć” o tym, co system robi. Martin porównuje to do planów budynku: po planie od razu widać, czy to szpital, czy biblioteka. Po katalogach projektu powinno być widać, że to system rezerwacji sal, a nie „aplikacja Django”.

```text
Krzyczy „Django”:                 Krzyczy „rezerwacje sal”:

project/                          rooms/
├── models.py                     ├── reservations/
├── views.py                      │   ├── reserve_room.py
├── serializers.py                │   ├── cancel_reservation.py
├── urls.py                       │   └── list_room_schedule.py
└── admin.py                      ├── rooms/
                                  │   └── add_room.py
                                  ├── notifications/
                                  └── web/          (framework na obrzeżu)
```

Po lewej widać framework, a nie wiadomo, co system robi. Po prawej najwyższy poziom to przypadki użycia i obszary biznesowe, a framework jest jednym z katalogów na obrzeżu.

Martin dodaje, że dobra architektura jest zorganizowana wokół przypadków użycia, a nie wokół frameworka. Framework jest narzędziem, więc nie powinien dyktować struktury. Nowa osoba w zespole, otwierając repozytorium, powinna od razu zobaczyć listę przypadków użycia.

## Co zapamiętać

- Humble Object dzieli kod na mały, trudny do testowania fragment i testowalną logikę.
- Presenter i widok to typowa para Humble Object, a wzorzec pojawia się na każdej granicy.
- Main Component tworzy i łączy wszystko, nic od niego nie zależy, jest wtyczką do aplikacji.
- Granice częściowe to tańsze warianty: pominięcie ostatniego kroku, Strategy i fasada.
- Decyzja o granicy zależy od kosztu jej braku i może zapaść później.
- Screaming Architecture: struktura projektu pokazuje przypadki użycia, a nie framework.

## Pytania sprawdzające

### 28. Czym jest wzorzec Humble Object i gdzie występuje w Clean Architecture?

<details>
<summary>Odpowiedź</summary>

To podział zachowania na część trudną do testowania, zredukowaną do minimum („skromną”), i część łatwą do testowania, zawierającą całą logikę. Klasyczna para to widok, który tylko przepisuje View Model, i presenter, który zawiera logikę formatowania. Wzorzec występuje na każdej granicy: UI (widok i presenter), baza (SQL i ORM oraz gateway jako interfejs), usługi zewnętrzne (klient HTTP i kod tłumaczący). Dzięki temu granica architektoniczna jest też granicą testowalności.

Zobacz: sekcja „Skromny obiekt na granicy”.

</details>

### 29. Czym jest Main Component i dlaczego jest „najbrudniejszym” miejscem w systemie?

<details>
<summary>Odpowiedź</summary>

To komponent, który czyta konfigurację, tworzy wszystkie obiekty (gateway'e, interactory, presentery, fabryki) i łączy je, a potem przekazuje sterowanie do aplikacji. Jest „najbrudniejszy”, bo zna wszystkie klasy i szczegóły techniczne. Nic od niego nie zależy, więc jest wtyczką do reszty systemu. Można mieć kilka wariantów Main, np. dla dev, prod i testów.

Zobacz: sekcja „Najbrudniejsze miejsce w systemie”.

</details>

### 30. Czym są częściowe granice (partial boundaries) i kiedy warto je stosować zamiast pełnych?

<details>
<summary>Odpowiedź</summary>

To tańsze warianty granicy na wypadek, gdyby pełna granica miała się przydać w przyszłości. Są trzy warianty. Pominięcie ostatniego kroku: kod jest podzielony jak dwa komponenty, ale wydawany jako jeden. Granica jednowymiarowa (Strategy): jeden interfejs zamiast pary boundaries. Fasada: jedna klasa przekazuje wywołania, bez odwracania zależności. Stosuje się je, gdy pełna granica jest za droga w stosunku do pewności, że będzie potrzebna, a decyzję można zmienić później.

Zobacz: sekcja „Tańsze granice”.

</details>

### 31. Co oznacza Screaming Architecture i jak struktura katalogów ma „krzyczeć” o domenie, a nie o frameworku?

<details>
<summary>Odpowiedź</summary>

Że struktura projektu powinna pokazywać, co system robi, tak jak plan budynku pokazuje, czy to szpital, czy biblioteka. Najwyższy poziom katalogów to obszary biznesowe i przypadki użycia (`reservations/reserve_room.py`, `cancel_reservation.py`), a framework jest jednym katalogiem na obrzeżu. Układ `models.py`, `views.py`, `serializers.py` krzyczy o Django, a nie o rezerwacjach sal.

Zobacz: sekcja „Struktura, która mówi o domenie”.

</details>
