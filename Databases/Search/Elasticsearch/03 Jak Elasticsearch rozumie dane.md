# Jak Elasticsearch rozumie dane

<a id="term-mapping"></a>Mapping jest kontraktem między dokumentem a wyszukiwaniem. Określa, jak Elasticsearch ma rozumieć każde pole, jak je indeksować oraz jakie operacje będą na nim dostępne. Kształt JSON-a mówi, jakie dane wysyłamy; mapping mówi, jak te dane mają działać.

```text
dokument JSON
    ↓
mapping
    ↓
typy pól i sposób indeksowania
    ↓
match / term / range / sort / agregacja
```

Jeżeli pole zostanie zmapowane niezgodnie z rzeczywistym zastosowaniem, problem pojawi się dopiero przy zapytaniu.

## Typ pola wynika z pytania

Do wyszukiwania tekstu służy <a id="term-text"></a>[`text`](00%20Glossary%20Elasticsearch.md#text), do dokładnych filtrów <a id="term-keyword"></a>[`keyword`](00%20Glossary%20Elasticsearch.md#keyword), do kwot <a id="term-scaled-float"></a>[`scaled_float`](00%20Glossary%20Elasticsearch.md#scaled-float), a do relacji w tablicach obiektów <a id="term-nested"></a>[`nested`](00%20Glossary%20Elasticsearch.md#nested).

Przed zdefiniowaniem mappingu warto spisać operacje, które aplikacja ma wykonywać. Na przykład `text` jest dobry do wyszukiwania słów, ale nie jest domyślnie dobrym polem do sortowania.

| Potrzeba | Typ pola | Przykład |
|---|---|---|
| Wyszukiwanie fragmentów tekstu | `text` | tytuł, opis |
| Dokładny filtr lub grupowanie | `keyword` | status, kod, kategoria |
| Wartość całkowita | `integer` lub `long` | liczba sztuk |
| Wartość dziesiętna | `float` lub `double` | ocena |
| Kwota wymagająca kontroli precyzji | `scaled_float` | cena |
| Data i zakres czasu | `date` | data publikacji |
| Prawda albo fałsz | `boolean` | dostępność |
| Relacja wewnątrz tablicy obiektów | `nested` | autorzy, warianty |

Nie wybieraj typu tylko dlatego, że odpowiada typowi w języku programowania. Wybierz go na podstawie tego, jak pole będzie wyszukiwane, filtrowane, sortowane i agregowane.

## `text` i `keyword`

To najważniejsza decyzja dla pól tekstowych. `text` jest analizowany przez [analyzer](00%20Glossary%20Elasticsearch.md#analyzer), a jego zawartość jest przygotowywana do [full-text search](00%20Glossary%20Elasticsearch.md#full-text-search). `keyword` przechowuje wartość jako całość i służy do dokładnego dopasowania, sortowania oraz agregacji.

```json
{
  "properties": {
    "title": { "type": "text" },
    "category": { "type": "keyword" }
  }
}
```

Dla `title` sensowne jest zapytanie `match`. Dla `category` sensowne jest `term`, ponieważ kategoria powinna być porównana jako dokładna wartość.

## Multi-field

Czasem to samo pole powinno obsługiwać dwa różne zastosowania. <a id="term-multi-field"></a>Multi-field indeksuje je pod kilkoma nazwami:

```json
{
  "properties": {
    "title": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword"
        }
      }
    }
  }
}
```

W tym mappingu:

- `title` służy do wyszukiwania pełnotekstowego,
- `title.keyword` służy do dokładnego dopasowania i sortowania.

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "match": {
      "title": "elasticsearch"
    }
  },
  "sort": [
    "title.keyword"
  ]
}
```

Multi-field nie tworzy drugiej wartości w dokumencie. Tworzy drugi sposób indeksowania tej samej wartości.

## Obiekty i `nested`

Dokument może zawierać obiekty zagnieżdżone. Domyślny typ <a id="term-object"></a>[object](00%20Glossary%20Elasticsearch.md#object) jest wygodny dla prostych struktur, ale tablica obiektów wymaga uwagi. Elasticsearch może spłaszczyć pola tak, że warunki pochodzące z różnych elementów tablicy zostaną potraktowane jak jedna kombinacja.

```json
{
  "name": "Książka",
  "authors": [
    { "name": "Anna", "country": "PL" },
    { "name": "John", "country": "US" }
  ]
}
```

`nested` zachowuje relację między polami tego samego elementu tablicy. Jest właściwy wtedy, gdy pytanie brzmi: „czy istnieje jeden autor, który jednocześnie spełnia oba warunki?”.

```http
PUT books
Content-Type: application/json

