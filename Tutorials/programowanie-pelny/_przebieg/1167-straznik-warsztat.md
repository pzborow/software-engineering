# Krok 1167 · strażnik_warsztat

Węzeł: `review` · dział: 10 · pytanie: 61 · próba: 1

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
--- blad_pusta.py ---
# blad_pusta.py - Traceback: dzielenie przez zero
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))

--- debug.py ---
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

--- dlugi.py ---
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
wypisz_dlugi(wydatki, osoby)

--- funkcje.py ---
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

--- interfejs.py ---
# interfejs.py - Wspólna Kasa pokazuje czytelne podsumowanie
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)

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

--- plik.py ---
# plik.py - Wspólna Kasa zapisuje wydatki do pliku i wczytuje je z powrotem
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")

--- pytaj.py ---
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

--- test_kasa.py ---
# test_kasa.py - testy funkcji Wspólnej Kasy
from funkcje import suma, na_osobe

assert suma([45.5, 20, 12.5]) == 78.0
assert suma([]) == 0
assert na_osobe(78.0, 3) == 26.0
assert na_osobe(0, 4) == 0
print("Wszystkie testy przeszły")
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. polecenie (Uruchamiamy funkcję, która liczy rozliczenie za nas):
$ python dlugi.py
podany wynik:
Ania dostaje 60.0 zł
Bartek dopłaca 15.0 zł
Celina dopłaca 45.0 zł
2. plik dlugi.py (Dopisujemy nagłówek, żeby wynik był czytelny) zmiana:
 def wypisz_dlugi(wydatki, osoby):
+    print("=== Rozliczenie ===")
     razem = 0
3. polecenie (Sprawdzamy, że zmiana działa):
$ python dlugi.py
podany wynik:
=== Rozliczenie ===
Ania dostaje 60.0 zł
Bartek dopłaca 15.0 zł
Celina dopłaca 45.0 zł
4. polecenie (Zapisujemy zmianę jako commit):
$ git add dlugi.py && git commit -m "Rozliczenie: nagłówek w wypisz_dlugi"
podany wynik:
[main 3f2a1c9] Rozliczenie: nagłówek w wypisz_dlugi
 1 file changed, 1 insertion(+)

SEKCJA "Automatyzacja prostych zadań":
[[automatyzacja|Automatyzacja]] to zlecenie komputerowi powtarzalnej czynności, którą wcześniej robiłeś(-aś) ręcznie. Osoba spoza IT zyskuje na niej czas i pewność: komputer nie nudzi się, nie myli przy setnej pozycji i robi to samo za każdym razem.

Mechanizm znasz: to [[petla|pętla]] i [[funkcja|funkcja]] na Twoich danych. Zamiast przepisywać kwoty do kalkulatora, opisujesz kroki raz, a program wykonuje je dla dowolnej liczby pozycji:

```python
faktury = [1000, 250, 50]
razem = 0
for kwota in faktury:
    razem = razem + kwota
vat = round(razem * 0.23, 2)
print(f"Netto: {razem} zł")
print(f"VAT 23%: {vat} zł")
print(f"Brutto: {razem + vat} zł")
```

```text
Netto: 1300 zł
VAT 23%: 299.0 zł
Brutto: 1599.0 zł
```

Jutro lista ma 200 faktur zamiast trzech, a kod zostaje ten sam. Podobnie działa Twój `dlugi.py`: raz opisany podział rachunku liczy się sam.

Nie automatyzuj wszystkiego. Opłaca się zadanie, które powtarzasz często, ma jasne reguły i da się sprawdzić na kartce. Zadanie robione raz w roku lub wymagające oceny człowieka zwykle lepiej zostawić sobie.

Konsekwencja jest praktyczna: zaczynasz od małego, nudnego zadania z własnej pracy i piszesz je tą samą pętlą nauki. Po commicie masz gotowe narzędzie, do którego możesz wracać.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "wynik",
      "severity": "blokująca",
      "target": "Krok 4: git add && git commit",
      "source": "stan czytelnika",
      "detail": "Punkt startowy nie obejmuje gita. W stanie nie ma repozytorium (brak `git init`) ani konfiguracji `user.name` i `user.email`, a git nie jest wymieniony jako zainstalowany. Bez tego `git add` zwróci `fatal: not a git repository`. Jeśli czytelnik zrobi `git init`, dlugi.py nie był wcześniej commitowany, więc podany wynik `1 file changed, 1 insertion(+)` jest nieprawdziwy. Pierwszy commit wypisze `[main (root-commit) <hash>] ...`, potem ` 1 file changed, 26 insertions(+)` i ` create mode 100644 dlugi.py`. Poprawka: przed krokiem 1 dodaj kroki instalacji i sprawdzenia gita (`git --version`), `git init -b main`, `git config user.name`/`user.email` oraz pierwszy commit dlugi.py bez nagłówka. Wtedy wynik kroku 4 (`1 file changed, 1 insertion(+)`) będzie poprawny. Alternatywnie zmień wynik kroku 4 na wersję z root-commit i 26 insertions. Hash jest zmienny, więc dodaj uwagę, że u czytelnika będzie inny."
    },
    {
      "kind": "spójność",
      "severity": "sugestia",
      "target": "Tekst sekcji: „pętla i funkcja”",
      "detail": "Tekst mówi, że mechanizmem jest pętla i funkcja, ale przykład z fakturami zawiera tylko pętlę, bez `def`. Dodaj funkcję (np. `def podsumuj(faktury):`) albo napisz, że w przykładzie użyto samej pętli."
    },
    {
      "kind": "wyjaśnienie",
      "severity": "sugestia",
      "target": "„pętla nauki” i „commit”",
      "detail": "Zwrot „tą samą pętlą nauki” oraz słowo „commit” pojawiają się bez definicji i bez odnośnika do glosariusza. Dodaj krótkie wyjaśnienie albo odnośnik."
    },
    {
      "kind": "przykład",
      "severity": "sugestia",
      "target": "Akapit „Nie automatyzuj wszystkiego”",
      "detail": "Kryteria opłacalności podano bez przykładu. Dodaj po jednym przykładzie: co się opłaca (miesięczne rozliczenie faktur) i co nie (decyzja, komu odpuścić dopłatę)."
    }
  ]
}
````
