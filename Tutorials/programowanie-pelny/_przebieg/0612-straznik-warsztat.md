# Krok 0612 · strażnik_warsztat

Węzeł: `review` · dział: 6 · pytanie: 34 · próba: 1

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
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik nieskonczona.py (Osobny plik z pętlą while, która nigdy się nie kończy) nowy plik:
# nieskonczona.py - pętla bez końca, tylko do obejrzenia
import time
while True:
    print("Liczę wydatki...")
    time.sleep(0.5)

2. polecenie (Po kilku liniach naciśnij Ctrl+C; ścieżka w komunikacie będzie u Ciebie inna):
$ python nieskonczona.py
podany wynik:
Liczę wydatki...
Liczę wydatki...
Liczę wydatki...
^CTraceback (most recent call last):
  File "/home/ty/wspolna_kasa/nieskonczona.py", line 5, in <module>
    time.sleep(0.5)
    ~~~~~~~~~~^^^^^
KeyboardInterrupt

SEKCJA "Pętla nieskończona":
[[petla-nieskonczona|Pętla nieskończona]] to pętla, która nigdy nie dochodzi do końca, bo jej [[warunek-zakonczenia|warunek zakończenia]] nigdy nie zostaje spełniony. Program powtarza wtedy ten sam fragment bez końca, więc nie dociera do dalszych linii i nie oddaje wyniku.

Pętla `for`, którą znasz, kończy się sama, bo zestaw danych się wyczerpuje. Pętla `while` („dopóki”) działa inaczej: powtarza wcięte linie, dopóki warunek daje `True`. Jeśli warunek jest zawsze prawdziwy, każda kolejna [[iteracja|iteracja]] zaczyna się od nowa.

```python
while True:
    print("Liczę wydatki...")
    ...
```

Tu warunek to na stałe `True`, a w ciele nic go nie zmienia. Zdarza się to też przez pomyłkę: warunek zależy od zmiennej, której pętla nigdy nie zmienia.

Problem jest praktyczny. Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków. Tak samo wyglądałaby „Wspólna Kasa”, która czeka na koniec listy, którego nie ma.

Zatrzymasz taki program skrótem Ctrl+C w terminalu. Python przerywa wtedy działanie i wypisuje komunikat `KeyboardInterrupt`, czyli „przerwano z klawiatury”. To nie awaria, tylko Twoja komenda.

Dlatego przy każdej pętli `while` zadaj sobie pytanie: co sprawi, że warunek w końcu stanie się fałszywy?
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "detail": "Zdanie „zajmuje procesor” nie zgadza się z przykładem: dzięki time.sleep(0.5) ten skrypt prawie nie obciąża procesora. Popraw np. na: „Program wygląda na zawieszony i nigdy nie pokaże sumy wydatków (bez pauzy w pętli zająłby też cały procesor).”",
      "severity": "sugestia",
      "target": "akapit „Problem jest praktyczny”"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Plik zawiera import time i time.sleep(0.5), których tekst nie tłumaczy. Dodaj jedno zdanie: „time.sleep(0.5) robi pół sekundy przerwy, żeby napisy nie zalały ekranu; sama pętla działałaby tak samo bez niej.”",
      "severity": "sugestia",
      "target": "nieskonczona.py"
    },
    {
      "kind": "spójność",
      "detail": "Fragment kodu w tekście ma „...” w miejscu time.sleep(0.5), a plik go nie zawiera. Zastąp „...” linią `time.sleep(0.5)` albo dopisz, że „...” oznacza pominięty kod.",
      "severity": "sugestia",
      "target": "fragment kodu w sekcji"
    },
    {
      "kind": "przykład",
      "detail": "Zdanie o pętli zależnej od zmiennej, której nikt nie zmienia, nie ma przykładu. Dodaj krótki kod, np. `licznik = 0` i `while licznik < 3:` z samym `print(licznik)` w ciele, bez zwiększania licznika.",
      "severity": "sugestia",
      "target": "„Zdarza się to też przez pomyłkę”"
    }
  ]
}
````
