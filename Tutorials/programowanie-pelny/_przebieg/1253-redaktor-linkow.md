# Krok 1253 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „U siebie w `funkcje.py` masz te same funkcje” (plik funkcje.py z funkcjami sumy i udziału na osobę z poprzedniego działu).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-07-czym-jest-funkcja]
Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:


2. [sec-06-petla-po-elementach-listy]
Suma zaczyna od zera, rośnie w każdej iteracji, a wynik pokazujesz dopiero po pętli, już bez wcięcia.
````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 to sekcja o funkcji, w której suma zostaje zamieniona w osobną funkcję. To ten kod czytelnik ma w funkcje.py. Miejsce 2 opisuje tylko pętlę, a nie funkcję."
}
````
