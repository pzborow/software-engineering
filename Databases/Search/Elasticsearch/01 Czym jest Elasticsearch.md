# Czym jest Elasticsearch

Elasticsearch jest rozproszonym silnikiem wyszukiwania i analizy danych. Przyjmuje <a id="term-document"></a>[dokumenty](00%20Glossary%20Elasticsearch.md#document) w formacie JSON, indeksuje ich <a id="term-field"></a>[pola](00%20Glossary%20Elasticsearch.md#field), a następnie udostępnia je przez zapytania HTTP. Jego głównym zadaniem jest szybkie znajdowanie i porządkowanie dokumentów według treści, filtrów lub wartości liczbowych.

Najprostszy model działania wygląda tak:

```text
dokument JSON
    ↓
indeksowanie
    ↓
indeks
    ↓
zapytanie
    ↓
wyniki wyszukiwania
```

## Dokumenty zamiast wierszy

Podstawową jednostką danych jest dokument. Dokument opisuje jeden obiekt jako JSON, na przykład produkt:

```json
{
  "id": "book-42",
  "title": "Elasticsearch od podstaw",
  "category": "books",
  "price": 49.90,
  "available": true
}
```

Dokument może zawierać tekst, liczby, daty, wartości logiczne, tablice i obiekty zagnieżdżone. Dokumenty w jednym <a id="term-index"></a>[indeksie](00%20Glossary%20Elasticsearch.md#index) nie muszą mieć dokładnie tego samego zestawu pól, ale sposób traktowania pól ustala <a id="term-mapping"></a>[mapping](00%20Glossary%20Elasticsearch.md#mapping).

## Indeks jako przestrzeń wyszukiwania

Dokumenty podobnego rodzaju umieszcza się w indeksie. Dla przykładu indeks `products` może zawierać produkty, a indeks `orders` zamówienia. Nazwa indeksu pojawia się w adresie żądania i wskazuje, gdzie Elasticsearch ma zapisać dokument albo gdzie ma szukać wyników.

Indeks nie jest jednak zwykłą tabelą. Oprócz dokumentów zawiera struktury przygotowane specjalnie do wyszukiwania. Dlatego projekt indeksu powinien wynikać z pytań, które aplikacja będzie zadawać danym.

## Mapping mówi, jak czytać pola

Mapping określa typy pól i sposób ich indeksowania. Dla przykładowego produktu możemy zdefiniować:

```json
{
  "properties": {
    "title": { "type": "text" },
    "category": { "type": "keyword" },
    "price": { "type": "float" },
    "available": { "type": "boolean" }
  }
}
```

Pole <a id="term-text"></a>[`text`](00%20Glossary%20Elasticsearch.md#text) jest przygotowywane do <a id="term-full-text-search"></a>[wyszukiwania pełnotekstowego](00%20Glossary%20Elasticsearch.md#full-text-search). Elasticsearch może podzielić jego zawartość na <a id="term-token"></a>[tokeny](00%20Glossary%20Elasticsearch.md#token) i normalizować tekst. Pole <a id="term-keyword"></a>[`keyword`](00%20Glossary%20Elasticsearch.md#keyword) jest traktowane jako dokładna wartość, dlatego pasuje do filtrów, sortowania i <a id="term-agregacja"></a>[agregacji](00%20Glossary%20Elasticsearch.md#agregacja). `float` pozwala wykonywać porównania liczbowe, a `boolean` przechowuje prawdę albo fałsz.

Po tytule książki zwykle szukamy słów, natomiast kategorię chcemy filtrować jako dokładną wartość. Dlatego jedno pole może potrzebować dwóch sposobów indeksowania, na przykład `title` do wyszukiwania i `title.keyword` do sortowania.

## Architektura klastra

Elasticsearch może działać jako pojedyncza instancja, ale jego architektura pozwala rozdzielać dane i pracę między wiele instancji. <a id="term-cluster"></a>[Cluster](00%20Glossary%20Elasticsearch.md#cluster) to cały logiczny system Elasticsearch, <a id="term-node"></a>[node](00%20Glossary%20Elasticsearch.md#node) to pojedyncza instancja należąca do klastra, a <a id="term-shard"></a>[shard](00%20Glossary%20Elasticsearch.md#shard) to fragment indeksu.

```text
cluster
├── node-a
│   └── products: shard 0
└── node-b
    └── products: shard 1
```

Podział indeksu na shardy pozwala obsługiwać większe zbiory danych i wykonywać część pracy równolegle. Każdy indeks ma <a id="term-primary-shard"></a>[primary shardy](00%20Glossary%20Elasticsearch.md#primary-shard). Można także utworzyć <a id="term-replica-shard"></a>[replica shardy](00%20Glossary%20Elasticsearch.md#replica-shard), czyli kopie shardów podstawowych. Repliki zwiększają odporność na awarię i mogą obsługiwać odczyty, ale nie są backupem. Backup wykonuje się za pomocą <a id="term-snapshot"></a>[snapshotów](00%20Glossary%20Elasticsearch.md#snapshot).

## Od dokumentu do wyszukiwania

Podczas indeksowania Elasticsearch przygotowuje pola zgodnie z mappingiem. Dla pola `text` <a id="term-analyzer"></a>[analyzer](00%20Glossary%20Elasticsearch.md#analyzer) dzieli tekst na tokeny i może normalizować ich postać. Te tokeny trafiają do struktur, które pozwalają później szybko znaleźć pasujące dokumenty. Oryginalna treść dokumentu pozostaje dostępna jako <a id="term-source"></a>[`_source`](00%20Glossary%20Elasticsearch.md#source).

```text
tytuł dokumentu
    ↓
analyzer
    ↓
tokeny
    ↓
struktury indeksu
    ↓
match query
    ↓
hits i score
```

Analyzer korzysta między innymi z <a id="term-tokenizer"></a>[tokenizera](00%20Glossary%20Elasticsearch.md#tokenizer), który dzieli tekst na tokeny. Filtry mogą na przykład zmienić litery na małe. Dzięki temu wyszukiwanie tekstu nie musi polegać na porównaniu całego pola znak po znaku.

Zapytanie <a id="term-match-query"></a>[`match`](00%20Glossary%20Elasticsearch.md#match-query) jest przeznaczone głównie do analizowanego wyszukiwania po polach `text`. Zapytanie <a id="term-term-query"></a>[`term`](00%20Glossary%20Elasticsearch.md#term-query) porównuje dokładną wartość i dlatego zwykle stosuje się je dla pól `keyword`.

## Jeden przepływ

Najpierw tworzymy indeks z mappingiem:

```http
PUT products
Content-Type: application/json

{
  "mappings": {
    "properties": {
      "title": { "type": "text" },
      "category": { "type": "keyword" },
      "price": { "type": "float" },
      "available": { "type": "boolean" }
    }
  }
}
```

Następnie zapisujemy dokument pod znanym identyfikatorem:

```http
PUT products/_doc/book-42
Content-Type: application/json

{
  "title": "Elasticsearch od podstaw",
  "category": "books",
  "price": 49.90,
  "available": true
}
```

Po zapisaniu możemy wyszukać tekst w tytule:

```http
GET products/_search
Content-Type: application/json

{
  "query": {
    "match": {
      "title": "elasticsearch"
    }
  }
}
```

Albo odfiltrować dokładną kategorię:

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

Wynik wyszukiwania zawiera między innymi <a id="term-hits"></a>[`hits`](00%20Glossary%20Elasticsearch.md#hits), czyli dopasowane dokumenty, `_source`, czyli ich oryginalne dane, oraz <a id="term-score"></a>[`_score`](00%20Glossary%20Elasticsearch.md#score), czyli ocenę dopasowania zapytania do dokumentu. Dokument może stać się widoczny dla wyszukiwania chwilę po zapisie, ponieważ Elasticsearch działa w modelu <a id="term-near-real-time"></a>[near real-time](00%20Glossary%20Elasticsearch.md#near-real-time).

## Co zapamiętać

- Elasticsearch wyszukuje i analizuje dokumenty JSON.
- Indeks jest przestrzenią wyszukiwania, a nie prostą tabelą.
- Mapping określa, jak Elasticsearch rozumie pola.
- `text` służy głównie do full-text search, a `keyword` do dokładnych wartości.
- Cluster składa się z nodes, a indeks może być podzielony na shardy.
- Replica zwiększa dostępność, ale snapshot jest właściwym backupem.
- Analyzer przygotowuje tekst do wyszukiwania, a `_source` zachowuje oryginalny dokument.
- `match` i `term` wybiera się na podstawie typu pola.
