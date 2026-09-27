# Ściągawka: Wzorce projektowe GoF w Pythonie: kreacyjne, strukturalne i behawioralne

Najważniejsze rzeczy z tutorialu na jednej stronie. Każda pozycja prowadzi do sekcji, która ją wyjaśnia.

## 01. Interfejsy ABC i Protocol

**Protocol zamiast ABC dla obcych klas**: ABC, gdy potrzebujesz wymuszonego dziedziczenia i wspólnego kodu; Protocol, gdy pasować mają klasy, których nie zmieniasz. → [ABC czy Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol)

```python
class Kalendarz(Protocol):
    def poniedzialki(self, rok: int) -> list[date]: ...
```

**Wzorzec czy zwykła funkcja**: Zacznij od funkcji; wzorzec dopiero przy wymiennych wariantach wybieranych przez klienta, stanie między wywołaniami lub rosnącym if. → [Wzorzec czy zwykła funkcja](01%20Interfejsy%20ABC%20i%20Protocol.md#wzorzec-czy-zwykła-funkcja)

**Mock z kontraktem i asercją wywołania**: Zależność podmieniaj przez konstruktor; spec= wyłapie wywołanie metody spoza kontraktu. → [Atrapa z podglądem wywołań](01%20Interfejsy%20ABC%20i%20Protocol.md#atrapa-z-podglądem-wywołań)

```python
kalendarz = Mock(spec=Kalendarz)
...
kalendarz.poniedzialki.assert_called_once_with(2024)
```

## 02. Model domeny wniosku

**Test tylko przez metody kontraktu**: Asertuj wynik lub wyjątek, nie prywatne pola (np. _kalendarz), inaczej test rozsypie się przy refaktorze. → [Test przez interfejs, nie implementację](02%20Model%20domeny%20wniosku.md#test-przez-interfejs-nie-implementację)

**Wartość jako frozen dataclass**: Zamrożenie jest płytkie: mutowalne pola w środku nadal można zmienić. → [Model wniosku jako dataclass](02%20Model%20domeny%20wniosku.md#model-wniosku-jako-dataclass)

```python
@dataclass(frozen=True)
class Pieczatka:
    rok: int
```

**Walidacja z bieżącym rokiem z zewnątrz**: Pieczątka z przyszłości to poprawna wartość; nieważność wykrywa metoda, a rok podajesz z zewnątrz (testowalność). → [Pieczątka z przyszłości](02%20Model%20domeny%20wniosku.md#pieczątka-z-przyszłości)

```python
def zweryfikuj(self, rok_biezacy: int) -> None:
    if self.rok > rok_biezacy:
        raise NiewaznaPieczatka(self, rok_biezacy)
```

**Data z formatem kalendarza obok**: Ten sam napis daty w różnych formatach to różne dni, więc zawsze noś nazwę formatu. → [Załącznik z obcego kalendarza](02%20Model%20domeny%20wniosku.md#załącznik-z-obcego-kalendarza)

```python
FORMATY = {"iso": "%Y-%m-%d", "us": "%m/%d/%Y", "eu": "%d/%m/%Y"}
...
return datetime.strptime(self.data, FORMATY[self.format]).date()
```

**Factory Method czy funkcja fabryczna**: Gdy wariant to tylko inna klasa, wystarczy funkcja; Factory Method, gdy podklasa zmienia też resztę przebiegu. → [Factory Method dla wniosków](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków)

```python
def zloz(klasa: type[Wniosek], numer, poniedzialek, pieczatka, rok_biezacy):
    pieczatka.zweryfikuj(rok_biezacy)
    return klasa(numer, poniedzialek, pieczatka)
```

**Abstract Factory: rodzina obiektów na format**: Jedna fabryka na format gwarantuje, że parser i walidator pochodzą z tego samego kalendarza. → [Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy)

```python
FABRYKI = {"iso": FabrykaIso(), "pl": FabrykaPolska()}

def fabryka_dla(zalacznik: Zalacznik) -> FabrykaKalendarza:
```

## 03. Tworzenie wniosków

**Builder z walidacją w build()**: build() to jedyne miejsce walidacji; metody krokowe zwracają Self, by dało się je łączyć w łańcuch. → [Builder składa wniosek](03%20Tworzenie%20wniosk%C3%B3w.md#builder-składa-wniosek)

```python
brak = [n for n, v in self._pola.items() if v is None]
if brak:
    raise ValueError(f"brak pól: {', '.join(brak)}")
```

**Prototype: copy czy deepcopy**: copy.copy przy polach niezmiennych, deepcopy przy mutowalnych; klon omija walidację z build(). → [Prototype klonuje wniosek](03%20Tworzenie%20wniosk%C3%B3w.md#prototype-klonuje-wniosek)

```python
plytka, gleboka = copy.copy(w), copy.deepcopy(w)
```

**Singleton jako funkcja z cache**: W testach wstrzykuj własną Konfiguracja i czyść cache przez konfiguracja.cache_clear() w fixture. → [Singleton jako konfiguracja urzędu](03%20Tworzenie%20wniosk%C3%B3w.md#singleton-jako-konfiguracja-urzędu)

```python
@cache
def konfiguracja() -> Konfiguracja:
    return Konfiguracja()
```

**Adapter obcego API przez kompozycję**: Adapter spełnia nasz Protocol i tłumaczy wywołania, a cudzy kod zostaje nietknięty. → [Adapter obcego kalendarza](03%20Tworzenie%20wniosk%C3%B3w.md#adapter-obcego-kalendarza)

```python
napisy = self._obcy.dni(rok, 0)
return [date.fromisoformat(n) for n in napisy]
```

**Bridge: abstrakcja trzyma implementację**: Zamienia iloczyn podklas (typ × kanał) na sumę; obie osie zmieniają się niezależnie. → [Bridge powiadomienia i kanału](03%20Tworzenie%20wniosk%C3%B3w.md#bridge-powiadomienia-i-kanału)

```python
class Powiadomienie:
    def __init__(self, kanal: Kanal):
        self._kanal = kanal
```

**Composite: rekurencja po dzieciach**: Liść i kontener dzielą kontrakt, więc klient nie rozróżnia pojedynczego wniosku od teczki. → [Composite i teczka wniosków](03%20Tworzenie%20wniosk%C3%B3w.md#composite-i-teczka-wniosków)

```python
def numery(self) -> list[int]:
    return [n for d in self._dzieci for n in d.numery()]
```

**Decorator GoF: ten sam kontrakt**: To obiekt składany w czasie działania, nie dekorator funkcji @ nakładany przy definicji. → [Decorator obiektowy kontra funkcyjny](03%20Tworzenie%20wniosk%C3%B3w.md#decorator-obiektowy-kontra-funkcyjny)

```python
class KontrolaZDziennikiem(Kontrola):
    def __init__(self, wewnetrzna: Kontrola, dziennik: list[str]):
```

## 04. Struktury wniosku

**Fasada: koordynuje, nie decyduje**: Reguły zostają w klasach domenowych, a wyjątki podsystemu przechodzą przez fasadę bez połykania. → [Fasada jako okienko urzędu](04%20Struktury%20wniosku.md#fasada-jako-okienko-urzędu)

```python
wniosek = wniosek_z_danych(dane, self._konf)
self._wnioski[wniosek.numer] = wniosek
return wniosek.numer
```

**Flyweight: pula współdzielonych wartości**: Współdziel tylko niezmienny stan wewnętrzny; sens ma dopiero przy wielu powtórzeniach. → [Flyweight i pula pieczątek](04%20Struktury%20wniosku.md#flyweight-i-pula-pieczątek)

```python
if rok not in self._pieczatki:
    self._pieczatki[rok] = Pieczatka(rok)
return self._pieczatki[rok]
```

**Proxy: leniwe tworzenie i cache wyników**: Proxy ma kontrakt prawdziwego obiektu; cache'uj tylko udane wyniki (wyjątek nie trafia do zbioru), uprawnienia sprawdzaj przed wywołaniem. → [Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora)

```python
if self._prawdziwy is None:
    self._prawdziwy = self._utworz()
self._prawdziwy.weryfikuj(pieczatka, rok_biezacy)
```

**Łańcuch odpowiedzialności: ogniwo decyduje**: Kolejność ogniw wpływa na wynik, więc ustawiaj ją świadomie. → [Łańcuch kontroli wniosku](04%20Struktury%20wniosku.md#łańcuch-kontroli-wniosku)

```python
if not self.ok(wniosek):
    return False
return self._nastepne.sprawdz(wniosek) if self._nastepne else True
```

**Command z execute i undo**: Cofanie w odwrotnej kolejności działa tylko, gdy polecenie zapisało dość stanu (np. poprzedni_status). → [Command i cofanie decyzji](04%20Struktury%20wniosku.md#command-i-cofanie-decyzji)

```python
historia.append(polecenie)
historia.pop().undo()
```

**Interpreter: reguły jako drzewo węzłów**: Tekst reguł zamieniaj na drzewo parserem, nigdy przez eval; przy jednej stałej regule wystarczy funkcja. → [Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji)

```python
regula = Oraz(Wiekszosc(2), Nie(Jednomyslnosc()))
regula.wartosc(decyzja.glosy)
```

**Iterator po drzewie: generator z yield from**: Leniwy i bez ręcznego stosu, ale jednorazowy. → [Iterator po teczce](04%20Struktury%20wniosku.md#iterator-po-teczce)

```python
if isinstance(skladnik, Teczka):
    yield from skladnik
```

## 05. Przepływ komisji

**Memento: migawka przez deepcopy**: Migawkę tworzy i czyta tylko sam obiekt, opiekun ją przechowuje; głęboka kopia chroni zapis, ale kosztuje pamięć. → [Memento jako migawka wniosku](05%20Przep%C5%82yw%20komisji.md#memento-jako-migawka-wniosku)

```python
return Migawka(copy.deepcopy(vars(self)))
...
vars(self).update(copy.deepcopy(migawka._stan))
```

**Observer ze słabą referencją i wypisaniem**: Uchwyt wypisania albo słaba referencja zapobiega wyciekowi subskrypcji. → [Observer i subskrybenci zdarzeń](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń)

```python
ref = weakref.WeakMethod(metoda)
self._refy.append(ref)
return lambda: self._refy.remove(ref)
```

**State jako Enum ze słownikiem przejść**: Gdy stany różnią się tylko grafem przejść, Enum wystarczy; klasy State dopiero przy różnym zachowaniu (KeyError = już rozstrzygnięty). → [State zamiast ifów po statusie](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie)

```python
PRZEJSCIA = {(Status.ZLOZONY, True): Status.PRZYZNANY, (Status.ZLOZONY, False): Status.ODRZUCONY}
nowy = PRZEJSCIA[(Status(wniosek.status), przyznana)]
```

**Strategy: funkcja, a klasa z `__call__` przy stanie**: Funkcja wystarcza, dopóki nie potrzebujesz stanu dostępnego z zewnątrz lub kilku operacji. → [Strategia jako funkcja albo klasa](05%20Przep%C5%82yw%20komisji.md#strategia-jako-funkcja-albo-klasa)

```python
def jednomyslnie(glosy): return all(g.za for g in glosy)
```

**Template Method: szkielet z hakiem**: Kolejność kroków w metodzie bazy, podklasy nadpisują tylko kroki; gdy zmienia się jeden krok, wystarczy strategia. → [Template Method i szablon rozpatrzenia](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia)

```python
def kontrola(self, wniosek): return True  # hak
@abstractmethod
def regula(self, glosy): ...
```

**Visitor: przyjmij i podwójna dyspozycja**: Łatwo dodać nową operację, ale każdy nowy typ elementu wymaga zmiany wszystkich wizytatorów. → [Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach)

```python
def przyjmij(self, w: Wizytator) -> None:
    w.odwiedz_teczke(self)
```

## 06. System Urzędu Zaginionych Poniedziałków

**Idiomy zamiast wzorców**: Zacznij od listy funkcji, Enuma ze słownikiem lub domknięcia; wzorzec dopiero przy wypisywaniu subskrybentów, zachowaniu stanów lub historii poleceń. → [Trzy wzorce i ich prostsze idiomy](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#trzy-wzorce-i-ich-prostsze-idiomy)

```python
_sluchacze: list[Callable] = []
for f in _sluchacze:
    f(zdarzenie)
```
