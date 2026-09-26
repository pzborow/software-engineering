# Krok 1243 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „wyjaśnimy w następnej części” (czym jest wykonawca kodu i czym różni się od kompilatora).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-03-kompilator-i-interpreter]
To ten wykonawca, o którym była mowa przy uruchamianiu programu. Gdy wpisujesz `python rozlicz.py`, Python działa jako interpreter: bierze plik i wykonuje go od góry.


2. [sec-03-co-znaczy-uruchomic-program]
Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam kod źródłowy leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś nie zacznie go realizować.

Plik z kodem czyta i wykonuje linia po linii inny program. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.

Polecenie wpisujemy w terminalu, czyli oknie, w którym komputer przyjmuje polecenia pisane tekstem i odpowiada tekstem.
````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 (sec-03-kompilator-i-interpreter) to właściwa sekcja: wyjaśnia, że wykonawcą jest interpreter, który bierze plik i wykonuje go od góry. Miejsce 2 to sekcja, z której pochodzi sama zapowiedź."
}
````
