# Przepływ danych

Praca z dokumentem nie kończy się na wysłaniu jednego żądania. Elasticsearch przyjmuje dokument, udostępnia go do wyszukiwania po <a id="term-refresh"></a>[refresh](00%20Glossary%20Elasticsearch.md#refresh), zwraca go przez <a id="term-search"></a>[search](00%20Glossary%20Elasticsearch.md#search), a później może go zmienić przez <a id="term-update"></a>[update](00%20Glossary%20Elasticsearch.md#update) albo usunąć przez <a id="term-delete"></a>[delete](00%20Glossary%20Elasticsearch.md#delete).

```text
index → refresh → search → update → delete
```

Ten przepływ wyjaśnia ważną właściwość Elasticsearch: zapis dokumentu i jego widoczność w wynikach wyszukiwania to dwa powiązane, ale różne momenty.

## Index: zapis dokumentu

Operacja <a id="term-indexing"></a>[indexing](00%20Glossary%20Elasticsearch.md#indexing) zapisuje dokument pod identyfikatorem. Jeżeli dokument o tym ID już istnieje, zapis zastępuje jego źródło:

```http
PUT products/_doc/book-42
Content-Type: application/json

{
  "title": "Elasticsearch od podstaw",
  "category": "books",
  "price": 49.90
}
```

ID może nadać aplikacja albo Elasticsearch. Jawny ID jest przydatny, gdy ponawianie żądania ma być idempotentne, czyli ponowny zapis tego samego dokumentu nie powinien tworzyć kolejnej kopii.

## Refresh: widoczność w wyszukiwaniu

[Refresh](00%20Glossary%20Elasticsearch.md#refresh) udostępnia ostatnie zmiany strukturom wyszukiwania. Domyślnie Elasticsearch wykonuje refresh okresowo, dlatego dokument może być zapisany, ale przez krótką chwilę niewidoczny w search.

```http
POST products/_refresh
```

Parametr `refresh=wait_for` pozwala poczekać na najbliższy refresh po zapisie:

```http
PUT products/_doc/book-42?refresh=wait_for
Content-Type: application/json

{
  "title": "Elasticsearch od podstaw",
  "category": "books"
}
```

Wymuszanie refresh po każdym zapisie zwiększa koszt operacji. Dla importu wielu dokumentów lepiej pozwolić Elasticsearchowi odświeżać indeks według normalnego harmonogramu.

## Search: odczyt dokumentów

Operacja search zwraca dokumenty pasujące do query. Wynik zawiera między innymi listę `hits`, `_source` oraz informacje o czasie i shardach:

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

Search czyta struktury przygotowane podczas indeksowania. Nie skanuje bezmyślnie każdego dokumentu w taki sam sposób jak prosta pętla po JSON-ach, dlatego mapping i analyzer wpływają na wynik oraz koszt zapytania.

## Update: zmiana fragmentu dokumentu

Update modyfikuje istniejący dokument bez konieczności wysyłania wszystkich jego pól. Elasticsearch odczytuje dokument, stosuje zmianę i ponownie indeksuje wynik:

```http
POST products/_update/book-42
Content-Type: application/json

{
  "doc": {
    "price": 39.90
  }
}
```

Update nie jest tym samym co częściowa zmiana w miejscu. Wewnętrznie dokument jest przygotowywany ponownie, więc częste aktualizacje dużych dokumentów mogą być kosztowne.

Można też użyć skryptu, gdy zmiana zależy od poprzedniej wartości:

```http
POST products/_update/book-42
Content-Type: application/json

{
  "script": {
    "source": "ctx._source.views += params.increment",
    "params": {
      "increment": 1
    }
  }
}
```

## Delete: usunięcie dokumentu

Delete usuwa dokument po jego ID:

```http
DELETE products/_doc/book-42
```

Usunięcie również musi przejść przez refresh, aby dokument przestał pojawiać się w wynikach wyszukiwania. Odpowiedź operacji informuje, czy dokument został usunięty, czy nie istniał.

Można usuwać także dokumenty pasujące do query przez `delete_by_query`, ale taka operacja powinna być wykonywana ostrożnie, z ograniczeniem zakresu i monitorowaniem wyników.

## Spójność przepływu

Każda operacja ma inny cel:

| Operacja | Zmienia dane? | Wpływa na widoczność w search? |
|---|---:|---:|
| `index` | Tak | Po refresh |
| `refresh` | Nie zmienia źródła | Udostępnia zmiany |
| `search` | Nie | Odczytuje widoczne dane |
| `update` | Tak | Po refresh |
| `delete` | Tak | Po refresh |

Dla aplikacji oznacza to, że odpowiedź `200 OK` po zapisie nie musi oznaczać, że natychmiastowe search zwróci nowy dokument. Jeżeli workflow wymaga odczytu zaraz po zapisie, użyj `refresh=wait_for` świadomie, tylko w miejscach, gdzie opóźnienie jest ważniejsze niż przepustowość.

## Co zapamiętać

- `index` zapisuje dokument, `search` go odczytuje, `update` modyfikuje, a `delete` usuwa.
- `refresh` decyduje o udostępnieniu zmian dla wyszukiwania.
- Zapis i widoczność w search nie są tym samym momentem.
- `refresh=wait_for` pomaga w workflow wymagającym odczytu po zapisie.
- Częsty refresh i aktualizowanie dużych dokumentów zwiększają koszt.
- Jawne ID ułatwia idempotentne ponawianie operacji.
