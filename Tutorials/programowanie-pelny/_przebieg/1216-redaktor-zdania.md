# Krok 1216 · redaktor_zdania

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem tutorialu: Programowanie od podstaw. W sekcji padła obietnica, której tutorial nie spełnił:
fraza „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” (własny plik funkcje.py, w którym czytelnik zobaczy błąd).

Podaj w old całe zdanie z tą obietnicą, dokładnie jak w tekście, a w new to samo zdanie bez obietnicy (zachowaj resztę sensu).
Jeśli zdanie jest samą zapowiedzią, new zostaw puste.

SEKCJA "Czym są argumenty funkcji":
[[argument-funkcji|Argumenty]] to dane, które przekazujesz funkcji w nawiasach przy wywołaniu, żeby miała na czym pracować. Funkcja bez argumentów robi zawsze to samo, a z argumentami to samo działanie wykonuje na różnych danych.

W definicji funkcji nazwy w nawiasach to [[parametr|parametry]]: puste miejsca, które funkcja wypełnia przy każdym wywołaniu. W `na_osobe(suma, osoby)` są dwa: `suma` i `osoby`. Wartości, które wpisujesz przy wywołaniu, to argumenty. Python przypisuje je parametrom tak samo jak przy przypisaniu: pierwszy argument trafia do pierwszego parametru, drugi do drugiego.

```python
def na_osobe(suma, osoby):
    return suma / osoby

print(na_osobe(300, 4))
print(na_osobe(osoby=4, suma=300))
```

```text
75.0
75.0
```

Pierwsze wywołanie podaje argumenty według kolejności. Drugie podaje je z nazwą, więc kolejność nie gra roli, a zapis mówi wprost, co oznacza każda liczba.

Liczba argumentów musi zgadzać się z liczbą parametrów. Wywołanie `na_osobe(300)` kończy się komunikatem [[typeerror|`TypeError`]]. To nazwa błędu, który Python zgłasza, gdy coś zrobiono w niewłaściwy sposób; tu znaczy: funkcję wywołano bez wartości dla `osoby`. Czytanie takich komunikatów omówimy przy błędach.

Kolejność też ma znaczenie: `na_osobe(4, 300)` da wynik bez błędu, ale zły, bo 4 zł podzielisz na 300 osób. U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`.
````

## Odpowiedź

````json
{
  "old": "U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`.",
  "new": ""
}
````
