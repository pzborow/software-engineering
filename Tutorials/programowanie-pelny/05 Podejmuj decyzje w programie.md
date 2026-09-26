# Podejmuj decyzje w programie

Dotąd program tylko przechowywał dane w zmiennych; w tym dziale nauczy się z nimi coś robić. Po jego przeczytaniu policzysz wynik z liczb, sklejisz z tekstów zdanie, porównasz dwie wartości i sprawisz, że program wybierze jedną z dróg, zamiast zawsze robić to samo. Wykorzystasz zmienne i typy z poprzedniego działu oraz rozgałęzienia ze schematów blokowych z działu 2. W przykładzie „Wspólna Kasa” program policzy udział jednej osoby i zdecyduje, czy ktoś jest winien pieniądze, czy ma dostać zwrot, a w warsztacie oceni, czy wydatek jest duży.

```text
1. Dane (zmienne):        kwota, liczba osób
          ↓
2. Działanie:            kwota podzielona przez liczbę osób
          ↓
3. Porównanie:           czy koszt jest większy niż limit?
          ↓
4. Decyzja:              jeśli tak → jedna droga
                         w przeciwnym razie → druga droga
```

**W tym dziale:**

- [Wykonuj działania matematyczne](#wykonuj-działania-matematyczne)
- [Połącz kilka tekstów](#połącz-kilka-tekstów)
- [Porównaj dwie wartości](#porównaj-dwie-wartości)
- [Zapisz warunek z if](#zapisz-warunek-z-if)
- [Dodaj drugą drogę](#dodaj-drugą-drogę)
- [Łącz warunki spójnikami](#łącz-warunki-spójnikami)

**Warsztat, punkt startowy:** pliki z końca działu 04: `kasa.py` ([treść](99%20Warsztat.md#po-dziale-04)).

## Wykonuj działania matematyczne

Program wykonuje te same działania co kalkulator: dodawanie, odejmowanie, mnożenie i dzielenie, a do tego dzielenie całkowite, resztę z dzielenia i potęgowanie. Zapisujesz je za pomocą [operatorów arytmetycznych](00%20Glosariusz.md#operator-arytmetyczny), czyli znaków, które mówią Pythonowi, jakie działanie wykonać na liczbach.

| Działanie | Operator |
|---|---|
| dodawanie | `+` |
| odejmowanie | `-` |
| mnożenie | `*` |
| dzielenie | `/` |
| dzielenie całkowite | `//` |
| reszta z dzielenia | `%` |
| potęgowanie | `**` |

Mnożenie to gwiazdka, a nie „x”. Dzielenie `/` zawsze daje liczbę z częścią ułamkową, `//` zostawia samą część całkowitą, a `%` pokazuje, ile zostało. Kolejność działań jest jak w szkole: mnożenie i dzielenie przed dodawaniem, a nawiasy zmieniają porządek.

```python
kwota = 100
print(kwota / 3)
print(kwota // 3)
print(kwota % 3)
```

```text
33.333333333333336
33
1
```

Końcówka `...336` to drobna nieścisłość: komputer trzyma ułamki w przybliżeniu.

Odejmowanie, dzielenie, `//`, `%` i `**` mają sens tylko na liczbach. [Skoro `nazwa_wyjazdu` jest tekstem](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#lm-24), `nazwa_wyjazdu / 2` kończy się błędem `TypeError`. Wyjątkiem są `+` i `*`, które na tekście działają inaczej: sklejają i powtarzają.

```python
print("Ania" + "Bartek")
print("Ha" * 3)
```

```text
AniaBartek
HaHaHa
```

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy koszt na osobę i resztę z dzielenia.

```diff
 print(czy_oplacone)
+liczba_osob = 3
+koszt_na_osobe = kwota_wydatku / liczba_osob
+print(koszt_na_osobe)
+print(kwota_wydatku % liczba_osob)
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
```

</details>

**Krok 2. Uruchom.** Uruchamiamy zmieniony skrypt.

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
2.5
```

_Wersje: Python 3.13 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-podejmuj-decyzje-w-programie)_

> **Z przymrużeniem oka:** Operator `%` to ten, kto liczy, ile kawałków pizzy zostanie, gdy każdy wziął po równo. Ludzie się wahają, czy sięgnąć po ostatni, ale Python nigdy nie ma z tym problemu: po prostu podaje liczbę.

## Połącz kilka tekstów

Program łączy teksty operatorem `+`, który skleja je w jeden, dokładnie w takiej kolejności i z takimi znakami, jakie mu podasz. Ta operacja nazywa się [sklejaniem tekstów](00%20Glosariusz.md#konkatenacja) (konkatenacją). <a id="ref-52"></a>[Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno](#wykonuj-działania-matematyczne), więc oto ono.

Python niczego nie dopowiada. Nie doda spacji ani przecinka, więc odstępy musisz wstawić sam, jako część tekstu w cudzysłowie:

```python
imie = "Ania"
kwota = 45.5
print(imie + " zapłaciła " + str(kwota) + " zł")
print(imie + "zapłaciła")
```

```text
Ania zapłaciła 45.5 zł
Aniazapłaciła
```

W drugiej linii zabrakło spacji, więc słowa się zlepiły.

Sklejać można tylko tekst z tekstem. Zapis `"Kwota: " + kwota` zatrzyma program błędem `TypeError`, bo liczby 45.5 nie da się dokleić do napisu. Zamienia ją na tekst funkcja `str()`: `str(kwota)` daje `"45.5"`. Nie zmienia to samej zmiennej `kwota`, która dalej jest liczbą.

Wygodniejszy bywa zapis z literą `f` przed cudzysłowem: `f"{imie} zapłaciła {kwota} zł"`. Nazwy w nawiasach klamrowych Python podmienia na wartości, także liczbowe.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy sklejenie tekstu z liczbą.

```diff
 print(kwota_wydatku % liczba_osob)
+print("Kwota: " + kwota_wydatku)
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
print("Kwota: " + kwota_wydatku)
```

</details>

**Krok 2. Uruchom.** Liczby nie da się dokleić do tekstu.

```bash
python kasa.py
```

Zobaczysz błąd (celowy, poprawimy go):

```text
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>
False
15.166666666666666
0.5
Traceback (most recent call last):
  File "/home/ania/wspolna_kasa/kasa.py", line 15, in <module>
    print("Kwota: " + kwota_wydatku)
          ~~~~~~~~~~^~~~~~~~~~~~~~~
TypeError: can only concatenate str (not "float") to str
```

**Krok 3. Zmień plik `kasa.py`.** Zamieniamy liczbę na tekst i dodajemy zapis z f.

```diff
 print(kwota_wydatku % liczba_osob)
-print("Kwota: " + kwota_wydatku)
+print("Kwota: " + str(kwota_wydatku) + " zł")
+print(f"Wyjazd: {nazwa_wyjazdu}, kwota: {kwota_wydatku} zł")
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
```

</details>

**Krok 4. Uruchom.**

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
```

_Wersje: Python 3.13 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-podejmuj-decyzje-w-programie)_

> **Wtręt:** W arkuszu Marta łączyła tekst z liczbą znakiem `&` i nigdy nie miała z tym kłopotu. Napisała więc w Pythonie `"Do zapłaty: " + udzial`, gdzie `udzial` było liczbą `22.75`, i zobaczyła czerwony `TypeError`. Python nie zgadł, że liczba ma stać się tekstem, bo takich rzeczy nie robi sam. Dopiero `str(udzial)` albo zapis z `f` przed cudzysłowem uspokoiły komputer.

## Porównaj dwie wartości

Program porównuje wartości [operatorami porównania](00%20Glosariusz.md#operator-porównania). To znaki takie jak `==` czy `>`, które zestawiają dwie wartości i zwracają wynik `True` albo `False`, czyli [wartość logiczną](00%20Glosariusz.md#wartość-logiczna).

| Zapis | Znaczenie |
|---|---|
| `a == b` | równe |
| `a != b` | różne |
| `a < b`, `a > b` | mniejsze, większe |
| `a <= b`, `a >= b` | mniejsze lub równe, większe lub równe |

Uwaga na `==`: [pojedynczy znak `=` to przypisanie](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#przypisz-wartość-zmiennej), czyli zapisanie wartości w zmiennej. Dopiero podwójny pyta „czy są równe?” i niczego nie zmienia.

```python
kwota = 45.5
print(kwota == 45.5)
print(kwota != 45.5)
print(kwota > 50)
print(kwota <= 45.5)
print("Ania" == "ania")
print("45.5" == 45.5)
```

```text
True
False
False
True
False
False
```

Dwa ostatnie wyniki pokazują, że porównanie jest ścisłe. Wielka i mała litera to różne znaki, więc `"Ania"` i `"ania"` się różnią. [Tekst `"45.5"` i liczba 45.5 to różne typy](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#lm-27), więc też nie są równe, choć wyglądają podobnie.

Sam wynik `True` lub `False` jeszcze nic nie robi. Dopiero [instrukcja warunkowa](00%20Glosariusz.md#instrukcja-warunkowa), o której będzie następna sekcja, pozwoli programowi wybrać na jego podstawie, co zrobić dalej.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy porównania na końcu.

```diff
 print(f"Wyjazd: {nazwa_wyjazdu}, kwota: {kwota_wydatku} zł")
+print(kwota_wydatku > 100)
+print(kwota_wydatku >= 45.5)
+print(liczba_osob != 3)
+print(nazwa_wyjazdu == "mazury")
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
```

</details>

**Krok 2. Uruchom.** Uruchamiamy skrypt i patrzymy na cztery nowe wyniki.

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
```

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-podejmuj-decyzje-w-programie)_

> **Z życia wzięte:** W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze statusem `"aktywny"` i skrypt po cichu je pomijał, bo porównanie jest ścisłe. Żaden błąd się nie pojawił, brakowało tylko kilkuset zamówień w raporcie. Od tamtej pory przed porównaniem tekstów z zewnątrz sprawdzam, w jakiej postaci naprawdę przychodzą, i pilnuję, żeby liczba wyników zgadzała się z oczekiwaną.

## Zapisz warunek z if

Instrukcja warunkowa to polecenie, które <a id="ref-69"></a>wykonuje wybrany fragment kodu tylko wtedy, gdy warunek jest prawdziwy. W Pythonie zapisujemy ją słowem `if`, czyli „jeśli”.

Warunek to zwykle [porównanie z poprzedniej sekcji](#porównaj-dwie-wartości), bo daje `True` albo `False`. <a id="ref-61"></a>Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej.

Które linie należą do warunku, pokazuje [wcięcie](00%20Glosariusz.md#wcięcie): przesunięcie linii o cztery spacje w prawo. Po warunku stawiamy dwukropek.

```python
kwota = 45.5
if kwota > 40:
    print("Kwota do sprawdzenia")
if kwota > 100:
    print("Bardzo duża kwota")
print("Koniec")
```

```text
Kwota do sprawdzenia
Koniec
```

Pierwszy warunek jest prawdziwy, więc jego linia się wykonała. Drugi jest fałszywy, więc jego wcięta linia została pominięta. <a id="lm-36"></a>Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.

Program przestaje więc biegnąć wszystkimi liniami po kolei: to, co wykona, zależy od danych. Co zrobić, gdy warunek jest fałszywy, pokażemy w następnej sekcji.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy dwa warunki i końcowy print.

```diff
 print(nazwa_wyjazdu == "mazury")
+if kwota_wydatku > 40:
+    print("Kwota do sprawdzenia")
+if kwota_wydatku > 100:
+    print("Bardzo duża kwota")
+print("Koniec")
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
print("Koniec")
```

</details>

**Krok 2. Uruchom.** Uruchamiamy skrypt i sprawdzamy, które linie się wykonały.

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
Koniec
```

_Wersje: Python 3.13 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-podejmuj-decyzje-w-programie)_

> **Wtręt:** Marta napisała: `if kwota > 100:`, pod spodem wcięte `print("Duża kwota")`, a linię `print("Sprawdź paragon")` zostawiła bez wcięcia, bo chciała ją pokazać tylko przy dużych kwotach. Program przy kwocie `45.5` wypisał napomnienie o paragonie, choć nic dużego nie kupiono. Ta linia nie miała wcięcia, więc nie należała do warunku i wykonywała się zawsze. Marta dopisała cztery spacje i napomnienia zniknęły z drobnych zakupów.

## Dodaj drugą drogę

Część `else`, czyli „w przeciwnym razie”, <a id="ref-71"></a>wykonuje swoje linie wtedy, gdy warunek z `if` jest fałszywy. Dzięki niej program zawsze wybiera jedną z dwóch dróg, a nie tylko „robi coś albo nic”.

Zapisujemy ją pod blokiem `if`, na tym samym poziomie wcięcia co samo `if`, z dwukropkiem po słowie `else`. Sama nie ma warunku: nie pyta o nic, bo obejmuje wszystko, czego `if` nie złapało. Jej własne linie też wcinamy o cztery spacje.

```python
kwota = 45.5
if kwota > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print("Koniec")
```

```text
Zwykła kwota
Koniec
```

Warunek `kwota > 100` jest fałszywy, więc Python pominął pierwszy wcięty blok i wykonał ten pod `else`. Gdyby kwota wynosiła 150, wypisałoby się tylko „Bardzo duża kwota”. Oba bloki nigdy nie wykonają się naraz. Ostatni `print` nie ma wcięcia, więc, [jak w poprzedniej sekcji, działa zawsze](#lm-36).

Dla „Wspólnej Kasy” to ważne: program może teraz w każdym przypadku powiedzieć coś sensownego, osobno o dużej i zwykłej kwocie. Sprawdzanie kilku warunków naraz, czyli „i” oraz „lub”, pokażemy w następnej sekcji.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy else do drugiego warunku.

```diff
     print("Bardzo duża kwota")
+else:
+    print("Zwykła kwota")
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
print("Koniec")
```

</details>

**Krok 2. Uruchom.** Uruchamiamy skrypt.

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
2.5
Kwota: 45.5 zł
Wyjazd: Mazury, kwota: 45.5 zł
False
True
False
False
Kwota do sprawdzenia
Zwykła kwota
Koniec
```

**Ilustracja:** _Z rozwidlenia `if` i `else` zawsze wychodzi się jedną drogą._

Tekst alternatywny: Wędrowiec z plecakiem stoi przy rozwidleniu drogi na dwie ścieżki, do domku i na łąkę, i wybiera jedną z nich.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Wiejska droga rozwidla się na dwie ścieżki: jedna prowadzi do niebieskiego domku z ogródkiem, druga na łąkę z drzewem. Przy rozwidleniu stoi uśmiechnięty wędrowiec z plecakiem i wybiera jedną ze ścieżek, a drugą zamyka niska drewniana furtka. Trzeciej drogi, na której można by stać w miejscu i nic nie robić, nie ma. Na słupku wskazującym kierunki widać tylko puste tabliczki, bez tekstu.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/05-dodaj-drugą-drogę-1.png`

</details>

## Łącz warunki spójnikami

[Operatory logiczne](00%20Glosariusz.md#operator-logiczny) `and` („i”) oraz `or` („lub”) <a id="ref-73"></a>łączą kilka warunków w jeden. Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: `True` albo `False`.

`and` daje `True` tylko wtedy, gdy prawdziwe są **oba** warunki. `or` daje `True`, gdy prawdziwy jest **którykolwiek** z nich, a `False` dopiero wtedy, gdy oba są fałszywe.

| Lewy warunek | Prawy warunek | `and` | `or` |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

Każdy z połączonych warunków zapisujemy w całości, [tak jak w porównywaniu wartości](#porównaj-dwie-wartości). Wynik można wypisać albo wstawić do `if`:

```python
kwota = 45.5
liczba_osob = 3
print(kwota > 40 and liczba_osob > 5)
print(kwota > 100 or liczba_osob == 3)
if kwota > 100 or liczba_osob > 5:
    print("Duża kwota")
else:
    print("Zwykła kwota")
```

```text
False
True
Zwykła kwota
```

W pierwszej linii drugi warunek zawiódł, więc `and` dało `False`. W drugiej wystarczył prawdziwy drugi warunek, więc `or` dało `True`. W `if` oba są fałszywe, więc zadziałało `else`.

Dla „Wspólnej Kasy” to znaczy, że kwotę można uznać za dużą, gdy jest wysoka **lub** dzieli ją dużo osób. U siebie w `kasa.py` dopisz te linie w warsztacie poniżej.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy warunki z and oraz or przed ostatnim print.

```diff
     print("Zwykła kwota")
+print(kwota_wydatku > 40 and liczba_osob > 5)
+print(kwota_wydatku > 100 or liczba_osob == 3)
+if kwota_wydatku > 100 or liczba_osob > 5:
+    print("Duża kwota")
+else:
+    print("Zwykła kwota")
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
print("Koniec")
```

</details>

**Krok 2. Uruchom.** Uruchamiamy skrypt i sprawdzamy nowe trzy linie wyniku.

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
2.5
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
Koniec
```

## Co zapamiętać

- Python zna siedem podstawowych operatorów arytmetycznych (`+ - * / // % **`); na tekście dzielić się nie da, a `+` i `*` znaczą tam sklejanie i powtarzanie.
- Plus skleja tylko tekst z tekstem, bez dodawania spacji, a liczbę trzeba przed sklejeniem zamienić funkcją str() albo użyć zapisu z f.
- Operatory porównania (`==`, `!=`, `<`, `>`, `<=`, `>=`) dają `True` albo `False`, a `==` pyta o równość, w przeciwieństwie do `=`, które przypisuje.
- Instrukcja `if` wykonuje wcięte pod nią linie tylko wtedy, gdy warunek daje `True`; w przeciwnym razie Python je pomija.
- `else` to droga „w przeciwnym razie”: wykonuje się tylko wtedy, gdy warunek z `if` jest fałszywy, więc program zawsze wybiera dokładnie jedną z dwóch dróg.
- `and` wymaga prawdziwości obu warunków, a `or` wystarczy jeden prawdziwy, żeby całość dała `True`.

## Pytania sprawdzające

### 26. Jakie podstawowe działania matematyczne może wykonać program?

<details>
<summary>Odpowiedź</summary>

Program potrafi dodawać, odejmować, mnożyć i dzielić, a także dzielić całkowicie, liczyć resztę z dzielenia i potęgować. Zapisuje się je operatorami `+`, `-`, `*`, `/`, `//`, `%` i `**`. Kolejność działań jest taka jak w szkole, a nawiasy ją zmieniają. Operatory `+` i `*` działają też na tekście, ale wtedy sklejają i powtarzają.

Zobacz: [sekcja „Wykonuj działania matematyczne”](#wykonuj-działania-matematyczne).

</details>

### 27. Jak program łączy ze sobą teksty?

<details>
<summary>Odpowiedź</summary>

Program łączy teksty operatorem `+`, który skleja je w jednym napisie dokładnie tak, jak podano, bez dodawania spacji. Sklejać można tylko tekst z tekstem, więc liczbę trzeba najpierw zamienić na tekst funkcją `str()`. Wygodną alternatywą jest zapis z literą `f` przed cudzysłowem i nazwami w nawiasach klamrowych.

Zobacz: [sekcja „Połącz kilka tekstów”](#połącz-kilka-tekstów).

</details>

### 28. Jak program porównuje dwie wartości?

<details>
<summary>Odpowiedź</summary>

Program porównuje dwie wartości operatorami takimi jak `==`, `!=`, `<`, `>`, `<=` i `>=`. Każde porównanie daje wynik `True` albo `False`. Podwójny `==` pyta o równość, a pojedynczy `=` zapisuje wartość w zmiennej. Porównanie jest ścisłe: różni się wielkość liter, a tekst `"45.5"` nie jest równy liczbie 45.5.

Zobacz: [sekcja „Porównaj dwie wartości”](#porównaj-dwie-wartości).

</details>

### 29. Czym jest instrukcja warunkowa „jeśli… to…”?

<details>
<summary>Odpowiedź</summary>

Instrukcja warunkowa to polecenie, które wykonuje wskazany fragment kodu tylko wtedy, gdy warunek jest prawdziwy. W Pythonie zapisuje się ją jako `if`, warunek i dwukropek, a należące do niej linie oznacza się wcięciem. Gdy warunek jest fałszywy, Python pomija te linie i wykonuje dalszy kod.

Zobacz: [sekcja „Zapisz warunek z if”](#zapisz-warunek-z-if).

</details>

### 30. Do czego służy część „w przeciwnym razie”?

<details>
<summary>Odpowiedź</summary>

Część „w przeciwnym razie” (`else`) wykonuje się wtedy, gdy warunek z `if` jest fałszywy. Dzięki niej program wybiera jedną z dwóch dróg: albo blok pod `if`, albo blok pod `else`. Nigdy oba naraz i nigdy żaden.

Zobacz: [sekcja „Dodaj drugą drogę”](#dodaj-drugą-drogę).

</details>

### 31. Do czego służą operatory „i” oraz „lub”?

<details>
<summary>Odpowiedź</summary>

Operator `and` („i”) daje `True` tylko wtedy, gdy oba łączone warunki są prawdziwe. Operator `or` („lub”) daje `True`, gdy prawdziwy jest choć jeden z nich. Dzięki temu program może sprawdzić kilka rzeczy naraz i podjąć jedną decyzję w `if`.

Zobacz: [sekcja „Łącz warunki spójnikami”](#łącz-warunki-spójnikami).

</details>
