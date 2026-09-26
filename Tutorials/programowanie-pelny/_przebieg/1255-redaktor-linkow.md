# Krok 1255 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „suchy wynik nic nie mówi komuś, kto nie zna kodu” (wniosek o opisywaniu wyniku z sekcji o danych wyjściowych).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-08-dane-wyjsciowe-programu]
Konsekwencja: o tym, co program wypisze, decydujesz Ty. Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. Do plików wrócimy osobno, a wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie.

2. [sec-08-czym-jest-plik]
Plik to nazwana porcja danych zapisana na dysku, która istnieje także wtedy, gdy program już nie działa. Zmienne żyją tylko podczas pracy programu i znikają wraz z jego zakończeniem, a plik zostaje. Dlatego plik jest miejscem, z którego dane wejściowe przychodzą i do którego trafiają dane wyjściowe.

````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 samo zawiera wniosek, że suchy wynik „26.0” nic nie mówi bez opisu i jednostki. Miejsce 2 dotyczy plików, a nie opisywania wyniku."
}
````
