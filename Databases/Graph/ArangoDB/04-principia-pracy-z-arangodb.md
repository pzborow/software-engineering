# Principia pracy z ArangoDB

## Opis

Praca z ArangoDB powinna zaczynać się od danych i zapytań, a dopiero potem od wyboru kolekcji, indeksów i konfiguracji. Najważniejsze zasady dotyczą jasnego modelu, świadomego używania relacji oraz kontroli kosztu zapytań.

## Kluczowe koncepty

- **Modelowanie pod zapytania** — projektowanie danych pod najważniejsze operacje.
- **Własność danych** — określenie, który obszar odpowiada za dokument.
- **Relacja jawna** — zapisanie powiązania jako danych, nie ukrytej konwencji.
- **Kontrolowany dostęp** — ograniczenie odczytu i modyfikacji do potrzeb.
- **Świadomy kompromis** — wybór elastyczności, spójności lub prostoty.

## Key points

- Najpierw trzeba rozumieć dane i pytania, a potem strukturę.
- Dokumenty i relacje powinny mieć jasne znaczenie.
- Elastyczność nie zwalnia z utrzymywania jakości danych.
- Indeksy i transakcje wynikają z potrzeb, nie z automatycznych założeń.
- Prostota modelu jest ważniejsza niż użycie wszystkich funkcji.

## Example

Jeżeli najczęstsze zapytanie przechodzi przez relacje, model grafowy może być naturalny. Jeżeli najczęściej pobierany jest cały obiekt, dokument powinien być zaprojektowany tak, aby ten odczyt był prosty.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Spisujemy najważniejsze pytania systemu.
2. Wybieramy model danych dla każdego pytania.
3. Ustalamy granice dokumentów i relacji.
4. Określamy wymagania spójności.
5. Dobieramy indeksy i sposób dostępu.
6. Mierzymy zachowanie i korygujemy model.

## Pytania

1. Od czego powinna zaczynać się praca z ArangoDB?
2. Co oznacza modelowanie pod zapytania?
3. Dlaczego relacje powinny być jawne?
4. Czy elastyczność oznacza brak reguł?
5. Kiedy dobiera się indeksy?
6. Co oznacza kontrolowany dostęp?
7. Dlaczego ważne są najczęstsze pytania?
8. Czy trzeba używać wszystkich modeli ArangoDB?
9. Co powinno poprzedzać wybór konfiguracji?
10. Jaki jest cel pomiaru zachowania modelu?

## Odpowiedzi

1. Od zrozumienia danych i najważniejszych zapytań.
2. Projektowanie struktury pod rzeczywiste operacje.
3. Aby znaczenie powiązań było zrozumiałe i możliwe do sprawdzenia.
4. Nie, dane nadal potrzebują reguł i jakości.
5. Po rozpoznaniu wzorców odczytu i filtrowania.
6. Dostęp tylko do potrzebnych danych i operacji.
7. One decydują o użyteczności i wydajności modelu.
8. Nie, należy używać tylko tych, które rozwiązują problem.
9. Analiza danych, zapytań i wymagań.
10. Sprawdzenie, czy model odpowiada rzeczywistym potrzebom.

[Powrót do spisu treści](README.md)
