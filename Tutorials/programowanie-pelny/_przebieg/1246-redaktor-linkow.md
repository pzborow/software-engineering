# Krok 1246 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „omówimy w następnej sekcji” (typ danych).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-04-czym-jest-typ-danych]
Typ danych to rodzaj wartości, który mówi Pythonowi, czym ta wartość jest i jakie działania są na niej dozwolone. Wcześniej pisaliśmy po prostu „rodzaj danych”, teraz mamy na to fachową nazwę.


2. [sec-04-czym-jest-dana]
Dana to każda informacja, na której pracuje program: imię, kwota, data, odpowiedź „tak” lub „nie”. Program bez danych nie miałby czego liczyć ani wypisać.

W arkuszu kalkulacyjnym danymi są wartości w komórkach: nazwisko w jednej, kwota w drugiej. W programie jest podobnie, tylko że dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz.

```python
# poza kanonem
print("Ania")       # tekst: imię
print(45.5)         # liczba: kwota
print(True)         # prawda albo fałsz: czy zapłacono
print(45.5 + 10)    # z liczbą można liczyć
```

```text
Ania
45.5
True
55.5
```

Każda z tych tr
````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 zawiera definicję typu danych (rodzaj wartości, jakie działania są dozwolone), czyli to, co zapowiada zdanie. Miejsce 2 omawia pojęcie „dana”, a nie typ danych."
}
````
