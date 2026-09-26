# Krok 1240 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „przykład, który będzie nam towarzyszył w kolejnych działach” (Wspólna Kasa wraca w kolejnych działach).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-03-kompilator-i-interpreter]
Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania. Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie. W praktyce Python najpierw przekłada plik na pośredni zapis, ale z Twojej strony to jedno polecenie.

2. [sec-03-co-znaczy-uruchomic-program]
Uruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. Tak wygląda codzienna praca: zapisz, uruchom, przeczytaj wynik.
````

## Odpowiedź

````json
{
  "hop": 1,
  "reason": "Miejsce 1 już mówi o Wspólnej Kasie jako przykładzie, z którym czytelnik pracuje (plik rozlicz.py, uruchamianie); miejsce 2 jest ogólne i nie wspomina o przykładzie."
}
````
