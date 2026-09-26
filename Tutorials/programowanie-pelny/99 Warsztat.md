# Warsztat: Wspólna Kasa krok po kroku

Czytelnik buduje u siebie w terminalu mały program w Pythonie do rozliczania wspólnych wydatków znajomych na wyjeździe. Program rośnie od pierwszego „Hello” do wersji z plikiem, funkcjami i testami.

**Dokąd zmierza:** Czytelnik zaczyna od sprawdzenia, że Python działa, i pisze pierwszy skrypt. Potem wprowadza dane o wydatkach, liczy sumy i decyzje, dodaje pętle po liście, wydziela funkcje, wczytuje dane z pliku i od użytkownika. Na końcu program sprawdza dane, ma testy i wersje w git, a czytelnik widzi, jak go rozbudować lub zautomatyzować.

**Punkt startowy:** Dowolny system (Windows, macOS lub Linux) z terminalem (PowerShell, bash lub zsh), zainstalowany Python 3.13 (sprawdzenie: python --version, na macOS/Linux ewentualnie python3 --version) oraz prosty edytor kodu, np. VS Code lub Notatnik. Pusty katalog roboczy ~/wspolna_kasa, w którym czytelnik otwiera terminal.

## Po dziale 03

Dział [03. Napisz i uruchom kod](03%20Napisz%20i%20uruchom%20kod.md): Czytelnik sprawdza python --version, zapisuje w edytorze plik kasa.py z jednym print i komentarzem, uruchamia go poleceniem python kasa.py, po czym celowo psuje nazwę print i ogląda pierwszy błąd.

