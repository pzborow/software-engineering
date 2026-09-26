# Krok 1233 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „sprawdzanie danych” (zapowiedź dobudowania sprawdzania danych wpisanych przez użytkownika).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-08-po-co-sprawdzac-dane-uzytkownika]
Ta kontrola to walidacja: sprawdzenie, czy wpisana wartość nadaje się do dalszej pracy, zanim program jej użyje. Pamiętasz, że input zawsze zwraca tekst. Gdy ktoś na pytanie „Ile zapłacił?” wpisze `abc`, samo `float("abc")` przerwie program komunikatem o błędzie. A gdy wpisze `-5`, program nie zgłosi żadnego błędu i po cichu policzy złe saldo.


2. [sec-08-pytanie-uzytkownika-o-informacje]
Pułapka: `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Dla Pythona to wciąż „45.5” w cudzysłowie, czyli tekst, którego nie da się dzielić ani dodawać do liczb (skończyłoby się to błędem TypeError). Dlatego `float()` zamienia tekst na liczbę. Spacja na końcu pytania oddziela je od tego, co wpisze użytkownik.

````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 samo wyjaśnia, czym jest walidacja i po co sprawdzać dane wpisane przez użytkownika (przykłady `abc` i `-5`). Miejsce 2 mówi tylko o typie zwracanym przez input i nie omawia sprawdzania danych."
}
````
