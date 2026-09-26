# Krok 1241 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „jak to działa, pokażemy przy uruchamianiu programu” (czytanie i wykonywanie pliku z kodem przez osobny program).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-03-co-znaczy-uruchomic-program]
Plik z kodem czyta i wykonuje linia po linii inny program. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.


2. [sec-03-kompilator-i-interpreter]
To ten wykonawca, o którym była mowa przy uruchamianiu programu. Gdy wpisujesz `python rozlicz.py`, Python działa jako interpreter: bierze plik i wykonuje go od góry.

````

## Odpowiedź

````json
{
  "hop": 2,
  "reason": "Miejsce 1 tylko zapowiada wyjaśnienie („wyjaśnimy w następnej części”). Faktyczne pokazanie, jak Python czyta plik i wykonuje go od góry (`python rozlicz.py`), jest dopiero w miejscu 2."
}
````
