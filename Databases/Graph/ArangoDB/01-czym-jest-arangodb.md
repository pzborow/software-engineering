# Czym jest ArangoDB

## Opis

ArangoDB to wielomodelowa baza danych, która pozwala przechowywać i analizować dokumenty JSON, relacje między nimi oraz dane przeznaczone do wyszukiwania. Najważniejszą cechą jest możliwość pracy z różnymi modelami w jednym systemie i za pomocą jednego języka zapytań.

## Kluczowe koncepty

- **Baza wielomodelowa** — łączy możliwości modeli dokumentowego, grafowego i wyszukiwania.
- **Dokument** — elastyczny obiekt danych w formacie JSON.
- **Graf** — wierzchołki i krawędzie opisujące relacje.
- **Kolekcja** — zbiór dokumentów albo krawędzi.
- **AQL** — ArangoDB Query Language, język zapytań i modyfikacji danych.

## Key points

- ArangoDB nie wymusza wyboru jednego modelu dla całego systemu.
- Dokumenty przechowują dane, a krawędzie opisują relacje.
- Graf jest naturalnym sposobem pracy z połączonymi danymi.
- AQL pozwala łączyć filtrowanie, agregacje, modyfikacje i traversale.
- Technologia nie zastępuje decyzji o właściwym modelu danych.

## Example

Jeden system może przechowywać obiekty jako dokumenty, relacje jako krawędzie, a następnie używać grafu do analizy połączeń i wyszukiwania do odnajdywania właściwych dokumentów.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Określamy rodzaj danych i relacji.
2. Wybieramy kolekcje dokumentów oraz krawędzi.
3. Definiujemy sposób identyfikacji i dostępu do danych.
4. Używamy AQL do odczytu, modyfikacji i analizy.
5. Dodajemy indeksy i reguły spójności stosownie do potrzeb.
6. Oceniamy, czy połączenie modeli upraszcza system.

## Pytania

1. Czym jest ArangoDB?
2. Co oznacza wielomodelowość?
3. Czym jest dokument?
4. Czym jest krawędź?
5. Do czego służy AQL?
6. Czym różni się kolekcja dokumentów od kolekcji krawędzi?
7. Czy ArangoDB wymaga jednego modelu danych?
8. Do czego nadaje się graf?
9. Co daje jeden język zapytań?
10. Czy sama technologia wybiera model danych za projektanta?

## Odpowiedzi

1. To wielomodelowa baza danych do pracy z dokumentami, grafami i wyszukiwaniem.
2. Możliwość używania kilku modeli danych w jednym systemie.
3. Obiekt danych zapisany jako JSON.
4. Element opisujący relację między dokumentami.
5. Do odczytu, modyfikacji i analizy danych.
6. Krawędzie przechowują relacje, a dokumenty przechowują obiekty.
7. Nie, można łączyć kilka modeli.
8. Do analizy relacji i przechodzenia po połączeniach.
9. Ujednolica sposób pracy z różnymi modelami.
10. Nie, model powinien wynikać z potrzeb danych i zapytań.

[Powrót do spisu treści](README.md)
