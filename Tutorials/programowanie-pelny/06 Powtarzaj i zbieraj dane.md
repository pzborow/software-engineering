# Powtarzaj i zbieraj dane

Dotąd każdą wartość trzymałeś w osobnej zmiennej i każdą czynność zapisywałeś osobno, a przy dziesięciu wydatkach to szybko zamienia się w żmudne kopiowanie. W tym dziale nauczysz się zbierać dane na liście i powtarzać instrukcje w pętli, więc jednym zapisem obsłużysz i trzy, i trzysta pozycji. Wykorzystasz zmienne z działu 04 oraz warunki z działu 05, a we „Wspólnej Kasie” lista wydatków i [pętla](00%20Glosariusz.md#pętla) `for` zsumują kwoty i policzą saldo każdej osoby. W warsztacie zobaczysz też pętlę, która się nie kończy, i zatrzymasz ją klawiszami Ctrl+C.

```text
wydatki = [40, 25, 60]      suma = 0
        |
        v
 +--> for każdy wydatek z listy:
 |        suma = suma + wydatek
 |        (40 -> suma 40, 25 -> suma 65, 60 -> suma 125)
 +--------- następny wydatek, aż lista się skończy
        |
        v
 koniec listy: suma = 125
```

**W tym dziale:**

- [Powtórz kod pętlą](#powtórz-kod-pętlą)
- [Zastąp kopiowanie pętlą](#zastąp-kopiowanie-pętlą)
- [Unikaj pętli nieskończonej](#unikaj-pętli-nieskończonej)
- [Zbierz dane w liście](#zbierz-dane-w-liście)
- [Wybierz element z listy](#wybierz-element-z-listy)
- [Przejdź przez całą listę](#przejdź-przez-całą-listę)

**Warsztat, punkt startowy:** pliki z końca działu 05: `kasa.py` ([treść](99%20Warsztat.md#po-dziale-05)).

## Powtórz kod pętlą

Pętla to instrukcja, która każe programowi wykonać ten sam fragment kodu wielokrotnie. Zamiast pisać tę samą linię trzy razy, zapisujesz ją raz i mówisz, ile razy albo dla czego ją powtórzyć.

Jedno powtórzenie fragmentu nazywamy [iteracją](00%20Glosariusz.md#iteracja). Pętla `for` wykonuje po jednej iteracji dla każdego elementu z zestawu danych. Taki zestaw to na razie po prostu lista wartości w nawiasach kwadratowych; [jej zapis omówimy osobno](#ref-75).

Wcięte linie pod `for` to ciało pętli, [tak samo jak przy `if`](05%20Podejmuj%20decyzje%20w%20programie.md#zapisz-warunek-z-if). Nazwa po słowie `for` to zmienna, która w każdej iteracji dostaje kolejny [element](00%20Glosariusz.md#element-listy):

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print("Cześć,", imie)
print("Koniec")
```

```text
Cześć, Ania
Cześć, Bartek
Cześć, Celina
Koniec
```

<a id="lm-39"></a>Ciało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. [Ostatni `print` nie ma wcięcia](05%20Podejmuj%20decyzje%20w%20programie.md#lm-36), więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.

Pętla ma więc początek, powtarzane kroki i koniec, a koniec wynika z [warunku zakończenia](00%20Glosariusz.md#warunek-zakończenia): w `for` jest nim wyczerpanie elementów. W „Wspólnej Kasie” dzięki temu jeden zapis obsłuży trzy osoby, ale też trzydzieści.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy listę kwot i pętlę, która je wypisuje i sumuje.

```diff
     print("Zwykła kwota")
+kwoty_wydatkow = [45.5, 20, 12.5]
+suma = 0
+for kwota in kwoty_wydatkow:
+    print(kwota)
+    suma = suma + kwota
+print(suma)
 print("Koniec")
```

<details>
<summary>Cały plik <code>kasa.py</code> po zmianie</summary>

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
nazwa_wyjazdu = "Mazury"
kwota_wydatku = 45.5
czy_oplacone = True
print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
print(type(nazwa_wyjazdu))
print(type(kwota_wydatku))
print(type(czy_oplacone))
czy_oplacone = False
print(czy_oplacone)
liczba_osob = 3
koszt_na_osobe = kwota_wydatku / liczba_osob
print(koszt_na_osobe)
print(kwota_wydatku % liczba_osob)
print("Kwota: " + str(kwota_wydatku) + " zł")
print(f"Wyjazd: {nazwa_wyjazdu}, kwota: {kwota_wydatku} zł")
print(kwota_wydatku > 100)
print(kwota_wydatku >= 45.5)
print(liczba_osob != 3)
print(nazwa_wyjazdu == "mazury")
if kwota_wydatku > 40:
    print("Kwota do sprawdzenia")
if kwota_wydatku > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print(kwota_wydatku > 40 and liczba_osob > 5)
print(kwota_wydatku > 100 or liczba_osob == 3)
if kwota_wydatku > 100 or liczba_osob > 5:
    print("Duża kwota")
else:
    print("Zwykła kwota")
kwoty_wydatkow = [45.5, 20, 12.5]
suma = 0
for kwota in kwoty_wydatkow:
    print(kwota)
    suma = suma + kwota
print(suma)
print("Koniec")
```

</details>

**Krok 2. Uruchom.** Uruchamiamy skrypt i sprawdzamy działanie pętli.

```bash
python kasa.py
```

Wynik:

```text
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>
False
15.166666666666666
0.5
Kwota: 45.5 zł
Wyjazd: Mazury, kwota: 45.5 zł
False
True
False
False
Kwota do sprawdzenia
Zwykła kwota
False
True
Zwykła kwota
45.5
20
12.5
78.0
Koniec
```

> **Wtręt:** Marta chciała wypisać komunikat dla każdego współlokatora, więc trzy razy wkleiła linię `print("Cześć,", imie)`, za każdym razem z innym imieniem. Gdy w mieszkaniu pojawiła się czwarta osoba, dopisała czwartą linię, a potem piątą, bo wprowadził się jeszcze kuzyn. Wtedy zauważyła, że w pętli `for` wystarczyłoby dopisać imię do listy, i zaczęła podejrzewać, że wklejanie było najdłuższą drogą.

## Zastąp kopiowanie pętlą

Pętli warto użyć, gdy ta sama czynność dotyczy wielu elementów albo liczba powtórzeń zależy od danych. Jeśli kopiujesz linię i zmieniasz w niej tylko jedną wartość, to znak, że [potrzebna jest pętla](00%20Glosariusz.md#pętla).

Powtarzanie ręczne ma dwie wady. Poprawkę trzeba wprowadzić w wielu miejscach, a przy każdej łatwo o pomyłkę. Poza tym taki kod nie dopasuje się do danych: napisany na trzy osoby nie obsłuży czwartej.

```python
osoby = ["Ania", "Bartek", "Celina"]
liczba_osob = 3
for imie in osoby:
    print(imie, "płaci", 300 / liczba_osob)
```

```text
Ania płaci 100.0
Bartek płaci 100.0
Celina płaci 100.0
```

Zmienia się tylko `imie`, więc reszta linii jest zapisana jeden raz. Poprawka wzoru to jedna zmiana zamiast trzech.

| Sytuacja | Rozwiązanie |
|---|---|
| Ta sama czynność dla każdego elementu zestawu | pętla |
| Liczba powtórzeń zależy od danych | pętla |
| Dwie różne czynności, każda raz | zwykłe linie |
| Pojedyncza czynność, która się nie powtarza | zwykła linia |

Pętla `for` ma z góry znany koniec. Pętlę, która nigdy się nie kończy, omówimy w następnej kolejności.

## Unikaj pętli nieskończonej

<a id="ref-79"></a>[Pętla nieskończona](00%20Glosariusz.md#pętla-nieskończona) to pętla, która nigdy nie dochodzi do końca, bo jej warunek zakończenia nigdy nie zostaje spełniony. Program powtarza wtedy ten sam fragment bez końca, więc nie dociera do dalszych linii i nie oddaje wyniku.

[Pętla `for`, którą znasz, kończy się sama](#powtórz-kod-pętlą), bo zestaw danych się wyczerpuje. Pętla `while` („dopóki”) działa inaczej: powtarza wcięte linie, dopóki warunek daje `True`. Jeśli warunek jest zawsze prawdziwy, każda kolejna iteracja zaczyna się od nowa.

```python
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

Tu warunek to na stałe `True`, a w ciele nic go nie zmienia. Linia `time.sleep(1)` robi tylko jednosekundową przerwę, żeby napisy nie zalały ekranu. Zdarza się to też przez pomyłkę: warunek zależy od zmiennej, której pętla nigdy nie zmienia.

Problem jest praktyczny. Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków. Tak samo wyglądałaby [„Wspólna Kasa”, która czeka na koniec listy](#lm-39), którego nie ma.

Zatrzymasz taki program skrótem Ctrl+C w terminalu. Python przerywa wtedy działanie i wypisuje komunikat `KeyboardInterrupt`, czyli „przerwano z klawiatury”. To nie awaria, tylko Twoja komenda.

Dlatego przy każdej pętli `while` zadaj sobie pytanie: co sprawi, że warunek w końcu stanie się fałszywy?

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `nieskonczona.py`.** Osobny skrypt z pętlą while bez warunku zakończenia.

```python
# nieskonczona.py - pętla, która nigdy się nie kończy
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

**Krok 2. Uruchom.** Po kilku liniach naciśnij Ctrl+C; ścieżka w komunikacie będzie u Ciebie inna.

```bash
python nieskonczona.py
```

Wynik:

```text
Liczę wydatki...
Liczę wydatki...
Liczę wydatki...
^CTraceback (most recent call last):
  File "/home/ania/wspolna_kasa/nieskonczona.py", line 5, in <module>
    time.sleep(1)
    ~~~~~~~~~~^^^
KeyboardInterrupt
```

_[źródła: 3](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-powtarzaj-i-zbieraj-dane)_

> **Z życia wzięte:** Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciele pętli nie dawałem jej nowej wartości. Skrypt działał całą noc, zajmował procesor i rano nie było raportu. Od tamtej pory przy każdym `while` zapisuję sobie, która linia zmieni warunek, a przy czekaniu na zewnętrzne zdarzenie dodaję limit prób.

**Ilustracja:** _Pętla bez warunku zakończenia: biegnie się chętnie, ale nie wiadomo dokąd._

Tekst alternatywny: Chomik biegnie w kole w klatce, choć z boku są otwarte drzwiczki. Obok stoi uśmiechnięta osoba z herbatą i wskazuje na nie palcem.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Ciepła scena w pokoju: puszysty chomik biegnie w kole w klatce, z determinacją na pyszczku. Z boku koła widać wyraźnie otwarte małe drzwiczki, ale chomik patrzy przed siebie i ich nie zauważa. Obok klatki stoi uśmiechnięta osoba z kubkiem herbaty i z rozbawieniem wskazuje palcem na drzwiczki. Na stole leży otwarty laptop z kilkoma abstrakcyjnymi paskami kodu na ekranie. Bez tekstu na obrazku.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/06-unikaj-pętli-nieskończonej-1.png`

</details>

## Zbierz dane w liście

[Lista danych](00%20Glosariusz.md#lista-danych) to jedna zmienna, która przechowuje wiele wartości w ustalonej kolejności. Zamiast trzech zmiennych z imionami masz jedną nazwę, pod którą leży cały zestaw.

Właśnie po takim zestawie chodzi pętla `for`: [wcześniej szła po imionach uczestników](#lm-39), a teraz przyglądamy się samej liście.

<a id="ref-75"></a>Listę zapisujesz w nawiasach kwadratowych, a wartości oddzielasz przecinkami. Każda wartość to element listy, czyli jedno miejsce w zestawie. Tekst ma cudzysłów, liczba nie, tak samo jak przy zwykłych zmiennych.

```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby)
print(len(osoby))
```

```text
['Ania', 'Bartek', 'Celina']
3
```

Funkcja `len()` podaje długość listy, czyli liczbę elementów. Python wypisuje listę w nawiasach, a teksty w apostrofach; to tylko sposób wyświetlania.

<a id="lm-42"></a>Kolejność ma znaczenie: „Ania” jest pierwsza i tak zostaje. Lista może być też dłuższa albo pusta (`[]`), a program nie musi z góry znać jej rozmiaru. Dlatego pasuje do „Wspólnej Kasy”: `osoby` to uczestnicy wyjazdu, a `wydatki` to zapłacone rachunki, których przybywa.

Jak sięgnąć po jeden element, omówimy osobno. To, co lista daje pętli, zobaczysz [przy przechodzeniu przez wszystkie elementy](#przejdź-przez-całą-listę).

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-powtarzaj-i-zbieraj-dane)_

> **Z przymrużeniem oka:** Pusta lista `[]` to torba na zakupy przed wejściem do sklepu: już istnieje, ale nic w niej nie ma. `len()` odpowie uczciwie: 0.

## Wybierz element z listy

<a id="ref-83"></a>Po element listy sięgasz przez jego numer w nawiasach kwadratowych: `osoby[0]`. Numer nazywa się [indeksem](00%20Glosariusz.md#indeks) i liczenie zaczyna się od zera, więc pierwszy element ma indeks 0, drugi 1, trzeci 2.

Wygląda to dziwnie, ale indeks mówi, o ile miejsc od początku listy się przesunąć. Pierwszy element jest na samym początku, więc przesunięcie wynosi zero. Kolejność zostaje taka, jak w sekcji Czym jest lista danych.

Ujemny indeks liczy od końca: `-1` to ostatni element, `-2` przedostatni. Jest wygodny, gdy nie wiesz, ile elementów ma lista.

```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby[0])
print(osoby[2])
print(osoby[-1])
```

```text
Ania
Celina
Celina
```

Indeks spoza listy kończy się błędem `IndexError`. Przy trzech osobach ostatni jest `osoby[2]`, a `osoby[3]` nie istnieje, więc program się zatrzyma. Największy poprawny indeks to `len(osoby) - 1`.

Odczyt niczego nie zmienia: lista zostaje taka sama, dostajesz tylko kopię wartości.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy wypisanie pierwszego i ostatniego wydatku z listy.

```diff
 print(suma)
+print(kwoty_wydatkow[0])
+print(kwoty_wydatkow[-1])
 print("Koniec")
```

<details>
<summary>Cały plik <code>kasa.py</code> po zmianie</summary>

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
nazwa_wyjazdu = "Mazury"
kwota_wydatku = 45.5
czy_oplacone = True
print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
print(type(nazwa_wyjazdu))
print(type(kwota_wydatku))
print(type(czy_oplacone))
czy_oplacone = False
print(czy_oplacone)
liczba_osob = 3
koszt_na_osobe = kwota_wydatku / liczba_osob
print(koszt_na_osobe)
print(kwota_wydatku % liczba_osob)
print("Kwota: " + str(kwota_wydatku) + " zł")
print(f"Wyjazd: {nazwa_wyjazdu}, kwota: {kwota_wydatku} zł")
print(kwota_wydatku > 100)
print(kwota_wydatku >= 45.5)
print(liczba_osob != 3)
print(nazwa_wyjazdu == "mazury")
if kwota_wydatku > 40:
    print("Kwota do sprawdzenia")
if kwota_wydatku > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print(kwota_wydatku > 40 and liczba_osob > 5)
print(kwota_wydatku > 100 or liczba_osob == 3)
if kwota_wydatku > 100 or liczba_osob > 5:
    print("Duża kwota")
else:
    print("Zwykła kwota")
kwoty_wydatkow = [45.5, 20, 12.5]
suma = 0
for kwota in kwoty_wydatkow:
    print(kwota)
    suma = suma + kwota
print(suma)
print(kwoty_wydatkow[0])
print(kwoty_wydatkow[-1])
print("Koniec")
```

</details>

**Krok 2. Uruchom.** Uruchamiamy skrypt i sprawdzamy dwa nowe wiersze przed słowem Koniec.

```bash
python kasa.py
```

Wynik:

```text
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>
False
15.166666666666666
0.5
Kwota: 45.5 zł
Wyjazd: Mazury, kwota: 45.5 zł
False
True
False
False
Kwota do sprawdzenia
Zwykła kwota
False
True
Zwykła kwota
45.5
20
12.5
78.0
45.5
12.5
Koniec
```

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-powtarzaj-i-zbieraj-dane)_

<details>
<summary>Na marginesie: Dlaczego liczenie zaczyna się od zera</summary>

Holenderski informatyk Edsger Dijkstra w krótkiej notatce z 1982 roku przekonywał, że numerację warto zaczynać od zera, a zakresy zapisywać tak, by początek był w nich wliczony, a koniec nie. Wtedy zakres ma tyle elementów, ile wynosi różnica jego końców, i nie trzeba dodawać ani odejmować jedynki. Python poszedł tą samą drogą, więc `osoby[0]` to pierwszy element, a `range(3)` daje trzy liczby: 0, 1 i 2.

Źródło: [Why numbering should start at zero (EWD831)](https://www.cs.utexas.edu/~EWD/transcriptions/EWD08xx/EWD831.html)

</details>

> **Wtręt:** Marta miała listę czterech współlokatorów i chciała pokazać ostatniego, więc napisała `osoby[4]`, bo liczyła po ludzku: pierwszy, drugi, trzeci, czwarty. Program zatrzymał się z `IndexError`, bo indeksy kończyły się na 3. Marta odetchnęła, zamieniła cyfrę na `-1` i ostatnia osoba pojawiła się bez liczenia.

## Przejdź przez całą listę

Przez wszystkie elementy listy przechodzisz pętlą `for`: `for imie in osoby:` bierze po kolei każdy element i wykonuje dla niego wcięty blok.

Przy pierwszym przebiegu (czyli iteracji) `imie` dostaje pierwszy element, przy drugim drugi, i tak do ostatniego. Gdy elementy się skończą, pętla sama przestaje, a program idzie dalej, do pierwszej linii bez wcięcia. Nie liczysz indeksów ani nie sprawdzasz długości listy.

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print(imie)
print("Koniec")
```

```text
Ania
Bartek
Celina
Koniec
```

Elementy przychodzą w kolejności listy, [więc „Ania” jest pierwsza](#lm-42). Dodasz czwartą osobę, a ta sama pętla obsłuży ją bez zmian.

Pętla może też coś zbierać. Przy liście `wydatki` dodaje kwotę każdego wydatku do sumy; zapis `wydatek["kwota"]` bierze z jednego wydatku pole `kwota`:

```python
wydatki = ...
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(suma)
```

<a id="lm-44"></a>Suma zaczyna od zera, rośnie w każdej iteracji, a wynik pokazujesz dopiero po pętli, już bez wcięcia.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-powtarzaj-i-zbieraj-dane)_

> **Z przymrużeniem oka:** Pętla `for` działa jak nauczyciel z dziennikiem: woła każdego z listy po kolei i na ostatnim nazwisku kończy. Nie stoi potem w drzwiach z pytaniem „a nie ma tu kogoś jeszcze?”.

## Co zapamiętać

- Pętla powtarza wcięty fragment kodu, a `for` robi to raz dla każdego elementu zestawu danych, po czym kończy pracę.
- Gdy kopiujesz linię i zmieniasz w niej tylko jedną wartość, użyj pętli: jeden zapis obsłuży dowolną liczbę elementów.
- Pętla nieskończona nigdy nie osiąga warunku zakończenia, więc program się „zawiesza”; zatrzymasz go Ctrl+C, a przy każdym `while` pytaj, co w końcu zmieni warunek na fałsz.
- Lista to jedna zmienna z wieloma wartościami w ustalonej kolejności, zapisana w nawiasach kwadratowych, z elementami rozdzielonymi przecinkami.
- Element listy pobierasz indeksem w nawiasach kwadratowych, licząc od zera, a `-1` oznacza ostatni element.
- Pętla `for element in lista:` wykonuje blok raz dla każdego elementu, w kolejności listy, i sama kończy pracę po ostatnim.

## Pytania sprawdzające

### 32. Czym jest pętla?

<details>
<summary>Odpowiedź</summary>

Pętla to instrukcja, która powtarza ten sam fragment kodu wiele razy. Jedno wykonanie nazywamy iteracją. Pętla `for` powtarza wcięte ciało dla każdego elementu zestawu danych i kończy się, gdy elementy się skończą.

Zobacz: [sekcja „Powtórz kod pętlą”](#powtórz-kod-pętlą).

</details>

### 33. Kiedy warto użyć pętli zamiast pisać to samo wiele razy?

<details>
<summary>Odpowiedź</summary>

Pętli warto użyć, gdy ta sama czynność dotyczy wielu elementów albo gdy liczba powtórzeń zależy od danych. Jeśli kopiujesz linię i zmieniasz w niej tylko jedną wartość, pętla skróci kod i ułatwi jego poprawianie. Zwykłe linie wystarczą, gdy czynność wykonujesz raz albo każdy krok jest inny.

Zobacz: [sekcja „Zastąp kopiowanie pętlą”](#zastąp-kopiowanie-pętlą).

</details>

### 34. Czym jest pętla nieskończona i dlaczego jest problemem?

<details>
<summary>Odpowiedź</summary>

Pętla nieskończona to pętla, której warunek zakończenia nigdy się nie spełnia, więc program powtarza ją bez końca. Jest problemem, bo program wygląda na zawieszony, zajmuje procesor i nigdy nie dochodzi do wyniku. Można ją przerwać z terminala skrótem Ctrl+C, ale lepiej od początku zadbać, by warunek kiedyś stał się fałszywy.

Zobacz: [sekcja „Unikaj pętli nieskończonej”](#unikaj-pętli-nieskończonej).

</details>

### 35. Czym jest lista danych?

<details>
<summary>Odpowiedź</summary>

Lista danych to jedna zmienna przechowująca wiele wartości w ustalonej kolejności. Zapisujesz ją w nawiasach kwadratowych, oddzielając elementy przecinkami. Może mieć dowolną długość, także zero elementów, a jej rozmiar podaje funkcja len().

Zobacz: [sekcja „Zbierz dane w liście”](#zbierz-dane-w-liście).

</details>

### 36. Jak odczytać konkretny element listy?

<details>
<summary>Odpowiedź</summary>

Element listy odczytujesz przez jego numer, czyli indeks, w nawiasach kwadratowych, np. `osoby[0]`. Numeracja zaczyna się od zera, a ujemne indeksy liczą od końca (`-1` to ostatni element). Indeks spoza listy powoduje błąd `IndexError`.

Zobacz: [sekcja „Wybierz element z listy”](#wybierz-element-z-listy).

</details>

### 37. Jak przejść przez wszystkie elementy listy?

<details>
<summary>Odpowiedź</summary>

Użyj pętli `for`, np. `for imie in osoby:`. Python bierze po kolei każdy element listy, wykonuje dla niego wcięty blok i sam kończy, gdy elementy się skończą. Nie musisz liczyć indeksów ani znać długości listy.

Zobacz: [sekcja „Przejdź przez całą listę”](#przejdź-przez-całą-listę).

</details>
