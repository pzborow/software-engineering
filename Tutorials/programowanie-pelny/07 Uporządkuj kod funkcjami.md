# Uporządkuj kod funkcjami

Gdy program rośnie, te same obliczenia zaczynają się powtarzać, a kod trudno przeczytać i poprawić. Ten dział pokazuje, jak zamknąć kawałek pracy w [funkcji](00%20Glosariusz.md#funkcja): nadać jej czytelną nazwę, przekazać dane i odebrać wynik. Po lekturze podzielisz program na małe, nazwane części i użyjesz ich wielokrotnie, tak jak w dziale 02 dzieliłeś problem na kroki, a pętle i listy z działu 06 zostaną w porządku. W przykładzie „Wspólnej Kasy” rozbijemy rozliczenie na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby. W warsztacie zbudujemy uproszczoną wersję: suma(wydatki) i na_osobe(suma, osoby), użyte dla dwóch różnych wyjazdów.

```text
                          osoby
                            │
                            ▼
wydatki ──► suma(wydatki) ──► suma ──► na_osobe(suma, osoby) ──► udział na osobę

Strzałka w funkcję: dane wchodzą. Strzałka z funkcji: wynik wychodzi.
```

**W tym dziale:**

- [Zdefiniuj i wywołaj funkcję](#zdefiniuj-i-wywołaj-funkcję)
- [Podziel program na funkcje](#podziel-program-na-funkcje)
- [Przekaż funkcji argumenty](#przekaż-funkcji-argumenty)
- [Odbierz wynik z funkcji](#odbierz-wynik-z-funkcji)
- [Nadawaj czytelne nazwy](#nadawaj-czytelne-nazwy)
- [Wykorzystaj kod ponownie](#wykorzystaj-kod-ponownie)

**Warsztat, punkt startowy:** pliki z końca działu 06: `kasa.py`, `nieskonczona.py` ([treść](99%20Warsztat.md#po-dziale-06)).

## Zdefiniuj i wywołaj funkcję

Funkcja to nazwany kawałek kodu, który raz opisujesz, a potem uruchamiasz, kiedy zechcesz, wpisując jego nazwę. Znasz już gotowe funkcje: `print()` i `str()` napisali twórcy Pythona.

Własną funkcję zaczynasz od `def`, nazwy, nawiasów i dwukropka. Wcięty blok pod spodem to jej treść. Ten zapis to [definicja funkcji](00%20Glosariusz.md#definicja-funkcji): tylko opisuje, co funkcja robi, i niczego jeszcze nie wykonuje. Dopiero [wywołanie](00%20Glosariusz.md#wywołanie-funkcji), czyli nazwa z nawiasami, uruchamia treść.

Weźmy pętlę zbierającą sumę, [taką jak w sekcji o pętli po elementach listy](06%20Powtarzaj%20i%20zbieraj%20dane.md#lm-44). <a id="ref-28"></a><a id="lm-45"></a>Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:

```python
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

print(suma([45.5, 20, 12.5]))
```

```text
78.0
```

Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. [Oba mechanizmy omówimy osobno w kolejnych sekcjach](#przekaż-funkcji-argumenty); na razie wystarczy, że dane wchodzą, a wynik wychodzi.

Konsekwencja: kod, który był kawałkiem długiego programu, ma teraz nazwę i można go wywołać w wielu miejscach, bez kopiowania.

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `funkcje.py`.** Tworzymy plik z definicją funkcji i jej wywołaniem.

```python
# funkcje.py - pierwsza funkcja Wspólnej Kasy
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

print(suma([45.5, 20, 12.5]))
```

**Krok 2. Uruchom.** Uruchamiamy program.

```bash
python funkcje.py
```

Wynik:

```text
78.0
```

## Podziel program na funkcje

Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach.

Zobacz to na „Wspólnej Kasie”. Funkcja `suma` już jest, więc dokładamy drugą, `na_osobe`, i używamy obu dla dwóch wyjazdów:

```python
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print("Mazury:", na_osobe(suma(mazury), 3))
print("Tatry:", na_osobe(suma(tatry), 4))
```

```text
Mazury: 26.0
Tatry: 112.5
```

Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz. Gdyby liczenie sumy trzeba było kiedyś zmienić, poprawiasz jedną funkcję, a oba wyniki będą poprawne.

Druga korzyść to czytelność: `na_osobe(suma(mazury), 3)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, [do czego wrócimy przy testowaniu programu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#ref-91).

U siebie masz już `funkcje.py` z funkcją `suma`.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `funkcje.py`.** Dopisujemy na_osobe i użycie funkcji dla dwóch wyjazdów.

```diff
-# funkcje.py - pierwsza funkcja Wspólnej Kasy
+# funkcje.py - funkcje Wspólnej Kasy
 def suma(wydatki):
…
 
-print(suma([45.5, 20, 12.5]))
+def na_osobe(suma, osoby):
+    return suma / osoby
+
+mazury = [45.5, 20, 12.5]
+tatry = [300, 150]
+print("Mazury:", na_osobe(suma(mazury), 3))
+print("Tatry:", na_osobe(suma(tatry), 4))
```

<details>
<summary>Cały plik <code>funkcje.py</code> po zmianie</summary>

```python
# funkcje.py - funkcje Wspólnej Kasy
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print("Mazury:", na_osobe(suma(mazury), 3))
print("Tatry:", na_osobe(suma(tatry), 4))
```

</details>

**Krok 2. Uruchom.** Uruchamiamy program.

```bash
python funkcje.py
```

Wynik:

```text
Mazury: 26.0
Tatry: 112.5
```

> **Pułapka: Parametr przesłania funkcję o tej samej nazwie.** W `na_osobe(suma, osoby)` nazwa `suma` oznacza liczbę, a nie funkcję `suma`, więc wewnątrz nie da się jej wywołać (błąd: liczba nie jest wywoływalna). Kod działa, bo ciało tego nie robi, ale to mylące. Nadaj parametrowi inną nazwę, np. `kwota_razem`.

## Przekaż funkcji argumenty

[Argumenty](00%20Glosariusz.md#argument-funkcji) to dane, które przekazujesz funkcji w nawiasach przy wywołaniu, żeby miała na czym pracować. Funkcja bez argumentów robi zawsze to samo, a z argumentami to samo działanie wykonuje na różnych danych.

W definicji funkcji nazwy w nawiasach to [parametry](00%20Glosariusz.md#parametr): puste miejsca, które funkcja wypełnia przy każdym wywołaniu. W `na_osobe(suma, osoby)` są dwa: `suma` i `osoby`. Wartości, które wpisujesz przy wywołaniu, to argumenty. Python przypisuje je parametrom [tak samo jak przy przypisaniu](00%20Glosariusz.md#przypisanie): pierwszy argument trafia do pierwszego parametru, drugi do drugiego.

```python
def na_osobe(suma, osoby):
    return suma / osoby

print(na_osobe(300, 4))
print(na_osobe(osoby=4, suma=300))
```

```text
75.0
75.0
```

Pierwsze wywołanie podaje argumenty według kolejności. Drugie podaje je z nazwą, więc kolejność nie gra roli, a zapis mówi wprost, co oznacza każda liczba.

Liczba argumentów musi zgadzać się z liczbą parametrów. Wywołanie `na_osobe(300)` kończy się komunikatem [`TypeError`](00%20Glosariusz.md#typeerror). To nazwa błędu, który Python zgłasza, gdy coś zrobiono w niewłaściwy sposób; tu znaczy: funkcję wywołano bez wartości dla `osoby`. [Czytanie takich komunikatów omówimy przy błędach](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#ref-94).

Kolejność też ma znaczenie: `na_osobe(4, 300)` <a id="lm-48"></a>da wynik bez błędu, ale zły, bo 4 zł podzielisz na 300 osób.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `funkcje.py`.** Dopisujemy wywołanie z jednym argumentem zamiast dwóch.

```diff
 print("Tatry:", na_osobe(suma(tatry), 4))
+print(na_osobe(300))
```

<details>
<summary>Cały plik <code>funkcje.py</code> po zmianie</summary>

```python
# funkcje.py - funkcje Wspólnej Kasy
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print("Mazury:", na_osobe(suma(mazury), 3))
print("Tatry:", na_osobe(suma(tatry), 4))
print(na_osobe(300))
```

</details>

**Krok 2. Uruchom.** Brakuje drugiego argumentu, więc Python zgłasza TypeError.

```bash
python funkcje.py
```

Zobaczysz błąd (celowy, poprawimy go):

```text
Mazury: 26.0
Tatry: 112.5
Traceback (most recent call last):
  File "funkcje.py", line 16, in <module>
    print(na_osobe(300))
          ~~~~~~~~^^^^^
TypeError: na_osobe() missing 1 required positional argument: 'osoby'
```

_Wersje: Python 3.13_

> **Z przymrużeniem oka:** Parametr to rubryka w formularzu, argument to to, co do niej wpiszesz. Formularz nie sprawdzi, czy w polu „imię” nie wylądowało nazwisko, a `na_osobe(4, 300)` też przyjmie wszystko bez mrugnięcia okiem.

## Odbierz wynik z funkcji

<a id="ref-89"></a>Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał. Ta oddana wartość to [wartość zwracana](00%20Glosariusz.md#wartość-zwracana): wywołanie funkcji staje się w kodzie właśnie nią, więc możesz ją zapisać do [zmiennej](00%20Glosariusz.md#zmienna) albo przekazać dalej.

Po `return` funkcja od razu kończy pracę. Nic, co stoi pod nim w ciele funkcji, już się nie wykona.

Zwracanie to nie to samo co wypisywanie. `print` tylko pokazuje tekst na ekranie, a program nie dostaje z niego nic do dalszej pracy. Funkcja bez `return` oddaje specjalną wartość [`None`](00%20Glosariusz.md#none), czyli „nic”.

```python
def na_osobe(suma, osoby):
    return suma / osoby

def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wynik = na_osobe(300, 4)
nic = wypisz_na_osobe(300, 4)
print(wynik)
print(nic)
```

```text
75.0
75.0
None
```

<a id="lm-49"></a>Pierwsza `75.0` pochodzi z `print` wewnątrz `wypisz_na_osobe`, w chwili wywołania. Druga to `wynik`, czyli wartość zwrócona i zapisana. Zmienna `nic` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła. Nazwy `wynik` i `nic` służą tylko tej ilustracji.

Konsekwencja jest praktyczna: tylko zwrócony wynik da się wykorzystać dalej. Dlatego `na_osobe(suma(mazury), 3)` działa: wynik jednej funkcji trafia jako argument do drugiej.

> **Wtręt:** Marta napisała funkcję `na_osobe`, która na końcu robiła `print(suma / osoby)`, i uznała, że wynik jest gotowy. Próbując dodać do niego napiwek, wpisała `na_osobe(300, 4) + 10` i dostała czerwony `TypeError` o `NoneType` i `int`. Na ekranie przecież widziała `75.0`, ale to było tylko wypisanie: funkcja nic nie oddała, więc do dodawania trafiło `None`. Zamieniła `print` na `return` i napiwek wreszcie się dodał.

> **Z życia wzięte:** Napisałem funkcję liczącą sumę zamówień klienta. Na końcu wypisywała wynik przez `print`, bo podczas testów tylko na niego patrzyłem na ekranie. Potem inny fragment skryptu zapisał tę sumę do raportu i w całej kolumnie pojawiło się słowo `None`. Nic nie zgłosiło błędu, bo zapisanie `None` do pliku jest poprawne. Od tamtej pory funkcje, które coś liczą, kończę instrukcją `return`, a wypisywanie zostawiam wywołującemu.

## Nadawaj czytelne nazwy

Nazwa to jedyna wskazówka, co kryje się w zmiennej albo funkcji. Komputerowi wszystko jedno, jak ją nazwiesz, ale kod czytasz Ty: dziś, za miesiąc i ktoś inny. Dobra nazwa zastępuje komentarz.

Porównaj dwie wersje tej samej rzeczy:

| Nieczytelnie | Czytelnie |
|---|---|
| `f(a, b)` | `udzial_na_osobe(suma, liczba_osob)` |
| `x = 3` | `liczba_osob = 3` |
| `dane2` | `kwoty_wydatkow` |

Przy `f(300, 4)` trzeba zgadywać, co się dzieje i która liczba jest która. [To ryzyko z zamienioną kolejnością, które znasz z argumentów funkcji](#lm-48): zły wynik bez błędu. Nazwa `udzial_na_osobe` mówi to od razu.

<a id="ref-29"></a>Funkcję nazywaj tak, by opisywała, co robi (`suma_wydatkow`), a zmienną tak, by opisywała, co trzyma (`liczba_osob`). Zwykle małe litery, słowa rozdzielone podkreśleniem, bez polskich znaków, tak jak w całym tutorialu.

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

print(udzial_na_osobe(suma_wydatkow([45.5, 20, 12.5]), 3))
```

```text
26.0
```

Ostatnią linię czyta się prawie jak zdanie. Ta czytelność przyda się [przy dzieleniu programu na funkcje](#podziel-program-na-funkcje) i [przy ponownym użyciu kodu, które omówimy za chwilę](#ref-100).

## Wykorzystaj kod ponownie

<a id="ref-100"></a>Ponowne użycie kodu to wykorzystanie tego samego fragmentu wiele razy zamiast pisania go od nowa. W Pythonie robisz to przez funkcję: definicję piszesz raz, a potem robisz dowolną liczbę wywołań z innymi danymi.

Zobacz dwa wyjazdy liczone tą samą logiką:

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print(udzial_na_osobe(suma_wydatkow(mazury), 3))
print(udzial_na_osobe(suma_wydatkow(tatry), 4))
```

```text
26.0
112.5
```

Zmieniają się tylko dane: lista wydatków i liczba osób. <a id="lm-51"></a>Logika liczenia leży w jednym miejscu, więc nie kopiujesz pętli dla każdego wyjazdu.

Ma to dwie konsekwencje. Gdy znajdziesz błąd w liczeniu sumy, poprawiasz go raz i naprawiasz wszystkie wyjazdy naraz. A trzeci wyjazd to jedna nowa lista i dwa wywołania, bez nowego kodu.

Właśnie po to funkcje mają parametry: to, co stałe, zostaje w środku, a to, co zmienne, wchodzi z zewnątrz.

U siebie w `funkcje.py` masz te same funkcje (pod krótszymi nazwami `suma` i `na_osobe`). Ostatnia linia wywołuje `na_osobe(300)` z jednym argumentem zamiast dwóch, stąd błąd.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `funkcje.py`.** Usuwamy błędną linię z na_osobe(300), która podawała tylko jeden argument.

```diff
 print("Tatry:", na_osobe(suma(tatry), 4))
-print(na_osobe(300))
```

<details>
<summary>Cały plik <code>funkcje.py</code> po zmianie</summary>

```python
# funkcje.py - funkcje Wspólnej Kasy
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print("Mazury:", na_osobe(suma(mazury), 3))
print("Tatry:", na_osobe(suma(tatry), 4))
```

</details>

**Krok 2. Uruchom.** Uruchamiamy ponownie: błąd zniknął, a te same funkcje policzyły oba wyjazdy.

```bash
python funkcje.py
```

Wynik:

```text
Mazury: 26.0
Tatry: 112.5
```

<details>
<summary>Na marginesie: Podprogramy: pomysł z pierwszych komputerów</summary>

Pomysł, by raz napisany fragment programu wywoływać wielokrotnie, jest starszy niż większość języków programowania. Za sformalizowanie go uważa się zwykle Maurice'a Wilkesa, Davida Wheelera i Stanleya Gilla, pracujących przy jednym z pierwszych komputerów, EDSAC. Zebrane przez nich gotowe podprogramy tworzyły coś w rodzaju biblioteki, z której programiści brali fragmenty zamiast pisać je od nowa. Nasze `suma_wydatkow` ma więc bardzo szacownych przodków.

Źródło: [Subroutine – Wikipedia](https://en.wikipedia.org/wiki/Subroutine)

</details>

**Ilustracja:** _Definicja raz, wywołań tyle, ile masz ciasta._

Tekst alternatywny: Piekarka wycina tą samą foremką w kształcie gwiazdki ciastka z trzech płatów ciasta w różnych kolorach; gotowe ciastka mają ten sam kształt, a różnią się kolorem.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Jasna kuchnia. Uśmiechnięta piekarka trzyma jedną metalową foremkę w kształcie gwiazdki. Na blacie leżą trzy płaty ciasta w różnych kolorach: jasne, kakaowe i różowe. Z każdego wycięła już kilka gwiazdek, a obok stygną na kratce rzędy identycznych kształtem ciastek w trzech kolorach. Foremka jest wyraźnie jedna, ciasta są różne. Bez tekstu na obrazku.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/07-wykorzystaj-kod-ponownie-1.png`

</details>

## Co zapamiętać

- Funkcję definiujesz raz przez def, a uruchamiasz każdym wywołaniem jej nazwy z nawiasami.
- Funkcje dają kodowi nazwy i jedno miejsce na każdą logikę, więc program jest czytelniejszy, a poprawki robisz raz.
- Argumenty to wartości podane przy wywołaniu, które trafiają do parametrów funkcji według kolejności lub nazwy, a ich liczba musi pasować do definicji.
- Return oddaje wartość wywołującemu, po czym kończy funkcję, a print tylko pokazuje tekst i niczego nie zwraca (funkcja bez return daje None).
- Nazywaj funkcję według tego, co robi, a zmienną według tego, co trzyma, bo kod czyta się częściej, niż pisze.
- Funkcję piszesz raz, a wywołujesz z różnymi danymi, więc poprawka w jednym miejscu naprawia wszystkie użycia.

## Pytania sprawdzające

### 38. Czym jest funkcja?

<details>
<summary>Odpowiedź</summary>

Funkcja to nazwany fragment kodu, który raz definiujesz słowem def, a potem uruchamiasz, wywołując jego nazwę z nawiasami. Może przyjmować dane i oddawać wynik. Dzięki temu ten sam kod działa w wielu miejscach bez kopiowania.

Zobacz: [sekcja „Zdefiniuj i wywołaj funkcję”](#zdefiniuj-i-wywołaj-funkcję).

</details>

### 39. Po co dzielić program na funkcje?

<details>
<summary>Odpowiedź</summary>

Funkcje dzielą program na nazwane kawałki, z których każdy robi jedną rzecz i istnieje w jednym miejscu. Dzięki temu kod jest czytelniejszy, ta sama logika działa dla różnych danych bez kopiowania, a poprawkę robisz w jednym miejscu. Małe funkcje łatwiej też sprawdzać osobno.

Zobacz: [sekcja „Podziel program na funkcje”](#podziel-program-na-funkcje).

</details>

### 40. Czym są argumenty funkcji?

<details>
<summary>Odpowiedź</summary>

Argumenty to wartości, które podajesz w nawiasach przy wywołaniu funkcji, żeby miała na czym pracować. Python przypisuje je parametrom, czyli nazwom z definicji funkcji, według kolejności albo według nazw. Dzięki temu ta sama funkcja liczy dla różnych danych. Zła liczba argumentów kończy się błędem TypeError.

Zobacz: [sekcja „Przekaż funkcji argumenty”](#przekaż-funkcji-argumenty).

</details>

### 41. Co to znaczy, że funkcja zwraca wynik?

<details>
<summary>Odpowiedź</summary>

Funkcja zwraca wynik, gdy instrukcją return oddaje wartość temu, kto ją wywołał, a wywołanie zamienia się wtedy w tę wartość. Można ją zapisać do zmiennej lub przekazać innej funkcji. Samo wypisanie na ekran to co innego: funkcja bez return oddaje None, czyli nic do dalszej pracy.

Zobacz: [sekcja „Odbierz wynik z funkcji”](#odbierz-wynik-z-funkcji).

</details>

### 42. Dlaczego nazwy zmiennych i funkcji powinny być czytelne?

<details>
<summary>Odpowiedź</summary>

Nazwa to jedyna wskazówka, co robi funkcja albo co trzyma zmienna. Komputer nie dba o nazwy, ale człowiek czyta kod wielokrotnie i musi go rozumieć bez zgadywania. Czytelna nazwa zapobiega też błędom, np. pomyleniu kolejności argumentów.

Zobacz: [sekcja „Nadawaj czytelne nazwy”](#nadawaj-czytelne-nazwy).

</details>

### 43. Czym jest ponowne użycie kodu?

<details>
<summary>Odpowiedź</summary>

Ponowne użycie kodu to korzystanie z tego samego fragmentu wiele razy bez przepisywania go. W Pythonie robisz to przez funkcję: piszesz ją raz i wywołujesz z różnymi danymi. Dzięki temu poprawka w jednym miejscu działa wszędzie, a nowy przypadek to tylko nowe dane.

Zobacz: [sekcja „Wykorzystaj kod ponownie”](#wykorzystaj-kod-ponownie).

</details>
