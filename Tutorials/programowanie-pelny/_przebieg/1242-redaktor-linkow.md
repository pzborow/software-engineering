# Krok 1242 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „Skoro kod jest zwykłym plikiem tekstowym” (kod źródłowy jako zwykły plik tekstowy).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-03-czym-jest-kod-zrodlowy]
Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to instrukcja zapisana według ścisłych reguł składni. Ten sam algorytm, który wcześniej opisywaliśmy słowami i schematem, tu dostaje zapis, którego nie da się zrozumieć na dwa sposoby.


2. [sec-02-czym-jest-algorytm]
```text
dane: lista wydatków (kto, ile) i liczba osób
1. Zsumuj wszystkie wydatki.
2. Podziel sumę przez liczbę osób: to udział jednej osoby.
3. Dla każdej osoby odejmij udział od tego, ile wydała.
4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna.
wynik: saldo każdej osoby
```
````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 wprost stwierdza, że kod źródłowy fizycznie jest zwykłym plikiem tekstowym, jak notatka czy lista zakupów. Miejsce 2 to tylko przykład algorytmu, a nie informacja o pliku tekstowym."
}
````