{
  "mappings": {
    "properties": {
      "authors": {
        "type": "nested",
        "properties": {
          "name": { "type": "text" },
          "country": { "type": "keyword" }
        }
      }
    }
  }
}
```

Zapytanie `nested` ogranicza warunki do jednego elementu tablicy. `nested` jest dokładniejszy semantycznie, ale zwiększa złożoność zapytań i koszt przetwarzania. Nie używaj go automatycznie dla każdego obiektu zagnieżdżonego.

## Mapping jawny i dynamiczny

Elasticsearch może sam utworzyć mapping na podstawie pierwszego dokumentu. To jest <a id="term-dynamic-mapping"></a>[dynamic mapping](00%20Glossary%20Elasticsearch.md#dynamic-mapping). Ułatwia szybki start, ale typ wybrany automatycznie może nie pasować do późniejszego zastosowania pola.

Ważne indeksy zwykle warto tworzyć z mappingiem jawnym:

```http
PUT products
Content-Type: application/json

{
  "mappings": {
    "dynamic": "strict",
    "properties": {
      "name": {
        "type": "text",
        "fields": {
          "keyword": { "type": "keyword" }
        }
      },
      "status": { "type": "keyword" },
      "price": {
        "type": "scaled_float",
        "scaling_factor": 100
      },
      "created_at": { "type": "date" }
    }
  }
}
```

Tryb <a id="term-strict"></a>[`strict`](00%20Glossary%20Elasticsearch.md#strict) odrzuca dokument z nieznanym polem. To pomaga wykryć literówki i niekontrolowane zmiany struktury. Tryb dynamiczny może być właściwy dla danych elastycznych, ale powinien być świadomą decyzją.

## Mapping nie jest łatwy do zmiany

Po utworzeniu indeksu nie można dowolnie zmienić typu istniejącego pola. Zmiana `text` na `keyword` albo `integer` na `date` wymaga nowego indeksu i ponownego zindeksowania dokumentów.

Typowy przepływ wygląda tak:

```text
products-v1
    ↓
nowy mapping
    ↓
products-v2
    ↓
reindex
    ↓
alias products wskazuje v2
```

<a id="term-reindex"></a>[Reindex](00%20Glossary%20Elasticsearch.md#reindex) kopiuje dokumenty do nowego indeksu według nowego mappingu. <a id="term-alias"></a>[Alias](00%20Glossary%20Elasticsearch.md#alias) pozwala aplikacji korzystać ze stałej nazwy logicznej, mimo że fizyczny indeks zmienia wersję.

```http
POST _reindex
Content-Type: application/json

{
  "source": {
    "index": "products-v1"
  },
  "dest": {
    "index": "products-v2"
  }
}
```

Po sprawdzeniu nowego indeksu alias można przełączyć atomowo:

```http
POST _aliases
Content-Type: application/json

{
  "actions": [
    { "remove": { "alias": "products", "index": "products-v1" } },
    { "add": { "alias": "products", "index": "products-v2" } }
  ]
}
```

## Jak sprawdzić mapping

Aktualny mapping indeksu odczytasz przez:

```http
GET products/_mapping
```

Przed zmianą mappingu sprawdź także rzeczywiste zapytania aplikacji. Sam JSON dokumentu nie odpowiada na pytanie, czy pole powinno być `text`, `keyword`, `date` albo `nested`.

## Co zapamiętać

- Mapping opisuje zachowanie pól, a nie tylko kształt dokumentu.
- `text` i `keyword` są przeznaczone do różnych operacji.
- Multi-field pozwala wyszukiwać tekst i jednocześnie sortować po dokładnej wartości.
- `nested` zachowuje relacje między polami jednego elementu tablicy.
- Dynamic mapping jest wygodny, ale jawny mapping daje większą kontrolę.
- Zmiana typu pola wymaga nowego indeksu i reindeksacji.
- Alias oddziela nazwę używaną przez aplikację od fizycznej wersji indeksu.
- Mapping projektuj na podstawie zapytań, filtrów, sortowania i agregacji.
