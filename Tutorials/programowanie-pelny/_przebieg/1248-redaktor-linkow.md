# Krok 1248 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „„Wspólna Kasa”, która czeka na koniec listy” (przykład programu dzielącego wydatki po osobach, przechodzącego przez listę osób).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-06-czym-jest-petla]
Ciało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. Ostatni `print` nie ma wcięcia, więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.


2. [sec-05-instrukcja-warunkowa-jesli-to]
Pierwszy warunek jest prawdziwy, więc jego linia się wykonała. Drugi jest fałszywy, więc jego wcięta linia została pominięta. Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.

````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 wprost wyjaśnia, że ostatni print bez wcięcia wykonuje się raz, po zakończeniu pętli, czyli na końcu listy. To dokładnie ta informacja; miejsce 2 dotyczy instrukcji warunkowej, nie pętli."
}
````
