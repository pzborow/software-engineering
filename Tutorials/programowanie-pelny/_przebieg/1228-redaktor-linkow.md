# Krok 1228 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „języku, którego użyjemy w tym tutorialu” (Python jako język tutorialu).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-02-czym-jest-algorytm]
Na razie nie piszemy kodu: to celowo zwykły język. Ten sam algorytm można potem zapisać w Pythonie, w arkuszu kalkulacyjnym albo wykonać ręcznie. Właśnie dlatego warto go oddzielać od kodu.


2. [sec-03-czym-jest-kod-zrodlowy]
Kod źródłowy zapisujemy w pliku o rozszerzeniu zależnym od języka. Pliki Pythona kończą się na `.py`. Taki plik będzie miał nasz przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Zaczyna się od pliku `rozlicz.py`:


3. [sec-03-do-czego-sluza-komentarze]
```python
# rozlicz.py - rozliczenie wspólnych wydatków
print("Wspólna Kasa")
# udział na dwie osoby
print(300 / 3)  # 300 zł na troje osób
# print(300 / 2)  <- ta linia jest wyłączona
```
````

## Odpowiedź

````json
{
  "hop": 2,
  "reason": "Miejsce 2 wprost stwierdza, że pliki są w Pythonie (.py) i że ten język towarzyszy przykładowi tutorialu. Miejsce 1 tylko wymienia Pythona jako jedną z opcji, a miejsce 3 to sam kod."
}
````
