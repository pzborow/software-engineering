# Krok 0937 · strażnik_warsztat

Węzeł: `review` · dział: 8 · pytanie: 48 · próba: 1

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
# pytaj.py - Wspólna Kasa pyta o wydatek
kto = input("Kto zapłacił? ")
kwota = float(input("Ile zapłacił? "))
print(f"Zapisano: {kto}, {kwota} zł")
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik interfejs.py (Nowy plik z opisanym wyjściem programu.) nowy plik:
# interfejs.py - Wspólna Kasa pokazuje czytelne podsumowanie
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)

2. polecenie (Uruchamiamy i oglądamy interfejs.):
$ python interfejs.py
podany wynik:
=== Wspólna Kasa ===
Ania: 120.5 zł
Bartek: 45.5 zł

SEKCJA "Czym jest interfejs użytkownika":
[[interfejs-uzytkownika|Interfejs użytkownika]] to część programu, przez którą człowiek się z nim komunikuje: to, co program wyświetla, oraz sposób, w jaki przyjmuje od człowieka dane i polecenia. Użytkownik nie widzi kodu, widzi tylko interfejs.

Interfejs bywa różny. W [[interfejs-tekstowy|interfejsie tekstowym]], czyli takim, który działa w [[terminal|terminalu]] na samych napisach, program zadaje pytania, a Ty odpisujesz z klawiatury. W interfejsie graficznym są okna i przyciski. Nasza „Wspólna Kasa” zostaje przy wersji tekstowej, bo wystarczą do niej dwie znane już rzeczy: [[input|input]] do pytań i [[print|print]] do wyników.

Interfejs ma dwie strony: **wejście** (pytania, odpowiedzi) i **wyjście** (wyniki, komunikaty). To dokładnie [[dane-wejsciowe|dane wejściowe]] i [[dane-wyjsciowe|dane wyjściowe]], tylko widziane oczami człowieka. Stąd wniosek z wcześniejszych sekcji: suchy wynik nic nie mówi komuś, kto nie zna kodu, więc trzeba go opisać.

```python
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```

```text
=== Wspólna Kasa ===
Ania: 120.5 zł
Bartek: 45.5 zł
```

Konsekwencja: pytanie w rodzaju „Ile zapłacił? ” i czytelne podsumowanie to nie ozdoby, tylko część działania programu. Interfejs trzeba więc projektować, a człowiek po drugiej stronie potrafi wpisać coś nieoczekiwanego.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "Kod używa słowników ({\"kto\": ..., \"kwota\": ...}) i odczytu wartości przez wydatek['kto'], a w dotychczasowych plikach ich nie było. Dodaj jedno zdanie: nawiasy {} grupują dane pod nazwami (kto, opis, kwota), a wydatek['kto'] wyciąga wartość o tej nazwie. Można też dopisać, że pole „opis” na razie nie jest używane. Kod działa, a wynik jest poprawny.",
      "severity": "sugestia",
      "target": "interfejs.py / wydatki (słownik)"
    }
  ]
}
````
