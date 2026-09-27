# Tworzenie wniosków

Fabryki z działu 02 wybierają, jaki obiekt powstanie, ale nie mówią, jak złożyć kompletny, poprawny wniosek ani jak wpiąć go w otoczenie Urzędu Zaginionych Poniedziałków. Po tym dziale złożysz wniosek Builderem z walidacją, sklonujesz go Prototypem i opanujesz konfigurację-[Singleton](00%20Glosariusz.md#singleton). Sprowadzisz też obcy kalendarz do własnego interfejsu ([Adapter](00%20Glosariusz.md#adapter)), rozdzielisz powiadomienie od kanału ([Bridge](00%20Glosariusz.md#bridge)), potraktujesz wniosek i teczkę jednakowo ([Composite](00%20Glosariusz.md#composite)) i dodasz zachowanie obiektowym Decoratorem. Wzorce kreacyjne i strukturalne przeplatają się: najpierw powstaje obiekt, potem łączymy go z otoczeniem, aż z danych wejściowych wychodzi wniosek w teczce. Opieramy się na modelu z działu 02 i kontraktach z działu 01.

```text
dane --(fabryki)--> Builder / Prototype --tworzy--> wniosek
konfiguracja (Singleton) --ustawienia--> Builder

Wzorce strukturalne, osobne gałęzie:
obcy kalendarz --Adapter--> wspólny interfejs kalendarza
powiadomienie --Bridge--> kanał wysyłki
wniosek, teczka --Composite--> jednakowy interfejs
obiekt --Decorator--> obiekt z dodatkowym zachowaniem
```

**W tym dziale:**

- [Builder składa wniosek](#builder-składa-wniosek)
- [Prototype klonuje wniosek](#prototype-klonuje-wniosek)
- [Singleton jako konfiguracja urzędu](#singleton-jako-konfiguracja-urzędu)
- [Od danych do kompletnego wniosku](#od-danych-do-kompletnego-wniosku)
- [Adapter obcego kalendarza](#adapter-obcego-kalendarza)
- [Bridge powiadomienia i kanału](#bridge-powiadomienia-i-kanału)
- [Composite i teczka wniosków](#composite-i-teczka-wniosków)
- [Decorator obiektowy kontra funkcyjny](#decorator-obiektowy-kontra-funkcyjny)

## Builder składa wniosek

[Builder](00%20Glosariusz.md#builder) zbiera części obiektu w kolejnych wywołaniach, a dopiero `build()` tworzy gotowy wniosek i sprawdza, czy części do siebie pasują. Wniosek nigdy nie istnieje w połowie złożony.

Każdy krok ustawia jedno pole i zwraca `self`, więc wywołania da się łańcuchować. To [interfejs płynny](00%20Glosariusz.md#interfejs-płynny): zapis czyta się jak opis wniosku, a nie lista argumentów pozycyjnych. <a id="lm-19"></a>Cała walidacja mieszka w jednym miejscu, czyli w `build()`.

```python
class BudowniczyWniosku:
    def __init__(self):
        self._pola = {"numer": None, "poniedzialek": None, "pieczatka": None}
        self._powod = ""
    def numer(self, numer: int) -> Self:
        self._pola["numer"] = numer
        return self
    ...  # poniedzialek(), pieczatka() i pilny(powod) tak samo
    def build(self, rok_biezacy: int) -> Wniosek:
        brak = [n for n, v in self._pola.items() if v is None]
        if brak:
            raise ValueError(f"brak pól: {', '.join(brak)}")
        self._pola["pieczatka"].zweryfikuj(rok_biezacy)
        ...  # z powodem: WniosekPilny(**self._pola, powod=...), inaczej Wniosek
```

`build()` robi dwie kontrole. Najpierw wykrywa brakujące pola i wymienia je wszystkie naraz. Potem woła `zweryfikuj` z pieczątki, więc nieważna pieczątka kończy się `NiewaznaPieczatka` ([sekcja „Pieczątka z przyszłości”](02%20Model%20domeny%20wniosku.md#pieczątka-z-przyszłości)). Rok, jak wcześniej, przychodzi z zewnątrz, bo zegar ma zostać poza budowniczym.

Wywołanie: `BudowniczyWniosku().numer(7).poniedzialek(date(2024, 3, 4)).pieczatka(Pieczatka(2024)).pilny("termin").build(2025)` zwraca `WniosekPilny`. Bez `pilny` dostajemy zwykły `Wniosek`.

Builder zwalnia z długiej listy argumentów i ze stanów niepełnych, ale kosztuje dodatkową klasę. Przy trzech polach wystarczy funkcja fabryczna; opłaca się, gdy pól przybywa, część jest opcjonalna, a poprawność zależy od ich zestawu. Do zestawienia z fabrykami i danymi wejściowymi [wrócimy przy składaniu całego wniosku](#ref-45).

_Wersje: Python 3.13 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-tworzenie-wniosków)_

> **Pułapka: Builder wielokrotnego użytku przecieka stan.** `_pola` i `_powod` żyją w instancji, a `build()` ich nie zeruje. Ponowne użycie tego samego budowniczego dla kolejnego wniosku odziedziczy `pilny` i stare pola, więc powstanie `WniosekPilny` zamiast `Wniosek`. Twórz nowego budowniczego na każdy wniosek albo czyść stan w `build()`.

## Prototype klonuje wniosek

Klonuj, gdy gotowy obiekt jest bliższy celowi niż nowy zestaw argumentów, a budowanie od zera powtarzałoby długą konfigurację. To wzorzec [Prototype](00%20Glosariusz.md#prototype): nowy obiekt powstaje jako kopia istniejącego, a potem zmieniasz tylko to, co się różni. W Pythonie robi to moduł `copy`, bez własnej metody `clone()`.

Kopie są dwie. [Kopia płytka](00%20Glosariusz.md#kopia-płytka) (`copy.copy`) tworzy nowy obiekt, ale jego pola wskazują na te same obiekty co w oryginale. [Kopia głęboka](00%20Glosariusz.md#kopia-głęboka) (`copy.deepcopy`) kopiuje rekurencyjnie także zawartość pól. Różnicę widać dopiero przy polu mutowalnym, jak lista. [To ten sam mechanizm co płytkie zamrożenie w `frozen`](02%20Model%20domeny%20wniosku.md#lm-11): poziom, na którym coś działa, kończy się na pierwszym zagnieżdżeniu.

```python
# poza kanonem: wniosek z listą uwag
@dataclass
class WniosekZUwagami(Wniosek):
    uwagi: list[str] = field(default_factory=list)

w = WniosekZUwagami(1, date(2024, 3, 4), Pieczatka(2024))
plytka, gleboka = copy.copy(w), copy.deepcopy(w)
w.uwagi.append("pilne")
print(plytka.uwagi, gleboka.uwagi)
```

```text
['pilne'] []
```

<a id="lm-20"></a>Kopia płytka dzieli listę z oryginałem, więc zmiana w jednym wniosku psuje drugi. Głęboka jest niezależna, ale kosztuje czas i pamięć.

| Sposób | Kiedy |
|---|---|
| [Builder od zera](#lm-19) | dużo kroków, ważna walidacja w `build()` |
| `copy.copy` / `copy.replace` | pola same niezmienne, np. `Pieczatka` |
| `copy.deepcopy` | pola mutowalne, kopia ma żyć własnym życiem |

Od Pythona 3.13 `copy.replace(wniosek, numer=8)` robi płytką kopię z podmienionymi polami. Skoro `Pieczatka` jest zamrożona, dzielenie jej między klonami jest bezpieczne. Klon omija jednak `build()`, więc nie sprawdza pieczątki od nowa.

_Wersje: Python 3.13 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-tworzenie-wniosków)_

## Singleton jako konfiguracja urzędu

Jedną instancję zapewnia w Pythonie zwykle funkcja z `functools.cache`, a w testach izolujesz ją czyszczeniem cache'u i przekazywaniem konfiguracji jako argumentu. Singleton gwarantuje, że klasa ma jedną instancję z globalnym punktem dostępu. Klasyczna wersja z `__new__` jest w Pythonie zbędna: moduł sam jest singletonem, a <a id="lm-21"></a>funkcja z cache'em tworzy obiekt raz, przy pierwszym wywołaniu.

```python
@dataclass(frozen=True)
class Konfiguracja:
    rok_biezacy: int = 2024
    format_domyslny: str = "iso"

@cache
def konfiguracja() -> Konfiguracja:
    return Konfiguracja()

print(konfiguracja() is konfiguracja())
print(konfiguracja())
```

```text
True
Konfiguracja(rok_biezacy=2024, format_domyslny='iso')
```

Konfiguracja jest zamrożona, bo wspólny obiekt zmieniany przez każdego psułby wszystkich. [Pamiętaj o płytkości `frozen`](02%20Model%20domeny%20wniosku.md#lm-11): pole `list` nadal dałoby się zmienić, więc trzymaj tu wartości niezmienne.

Globalny stan to główny koszt: testy zaczynają na siebie wpływać. Dlatego kod domeny nie woła `konfiguracja()` sam, tylko dostaje wartości z zewnątrz. To [wstrzykiwanie zależności](00%20Glosariusz.md#wstrzykiwanie-zależności): obiekt dostaje to, czego potrzebuje, jako argument. Tak już robimy z bieżącym rokiem. Po funkcję sięga tylko brzeg aplikacji.

```python
@pytest.fixture(autouse=True)
def czysta_konfiguracja():
    konfiguracja.cache_clear()
    yield
    konfiguracja.cache_clear()

def test_zlozenie_z_wlasna_konfiguracja():
    konf = Konfiguracja(rok_biezacy=2030)
    w = zloz(Wniosek, 1, date(2024, 3, 4), Pieczatka(2024), konf.rok_biezacy)
    assert w.numer == 1
```

<a id="lm-22"></a>Test buduje własną `Konfiguracja` i nie dotyka singletona. Fixture czyści cache przed każdym testem i po nim, więc nic nie przecieka między testami.

_Wersje: Python 3.13, pytest 8.x · [źródła: 3](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-tworzenie-wniosków)_

## Od danych do kompletnego wniosku

<a id="ref-45"></a>Wniosek powstaje w jednej funkcji na brzegu aplikacji, a każdy wzorzec dostaje w niej jedną rolę: konfiguracja daje rok, fabryka dobiera parser daty, Builder składa i waliduje, Prototype powiela gotowy wzór. Wzorce się nie mieszają, bo każdy odpowiada na inne pytanie.

| Pytanie | Kto odpowiada |
|---|---|
| Jaki jest rok bieżący? | `konfiguracja()`, czytana tylko na brzegu |
| Jak czytać datę z załącznika? | `fabryka_dla(zalacznik)` |
| Czy dane są kompletne i ważne? | `build()` |
| Jak zrobić kolejny podobny wniosek? | klon sprawdzonego wzoru |

```text
dane (dict) -> konfiguracja() -> rok
            -> Zalacznik -> fabryka_dla -> parser -> data
            -> BudowniczyWniosku -> build(rok) -> wzór (Wniosek)
            -> replace(wzór, numer=...) -> kolejne wnioski
```

Funkcja dostaje `Konfiguracja` jako argument, więc test podaje własną, jak w sekcji o Singletonie. Singleton czyta dopiero kod wywołujący:

```python
def wniosek_z_danych(dane: dict, konf: Konfiguracja) -> Wniosek:
    zal = Zalacznik(**dane["zalacznik"])
    poniedzialek = fabryka_dla(zal).parser().parsuj(zal.data)
    b = BudowniczyWniosku().numer(dane["numer"])
    ...  # poniedziałek i pieczątka z danych
    if "powod" in dane:
        b = b.pilny(dane["powod"])
    return b.build(konf.rok_biezacy)

wzor = wniosek_z_danych(dane, konfiguracja())
kolejny = dataclasses.replace(wzor, numer=2)
```

[Walidacja nadal mieszka w jednym miejscu, w `build()`](#lm-19), więc zła pieczątka zatrzyma wniosek, zanim powstanie. Prototype wchodzi dopiero po tym: `replace` kopiuje pola wzoru i podmienia numer. Wystarcza, bo pieczątka jest zamrożona; przy polach mutowalnych sięgnij po `copy.deepcopy`. Klon omija walidację, więc wzór musi wcześniej przejść `build()`.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-tworzenie-wniosków)_

## Adapter obcego kalendarza

Wnioski już powstają poprawnie, więc czas na to, co z nimi robić dalej. Zaczynamy od kalendarzy, bo `KontrolaPoniedzialku` oczekuje obiektu z metodą `poniedzialki(rok)`, a kalendarze z zewnątrz mają inne API.

Adapter to cienka klasa, która przyjmuje obcy obiekt, sama spełnia nasz kontrakt i tłumaczy każde wywołanie na język obcego kodu. Obcego kodu nie ruszamy: nie możemy go edytować, a nawet gdybyśmy mogli, nie chcemy go wiązać z naszym pakietem.

Załóżmy, że biblioteka dostawcy daje klasę `KalendarzZewnetrzny` z metodą `dni(rok, dzien_tygodnia)`, która zwraca daty jako napisy ISO (0 to poniedziałek). Nasz [Protocol](00%20Glosariusz.md#protocol) `Kalendarz` wymaga `poniedzialki(rok) -> list[date]`. Adapter wypełnia tę różnicę:

```python
class AdapterKalendarza:
    def __init__(self, obcy: KalendarzZewnetrzny):
        self._obcy = obcy

    def poniedzialki(self, rok: int) -> list[date]:
        napisy = self._obcy.dni(rok, 0)
        return [date.fromisoformat(n) for n in napisy]

kontrola = KontrolaPoniedzialku(AdapterKalendarza(obcy))
```

<a id="lm-24"></a>Adapter nie dziedziczy po niczym, bo `Kalendarz` to Protocol: wystarczy pasujący kształt. Obcy obiekt trzyma [przez kompozycję](00%20Glosariusz.md#kompozycja), więc jedna klasa adaptera obsłuży każdą jego podklasę.

Kontrola nie wie, że po drugiej stronie stoi cudza biblioteka. [Test sprawdza tylko kontrakt](02%20Model%20domeny%20wniosku.md#test-przez-interfejs-nie-implementację): `AdapterKalendarza(obcy).poniedzialki(2024)[0] == date(2024, 1, 1)`. <a id="ref-25"></a>Zmiana dostawcy to nowy adapter, a nie poprawki w kontrolach. Adapter tłumaczy tylko interfejs, więc nie dodawaj do niego reguł urzędu.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-tworzenie-wniosków)_

## Bridge powiadomienia i kanału

Bridge to wzorzec, który wydziela jedną z dwóch niezależnie zmiennych osi do osobnej hierarchii i łączy ją z drugą przez referencję. <a id="ref-6"></a>Powiadomienie (co mówimy) trzyma kanał (którędy to wysyłamy), więc obie hierarchie rosną osobno.

Bez Bridge'a dziedziczenie mnoży klasy: `PowiadomienieEmail`, `PowiadomienieSms`, `PowiadomieniePilneEmail`, `PowiadomieniePilneSms` i tak dalej. Każdy nowy kanał wymaga wersji każdego rodzaju powiadomienia.

| Podejście | 2 rodzaje, 3 kanały | Dodanie kanału |
|---|---|---|
| Podklasa na parę | 6 klas | +1 klasa na rodzaj |
| Bridge | 2 + 3 = 5 klas | +1 klasa |

Kanał opisujemy Protocolem, a powiadomienie dostaje go przez konstruktor:

```python
class Kanal(Protocol):
    def wyslij(self, adresat: str, tresc: str) -> None: ...

class Powiadomienie:
    def __init__(self, kanal: Kanal):
        self._kanal = kanal

    def o_decyzji(self, decyzja: DecyzjaPodjeta, adresat: str) -> None:
        wynik = "przyznana" if decyzja.przyznana else "odrzucona"
        self._kanal.wyslij(adresat, f"Wniosek {decyzja.numer}: {wynik}")

class PowiadomieniePilne(Powiadomienie): ...   # inna treść, ten sam kanał
```

```text
Powiadomienie  --kanal-->  Kanal
   ^                          ^
PowiadomieniePilne     KanalEmail, KanalSms
```

[Różnica wobec adaptera z poprzedniej sekcji](#adapter-obcego-kalendarza): adapter dopasowuje gotowy, obcy interfejs po fakcie, a Bridge projektujemy z góry, żeby dwie osie zmian się nie splatały.

Powiadomienie o cofnięciu decyzji to tylko kolejna metoda abstrakcji, kanały zostają bez zmian. Test podstawia kanał-atrapę zapisujący wysłane treści i sprawdza wynik przez kontrakt.

## Composite i teczka wniosków

Composite pozwala traktować pojedynczy wniosek i teczkę jednakowo, bo oba spełniają ten sam kontrakt, a teczka wykonuje operację, przekazując ją swoim elementom. Klient woła jedną metodę i nie sprawdza, czy ma przed sobą liść, czy gałąź.

Kontrakt opisujemy Protocolem, więc `Wniosek` nie musi po niczym dziedziczyć. Dopisujemy mu jedną metodę, a `Teczka` trzyma składniki, wśród których mogą być inne teczki:

```python
class Skladnik(Protocol):
    def numery(self) -> list[int]: ...

class Wniosek:   # dataclass bez zmian, dopisujemy metodę
    def numery(self) -> list[int]:
        return [self.numer]

class Teczka:
    def __init__(self, nazwa: str):
        self._dzieci: list[Skladnik] = []
    def dodaj(self, skladnik: Skladnik) -> None: ...
    def numery(self) -> list[int]:
        return [n for d in self._dzieci for n in d.numery()]
```

Rekurencja robi całą robotę: <a id="lm-27"></a>teczka w teczce w teczce zwraca numery wszystkich wniosków w drzewie, a kod wołający wygląda tak samo dla jednego wniosku i dla całego archiwum.

### Gdzie dać `dodaj`

<a id="lm-28"></a>Metodę `dodaj` zostawiamy tylko w `Teczka`. Wersja „przezroczysta” (`dodaj` też we wniosku, rzucająca wyjątek) daje jednolitość, ale przenosi błędy na czas działania. Pilnuj też cykli: teczka dodana do samej siebie zapętli `numery()`.

Kolejne operacje na drzewie, czyli [przechodzenie po teczce](04%20Struktury%20wniosku.md#ref-61) i [dodawanie nowych operacji bez zmiany klas](05%20Przep%C5%82yw%20komisji.md#ref-62), omówimy przy Iteratorze i Visitorze.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-tworzenie-wniosków)_

## Decorator obiektowy kontra funkcyjny

[Decorator](00%20Glosariusz.md#decorator) GoF to obiekt, który opakowuje inny obiekt o tym samym kontrakcie i dodaje zachowanie przed wywołaniem albo po nim. Dekorator funkcji w Pythonie (`@cache`, `@wraps`) opakowuje jedną funkcję w momencie definicji. Różnica leży w tym, co opakowujemy i kiedy.

Weźmy `Kontrola`. Chcemy zapisywać w dzienniku wynik każdej kontroli, ale bez ruszania `KontrolaPoniedzialku`. <a id="lm-29"></a>Opakowanie jest kontrolą, która trzyma inną kontrolę przez kompozycję:

```python
class KontrolaZDziennikiem(Kontrola):
    def __init__(self, wewnetrzna: Kontrola, dziennik: list[str]):
        self._wewnetrzna = wewnetrzna
        self._dziennik = dziennik

    def sprawdz(self, wniosek: object) -> bool:
        wynik = self._wewnetrzna.sprawdz(wniosek)
        self._dziennik.append(f"{type(self._wewnetrzna).__name__}: {wynik}")
        return wynik
```

Klient nadal widzi `Kontrola`, więc opakowania da się zagnieżdżać: dziennik wokół licznika wokół `KontrolaPoniedzialku`. Kolejność składania wybieramy w czasie działania, np. z konfiguracji.

| | Decorator GoF | Dekorator funkcji |
|---|---|---|
| Opakowuje | obiekt z kontraktem (wiele metod) | jedną funkcję |
| Kiedy | dowolnie, przy składaniu obiektów | zwykle przy definicji |
| Stan | własny, per instancja | domknięcie albo atrybut funkcji |
| Kontrakt | ten sam typ (ABC/Protocol) | ta sama sygnatura |

Dekoratora funkcji użyj, gdy dodatek dotyczy jednej funkcji i jest stały. Obiektowy wybierz, gdy opakowujesz obiekt z kilkoma metodami, dekorator ma stan (tu `dziennik`) albo zestaw opakowań zmienia się między środowiskami. Cena: więcej klas i ślad wywołań przechodzący przez kilka warstw.

> **Pułapka: Dziennik przy zagnieżdżeniu loguje nazwę opakowania.** `type(self._wewnetrzna).__name__` zwraca klasę bezpośrednio opakowanego obiektu. Gdy dziennik stoi wokół licznika wokół `KontrolaPoniedzialku`, wpis brzmi np. `KontrolaZLicznikiem: True`, a nie nazwa właściwej kontroli. Ten sam problem dotyczy `isinstance` i `type()` na opakowanej kontroli. Rozwiązanie: dekorator wystawia nazwę (np. `nazwa` przekazywaną w dół łańcucha) albo loguje się jawną etykietę.

## Co zapamiętać

- Builder ustawia pola krok po kroku, a jedyne miejsce walidacji, build(), sprawdza kompletność i pieczątkę, zanim powstanie wniosek.
- Klonuj `copy.copy` przy polach niezmiennych, a `copy.deepcopy` przy mutowalnych, pamiętając, że klon omija walidację z `build()`.
- Singleton w Pythonie to funkcja z cache'em zwracająca zamrożoną konfigurację; w testach wstrzykuj własną Konfiguracja i czyść cache fixture'em.
- Wnioski składaj w jednej funkcji na brzegu: konfiguracja daje rok, fabryka parser, Builder waliduje, a klon powiela tylko wzór, który już przeszedł build().
- Adapter opakowuje obcy obiekt przez kompozycję i spełnia nasz Protocol, tłumacząc wywołania, więc klient nie zna cudzego API, a cudzy kod pozostaje nietknięty.
- Bridge zastępuje iloczyn podklas sumą: abstrakcja (powiadomienie) trzyma przez referencję implementację (kanał), więc obie osie zmieniają się niezależnie.
- Composite daje liściowi i kontenerowi wspólny kontrakt, a kontener realizuje operację rekurencyjnie przez swoje elementy.
- Decorator GoF to obiekt o tym samym kontrakcie co opakowywany, składany dowolnie w czasie działania; dekorator funkcji opakowuje jedną funkcję, zwykle przy definicji.

## Pytania sprawdzające

### 17. Jak Builder składa wniosek krok po kroku i waliduje go w build()?

<details>
<summary>Odpowiedź</summary>

Builder zbiera pola wniosku w kolejnych krokach, z których każdy zwraca self. Dopiero build() tworzy obiekt: sprawdza, czy nie brakuje pól, i woła zweryfikuj na pieczątce z rokiem podanym z zewnątrz. Zwraca Wniosek albo WniosekPilny, gdy ustawiono powód, więc wniosek nie istnieje w stanie niepełnym.

Zobacz: [sekcja „Builder składa wniosek”](#builder-składa-wniosek).

</details>

### 18. Kiedy klonowanie przez copy/deepcopy jest lepsze od budowania od zera i jaka jest różnica między kopią płytką a głęboką?

<details>
<summary>Odpowiedź</summary>

Klonowanie jest lepsze, gdy gotowy obiekt jest bliższy celowi niż nowy zestaw argumentów i budowanie od zera powtarzałoby długą konfigurację. Kopia płytka tworzy nowy obiekt, ale jego pola wskazują na te same obiekty co oryginał. Kopia głęboka kopiuje rekurencyjnie także zawartość pól, więc jest niezależna, lecz droższa. Różnica ma znaczenie przy polach mutowalnych, np. listach.

Zobacz: [sekcja „Prototype klonuje wniosek”](#prototype-klonuje-wniosek).

</details>

### 19. Jak zapewnić jedną instancję konfiguracji i jak ją izolować w testach?

<details>
<summary>Odpowiedź</summary>

W Pythonie jedną instancję konfiguracji daje funkcja z `functools.cache` (albo sam moduł), a konfiguracja powinna być zamrożonym dataclassem. Kod domeny dostaje wartości jako argumenty zamiast sięgać po globalny obiekt, więc test tworzy własną Konfiguracja. Dodatkowo fixture z `cache_clear()` zapobiega przeciekaniu stanu między testami.

Zobacz: [sekcja „Singleton jako konfiguracja urzędu”](#singleton-jako-konfiguracja-urzędu).

</details>

### 20. Jak połączyć fabryki, Builder, Prototype i konfigurację, by z danych wejściowych powstał kompletny wniosek?

<details>
<summary>Odpowiedź</summary>

Całość to jedna funkcja na brzegu aplikacji. Konfiguracja dostarcza rok bieżący, fabryka dobiera parser daty do formatu załącznika, Builder składa dane i waliduje je w build(), a Prototype powiela sprawdzony wzór przy serii podobnych wniosków. Każdy wzorzec ma osobną rolę, a domena dostaje wartości z zewnątrz zamiast sięgać po singleton.

Zobacz: [sekcja „Od danych do kompletnego wniosku”](#od-danych-do-kompletnego-wniosku).

</details>

### 21. Jak Adapter sprowadza obcy kalendarz do wspólnego interfejsu bez zmiany jego kodu?

<details>
<summary>Odpowiedź</summary>

Adapter to klasa, która trzyma obcy obiekt, sama spełnia nasz kontrakt (tu Protocol Kalendarz) i tłumaczy każde wywołanie poniedzialki(rok) na metodę oraz format danych obcego kodu. Obcego kodu nie zmieniamy, a klient, na przykład kontrola poniedziałku, widzi tylko wspólny interfejs. Zmiana dostawcy oznacza napisanie nowego adaptera, a nie poprawianie klientów.

Zobacz: [sekcja „Adapter obcego kalendarza”](#adapter-obcego-kalendarza).

</details>

### 22. Jak Bridge rozdziela abstrakcję powiadomienia od kanału wysyłki, by nie mnożyć podklas?

<details>
<summary>Odpowiedź</summary>

Bridge wydziela kanał wysyłki do osobnej hierarchii (Protocol) i wstrzykuje go do powiadomienia przez konstruktor. Rodzaje powiadomień i kanały rosną niezależnie: zamiast iloczynu klas (rodzaje × kanały) mamy ich sumę. Nowy kanał to jedna klasa, a nowy rodzaj powiadomienia nie wymaga zmian w kanałach.

Zobacz: [sekcja „Bridge powiadomienia i kanału”](#bridge-powiadomienia-i-kanału).

</details>

### 23. Jak Composite pozwala traktować pojedynczy wniosek i teczkę jednakowo?

<details>
<summary>Odpowiedź</summary>

Composite daje pojedynczemu wnioskowi i teczce ten sam kontrakt, np. metodę numery(). Teczka wykonuje operację, przekazując ją rekurencyjnie wszystkim składnikom, także innym teczkom. Klient woła jedną metodę i nie rozróżnia liścia od gałęzi.

Zobacz: [sekcja „Composite i teczka wniosków”](#composite-i-teczka-wniosków).

</details>

### 24. Czym obiektowy Decorator GoF różni się od dekoratora funkcji w Pythonie?

<details>
<summary>Odpowiedź</summary>

Obiektowy Decorator opakowuje obiekt o tym samym kontrakcie (ABC lub Protocol), więc można go zagnieżdżać i składać w czasie działania, także ze stanem. Dekorator funkcji opakowuje jedną funkcję, zwykle przy definicji. Pierwszego używamy przy obiektach z wieloma metodami lub stanem, drugiego przy prostym, stałym dodatku do jednej funkcji.

Zobacz: [sekcja „Decorator obiektowy kontra funkcyjny”](#decorator-obiektowy-kontra-funkcyjny).

</details>
