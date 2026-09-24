# Kiedy warto je stosować

## Opis

ArangoDB warto rozważyć, gdy system pracuje jednocześnie z elastycznymi dokumentami, relacjami i wyszukiwaniem albo gdy te potrzeby mogą zmieniać się w czasie. Największą wartością jest uniknięcie rozdzielania powiązanych modeli na wiele niezależnych technologii.

## Kluczowe koncepty

- **Dane połączone** — dane, których znaczenie zależy od relacji.
- **Elastyczny model** — możliwość przechowywania zmiennych struktur dokumentów.
- **Wspólny silnik** — jedna platforma dla kilku sposobów pracy z danymi.
- **Koszt specjalizacji** — cena utrzymywania wielu wyspecjalizowanych baz.
- **Dopasowanie zapytań** — zgodność modelu z rzeczywistymi operacjami.

## Key points

- ArangoDB jest szczególnie interesująca przy silnie połączonych danych.
- Daje wartość, gdy dokumenty i relacje występują razem.
- Nie każdy prosty przypadek wymaga bazy wielomodelowej.
- Mniejsza liczba technologii nie zawsze oznacza mniejszą złożoność.
- Decyzję należy oprzeć na wzorcach odczytu i zapisu.

## Example

Jeśli system przechowuje elastyczne obiekty, analizuje ich relacje i potrzebuje wyszukiwania, jeden silnik może uprościć architekturę. Jeśli potrzebuje wyłącznie prostych tabel i transakcji, inne rozwiązanie może być wystarczające.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Spisujemy typy danych i najważniejsze relacje.
2. Opisujemy zapytania, które będą wykonywane najczęściej.
3. Sprawdzamy potrzebę dokumentów, grafu i wyszukiwania.
4. Porównujemy ArangoDB z prostszymi alternatywami.
5. Oceniamy kompetencje zespołu i koszt utrzymania.
6. Podejmujemy decyzję na podstawie realnych potrzeb.

## Pytania

1. Kiedy warto rozważyć ArangoDB?
2. Co oznaczają dane połączone?
3. Dlaczego połączenie modeli może być korzyścią?
4. Czy każda aplikacja potrzebuje bazy wielomodelowej?
5. Co należy przeanalizować przed wyborem bazy?
6. Kiedy prostsza baza może być lepsza?
7. Czym jest koszt specjalizacji?
8. Dlaczego ważne są wzorce zapytań?
9. Czy elastyczny model zawsze jest zaletą?
10. Jaki jest cel oceny dopasowania technologii?

## Odpowiedzi

1. Gdy system łączy dokumenty, relacje i wyszukiwanie.
2. To dane, których znaczenie zależy od powiązań z innymi danymi.
3. Pozwala obsługiwać powiązane potrzeby w jednym systemie.
4. Nie, wybór powinien wynikać z problemu.
5. Dane, relacje, zapytania, zespół i koszt utrzymania.
6. Gdy problem jest prosty i nie wymaga wielu modeli.
7. To koszt utrzymywania wielu wyspecjalizowanych technologii.
8. Bo model powinien odpowiadać temu, jak dane są używane.
9. Nie, może też utrudniać kontrolę spójności.
10. Wybór rozwiązania adekwatnego do problemu.

[Powrót do spisu treści](README.md)
