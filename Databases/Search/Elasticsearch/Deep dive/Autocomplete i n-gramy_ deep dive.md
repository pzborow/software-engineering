# Autocomplete i n-gramy: deep dive

Autocomplete może używać prefiksów albo <a id="term-ngram"></a>[n-gramów](00%20Glossary%20Elasticsearch.md#ngram). N-gram dzieli token na nakładające się fragmenty, a edge n-gram ogranicza fragmenty do początku tokenu. Dla `Jan Kowalski` n-gram długości 2 może utworzyć między innymi `ja`, `an`, `ko`, `ow` i `wa`.

## Dedykowane pole

Nie zmieniaj zwykłego pola wyszukiwawczego tylko po to, aby obsłużyć autocomplete. Dodaj multi-field albo osobne pole, ponieważ indeksowanie n-gramów zwiększa liczbę tokenów i rozmiar indeksu.

```json
{
  "mappings": {
    "properties": {
      "name": {
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

Pole `name` pozostaje dobre dla zwykłego full-text search, a `name.autocomplete` służy do podpowiedzi.

## Analyzer indeksujący i search analyzer

Analyzer indeksujący tworzy n-gramy podczas zapisu dokumentu. Search analyzer powinien zwykle analizować wpis użytkownika bez tworzenia kolejnego zestawu n-gramów:

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

Dla wyszukiwania po dowolnym fragmencie słowa można użyć zwykłego `ngram`, ale generuje on więcej tokenów niż `edge_ngram`. W klasycznym autocomplete prefiksowym edge n-gram jest zwykle bardziej przewidywalny.

## Kolejność filtrów

Filtry są stosowane w kolejności zapisanej w analyzerze. Lowercase powinien poprzedzać edge n-gram, aby tokeny były normalizowane przed utworzeniem prefiksów. Stop words i stemming trzeba dobierać ostrożnie, bo mogą zmienić oczekiwany kształt podpowiedzi.

## Testowanie przez `_analyze`

Zanim zaczniesz oceniać query, sprawdź tokeny:

```http
POST products/_analyze
Content-Type: application/json

{
  "analyzer": "autocomplete_index",
  "text": "Jan Kowalski"
}
```

Sprawdź krótkie prefiksy, polskie znaki, wielkość liter, dwuczłonowe nazwy oraz wartości zawierające cyfry. Jeśli analyzer tworzy nieoczekiwane tokeny, query nie naprawi problemu bez zmiany konfiguracji indeksu.

## Rozmiar i wydajność

`min_gram` oraz `max_gram` są kompromisem między jakością podpowiedzi a kosztem indeksu. Zbyt małe gramy tworzą dużo tokenów, a zbyt duże mogą nie obsługiwać krótkich zapytań.

Ogranicz liczbę wyników, stosuj minimalną długość wpisu i debounce po stronie UI. Autocomplete nie powinien wysyłać ciężkiego query dla każdego znaku bez kontroli częstotliwości.

## Co zapamiętać

- N-gram tworzy nakładające się fragmenty tokenu, a edge n-gram fragmenty od początku.
- Autocomplete powinien mieć osobne pole lub multi-field.
- Analyzer indeksujący i search analyzer mają różne role.
- Kolejność filtrów wpływa na tokeny.
- `_analyze` pozwala sprawdzić, co naprawdę trafiło do indeksu.
- Zakres gramów wpływa bezpośrednio na rozmiar i koszt indeksu.
