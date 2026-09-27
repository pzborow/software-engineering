# Przykład przewodni: Urząd Zaginionych Poniedziałków

Pakiet Pythona `urzad` obsługujący wnioski o odzyskanie zaginionego poniedziałku: pieczątki (także z przyszłości), załączniki z obcych kalendarzy, teczki, kontrole, głosowanie komisji, decyzje z powiadomieniami i cofaniem.

**Dokąd zmierza:** Zaczynamy od kontraktów (ABC/Protocol) i minimalnego pakietu z testem pytest. Potem powstaje model wniosku, następnie tworzenie (fabryki, Builder, Prototype, Singleton), struktury (Adapter, Bridge, Composite, Decorator, Fasada, Flyweight, Proxy) i zachowania (łańcuch kontroli, Command, Interpreter, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor). Na końcu fasada Okienko prowadzi wniosek od złożenia do decyzji i cofnięcia, co sprawdza test end-to-end.

## Plan przyrostów

| Dział | Co przybywa |
|---|---|
| [01. Interfejsy ABC i Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md) | Powstaje pakiet urzad z kontraktami Kalendarz (Protocol) i Kontrola (ABC) oraz pierwszy test pytest z atrapą. |
| [02. Model domeny wniosku](02%20Model%20domeny%20wniosku.md) | Przybywają dataclassy Wniosek, Pieczatka, Zalacznik, Glos, Decyzja, zdarzenia, wyjątek NiewaznaPieczatka oraz Factory Method i Abstract Factory parserów/walidatorów kalendarzy. |
| [03. Tworzenie wniosków](03%20Tworzenie%20wniosk%C3%B3w.md) | Wnioski powstają przez Builder, Prototype i konfigurację-Singleton, a Adapter, Bridge, Composite i Decorator dają obce kalendarze, powiadomienia, teczki i opakowania. |
| [04. Struktury wniosku](04%20Struktury%20wniosku.md) | Fasada Okienko, Flyweight pieczątek i Proxy weryfikatora składają się w strukturę, dochodzą łańcuch kontroli, Command, Interpreter reguł i iterator po teczce. |
| [05. Przepływ komisji](05%20Przep%C5%82yw%20komisji.md) | Mediator, Memento, Observer, State, Strategy, Template Method i Visitor łączą się w przepływ prowadzący wniosek do decyzji komisji. |
| [06. System Urzędu Zaginionych Poniedziałków](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md) | Command, Memento i Observer dają cofalną decyzję z powiadomieniami, a test end-to-end przez Okienko przeprowadza wniosek od złożenia do cofnięcia i ocenia, co zastąpić prostszym idiomem. |

## Stan kodu po ostatnim dziale

Szkic, nie działający kod: nazwy i sygnatury, których trzymają się przykłady w tekście.

### `tests/conftest.py`

```python
@pytest.fixture(autouse=True)
def czysta_konfiguracja(): ...
```

