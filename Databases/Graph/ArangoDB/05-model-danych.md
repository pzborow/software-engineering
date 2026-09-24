# Model danych

## Opis

Model danych w ArangoDB opisuje dokumenty, ich identyfikatory, kolekcje oraz relacje. Może pozostać elastyczny, ale powinien mieć jasno określone znaczenie i reguły potrzebne aplikacji.

## Kluczowe koncepty

- **Dokument JSON** — podstawowa struktura przechowująca dane.
- **Klucz dokumentu** — identyfikator dokumentu w kolekcji.
- **Kolekcja** — logiczny zbiór dokumentów lub krawędzi.
- **Atrybut** — pole dokumentu opisujące jego właściwość.
- **Relacja** — połączenie dokumentów reprezentowane przez krawędź.

## Key points

- Dokument powinien reprezentować spójny obiekt lub fragment informacji.
- Elastyczny schemat nie oznacza dowolnego schematu.
- Identyfikatory i nazwy atrybutów są częścią kontraktu danych.
- Relacje warto modelować jawnie, gdy są przedmiotem zapytań.
- Struktura powinna wspierać najważniejsze operacje.

## Example

Dokument może zawierać identyfikator, podstawowe atrybuty i informacje potrzebne do odczytu. Jeśli połączenie z innym dokumentem jest ważne, można reprezentować je osobną krawędzią.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Określamy obiekty i ich odpowiedzialności.
2. Ustalamy atrybuty konieczne do pracy systemu.
3. Wybieramy kolekcje dla spójnych grup danych.
4. Definiujemy identyfikację dokumentów.
5. Modelujemy ważne relacje.
6. Sprawdzamy model na rzeczywistych zapytaniach.

## Pytania

1. Co opisuje model danych?
2. Czym jest dokument JSON?
3. Do czego służy klucz dokumentu?
4. Czym jest kolekcja?
5. Czy elastyczny schemat oznacza brak zasad?
6. Kiedy relację warto zapisać jako krawędź?
7. Co jest częścią kontraktu danych?
8. Jak wybrać granice dokumentu?
9. Dlaczego model należy sprawdzać zapytaniami?
10. Jaki jest cel dobrego modelu danych?

## Odpowiedzi

1. Dokumenty, kolekcje, identyfikatory, atrybuty i relacje.
2. Podstawowy obiekt przechowujący dane.
3. Do jednoznacznego rozpoznania dokumentu.
4. Logicznym zbiorem dokumentów lub krawędzi.
5. Nie, potrzebne są reguły jakości i znaczenia.
6. Gdy powiązanie jest ważne i będzie analizowane.
7. Identyfikatory, nazwy i znaczenie atrybutów.
8. Według spójności obiektu i najczęstszych operacji.
9. Aby sprawdzić dopasowanie do rzeczywistego użycia.
10. Ułatwienie poprawnego, zrozumiałego i efektywnego dostępu.

[Powrót do spisu treści](README.md)
