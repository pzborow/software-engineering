# Krok 0970 · strażnik_warsztat

Węzeł: `review` · dział: 9 · pytanie: 50 · próba: 1

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
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik blad_skladni.py (Zapisujemy skrypt z celowym błędem składni.) nowy plik:
# blad_skladni.py - błąd składni: brakuje dwukropka
kwota = 45.5
if kwota > 40
    print("Kwota do sprawdzenia")

2. polecenie (Python odmawia startu i wskazuje linię 3.) [CELOWY BŁĄD]:
$ python blad_skladni.py
podany wynik:
  File "blad_skladni.py", line 3
    if kwota > 40
                 ^
SyntaxError: expected ':'
3. plik blad_logiczny.py (Skrypt bez błędu składni, ale z błędem w pomyśle: osoby są trzy.) nowy plik:
# blad_logiczny.py - zły dzielnik: poprawny zapis, zły wynik
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)

4. polecenie (Brak komunikatu, a wynik zły (powinno być 26.0).):
$ python blad_logiczny.py
podany wynik:
Na osobę: 39.0

SEKCJA "Błąd składni a błąd logiczny":
Błąd składni łamie zasady zapisu, więc Python zatrzymuje się, zanim cokolwiek wykona. Błąd logiczny ma zapis poprawny, ale robi coś innego, niż zamierzałeś, więc program działa i po cichu podaje zły wynik.

[[blad-skladni|Błąd składni]] to naruszenie [[skladnia|składni]] języka, czyli reguł zapisu: brakujący dwukropek po `if`, niedomknięty cudzysłów, źle wcięta linia. Python czyta cały plik przed startem i takiego zapisu nie rozumie, więc nie wykona nawet linii przed błędem. Komunikat wskazuje linię i miejsce.

[[blad-logiczny|Błąd logiczny]] to pomyłka w pomyśle: zły wzór, zły dzielnik, zły warunek. Python nie ma jak jej zauważyć, bo każda instrukcja jest poprawna. Widzisz go tylko wtedy, gdy porównasz wynik z tym, czego się spodziewałeś.

| | Błąd składni | Błąd logiczny |
|---|---|---|
| Kiedy wychodzi | przed startem programu | w trakcie i po nim |
| Komunikat | jest, ze wskazaną linią | brak |
| Kto go znajduje | Python | Ty |

Trzy osoby dzielą wydatki 45.5, 20 i 12.5 zł:

```python
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)
```

```text
Na osobę: 39.0
```

Program nie zgłasza żadnego problemu, a wynik jest zły: powinno być 26.0, bo osoby są trzy. Podobnie działał zły wpis `-5` z poprzedniej sekcji: brak komunikatu, zły wynik. Konsekwencja: błędy składni są uciążliwe, ale łatwe, bo Python je wskaże. Za błędy logiczne odpowiadasz Ty, dlatego wynik zawsze sprawdzaj z rachunkiem na kartce. Jak czytać komunikaty i szukać takich błędów, omówimy osobno, w dalszych sekcjach tego działu.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "severity": "blokująca",
      "target": "zdanie „Podobnie działał zły wpis `-5` z poprzedniej sekcji”",
      "detail": "Odwołanie nie zgadza się ze stanem czytelnika. W pytaj.py funkcja sprawdz_kwote odrzuca „-5”, bo \"-5\".isdigit() daje False. Program wypisze wtedy „To nie jest poprawna kwota...” i zapyta ponownie. Nie będzie więc ani braku komunikatu, ani złego wyniku. Czytelnik, który wpisze -5, zobaczy coś przeciwnego niż w tekście. Zastąp to zdanie odwołaniem prawdziwym dla tego stanu, np. „Tak samo zachowałby się program, który przyjmuje dowolną kwotę bez sprawdzania: zapisałby złą wartość bez ostrzeżenia”. Możesz też po prostu usunąć to zdanie."
    }
  ]
}
````
