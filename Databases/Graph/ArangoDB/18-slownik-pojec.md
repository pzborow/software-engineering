# Słownik pojęć

## Opis

Słownik zbiera podstawowe pojęcia potrzebne do rozmowy o ArangoDB. Służy do szybkiego przypomnienia znaczeń, a szersze wyjaśnienia znajdują się w pozostałych rozdziałach.

## Kluczowe koncepty

- **ArangoDB** — wielomodelowa baza danych.
- **Dokument** — obiekt JSON.
- **Kolekcja** — zbiór dokumentów lub krawędzi.
- **Krawędź** — dokument opisujący relację.
- **Graf** — wierzchołki i krawędzie.
- **AQL** — język zapytań ArangoDB.
- **Indeks** — struktura przyspieszająca dostęp.
- **Transakcja** — grupa operacji traktowana jako całość.
- **Sharding** — podział danych.
- **Replikacja** — utrzymywanie kopii.

## Key points

- Pojęcia opisują zarówno dane, jak i sposób utrzymania bazy.
- Jeden termin może mieć znaczenie zależne od kontekstu.
- Słownik pomaga ujednolicić rozmowę w zespole.
- Znajomość terminów nie zastępuje decyzji architektonicznych.
- Przy wątpliwościach należy wrócić do właściwego rozdziału.

## Example

Gdy mowa o grafie, warto doprecyzować, czy chodzi o model danych, traversal, nazwany graf czy sposób przechowywania relacji.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Identyfikujemy termin.
2. Sprawdzamy jego znaczenie w danym kontekście.
3. Łączymy go z modelem danych lub operacją.
4. Oceniamy wpływ na spójność, wydajność i utrzymanie.
5. Wracamy do szczegółowego rozdziału.

## Pytania

1. Czym jest ArangoDB?
2. Czym jest dokument?
3. Czym jest kolekcja?
4. Czym jest krawędź?
5. Co tworzy graf?
6. Do czego służy AQL?
7. Czym jest indeks?
8. Czym jest transakcja?
9. Czym różni się sharding od replikacji?
10. Czy słownik zastępuje pozostałe rozdziały?

## Odpowiedzi

1. Wielomodelową bazą danych.
2. Obiektem danych w formacie JSON.
3. Zbiorem dokumentów lub krawędzi.
4. Dokumentem opisującym relację.
5. Wierzchołki i krawędzie.
6. Do zapytań i modyfikacji danych.
7. Strukturą przyspieszającą określony dostęp.
8. Grupą operacji traktowaną jako całość.
9. Sharding dzieli dane, a replikacja utrzymuje ich kopie.
10. Nie, jest tylko szybkim przypomnieniem pojęć.

[Powrót do spisu treści](README.md)
