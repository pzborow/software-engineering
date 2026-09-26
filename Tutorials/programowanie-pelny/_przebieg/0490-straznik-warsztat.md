# Krok 0490 · strażnik_warsztat

Węzeł: `review` · dział: 5 · pytanie: 27 · próba: 2

## Prompt

````text
Jesteś weryfikatorem warsztatu „Wspólna Kasa krok po kroku” w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.
Czytelnik wykonuje kroki u siebie dosłownie. Punkt startowy: Dowolny system (Windows, macOS lub Linux) z terminalem (PowerShell, bash lub zsh), zainstalowany Python 3.13 (sprawdzenie: python --version, na macOS/Linux ewentualnie python3 --version) oraz prosty edytor kodu, np. VS Code lub Notatnik. Pusty katalog roboczy ~/wspolna_kasa, w którym czytelnik otwiera terminal..

Wykonaj kroki w myślach na stanie poniżej i sprawdź:
1. Czy każde polecenie da się wykonać w tym stanie (pliki istnieją, narzędzia są w punkcie startowym albo zainstalowane wcześniej).
2. Czy podany wynik zgadza się znak w znak z tym, co naprawdę wypisze polecenie (wartości, zaokrąglenia, formatowanie,
   kolejność). Przy celowym błędzie: czy komunikat jest prawdziwy dla tego narzędzia i wersji.
3. Czy zmiany w plikach dotyczą tego, o czym mówi sekcja, bez przypadkowych zmian w innych miejscach.
4. Czy tekst sekcji zgadza się z krokami (nazwy plików, wartości, wyniki).
Każdy problem zgłoś jako kind="wynik" (zły albo brakujący wynik) lub "spójność" (reszta), target=krok albo plik,
detail=co się nie zgadza i DOKŁADNIE jak poprawić (poprawny wynik, poprawna linia). Błąd wykonania jest blokujący.
Nie żądaj usunięcia kroków: warsztat poprawiamy, nie odrzucamy.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

STAN U CZYTELNIKA PRZED SEKCJĄ:
```text
--- kasa.py ---
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
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik kasa.py (Dopisujemy sklejenie tekstu z liczbą) zmiana:
 print(kwota_wydatku % liczba_osob)
+print("Kwota: " + kwota_wydatku)
2. polecenie (Liczby nie da się dokleić do tekstu) [CELOWY BŁĄD]:
$ python kasa.py
podany wynik:
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
3. plik kasa.py (Zamieniamy liczbę na tekst i dodajemy zapis z f) zmiana:
 print(kwota_wydatku % liczba_osob)
-print("Kwota: " + kwota_wydatku)
+print("Kwota: " + str(kwota_wydatku) + " zł")
+print(f"Wyjazd: {nazwa_wyjazdu}, kwota: {kwota_wydatku} zł")
4. polecenie ():
$ python kasa.py
podany wynik:
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

SEKCJA "Łączenie tekstów":
Program łączy teksty operatorem `+`, który skleja je w jeden, dokładnie w takiej kolejności i z takimi znakami, jakie mu podasz. Ta operacja nazywa się [[konkatenacja|sklejaniem tekstów]] (konkatenacją). Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono.

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

Ten błąd możesz wywołać od razu: w warsztacie poniżej dopisujesz do swojego skryptu linię, która skleja tekst z liczbą.

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [wynik] krok 2, traceback: Podany wynik nie zgadza się znak w znak z tym, co wypisze Python 3.13. (1) Linia ze ścieżką: od Pythona 3.9 skrypt uruchomiony jako `python kasa.py` ma ścieżkę bezwzględną, więc czytelnik zobaczy `File "/…/wspolna_kasa/kasa.py", line 8, in <module>`, a nie `File "kasa.py"`. Podaj przykładową ścieżkę, np. `File "/home/ania/wspolna_kasa/kasa.py", line 8, in <module>`, i dopisz, że ścieżka u czytelnika będzie inna. (2) Podkreślenie pod wyrażeniem `"Kwota: " + kwota_wydatku` ma za dużo znaków `~`. Wyrażenie ma 25 znaków: 10 znaków przed `+` (`"Kwota: "` i spacja), `+` oraz 14 znaków po nim (spacja i `kwota_wydatku`). Poprawna linia: 10 spacji wcięcia, potem `~~~~~~~~~~^~~~~~~~~~~~~~~` (10 tyldek, `^`, 14 tyldek).
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "wynik",
      "target": "krok 2, traceback",
      "severity": "blokująca",
      "status": "niespełniona",
      "detail": "Podkreślenie nadal ma za dużo znaków ~. Wyrażenie `\"Kwota: \" + kwota_wydatku` ma 25 znaków, więc linia ma być: 10 spacji wcięcia, potem 10 tyldek, `^`, 14 tyldek: `          ~~~~~~~~~~^~~~~~~~~~~~~~`. Teraz po `^` stoi 15 tyldek.",
      "source": "uwaga 2 z poprzedniej recenzji"
    },
    {
      "kind": "wynik",
      "target": "krok 2, traceback",
      "severity": "blokująca",
      "status": "nowa",
      "detail": "Numer linii jest zły. Po dopisaniu nowa linia `print(\"Kwota: \" + kwota_wydatku)` jest w kasa.py linią 16 (poprzednia, `print(kwota_wydatku % liczba_osob)`, to linia 15). Popraw na `File \"/home/ania/wspolna_kasa/kasa.py\", line 16, in <module>`."
    },
    {
      "kind": "spójność",
      "target": "krok 2, traceback",
      "severity": "sugestia",
      "status": "niespełniona",
      "detail": "Ścieżka jest już bezwzględna, ale nigdzie nie napisano, że u czytelnika będzie inna (inny użytkownik, na Windows np. C:\\Users\\...\\wspolna_kasa\\kasa.py). Dopisz jedno zdanie przy kroku 2.",
      "source": "uwaga 1 z poprzedniej recenzji"
    }
  ]
}
````
