# Jak działa wyszukiwanie

Wyszukiwanie w Elasticsearch jest wynikiem współpracy trzech elementów: mappingu, przygotowania tekstu i <a id="term-query"></a>[query](00%20Glossary%20Elasticsearch.md#query). Mapping mówi, czym jest pole. <a id="term-analyzer"></a>[Analyzer](00%20Glossary%20Elasticsearch.md#analyzer) przygotowuje tekst do porównania. Query określa, czego szukamy.

```text
mapping pola
    ↓
analyzer podczas indeksowania
    ↓
wartości dostępne w strukturach wyszukiwania
    ↓
query użytkownika
    ↓
hits uporządkowane według score
```

Nie istnieje jedno uniwersalne zapytanie do wszystkich pól. To samo żądanie może być właściwe dla `text`, a niewłaściwe dla `keyword`. Dlatego diagnozowanie wyszukiwania zaczyna się od sprawdzenia mappingu, a nie od przypadkowego zmieniania query.

## Analiza tekstu

Dla pola [`text`](00%20Glossary%20Elasticsearch.md#text) Elasticsearch nie musi przechowywać tekstu wyłącznie jako jednej wartości do dokładnego porównania. Analyzer rozkłada tekst na <a id="term-token"></a>[tokeny](00%20Glossary%20Elasticsearch.md#token) i może go normalizować. Na przykład tytuł `Elasticsearch od podstaw` może zostać przygotowany jako kilka tokenów zapisanych w strukturach wyszukiwania.

Analyzer składa się zwykle z <a id="term-tokenizer"></a>[tokenizera](00%20Glossary%20Elasticsearch.md#tokenizer) i filtrów. Tokenizer dzieli tekst na tokeny, a filtr może zmienić ich postać, na przykład zapisać litery małymi znakami. Ta sama logika analizy powinna być przemyślana dla indeksowania i dla zapytań, inaczej tekst zapisany i tekst szukany mogą nie być porównywalne.

Do sprawdzenia wyniku analizy służy endpoint `_analyze`:

```http
POST products/_analyze
Content-Type: application/json

{
  "analyzer": "standard",
  "text": "Elasticsearch od podstaw"
}
```

Wynik pokazuje tokeny, które Elasticsearch może wykorzystać przy wyszukiwaniu. To najprostszy sposób, aby sprawdzić, dlaczego dana odmiana słowa albo wielkość liter pasuje lub nie pasuje do dokumentu.

## Wyszukiwanie analizowane

<a id="term-match-query"></a>[`match`](00%20Glossary%20Elasticsearch.md#match-query) jest podstawowym query dla analizowanego wyszukiwania po polach `text`:
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

Treść zapytania przechodzi przez analyzer, a następnie Elasticsearch porównuje powstałe tokeny z tokenami dokumentów. Wyniki otrzymują score, czyli ocenę dopasowania do konkretnego query.

`match` nie oznacza wyszukiwania identycznego całego pola. Jeżeli potrzebujesz dopasowania dokładnej wartości, użyj pola `keyword` i query <a id="term-term-query"></a>[`term`](00%20Glossary%20Elasticsearch.md#term-query).

## Dokładne dopasowanie wartości

`term` porównuje wartość bez analizowania jej jako tekstu. Pasuje do pól [`keyword`](00%20Glossary%20Elasticsearch.md#keyword), liczb, wartości logicznych i innych pól, dla których ważna jest dokładność:

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

Jeżeli `category` jest polem `keyword`, wartość `Books` może nie pasować do `books`. To nie jest błąd query, tylko konsekwencja dokładnego charakteru pola. Normalizację wielkości liter trzeba przewidzieć w mappingu.

Najkrótsza reguła wyboru wygląda tak:

| Cel | Pole | Query |
|---|---|---|
| Szukanie słów i fragmentów tekstu | `text` | `match` |
| Dokładny status lub kod | `keyword` | `term` |
| Zakres liczb albo dat | `integer`, `float`, `date` | `range` |

## Łączenie warunków przez `bool`

Rzeczywiste wyszukiwanie zwykle łączy tekst użytkownika z filtrami katalogowymi. Do budowania takiego query służy <a id="term-bool-query"></a>[bool query](00%20Glossary%20Elasticsearch.md#bool-query).

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "title": "elasticsearch"
          }
        }
      ],
      "filter": [
        {
      ## `term` dla dokładnej wartości
            "category": "books"
          }
        },
        {
          "range": {
            "price": {
              "lte": 100
            }
          }
        },
        {
          "term": {
            "available": true
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "visibility": "hidden"
          }
        }
      ]
    }
  }
}
```

`must` opisuje warunek głównego dopasowania. `filter` zawęża wyniki według warunków, które zwykle nie powinny zmieniać score. `must_not` wyklucza dokumenty. `should` może wskazywać dodatkowe preferowane dopasowania.

Rozdzielenie wyszukiwania tekstowego od filtrów jest ważne także dla czytelności. Tekst wpływa na ranking, a status, cena i dostępność najczęściej są tylko ograniczeniami zbioru wyników.

## Score nie jest oceną biznesową

Score mówi, jak dobrze dokument pasuje do konkretnego query. Nie jest ogólną oceną jakości produktu ani jego popularności. Ten sam dokument może otrzymać inną wartość score po zmianie tekstu zapytania albo zbioru dokumentów.

Na wynik może wpływać między innymi obecność tokenu, częstość tokenu w dokumencie, rzadkość tokenu w indeksie, długość tekstu oraz struktura query. Do wyszukiwania tej samej treści w kilku polach służy <a id="term-multi-match"></a>[`multi_match`](00%20Glossary%20Elasticsearch.md#multi-match). Znaczenie wybranego pola można zwiększyć przez <a id="term-boost"></a>[boost](00%20Glossary%20Elasticsearch.md#boost):

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "multi_match": {
      "query": "elasticsearch",
      "fields": [
        "title^3",
        "description"
      ]
    }
  }
}
```

