# Krok 1205 · audytor_obietnic

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem obietnic w tutorialu: Programowanie od podstaw. Wcześniej w tekście padła obietnica:
„Za chwilę dopiszesz `na_osobe` i użyjesz obu” (zapowiedź ćwiczenia praktycznego z funkcją na_osobe).
Czy ta sekcja ją spełnia? reference_id="ref-93", status spełniona | częściowo | brak, section_id="sec-07-ponowne-uzycie-kodu",
quote = dokładny cytat (5-15 słów) z sekcji, który ją spełnia, explanation krótko.

SEKCJA [sec-07-ponowne-uzycie-kodu] "Ponowne użycie kodu":
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
  "reference_id": "ref-93",
  "status": "brak",
  "section_id": "sec-07-ponowne-uzycie-kodu",
  "quote": "",
  "explanation": "Sekcja tylko pokazuje gotowe funkcje i wspomina, że `na_osobe` jest w `funkcje.py`. Nie ma w niej ćwiczenia, w którym czytelnik dopisuje `na_osobe` i używa obu funkcji. Ćwiczenie zostało odsunięte do „warsztatu poniżej”, a tam sekcja tego nie zawiera."
}
````
