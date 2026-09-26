# Krok 0735 · strażnik_warsztat

Węzeł: `review` · dział: 7 · pytanie: 39 · próba: 1

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
--- funkcje.py ---
# funkcje.py - pierwsza funkcja Wspólnej Kasy
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

print(suma([45.5, 20, 12.5]))

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
print(kwoty_wydatkow[0])
print(kwoty_wydatkow[-1])
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
1. plik funkcje.py (Dopisujemy drugą funkcję i używamy obu dla dwóch wyjazdów) zmiana:
 
-print(suma([45.5, 20, 12.5]))
+def na_osobe(suma, osoby):
+    return suma / osoby
+
+mazury = [45.5, 20, 12.5]
+tatry = [300, 150]
+print("Mazury:", na_osobe(suma(mazury), 3))
+print("Tatry:", na_osobe(suma(tatry), 4))
2. polecenie ():
$ python funkcje.py
podany wynik:
Mazury: 26.0
Tatry: 112.5

SEKCJA "Po co dzielić program na funkcje":
Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach.

Zobacz to na „Wspólnej Kasie”. Sumę wydatków wydzieliliśmy już do funkcji, a teraz dokładamy drugą, która z niej korzysta:

```python
def suma_wydatkow(wydatki):
    suma = 0
    for wydatek in wydatki:
        suma = suma + wydatek["kwota"]
    return suma

def udzial_na_osobe(wydatki, liczba_osob):
    return suma_wydatkow(wydatki) / liczba_osob

mazury = [{"kto": "Ania", "kwota": 120.5}, {"kto": "Bartek", "kwota": 79.5}]
tatry = [{"kto": "Celina", "kwota": 450}]
print(udzial_na_osobe(mazury, 2))
print(udzial_na_osobe(tatry, 3))
```

```text
100.0
150.0
```

Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz. Gdyby liczenie sumy trzeba było kiedyś zmienić, poprawiasz jedną funkcję, a oba wyniki będą poprawne.

Druga korzyść to czytelność: `udzial_na_osobe(mazury, 2)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, do czego wrócimy przy testowaniu programu.

U siebie masz już `funkcje.py` z jedną funkcją. Za chwilę dopiszesz drugą i użyjesz obu dla dwóch wyjazdów.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "detail": "Kod w tekście sekcji nie zgadza się z krokami czytelnika. Sekcja używa funkcji `suma_wydatkow` i `udzial_na_osobe`, a plik czytelnika ma `suma` i `na_osobe`. Sekcja podaje wyjazdy jako listy słowników (`{\"kto\": ..., \"kwota\": ...}`, `wydatek[\"kwota\"]`), a czytelnik ma zwykłe listy liczb (`[45.5, 20, 12.5]`). Słowniki nie zostały wcześniej wprowadzone. Wyniki też się różnią: sekcja podaje 100.0 i 150.0, a krok 2 wypisuje `Mazury: 26.0` i `Tatry: 112.5`. Popraw przykład w tekście tak, żeby był tym samym kodem co w kroku 1: `def suma(wydatki): ...`, `def na_osobe(suma, osoby): return suma / osoby`, `mazury = [45.5, 20, 12.5]`, `tatry = [300, 150]`, `print(\"Mazury:\", na_osobe(suma(mazury), 3))`, `print(\"Tatry:\", na_osobe(suma(tatry), 4))`. Blok wyniku ma wtedy brzmieć `Mazury: 26.0` i `Tatry: 112.5`. Wywołanie w zdaniu o czytelności zmień na `na_osobe(suma(mazury), 3)`. Nie wprowadzaj słowników.",
      "target": "Przykład kodu i wyniku w sekcji",
      "severity": "blokująca"
    },
    {
      "kind": "spójność",
      "detail": "Zdanie „Sumę wydatków wydzieliliśmy już do funkcji, a teraz dokładamy drugą, która z niej korzysta” jest prawdziwe tylko po zmianie przykładu na kod z kroku 1. Wtedy druga funkcja `na_osobe` dostaje wynik `suma(...)` jako argument. Nie wywołuje `suma` w środku, więc doprecyzuj: „druga dzieli wynik pierwszej”.",
      "target": "Zdanie o drugiej funkcji",
      "severity": "sugestia"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "W `na_osobe(suma, osoby)` parametr `suma` ma taką samą nazwę jak funkcja `suma`. Działa to poprawnie, bo wewnątrz `na_osobe` nazwa oznacza liczbę. Początkującego może to jednak zmylić. Rozważ nazwę parametru `razem` (`def na_osobe(razem, osoby): return razem / osoby`).",
      "target": "krok 1, def na_osobe",
      "severity": "sugestia"
    }
  ]
}
````
