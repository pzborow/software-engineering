# Testowanie

## Opis

Testowanie ArangoDB powinno obejmować poprawność modelu, zapytań, transakcji, indeksów i zachowania środowiska. Testy powinny sprawdzać ryzyka ważne dla konkretnego systemu, a nie tylko to, czy pojedyncze zapytanie zwraca wynik.

## Kluczowe koncepty

- **Test zapytania** — sprawdzenie wyniku i reguł zapytania.
- **Test modelu** — sprawdzenie struktury dokumentów i relacji.
- **Test integracyjny** — sprawdzenie współpracy aplikacji z bazą.
- **Test wydajności** — sprawdzenie czasu i kosztu pod obciążeniem.
- **Test odtworzenia** — sprawdzenie możliwości przywrócenia danych.

## Key points

- Testy powinny obejmować dane poprawne i błędne.
- Trzeba sprawdzać także migracje oraz kompatybilność.
- Test wydajności wymaga reprezentatywnych danych.
- Testy awarii i restore ujawniają ryzyka operacyjne.
- Powtarzalność środowiska ułatwia diagnozę.

## Example

Test może sprawdzić, czy traversal zwraca właściwe relacje, czy walidacja odrzuca błędny dokument, a proces restore odtwarza użyteczny stan.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Spisujemy ryzyka i wymagania.
2. Przygotowujemy reprezentatywny model danych.
3. Testujemy zapytania, walidację i transakcje.
4. Testujemy wydajność oraz zachowanie przy błędach.
5. Sprawdzamy backup i restore.
6. Uruchamiamy testy automatycznie przy zmianach.

## Pytania

1. Co powinno obejmować testowanie ArangoDB?
2. Czym jest test zapytania?
3. Czym jest test modelu?
4. Po co testować dane błędne?
5. Dlaczego wydajność wymaga właściwych danych?
6. Co sprawdza test odtworzenia?
7. Czy trzeba testować migracje?
8. Co daje powtarzalne środowisko?
9. Jakie ryzyka ujawniają testy awarii?
10. Jaki jest cel automatyzacji testów?

## Odpowiedzi

1. Model, zapytania, transakcje, wydajność i utrzymanie.
2. Poprawność wyniku i reguł zapytania.
3. Poprawność dokumentów, kolekcji i relacji.
4. Aby sprawdzić odporność reguł i walidacji.
5. Mała próbka może ukryć problemy skali.
6. Możliwość przywrócenia użytecznych danych.
7. Tak, bo zmieniają istniejący stan.
8. Powtarzalność wyników i łatwiejszą diagnozę.
9. Zachowanie systemu przy niedostępności lub utracie danych.
10. Szybkie i powtarzalne wykrywanie regresji.

[Powrót do spisu treści](README.md)
