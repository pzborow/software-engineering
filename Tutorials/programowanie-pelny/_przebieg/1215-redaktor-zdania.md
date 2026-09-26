# Krok 1215 · redaktor_zdania

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem tutorialu: Programowanie od podstaw. W sekcji padła obietnica, której tutorial nie spełnił:
fraza „Za chwilę dopiszesz `na_osobe` i użyjesz obu” (zapowiedź ćwiczenia praktycznego z funkcją na_osobe).

Podaj w old całe zdanie z tą obietnicą, dokładnie jak w tekście, a w new to samo zdanie bez obietnicy (zachowaj resztę sensu).
Jeśli zdanie jest samą zapowiedzią, new zostaw puste.

SEKCJA "Po co dzielić program na funkcje":
Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach.

Zobacz to na „Wspólnej Kasie”. Funkcja `suma` już jest, więc dokładamy drugą, `na_osobe`, i używamy obu dla dwóch wyjazdów:

```python
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
```

```text
Mazury: 26.0
Tatry: 112.5
```

Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz. Gdyby liczenie sumy trzeba było kiedyś zmienić, poprawiasz jedną funkcję, a oba wyniki będą poprawne.

Druga korzyść to czytelność: `na_osobe(suma(mazury), 3)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, do czego wrócimy przy testowaniu programu.

U siebie masz już `funkcje.py` z funkcją `suma`. Za chwilę dopiszesz `na_osobe` i użyjesz obu dla dwóch wyjazdów.
````

## Odpowiedź

````json
{
  "old": "U siebie masz już `funkcje.py` z funkcją `suma`. Za chwilę dopiszesz `na_osobe` i użyjesz obu dla dwóch wyjazdów.",
  "new": "U siebie masz już `funkcje.py` z funkcją `suma`."
}
````
