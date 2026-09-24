# Routing dokumentów

Elasticsearch musi zdecydować, do którego shardu trafi dokument. Domyślnie oblicza routing na podstawie identyfikatora dokumentu i liczby primary shardów.

## Domyślny routing

[Routing](00%20Glossary%20Elasticsearch.md#routing) jest wartością używaną do wyboru shardu. W domyślnym scenariuszu dokumenty rozkładają się według `_id`, dzięki czemu kolejne ID nie trafiają automatycznie do jednego shardu.

```text
shard = hash(_routing) mod number_of_primary_shards
```

Domyślny routing jest zwykle wystarczający. Ważne jest jednak, aby pamiętać, że zwiększenie liczby primary shardów zmienia sposób rozkładu nowych dokumentów i jest decyzją indeksu.

## Custom routing

[Custom routing](00%20Glossary%20Elasticsearch.md#custom-routing) pozwala użyć własnej wartości zamiast `_id`, na przykład `tenant_id`. Dokumenty jednego klienta mogą wtedy trafić do tego samego shardu:

```http
PUT orders/_doc/order-42?routing=tenant-7
Content-Type: application/json

{
  "tenant_id": "tenant-7",
  "total": 129.90
}
```

Odczyt dokumentu musi użyć tej samej wartości routingu:

```http
GET orders/_doc/order-42?routing=tenant-7
```

Brak właściwego routingu może sprawić, że Elasticsearch nie znajdzie dokumentu albo przeszuka niepotrzebnie wiele shardów.

## Korzyści i ryzyka

Routing może ograniczyć zakres zapytań do jednego shardu, co bywa przydatne dla izolacji tenantów. Jednocześnie nierówny rozkład wartości może stworzyć [hot shard](00%20Glossary%20Elasticsearch.md#hot-shard), czyli shard przeciążony większą ilością danych lub ruchu niż pozostałe.

Custom routing komplikuje także reindex, usuwanie i zapytania administracyjne. Warto go wprowadzać dopiero po pomiarach i po określeniu, jak aplikacja zawsze uzyska właściwą wartość routingu.

## Co zapamiętać

- Routing decyduje, do którego primary shardu trafi dokument.
- Domyślnie routing opiera się na `_id`.
- Custom routing może grupować dokumenty jednego tenanta na shardzie.
- Odczyt dokumentu z custom routing wymaga tej samej wartości.
- Nierówny routing może stworzyć hot shard.