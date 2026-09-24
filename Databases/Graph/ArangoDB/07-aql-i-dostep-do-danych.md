# AQL i dostęp do danych

## Opis

AQL jest językiem zapytań ArangoDB służącym do odczytu, modyfikacji i analizy danych. Pozwala pracować z dokumentami, kolekcjami i grafami w jednym modelu zapytań.

## Kluczowe koncepty

- **AQL** — język zapytań ArangoDB.
- **Filtrowanie** — wybór dokumentów spełniających warunki.
- **Agregacja** — obliczanie wartości na podstawie zbioru danych.
- **Traversal** — przechodzenie po relacjach grafu.
- **Modyfikacja** — wstawianie, aktualizacja, zastępowanie i usuwanie danych.

## Key points

- AQL obejmuje odczyt, modyfikacje i zapytania grafowe.
- Zapytania powinny być czytelne i odpowiadać modelowi danych.
- Warto oddzielać parametry od struktury zapytania.
- Koszt zapytania zależy od ilości danych i sposobu filtrowania.
- Ten sam język nie oznacza, że każde zapytanie ma ten sam koszt.

## Example

Jedno zapytanie może filtrować dokumenty, połączyć je z informacjami z innej kolekcji, wykonać agregację albo przejść po relacjach grafu.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Opisujemy oczekiwany wynik.
2. Wybieramy kolekcje i relacje potrzebne do zapytania.
3. Budujemy filtr, projekcję lub traversal.
4. Dodajemy sortowanie i agregację tylko wtedy, gdy są potrzebne.
5. Sprawdzamy plan i koszt zapytania.
6. Mierzymy zachowanie na danych zbliżonych do rzeczywistych.

## Pytania

1. Czym jest AQL?
2. Do czego służy filtrowanie?
3. Czym jest agregacja?
4. Co oznacza traversal?
5. Czy AQL służy tylko do odczytu?
6. Dlaczego parametry powinny być oddzielone od zapytania?
7. Od czego zależy koszt zapytania?
8. Czy jeden język oznacza jednakowy koszt operacji?
9. Co sprawdza się przed użyciem zapytania na produkcji?
10. Jaki jest cel czytelnego zapytania?

## Odpowiedzi

1. To język zapytań ArangoDB.
2. Do wybrania dokumentów spełniających warunki.
3. Obliczenie podsumowania na podstawie danych.
4. Przechodzenie po relacjach grafu.
5. Nie, służy też do modyfikacji danych.
6. Dla bezpieczeństwa, czytelności i ponownego użycia.
7. Od danych, filtrów, sortowania, relacji i indeksów.
8. Nie, różne operacje mają różny koszt.
9. Plan, poprawność i zachowanie na reprezentatywnych danych.
10. Ułatwienie zrozumienia, utrzymania i optymalizacji.

[Powrót do spisu treści](README.md)
