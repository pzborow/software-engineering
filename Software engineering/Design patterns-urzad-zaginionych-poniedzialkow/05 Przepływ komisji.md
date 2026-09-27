# Przepływ komisji

Wniosek, który przeszedł kontrole z działu 04, musi jeszcze dojść do decyzji komisji, a tu kod zwykle zamienia się w splątane powiązania, łańcuchy `if` po statusie i procedury kopiowane między wariantami. Po tym dziale rozdzielisz odpowiedzialności między członków komisji, zapiszesz i przywrócisz [stan](00%20Glosariusz.md#state) wniosku, powiadomisz zainteresowanych o zdarzeniu, wymienisz reguły oraz dodasz operacje do teczek bez zmiany ich klas. Siedem wzorców behawioralnych, zbudowanych na modelu, kontrolach i regułach z poprzednich działów, złożysz w jeden przepływ prowadzący wniosek do decyzji.

```text
Przepływ wniosku (wzorce użyte na etapie):
wniosek --> kontrole --> stany --> głosowanie --> decyzja
            (dział 04)   State     Mediator,
                         Template  Strategy
                         Method

Wzorce przekrojowe (działają obok całego przepływu):
Observer - powiadamia subskrybentów o zdarzeniach na każdym etapie
Memento  - zapisuje i przywraca stan wniosku
Visitor  - dodaje operacje do teczek bez zmiany ich klas
```

**W tym dziale:**

- [Mediator w środku komisji](#mediator-w-środku-komisji)
- [Memento jako migawka wniosku](#memento-jako-migawka-wniosku)
- [Observer i subskrybenci zdarzeń](#observer-i-subskrybenci-zdarzeń)
- [State zamiast ifów po statusie](#state-zamiast-ifów-po-statusie)
- [Strategia jako funkcja albo klasa](#strategia-jako-funkcja-albo-klasa)
- [Template Method i szablon rozpatrzenia](#template-method-i-szablon-rozpatrzenia)
- [Visitor i raporty po teczkach](#visitor-i-raporty-po-teczkach)
- [Od kontroli do decyzji](#od-kontroli-do-decyzji)

## Mediator w środku komisji

[Mediator](00%20Glosariusz.md#mediator) to obiekt, przez który komunikują się równorzędni uczestnicy, więc żaden z nich nie zna pozostałych, tylko pośrednika. Członków komisji łączy wtedy N powiązań z mediatorem zamiast N·(N−1) powiązań każdy z każdym.

Bez mediatora członek, który zagłosował, musiałby sam powiadomić przewodniczącego, sekretarza i resztę, a dodanie nowego członka zmieniałoby wszystkich. Z mediatorem człowiek głosuje w jednym miejscu, a zliczanie i moment podjęcia decyzji należą do `Komisja`. To różni go od [fasady, która koordynuje, ale nie decyduje](04%20Struktury%20wniosku.md#lm-30): [fasada](00%20Glosariusz.md#fasada) upraszcza wejście do podsystemu z jednej strony, a mediator pośredniczy między obiektami na tym samym poziomie i trzyma ich wspólną regułę współpracy.

```python
class Komisja:
    def __init__(self, wniosek: Wniosek, liczba: int): ...
    def zglos(self, glos: Glos) -> Decyzja | None:
        self._glosy.append(glos)
        if len(self._glosy) < self._liczba:
            return None
        return Decyzja(self.wniosek.numer, tuple(self._glosy),
                       self.wniosek.status)

class CzlonekKomisji:
    def __init__(self, nazwa: str, komisja: Komisja): ...
    def glosuj(self, za: bool) -> Decyzja | None:
        return self._komisja.zglos(Glos(self.nazwa, za))
```

<a id="lm-38"></a>`CzlonekKomisji` nie ma referencji do innych członków, tylko do `Komisja`. Decyzja powstaje dopiero przy ostatnim głosie i niesie `poprzedni_status`, który później trzeba będzie umieć cofnąć.

Cena jest realna: mediator łatwo puchnie w „boski obiekt”, w którym siedzi cała logika. Trzymaj w nim wyłącznie koordynację, a reguły rozstrzygania zostaw w klasach domenowych, [na przykład w regułach komisji](04%20Struktury%20wniosku.md#lm-36). Test wystarczy oprzeć na dwóch członkach i jednym `zglos`, bez znajomości ich wnętrza.

> **Pułapka: Mediator zlicza głosy, nie członków.** `zglos` porównuje tylko `len(self._glosy)` z `_liczba`, więc ten sam `CzlonekKomisji` może zagłosować dwa razy i zamknąć głosowanie za nieobecnych. Każdy głos po osiągnięciu progu też zwraca kolejną `Decyzja`, bo warunek to `<`, a nie stan zamknięcia. Ponieważ członkowie nie znają siebie nawzajem, jedyną barierą jest mediator: trzeba w nim śledzić, kto już głosował, i pamiętać o zamknięciu głosowania.

## Memento jako migawka wniosku

[Memento](00%20Glosariusz.md#memento) zapisuje stan obiektu w nieprzejrzystej migawce, którą tylko ten sam obiekt umie odczytać i przywrócić. Reszta kodu może migawkę przechować i oddać, ale nie zajrzy do środka, więc enkapsulacja zostaje.

[W sekcji o cofaniu decyzji](04%20Struktury%20wniosku.md#command-i-cofanie-decyzji) `poprzedni_status` wystarczał, bo decyzja zmieniała jedno pole. <a id="ref-75"></a>Gdy zmienia się więcej (status, pieczątka, `powod` w `WniosekPilny`), Decyzja nie może nieść wszystkiego. Wtedy wniosek sam robi kopię całego stanu.

Role są trzy: autor (`Wniosek`) tworzy i przyjmuje migawki, [migawka](00%20Glosariusz.md#migawka) to niezmienny pojemnik na kopię stanu, a opiekun (np. lista lub stos) tylko je przechowuje.

```python
@dataclass(frozen=True)
class Migawka:
    _stan: dict = field(repr=False)

class Wniosek:
    ...
    def zapisz(self) -> Migawka:
        return Migawka(copy.deepcopy(vars(self)))
    def przywroc(self, migawka: Migawka) -> None:
        vars(self).update(copy.deepcopy(migawka._stan))
```

Python nie ma pól prywatnych, więc nieprzejrzystość to konwencja: podkreślnik i `repr=False` mówią „nie czytaj”, a `print(migawka)` pokazuje tylko `Migawka()`. Kopia głęboka jest potrzebna w obie strony. Zamrożenie jest płytkie, więc bez niej późniejsza zmiana wniosku zmieniłaby też zapisany stan.

Opiekun wygląda tak:

```text
zapisz()   Wniosek ──► Migawka ──► historia (lista)
przywroc() historia.pop() ──► Wniosek.przywroc(migawka)
```

Konsekwencja: każda migawka to pełna kopia, więc przy dużych wnioskach i długiej historii pamięć rośnie. Przy jednym polu do cofnięcia zostań przy `poprzedni_status`. Migawka ma sens, gdy stanu jest dużo albo zmienia go wiele operacji. Połączenie jej z poleceniami i powiadomieniami pokażemy [przy cofaniu decyzji z wysyłką powiadomień](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#ref-84).

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-przepływ-komisji)_

> **Pułapka: Migawka z vars(self) kopiuje też współpracowników.** `copy.deepcopy(vars(self))` obejmuje każde pole wniosku, także referencje do obiektów zewnętrznych, np. obserwatorów, mediatora czy dziennika. `przywroc` podmienia je wtedy na kopie, więc wniosek przestaje powiadamiać oryginalne obiekty, a zapis do dziennika trafia do duplikatu. Zapisuj tylko jawnie wybrane pola stanu albo wyłącz zależności z migawki.

## Observer i subskrybenci zdarzeń

[Observer](00%20Glosariusz.md#observer) pozwala jednemu obiektowi ogłaszać [zdarzenia domenowe](00%20Glosariusz.md#zdarzenie-domenowe), a wielu innym reagować na nie bez wiedzy nawzajem o sobie. Wycieku subskrypcji unikasz, oddając subskrybentowi sposób wypisania się albo trzymając go przez [słabą referencję](00%20Glosariusz.md#słaba-referencja), czyli odwołanie, które nie podtrzymuje życia obiektu.

Nadawca (`Publikator`) trzyma listę wywoływalnych obserwatorów. `Komisja` się nie zmienia: nadal zwraca `Decyzję` z `zglos`. Zdarzenie publikuje kod wołający, np. `Okienko.zdecyduj`, gdy dostanie `Decyzję`: buduje z niej `DecyzjaPodjeta` i woła `publikuj`. Powiadomienie, dziennik i statystyki nie znają się nawzajem, a komisja nie wie o żadnym z nich.

Wyciek bierze się stąd, że lista trzyma silne referencje. Obserwator, którego nikt już nie używa, żyje dalej, bo nadawca wciąż go woła, więc każde zdarzenie uruchamia martwy kod, a pamięć rośnie.

```python
class Publikator:
    def __init__(self):
        self._refy: list[weakref.WeakMethod] = []
    def subskrybuj(self, metoda) -> Callable[[], None]:
        ref = weakref.WeakMethod(metoda)
        self._refy.append(ref)
        return lambda: self._refy.remove(ref)
    def publikuj(self, zdarzenie: DecyzjaPodjeta) -> None:
        for ref in list(self._refy):
            if (m := ref()) is None: self._refy.remove(ref)
            else: m(zdarzenie)
```

<a id="lm-40"></a>Kopia listy w pętli jest celowa: obserwator może wypisać się w trakcie powiadamiania. `WeakMethod` jest potrzebny, bo zwykła słaba referencja do metody związanej umiera od razu, gdy znika tymczasowy obiekt metody. Dla zwykłych funkcji wystarczy `weakref.ref`.

| Sposób | Kto sprząta | Ryzyko |
|---|---|---|
| Uchwyt wypisania | obserwator, jawnie | zapomniane wywołanie |
| Słaba referencja | odśmiecacz | obserwator znika, gdy nikt go nie trzyma |

Wyjątek jednego obserwatora przerwie pętlę i pozostali nie dostaną zdarzenia, więc zdecyduj, czy go łapiesz. Połączenie Observera z poleceniami i migawkami pokażemy [przy decyzji, która wysyła powiadomienia i daje się cofnąć](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#ref-87).

_Wersje: Python 3.13 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-przepływ-komisji)_

> **Pułapka: Uchwyt wypisania rzuca ValueError przy ponownym użyciu.** `lambda: self._refy.remove(ref)` rzuci `ValueError`, jeśli `ref` już usunięto: przy drugim wywołaniu uchwytu albo gdy `publikuj` sprzątnęło wcześniej martwą referencję. Obie metody sprzątania (uchwyt i odśmiecacz) się na siebie nakładają, więc uchwyt powinien być idempotentny, np. sprawdzać `if ref in self._refy`.

## State zamiast ifów po statusie

State to wzorzec, w którym każdy status wniosku jest osobnym obiektem, a ten zna dozwolone przejścia z siebie i zastępuje łańcuch `if wniosek.status == ...`. Gdy stany różnią się tylko nazwą następnika, wystarczy `Enum` ze słownikiem przejść.

[Maszyna stanów](00%20Glosariusz.md#maszyna-stanów) to zbiór statusów i [reguł](00%20Glosariusz.md#interpreter) przejść między nimi. Bez wzorca każda operacja zaczyna się od `if`, a nowy status wymaga poprawek w wielu miejscach. Ze State każdy status to klasa z metodą `decyduj`, która zwraca następny stan albo zgłasza wyjątek dla przejścia niedozwolonego.

```python
class Stan(ABC):
    nazwa: str
    @abstractmethod
    def decyduj(self, przyznana: bool) -> "Stan": ...

class Zlozony(Stan):
    nazwa = "zlozony"
    def decyduj(self, przyznana):
        return Przyznany() if przyznana else Odrzucony()

class Odrzucony(Stan):  # Przyznany wygląda tak samo
    nazwa = "odrzucony"
    def decyduj(self, przyznana): raise ValueError("już rozstrzygnięty")

STANY = {k.nazwa: k for k in (Zlozony, Przyznany, Odrzucony)}
```

`Wniosek` nadal trzyma `status` jako napis, więc obiekt stanu bierzesz ze słownika `STANY`. Najpierw utwórz `Decyzję` z `poprzedni_status=wniosek.status`, bo jest zamrożona i dostaje to pole przy tworzeniu. Potem ustaw `wniosek.status = STANY[wniosek.status]().decyduj(decyzja.przyznana).nazwa`.

<a id="lm-41"></a>Ten sam graf w wersji z enumem zajmuje kilka linii:

```python
class Status(Enum):
    ZLOZONY = "zlozony"
    PRZYZNANY = "przyznany"
    ODRZUCONY = "odrzucony"

PRZEJSCIA = {(Status.ZLOZONY, True): Status.PRZYZNANY, (Status.ZLOZONY, False): Status.ODRZUCONY}
nowy = PRZEJSCIA[(Status(wniosek.status), przyznana)]  # KeyError, gdy już rozstrzygnięty
```

| Sytuacja | Wybór |
|---|---|
| Stany różnią się tylko dozwolonymi przejściami | `Enum` + słownik |
| Każdy stan ma własne zachowanie i dane | klasy `Stan` |
| Przejścia zależą od wielu warunków naraz | klasy `Stan` |

Słownik to dane, łatwe do wypisania i przetestowania. Klasy opłacają się, gdy stan ma własne zachowanie, np. inne kontrole.

> **Pułapka: Status jako napis rozjeżdża się ze stanem.** Stan istnieje tylko chwilowo: `STANY[wniosek.status]()` tworzy obiekt, a do `Wniosek` wraca sam napis `.nazwa`. Jeśli `decyduj` rzuci wyjątek po utworzeniu `Decyzji`, decyzja z `poprzedni_status` już powstała, a status się nie zmienił. Kolejność operacji nie jest atomowa, więc powstaje decyzja bez przejścia. Najpierw wywołaj `decyduj`, potem twórz `Decyzję`.

## Strategia jako funkcja albo klasa

[Strategy](00%20Glosariusz.md#strategy) to wymienny algorytm wybierany przez klienta. W Pythonie strategią jest zwykle zwykła funkcja przekazana jako argument. Klasę wybierz dopiero wtedy, gdy strategia ma własny stan, który trzeba odczytać z zewnątrz, albo więcej niż jedną operację.

Strategia głosowania to wywołanie `(glosy) -> bool`: dostaje krotkę `Glos` i mówi, czy wniosek przechodzi. Kontrakt ma jedno wywołanie, więc osobny interfejs z jedną metodą byłby ceremonią. [To ten sam kontrakt co `wartosc` w regule komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji), tylko bez drzewa: tam reguły się składały, tu wybieramy jedną z gotowych.

Funkcja `jednomyslnie` wystarcza, bo nie pamięta niczego między wywołaniami. Inaczej jest, gdy komisja chce wiedzieć, jak strategia się zachowywała: ile razy i z jakim wynikiem głosowała.

```python
from urzad.model import Glos
def jednomyslnie(glosy): return all(g.za for g in glosy)
class Kwalifikowana:
    def __init__(self, ulamek):
        self.ulamek, self.wyniki = ulamek, []
    def __call__(self, glosy):
        wynik = sum(g.za for g in glosy) >= self.ulamek * len(glosy)
        self.wyniki.append(wynik)
        return wynik

glosy = (Glos("Ada", True), Glos("Bo", True), Glos("Cy", False))
kw = Kwalifikowana(0.6)
for s in (jednomyslnie, kw, kw):
    print(s(glosy))
print(kw.ulamek, kw.wyniki)
```

```text
False
True
True
0.6 [True, True]
```

Closure też utrzyma listę wyników, ale tylko w zmiennej domknięcia: z zewnątrz jej nie odczytasz, a do licznika potrzebujesz `nonlocal`. Sam parametr (`ulamek`) to za mało na klasę, wystarczyłby `partial`. Klasa opłaca się przy stanie do inspekcji albo gdy strategię trzeba wypisać i porównać. Wciąż pasuje do klienta oczekującego funkcji, bo ma `__call__`.

| Strategia | Wybór |
|---|---|
| Jedno wywołanie, bez stanu | funkcja |
| Jeden parametr | closure lub `partial` |
| Stan do odczytu, kilka metod | klasa (`__call__` lub własne metody) |

W teście funkcję podmienisz lambdą, bez atrapy.

> **Pułapka: Strategia ze stanem współdzielona między komisje.** Instancja `Kwalifikowana` trzyma `wyniki` i ta sama `kw` użyta w kilku głosowaniach lub komisjach miesza historię. Lista rośnie bez końca i jest niebezpieczna przy współbieżnym użyciu. Twórz instancję na komisję albo resetuj stan.

## Template Method i szablon rozpatrzenia

[Template Method](00%20Glosariusz.md#template-method) ustala szkielet procedury w jednej metodzie klasy bazowej, a wybrane kroki oddaje podklasom. Kolejność kroków zostaje w bazie, podklasa zmienia tylko ich treść.

Rozpatrzenie wniosku ma stały przebieg: kontrola formalna, głosowanie, zapis statusu. Zmienia się reguła głosowania, a czasem kontrola. Szkielet trafia więc do klasy abstrakcyjnej, a krok, który musi się różnić, dostaje `@abstractmethod`. Krok z sensownym domyślnym działaniem to [hak](00%20Glosariusz.md#hak): zwykła metoda, którą podklasa może nadpisać, ale nie musi.

```python
class Rozpatrzenie(ABC):
    def rozpatrz(self, wniosek, glosy):      # metoda szablonowa
        if not self.kontrola(wniosek):
            return wniosek.status
        stan = Zlozony().decyduj(self.regula(glosy))
        wniosek.status = stan.nazwa
        return wniosek.status
    def kontrola(self, wniosek): return True  # hak
    @abstractmethod
    def regula(self, glosy): ...

class Jednomyslne(Rozpatrzenie):
    def regula(self, glosy): return all(g.za for g in glosy)
```

Klient woła `Jednomyslne().rozpatrz(wniosek, glosy)` i nie zna kroków. To baza woła podklasę, nie odwrotnie. Już to widziałeś w `Ogniwo` z łańcucha kontroli: `sprawdz` jest szablonem, a `ok` krokiem podklasy.

[Factory Method to szczególny przypadek tego wzorca](00%20Glosariusz.md#factory-method): `Rejestr.zloz` jest szablonem, a jedynym krokiem podklasy jest `utworz_wniosek`.

### Szablon czy strategia

| | Template Method | Strategy |
|---|---|---|
| Mechanizm | dziedziczenie | składanie |
| Zmiana wariantu | nowa podklasa | inny argument w czasie działania |
| Szkielet | zamrożony w bazie | w kliencie |

Jeśli zmienia się jeden krok, a szkielet jest stały, często wystarczy [funkcja jako strategia](#strategia-jako-funkcja-albo-klasa) przekazana do zwykłej funkcji. Szablon wybierz, gdy podklasy zmieniają kilka powiązanych kroków naraz albo gdy kolejność ma być gwarantowana. Nie nadpisuj w podklasie samej `rozpatrz`, bo zniszczysz tę gwarancję. Jak szablon, stany i głosowanie [łączą się w jeden przepływ](#ref-92), zobaczysz przy składaniu całej komisji.

> **Pułapka: Hak bez return po cichu blokuje głosowanie.** Baza sprawdza wynik `kontrola` przez `if not self.kontrola(wniosek)`. Podklasa, która nadpisze hak i zapomni o `return` na którejś ścieżce, zwraca `None`, więc szablon traktuje to jak odmowę. `rozpatrz` zwraca wtedy stary `wniosek.status`, nie zgłasza błędu i nie odróżnia „odrzucono kontrolę” od „jeszcze nie rozpatrzono”. Pilnuj tego testem każdej ścieżki nadpisanego haka albo wymuś `bool` zwracany z haka.

## Visitor i raporty po teczkach

[Visitor](00%20Glosariusz.md#visitor) to wzorzec, w którym <a id="ref-8"></a>operacja na strukturze trafia do osobnego obiektu, wizytatora, a klasy struktury dostają tylko jedną metodę `przyjmij`. <a id="ref-62"></a>Dodanie kolejnego raportu to nowa klasa wizytatora, bez ruszania `Wniosek` ani `Teczka`.

Mechanizm to [podwójna dyspozycja](00%20Glosariusz.md#podwójna-dyspozycja): element wybiera metodę wizytatora po własnym typie, wizytator po swoim. Liść wywołuje `odwiedz_wniosek`, a [teczka najpierw `odwiedz_teczke`](00%20Glosariusz.md#teczka), potem przekazuje wizytatora każdemu składnikowi. Rekurencję po drzewie niesie więc `przyjmij`, a nie wizytator.

Skoro `Teczka` woła `przyjmij` na składnikach, ta metoda staje się częścią kontraktu `Skladnik` obok `numery`. Dostają ją więc i `Wniosek`, i `Teczka`.

```python
class Wizytator(Protocol):
    def odwiedz_wniosek(self, wniosek: Wniosek) -> None: ...
    def odwiedz_teczke(self, teczka: Teczka) -> None: ...

class Teczka:
    def przyjmij(self, w: Wizytator) -> None:
        w.odwiedz_teczke(self)
        for s in self.skladniki:
            s.przyjmij(w)

class RaportStatusow:
    def __init__(self): self.liczniki = Counter()
    def odwiedz_wniosek(self, wniosek): self.liczniki[wniosek.status] += 1
    def odwiedz_teczke(self, teczka): pass
```

`Wniosek.przyjmij` to jedna linia: `w.odwiedz_wniosek(self)`. Klient pisze `raport = RaportStatusow(); teczka.przyjmij(raport)` i czyta `raport.liczniki`. Wizytator może trzymać stan, więc zbiera sumy w trakcie przejścia.

### Koszt i alternatywy

| | Nowa operacja | Nowy typ elementu |
|---|---|---|
| Metoda w klasach | zmiana każdej klasy | jedna nowa klasa |
| Visitor | jedna nowa klasa | zmiana każdego wizytatora |

Visitor opłaca się przy stabilnym zestawie klas i rosnącej liście operacji. Gdy wystarczy przejść po wnioskach, [prostszy jest `Iterator` po teczce](04%20Struktury%20wniosku.md#iterator-po-teczce) z zwykłą funkcją, bez `przyjmij`. Gdy chcesz uniknąć nawet `przyjmij`, `functools.singledispatch` wybiera funkcję po typie argumentu.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-przepływ-komisji)_

> **Pułapka: Wizytator liczy stan, którego nie da się użyć ponownie.** `RaportStatusow` trzyma `liczniki` w instancji, więc drugie `teczka.przyjmij(raport)` dolicza do starych wyników zamiast zacząć od zera. Dla każdego przejścia twórz nowego wizytatora albo dodaj reset.

## Od kontroli do decyzji

<a id="ref-92"></a>Wniosek dochodzi do decyzji, gdy jedna funkcja woła elementy w stałej kolejności: kontrola, migawka, głosowanie, reguła, stan, zdarzenie. Każdy wzorzec robi swoją część, a funkcja tylko je składa, podobnie jak fasada w okienku.

Kolejność ma znaczenie. [Łańcuch kontroli](00%20Glosariusz.md#łańcuch-odpowiedzialności) działa pierwszy, bo wniosek nie powinien trafić do komisji, jeśli nie przejdzie `OgniwoNumeru` i `OgniwoStatusu`. Potem migawka, bo zapisać trzeba stan sprzed zmiany. Dalej komisja zbiera głosy i przy ostatnim oddaje `Decyzja`, a drzewo reguł liczy z jej głosów, czy przyznać. Stan bieżącego statusu wylicza następny, a na końcu Publikator rozsyła `DecyzjaPodjeta`.

```python
STANY = {s.nazwa: s for s in (Zlozony(), Przyznany(), Odrzucony())}
def poprowadz(wniosek, glosy, kontrola, regula, publikator):
    if not glosy or not kontrola.sprawdz(wniosek):
        return None
    migawka = wniosek.zapisz()
    komisja = Komisja(wniosek, len(glosy))
    decyzja = [komisja.zglos(g) for g in glosy][-1]
    try:
        przyznana = regula.wartosc(decyzja.glosy)
        wniosek.status = STANY[wniosek.status].decyduj(przyznana).nazwa
    except Exception:
        wniosek.przywroc(migawka)
        raise
    publikator.publikuj(DecyzjaPodjeta(wniosek.numer, przyznana, decyzja.poprzedni_status))
    return decyzja, migawka
```

```text
kontrola -> zapisz -> Komisja.zglos -> regula -> Stan.decyduj -> publikuj
   |                                      |                        |
   stop: None            błąd: przywróć migawkę, wyjątek dalej     |
                                                 (decyzja, migawka)
```

<a id="lm-46"></a>Gdy reguła albo przejście rzuci wyjątek, wniosek wraca z migawki, a zdarzenia nie ma: obserwatorzy nie dowiedzą się o decyzji, która się nie udała. Funkcja zwraca `Decyzję`, z której `PoleceniaDecyzji` cofa przez `poprzedni_status`, oraz migawkę jako pełny zapis stanu. <a id="lm-47"></a>Reguły zostają w klasach domenowych, funkcja nie decyduje sama. [Powiadomienia i cofanie spinamy w następnej sekcji](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#ref-96).

> **Pułapka: Wyjątek obserwatora po zmianie statusu bez cofnięcia.** `publikuj` jest poza blokiem `try`, więc gdy któryś obserwator rzuci wyjątek, `wniosek.status` zostaje już zmieniony, a `migawka` nie jest przywrócona. Wywołujący widzi błąd, choć decyzja zapadła, a część obserwatorów mogła nie dostać `DecyzjaPodjeta`. Trzeba objąć publikację tą samą granicą błędu albo odizolować wyjątki obserwatorów w `Publikator`.

## Co zapamiętać

- Mediator zastępuje powiązania każdy z każdym powiązaniami z jednym pośrednikiem, ale ma tylko koordynować, a reguły zostają w klasach domenowych.
- Memento to niezmienna migawka pełnego stanu, tworzona i odczytywana tylko przez sam obiekt, a opiekun ją wyłącznie przechowuje; kopia głęboka chroni zapis, ale kosztuje pamięć.
- Observer rozsyła zdarzenie do wielu obserwatorów bez wiązania ich z nadawcą, a wyciek subskrypcji zapobiega uchwyt wypisania albo słaba referencja.
- State zastępuje if po statusie klasami z przejściami, ale gdy stany różnią się tylko grafem przejść, wystarczy Enum ze słownikiem.
- Strategią jest funkcja, dopóki nie potrzebujesz stanu dostępnego z zewnątrz albo kilku operacji; wtedy klasa z `__call__`.
- Template Method trzyma kolejność kroków w metodzie bazy, a podklasy nadpisują tylko kroki abstrakcyjne i haki; gdy zmienia się jeden krok, wystarczy strategia.
- Visitor dodaje operacje do struktury teczek przez jedną metodę `przyjmij` i podwójną dyspozycję, ale każdy nowy typ elementu wymaga zmiany wszystkich wizytatorów.
- Przepływ komisji to jedna funkcja składająca kontrolę, migawkę, komisję, regułę, stan i zdarzenie w stałej kolejności, z przywróceniem migawki przy błędzie.

## Pytania sprawdzające

### 33. Jak Mediator ogranicza bezpośrednie powiązania między członkami komisji?

<details>
<summary>Odpowiedź</summary>

Mediator jest jedynym obiektem, który zna wszystkich członków komisji, a oni znają tylko jego. Zamiast N·(N−1) powiązań każdy z każdym jest N powiązań z mediatorem. Głos trafia do Komisji, ona zlicza i decyduje o momencie podjęcia decyzji, więc dodanie członka nie zmienia pozostałych. Ryzykiem jest rozrost mediatora w boski obiekt, dlatego trzyma on tylko koordynację.

Zobacz: [sekcja „Mediator w środku komisji”](#mediator-w-środku-komisji).

</details>

### 34. Jak Memento zapisuje i przywraca stan wniosku bez łamania enkapsulacji?

<details>
<summary>Odpowiedź</summary>

Wniosek sam tworzy migawkę: niezmienny, nieprzejrzysty pojemnik z głęboką kopią swojego stanu, a sam też ją przyjmuje w przywroc. Opiekun (lista lub stos) tylko przechowuje migawki i nie zna ich wnętrza. W Pythonie nieprzejrzystość jest konwencją (podkreślnik, repr=False), a kopia głęboka chroni zapis przed późniejszymi zmianami wniosku.

Zobacz: [sekcja „Memento jako migawka wniosku”](#memento-jako-migawka-wniosku).

</details>

### 35. Jak Observer powiadamia subskrybentów o zdarzeniu i jak uniknąć wycieku subskrypcji?

<details>
<summary>Odpowiedź</summary>

Observer trzyma listę obserwatorów i przy zdarzeniu woła każdego z nich, przekazując to samo zdarzenie; nadawca nie zna konkretnych odbiorców. Wyciek subskrypcji powstaje, bo lista trzyma silne referencje do obserwatorów, którzy dawno przestali być potrzebni. Unikasz go, zwracając uchwyt wypisania przy subskrypcji albo trzymając obserwatorów przez słabe referencje (WeakMethod dla metod).

Zobacz: [sekcja „Observer i subskrybenci zdarzeń”](#observer-i-subskrybenci-zdarzeń).

</details>

### 36. Jak State usuwa łańcuchy if po statusie i kiedy wystarczy enum ze słownikiem przejść?

<details>
<summary>Odpowiedź</summary>

State zamienia łańcuch if po statusie na obiekty, z których każdy zna dozwolone przejścia z jednego statusu i zwraca następny stan albo zgłasza wyjątek. Wniosek może dalej trzymać status jako napis, a obiekt stanu znajdujesz słownikiem nazwa -> klasa. Gdy stany różnią się tylko dozwolonymi przejściami, wystarczy Enum ze słownikiem (status, przyznana) -> status, gdzie brak klucza oznacza przejście niedozwolone. Klasy wybierz, gdy stan ma własne zachowanie albo przejścia zależą od wielu warunków.

Zobacz: [sekcja „State zamiast ifów po statusie”](#state-zamiast-ifów-po-statusie).

</details>

### 37. Kiedy Strategy to klasa, a kiedy zwykła funkcja przekazana jako argument?

<details>
<summary>Odpowiedź</summary>

Strategia to zwykle funkcja przekazana jako argument, bo kontrakt ma jedno wywołanie i interfejs z jedną metodą to ceremonia. Sam parametr załatwia closure lub partial. Klasa opłaca się, gdy strategia ma stan, który trzeba odczytać z zewnątrz (np. historię wyników), albo gdy ma kilka operacji lub trzeba ją wypisać i porównać.

Zobacz: [sekcja „Strategia jako funkcja albo klasa”](#strategia-jako-funkcja-albo-klasa).

</details>

### 38. Jak Template Method ustala szkielet procedury i pozwala podklasom zmienić kroki?

<details>
<summary>Odpowiedź</summary>

Template Method umieszcza szkielet procedury w metodzie klasy bazowej, która wywołuje kroki w stałej kolejności. Kroki obowiązkowe są abstrakcyjne, opcjonalne to haki z domyślnym działaniem, a podklasy nadpisują tylko je. Dzięki temu kolejność jest gwarantowana przez bazę, a wariant to nowa podklasa. Gdy zmienia się jeden krok, prostsza bywa strategia.

Zobacz: [sekcja „Template Method i szablon rozpatrzenia”](#template-method-i-szablon-rozpatrzenia).

</details>

### 39. Jak Visitor dodaje operacje do struktury teczek bez zmiany jej klas?

<details>
<summary>Odpowiedź</summary>

Visitor przenosi operację ze struktury do osobnego obiektu-wizytatora. Klasy teczek dostają jedną metodę `przyjmij`, która przez podwójną dyspozycję wywołuje metodę wizytatora odpowiednią dla swojego typu, a teczka dodatkowo przekazuje wizytatora składnikom. Nowy raport to nowa klasa wizytatora, bez zmian w `Wniosek` i `Teczka`. Kosztem jest to, że nowy typ elementu wymusza zmianę wszystkich wizytatorów.

Zobacz: [sekcja „Visitor i raporty po teczkach”](#visitor-i-raporty-po-teczkach).

</details>

### 40. Jak połączyć kontrole, stany, głosowanie i reguły, by wniosek przeszedł do decyzji komisji?

<details>
<summary>Odpowiedź</summary>

Wniosek prowadzi jedna funkcja, która woła wzorce w stałej kolejności: łańcuch kontroli, migawka, komisja zbierająca głosy, reguła, stan, zdarzenie. Wzorce robią swoje, a funkcja tylko je składa i nie decyduje sama. Przy błędzie wniosek wraca z migawki i nie ma zdarzenia. Zwracana `Decyzja` pozwala później cofnąć decyzję.

Zobacz: [sekcja „Od kontroli do decyzji”](#od-kontroli-do-decyzji).

</details>
