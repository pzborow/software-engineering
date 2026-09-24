# Transakcje i spójność

## Opis

Transakcje określają, jak ArangoDB traktuje grupę zmian jako całość. Spójność oznacza zachowanie reguł danych mimo odczytów, modyfikacji i równoległego działania wielu operacji.

## Kluczowe koncepty

- **Transakcja** — grupa operacji traktowana jako jedna jednostka.
- **Atomowość** — wszystkie zmiany są zastosowane albo żadna.
- **Izolacja** — ograniczenie wpływu równoległych operacji na siebie.
- **Spójność** — zachowanie ustalonych reguł danych.
- **Zakres transakcji** — dokumenty i kolekcje objęte jedną operacją.

## Key points

- Transakcja powinna obejmować tylko potrzebny zakres.
- AQL może wykonywać operacje w sposób transakcyjny.
- Większa spójność może oznaczać większy koszt i mniejszą równoległość.
- Operacje między niezależnymi granicami wymagają świadomego projektu.
- Reguły biznesowe powinny określać wymaganą spójność.

## Example

Jeśli kilka zmian musi zostać zastosowanych razem, można objąć je jedną transakcją. Jeśli opóźnienie między zmianami jest akceptowalne, nie trzeba wymuszać jednej transakcji dla całego procesu.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Określamy regułę, która musi pozostać prawdziwa.
2. Wskazujemy dane objęte zmianą.
3. Ustalamy potrzebny poziom atomowości i izolacji.
4. Ograniczamy zakres transakcji.
5. Sprawdzamy zachowanie przy błędzie i równoległości.
6. Mierzymy koszt wybranego poziomu spójności.

## Pytania

1. Czym jest transakcja?
2. Co oznacza atomowość?
3. Czym jest izolacja?
4. Co oznacza spójność danych?
5. Dlaczego zakres transakcji powinien być ograniczony?
6. Czy każda operacja wymaga transakcji?
7. Co powinno określać wymagany poziom spójności?
8. Jaki może być koszt silniejszej spójności?
9. Co trzeba sprawdzić przy równoległych operacjach?
10. Jaki jest cel transakcji?

## Odpowiedzi

1. Grupą operacji traktowaną jako jedna jednostka.
2. Wszystkie zmiany są wykonane albo żadna.
3. Ograniczenie wzajemnego wpływu równoległych operacji.
4. Zachowanie ustalonych reguł danych.
5. Aby ograniczyć koszt i zwiększyć czytelność.
6. Nie, zależy to od reguł i charakteru procesu.
7. Reguły biznesowe i wymagania procesu.
8. Mniejsza równoległość i większy koszt wykonania.
9. Konflikty, kolejność i wynik zmian.
10. Bezpieczne zastosowanie powiązanych zmian.

[Powrót do spisu treści](README.md)
