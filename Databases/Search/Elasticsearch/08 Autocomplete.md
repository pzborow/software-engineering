# Autocomplete

Autocomplete podpowiada wyniki podczas wpisywania tekstu. Nie jest tym samym co zwykły full-text search: użytkownik wysyła niepełny tekst, a indeks musi być przygotowany do dopasowania prefiksu przez <a id="term-edge-ngram"></a>[edge n-gram](00%20Glossary%20Elasticsearch.md#edge-ngram) albo typ pola <a id="term-search-as-you-type"></a>[`search_as_you_type`](00%20Glossary%20Elasticsearch.md#search-as-you-type).

## Prefiks i edge n-gram

Edge n-gram jest fragmentem tokenu tworzonym od jego początku. Dla słowa `elasticsearch` może utworzyć `el`, `ela`, `elas` i kolejne prefiksy. Dzięki temu zapytanie `elas` może znaleźć pełną wartość.

```json
{
  "settings": {
    "analysis": {
      "filter": {
        "autocomplete_edge": {
          "type": "edge_ngram",
          "min_gram": 2,
          "max_gram": 15
        }
      },
      "analyzer": {
        "autocomplete_index": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": ["lowercase", "autocomplete_edge"]
        },
        "autocomplete_search": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": ["lowercase"]
        }
      }
    }
  }
}
```

Analyzer indeksujący tworzy prefiksy, a search analyzer analizuje zapytanie prościej. Oddzielenie tych ról ogranicza ryzyko, że krótki tekst zapytania zostanie niepotrzebnie pocięty drugi raz.

## Pole autocomplete

Pole autocomplete powinno często być multi-fieldem, aby zwykłe wyszukiwanie i podpowiedzi nie wymuszały tego samego sposobu indeksowania:

```json
{
  "mappings": {
    "properties": {
      "title": {
        "type": "text",
        "fields": {
          "autocomplete": {
            "type": "text",
            "analyzer": "autocomplete_index",
            "search_analyzer": "autocomplete_search"
          }
        }
      }
    }
  }
}
```

Zapytanie może użyć pola `title.autocomplete`:

```http
GET products/_search
Content-Type: application/json

{
  "size": 5,
  "_source": ["title"],
  "query": {
    "match": {
      "title.autocomplete": "elas"
    }
  }
}
```

Zakres `min_gram` i `max_gram` jest decyzją o kompromisie. Małe gramy zwiększają liczbę tokenów i rozmiar indeksu, a zbyt duże mogą pogorszyć podpowiedzi dla krótkich zapytań.

## search_as_you_type

Typ pola `search_as_you_type` jest gotowym rozwiązaniem dla typowych podpowiedzi tekstowych. Elasticsearch tworzy pomocnicze pola i można użyć query `bool_prefix`:

```http
PUT products
Content-Type: application/json

{
  "mappings": {
    "properties": {
      "title": {
        "type": "search_as_you_type"
      }
    }
  }
}
```

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "multi_match": {
      "query": "elast",
      "type": "bool_prefix",
      "fields": [
        "title",
        "title._2gram",
        "title._3gram",
        "title._index_prefix"
      ]
    }
  }
}
```

`search_as_you_type` zmniejsza ilość własnej konfiguracji, ale daje mniej kontroli niż własny analyzer z edge n-gram. Wybierz je, gdy potrzebujesz typowego wyszukiwania podczas pisania, a nie niestandardowych reguł językowych.

## Prefix query

[Prefix query](00%20Glossary%20Elasticsearch.md#prefix-query) działa na początku indeksowanej wartości. Jest prosty i przydatny dla pól `keyword`, na przykład kodów produktów:

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "prefix": {
      "sku": "book-"
    }
  }
}
```

Prefix query nie zastępuje analizowanego autocomplete dla zdań i nazw. Jeśli podpowiedzi mają uwzględniać analizę językową, użyj edge n-gram albo `search_as_you_type`.

## Produkcyjne ograniczenia

Autocomplete powinien mieć limit wyników, minimalną długość zapytania i kontrolę opóźnienia. Nie wysyłaj zapytania dla każdego pojedynczego znaku bez debouncingu po stronie aplikacji.

Testuj rzeczywiste przypadki: polskie znaki, wielkość liter, krótkie prefiksy, literówki i wartości o wspólnym początku. Zmiana analyzera wymaga nowego indeksu i reindeksacji.

## Co zapamiętać

- Edge n-gram tworzy prefiksy tokenów podczas indeksowania.
- `search_as_you_type` jest wygodnym typem pola dla typowego autocomplete.
- Prefix query pasuje do początku dokładnej wartości.
- Osobne pole autocomplete chroni zwykłe full-text search przed kompromisami.
- Autocomplete wymaga limitów, debouncingu i pomiaru rozmiaru indeksu.
