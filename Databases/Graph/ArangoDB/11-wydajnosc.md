# Wydajność

## Opis

Wydajność ArangoDB zależy od modelu danych, zapytań, indeksów, rozmiaru danych i sposobu wdrożenia. Nie można ocenić jej wyłącznie na podstawie pojedynczej funkcji lub przykładowego zapytania.

## Kluczowe koncepty

- **Plan zapytania** — sposób, w jaki baza zamierza wykonać zapytanie.
- **Koszt zapytania** — zasoby i czas potrzebne do uzyskania wyniku.
- **Obciążenie** — liczba i charakter operacji w czasie.
- **Wąskie gardło** — element ograniczający całość działania.
- **Dane reprezentatywne** — dane podobne skalą i strukturą do rzeczywistych.

## Key points

- Najpierw mierzymy, potem optymalizujemy.
- Plan zapytania pomaga znaleźć zbędne operacje.
- Indeks może poprawić odczyt, ale zwiększyć koszt zapisu.
- Grafowe traversale mogą mieć różny koszt zależnie od głębokości i rozgałęzienia.
- Test na małej próbce nie przewiduje zachowania przy dużej skali.

## Example

To samo zapytanie może działać dobrze na małej kolekcji, ale wymagać zmiany indeksu lub modelu po zwiększeniu liczby dokumentów i relacji.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Definiujemy oczekiwany czas i obciążenie.
2. Mierzymy zapytania na reprezentatywnych danych.
3. Analizujemy plan wykonania.
4. Korygujemy model, indeksy lub zapytanie.
5. Sprawdzamy koszt odczytu i zapisu.
6. Powtarzamy pomiar po zmianie.

## Pytania

1. Od czego zależy wydajność ArangoDB?
2. Czym jest plan zapytania?
3. Co oznacza wąskie gardło?
4. Dlaczego najpierw należy mierzyć?
5. Czy indeks zawsze pomaga?
6. Od czego zależy koszt traversalu?
7. Czym są dane reprezentatywne?
8. Czy mała próbka wystarcza do oceny skali?
9. Co można zmienić podczas optymalizacji?
10. Jaki jest cel pomiaru po zmianie?

## Odpowiedzi

1. Od danych, zapytań, indeksów, obciążenia i wdrożenia.
2. Przewidywanym sposobem wykonania zapytania.
3. Element ograniczający wydajność całego systemu.
4. Aby zmiana rozwiązywała rzeczywisty problem.
5. Nie, zwiększa też koszt zmian danych.
6. Od głębokości, rozgałęzienia i liczby odwiedzanych elementów.
7. Danymi podobnymi do rzeczywistych pod względem skali i struktury.
8. Nie, może ukryć problemy wzrostu.
9. Model, zapytanie, indeksy lub sposób wdrożenia.
10. Sprawdzenie, czy optymalizacja przyniosła efekt.

[Powrót do spisu treści](README.md)
