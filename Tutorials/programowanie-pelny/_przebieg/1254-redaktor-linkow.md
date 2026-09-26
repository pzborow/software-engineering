# Krok 1254 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne” (kod stały, dane zmienne).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-08-dane-wejsciowe-programu]
Do tej pory kwoty wpisywaliśmy w kodzie, np. `mazury = [45.5, 20, 12.5]`. Wtedy każda zmiana danych wymagała edycji programu. Dane wejściowe rozdzielają obie sprawy: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne.


2. [sec-07-ponowne-uzycie-kodu]
Zmieniają się tylko dane: lista wydatków i liczba osób. Logika liczenia leży w jednym miejscu, więc nie kopiujesz pętli dla każdego wyjazdu.

````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 samo zawiera to zdanie i wyjaśnia, że kod jest stały, a dane przychodzą inne przy każdym uruchomieniu. Miejsce 2 opisuje tylko ponowne użycie kodu."
}
````
