# Krok 0456 · strażnik_warsztat

Węzeł: `review` · dział: 5 · pytanie: 26 · próba: 1

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
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik kasa.py (Dopisujemy dzielenie i mnożenie kwoty) zmiana:
 print(czy_oplacone)
+liczba_osob = 2
+koszt_na_osobe = kwota_wydatku / liczba_osob
+print(koszt_na_osobe)
+print(kwota_wydatku * 2)
2. polecenie ():
$ python kasa.py
podany wynik:
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>
False
22.75
91.0

SEKCJA "Działania matematyczne w programie":
Program wykonuje te same działania co kalkulator: dodawanie, odejmowanie, mnożenie i dzielenie, a do tego dzielenie całkowite, resztę z dzielenia i potęgowanie. Zapisujesz je za pomocą [[operator-arytmetyczny|operatorów arytmetycznych]], czyli znaków, które mówią Pythonowi, jakie działanie wykonać na liczbach.

| Działanie | Operator |
|---|---|
| dodawanie | `+` |
| odejmowanie | `-` |
| mnożenie | `*` |
| dzielenie | `/` |
| dzielenie całkowite | `//` |
| reszta z dzielenia | `%` |
| potęgowanie | `**` |

Mnożenie to gwiazdka, a nie „x”. Dzielenie `/` zawsze daje liczbę z częścią ułamkową. Dzielenie całkowite `//` zostawia samą część całkowitą, a `%` pokazuje, ile zostało. Przy dzieleniu kwoty między osoby to bardzo przydatne.

```python
kwota = 100
print(kwota + 20)
print(kwota - 20)
print(kwota * 2)
print(kwota / 3)
print(kwota // 3)
print(kwota % 3)
print(kwota ** 2)
```

```text
120
80
200
33.333333333333336
33
1
10000
```

Zwróć uwagę na wynik `33.333333333333336`. Komputer trzyma ułamki w przybliżeniu, więc na końcu bywa drobna nieścisłość. Kolejność działań jest jak w szkole: mnożenie i dzielenie przed dodawaniem, a nawiasy zmieniają porządek.

Konsekwencja: działania mają sens tylko na liczbach. Tekstu w rodzaju `"Ania"` nie podzielisz, co widzieliśmy przy typach danych.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "severity": "blokująca",
      "target": "Ostatnie zdania sekcji („działania mają sens tylko na liczbach…”)",
      "detail": "Błąd merytoryczny: w Pythonie `+` i `*` działają też na tekstach (`\"Ania\" + \"Kowalska\"` daje `AniaKowalska`, `\"Ha\" * 3` daje `HaHaHa`). Poprawka: zamień zdanie na np. „Operatory `-`, `/`, `//`, `%`, `**` mają sens tylko na liczbach. Tekstu w rodzaju `\"Ania\"` nie podzielisz (`\"Ania\" / 2` kończy się błędem `TypeError`), a `+` i `*` na tekście działają inaczej niż na liczbach”. Dodaj krótki przykład kodu z tą tezą.",
      "source": "Konsekwencja: działania mają sens tylko na liczbach."
    },
    {
      "kind": "spójność",
      "severity": "blokująca",
      "target": "Odwołanie „co widzieliśmy przy typach danych”",
      "detail": "W stanie czytelnika (kasa.py) nigdzie nie dzielono tekstu; czytelnik widział tylko `type(...)` zwracające `<class 'str'>`. Zdanie odwołuje się do czegoś, czego nie było. Usuń „co widzieliśmy przy typach danych” albo zastąp je zdaniem: „Wiemy już, że `nazwa_wyjazdu` jest tekstem (`str`), więc `nazwa_wyjazdu / 2` się nie uda”.",
      "source": "co widzieliśmy przy typach danych"
    },
    {
      "kind": "spójność",
      "severity": "sugestia",
      "target": "Zdanie o dzieleniu `/`",
      "detail": "„zawsze daje liczbę z częścią ułamkową” bywa mylące: `100 / 4` daje `25.0`, `kwota_wydatku * 2` w kasa.py daje `91.0`. Lepiej: „Dzielenie `/` zawsze daje liczbę ułamkową (typ `float`), np. `100 / 4` to `25.0`”.",
      "source": "Dzielenie `/` zawsze daje liczbę z częścią ułamkową."
    },
    {
      "kind": "spójność",
      "severity": "sugestia",
      "target": "Sekcja a kasa.py",
      "detail": "Tekst sekcji nie odwołuje się do kroków w kasa.py (`liczba_osob`, `koszt_na_osobe`, wyniki `22.75` i `91.0`). Dodaj zdanie wyjaśniające, że `45.5 / 2` daje `22.75` (koszt na osobę), a `45.5 * 2` daje `91.0`, oraz że wynik mnożenia float przez int to `float`.",
      "source": "krok 1"
    }
  ]
}
````
