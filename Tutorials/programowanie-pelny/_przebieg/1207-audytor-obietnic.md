# Krok 1207 · audytor_obietnic

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem obietnic w tutorialu: Programowanie od podstaw. Wcześniej w tekście padła obietnica:
„U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” (własny plik funkcje.py, w którym czytelnik zobaczy błąd).
Czy ta sekcja ją spełnia? reference_id="ref-96", status spełniona | częściowo | brak, section_id="sec-07-zwracanie-wyniku-przez-funkcje",
quote = dokładny cytat (5-15 słów) z sekcji, który ją spełnia, explanation krótko.

SEKCJA [sec-07-zwracanie-wyniku-przez-funkcje] "Zwracanie wyniku przez funkcję":
Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał. Ta oddana wartość to [[wartosc-zwracana|wartość zwracana]]: wywołanie funkcji staje się w kodzie właśnie nią, więc możesz ją zapisać do zmiennej albo przekazać dalej.

Po `return` funkcja od razu kończy pracę. Nic, co stoi pod nim w ciele funkcji, już się nie wykona.

Zwracanie to nie to samo co wypisywanie. `print` tylko pokazuje tekst na ekranie, a program nie dostaje z niego nic do dalszej pracy. Funkcja bez `return` oddaje specjalną wartość [[none|`None`]], czyli „nic”.

```python
def na_osobe(suma, osoby):
    return suma / osoby

def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wynik = na_osobe(300, 4)
nic = wypisz_na_osobe(300, 4)
print(wynik)
print(nic)
```

```text
75.0
75.0
None
```

Pierwsza `75.0` pochodzi z `print` wewnątrz `wypisz_na_osobe`, w chwili wywołania. Druga to `wynik`, czyli wartość zwrócona i zapisana. Zmienna `nic` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła. Nazwy `wynik` i `nic` służą tylko tej ilustracji.

Konsekwencja jest praktyczna: tylko zwrócony wynik da się wykorzystać dalej. Dlatego `na_osobe(suma(mazury), 3)` działa: wynik jednej funkcji trafia jako argument do drugiej.
````

## Odpowiedź

````json
{
  "reference_id": "ref-96",
  "status": "brak",
  "section_id": "sec-07-zwracanie-wyniku-przez-funkcje",
  "explanation": "Sekcja nie pokazuje ani nie wywołuje żadnego TypeError. Przykład kończy się poprawnie (75.0, 75.0, None), a w tekście nie ma polecenia uruchomienia własnego funkcje.py, w którym czytelnik zobaczy błąd. Nie ma też mowy o próbie użycia None w obliczeniach, która by go wywołała."
}
````
