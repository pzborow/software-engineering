# Krok 1261 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „Tak wygląda to we Wspólnej Kasie” (przykładowy program Kasa dzielący rachunek).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-10-strona-internetowa-a-aplikacja-mobilna]
Pod spodem obie robią to samo, co każdy program: dane wejściowe, przetwarzanie, dane wyjściowe. We „Wspólnej Kasie” wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.


2. [sec-10-programy-uzywane-na-co-dzien]
Na co dzień używasz dziesiątek programów, choć rzadko o tym myślisz: komunikatora, mapy, banku w telefonie, arkusza kalkulacyjnego, przeglądarki. Każdy z nich to program albo aplikacja, czyli program z oprawą dla użytkownika, i działa według tego samego schematu, który znasz z własnych skryptów.

Zawsze są dane wejściowe, jakieś przetwarzanie i dane wyjściowe:

| Program | Wejście | Co robi | Wyjście |
|---|---|---|---|
| Nawigacja | cel podróży, Twoja pozycja | wybiera najkrótszą trasę | trasa na mapie |
| Bank w tele
````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 już pokazuje, jak wygląda to we „Wspólnej Kasie”: wejście to kwoty wpisane przez znajomych, przetwarzanie to podział rachunku, wyjście to wynik na ekranie. Miejsce 2 jest ogólne i mówi o programach na co dzień, nie o Kasie."
}
````
