# Output odpowiedzi query

Odpowiedź Elasticsearch nie zawiera tylko listy znalezionych dokumentów. Zawiera także informacje potrzebne do oceny trafności, czasu wykonania i stanu pracy shardów.

## Najważniejsza struktura odpowiedzi

Typowa odpowiedź search zawiera pola `took`, `timed_out`, `_shards` i `hits`. `took` informuje o czasie wykonania po stronie Elasticsearch, `timed_out` mówi o przekroczeniu limitu, a `_shards` pokazuje, ile shardów uczestniczyło w operacji i czy któryś zgłosił błąd.

```json
{
  "took": 7,
  "timed_out": false,
  "_shards": {
    "total": 3,
    "successful": 3,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 2,
      "relation": "eq"
    },
    "max_score": 1.4,
    "hits": []
  }
}
```

## Hits i total

`hits` jest listą dopasowanych dokumentów, a `hits.total` opisuje liczbę wszystkich trafień niezależnie od bieżącego `size`. Wartość `relation` mówi, czy liczba jest dokładna (`eq`), czy tylko oszacowana (`gte`).

`size` ogranicza liczbę zwracanych dokumentów, ale nie zmienia całkowitej liczby dopasowań. Przy dużych zbiorach nie należy zakładać, że `hits.total` zawsze jest dokładnym pełnym zliczeniem bez dodatkowego kosztu.

## `_source`, `_id` i `_score`

Każdy element `hits.hits` może zawierać `_index`, `_id`, `_score` oraz `_source`. `_source` jest oryginalnym dokumentem, `_id` identyfikuje dokument, a `_score` opisuje dopasowanie do konkretnego query.

```json
{
  "_index": "products",
  "_id": "book-42",
  "_score": 1.4,
  "_source": {
    "title": "Elasticsearch od podstaw",
    "category": "books"
  }
}
```

`_score` nie jest oceną biznesową. Jeśli query używa wyłącznie filtrów, wynik może nie mieć użytecznej wartości rankingowej. Sortowanie po własnym polu trzeba zaprojektować jawnie.

## `_source` filtering

Gdy dokument zawiera dużo pól, można ograniczyć odpowiedź przez `_source` filtering:

```http
GET products/_search
Content-Type: application/json

{
  "_source": ["title", "category"],
  "query": {
    "match": {
      "title": "elasticsearch"
    }
  }
}
```

Zmniejsza to rozmiar odpowiedzi, ale nie zmienia samego dopasowania. Nie należy mylić ograniczenia `_source` z wyłączeniem pola z indeksowania.

## Highlight

[Highlighting](00%20Glossary%20Elasticsearch.md#highlighting) dodaje fragmenty tekstu pokazujące, gdzie dokument pasuje do query:

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "match": {
      "description": "search"
    }
  },
  "highlight": {
    "fields": {
      "description": {}
    }
  }
}
```

Highlight jest funkcją prezentacyjną. Nie powinien być traktowany jako dowód, że ranking jest poprawny, ani jako zamiennik przechowywanego `_source`.

## Agregacje w odpowiedzi

[Aggregations](00%20Glossary%20Elasticsearch.md#aggregations) pojawiają się obok `hits`, gdy query zawiera sekcję `aggs`. Wynik agregacji nie jest kolejną listą dokumentów, tylko podsumowaniem lub grupowaniem:

```http
GET products/_search
Content-Type: application/json

{
  "size": 0,
  "aggs": {
    "by_category": {
      "terms": {
        "field": "category"
      }
    }
  }
}
```

`size: 0` oznacza, że interesują nas agregacje, a nie lista dokumentów. To często właściwy wybór dla dashboardów.

## Jak czytać odpowiedź diagnostycznie

Przed uznaniem query za poprawne sprawdź:

- czy `timed_out` jest `false`,
- czy `_shards.failed` wynosi zero,
- czy `hits.total` ma właściwą relację,
- czy `_score` odpowiada intencji query,
- czy `_source` zawiera pola potrzebne UI,
- czy agregacje używają właściwego mappingu.

Samo HTTP `200` nie oznacza, że wynik jest semantycznie poprawny. Odpowiedź może być formalnie poprawna, ale zawierać timeout, częściowy błąd shardów albo ranking niepasujący do wymagań.

## Co zapamiętać

- Odpowiedź search opisuje dokumenty, ranking, czas i stan shardów.
- `hits.total` i `hits.hits` mają różne role.
- `_source` to oryginalne dane dokumentu, a `_score` to wynik dopasowania.
- Highlight służy prezentacji fragmentów dopasowania.
- Agregacje pojawiają się obok hits i mogą działać bez zwracania dokumentów.
- Zawsze sprawdzaj `_shards.failed` i `timed_out`, nie tylko kod HTTP.
