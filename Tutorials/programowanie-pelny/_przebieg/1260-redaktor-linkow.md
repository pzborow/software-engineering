# Krok 1260 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „W kolejnej sekcji zobaczysz, jak taki kawałek kodu zaczyna pracować za Ciebie” (automatyzacja prostych zadań).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-10-automatyzacja-prostych-zadan]
Mechanizm znasz: to pętla po danych i funkcja. Zamiast przepisywać kwoty do kalkulatora, opisujesz kroki raz, a program wykonuje je dla dowolnej liczby pozycji. Tak wygląda to we Wspólnej Kasie:


2. [sec-10-strona-internetowa-a-aplikacja-mobilna]
Pod spodem obie robią to samo, co każdy program: dane wejściowe, przetwarzanie, dane wyjściowe. We „Wspólnej Kasie” wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.


3. [sec-10-programy-uzywane-na-co-dzien]
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
  "reason": "Miejsce 1 samo zawiera treść, do której odsyła zdanie: pokazuje, jak kod (pętla i funkcja) pracuje za czytelnika, zamiast przepisywania kwot, i zapowiada przykład z Wspólnej Kasy. Miejsca 2 i 3 dotyczą innych tematów (strona a aplikacja, programy na co dzień)."
}
````
