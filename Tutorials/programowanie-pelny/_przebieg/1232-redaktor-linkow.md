# Krok 1232 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „pytania do użytkownika” (zapowiedź dobudowania pytań do użytkownika jako oprawy programu).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-08-pytanie-uzytkownika-o-informacje]
Pokażemy to na przykładzie, który będzie nam towarzyszył: „Wspólnej Kasie”, czyli programie do rozliczania wspólnych wydatków znajomych. Zaczynamy dobudowywać do niego pytania do użytkownika, a pierwsze dotyczy nowego wydatku:


2. [sec-09-po-co-zapisywac-wersje-kodu]
Robi to Git, program do zapisywania historii plików. Zapis jednej wersji to commit: zdjęcie wybranych plików z danej chwili, z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię, to repozytorium. W przykładowym programie do dzielenia wydatków, „Wspólnej Kasie”, będzie nim folder `wspolna_kasa`, w którym leżą pliki programu.

````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 samo zawiera zapowiedź dobudowania pytań do użytkownika i pierwsze pytanie o nowy wydatek; miejsce 2 dotyczy Gita, nie pytań."
}
````
