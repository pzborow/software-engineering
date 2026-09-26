# Krok 1247 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „Jak to zapisać, pokażemy przy instrukcji warunkowej” (zapisywanie decyzji na podstawie wartości logicznej).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-05-instrukcja-warunkowa-jesli-to]
Warunek to zwykle porównanie z poprzedniej sekcji, bo daje `True` albo `False`. Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej.


2. [sec-05-porownywanie-wartosci]
Program porównuje wartości operatorami porównania. To znaki takie jak `==` czy `>`, które zestawiają dwie wartości i zwracają wynik `True` albo `False`, czyli wartość logiczną.

| Zapis | Znaczenie |
|---|---|
| `a == b` | równe |
| `a != b` | różne |
| `a < b`, `a > b` | mniejsze, większe |
| `a <= b`, `a >= b` | mniejsze lub równe, większe lub równe |

Uwaga na `==`: pojedynczy znak `=` to przypisanie, czyli zapisanie wartości w zmiennej. Dopiero podwójny pyta „czy są równe?” i niczego nie zmienia.

```python
kwota = 45.5
print(kwota == 45.5)

````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 to sekcja o instrukcji warunkowej i opisuje, jak Python podejmuje decyzję na podstawie wartości logicznej (True wykonuje linie, False pomija). Miejsce 2 dotyczy tylko porównań, a nie zapisywania decyzji."
}
````
