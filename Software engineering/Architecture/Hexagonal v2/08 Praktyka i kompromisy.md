# Praktyka i kompromisy

Znasz już porty, adaptery, testy i transakcje, więc pora sprawdzić, jak to działa w prawdziwym projekcie. W „Rowerku” ułożymy pakiety domain/application/adapters, wymusimy kierunek zależności import-linterem, omówimy migrację monolitu i odczyty CQRS omijające porty.

```text
adapters --> application --> domain
   (import-linter pilnuje strzałek)
```

## Struktura pakietów projektu

Pakiety układaj według kierunku zależności, a nie według rodzaju klasy. Podział na `models/`, `repositories/` i `services/` miesza rdzeń z technologią. Zamiast tego [rdzeń](00%20Glosariusz.md#rdzeń) dzieli się na dwa pakiety, a wszystko zależne od technologii leży obok.

```text
rowerek/
├── core/
│   ├── domain/       # entities.py, pricing.py, events.py
│   └── application/  # ports.py, use_cases.py
├── infra/            # adaptery: sqlalchemy_*, stripe_gateway,
│                     #   rentals_router, lock_consumer
├── app/              # composition.py: składa całość
└── tests/            # fakes.py, testy
```

W przykładzie adaptery leżą w `infra/`; nazwa `adapters/` znaczy to samo. Ważny jest podział, nie nazwa.

### Kto co może importować

| Pakiet | Może importować |
|---|---|
| `core/domain` | tylko bibliotekę standardową |
| `core/application` | `core/domain` |
| `infra` | `core` (implementuje [porty](00%20Glosariusz.md#port)) |
| `app` | wszystko, bo to [composition root](00%20Glosariusz.md#composition-root) |

Porty leżą w `application`, bo opisują potrzeby scenariuszy. Używają jednak typów z `domain`, więc zależność biegnie właściwą stroną.

### Konsekwencja

Regułę „domain nie importuje niczego" można sprawdzać automatycznie. Robi to [import-linter](00%20Glosariusz.md#import-linter), narzędzie, które w CI zgłasza importy łamiące zadeklarowane kierunki; jego konfigurację omawia następna sekcja. Płacisz dodatkowym poziomem zagnieżdżenia. W małym projekcie `domain` i `application` możesz na start trzymać w jednym pliku, byle zachować kierunek.

## Wymuszanie kierunku importów

Kierunek zależności wymusisz kontraktami import-lintera w `pyproject.toml`, uruchamianymi w CI poleceniem `lint-imports`. Narzędzie buduje graf importów pakietu i sprawdza go z kontraktami. Naruszenie kończy się niezerowym kodem wyjścia.

Podstawą jest kontrakt `layers`: wymieniasz pakiety od najbardziej zewnętrznego do najbardziej wewnętrznego, a wyższa warstwa może importować niższą, nigdy odwrotnie. Zakładamy układ z poprzedniej sekcji, czyli rdzeń rozdzielony na `core/domain` i `core/application`.

```toml
[tool.importlinter]
root_package = "rowerek"
include_external_packages = true

[[tool.importlinter.contracts]]
name = "Kierunek zależności"
type = "layers"
layers = [
    "rowerek.app",
    "rowerek.infra",
    "rowerek.core.application",
    "rowerek.core.domain",
]
```

Ten kontrakt odtwarza tabelę importów z poprzedniej sekcji: `domain` nie sięgnie do `application`, a rdzeń do `infra`. Nie łapie jednak bibliotek zewnętrznych. Do tego służy drugi kontrakt, `type = "forbidden"`, z `source_modules = ["rowerek.core"]` i `forbidden_modules = ["sqlalchemy", "fastapi", "stripe"]`. Wymaga on `include_external_packages = true`, ustawionego wyżej.

### Konsekwencja

Import `sqlalchemy` w `core/domain/entities.py` przerywa build, zanim trafi do review. Importy pod `TYPE_CHECKING` narzędzie domyślnie też liczy, co zwykle jest pożądane. Wyjątki dopisywane przez `ignore_imports` traktuj jak dług: każdy to świadoma dziura w regule.

## Kiedy heksagon to nadmiar

Heksagon jest nadmiarowy, gdy nie masz reguł biznesowych do ochrony ani realnej zmienności technologii. Wtedy płacisz za strukturę, która nic nie kupuje.

Koszt jest stały: osobny model domenowy i model ORM, mapowanie między nimi, port na każdą rozmowę ze światem i okablowanie w composition root. Zysk zależy od tego, ile jest reguł do przetestowania w izolacji i ile razy zmienisz [adapter](00%20Glosariusz.md#adapter). Jeśli oba są bliskie zera, bilans jest ujemny.

| Sytuacja | Werdykt |
|---|---|
| Panel administracyjny z formularzami CRUD | Nadmiar, użyj ORM wprost |
| Skrypt, prototyp, jednorazowa migracja | Nadmiar |
| Mały serwis z jedną integracją i bez reguł | Zwykle nadmiar |
| Reguły z wyjątkami, wiele integracji, długie życie | Uzasadniony |

W „Rowerku” limit jednego wypożyczenia, blokada przy zaległej płatności i cennik uzasadniają rdzeń. Ekran edycji stacji już nie. Rozpoznasz go po takim [przypadku użycia](00%20Glosariusz.md#przypadek-użycia):

```python
# poza kanonem
class ListStations:
    def __init__(self, repo: StationRepository) -> None: ...
    def __call__(self) -> list[Station]:
        return self.repo.all()
```

Nie ma tu reguły, którą trzeba by izolować, więc jest tylko dodatkowa warstwa. Podobnie mapper kopiujący pola jeden do jednego.

### Konsekwencja

Stosuj heksagon selektywnie: rdzeń tam, gdzie żyją reguły, a proste fragmenty zostaw bez portów. Pomyłkę w drugą stronę naprawisz taniej, bo wyodrębnienie rdzenia z działającego kodu to znana ścieżka, a usuwanie niepotrzebnych warstw z całego systemu jest żmudne.

## Migracja monolitu krok po kroku

Zacznij od jednego scenariusza, np. rozpoczęcia wypożyczenia w „Rowerku”, i przechodź go w czterech krokach. Każdy krok kończy się działającym, wdrażalnym systemem.

| Krok | Co robisz | Ryzyko |
|---|---|---|
| 1 | Testy charakteryzujące zachowanie widoku, przez HTTP i prawdziwą bazę | brak |
| 2 | Reguły (limit, blokada, cennik) do [obiektów wartości](00%20Glosariusz.md#obiekt-wartości) i encji | niskie |
| 3 | [Port repozytorium](00%20Glosariusz.md#port-repozytorium) z adapterem opakowującym modele ORM | średnie |
| 4 | Przypadek użycia w rdzeniu, a widok tylko go wywołuje | niskie |

Sednem jest krok 3. Adapter czyta i zapisuje te same tabele co dotąd, ale na zewnątrz zwraca encje:

```python
class SqlAlchemyRentalRepository(RentalRepository):
    def __init__(self, session: Session) -> None:
        self.session = session

    def active_for_user(self, user_id: str) -> Rental | None:
        row = (self.session.query(RentalRow)  # istniejący model ORM
               .filter_by(user_id=user_id, returned_at=None).first())
        return self._to_domain(row) if row else None

    def add(self, rental: Rental) -> None:
        self.session.add(RentalRow(id=rental.id, ...))

    @staticmethod
    def _to_domain(row: RentalRow) -> Rental:
        return Rental(id=row.id, bike_id=row.bike_id, user_id=row.user_id)
```

`RentalRow` zostaje bez zmian, więc niemigrowane widoki nadal z niego korzystają. Po kroku 4 widok jest cienki:

```python
@router.post("/rentals")
def start_rental(body: StartRentalRequest,
                 use_case: StartRental = Depends(get_start_rental)) -> RentalResponse:
    rental = use_case(body.user_id, body.bike_id)
    return RentalResponse(id=rental.id, ...)
```

### Pilnuj granicy

Nowe pakiety obejmij kontraktami import-lintera od pierwszego dnia, a stare moduły zostaw poza nimi. Znane wyjątki wpisuj jawnie do `ignore_imports`; ich lista ma się kurczyć.

### Konsekwencja

Migracja jest odwracalna scenariusz po scenariuszu, bo widok i stare modele wciąż istnieją. Reszta monolitu może zostać bez portów.

## Odczyty CQRS a porty domeny

Nie, odczyty nie muszą przechodzić przez porty domeny. W [CQRS](00%20Glosariusz.md#cqrs) (rozdzieleniu poleceń zmieniających stan od zapytań, które go tylko czytają) zapytanie może pójść prosto do bazy i zwrócić gotowy model odczytu, z pominięciem encji i portów repozytoriów.

Powód jest prosty: porty i encje chronią reguły biznesowe przy zmianie stanu. Zapytanie żadnych reguł nie egzekwuje, więc ładowanie agregatów tylko po to, by zaraz przepisać je na JSON, jest kosztem bez zysku. Lista wypożyczeń użytkownika z nazwą stacji to zwykły `JOIN`, a nie scenariusz domeny.

Polecenia zostają bez zmian: `StartRental` i `FinishRental` nadal idą przez [Unit of Work](00%20Glosariusz.md#unit-of-work) i porty. Zapytanie to osobna, cienka ścieżka, którą import-linter może dopuścić do infrastruktury, ale nie do rdzenia w drugą stronę:

```text
POST /rentals      → StartRental → UnitOfWork → baza
GET  /users/{id}/rentals → RentalHistoryQuery → SQL (bez encji)
```

Ścieżka odczytu może mieć własny [port wejściowy](00%20Glosariusz.md#port-wejściowy-driving) lub być zwykłą funkcją w adapterze; ważne, by zwracała obiekty wartości lub DTO, a nie wiersze ORM.

### Granica

Odczyt omija porty, ale nie reguły. Jeśli zapytanie musi zdecydować, co wolno (np. „czy użytkownik może wypożyczyć”), to reguła domenowa i wraca do rdzenia. Uważaj też na odczyt tuż przed zapisem: sprawdzenie limitu na modelu odczytu, a potem polecenie, daje wyścig. Kontrolę wykonaj w poleceniu, w transakcji.

## Co zapamiętać

- Układaj pakiety według kierunku zależności (adapters → application → domain), a nie według rodzaju klasy.
- Kontrakty `layers` i `forbidden` w import-linterze zamieniają regułę kierunku zależności w test CI, który przerywa build przy każdym niedozwolonym imporcie.
- Heksagon opłaca się tam, gdzie są reguły biznesowe i zmienna infrastruktura; przy czystym CRUD-zie i krótkim życiu kodu jest tylko kosztem.
- Migruj scenariusz po scenariuszu: adapter opakowuje istniejące modele ORM i zwraca encje, schemat się nie zmienia, a stare widoki działają dalej.
- Odczyty CQRS mogą omijać porty i encje, bo nie chronią reguł, ale każda decyzja biznesowa należy do polecenia w transakcji.

## Pytania sprawdzające

### 41. Jak zorganizować strukturę pakietów projektu w Pythonie (domain, application, adapters)?

<details>
<summary>Odpowiedź</summary>

Podziel projekt na pakiety odpowiadające kierunkowi zależności: domain (encje, obiekty wartości, zdarzenia), application (przypadki użycia i porty) oraz adapters z infrastrukturą. Okablowanie i testy leżą osobno, bo mogą znać wszystko. Importy idą tylko do środka: adapters → application → domain, a domain nie importuje niczego z projektu. Dzięki temu strukturę da się sprawdzić mechanicznie, a nie tylko konwencją.

Zobacz: [sekcja „Struktura pakietów projektu”](#struktura-pakietów-projektu).

</details>

### 42. Jak automatycznie wymusić kierunek zależności, np. za pomocą import-linter?

<details>
<summary>Odpowiedź</summary>

Zadeklaruj kontrakty import-lintera w `pyproject.toml` i uruchamiaj `lint-imports` w CI. Kontrakt `layers` pilnuje kierunku między pakietami (app → infra → application → domain), a kontrakt `forbidden` blokuje importy bibliotek takich jak sqlalchemy czy fastapi w rdzeniu. Naruszenie daje niezerowy kod wyjścia, więc łamiący regułę import nie przechodzi przez CI.

Zobacz: [sekcja „Wymuszanie kierunku importów”](#wymuszanie-kierunku-importów).

</details>

### 43. Kiedy architektura heksagonalna jest nadmiarowa (over-engineering)?

<details>
<summary>Odpowiedź</summary>

Architektura heksagonalna jest nadmiarowa, gdy nie ma czego chronić: aplikacja to głównie CRUD bez logiki domenowej, kod jest krótkotrwały albo technologia na pewno się nie zmieni. Koszt (dodatkowe pakiety, mapowanie modeli, pośrednictwo portów) płacisz zawsze, a zysk (testowalne reguły, wymienialna infrastruktura) dostajesz tylko wtedy, gdy reguły i zmienność istnieją. Objawem nadmiaru są przypadki użycia, które tylko delegują do repozytorium, i encje bez zachowania.

Zobacz: [sekcja „Kiedy heksagon to nadmiar”](#kiedy-heksagon-to-nadmiar).

</details>

### 44. Jak stopniowo wprowadzić architekturę heksagonalną do monolitu z logiką w widokach i modelach ORM?

<details>
<summary>Odpowiedź</summary>

Migruj po jednym scenariuszu, w czterech krokach, a każdy kończ działającym systemem. Najpierw testy charakteryzujące, potem reguły w czystych klasach, potem port repozytorium z adapterem opakowującym istniejące modele ORM, na końcu przypadek użycia wywoływany przez cienki widok. Schemat bazy się nie zmienia, a stare widoki działają dalej, więc każdy krok da się cofnąć. Migrujesz tylko to, co zmieniasz albo co się psuje.

Zobacz: [sekcja „Migracja monolitu krok po kroku”](#migracja-monolitu-krok-po-kroku).

</details>

### 45. Czy odczyty w podejściu CQRS muszą przechodzić przez porty domeny?

<details>
<summary>Odpowiedź</summary>

Nie. W CQRS zapytania nie egzekwują reguł biznesowych, więc mogą czytać bazę bezpośrednio i zwracać modele odczytu, bez ładowania encji i przechodzenia przez porty repozytoriów. Polecenia nadal idą przez use case'y, Unit of Work i porty. Decyzje biznesowe, także te podejmowane tuż przed zapisem, muszą jednak zostać w poleceniu, w transakcji.

Zobacz: [sekcja „Odczyty CQRS a porty domeny”](#odczyty-cqrs-a-porty-domeny).

</details>
