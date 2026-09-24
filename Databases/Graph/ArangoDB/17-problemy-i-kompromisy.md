# Typowe problemy i kompromisy

## Opis

ArangoDB upraszcza obsługę wielu modeli, ale może też zachęcać do nadmiernej elastyczności i używania niewłaściwego modelu. Najczęstsze problemy wynikają z braku reguł, niekontrolowanego wzrostu zapytań i niedoszacowania kosztu utrzymania.

## Kluczowe koncepty

- **Nadmierna elastyczność** — struktura danych zmienia się bez kontroli.
- **Niewłaściwy model** — użycie dokumentów lub grafu niezgodnie z problemem.
- **Koszt wielomodelowości** — potrzeba rozumienia kilku sposobów pracy.
- **Ciężkie zapytanie** — operacja zużywająca dużo czasu lub zasobów.
- **Dług danych** — konsekwencje nieuporządkowanych struktur i migracji.

## Key points

- Jedna technologia nie usuwa potrzeby dobrego modelowania.
- Elastyczność bez walidacji prowadzi do niespójności.
- Graf nie jest automatycznie najlepszy dla każdej relacji.
- Wspólny silnik nadal wymaga kompetencji i monitorowania.
- Złożone zapytanie może ukrywać problem modelu.

## Example

Jeśli każdy dokument ma inną strukturę, a zapytania muszą obsługiwać wiele wyjątków, elastyczność stała się kosztem. Warto wtedy ujednolicić najważniejsze reguły.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Zbieramy objawy i przypadki problemów.
2. Sprawdzamy model, walidację i zapytania.
3. Identyfikujemy dane historyczne wymagające uporządkowania.
4. Mierzymy koszt zmian i utrzymania.
5. Ujednolicamy reguły albo upraszczamy model.
6. Wprowadzamy monitoring zapobiegający powrotowi problemu.

## Pytania

1. Czym jest nadmierna elastyczność?
2. Co oznacza niewłaściwy model?
3. Jaki koszt ma wielomodelowość?
4. Czym jest ciężkie zapytanie?
5. Czym jest dług danych?
6. Czy jedna technologia usuwa potrzebę modelowania?
7. Czy graf jest dobry dla każdej relacji?
8. Co może oznaczać wiele wyjątków w zapytaniu?
9. Jak reagować na niespójne dokumenty?
10. Jaki jest cel analizy kompromisów?

## Odpowiedzi

1. Zmienianie struktury bez kontroli reguł.
2. Użycie modelu niepasującego do danych i zapytań.
3. Potrzebę rozumienia oraz utrzymywania kilku sposobów pracy.
4. Operacja zużywająca dużo czasu lub zasobów.
5. Koszt wynikający z nieuporządkowanych danych i migracji.
6. Nie, nadal potrzebna jest architektura danych.
7. Nie, zależy to od charakteru relacji i zapytań.
8. Problem modelu, walidacji albo zapytania.
9. Ustalić reguły, zaplanować migrację i dodać walidację.
10. Świadomy wybór wartości i kosztów rozwiązania.

[Powrót do spisu treści](README.md)
