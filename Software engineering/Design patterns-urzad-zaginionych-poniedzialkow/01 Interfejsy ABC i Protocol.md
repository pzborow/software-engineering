# Interfejsy ABC i Protocol

Wzorce projektowe GoF w Pythonie to sprawdzone sposoby układania klas i obiektów, dzięki którym kod rośnie bez przepisywania go od nowa przy każdej zmianie wymagań. Dzielą się na kreacyjne (jak powstają obiekty), [strukturalne](00%20Glosariusz.md#typowanie-strukturalne) (jak się łączą) i behawioralne (jak współpracują i dzielą obowiązki). W tym dziale dziedziny łączą się tak: projektowanie obiektowe pokazujemy na przykładach z urzędu rozpatrującego wnioski o zaginiony poniedziałek, a każde rozwiązanie sprawdzamy testami w [pytest](00%20Glosariusz.md#pytest). Po tym dziale ustalisz, jakie metody ma udostępniać dana część kodu, by inne mogły z niej korzystać bez znajomości jej wnętrza, uzasadnisz wybór między klasą bazową wymuszającą implementację a samym opisem wymaganych metod i uruchomisz pierwszy test, w którym sztuczny obiekt zastępuje prawdziwy składnik.

**W tym dziale:**

- [ABC czy Protocol](#abc-czy-protocol)
- [Trzy wnioski o poniedziałek](#trzy-wnioski-o-poniedziałek)
- [Składanie zamiast dziedziczenia](#składanie-zamiast-dziedziczenia)
- [Idea podwójnej dyspozycji](#idea-podwójnej-dyspozycji)
- [Trzy rodziny wzorców](#trzy-rodziny-wzorców)
- [Wzorzec czy zwykła funkcja](#wzorzec-czy-zwykła-funkcja)
- [Struktura pakietu i pierwszy test](#struktura-pakietu-i-pierwszy-test)
- [Atrapa z podglądem wywołań](#atrapa-z-podglądem-wywołań)
- [Koszt podwójnej dyspozycji](#koszt-podwójnej-dyspozycji)
- [Uruchamianie pytest w terminalu](#uruchamianie-pytest-w-terminalu)

## ABC czy Protocol

Wybierz [ABC](00%20Glosariusz.md#abc-klasa-abstrakcyjna) (klasę abstrakcyjną), gdy kontrakt ma wymuszać dziedziczenie i dostarczać wspólny kod. Wybierz [Protocol](00%20Glosariusz.md#protocol), gdy chcesz opisać samo zachowanie, a implementacje mają pozostać niezależne, także te z cudzych bibliotek.

Różnica leży w typowaniu. ABC jest [nominalne](00%20Glosariusz.md#typowanie-nominalne) (obiekt spełnia kontrakt, bo jawnie po nim dziedziczy): próba utworzenia instancji z niezaimplementowaną `@abstractmethod` kończy się `TypeError` już w konstruktorze. Protocol jest strukturalne (liczy się kształt metod, nie deklarowane pochodzenie): sprawdza go dopiero type checker (np. mypy), nie interpreter.

| | ABC | Protocol |
|---|---|---|
| Spełnienie kontraktu | przez dziedziczenie | przez zgodny kształt |
| Kiedy błąd | w czasie działania, przy tworzeniu obiektu | w type checkerze |
| Wspólny kod w bazie | tak | zwykle nie |
| Obce klasy | trzeba opakować | pasują bez zmian |

W urzędzie mamy oba przypadki. `Kalendarz` opisują obce systemy, których kodu nie zmienimy, więc to Protocol. `Kontrola` to nasza rodzina kontroli, która ma wymuszony wspólny szkielet, więc to ABC.

<a id="lm-1"></a>

```python
class Kalendarz(Protocol):
    def poniedzialki(self, rok: int) -> list[date]: ...

class Kontrola(ABC):
    @abstractmethod
    def sprawdz(self, wniosek: object) -> bool: ...

class KalendarzObcy:  # nie dziedziczy po Kalendarz
    def poniedzialki(self, rok: int) -> list[date]:
        return [date(rok, 1, 6)]
```

`KalendarzObcy` pasuje wszędzie tam, gdzie oczekiwany jest `Kalendarz`, mimo braku dziedziczenia. Protocol daje też małą [atrapę](00%20Glosariusz.md#atrapa) w testach bez żadnej bazy.

_Wersje: Python 3.13 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-interfejsy-abc-i-protocol)_

## Trzy wnioski o poniedziałek

Kontrakty z poprzedniej sekcji dostaną teraz prawdziwe dane, żeby było widać, co mają obsłużyć. Poniżej trzy wnioski o zaginiony poniedziałek, każdy z innym kłopotem. Na razie to zwykłe słowniki, bo [model wniosku (klasę) zbudujemy później](02%20Model%20domeny%20wniosku.md#ref-2).

```python
WNIOSKI = [
    {"id": 1, "poniedzialek": date(2025, 3, 3), "pieczatka": date(2025, 3, 4),
     "zalaczniki": [("gregoriański", "2025-03-03")], "decyzja": "przyznana"},
    {"id": 2, "poniedzialek": date(2025, 3, 10), "pieczatka": date(2031, 1, 1),
     "zalaczniki": [("juliański", "2025-02-25")], "decyzja": None},
    {"id": 3, "poniedzialek": date(2025, 3, 17), "pieczatka": None,
     "zalaczniki": [], "decyzja": "odrzucona"},
]
for w in WNIOSKI:
    print(w["id"], w["pieczatka"], len(w["zalaczniki"]), w["decyzja"])
```

```text
1 2025-03-04 1 przyznana
2 2031-01-01 1 None
3 None 0 odrzucona
```

Każdy wniosek pokazuje inną trudność:

- **Wniosek 1** jest poprawny. Pieczątka jest z następnego dnia, załącznik ma ten sam kalendarz co urząd, a decyzja zapadła.
- <a id="lm-2"></a>**Wniosek 2** ma pieczątkę z przyszłości (rok 2031), więc trzeba ją rozpoznać i odrzucić. Załącznik pochodzi z kalendarza juliańskiego: ten sam poniedziałek to tam 25 lutego, więc bez przeliczenia daty się nie zgadzają. Decyzji jeszcze brak.
- **Wniosek 3** nie ma pieczątki ani załączników, a decyzja jest odrzucona. Jest to więc wniosek zamknięty, [który później trzeba będzie umieć cofnąć](04%20Struktury%20wniosku.md#ref-3).

Wspólny problem to niejednorodność. Daty przychodzą w różnych kalendarzach, pieczątki mogą być nieważne, a decyzja bywa pusta. Dlatego urząd opiera się na kontraktach, a nie na konkretnych klasach.

## Składanie zamiast dziedziczenia

Kontrakty są gotowe, więc pora zdecydować, jak z nich budować kontrole urzędu. Składanie bywa elastyczniejsze, bo [kompozycja](00%20Glosariusz.md#kompozycja) (obiekt trzyma inny obiekt i deleguje mu pracę) pozwala wymienić część w czasie działania, a dziedziczenie wiąże ją na stałe w definicji klasy.

Weźmy kontrolę, czy poniedziałek z wniosku istnieje w kalendarzu. Przy dziedziczeniu każdy kalendarz wymusza własną podklasę: `KontrolaGregorianska`, `KontrolaJulianska` i tak dalej. Każdy nowy wymiar (np. inny rok) mnoży klasy.

Przy składaniu jest jedna klasa, a kalendarz dostaje w konstruktorze:

```python
class KontrolaPoniedzialku(Kontrola):
    def __init__(self, kalendarz: Kalendarz):
        self.kalendarz = kalendarz

    def sprawdz(self, wniosek: object) -> bool:
        ...  # bierze poniedziałek z wniosku
        return dzien in self.kalendarz.poniedzialki(rok)

KontrolaPoniedzialku(KalendarzObcy())
```

Działa to dzięki temu, że `KontrolaPoniedzialku` zna tylko Protocol `Kalendarz`. Obca klasa `KalendarzObcy`, [która nie dziedziczy po Kalendarz](#lm-1), pasuje bez żadnych zmian.

| | Dziedziczenie | Składanie |
|---|---|---|
| Moment wyboru | definicja klasy | konstruktor, także w testach |
| Nowy kalendarz | nowa podklasa | nowy obiekt |
| Sprzężenie | z całą klasą bazową | z jedną metodą kontraktu |

Dziedziczenie zostaje tam, gdzie [ABC daje wspólny kod](#abc-czy-protocol), jak `Kontrola` dla wszystkich kontroli. Zmienną część wkładamy jednak do środka, jako składnik. Ten sam ruch wróci przy [Bridge, który rozdzieli powiadomienie od kanału wysyłki](03%20Tworzenie%20wniosk%C3%B3w.md#ref-6).

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-interfejsy-abc-i-protocol)_

## Idea podwójnej dyspozycji

[Podwójna dyspozycja](00%20Glosariusz.md#podwójna-dyspozycja) to wybór wykonywanego kodu według typów dwóch obiektów naraz. Zwykłe wywołanie metody tego nie daje, bo Python wybiera metodę wyłącznie po typie obiektu, na którym ją wywołujesz.

W `kontrola.sprawdz(x)` o wyborze decyduje klasa `kontrola`. Typ argumentu `x` nie ma wpływu: Python nie przeciąża metod po typach parametrów. Jeśli kontrola ma inaczej traktować wniosek, a inaczej załącznik, zostaje łańcuch `isinstance` w środku metody. Każdy nowy typ oznacza edycję tego łańcucha.

Sztuczka polega na dwóch wywołaniach z zamienionymi rolami. Element woła metodę kontrolera, której nazwa zdradza jego typ, i przekazuje siebie:

```python
# poza kanonem
class Wniosek:
    def przyjmij(self, k): return k.dla_wniosku(self)

class Zalacznik:
    def przyjmij(self, k): return k.dla_zalacznika(self)

class Kontroler:
    def dla_wniosku(self, w): return "kontrola pieczątki"
    def dla_zalacznika(self, z): return "kontrola kalendarza"

for e in (Wniosek(), Zalacznik()):
    print(e.przyjmij(Kontroler()))
```

```text
kontrola pieczątki
kontrola kalendarza
```

<a id="lm-4"></a>Pierwsza dyspozycja wybiera `przyjmij` po typie elementu. Druga wybiera `dla_...` po typie kontrolera. Wynik zależy od pary typów, a żadnego `isinstance` nie ma.

Ten mechanizm jest sercem wzorca Visitor, [do którego wrócimy przy operacjach na strukturze teczek](05%20Przep%C5%82yw%20komisji.md#ref-8).

> **Pułapka: Nowy typ elementu bez metody w Kontroler.** Każdy nowy typ elementu wymaga równoległej metody `dla_...` w `Kontroler` i we wszystkich kontrolerach. Brak jej wychodzi dopiero w runtime jako `AttributeError` przy `przyjmij`, a nie przy definicji klasy. Wspólny interfejs (ABC z `@abstractmethod`) przenosi błąd na instancjonowanie.

## Trzy rodziny wzorców

Każda rodzina zmienia co innego: wzorzec kreacyjny zmienia to, **jak powstaje** obiekt, strukturalny to, **jak obiekty się łączą**, a behawioralny to, **kto co robi w czasie działania**. Wszystkie trzy opierają się na kontraktach z tego działu, bo wymiana części jest możliwa tylko wtedy, gdy klient zna interfejs, a nie klasę.

| Rodzina | Zmienia | Przykład w urzędzie |
|---|---|---|
| kreacyjna | tworzenie obiektu | fabryka wybiera kalendarz, klient nie zna jego klasy |
| strukturalna | budowę z części | cache owinięty wokół `Kalendarz`, z tym samym interfejsem |
| behawioralna | podział obowiązków | lista kontroli zamiast jednej wielkiej metody |

```python
# poza kanonem
# kreacyjny: klient nie wywołuje konstruktora
kalendarz = fabryka_kalendarzy("obcy")
# strukturalny: ten sam kontrakt, dodatkowa warstwa
kontrola = KontrolaPoniedzialku(KalendarzZCache(kalendarz))
# behawioralny: kontrole ustawiamy w kolejności, wniosek przechodzi przez nie
kontrole: list[Kontrola] = [kontrola, ...]
ok = all(k.sprawdz(wniosek) for k in kontrole)
```

Zauważ, że `KontrolaPoniedzialku` nie zmienia się w żadnym z trzech przypadków. Zmieniają się tylko okoliczności: skąd bierze kalendarz, w co ten kalendarz jest opakowany i w jakim towarzystwie kontrola pracuje.

Ta typologia pomaga szukać wzorca: gdy boli `new` rozsiane po kodzie, patrz na kreacyjne. Gdy boli sklejanie niezgodnych części, patrz na strukturalne. Gdy boli rozrastający się `if`, patrz na behawioralne. Do cofania decyzji, czyli zachowania, [wrócimy przy wzorcu Command](04%20Struktury%20wniosku.md#ref-10).

> **Pułapka: all() przerywa listę kontroli na pierwszej odmowie.** `all(k.sprawdz(wniosek) for k in kontrole)` jest leniwe: po pierwszym `False` kolejne kontrole w ogóle się nie wykonują. Kolejność ma więc znaczenie, a kontrola z efektem ubocznym (audyt, zbieranie powodów odmowy) lub kosztowna zależność może nie zostać uruchomiona. Gdy potrzeba pełnego raportu, trzeba najpierw zebrać wyniki wszystkich kontroli do listy.

## Wzorzec czy zwykła funkcja

Wzorzec jest potrzebny, gdy zmienna część kodu ma kilka wymiennych wariantów, a klient ma jej używać przez kontrakt, nie przez konkretną klasę. Jeśli jest jeden wariant, a operacja nie niesie stanu, wystarczy funkcja albo moduł.

```python
# poza kanonem
# wystarczy funkcja: jeden wariant, brak stanu
def rok_w_przyszlosci(rok: int, dzis: date) -> bool:
    return rok > dzis.year

# potrzebny kontrakt: warianty wymienia ten, kto składa obiekt
kontrole: list[Kontrola] = [KontrolaPoniedzialku(kalendarz), ...]
```

Pytaj o cztery rzeczy:

| Sygnał | Zwykła funkcja lub moduł | Wzorzec |
|---|---|---|
| Liczba wariantów | jeden, stały | co najmniej dwa, dochodzą kolejne |
| Kto wybiera wariant | autor kodu | klient albo konfiguracja, w czasie działania |
| Stan | brak, wynik zależy od argumentów | obiekt pamięta coś między wywołaniami |
| Rozrastający się `if` | nie ma | `if` po typie lub statusie rośnie z każdym przypadkiem |

[Sprawdzenie, czy rok pieczątki nie leży w przyszłości](#lm-2), to przykład z pierwszej kolumny. Nikt nie będzie go podmieniał, więc kontrakt tylko by utrudniał czytanie. [Kalendarze załączników to przykład z drugiej: obcych formatów przybywa](#lm-1), a urząd musi je obsłużyć bez zmian w kontroli.

Przyznanie poniedziałku też wymaga wzorca, bo urząd musi umieć tę decyzję cofnąć. Funkcja `przyznaj()` zrobi swoje i o niej zapomni, a cofnięcie potrzebuje obiektu, który pamięta, co zrobił. Takim wzorcem jest Command, czyli czynność opakowana w obiekt, i [wrócimy do niego przy zachowaniach](04%20Struktury%20wniosku.md#ref-11).

Nie sięgaj po wzorzec na zapas. Zacznij od funkcji i przejdź do wzorca dopiero wtedy, gdy zaczną się mnożyć warianty, stan albo `if`-y.

## Struktura pakietu i pierwszy test

[Kontrakty `Kalendarz` i `Kontrola`](#abc-czy-protocol) istnieją na razie tylko na papierze, więc czas dać im dom i sprawdzić, że działają. Pakiet `urzad` z katalogiem `tests/` obok i jedną linią konfiguracji wystarczy, by `pytest` w terminalu znalazł kod i testy.

```text
urzad-projekt/
├── pyproject.toml
├── urzad/
│   ├── __init__.py
│   └── kontrakty.py
└── tests/
    └── test_kontrola.py
```

pytest to narzędzie testowe uruchamiane z terminala. Szuka plików `test_*.py`, wykonuje funkcje `test_*` i traktuje zwykły `assert` jako sprawdzenie. Nie trzeba dziedziczyć po żadnej klasie.

Testy leżą poza pakietem, więc pytest musi wiedzieć, gdzie szukać `urzad`. Robi to `pythonpath = ["."]` w `pyproject.toml`, dzięki czemu `import urzad` działa bez instalowania pakietu.

Pierwszy test nie potrzebuje prawdziwego kalendarza. <a id="lm-7"></a>Podstawiamy atrapę, czyli prosty obiekt udający zależność ze stałą odpowiedzią. Dzięki typowaniu strukturalnemu `Protocol` przyjmie ją bez dziedziczenia:

```python
class KalendarzStaly:
    def poniedzialki(self, rok: int) -> list[date]:
        return [date(2024, 1, 1)]

def test_poniedzialek_z_kalendarza_przechodzi():
    kontrola = KontrolaPoniedzialku(KalendarzStaly())
    assert kontrola.sprawdz(date(2024, 1, 1)) is True
```

Kroki poniżej tworzą wszystkie pliki i uruchamiają test. Podmianę atrapy i sprawdzanie wywołań rozwiniemy w następnej sekcji.

_Wersje: pytest 8.x, Python 3.13 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-interfejsy-abc-i-protocol)_

## Atrapa z podglądem wywołań

Zależność podmieniasz, przekazując atrapę przez konstruktor, a wywołanie sprawdzasz na [mocku](00%20Glosariusz.md#mock): obiekcie z `unittest.mock`, który zapamiętuje, jak go użyto. `KalendarzStaly` z poprzedniej sekcji odpowiada tylko na pytania. Mock dodatkowo pozwala zapytać, czy i z czym go zawołano.

Wystarczy `Mock(spec=Kalendarz)`. Argument `spec` ogranicza obiekt do metod kontraktu, więc literówka w nazwie metody kończy się błędem zamiast po cichu przejść. Wartość zwracaną ustawiasz przez `return_value`:

<a id="ref-15"></a>

```python
def test_kontrola_pyta_kalendarz_o_rok_wniosku():
    kalendarz = Mock(spec=Kalendarz)
    kalendarz.poniedzialki.return_value = [date(2024, 1, 1)]

    kontrola = KontrolaPoniedzialku(kalendarz)

    assert kontrola.sprawdz(date(2024, 1, 1)) is True
    <a id="lm-8"></a>kalendarz.poniedzialki.assert_called_once_with(2024)
```

Zwykły `assert` sprawdza wynik, a `assert_called_once_with` sprawdza współpracę: kontrola zapytała dokładnie raz i o rok 2024. Przy błędzie pytest pokaże faktyczne wywołania.

Konstruktor przyjmujący `Kalendarz` sam jest miejscem podmiany. Dlatego nie potrzebujemy tu `monkeypatch`, który podmienia atrybuty istniejących obiektów i modułów, gdy zależność jest wpisana na sztywno.

Sprawdzaj wywołania tylko tam, gdzie wywołanie jest sednem zachowania. Gdy liczy się wynik, wystarczy prosta atrapa ze stałą odpowiedzią.

_Wersje: Python 3.13, pytest 8.x · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-interfejsy-abc-i-protocol)_

## Koszt podwójnej dyspozycji

Podwójna dyspozycja to wybór kodu według typów dwóch obiektów naraz. Zwykłe wywołanie `a.f(b)` wybiera implementację tylko po typie odbiorcy `a`, a Python nie przeciąża metod po typie argumentu `b`. Drugi typ trzeba więc rozpoznać ręcznie przez `isinstance` albo zamienić role w drugim wywołaniu.

Rozwiązanie to dwa wywołania. Element woła na obiekcie odwiedzającym, czyli na `Wizytator`, metodę nazwaną od swojego typu i przekazuje siebie:

```python
class Wniosek:
    def przyjmij(self, w: Wizytator) -> None:
        w.odwiedz_wniosek(self)   # 1. typ elementu wybiera nazwę metody

class Teczka:
    def przyjmij(self, w: Wizytator) -> None:
        w.odwiedz_teczke(self)    # 2. typ wizytatora wybiera kod
```

[Pierwsza dyspozycja (`przyjmij`) wybiera się po typie elementu](#lm-4), druga (`odwiedz_...`) po typie wizytatora. Nikt nie pyta o typ jawnie. To podstawa wzorca Visitor.

### Koszt: asymetria rozszerzania

Te dwa wywołania nie są za darmo. Zamiast `isinstance` w jednym miejscu masz w kontrakcie `Wizytator` metodę dla każdego typu elementu, który sam woła `przyjmij` po swojemu.

| Zmiana | Skutek |
|---|---|
| nowy wizytator (np. kolejny raport) | jedna nowa klasa, nic więcej się nie zmienia |
| nowy element z własnym `przyjmij` (np. `Segregator` wołający `w.odwiedz_segregator(self)`) | nowa metoda w kontrakcie i w **każdym** wizytatorze |

`WniosekPilny` dziedziczy `przyjmij` po `Wniosek`, więc trafia do `odwiedz_wniosek` bez zmian. Własnej metody, np. `odwiedz_wniosek_pilny`, wymaga dopiero wtedy, gdy nadpisze `przyjmij`.

Dopóki zbiór typów jest stabilny, a przybywają operacje, układ się opłaca. Gdy przybywają typy, koszt rośnie z liczbą wizytatorów. Wtedy prostszy bywa `match` po typie w jednej funkcji.

> **Pułapka: Podklasa po cichu odwiedzana jako klasa bazowa.** `WniosekPilny` dziedziczy `przyjmij`, więc każdy wizytator dostaje go w `odwiedz_wniosek` jako zwykły `Wniosek`. Żaden błąd ani ostrzeżenie nie pojawia się, a logika dla pilnych wniosków po cichu nie działa. Trzeba nadpisać `przyjmij` w każdej podklasie, której wizytatorzy mają rozróżniać, i dodać `odwiedz_wniosek_pilny` do kontraktu.

## Uruchamianie pytest w terminalu

[Kontrakty i atrapy](#abc-czy-protocol) z poprzednich sekcji zostają na papierze, dopóki nie mamy gdzie ich sprawdzić. Zbudujmy więc projekt, w którym każdy kolejny wzorzec dostanie swój test.

Układ jest płaski: w katalogu `urzad-projekt/` leży `pyproject.toml`, pakiet `urzad/` (z `__init__.py` i `kontrakty.py`) oraz `tests/` z plikiem `test_kontrola.py`. Testy nie należą do pakietu, więc pytest, czyli narzędzie do znajdowania i uruchamiania testów, musi wiedzieć, gdzie szukać `urzad`. Załatwia to `pythonpath = ["."]` w sekcji `[tool.pytest.ini_options]`.

Pierwszy test podstawia atrapę kalendarza i woła tylko kontrakt: `sprawdz`.

```python
# tests/test_kontrola.py
class KalendarzStaly:
    def poniedzialki(self, rok: int) -> list[date]:
        return [date(2024, 1, 1)]

def test_poniedzialek_z_kalendarza_przechodzi():
    kontrola = KontrolaPoniedzialku(KalendarzStaly())
    wniosek = Wniosek(1, date(2024, 1, 1), Pieczatka(2024))
    assert kontrola.sprawdz(wniosek) is True
```

Teraz terminal. Środowisko wirtualne trzyma pytest osobno od systemowego Pythona, a `pyproject.toml` ma trzy linie.

```text
# pyproject.toml
[tool.pytest.ini_options]
pythonpath = ["."]

$ cd urzad-projekt
$ python -m venv .venv
$ source .venv/bin/activate
$ pip install pytest
$ pytest
============================= test session starts ==============================
platform linux -- Python 3.13.0, pytest-8.3.4, pluggy-1.5.0
rootdir: /home/ty/urzad-projekt
configfile: pyproject.toml
collected 1 item

tests/test_kontrola.py .                                                 [100%]

============================== 1 passed in 0.02s ===============================
```

Wersje i czas będą u Ciebie inne; liczy się `1 passed`. Pytest szuka plików `test_*.py` i funkcji `test_*`, a przy porażce pokaże wartości po obu stronach `assert`. Przy `collected 0 items` sprawdź najpierw nazwy.

_Wersje: Python 3.13, pytest 8.x · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-interfejsy-abc-i-protocol)_

## Co zapamiętać

- ABC wymusza dziedziczenie i daje wspólny kod, Protocol opisuje sam kształt i pasuje do obcych klas bez zmian.
- Wnioski różnią się ważnością pieczątki, kalendarzem załączników i stanem decyzji, więc urząd potrzebuje kontraktów, a nie jednej konkretnej klasy.
- Zmienną część obiektu wkładaj do środka jako składnik z kontraktem, a dziedziczenia używaj do wspólnego kodu.
- Python wybiera metodę po typie jednego obiektu, więc dwa typy naraz rozstrzygasz dwoma wywołaniami: element woła metodę kontrolera nazwaną od swojego typu.
- Kreacyjne zmieniają, jak obiekt powstaje, strukturalne, jak obiekty się łączą, a behawioralne, kto co robi w czasie działania.
- Zacznij od funkcji i sięgaj po wzorzec, gdy pojawiają się wymienne warianty wybierane przez klienta, stan między wywołaniami albo rosnący `if`.
- Pakiet z katalogiem tests obok i pythonpath w pyproject.toml wystarczą, by pytest uruchomił testy zwykłymi assertami.
- Podmieniaj zależność przez konstruktor, a wywołanie sprawdzaj na Mock(spec=Kontrakt) przez assert_called_once_with.
- Podwójna dyspozycja to dwa wywołania z zamienionymi rolami; łatwo dodać wizytatora, ale nowy typ elementu z własnym przyjmij zmienia wszystkie wizytatory.
- Środowisko wirtualne, pip install pytest i pytest z korzenia projektu uruchamiają test, o ile pyproject.toml ma pythonpath = ["."], a nazwy to test_*.py i test_*.

## Pytania sprawdzające

### 1. Kiedy wybrać ABC, a kiedy Protocol do zdefiniowania kontraktu?

<details>
<summary>Odpowiedź</summary>

ABC wybierz, gdy kontrakt ma wymuszać dziedziczenie i dostarczać wspólny kod; błąd zgłasza interpreter przy tworzeniu obiektu. Protocol wybierz, gdy liczy się tylko kształt metod i implementacje mają pozostać niezależne, także obce; zgodność sprawdza type checker. W urzędzie Kalendarz to Protocol (obce systemy), a Kontrola to ABC (nasz wspólny szkielet).

Zobacz: [sekcja „ABC czy Protocol”](#abc-czy-protocol).

</details>

### 2. Jak wygląda kilka konkretnych wniosków o zaginiony poniedziałek (z pieczątką, załącznikami z obcych kalendarzy, decyzją) i co w nich sprawia trudność?

<details>
<summary>Odpowiedź</summary>

Przykładowe wnioski to trzy przypadki: poprawny (pieczątka, załącznik w kalendarzu urzędu, decyzja przyznana), z pieczątką z przyszłości i załącznikiem w kalendarzu juliańskim oraz pusty, odrzucony. Trudność stanowi niejednorodność danych: nieważne pieczątki, niezgodne kalendarze załączników i brakująca albo cofalna decyzja.

Zobacz: [sekcja „Trzy wnioski o poniedziałek”](#trzy-wnioski-o-poniedziałek).

</details>

### 3. Dlaczego składanie obiektów bywa elastyczniejsze niż dziedziczenie? Podaj przykład z urzędu.

<details>
<summary>Odpowiedź</summary>

Składanie pozwala wybrać zmienną część w konstruktorze, w czasie działania, zamiast utrwalać ją w podklasie. Kontrola poniedziałku dostaje dowolny kalendarz spełniający Protocol, więc jedna klasa zastępuje rodzinę podklas. Dziedziczenie zostaje dla wspólnego kodu, a to, co się zmienia, wkłada się do środka jako składnik.

Zobacz: [sekcja „Składanie zamiast dziedziczenia”](#składanie-zamiast-dziedziczenia).

</details>

### 4. Na czym polega podwójna dyspozycja i czemu zwykłe wywołanie metody jej nie daje?

<details>
<summary>Odpowiedź</summary>

Podwójna dyspozycja to wybór kodu według typów dwóch obiektów naraz. Zwykłe wywołanie metody wybiera implementację tylko po typie odbiorcy, a Python nie przeciąża metod po typie argumentu, więc drugi typ trzeba by rozpoznawać przez isinstance. Rozwiązaniem są dwa wywołania z zamienionymi rolami: element woła na Wizytatorze metodę odpowiadającą jego typowi i przekazuje siebie. To podstawa wzorca Visitor, ale ma koszt: nowy typ elementu z własnym przyjmij wymaga nowej metody w każdym wizytatorze, podczas gdy nowy wizytator nie zmienia nic innego. Podklasa dziedzicząca przyjmij (jak WniosekPilny) tego nie wymusza.

Zobacz: [sekcja „Idea podwójnej dyspozycji”](#idea-podwójnej-dyspozycji), [sekcja „Koszt podwójnej dyspozycji”](#koszt-podwójnej-dyspozycji).

</details>

### 5. Co zmienia wzorzec kreacyjny, strukturalny i behawioralny? Uzasadnij na jednym przykładzie każdej rodziny.

<details>
<summary>Odpowiedź</summary>

Wzorzec kreacyjny zmienia sposób powstawania obiektów (klient nie zna konkretnej klasy), strukturalny zmienia sposób łączenia obiektów w większe całości przy zachowaniu interfejsu, a behawioralny zmienia podział obowiązków i przepływ w czasie działania. W urzędzie odpowiadają im: fabryka wybierająca kalendarz, cache owinięty wokół Kalendarza oraz lista kontroli, przez którą przechodzi wniosek. We wszystkich trzech przypadkach klasa KontrolaPoniedzialku pozostaje bez zmian.

Zobacz: [sekcja „Trzy rodziny wzorców”](#trzy-rodziny-wzorców).

</details>

### 6. Po czym poznać, że problem wymaga wzorca, a nie zwykłej funkcji lub modułu?

<details>
<summary>Odpowiedź</summary>

Wzorzec jest potrzebny, gdy istnieje kilka wymiennych wariantów, wybieranych przez klienta lub konfigurację w czasie działania, a obiekt niesie stan albo rośnie `if` po typie lub statusie. Przy jednym stałym wariancie bez stanu wystarczy funkcja lub moduł. Cofanie decyzji wymaga obiektu pamiętającego, co zrobił, więc tam wzorzec się opłaca.

Zobacz: [sekcja „Wzorzec czy zwykła funkcja”](#wzorzec-czy-zwykła-funkcja).

</details>

### 7. Jak zorganizować pakiet urzędu i uruchomić pierwszy test pytest z terminala?

<details>
<summary>Odpowiedź</summary>

Utwórz katalog projektu z pakietem `urzad` (`__init__.py`, `kontrakty.py`), katalogiem `tests/` i `pyproject.toml` z sekcją `[tool.pytest.ini_options]` i `pythonpath = ["."]`. W terminalu wykonaj `python -m venv .venv`, aktywuj środowisko (`source .venv/bin/activate`), zainstaluj pytest przez `pip install pytest` i uruchom `pytest` z korzenia projektu. Pytest znajdzie pliki `test_*.py` i funkcje `test_*`, a zwykły `assert` wystarczy jako sprawdzenie. Poprawny przebieg kończy się linią `1 passed`, a `collected 0 items` zwykle oznacza złe nazwy plików lub funkcji.

Zobacz: [sekcja „Struktura pakietu i pierwszy test”](#struktura-pakietu-i-pierwszy-test), [sekcja „Uruchamianie pytest w terminalu”](#uruchamianie-pytest-w-terminalu).

</details>

### 8. Jak w pytest podmienić zależność atrapą i sprawdzić wywołanie?

<details>
<summary>Odpowiedź</summary>

Zależność przekazujesz przez konstruktor, więc w teście wstawiasz w jej miejsce `Mock(spec=Kalendarz)` z ustawionym `return_value`. Po wywołaniu testowanego kodu sprawdzasz współpracę przez `assert_called_once_with`. Argument `spec` pilnuje, by atrapa miała tylko metody kontraktu. Gdy liczy się sam wynik, wystarcza prosta klasa ze stałą odpowiedzią.

Zobacz: [sekcja „Atrapa z podglądem wywołań”](#atrapa-z-podglądem-wywołań).

</details>
