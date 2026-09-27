# Struktury wniosku

Masz już teczki, adaptery i dekoratory, ale klient wciąż musiałby znać każdy z tych elementów osobno; ten dział składa je w strukturę obsługiwaną przez jedno [okienko](00%20Glosariusz.md#fasada). Po lekturze ukryjesz złożoność za Fasadą, oszczędzisz pamięć na pieczątkach we Flyweightcie i ochronisz drogiego weryfikatora przez [Proxy](00%20Glosariusz.md#proxy). Potem opiszesz, co dzieje się z wnioskiem w czasie działania: łańcuchem kontroli, Commandem z cofaniem, regułami komisji w Interpreterze i iteracją po [teczce](00%20Glosariusz.md#teczka). Wzorce strukturalne dają kształt, a behawioralne wprowadzają w nim ruch, więc pytania idą na zmianę: raz budujemy układ, raz przepuszczamy przez niego wniosek.

```text
STRUKTURA (kształt)
klient -> Okienko (Fasada) -> teczki, adaptery
          Okienko -> Proxy -> weryfikator pieczątek
          teczki -> pieczątki (Flyweight, współdzielone)

RUCH WNIOSKU (zachowanie), wywoływany przez Okienko
Okienko -> łańcuch kontroli    (przekazuje dalej / zatrzymuje)
Okienko -> Command             (execute / undo)
Okienko -> Interpreter reguł   (ocena reguły komisji)
Okienko -> iterator po teczce  (przegląd wniosków)
```

**W tym dziale:**

- [Fasada jako okienko urzędu](#fasada-jako-okienko-urzędu)
- [Flyweight i pula pieczątek](#flyweight-i-pula-pieczątek)
- [Proxy jako strażnik weryfikatora](#proxy-jako-strażnik-weryfikatora)
- [Struktura wniosku przez okienko](#struktura-wniosku-przez-okienko)
- [Łańcuch kontroli wniosku](#łańcuch-kontroli-wniosku)
- [Command i cofanie decyzji](#command-i-cofanie-decyzji)
- [Interpreter reguł komisji](#interpreter-reguł-komisji)
- [Iterator po teczce](#iterator-po-teczce)

## Fasada jako okienko urzędu

Fasada to jeden prosty obiekt przed grupą współpracujących klas: klient woła kilka metod okienka i nie wie, że za nim działają konfiguracja, fabryka, Builder, [decyzja](00%20Glosariusz.md#decyzję) i powiadomienie. Ukrywa kolejność wywołań, składanie zależności i pośrednie typy. Nie zamyka podsystemu na siłę: kto go potrzebuje, nadal może sięgnąć po `Builder` czy `Decyzja` bezpośrednio.

Kilka wywołań, które klient musiałby znać, zamienia się w dwa:

```python
class Okienko:
    def __init__(self, konf: Konfiguracja, powiadomienie: Powiadomienie): ...

    def zloz(self, dane: dict) -> int:
        wniosek = wniosek_z_danych(dane, self._konf)
        self._wnioski[wniosek.numer] = wniosek
        return wniosek.numer

    def zdecyduj(self, numer, glosy, adresat) -> bool:
        wniosek = self._wnioski[numer]
        decyzja = Decyzja(numer, glosy, wniosek.status)
        ...  # zmiana statusu wniosku
        zdarzenie = DecyzjaPodjeta(numer, decyzja.przyznana, decyzja.poprzedni_status)
        self._powiadomienie.o_decyzji(zdarzenie, adresat)
        return decyzja.przyznana
```

Klient nie widzi `Builder`a, roku z `Konfiguracja` ani `DecyzjaPodjeta`. Dostaje numer i wynik. Zapisany `poprzedni_status` zostaje w zdarzeniu, więc decyzję da się później cofnąć, ale [samo cofanie omówimy przy Command](#ref-63).

### Czego fasada nie robi

<a id="lm-30"></a>Fasada **koordynuje**, nie **decyduje**. Reguła „przyznana” żyje w `Decyzja`, [walidacja w `build()`](03%20Tworzenie%20wniosk%C3%B3w.md#lm-19), a fasada tylko je wywołuje. Gdy w okienku pojawi się `if` o pieczątkach albo głosach, urząd ma nowy podsystem ukryty w fasadzie.

Druga pułapka to „boski obiekt”: fasada, przez którą przechodzi wszystko, rośnie w klasę na 40 metod. Trzymaj ją wąską, a wyjątki domenowe (np. `NiewaznaPieczatka`) przepuszczaj, zamiast je połykać.

> **Pułapka: Fasada trzyma stan i zdarzenie ginie.** `zdecyduj` zmienia status wniosku w słowniku `_wnioski` (stan w pamięci fasady) i tworzy `DecyzjaPodjeta` tylko lokalnie, przekazując je do `Powiadomienie`. Jeśli `o_decyzji` rzuci wyjątek po zmianie statusu, wniosek ma już nowy status, a klient nie dostaje wyniku ani zdarzenia. Zdarzenie z `poprzedni_status` nie jest nigdzie zachowane, więc obiecane cofnięcie nie ma na czym działać. Kolejność: najpierw powiadomienie albo trwały zapis zdarzenia w spójnej operacji.

## Flyweight i pula pieczątek

[Flyweight](00%20Glosariusz.md#flyweight) to współdzielony, niezmienny obiekt, który trzyma tylko to, co wspólne dla wielu użytkowników. Resztę dostaje z zewnątrz przy każdym wywołaniu. <a id="lm-31"></a>Tysiąc wniosków z pieczątką z 2023 roku nie potrzebuje tysiąca obiektów `Pieczatka`, wystarczy jeden.

### Co współdzielić, a co podawać

Kryterium jest proste: czy dana informacja jest taka sama dla wszystkich użytkowników obiektu?

| | [Stan wewnętrzny](00%20Glosariusz.md#stan-wewnętrzny) | [Stan zewnętrzny](00%20Glosariusz.md#stan-zewnętrzny) |
|---|---|---|
| Znaczenie | stan wewnętrzny: wspólny, niezmienny, mieszka w obiekcie | stan zewnętrzny: zależy od kontekstu, przychodzi z zewnątrz |
| U nas | `rok` pieczątki | `rok_biezacy` w `zweryfikuj(self, rok_biezacy)`, numer wniosku |
| Gdzie | w `Pieczatka` | w argumencie metody i w `Wniosek` |

`Pieczatka` nie zna roku bieżącego, bo dostaje go jako argument metody `zweryfikuj`. Dlatego jeden egzemplarz obsłuży każdy wniosek.

### Pula

Pula wydaje ten sam obiekt dla tego samego roku:

```python
class PulaPieczatek:
    def __init__(self):
        self._pieczatki: dict[int, Pieczatka] = {}

    def daj(self, rok: int) -> Pieczatka:
        if rok not in self._pieczatki:
            self._pieczatki[rok] = Pieczatka(rok)
        return self._pieczatki[rok]

    def __len__(self) -> int:
        return len(self._pieczatki)

pula = PulaPieczatek()
wnioski = [pula.daj(2023) for _ in range(1000)]
print(len(pula), wnioski[0] is wnioski[999])
```

```text
1 True
```

Współdzielenie jest bezpieczne tylko dlatego, że `Pieczatka` to dataclass z `frozen=True`: jej pól nie da się zmienić po utworzeniu. Przy mutowalnym obiekcie zmiana w jednym wniosku psułaby wszystkie inne, [jak w kopii płytkiej listy](03%20Tworzenie%20wniosk%C3%B3w.md#lm-20). Zysk widać dopiero przy wielu powtórzeniach: przy pieczątkach z dziesiątek różnych lat pula nic nie da. W Pythonie ten sam efekt da [funkcja z `@cache`](03%20Tworzenie%20wniosk%C3%B3w.md#lm-21), ale pula jako obiekt daje się wstrzyknąć i wyczyścić w teście. Do tożsamości (`is`) nie dopisuj logiki, bo o równości decyduje wartość.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-struktury-wniosku)_

## Proxy jako strażnik weryfikatora

Proxy to obiekt o tym samym kontrakcie co prawdziwy, który stoi przed nim i decyduje, czy, kiedy i ile razy go wywołać. Klient nie widzi różnicy, a drogi weryfikator pieczątek pracuje tylko wtedy, gdy naprawdę musi.

Kontraktem jest `Weryfikator`, [Protocol](00%20Glosariusz.md#protocol) z jedną metodą `weryfikuj(pieczatka, rok_biezacy)`. Zastępnik i prawdziwy weryfikator go spełniają, więc klient dostaje którykolwiek z nich.

### Trzy zadania zastępnika

| Rodzaj | Co robi | U nas |
|---|---|---|
| Leniwy | [tworzy prawdziwy obiekt dopiero przy pierwszym użyciu](00%20Glosariusz.md#leniwa-inicjalizacja) | weryfikator powstaje przy pierwszej weryfikacji |
| Cache | pamięta wynik dla tych samych argumentów | para (rok pieczątki, rok bieżący) |
| Ochronny | sprawdza uprawnienia przed wywołaniem | `PermissionError` dla nieuprawnionego |

```python
class ProxyWeryfikatora:
    def __init__(self, utworz: Callable[[], Weryfikator], uprawniony: bool = True):
        self._utworz, self._uprawniony = utworz, uprawniony
        self._prawdziwy: Weryfikator | None = None
        self._zweryfikowane: set[tuple[int, int]] = set()

    def weryfikuj(self, pieczatka: Pieczatka, rok_biezacy: int) -> None:
        if not self._uprawniony:
            raise PermissionError("brak uprawnień do weryfikacji")
        klucz = (pieczatka.rok, rok_biezacy)
        if klucz not in self._zweryfikowane:
            if self._prawdziwy is None:
                self._prawdziwy = self._utworz()
            self._prawdziwy.weryfikuj(pieczatka, rok_biezacy)
            self._zweryfikowane.add(klucz)
```

Do cache trafiają tylko udane weryfikacje. <a id="lm-33"></a>Wyjątek `NiewaznaPieczatka` przechodzi bez połykania i nic nie zapisuje, więc błąd nie zostaje utrwalony.

### Działanie

```python
class WeryfikatorPieczatek:
    utworzone = wywolania = 0
    def __init__(self):
        WeryfikatorPieczatek.utworzone += 1
    def weryfikuj(self, pieczatka, rok_biezacy):
        WeryfikatorPieczatek.wywolania += 1
        pieczatka.zweryfikuj(rok_biezacy)

proxy = ProxyWeryfikatora(WeryfikatorPieczatek)
p = Pieczatka(2023)
print(WeryfikatorPieczatek.utworzone)
for _ in range(3):
    proxy.weryfikuj(p, 2024)
print(WeryfikatorPieczatek.utworzone, WeryfikatorPieczatek.wywolania)
```

```text
0
1 1
```

Trzy weryfikacje dały jedno utworzenie i jedno prawdziwe wywołanie. Zastępnik przyjmuje wywoływalny obiekt tworzący weryfikator (tu sama klasa) zamiast gotowej instancji, bo inaczej leniwość byłaby pozorna.

Proxy wygląda jak [Decorator](00%20Glosariusz.md#decorator) [z sekcji o opakowaniu kontroli](03%20Tworzenie%20wniosk%C3%B3w.md#lm-29), ale różni się intencją: dekorator dodaje zachowanie, zastępnik kontroluje dostęp. Cache pieczątek jest też [bliski puli](#lm-31), lecz pula współdzieli obiekty, a zastępnik pamięta wyniki. Koszt to dodatkowy poziom pośredni i ryzyko nieaktualnego cache, gdy wynik zależy od czegoś spoza klucza.

> **Pułapka: Wyścig przy leniwym tworzeniu weryfikatora.** Sprawdzenie `self._prawdziwy is None` i przypisanie nie są atomowe. Przy współbieżnych pierwszych wywołaniach (wątki) powstaje kilka weryfikatorów, a licznik `utworzone` przestaje być równy 1. Zabezpiecz tworzenie blokadą albo utwórz weryfikator przed udostępnieniem zastępnika.

## Struktura wniosku przez okienko

Wzorce strukturalne składasz w jedną strukturę, dając klientowi jedno wejście: Fasada `Okienko` trzyma resztę i wywołuje ją w stałej kolejności. Klient podaje dane, a pod spodem pracują pula, proxy, adapter i teczka.

| Warstwa | Wzorzec | Rola w `zloz` |
|---|---|---|
| pieczątki | `PulaPieczatek` | jeden obiekt na rok |
| weryfikacja | `ProxyWeryfikatora` | leniwa, z cache |
| załączniki | `AdapterKalendarza` | obcy kalendarz spełnia `Kalendarz` |
| grupowanie | `Teczka` | wnioski pod wspólnym `numery()` |

Kolejność ma znaczenie: najpierw tanie sprawdzenia, na końcu zmiana stanu. <a id="lm-34"></a>Wniosek trafia do teczki dopiero wtedy, gdy pieczątka i wszystkie załączniki przeszły kontrole, więc błąd niczego nie zostawia w środku.

```python
class Okienko:
    def __init__(self, konf, powiadomienie):
        self._konf, self._pula = konf, PulaPieczatek()
        self._proxy = ProxyWeryfikatora(WeryfikatorPieczatek)
        self._kalendarz = AdapterKalendarza(KalendarzZewnetrzny())
        self.teczka = Teczka("wnioski")
    def zloz(self, dane: dict) -> int:
        p = self._pula.daj(dane["rok"])
        self._proxy.weryfikuj(p, self._konf.rok_biezacy)
        for z in dane.get("zalaczniki", ()):
            d = z.jako_date()
            if d not in self._kalendarz.poniedzialki(d.year):
                raise ValueError(f"{z.nazwa}: {d} to nie poniedziałek")
        self.teczka.dodaj(Wniosek(dane["numer"], dane["poniedzialek"], p))
        return dane["numer"]
```

```python
okienko = Okienko(Konfiguracja(), Powiadomienie(None))
z = Zalacznik("a.ics", "iso", "2023-01-02")
for n in (1, 2):
    okienko.zloz({"numer": n, "rok": 2023, "poniedzialek": date(2023, 1, 2), "zalaczniki": (z,)})
print(okienko.teczka.numery())
```

```text
[1, 2]
```

Zakładam tu, że obcy kalendarz zna poniedziałki 2023 roku. Dwa wnioski współdzielą jedną pieczątkę, a weryfikator powstał raz. [Fasada nadal tylko koordynuje](#lm-30): reguły siedzą w `Pieczatka`, adapterze i teczce, a [wyjątki przechodzą bez połykania](#lm-33). Koszt to zależności utworzone w konstruktorze; do testów lepiej je wstrzykiwać. Ta struktura jest też [gotowa pod cofanie decyzji, bo `Decyzja` pamięta `poprzedni_status`](00%20Glosariusz.md#decyzję).

## Łańcuch kontroli wniosku

Wniosek jest już złożony i leży w teczce, więc czas zająć się tym, kto i w jakiej kolejności go sprawdza. [Łańcuch odpowiedzialności](00%20Glosariusz.md#łańcuch-odpowiedzialności) to ciąg obiektów, z których każdy sam decyduje: zatrzymuje wniosek albo przekazuje go następnemu.

Każde ogniwo implementuje kontrakt `Kontrola` i trzyma referencję do następnego przez [kompozycję](00%20Glosariusz.md#kompozycja). Jeśli własne sprawdzenie nie przejdzie, ogniwo zwraca `False` i dalsze się nie wykonują. Jeśli przejdzie, oddaje wniosek dalej, a na końcu łańcucha wynikiem jest `True`.

```python
class Ogniwo(Kontrola):
    def __init__(self, nastepne: Kontrola | None = None): ...

    def sprawdz(self, wniosek) -> bool:
        if not self.ok(wniosek):
            return False
        return self._nastepne.sprawdz(wniosek) if self._nastepne else True

    @abstractmethod
    def ok(self, wniosek) -> bool: ...

class OgniwoNumeru(Ogniwo):
    def ok(self, wniosek) -> bool: return wniosek.numer > 0
```

Pętlę przekazywania pisze się raz w `Ogniwo`, a konkretne ogniwo mówi tylko, co sprawdza. Łańcuch składasz z zewnątrz, na przykład `OgniwoStatusu(OgniwoNumeru())`, gdzie `OgniwoStatusu` wymaga statusu `"zlozony"`. Wniosek o numerze 0 albo ze statusem `"odrzucony"` zatrzyma się na pierwszym ogniwie, które go odrzuci.

Wygląda podobnie do [opakowania z `KontrolaZDziennikiem`](03%20Tworzenie%20wniosk%C3%B3w.md#lm-29), ale Decorator zawsze woła wewnętrzną kontrolę i dokłada zachowanie, a ogniwo może przerwać przebieg. Koszt: kolejność ogniw jest częścią wyniku, a bez śladu trudno powiedzieć, które ogniwo odrzuciło wniosek. Każde ogniwo testujesz osobno, bez reszty łańcucha.

## Command i cofanie decyzji

[Command](00%20Glosariusz.md#command) to wzorzec, w którym <a id="ref-10"></a>czynność staje się obiektem z metodami `execute` i `undo`. Obiekt trzyma odbiorcę czynności i dane potrzebne do jej odwrócenia, więc wywołujący nie musi wiedzieć, co dokładnie się stało.

Dla urzędu odbiorcą jest `Wniosek`, a [dane do cofnięcia już mamy](00%20Glosariusz.md#decyzję). Decyzja niesie pole `poprzedni_status`, zapisane w chwili głosowania. Polecenie nie musi więc niczego zgadywać: <a id="ref-35"></a>`execute` ustawia nowy status, a <a id="ref-3"></a>`undo` wpisuje ten zapisany.

```python
class PoleceniaDecyzji:
    def __init__(self, wniosek: Wniosek, decyzja: Decyzja):
        self.cel, self.wynik = wniosek, decyzja

    def execute(self) -> None:
        self.cel.status = "przyznany" if self.wynik.przyznana else "odrzucony"

    def undo(self) -> None:
        self.cel.status = self.wynik.poprzedni_status

historia: list[PoleceniaDecyzji] = []
polecenie = PoleceniaDecyzji(wniosek, decyzja)
polecenie.execute()
historia.append(polecenie)
historia.pop().undo()
```

Cały pomysł mieści się w ostatnich liniach: <a id="ref-11"></a>wykonane polecenia lądują na stosie, a cofnięcie zdejmuje ostatnie i woła `undo`. <a id="ref-63"></a>Cofanie kilku decyzji to kolejne `pop`, w odwrotnej kolejności do wykonania.

Koszt: `undo` jest tak dobre, jak zapisany stan. Tu wystarcza jedno pole, ale przy bogatszym wniosku trzeba by zapisać więcej, [do czego wrócimy przy zapisie i przywracaniu stanu](05%20Przep%C5%82yw%20komisji.md#ref-75). Powiadomienia o decyzji i o cofnięciu polecenie zostawia na zewnątrz, a jak to złożyć w całość, [pokażemy przy łączeniu Command z obserwatorami](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#ref-76).

> **Pułapka: Undo przywraca stan z głosowania, nie sprzed execute.** `undo` wpisuje `self.wynik.poprzedni_status`, zapisany w chwili głosowania, a nie status z momentu `execute`. Jeśli między głosowaniem a `execute` status `Wniosek` się zmienił (np. wykonano inne polecenie na tym samym wniosku), cofnięcie przywróci nieaktualną wartość i złamie odwrotną kolejność stosu. Stan do cofnięcia należy zapisywać w `execute`, z bieżącego `self.cel.status`.

## Interpreter reguł komisji

[Interpreter](00%20Glosariusz.md#interpreter) zapisuje regułę jako drzewo obiektów, z których każdy umie się sam „obliczyć” dla danych wejściowych. Sięgaj po niego, gdy reguły składa się z małych klocków i często zmienia; przy jednej stałej regule wystarczy funkcja.

Regułę komisji, np. „co najmniej dwa [głosy](00%20Glosariusz.md#głos-komisji) za i nie jednomyślnie”, budujemy z [drzewa wyrażeń](00%20Glosariusz.md#drzewo-wyrażeń): liście to proste testy, węzły łączą je operatorami. To [ta sama rekurencja co w teczce](03%20Tworzenie%20wniosk%C3%B3w.md#lm-27): węzeł woła `wartosc` na dzieciach. Wejściem są głosy z decyzji.

```python
@dataclass(frozen=True)
class Wiekszosc:
    prog: int
    def wartosc(self, glosy: tuple[Glos, ...]) -> bool:
        return sum(g.za for g in glosy) >= self.prog

class Jednomyslnosc:
    def wartosc(self, glosy: tuple[Glos, ...]) -> bool:
        return all(g.za for g in glosy)

# Oraz(lewa, prawa) i Nie(regula) działają analogicznie
regula = Oraz(Wiekszosc(2), Nie(Jednomyslnosc()))
regula.wartosc(decyzja.glosy)
```

`Regula` to `Protocol` z jedną metodą, więc nowy węzeł nie dziedziczy po niczym. <a id="lm-36"></a>Węzły `Oraz` i `Nie` łączą dowolne reguły, a `Jednomyslnosc` nie zależy od rozmiaru komisji. Drzewo jest niezmienne, można je współdzielić i testować po kawałku.

### Kiedy prościej

| Sytuacja | Wybór |
|---|---|
| jedna reguła, zmieniana razem z kodem | zwykła funkcja |
| reguły składane z klocków w kodzie | drzewo wyrażeń |
| reguły w pliku lub od użytkownika | parser tekstu budujący drzewo |

Nigdy nie interpretuj tekstu reguły przez `eval`: wykona dowolny kod. Mały parser zwraca to samo drzewo, a przyjmuje tylko znane słowa. Koszt wzorca to klasa na każdy rodzaj węzła, więc opłaca się dopiero przy wielu regułach.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-struktury-wniosku)_

## Iterator po teczce

[Iterator](00%20Glosariusz.md#iterator) to obiekt, który podaje elementy kolekcji po jednym i ukrywa jej wewnętrzną budowę. W Pythonie zwykle nie piszesz go ręcznie: wystarczy [generator](00%20Glosariusz.md#generator), czyli funkcja z `yield`, którą interpreter sam zamienia w iterator.

Klasyczny iterator GoF to osobna klasa z metodami `__iter__` i `__next__`. Dla płaskiej listy to proste, ale teczka jest drzewem: teczka w teczce w teczce. Ręczny iterator musiałby sam trzymać stos „gdzie jestem na każdym poziomie”, a generator trzyma ten stan w swoich ramkach wywołań.

```python
class Teczka:
    ...
    def __iter__(self) -> Iterator[int]:
        for skladnik in self._elementy:
            if isinstance(skladnik, Teczka):
                yield from skladnik
            else:
                yield from skladnik.numery()
```

`yield from` deleguje do podteczki, więc rekurencja działa tak samo jak przy [zwracaniu numerów z całego drzewa](03%20Tworzenie%20wniosk%C3%B3w.md#lm-27), tylko leniwie. Wnioski są liśćmi spełniającymi `Skladnik`, a `_elementy` to lista, [do której `dodaj` dopisuje składniki](03%20Tworzenie%20wniosk%C3%B3w.md#lm-28). Teraz <a id="ref-61"></a>`for numer in teczka` oraz `next(iter(teczka))` nie budują całej listy: znalezienie pierwszego pasującego wniosku przerywa przechodzenie od razu.

| Podejście | Kiedy |
|---|---|
| generator w `__iter__` | domyślnie, także dla drzew |
| klasa z `__next__` | gdy iterator ma mieć dodatkowe metody albo stan widoczny z zewnątrz |
| lista z `numery()` | gdy potrzebujesz całości i rozmiaru |

Pamiętaj o dwóch ograniczeniach. Generator jest jednorazowy, więc drugi przebieg wymaga nowego `iter(teczka)`, co `for` robi samo. Dodawanie do teczki w trakcie pętli daje nieprzewidywalny wynik, więc iteruj po stałej teczce albo po kopii.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-struktury-wniosku)_

## Co zapamiętać

- Fasada koordynuje podsystem i ukrywa jego kolejność wywołań oraz typy, ale nie decyduje: reguły zostają w klasach domenowych, a wyjątki przechodzą bez połykania.
- Flyweight współdzieli niezmienny stan wewnętrzny przez pulę, a stan zewnętrzny przekazuje się w argumentach, co oszczędza pamięć tylko przy wielu powtórzeniach.
- Proxy spełnia kontrakt prawdziwego obiektu i kontroluje dostęp: tworzy go leniwie, cache'uje udane wyniki i chroni wywołanie uprawnieniami.
- Fasada składa pulę, proxy, adapter i teczkę w jedną kolejność wywołań, a wniosek trafia do teczki dopiero po wszystkich kontrolach.
- W łańcuchu odpowiedzialności każde ogniwo samo decyduje, czy zatrzymać wniosek, czy oddać go następnemu, a kolejność ogniw wpływa na wynik.
- Command opakowuje czynność jako obiekt z execute i undo, a stos wykonanych poleceń pozwala cofać w odwrotnej kolejności, o ile polecenie zapisało dość stanu.
- Interpreter przechowuje regułę jako drzewo węzłów obliczanych rekurencyjnie; przy jednej stałej regule wybierz funkcję, a tekst reguł zamieniaj na drzewo parserem, nigdy przez eval.
- W Pythonie iterator po drzewie teczek to zwykle generator w `__iter__` z `yield from`: leniwy, bez ręcznego stosu, ale jednorazowy.

## Pytania sprawdzające

### 25. Co ukrywa fasada urzędu przed klientem i czego nie powinna robić?

<details>
<summary>Odpowiedź</summary>

Fasada ukrywa przed klientem kolejność wywołań, składanie zależności (konfiguracja, fabryka, Builder) i pośrednie typy, takie jak Decyzja czy DecyzjaPodjeta. Klient dostaje kilka prostych metod: złóż i zdecyduj. Fasada ma tylko koordynować, więc nie wolno jej przejmować reguł domenowych, rosnąć w boski obiekt ani połykać wyjątków domenowych.

Zobacz: [sekcja „Fasada jako okienko urzędu”](#fasada-jako-okienko-urzędu).

</details>

### 26. Jak Flyweight rozdziela stan wewnętrzny od zewnętrznego i oszczędza pamięć?

<details>
<summary>Odpowiedź</summary>

Flyweight dzieli obiekt na stan wewnętrzny, wspólny i niezmienny (rok pieczątki), oraz zewnętrzny, zależny od kontekstu (rok bieżący, numer wniosku). Pula wydaje ten sam egzemplarz dla tej samej wartości wewnętrznej, więc tysiąc wniosków dzieli jedną pieczątkę. Oszczędność wymaga niezmienności obiektu i wielu powtórzeń tych samych wartości.

Zobacz: [sekcja „Flyweight i pula pieczątek”](#flyweight-i-pula-pieczątek).

</details>

### 27. Jak Proxy kontroluje dostęp do drogiego weryfikatora pieczątek (cache, leniwość, ochrona)?

<details>
<summary>Odpowiedź</summary>

Proxy ma ten sam kontrakt co drogi weryfikator i stoi przed nim. Tworzy go leniwie, dopiero przy pierwszej weryfikacji, pamięta udane wyniki dla pary (rok pieczątki, rok bieżący) i odrzuca nieuprawnionych przez PermissionError przed jakimkolwiek kosztownym wywołaniem. Wyjątek o nieważnej pieczątce przechodzi bez zapisu w cache.

Zobacz: [sekcja „Proxy jako strażnik weryfikatora”](#proxy-jako-strażnik-weryfikatora).

</details>

### 28. Jak złożyć teczki, adaptery, pieczątki i fasadę w jedną strukturę, którą klient obsługuje przez okienko?

<details>
<summary>Odpowiedź</summary>

Składasz je za fasadą Okienko, która w konstruktorze trzyma pulę pieczątek, proxy weryfikatora, adapter kalendarza i teczkę. Metoda zloz wykonuje w stałej kolejności: pobiera pieczątkę z puli, weryfikuje ją przez proxy, sprawdza załączniki przez adapter i dopiero potem dodaje wniosek do teczki. Klient widzi jedno wywołanie, a reguły zostają w klasach domenowych.

Zobacz: [sekcja „Struktura wniosku przez okienko”](#struktura-wniosku-przez-okienko).

</details>

### 29. Jak łańcuch kontroli przekazuje wniosek dalej albo go zatrzymuje?

<details>
<summary>Odpowiedź</summary>

Każde ogniwo łańcucha wykonuje własne sprawdzenie. Jeśli ono nie przejdzie, zwraca False i dalsze ogniwa nie działają; jeśli przejdzie, przekazuje wniosek następnemu, a koniec łańcucha daje True. Pętlę przekazywania pisze się raz w klasie bazowej, a konkretne ogniwa definiują tylko, co sprawdzają.

Zobacz: [sekcja „Łańcuch kontroli wniosku”](#łańcuch-kontroli-wniosku).

</details>

### 30. Jak Command opakowuje czynność jako obiekt z execute i undo?

<details>
<summary>Odpowiedź</summary>

Command zamienia czynność w obiekt z metodami execute i undo, który trzyma odbiorcę oraz dane potrzebne do odwrócenia. W urzędzie polecenie decyzji ustawia status wniosku, a undo przywraca poprzedni_status zapisany w Decyzji. Wykonane polecenia trafiają na stos, więc cofanie idzie w odwrotnej kolejności.

Zobacz: [sekcja „Command i cofanie decyzji”](#command-i-cofanie-decyzji).

</details>

### 31. Jak drzewo wyrażeń interpretuje regułę komisji i kiedy lepszy jest zwykły eval-free parser lub funkcja?

<details>
<summary>Odpowiedź</summary>

Drzewo wyrażeń zapisuje regułę komisji jako obiekty-węzły: liście (większość, jednomyślność) i operatory (oraz, nie), a każdy węzeł oblicza się rekurencyjnie na głosach. Gdy reguła jest jedna i zmienia się razem z kodem, wystarczy zwykła funkcja. Gdy reguły przychodzą z pliku lub od użytkownika, mały parser tekstu buduje to samo drzewo, bez `eval`, który wykonałby dowolny kod.

Zobacz: [sekcja „Interpreter reguł komisji”](#interpreter-reguł-komisji).

</details>

### 32. Jak zaimplementować iterator po teczce i czemu w Pythonie zwykle wystarcza generator?

<details>
<summary>Odpowiedź</summary>

Iterator po teczce to obiekt podający numery wniosków po jednym; klasycznie jest to klasa z `__iter__` i `__next__`. W Pythonie wystarczy generator w `__iter__` z `yield from` dla podteczek, bo trzyma on stan przechodzenia po drzewie w ramkach wywołań i działa leniwie. Ręczną klasę pisz tylko wtedy, gdy iterator potrzebuje własnych metod albo widocznego stanu.

Zobacz: [sekcja „Iterator po teczce”](#iterator-po-teczce).

</details>
