# Python i zdalny endpoint

## Opis

Python może komunikować się z Fuseki przez HTTP. Do prostych operacji wystarczą biblioteki HTTP, a do pracy lokalnej przydatny jest RDFLib; ważne jest rozróżnienie endpointu query, update i data.

## Kluczowe koncepty

- **HTTP client** — biblioteka wysyłająca żądania.
- **SPARQLWrapper** — biblioteka upraszczająca zapytania SPARQL.
- **Query URL** — endpoint odczytu.
- **Update URL** — endpoint modyfikacji.
- **Response parsing** — odczyt odpowiedzi JSON, CSV lub RDF.

## Key points

- Zapytanie do Fuseki nie musi ładować całego grafu do pamięci.
- Parametry endpointu i dane uwierzytelniające należy konfigurować bezpiecznie.
- Wynik SELECT można czytać jako JSON.
- Dane RDF można wysłać jako Turtle przez HTTP.
- W produkcji trzeba obsłużyć timeouty i błędy HTTP.

## Example

```python
import requests

query = "SELECT * WHERE { ?s ?p ?o } LIMIT 5"
r = requests.post(
    "http://localhost:3030/ds/sparql",
    data={"query": query},
    headers={"Accept": "application/sparql-results+json"},
    timeout=10,
)
r.raise_for_status()
print(r.json())
```

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Instalujemy `requests` albo `SPARQLWrapper`.
2. Ustawiamy adres query endpointu.
3. Budujemy zapytanie.
4. Wysyłamy żądanie z timeoutem.
5. Parsujemy odpowiedź.
6. Obsługujemy błędy i logujemy metadane bez sekretów.

## Pytania

1. Jak Python komunikuje się z Fuseki?
2. Czy trzeba pobierać cały graf?
3. Do czego służy requests?
4. Do czego służy SPARQLWrapper?
5. Co zwraca SELECT?
6. Dlaczego potrzebny jest timeout?
7. Gdzie trzymać dane dostępowe?
8. Jak wysłać Turtle?
9. Co zrobić z błędem HTTP?
10. Czym różni się lokalny Graph od endpointu?

## Odpowiedzi

1. Przez HTTP.
2. Nie, można wysłać zapytanie do endpointu.
3. Do wykonywania żądań HTTP.
4. Do wygodnej obsługi zapytań SPARQL.
5. Wyniki związania zmiennych.
6. Aby aplikacja nie czekała bez końca.
7. Poza kodem, w bezpiecznej konfiguracji.
8. Żądaniem HTTP do endpointu data.
9. Obsłużyć, zarejestrować i nie ignorować.
10. Graph jest lokalny, endpoint zdalny.

[Powrót do spisu treści](README.md)
