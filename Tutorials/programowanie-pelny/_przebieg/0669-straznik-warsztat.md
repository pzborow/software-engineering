# Krok 0669 · strażnik_warsztat

Węzeł: `review` · dział: 6 · pytanie: 36 · próba: 2

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

--- nieskonczona.py ---
# nieskonczona.py - pętla, która nigdy się nie kończy
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik kasa.py (Dopisujemy wypisanie pierwszego i ostatniego wydatku z listy.) zmiana:
 print(suma)
+print(kwoty_wydatkow[0])
+print(kwoty_wydatkow[-1])
 print("Koniec")
2. polecenie (Uruchamiamy skrypt i sprawdzamy dwa nowe wiersze przed słowem Koniec.):
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

SEKCJA "Odczyt elementu listy":
Po element listy sięgasz przez jego numer w nawiasach kwadratowych: `osoby[0]`. Numer nazywa się [[indeks|indeksem]] i liczenie zaczyna się od zera, więc pierwszy element ma indeks 0, drugi 1, trzeci 2.

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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "spójność",
      "severity": "sugestia",
      "target": "Tekst sekcji vs krok 1",
      "detail": "Tekst tłumaczy indeksy na liście osoby, a krok dopisuje kwoty_wydatkow[0] i kwoty_wydatkow[-1]. Warto dodać jedno zdanie po kroku: pierwszy wydatek to 45.5, ostatni to 12.5, zgodnie z dwoma nowymi wierszami przed Koniec.",
      "source": "sekcja"
    },
    {
      "kind": "przykład",
      "severity": "sugestia",
      "target": "IndexError",
      "detail": "Błąd IndexError jest opisany, ale nie pokazany. Można dodać krótki przykład print(osoby[3]) z komunikatem: IndexError: list index out of range.",
      "source": "sekcja"
    },
    {
      "kind": "wyjaśnienie",
      "severity": "sugestia",
      "target": "Odczyt niczego nie zmienia",
      "detail": "Zdanie „dostajesz tylko kopię wartości” jest nieprecyzyjne. Lepiej: „dostajesz wartość tego elementu, a lista zostaje bez zmian”.",
      "source": "sekcja"
    }
  ]
}
````