- **czysta_konfiguracja** (fixture pytest (autouse)): Czyści cache konfiguracji przed testem i po nim. Wprowadzony: [03 › Singleton jako konfiguracja urzędu](03%20Tworzenie%20wniosk%C3%B3w.md#singleton-jako-konfiguracja-urzędu).

### `tests/test_end_to_end.py`

```python
def test_od_zlozenia_do_cofniecia(): ...
```

- **test_od_zlozenia_do_cofniecia** (funkcja (test pytest)): Test end-to-end przez Okienko. Wprowadzony: [06 › Test end-to-end przez Okienko](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#test-end-to-end-przez-okienko).

### `tests/test_kontrola.py`

```python
class KalendarzStaly:
    def poniedzialki(self, rok: int) -> list[date]: ...

def test_poniedzialek_z_kalendarza_przechodzi(): ...
```

- **KalendarzStaly** (klasa (atrapa)): Atrapa kalendarza ze stałą listą poniedziałków, spełniająca Kalendarz strukturalnie. Wprowadzony: [01 › Struktura pakietu i pierwszy test](01%20Interfejsy%20ABC%20i%20Protocol.md#struktura-pakietu-i-pierwszy-test).
- **test_poniedzialek_z_kalendarza_przechodzi** (funkcja (test pytest)): Pierwszy test: KontrolaPoniedzialku z atrapą kalendarza. Wprowadzony: [01 › Uruchamianie pytest w terminalu](01%20Interfejsy%20ABC%20i%20Protocol.md#uruchamianie-pytest-w-terminalu).

### `urzad/fabryki.py`

```python
class Rejestr(ABC):
    def zloz(self, numer, poniedzialek, pieczatka, rok_biezacy) -> Wniosek: ...
    @abstractmethod
    def utworz_wniosek(self, numer, poniedzialek, pieczatka) -> Wniosek: ...

class RejestrPilnych(Rejestr):
    def utworz_wniosek(self, numer, poniedzialek, pieczatka) -> Wniosek: ...

def zloz(klasa: type[Wniosek], numer, poniedzialek, pieczatka, rok_biezacy) -> Wniosek: ...

class BudowniczyWniosku:
    def numer(self, numer: int) -> Self: ...
    def pilny(self, powod: str) -> Self: ...
    def build(self, rok_biezacy: int) -> Wniosek: ...

def wniosek_z_danych(dane: dict, konf: Konfiguracja) -> Wniosek: ...
```

- **Rejestr** (klasa abstrakcyjna (ABC)): Twórca Factory Method ze stałym przebiegiem składania. Wprowadzony: [02 › Factory Method dla wniosków](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków).
- **RejestrPilnych** (klasa (podklasa Rejestr)): Tworzy WniosekPilny. Wprowadzony: [02 › Factory Method dla wniosków](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków).
- **zloz** (funkcja): Funkcja fabryczna: prostsza alternatywa dla Rejestr. Wprowadzony: [02 › Factory Method dla wniosków](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków).
- **BudowniczyWniosku** (klasa (Builder)): Składa wniosek krok po kroku i waliduje go w build(). Wprowadzony: [03 › Builder składa wniosek](03%20Tworzenie%20wniosk%C3%B3w.md#builder-składa-wniosek).
- **wniosek_z_danych** (funkcja): Składa wniosek z danych wejściowych: fabryka parsera, Builder i rok z konfiguracji. Wprowadzony: [03 › Od danych do kompletnego wniosku](03%20Tworzenie%20wniosk%C3%B3w.md#od-danych-do-kompletnego-wniosku).

### `urzad/glosowanie.py`

```python
def jednomyslnie(glosy: tuple[Glos, ...]) -> bool: ...

class Kwalifikowana:
    def __init__(self, ulamek): ...
    wyniki: list[bool]
    def __call__(self, glosy: tuple[Glos, ...]) -> bool: ...
```

- **jednomyslnie** (funkcja (Strategy)): Bezstanowa strategia głosowania jako zwykła funkcja. Wprowadzony: [05 › Strategia jako funkcja albo klasa](05%20Przep%C5%82yw%20komisji.md#strategia-jako-funkcja-albo-klasa).
- **Kwalifikowana** (klasa (Strategy ze stanem)): Strategia z historią wyników dostępną z zewnątrz. Wprowadzony: [05 › Strategia jako funkcja albo klasa](05%20Przep%C5%82yw%20komisji.md#strategia-jako-funkcja-albo-klasa).

### `urzad/kalendarze.py`

```python
class ParserDaty(Protocol):
    def parsuj(self, tekst: str) -> date: ...

class WalidatorDaty(Protocol):
    def czy_poprawna(self, tekst: str) -> bool: ...

class FabrykaKalendarza(ABC):
    @abstractmethod
    def parser(self) -> ParserDaty: ...
    @abstractmethod
    def walidator(self) -> WalidatorDaty: ...

class FabrykaPolska(FabrykaKalendarza):
    def parser(self) -> ParserDaty: ...
    def walidator(self) -> WalidatorDaty: ...

class FabrykaIso(FabrykaKalendarza):
    def parser(self) -> ParserDaty: ...
    def walidator(self) -> WalidatorDaty: ...

def fabryka_dla(zalacznik: Zalacznik) -> FabrykaKalendarza: ...

class AdapterKalendarza:
    def __init__(self, obcy: KalendarzZewnetrzny): ...
    def poniedzialki(self, rok: int) -> list[date]: ...
```

- **ParserDaty** (protokół (Protocol)): Produkt rodziny: zamienia napis w danym formacie na datę. Wprowadzony: [02 › Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
- **WalidatorDaty** (protokół (Protocol)): Produkt rodziny: sprawdza, czy napis jest poprawny w danym formacie. Wprowadzony: [02 › Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
- **FabrykaKalendarza** (klasa abstrakcyjna (ABC)): Abstract Factory rodziny parser + walidator. Wprowadzony: [02 › Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
- **FabrykaPolska** (klasa (podklasa FabrykaKalendarza)): Rodzina dla formatu "pl" (04.03.2024). Wprowadzony: [02 › Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
- **FabrykaIso** (klasa (podklasa FabrykaKalendarza)): Rodzina dla formatu "iso". Wprowadzony: [02 › Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
- **fabryka_dla** (funkcja): Dobiera fabrykę do formatu załącznika przez słownik FABRYKI. Wprowadzony: [02 › Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
- **AdapterKalendarza** (klasa (Adapter)): Spełnia Protocol Kalendarz, tłumacząc wywołania na KalendarzZewnetrzny. Wprowadzony: [03 › Adapter obcego kalendarza](03%20Tworzenie%20wniosk%C3%B3w.md#adapter-obcego-kalendarza).

### `urzad/komisja.py`

```python
class Komisja:
    def __init__(self, wniosek: Wniosek, liczba: int): ...
    wniosek: Wniosek
    def zglos(self, glos: Glos) -> Decyzja | None: ...

class CzlonekKomisji:
    def __init__(self, nazwa: str, komisja: Komisja): ...
    def glosuj(self, za: bool) -> Decyzja | None: ...
```

- **Komisja** (klasa (Mediator)): Mediator zliczający głosy członków i zwracający Decyzja po ostatnim głosie. Wprowadzony: [05 › Mediator w środku komisji](05%20Przep%C5%82yw%20komisji.md#mediator-w-środku-komisji).
- **CzlonekKomisji** (klasa): Uczestnik znający tylko mediatora, nie innych członków. Wprowadzony: [05 › Mediator w środku komisji](05%20Przep%C5%82yw%20komisji.md#mediator-w-środku-komisji).

### `urzad/konfiguracja.py`

```python
@dataclass(frozen=True)
class Konfiguracja:
    rok_biezacy: int = 2024
    format_domyslny: str = "iso"

@cache
def konfiguracja() -> Konfiguracja: ...
```

- **Konfiguracja** (klasa (dataclass, frozen)): Zamrożona konfiguracja urzędu. Wprowadzony: [03 › Singleton jako konfiguracja urzędu](03%20Tworzenie%20wniosk%C3%B3w.md#singleton-jako-konfiguracja-urzędu).
- **konfiguracja** (funkcja (Singleton, @cache)): Zwraca zawsze tę samą instancję konfiguracji. Wprowadzony: [03 › Singleton jako konfiguracja urzędu](03%20Tworzenie%20wniosk%C3%B3w.md#singleton-jako-konfiguracja-urzędu).

### `urzad/kontrakty.py`

```python
class KalendarzObcy:
    def poniedzialki(self, rok: int) -> list[date]: ...

class Kalendarz(Protocol):
    def poniedzialki(self, rok: int) -> list[date]: ...

class Kontrola(ABC):
    @abstractmethod
    def sprawdz(self, wniosek: object) -> bool: ...

class KontrolaPoniedzialku(Kontrola):
    def __init__(self, kalendarz: Kalendarz): ...
    def sprawdz(self, wniosek: object) -> bool: ...

class KontrolaZDziennikiem(Kontrola):
    def __init__(self, wewnetrzna: Kontrola, dziennik: list[str]): ...
    def sprawdz(self, wniosek: object) -> bool: ...

class Ogniwo(Kontrola):
    def __init__(self, nastepne: Kontrola | None = None): ...
    def sprawdz(self, wniosek) -> bool: ...
    @abstractmethod
    def ok(self, wniosek) -> bool: ...

class OgniwoNumeru(Ogniwo):
    def ok(self, wniosek) -> bool: ...

class OgniwoStatusu(Ogniwo):
    def ok(self, wniosek) -> bool: ...
```

- **KalendarzObcy** (klasa): Obca klasa spełniająca Kalendarz bez dziedziczenia. Wprowadzony: [01 › ABC czy Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
- **Kalendarz** (protokół (Protocol)): Kontrakt dla obcych kalendarzy, spełniany przez kształt. Wprowadzony: [01 › ABC czy Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
- **Kontrola** (klasa abstrakcyjna (ABC)): Wspólny szkielet kontroli wniosków, wymuszony dziedziczeniem. Wprowadzony: [01 › ABC czy Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
- **KontrolaPoniedzialku** (klasa (podklasa Kontrola)): Kontrola z kalendarzem wstrzykniętym przez kompozycję. Wprowadzony: [01 › Składanie zamiast dziedziczenia](01%20Interfejsy%20ABC%20i%20Protocol.md#składanie-zamiast-dziedziczenia).
- **KontrolaZDziennikiem** (klasa (Decorator, podklasa Kontrola)): Opakowuje dowolną Kontrola i zapisuje jej wynik w dzienniku. Wprowadzony: [03 › Decorator obiektowy kontra funkcyjny](03%20Tworzenie%20wniosk%C3%B3w.md#decorator-obiektowy-kontra-funkcyjny).
- **Ogniwo** (klasa abstrakcyjna (podklasa Kontrola)): Ogniwo łańcucha: sprawdza własnym ok() i przekazuje dalej. Wprowadzony: [04 › Łańcuch kontroli wniosku](04%20Struktury%20wniosku.md#łańcuch-kontroli-wniosku).
- **OgniwoNumeru** (klasa (podklasa Ogniwo)): Wymaga dodatniego numeru. Wprowadzony: [04 › Łańcuch kontroli wniosku](04%20Struktury%20wniosku.md#łańcuch-kontroli-wniosku).
- **OgniwoStatusu** (klasa (podklasa Ogniwo)): Wymaga statusu zlozony. Wprowadzony: [04 › Łańcuch kontroli wniosku](04%20Struktury%20wniosku.md#łańcuch-kontroli-wniosku).

### `urzad/model.py`

```python
@dataclass
class Wniosek:
    numer: int
    poniedzialek: date
    pieczatka: Pieczatka
    status: str = "zlozony"
    def numery(self) -> list[int]: ...
    def zapisz(self) -> Migawka: ...
    def przywroc(self, migawka: Migawka) -> None: ...
    def przyjmij(self, w: Wizytator) -> None: ...

@dataclass(frozen=True)
class Pieczatka:
    rok: int
    def zweryfikuj(self, rok_biezacy: int) -> None: ...

class NiewaznaPieczatka(ValueError):
    def __init__(self, pieczatka: Pieczatka, rok_biezacy: int): ...

@dataclass(frozen=True)
class Zalacznik:
    nazwa: str
    format: str
    data: str
    def jako_date(self) -> date: ...

@dataclass(frozen=True)
class Glos:
    czlonek: str
    za: bool

@dataclass(frozen=True)
class Decyzja:
    numer: int
    glosy: tuple[Glos, ...]
    poprzedni_status: str
    @property
    def przyznana(self) -> bool: ...

@dataclass(frozen=True)
class DecyzjaPodjeta:
    numer: int
    przyznana: bool
    poprzedni_status: str

@dataclass(frozen=True)
class PieczatkaOdrzucona:
    numer: int
    rok: int
    rok_biezacy: int

@dataclass
class WniosekPilny(Wniosek):
    powod: str = ""

@dataclass(frozen=True)
class Migawka:
    _stan: dict = field(repr=False)

@dataclass(frozen=True)
class DecyzjaCofnieta:
    numer: int
    przywrocony_status: str
```

- **Wniosek** (klasa (dataclass)): Mutowalny byt o zmiennym statusie. Wprowadzony: [02 › Model wniosku jako dataclass](02%20Model%20domeny%20wniosku.md#model-wniosku-jako-dataclass).
  - zmiana w [03 › Composite i teczka wniosków](03%20Tworzenie%20wniosk%C3%B3w.md#composite-i-teczka-wniosków): Wniosek jako liść Composite potrzebuje metody numery().
  - zmiana w [05 › Memento jako migawka wniosku](05%20Przep%C5%82yw%20komisji.md#memento-jako-migawka-wniosku): Wniosek zyskuje zapis i przywracanie migawki (Memento).
  - zmiana w [05 › Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach): Wniosek jako liść przyjmuje wizytatora: w.odwiedz_wniosek(self).
- **Pieczatka** (klasa (dataclass, frozen)): Niezmienna wartość: rok pieczątki na wniosku. Wprowadzony: [02 › Model wniosku jako dataclass](02%20Model%20domeny%20wniosku.md#model-wniosku-jako-dataclass).
  - zmiana w [02 › Pieczątka z przyszłości](02%20Model%20domeny%20wniosku.md#pieczątka-z-przyszłości): Pieczatka dostaje metodę zweryfikuj sprawdzającą ważność względem bieżącego roku.
- **NiewaznaPieczatka** (wyjątek (podklasa ValueError)): Zgłaszany, gdy rok pieczątki jest późniejszy niż bieżący. Wprowadzony: [02 › Pieczątka z przyszłości](02%20Model%20domeny%20wniosku.md#pieczątka-z-przyszłości).
- **Zalacznik** (klasa (dataclass, frozen)): Załącznik z obcego kalendarza niesie nazwę formatu obok tekstowej daty. Wprowadzony: [02 › Załącznik z obcego kalendarza](02%20Model%20domeny%20wniosku.md#załącznik-z-obcego-kalendarza).
- **Glos** (klasa (dataclass, frozen)): Niezmienny głos jednego członka komisji. Wprowadzony: [02 › Głos i decyzja komisji](02%20Model%20domeny%20wniosku.md#głos-i-decyzja-komisji).
- **Decyzja** (klasa (dataclass, frozen)): Wynik głosowania z danymi potrzebnymi do cofnięcia. Wprowadzony: [02 › Głos i decyzja komisji](02%20Model%20domeny%20wniosku.md#głos-i-decyzja-komisji).
- **DecyzjaPodjeta** (klasa (dataclass, frozen)): Zdarzenie decyzji z zapisem statusu do cofnięcia. Wprowadzony: [02 › Zdarzenia w życiu wniosku](02%20Model%20domeny%20wniosku.md#zdarzenia-w-życiu-wniosku).
- **PieczatkaOdrzucona** (klasa (dataclass, frozen)): Zdarzenie odrzucenia pieczątki. Wprowadzony: [02 › Zdarzenia w życiu wniosku](02%20Model%20domeny%20wniosku.md#zdarzenia-w-życiu-wniosku).
- **WniosekPilny** (klasa (dataclass, podklasa Wniosek)): Wniosek pilny z dodatkowym polem powod. Wprowadzony: [02 › Factory Method dla wniosków](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków).
- **Migawka** (klasa (dataclass, frozen, Memento)): Niezmienna, nieprzejrzysta kopia stanu wniosku. Wprowadzony: [05 › Memento jako migawka wniosku](05%20Przep%C5%82yw%20komisji.md#memento-jako-migawka-wniosku).
- **DecyzjaCofnieta** (klasa (dataclass, frozen)): Zdarzenie cofnięcia decyzji. Wprowadzony: [06 › Decyzja z powiadomieniami i cofaniem](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem).

### `urzad/obce.py`

```python
class KalendarzZewnetrzny:
    def dni(self, rok: int, dzien_tygodnia: int) -> list[str]: ...
```

- **KalendarzZewnetrzny** (klasa (obca, nie do zmiany)): Kalendarz dostawcy z innym API, zwraca daty jako napisy ISO. Wprowadzony: [03 › Adapter obcego kalendarza](03%20Tworzenie%20wniosk%C3%B3w.md#adapter-obcego-kalendarza).

### `urzad/okienko.py`

```python
class Okienko:
    def __init__(self, konf: Konfiguracja, powiadomienie: Powiadomienie): ...
    teczka: Teczka
    def zloz(self, dane: dict) -> int: ...
    def zdecyduj(self, numer, glosy, adresat) -> bool: ...
    def cofnij(self, numer, adresat) -> None: ...
```

- **Okienko** (klasa (fasada)): Fasada urzędu: składa wniosek z danych i przeprowadza decyzję z powiadomieniem. Wprowadzony: [04 › Fasada jako okienko urzędu](04%20Struktury%20wniosku.md#fasada-jako-okienko-urzędu).
  - zmiana w [04 › Struktura wniosku przez okienko](04%20Struktury%20wniosku.md#struktura-wniosku-przez-okienko): Okienko tworzy pulę, proxy, adapter i teczkę w konstruktorze; zloz składa je w jedną kolejność, a teczka jest dostępna publicznie.
  - zmiana w [06 › Test end-to-end przez Okienko](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#test-end-to-end-przez-okienko): Test end-to-end przez fasadę wymaga cofnięcia bez sięgania do poleceń; Okienko trzyma stos poleceń.

### `urzad/pieczatki.py`

```python
class PulaPieczatek:
    def daj(self, rok: int) -> Pieczatka: ...
    def __len__(self) -> int: ...

class Weryfikator(Protocol):
    def weryfikuj(self, pieczatka: Pieczatka, rok_biezacy: int) -> None: ...

class WeryfikatorPieczatek:
    def weryfikuj(self, pieczatka: Pieczatka, rok_biezacy: int) -> None: ...

class ProxyWeryfikatora:
    def __init__(self, utworz: Callable[[], Weryfikator], uprawniony: bool = True): ...
    def weryfikuj(self, pieczatka: Pieczatka, rok_biezacy: int) -> None: ...
```

- **PulaPieczatek** (klasa (Flyweight)): Pula wydaje jeden współdzielony egzemplarz Pieczatka na rok. Wprowadzony: [04 › Flyweight i pula pieczątek](04%20Struktury%20wniosku.md#flyweight-i-pula-pieczątek).
- **Weryfikator** (protokół (Protocol)): Kontrakt wspólny dla prawdziwego weryfikatora i zastępnika. Wprowadzony: [04 › Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).
- **WeryfikatorPieczatek** (klasa): Drogi prawdziwy weryfikator, który woła Pieczatka.zweryfikuj. Wprowadzony: [04 › Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).
- **ProxyWeryfikatora** (klasa (Proxy)): Leniwy, cache'ujący i ochronny zastępnik weryfikatora. Wprowadzony: [04 › Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).

### `urzad/polecenia.py`

```python
class PoleceniaDecyzji:
    def __init__(self, wniosek: Wniosek, decyzja: Decyzja): ...
    def execute(self) -> None: ...
    def undo(self) -> None: ...

class CofalnaDecyzja(PoleceniaDecyzji):
    def __init__(self, wniosek, decyzja, migawka, publikator): ...
    def undo(self) -> None: ...
```

- **PoleceniaDecyzji** (klasa (Command)): Polecenie ustawia status wniosku według decyzji, a undo przywraca poprzedni_status. Wprowadzony: [04 › Command i cofanie decyzji](04%20Struktury%20wniosku.md#command-i-cofanie-decyzji).
- **CofalnaDecyzja** (klasa (podklasa PoleceniaDecyzji)): Polecenie przywraca migawkę i publikuje DecyzjaCofnieta. Wprowadzony: [06 › Decyzja z powiadomieniami i cofaniem](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem).

### `urzad/powiadomienia.py`

```python
class Kanal(Protocol):
    def wyslij(self, adresat: str, tresc: str) -> None: ...

class Powiadomienie:
    def __init__(self, kanal: Kanal): ...
    def o_decyzji(self, zdarzenie: DecyzjaPodjeta | DecyzjaCofnieta, adresat: str) -> None: ...

class PowiadomieniePilne(Powiadomienie): ...
```

- **Kanal** (protokół (Protocol)): Implementacja w Bridge: kanał wysyłki. Wprowadzony: [03 › Bridge powiadomienia i kanału](03%20Tworzenie%20wniosk%C3%B3w.md#bridge-powiadomienia-i-kanału).
- **Powiadomienie** (klasa (abstrakcja Bridge)): Trzyma kanał i buduje treść o decyzji. Wprowadzony: [03 › Bridge powiadomienia i kanału](03%20Tworzenie%20wniosk%C3%B3w.md#bridge-powiadomienia-i-kanału).
  - zmiana w [06 › Decyzja z powiadomieniami i cofaniem](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem): Publikator rozsyła też DecyzjaCofnieta, więc powiadomienie musi obsłużyć oba zdarzenia.
- **PowiadomieniePilne** (klasa (podklasa Powiadomienie)): Inna treść, ten sam kanał. Wprowadzony: [03 › Bridge powiadomienia i kanału](03%20Tworzenie%20wniosk%C3%B3w.md#bridge-powiadomienia-i-kanału).

### `urzad/przeplyw.py`

```python
def poprowadz(wniosek, glosy, kontrola, regula, publikator) -> tuple[Decyzja, Migawka] | None: ...

STANY = {s.nazwa: s for s in (Zlozony(), Przyznany(), Odrzucony())}
```

- **poprowadz** (funkcja): Składa kontrolę, migawkę, komisję, regułę, stan i zdarzenie w przepływ do decyzji. Wprowadzony: [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji).
- **STANY** (słownik): Wybiera obiekt stanu po bieżącym statusie wniosku. Wprowadzony: [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji).

### `urzad/reguly.py`

```python
@dataclass(frozen=True)
class Wiekszosc:
    prog: int
    def wartosc(self, glosy: tuple[Glos, ...]) -> bool: ...

class Jednomyslnosc:
    def wartosc(self, glosy: tuple[Glos, ...]) -> bool: ...

@dataclass(frozen=True)
class Oraz:
    lewa: Regula
    prawa: Regula
    def wartosc(self, glosy: tuple[Glos, ...]) -> bool: ...

@dataclass(frozen=True)
class Nie:
    regula: Regula
    def wartosc(self, glosy: tuple[Glos, ...]) -> bool: ...

class Regula(Protocol):
    def wartosc(self, glosy: tuple[Glos, ...]) -> bool: ...
```

- **Wiekszosc** (klasa (dataclass, frozen, węzeł Interpreter)): Liść reguły: co najmniej prog głosów za. Wprowadzony: [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
- **Jednomyslnosc** (klasa (węzeł Interpreter)): Liść reguły: wszystkie głosy za. Wprowadzony: [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
- **Oraz** (klasa (dataclass, frozen, węzeł Interpreter)): Iloczyn dwóch reguł. Wprowadzony: [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
- **Nie** (klasa (dataclass, frozen, węzeł Interpreter)): Negacja reguły. Wprowadzony: [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
- **Regula** (protokół (Protocol)): Kontrakt węzła drzewa reguł. Wprowadzony: [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).

### `urzad/rozpatrzenie.py`

```python
class Rozpatrzenie(ABC):
    def rozpatrz(self, wniosek, glosy) -> str: ...
    def kontrola(self, wniosek) -> bool: ...
    @abstractmethod
    def regula(self, glosy) -> bool: ...

class Jednomyslne(Rozpatrzenie):
    def regula(self, glosy) -> bool: ...
```

- **Rozpatrzenie** (klasa abstrakcyjna (Template Method)): Szablon rozpatrzenia: kontrola, głosowanie, zapis statusu. Wprowadzony: [05 › Template Method i szablon rozpatrzenia](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia).
- **Jednomyslne** (klasa (podklasa Rozpatrzenie)): Rozpatrzenie z regułą jednomyślności. Wprowadzony: [05 › Template Method i szablon rozpatrzenia](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia).

### `urzad/stany.py`

```python
class Stan(ABC):
    nazwa: str
    @abstractmethod
    def decyduj(self, przyznana: bool) -> "Stan": ...

class Zlozony(Stan):
    nazwa = "zlozony"
    def decyduj(self, przyznana): ...

class Przyznany(Stan):
    nazwa = "przyznany"
    def decyduj(self, przyznana): ...

class Odrzucony(Stan):
    nazwa = "odrzucony"
    def decyduj(self, przyznana): ...

class Status(Enum):
    ZLOZONY = "zlozony"
    PRZYZNANY = "przyznany"
    ODRZUCONY = "odrzucony"
```

- **Stan** (klasa abstrakcyjna (ABC)): Status wniosku jako obiekt zwracający następny stan. Wprowadzony: [05 › State zamiast ifów po statusie](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie).
- **Zlozony** (klasa (podklasa Stan)): Zwraca Przyznany albo Odrzucony. Wprowadzony: [05 › State zamiast ifów po statusie](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie).
- **Przyznany** (klasa (podklasa Stan)): Stan końcowy, zgłasza ValueError. Wprowadzony: [05 › State zamiast ifów po statusie](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie).
- **Odrzucony** (klasa (podklasa Stan)): Stan końcowy, zgłasza ValueError. Wprowadzony: [05 › State zamiast ifów po statusie](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie).
- **Status** (enum): Prostsza alternatywa: enum ze słownikiem PRZEJSCIA. Wprowadzony: [05 › State zamiast ifów po statusie](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie).

### `urzad/teczki.py`

```python
class Teczka:
    def __init__(self, nazwa: str): ...
    def dodaj(self, skladnik: Skladnik) -> None: ...
    def numery(self) -> list[int]: ...
    def __iter__(self) -> Iterator[int]: ...
    def przyjmij(self, w: Wizytator) -> None: ...

class Skladnik(Protocol):
    def numery(self) -> list[int]: ...
    def przyjmij(self, w: Wizytator) -> None: ...
```

- **Teczka** (klasa (Composite)): Kontener składników, który rekurencyjnie zbiera numery wniosków. Wprowadzony: [03 › Composite i teczka wniosków](03%20Tworzenie%20wniosk%C3%B3w.md#composite-i-teczka-wniosków).
  - zmiana w [04 › Iterator po teczce](04%20Struktury%20wniosku.md#iterator-po-teczce): Teczka dostaje __iter__ jako generator po drzewie składników; lista składników nazywa się _elementy.
  - zmiana w [05 › Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach): Teczka dostaje przyjmij, które rekurencyjnie przekazuje wizytatora składnikom.
- **Skladnik** (protokół (Protocol)): Wspólny kontrakt wniosku i teczki. Wprowadzony: [03 › Composite i teczka wniosków](03%20Tworzenie%20wniosk%C3%B3w.md#composite-i-teczka-wniosków).
  - zmiana w [05 › Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach): Teczka woła s.przyjmij(w) na składnikach, więc kontrakt musi ją zawierać.

### `urzad/wizytatorzy.py`

```python
class Wizytator(Protocol):
    def odwiedz_wniosek(self, wniosek: Wniosek) -> None: ...
    def odwiedz_teczke(self, teczka: Teczka) -> None: ...

class RaportStatusow:
    liczniki: Counter
    def odwiedz_wniosek(self, wniosek): ...
    def odwiedz_teczke(self, teczka): ...
```

- **Wizytator** (protokół (Protocol)): Kontrakt wizytatora teczek. Wprowadzony: [05 › Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach).
- **RaportStatusow** (klasa (Visitor)): Zlicza wnioski według statusu. Wprowadzony: [05 › Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach).

### `urzad/zdarzenia.py`

```python
class Publikator:
    def subskrybuj(self, metoda) -> Callable[[], None]: ...
    def publikuj(self, zdarzenie: DecyzjaPodjeta | DecyzjaCofnieta) -> None: ...
```

- **Publikator** (klasa (Observer)): Trzyma słabe referencje do obserwatorów i rozsyła DecyzjaPodjeta. Wprowadzony: [05 › Observer i subskrybenci zdarzeń](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń).
  - zmiana w [06 › Decyzja z powiadomieniami i cofaniem](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem): Publikator przyjmuje też DecyzjaCofnieta.
