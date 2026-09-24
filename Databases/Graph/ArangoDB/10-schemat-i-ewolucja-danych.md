# Schemat i ewolucja danych

## Opis

ArangoDB pozwala przechowywać dokumenty o elastycznej strukturze, ale system nadal potrzebuje zasad jakości danych. Schemat może być kontrolowany w aplikacji lub wspierany przez walidację kolekcji, a jego zmiany powinny być planowane.

## Kluczowe koncepty

- **Schemat** — oczekiwana struktura i reguły danych.
- **Walidacja** — sprawdzanie, czy dokument spełnia wymagania.
- **Migracja danych** — kontrolowana zmiana istniejących dokumentów.
- **Kompatybilność** — możliwość współpracy starych i nowych wersji.
- **Wersja dokumentu** — informacja pomagająca obsłużyć ewolucję struktury.

## Key points

- Schemat elastyczny nadal wymaga kontroli jakości.
- Walidacja powinna chronić najważniejsze reguły.
- Zmiana struktury może wymagać migracji istniejących dokumentów.
- Nowa wersja aplikacji powinna uwzględniać stare dane w okresie przejściowym.
- Brak planu ewolucji prowadzi do niespójności i trudnych zapytań.

## Example

Nowe dokumenty mogą otrzymać dodatkowy atrybut, a aplikacja przez pewien czas obsługuje jego brak w starszych dokumentach. Później można przeprowadzić kontrolowaną migrację.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Opisujemy oczekiwaną strukturę dokumentów.
2. Wskazujemy reguły wymagające walidacji.
3. Planujemy zmianę i wpływ na istniejące dane.
4. Wprowadzamy kompatybilny okres przejściowy.
5. Migrujemy dokumenty etapami.
6. Usuwamy stare reguły dopiero po zakończeniu przejścia.

## Pytania

1. Czy elastyczne dokumenty nie potrzebują schematu?
2. Czym jest walidacja?
3. Czym jest migracja danych?
4. Dlaczego potrzebna jest kompatybilność?
5. Po co wersjonować dokumenty?
6. Co grozi przy braku reguł jakości?
7. Czy każdą zmianę trzeba wdrażać jednocześnie?
8. Co należy przeanalizować przed zmianą struktury?
9. Jak bezpiecznie obsługiwać starsze dokumenty?
10. Jaki jest cel ewolucji schematu?

## Odpowiedzi

1. Potrzebują zasad, nawet jeśli struktura jest elastyczna.
2. Sprawdzenie dokumentu względem wymagań.
3. Kontrolowana zmiana istniejących dokumentów.
4. Aby stare i nowe wersje mogły współpracować.
5. Aby rozpoznawać różne struktury i sposób ich obsługi.
6. Niespójność i trudniejsze zapytania.
7. Nie, zmiany mogą być stopniowe.
8. Istniejące dane, zapytania, aplikacje i reguły biznesowe.
9. Przez okres przejściowy i obsługę brakujących pól.
10. Kontrolowana zmiana danych bez nieplanowanych przerw.

[Powrót do spisu treści](README.md)
