# Zapytania do Fuseki

## Opis

Fuseki udostępnia endpoint SPARQL, do którego można wysyłać zapytania HTTP. Najczęściej używa się SELECT do odczytu, CONSTRUCT do grafu, ASK do sprawdzenia warunku i UPDATE do zmiany danych.

## Kluczowe koncepty

- **Query endpoint** — adres dla zapytań odczytujących.
- **Update endpoint** — adres dla zmian.
- **Result format** — np. JSON, CSV lub XML.
- **LIMIT/OFFSET** — ograniczanie i dzielenie wyników.
- **HTTP POST** — typowy sposób przesłania zapytania.

## Key points

- Query i update powinny być rozdzielone logicznie.
- Zapytanie warto testować najpierw w konsoli Fuseki.
- `LIMIT` chroni przed przypadkowo dużym wynikiem.
- Wyniki SELECT mogą być zwracane jako SPARQL Results JSON.
- Dostęp produkcyjny wymaga uwierzytelniania i kontroli uprawnień.

## Example

```bash
curl --data-urlencode 'query=SELECT * WHERE { ?s ?p ?o } LIMIT 10' \
  -H 'Accept: application/sparql-results+json' \
  http://localhost:3030/ds/sparql
```

## Dodatkowe wyjaśnienie

W Fuseki najważniejsze jest rozróżnienie między odczytem a modyfikacją. `SELECT` zwraca tabelę wyników, `ASK` odpowiada tak/nie na pytanie o istnienie danych, `CONSTRUCT` buduje nowy graf, a `UPDATE` zmienia zawartość datasetu. W środowisku produkcyjnym nie wystarczy samo poprawne zapytanie — trzeba też dbać o bezpieczeństwo endpointu, ograniczenie dostępu i kontrolę rozmiaru wyników.

## Pełny flow

1. Wybieramy endpoint datasetu.
2. Piszymy zapytanie SPARQL.
3. Dodajemy prefiksy i ograniczenie wyniku.
4. Wysyłamy HTTP POST.
5. Odczytujemy format odpowiedzi.
6. Weryfikujemy wynik i koszt zapytania.

## Pytania

1. Do czego służy query endpoint?
2. Do czego służy update endpoint?
3. Jakie zapytanie zwraca tabelę wyników?
4. Jakie zapytanie tworzy graf?
5. Po co używać LIMIT?
6. Jak można wysłać zapytanie?
7. Co określa Accept?
8. Gdzie warto testować zapytania na początku?
9. Czy endpoint produkcyjny powinien być publiczny bez ochrony?
10. Co trzeba sprawdzić poza wynikiem?

## Odpowiedzi

1. Do odczytu danych.
2. Do ich modyfikacji.
3. SELECT.
4. CONSTRUCT.
5. Aby ograniczyć rozmiar wyniku.
6. Na przykład HTTP POST.
7. Oczekiwany format odpowiedzi.
8. W interfejsie lub konsoli Fuseki.
9. Nie.
10. Poprawność, format i koszt zapytania.

[Powrót do spisu treści](README.md)
