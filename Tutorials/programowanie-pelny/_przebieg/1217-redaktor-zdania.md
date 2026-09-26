# Krok 1217 · redaktor_zdania

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem tutorialu: Programowanie od podstaw. W sekcji padła obietnica, której tutorial nie spełnił:
fraza „Usuwamy ją w warsztacie poniżej.” (zapowiedź poprawienia błędnej ostatniej linii w warsztacie).

Podaj w old całe zdanie z tą obietnicą, dokładnie jak w tekście, a w new to samo zdanie bez obietnicy (zachowaj resztę sensu).
Jeśli zdanie jest samą zapowiedzią, new zostaw puste.

SEKCJA "Ponowne użycie kodu":
Ponowne użycie kodu to wykorzystanie tego samego fragmentu wiele razy zamiast pisania go od nowa. W Pythonie robisz to przez [[funkcja|funkcję]]: [[definicja-funkcji|definicję]] piszesz raz, a potem robisz dowolną liczbę [[wywolanie-funkcji|wywołań]] z innymi danymi.

Zobacz dwa wyjazdy liczone tą samą logiką:

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print(udzial_na_osobe(suma_wydatkow(mazury), 3))
print(udzial_na_osobe(suma_wydatkow(tatry), 4))
```

```text
26.0
112.5
```

Zmieniają się tylko dane: lista wydatków i liczba osób. Logika liczenia leży w jednym miejscu, więc nie kopiujesz pętli dla każdego wyjazdu.

Ma to dwie konsekwencje. Gdy znajdziesz błąd w liczeniu sumy, poprawiasz go raz i naprawiasz wszystkie wyjazdy naraz. A trzeci wyjazd to jedna nowa lista i dwa wywołania, bez nowego kodu.

Właśnie po to funkcje mają parametry: to, co stałe, zostaje w środku, a to, co zmienne, wchodzi z zewnątrz.

U siebie w `funkcje.py` masz te same funkcje (pod krótszymi nazwami `suma` i `na_osobe`). Ostatnia linia wywołuje `na_osobe(300)` z jednym argumentem zamiast dwóch, stąd błąd. Usuwamy ją w warsztacie poniżej.
````

## Odpowiedź

````json
{
  "old": "Usuwamy ją w warsztacie poniżej.",
  "new": ""
}
````
