# SPARQL

## Opis

SPARQL to język zapytań do danych RDF. Pozwala wyszukiwać wzorce trójek, łączyć warunki, filtrować wyniki, agregować dane oraz modyfikować graf przez SPARQL Update.

## Kluczowe koncepty

- **Triple pattern** — wzorzec trójki z niewiadomymi.
- **SELECT** — zwraca wybrane zmienne.
- **CONSTRUCT** — tworzy nowy graf.
- **ASK** — odpowiada true lub false.
- **SPARQL Update** — zmienia dane.

## Key points

- Zmienne w SPARQL zaczynają się od `?`.
- Wzorzec trójki opisuje, czego szukamy.
- `FILTER`, `OPTIONAL`, `UNION` rozszerzają zapytanie.
- `PREFIX` poprawia czytelność.
- Zapytanie może działać lokalnie albo przez endpoint Fuseki.

## Example

```sparql
PREFIX ex: <https://example.org/>
SELECT ?name
WHERE {
  ?person ex:name ?name .
}
```

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Określamy informację, której szukamy.
2. Zapisujemy wzorzec trójki.
3. Dodajemy prefiksy i warunki.
4. Wybieramy formę wyniku.
5. Uruchamiamy zapytanie na grafie lub endpointcie.

## Pytania

1. Czym jest SPARQL?
2. Czym jest triple pattern?
3. Do czego służy SELECT?
4. Do czego służy CONSTRUCT?
5. Do czego służy ASK?
6. Czym jest SPARQL Update?
7. Jak oznacza się zmienną?
8. Do czego służy PREFIX?
9. Gdzie może działać zapytanie?
10. Co opisuje wzorzec trójki?

## Odpowiedzi

1. Językiem zapytań do RDF.
2. Wzorem opisującym szukane trójki.
3. Do zwracania wyników tabelarycznych.
4. Do budowania grafu z wyników.
5. Do sprawdzenia, czy istnieje dopasowanie.
6. Do modyfikowania danych RDF.
7. Znakiem `?` albo `$`.
8. Do skrócenia IRI.
9. Lokalnie albo przez endpoint SPARQL.
10. Subject, predicate i object z możliwymi zmiennymi.

[Powrót do spisu treści](README.md)
