# Kolekcje, dokumenty i krawędzie

## Opis

Kolekcje organizują dane w ArangoDB. Dokumenty przechowują obiekty, a krawędzie opisują kierunkowe relacje między dokumentami. Razem tworzą podstawę modelu dokumentowego i grafowego.

## Kluczowe koncepty

- **Kolekcja dokumentowa** — zbiór zwykłych dokumentów.
- **Kolekcja krawędzi** — zbiór dokumentów opisujących relacje.
- **Wierzchołek** — dokument występujący jako element grafu.
- **`_from` i `_to`** — punkty początku i końca krawędzi.
- **Graf nazwany** — logiczna definicja kolekcji i relacji tworzących graf.

## Key points

- Dokument może być elementem grafu bez utraty swojej dokumentowej natury.
- Krawędź jest dokumentem z informacją o początku i końcu relacji.
- Kierunek relacji powinien mieć znaczenie albo być świadomie pominięty w zapytaniu.
- Kolekcje powinny grupować dane o podobnej odpowiedzialności.
- Graf nazwany ułatwia wyrażenie struktury relacji.

## Example

Dwa dokumenty mogą reprezentować obiekty, a krawędź między nimi może opisywać relację. Dodatkowe atrybuty krawędzi mogą przechowywać właściwości samego powiązania.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Tworzymy kolekcje dla obiektów.
2. Tworzymy kolekcję krawędzi dla ważnych relacji.
3. Wskazujemy dokument początkowy i końcowy.
4. Nadajemy relacji znaczenie biznesowe lub techniczne.
5. Definiujemy graf logiczny, jeśli upraszcza pracę.
6. Sprawdzamy traversal na rzeczywistych przypadkach.

## Pytania

1. Do czego służą kolekcje?
2. Co przechowuje dokument?
3. Co przechowuje krawędź?
4. Czym jest wierzchołek?
5. Do czego służą pola `_from` i `_to`?
6. Czym jest graf nazwany?
7. Czy dokument może być częścią grafu?
8. Czy krawędź może mieć własne atrybuty?
9. Po co określać kierunek relacji?
10. Jak dobrać kolekcje?

## Odpowiedzi

1. Organizują dokumenty i krawędzie w logiczne grupy.
2. Obiekt lub fragment informacji w formacie JSON.
3. Relację między dokumentami.
4. Dokument używany jako element grafu.
5. Wskazują początek i koniec relacji.
6. Logicznym opisem kolekcji i połączeń grafu.
7. Tak, dokument może być jednocześnie wierzchołkiem.
8. Tak, opisują właściwości relacji.
9. Aby poprawnie interpretować przejścia po grafie.
10. Według odpowiedzialności i podobieństwa danych.

[Powrót do spisu treści](README.md)
