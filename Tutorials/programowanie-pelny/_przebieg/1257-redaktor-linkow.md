# Krok 1257 · redaktor_linków

Węzeł: `resolve_chains` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Zdanie w tekście odsyła czytelnika: „Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu” (czytanie komunikatów o błędach i debugowanie).
Link prowadzi do miejsca 1, ale ono samo odsyła dalej. Poniżej cała ścieżka.
Wybierz miejsce, w którym czytelnik NAPRAWDĘ znajdzie informację, do której odsyła zdanie (nie kolejną wzmiankę ani zapowiedź).
Gdy miejsce 1 już ją zawiera, wybierz 1. Podaj hop (numer) i krótko reason.

ŚCIEŻKA:
1. [sec-09-jak-czytac-komunikat-o-bledzie]
Konsekwencja: nie bój się czerwonego tekstu. Przeczytaj ostatnią linię, znajdź w śladzie własny plik i numer linii, a zwykle już wiesz, gdzie szukać. Szukanie przyczyny krok po kroku omówimy przy debugowaniu.

2. [sec-09-czym-jest-debugowanie]
Debugowanie to szukanie przyczyny błędu i jej usuwanie. Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach.

````

## Odpowiedź

````json
{
  "hop": 2,
  "reason": "Miejsce 1 tylko zapowiada („omówimy przy debugowaniu”) i zawiera krótką wskazówkę o czytaniu śladu. Miejsce 2 wyjaśnia, czym jest debugowanie, więc tam czytelnik znajdzie omówienie szukania błędów."
}
````
