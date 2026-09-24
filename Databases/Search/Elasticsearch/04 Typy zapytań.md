# Typy zapytań

Po zaprojektowaniu mappingu trzeba dobrać query do rodzaju pytania. `match` szuka analizowanego tekstu, `term` porównuje dokładną wartość, a pozostałe query budują warunki na dokumentach.

## Wyszukiwanie analizowanego tekstu

[Match query](00%20Glossary%20Elasticsearch.md#match-query) służy do wyszukiwania tekstu w polach `text`. Treść query przechodzi przez analyzer, więc zapytanie odpowiada sposobowi, w jaki tekst został przygotowany podczas indeksowania:

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "match": {
      "title": "elasticsearch search"
    }
  }
}
```

`match` nie jest porównaniem całej wartości znak po znaku. Jeżeli aplikacja ma wyszukiwać dokładny kod albo status, użyj `term` na polu `keyword`.

## Dokładna wartość

[Term query](00%20Glossary%20Elasticsearch.md#term-query) nie analizuje tekstu zapytania. Porównuje wartość dokładnie, dlatego nadaje się do kategorii, statusów, identyfikatorów i wartości logicznych:

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "term": {
      "category": "books"
    }
  }
}
```

Wartość `Books` może nie pasować do `books`. Jeżeli dokładne wartości mają być niewrażliwe na wielkość liter, trzeba przewidzieć to w mappingu przez <a id="term-normalizer"></a>[normalizer](00%20Glossary%20Elasticsearch.md#normalizer).

## Łączenie warunków

[Bool query](00%20Glossary%20Elasticsearch.md#bool-query) łączy kilka warunków w jednym query. `must` opisuje główne dopasowanie, `filter` zawęża wyniki bez wpływania na ranking, `must_not` wyklucza dokumenty, a `should` dodaje preferowane dopasowania:

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "bool": {
      "must": [
        { "match": { "title": "elasticsearch" } }
      ],
      "filter": [
        { "term": { "available": true } },
        { "range": { "price": { "lte": 100 } } }
      ],
      "must_not": [
        { "term": { "visibility": "hidden" } }
      ]
    }
  }
}
```

Warunki dotyczące statusu, ceny i dostępności zwykle należą do `filter`. Dzięki temu ranking opisuje dopasowanie tekstu, a nie przypadkową różnicę między filtrami.

## Zakres wartości

[Range query](00%20Glossary%20Elasticsearch.md#range-query) porównuje wartości uporządkowane, takie jak liczby i daty. Obsługuje operatory `gt`, `gte`, `lt` i `lte`:

```json
{
  "query": {
    "range": {
      "price": {
        "gte": 20,
        "lt": 100
      }
    }
  }
}
```

Range query nie zastępuje wyszukiwania tekstowego. Pole musi mieć typ, dla którego istnieje naturalny porządek, na przykład `integer`, `float` albo `date`.

## Istnienie pola

<a id="term-exists-query"></a>[Exists query](00%20Glossary%20Elasticsearch.md#exists-query) sprawdza, czy dokument ma indeksowaną wartość pod wskazaną nazwą pola:

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "exists": {
      "field": "description"
    }
  }
}
```

`exists` nie sprawdza, czy tekst jest sensowny ani czy liczba jest różna od zera. Sprawdza dostępność wartości w indeksie. Można użyć go także w `must_not`, aby znaleźć dokumenty bez pola.

## Początek wartości

<a id="term-prefix-query"></a>[Prefix query](00%20Glossary%20Elasticsearch.md#prefix-query) dopasowuje wartości zaczynające się od podanego prefiksu. Najczęściej stosuje się go na polu `keyword`:

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

`prefix` nie jest tym samym co pełnotekstowe `match`. Działa na indeksowanej wartości i nie analizuje jej tak jak zwykłe wyszukiwanie tekstu. Dla rozbudowanego autocomplete lepszy może być osobny analyzer albo `search_as_you_type`.

## Wybór query

| Pytanie | Query | Typ pola |
|---|---|---|
| Czy tekst pasuje znaczeniowo? | `match` | `text` |
| Czy wartość jest dokładnie taka sama? | `term` | `keyword`, liczba, boolean |
| Czy dokument spełnia kilka warunków? | `bool` | różne pola |
| Czy wartość mieści się w zakresie? | `range` | liczba, data |
| Czy pole istnieje? | `exists` | dowolne indeksowane pole |
| Czy wartość zaczyna się od prefiksu? | `prefix` | najczęściej `keyword` |

Najpierw nazwij pytanie biznesowe, potem wybierz query. Nie wybieraj query na podstawie samej nazwy pola, ponieważ jedno pole może mieć różne zastosowania przez multi-field.

## Co zapamiętać

- `match` analizuje tekst, a `term` porównuje dokładną wartość.
- `bool` składa większe zapytanie z warunków o różnych rolach.
- `filter` zawęża wyniki bez zmiany score.
- `range` służy do liczb i dat.
- `exists` sprawdza obecność wartości.
- `prefix` szuka wartości zaczynających się od podanego tekstu.
- Query musi pasować do mappingu pola.