`multi_match` wyszukuje tę samą frazę w kilku polach. `title^3` zwiększa wpływ pola `title` na ranking. Boost jest wskazówką dla rankingu, a nie gwarancją kolejności w każdej sytuacji.

## Zakresy

<a id="term-range-query"></a>[Range query](00%20Glossary%20Elasticsearch.md#range-query) służy do porównań wartości uporządkowanych, najczęściej liczb i dat:

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

`gt` oznacza „większe niż”, `gte` „większe lub równe”, `lt` „mniejsze niż”, a `lte` „mniejsze lub równe”. Dla dat można używać także wartości względnych, na przykład `now-30d/d`.

## Gdy wynik jest pusty

Brak wyników nie musi oznaczać, że dokumentu nie ma w indeksie. Sprawdź kolejno:

1. Czy query wskazuje właściwy indeks.
2. Czy pole istnieje w mappingu.
3. Czy `match`, `term` albo `range` pasuje do typu pola.
4. Czy dokładna wartość `keyword` ma właściwą wielkość liter.
5. Jak analyzer przetworzył tekst przez `_analyze`.
6. Czy dokument jest już widoczny po odświeżeniu indeksu.
7. Czy filtr nie wyklucza wszystkich dokumentów.

Do obejrzenia mappingu służy:

```http
GET products/_mapping
```

Do sprawdzenia dokumentów bez złożonych warunków można użyć prostego:

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "match_all": {}
  }
}
```

## Przepływ zapytania

Dla katalogu produktów pełny przepływ może wyglądać tak:

```text
tekst użytkownika → match na title
filtry katalogowe → filter
wykluczenia → must_not
sortowanie lub paginacja → parametry wyników
odpowiedź → hits i score
```

Najpierw sprawdź, czy mapping umożliwia oczekiwane operacje. Potem dobierz query do typu pola. Na końcu oceń wyniki na rzeczywistych przykładach, bo poprawna składnia nie gwarantuje użytecznego rankingu.

## Co zapamiętać

- Mapping, analyzer i query tworzą jeden system.
- Analyzer przygotowuje tekst do indeksowania i wyszukiwania.
- `match` służy głównie do analizowanego wyszukiwania po `text`.
- `term` służy do dokładnych wartości, najczęściej `keyword`.
- `bool` pozwala połączyć główne wyszukiwanie, filtry i wykluczenia.
- `filter` zawęża wyniki i zwykle nie wpływa na score.
- Score opisuje dopasowanie do query, nie wartość biznesową dokumentu.
- Przy pustym wyniku najpierw sprawdź mapping, analyzer i typ query.