- [Pisz kod w edytorze](03%20Napisz%20i%20uruchom%20kod.md#pisz-kod-w-edytorze): `python --version`; plik `kasa.py`
- [Uruchom swój program](03%20Napisz%20i%20uruchom%20kod.md#uruchom-swój-program): `python kasa.py`
- [Rozpoznaj błąd w programie](03%20Napisz%20i%20uruchom%20kod.md#rozpoznaj-błąd-w-programie): plik `kasa.py`; `python kasa.py` (celowy błąd)
- [Opisuj kod komentarzami](03%20Napisz%20i%20uruchom%20kod.md#opisuj-kod-komentarzami): plik `kasa.py`; `python kasa.py`

Stan plików na koniec działu:

<details>
<summary><code>kasa.py</code></summary>

```
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
```

</details>

## Po dziale 04

Dział [04. Zapamiętaj dane w zmiennych](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md): W kasa.py pojawiają się zmienne: nazwa wyjazdu (tekst), kwota wydatku (liczba) i czy_oplacone (prawda/fałsz), wypisywane razem z typami przez type().

- [Wyobraź sobie pudełko z etykietą](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#wyobraź-sobie-pudełko-z-etykietą): plik `kasa.py`; `python kasa.py`
- [Rozróżnij liczbę i tekst](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#rozróżnij-liczbę-i-tekst): plik `kasa.py`; `python kasa.py` (celowy błąd)
- [Sprawdź typ danych](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#sprawdź-typ-danych): plik `kasa.py`; `python kasa.py`
- [Użyj prawdy i fałszu](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#użyj-prawdy-i-fałszu): plik `kasa.py`; `python kasa.py`

Stan plików na koniec działu:

<details>
<summary><code>kasa.py</code></summary>

```
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
```

</details>

## Po dziale 05

Dział [05. Podejmuj decyzje w programie](05%20Podejmuj%20decyzje%20w%20programie.md): Program liczy koszt na osobę (dzielenie kwoty przez liczbę osób), skleja teksty w zdanie i za pomocą if/else oraz operatorów and/or ocenia, czy wydatek jest duży.

- [Wykonuj działania matematyczne](05%20Podejmuj%20decyzje%20w%20programie.md#wykonuj-działania-matematyczne): plik `kasa.py`; `python kasa.py`
- [Połącz kilka tekstów](05%20Podejmuj%20decyzje%20w%20programie.md#połącz-kilka-tekstów): plik `kasa.py`; `python kasa.py` (celowy błąd); plik `kasa.py`; `python kasa.py`
- [Porównaj dwie wartości](05%20Podejmuj%20decyzje%20w%20programie.md#porównaj-dwie-wartości): plik `kasa.py`; `python kasa.py`
- [Zapisz warunek z if](05%20Podejmuj%20decyzje%20w%20programie.md#zapisz-warunek-z-if): plik `kasa.py`; `python kasa.py`
- [Dodaj drugą drogę](05%20Podejmuj%20decyzje%20w%20programie.md#dodaj-drugą-drogę): plik `kasa.py`; `python kasa.py`
- [Łącz warunki spójnikami](05%20Podejmuj%20decyzje%20w%20programie.md#łącz-warunki-spójnikami): plik `kasa.py`; `python kasa.py`

Stan plików na koniec działu:

<details>
<summary><code>kasa.py</code></summary>

```
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

## Po dziale 06

Dział [06. Powtarzaj i zbieraj dane](06%20Powtarzaj%20i%20zbieraj%20dane.md): Wydatki trafiają do listy, a pętla for wypisuje je wszystkie, sumuje i wybiera pierwszy oraz ostatni element; czytelnik widzi też, jak wygląda while bez warunku zakończenia i zatrzymuje go Ctrl+C.

- [Powtórz kod pętlą](06%20Powtarzaj%20i%20zbieraj%20dane.md#powtórz-kod-pętlą): plik `kasa.py`; `python kasa.py`
- [Unikaj pętli nieskończonej](06%20Powtarzaj%20i%20zbieraj%20dane.md#unikaj-pętli-nieskończonej): plik `nieskonczona.py`; `python nieskonczona.py`
- [Wybierz element z listy](06%20Powtarzaj%20i%20zbieraj%20dane.md#wybierz-element-z-listy): plik `kasa.py`; `python kasa.py`

Stan plików na koniec działu:

<details>
<summary><code>kasa.py</code></summary>

```
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

<details>
<summary><code>nieskonczona.py</code></summary>

```
# nieskonczona.py - pętla, która nigdy się nie kończy
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

</details>

## Po dziale 07

Dział [07. Uporządkuj kod funkcjami](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md): Kod jest dzielony na funkcje suma(wydatki) i na_osobe(suma, osoby) z argumentami i wartością zwracaną oraz czytelnymi nazwami, a funkcje są używane ponownie dla dwóch różnych wyjazdów.

- [Zdefiniuj i wywołaj funkcję](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#zdefiniuj-i-wywołaj-funkcję): plik `funkcje.py`; `python funkcje.py`
- [Podziel program na funkcje](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#podziel-program-na-funkcje): plik `funkcje.py`; `python funkcje.py`
- [Przekaż funkcji argumenty](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#przekaż-funkcji-argumenty): plik `funkcje.py`; `python funkcje.py` (celowy błąd)
- [Wykorzystaj kod ponownie](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#wykorzystaj-kod-ponownie): plik `funkcje.py`; `python funkcje.py`

Stan plików na koniec działu:

<details>
<summary><code>funkcje.py</code></summary>

```
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

<details>
<summary><code>kasa.py</code></summary>

```
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

<details>
<summary><code>nieskonczona.py</code></summary>

```
# nieskonczona.py - pętla, która nigdy się nie kończy
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

</details>

## Po dziale 08

Dział [08. Porozmawiaj z użytkownikiem](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md): Program pyta użytkownika przez input() o imię i kwotę, zapisuje wydatki do pliku wydatki.txt i wczytuje je z powrotem, a błędnie wpisaną kwotę (np. tekst) odrzuca z komunikatem i ponownym pytaniem.

- [Zapytaj użytkownika o dane](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapytaj-użytkownika-o-dane): plik `pytaj.py`; `python pytaj.py`
- [Zapisz dane w pliku](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapisz-dane-w-pliku): plik `plik.py`; `python plik.py`
- [Zaprojektuj jasny interfejs](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zaprojektuj-jasny-interfejs): plik `interfejs.py`; `python interfejs.py`
- [Weryfikuj wpisane dane](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#weryfikuj-wpisane-dane): plik `pytaj.py`; `python pytaj.py`

Stan plików na koniec działu:

<details>
<summary><code>funkcje.py</code></summary>

```
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

<details>
<summary><code>interfejs.py</code></summary>

```
# interfejs.py - Wspólna Kasa pokazuje czytelne podsumowanie
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```

</details>

<details>
<summary><code>kasa.py</code></summary>

```
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

<details>
<summary><code>nieskonczona.py</code></summary>

```
# nieskonczona.py - pętla, która nigdy się nie kończy
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

</details>

<details>
<summary><code>plik.py</code></summary>

```
# plik.py - Wspólna Kasa zapisuje wydatki do pliku i wczytuje je z powrotem
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")
```

</details>

<details>
<summary><code>pytaj.py</code></summary>

```
# pytaj.py - Wspólna Kasa pyta o wydatek i sprawdza kwotę
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

kto = input("Kto zapłacił? ")
tekst = input("Ile zapłacił? ")
while not sprawdz_kwote(tekst):
    print("To nie jest poprawna kwota. Wpisz liczbę większą od zera, np. 45.5")
    tekst = input("Ile zapłacił? ")
kwota = float(tekst)
print(f"Zapisano: {kto}, {kwota} zł")
```

</details>

## Po dziale 09

Dział [09. Oswój błędy w kodzie](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md): Czytelnik wywołuje błąd składni i błąd logiczny (np. dzielenie przez złą liczbę), czyta komunikat Traceback, dopisuje kilka testów z assert w test_kasa.py, debuguje przez print i zapisuje wersję w git (git init, git add, git commit).

- [Czytaj komunikat o błędzie](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#czytaj-komunikat-o-błędzie): plik `blad_pusta.py`; `python blad_pusta.py` (celowy błąd)
- [Przetestuj swój program](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#przetestuj-swój-program): plik `test_kasa.py`; `python test_kasa.py`
- [Wytrop błąd krok po kroku](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#wytrop-błąd-krok-po-kroku): plik `debug.py`; `python debug.py`; plik `debug.py`; `python debug.py`
- [Zapisuj wersje kodu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#zapisuj-wersje-kodu): `git --version`; `git config --global user.name "Twoje Imie"`; `git config --global user.email "ty@example.com"`; `git init -b main`; `git add funkcje.py test_kasa.py`; `git commit -m "Funkcje Wspolnej Kasy i testy"`

Stan plików na koniec działu:

<details>
<summary><code>blad_pusta.py</code></summary>

```
# blad_pusta.py - Traceback: dzielenie przez zero
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))
```

</details>

<details>
<summary><code>debug.py</code></summary>

```
# debug.py - szukanie przyczyny złego wyniku przez print
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
liczba_osob = 3
print("Mazury na osobę:", na_osobe(suma(mazury), liczba_osob))
```

</details>

<details>
<summary><code>funkcje.py</code></summary>

```
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

<details>
<summary><code>interfejs.py</code></summary>

```
# interfejs.py - Wspólna Kasa pokazuje czytelne podsumowanie
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```

</details>

<details>
<summary><code>kasa.py</code></summary>

```
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

<details>
<summary><code>nieskonczona.py</code></summary>

```
# nieskonczona.py - pętla, która nigdy się nie kończy
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

</details>

<details>
<summary><code>plik.py</code></summary>

```
# plik.py - Wspólna Kasa zapisuje wydatki do pliku i wczytuje je z powrotem
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")
```

</details>

<details>
<summary><code>pytaj.py</code></summary>

```
# pytaj.py - Wspólna Kasa pyta o wydatek i sprawdza kwotę
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

kto = input("Kto zapłacił? ")
tekst = input("Ile zapłacił? ")
while not sprawdz_kwote(tekst):
    print("To nie jest poprawna kwota. Wpisz liczbę większą od zera, np. 45.5")
    tekst = input("Ile zapłacił? ")
kwota = float(tekst)
print(f"Zapisano: {kto}, {kwota} zł")
```

</details>

<details>
<summary><code>test_kasa.py</code></summary>

```
# test_kasa.py - testy funkcji Wspólnej Kasy
from funkcje import suma, na_osobe

assert suma([45.5, 20, 12.5]) == 78.0
assert suma([]) == 0
assert na_osobe(78.0, 3) == 26.0
assert na_osobe(0, 4) == 0
print("Wszystkie testy przeszły")
```

</details>

## Po dziale 10

Dział [10. Zastosuj wiedzę w praktyce](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md): Czytelnik dopisuje do Wspólnej Kasy jedną własną drobną funkcję, np. wypisanie, kto komu ile jest winien, i zapisuje ją jako kolejny commit, widząc w praktyce automatyzację prostego zadania.

- [Zacznij naukę od małego problemu](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md#zacznij-naukę-od-małego-problemu): plik `dlugi.py`; `python dlugi.py`; `git add dlugi.py`; `git commit -m "Dodaj funkcję wypisz_dlugi"`
- [Zautomatyzuj proste zadania](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md#zautomatyzuj-proste-zadania): `git --version`; `git init -b main`; `git config user.name "Twoje Imię" && git config user.email "ty@example.com"`; `git add dlugi.py && git commit -m "Dlugi: kto ile doplaca"`; plik `dlugi.py`; `python dlugi.py`; `git add dlugi.py && git commit -m "Naglowek rozliczenia"`

Stan plików na koniec działu:

<details>
<summary><code>blad_pusta.py</code></summary>

```
# blad_pusta.py - Traceback: dzielenie przez zero
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))
```

</details>

<details>
<summary><code>debug.py</code></summary>

```
# debug.py - szukanie przyczyny złego wyniku przez print
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
liczba_osob = 3
print("Mazury na osobę:", na_osobe(suma(mazury), liczba_osob))
```

</details>

<details>
<summary><code>dlugi.py</code></summary>

```
# dlugi.py - kto ile dopłaca, a kto dostaje
def wypisz_dlugi(wydatki, osoby):
    razem = 0
    for wydatek in wydatki:
        razem = razem + wydatek["kwota"]
    udzial = razem / len(osoby)
    for imie in osoby:
        zaplacil = 0
        for wydatek in wydatki:
            if wydatek["kto"] == imie:
                zaplacil = zaplacil + wydatek["kwota"]
        saldo = zaplacil - udzial
        if saldo < 0:
            print(f"{imie} dopłaca {-saldo} zł")
        else:
            print(f"{imie} dostaje {saldo} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.0},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.0},
           {"kto": "Celina", "opis": "bilety", "kwota": 15.0}]
osoby = ["Ania", "Bartek", "Celina"]
print("=== Rozliczenie ===")
wypisz_dlugi(wydatki, osoby)
```

</details>

<details>
<summary><code>funkcje.py</code></summary>

```
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

<details>
<summary><code>interfejs.py</code></summary>

```
# interfejs.py - Wspólna Kasa pokazuje czytelne podsumowanie
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```

</details>

<details>
<summary><code>kasa.py</code></summary>

```
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

<details>
<summary><code>nieskonczona.py</code></summary>

```
# nieskonczona.py - pętla, która nigdy się nie kończy
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

</details>

<details>
<summary><code>plik.py</code></summary>

```
# plik.py - Wspólna Kasa zapisuje wydatki do pliku i wczytuje je z powrotem
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")
```

</details>

<details>
<summary><code>pytaj.py</code></summary>

```
# pytaj.py - Wspólna Kasa pyta o wydatek i sprawdza kwotę
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

kto = input("Kto zapłacił? ")
tekst = input("Ile zapłacił? ")
while not sprawdz_kwote(tekst):
    print("To nie jest poprawna kwota. Wpisz liczbę większą od zera, np. 45.5")
    tekst = input("Ile zapłacił? ")
kwota = float(tekst)
print(f"Zapisano: {kto}, {kwota} zł")
```

</details>

<details>
<summary><code>test_kasa.py</code></summary>

```
# test_kasa.py - testy funkcji Wspólnej Kasy
from funkcje import suma, na_osobe

assert suma([45.5, 20, 12.5]) == 78.0
assert suma([]) == 0
assert na_osobe(78.0, 3) == 26.0
assert na_osobe(0, 4) == 0
print("Wszystkie testy przeszły")
```

</details>
