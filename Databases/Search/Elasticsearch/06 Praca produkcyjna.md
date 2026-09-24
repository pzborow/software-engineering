# Praca produkcyjna

W produkcji Elasticsearch trzeba zarządzać nie tylko query, ale też sposobem rozmieszczenia danych, zmianą indeksów, importem i backupem. Najważniejsza decyzja brzmi: jak utrzymać wyszukiwanie dostępne, przewidywalne i możliwe do odtworzenia.

## Shardy i repliki

[Shard](00%20Glossary%20Elasticsearch.md#shard) jest fragmentem indeksu. [Primary shard](00%20Glossary%20Elasticsearch.md#primary-shard) przechowuje główną kopię fragmentu, a [replica shard](00%20Glossary%20Elasticsearch.md#replica-shard) jego kopię. Elasticsearch może rozłożyć je między nody, aby część pracy wykonywać równolegle i przetrwać awarię jednego noda.

```text
products
├── primary shard 0  ── node-a
├── replica shard 0  ── node-b
└── primary shard 1  ── node-b
```

Replica nie jest backupem. Chroni przed awarią części klastra, ale nie przed przypadkowym usunięciem lub błędnym update wykonanym poprawnie na wszystkich kopiach.

## Liczba shardów

Liczbę primary shardów wybiera się przy tworzeniu indeksu. Zbyt wiele shardów zwiększa narzut zarządzania, a zbyt mało może ograniczyć rozłożenie danych i pracy.

Nie ma jednej idealnej liczby shardów dla każdego indeksu. Decyzję należy oprzeć na rozmiarze danych, liczbie zapytań, tempie indeksowania i planowanym wzroście. Pusty indeks z dziesiątkami shardów może być problemem jeszcze zanim pojawią się właściwe dane.

## Alias i zmiana wersji indeksu

[Alias](00%20Glossary%20Elasticsearch.md#alias) jest logiczną nazwą wskazującą na fizyczny indeks. Aplikacja może używać `products`, podczas gdy rzeczywisty indeks nazywa się `products-v2`:

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

Alias pozwala przygotować nową wersję indeksu, przetestować ją i przełączyć ruch bez zmiany konfiguracji aplikacji. Przełączenie operacji aliasów jest atomowe.

## Reindex

[Reindex](00%20Glossary%20Elasticsearch.md#reindex) kopiuje dokumenty do innego indeksu. Używa się go po zmianie mappingu, analyzera albo struktury dokumentów:

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

Reindex nie jest magiczną zmianą typu pola w istniejącym indeksie. Tworzy dokumenty w miejscu docelowym według mappingu tego indeksu, dlatego przed przełączeniem aliasu trzeba sprawdzić błędy, liczbę dokumentów i wyniki przykładowych zapytań.

## Bulk

<a id="term-bulk-api"></a>[Bulk API](00%20Glossary%20Elasticsearch.md#bulk-api) przyjmuje wiele operacji w jednym żądaniu. Zmniejsza narzut komunikacji przy imporcie, ale odpowiedź trzeba analizować dla każdej operacji osobno:

```http
POST _bulk
Content-Type: application/x-ndjson

{ "index": { "_index": "products", "_id": "book-42" } }
{ "title": "Elasticsearch od podstaw", "price": 49.90 }
{ "delete": { "_index": "products", "_id": "old-book" } }
```

Bulk nie gwarantuje, że wszystkie operacje zakończą się sukcesem. Import powinien obsługiwać częściowe błędy, retry, idempotencję i kontrolowany rozmiar paczek.

## Snapshot

[Snapshot](00%20Glossary%20Elasticsearch.md#snapshot) jest backupem danych klastra zapisanym w repozytorium snapshotów. Replika nie zastępuje snapshotu, bo replika nie chroni przed logicznym błędem wykonanym na całym indeksie.

Backup jest użyteczny dopiero wtedy, gdy można z niego odtworzyć dane. Dlatego należy testować restore, znać czas odtworzenia i przechowywać kopie poza tym samym punktem awarii.

## Operacyjna checklista

Przed produkcją sprawdź:

- czy liczba shardów odpowiada rozmiarowi i wzrostowi danych,
- czy repliki są rozmieszczone na innych nodach,
- czy aplikacja używa aliasu zamiast wersji fizycznego indeksu,
- czy reindex można wykonać bez przerwy w wyszukiwaniu,
- czy bulk raportuje częściowe błędy,
- czy snapshot i restore były przetestowane.

## Co zapamiętać

- Primary i replica shardy rozwiązują problemy dostępności i skali, ale replica nie jest backupem.
- Alias umożliwia bezpieczne przełączanie wersji indeksu.
- Reindex buduje nowy indeks, gdy zmiana starego mappingu nie jest możliwa.
- Bulk zmniejsza narzut importu, ale wymaga analizy błędów każdej operacji.
- Snapshot jest podstawą odtworzenia danych po awarii lub błędzie logicznym.
