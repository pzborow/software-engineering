# Instalacja, Docker i health klastra

Lokalne uruchomienie Elasticsearch powinno dać możliwość szybkiego sprawdzenia API, stanu klastra i logów. Docker upraszcza start, ale nie zastępuje konfiguracji zasobów, bezpieczeństwa i trwałego storage.

## Elasticsearch w Dockerze

Najprostszy lokalny kontener może wyglądać tak:

```bash
docker network create elastic

docker run --name elasticsearch --net elastic \\
  -p 9200:9200 -p 9300:9300 \\
  -e discovery.type=single-node \\
  -e xpack.security.enabled=false \\
  docker.elastic.co/elasticsearch/elasticsearch:8.15.0
```

Parametr `discovery.type=single-node` jest wygodny lokalnie, ale nie opisuje architektury produkcyjnego klastra. Wyłączenie security powinno być ograniczone do izolowanego środowiska developerskiego.

## Sprawdzenie połączenia

[Cluster health](00%20Glossary%20Elasticsearch.md#cluster-health) pokazuje stan klastra:

```http
GET _cluster/health
```

Stan `green` oznacza, że primary i replica shardy są przydzielone. `yellow` zwykle oznacza działające primary przy nieprzydzielonych replikach, co jest częste w klastrze jedno-węzłowym. `red` oznacza problem z co najmniej jednym primary shardem.

## Podstawowa diagnostyka

Po uruchomieniu sprawdź także:

```http
GET

GET _cat/nodes?v

GET _cat/indices?v

GET products/_mapping
```

Endpointy `_cat` są wygodne do diagnostyki operatorskiej, a mapping pozwala potwierdzić, jak Elasticsearch interpretuje pola indeksu.

## Kibana

[Kibana](00%20Glossary%20Elasticsearch.md#kibana) jest interfejsem do pracy z Elasticsearch, wizualizacji i eksploracji danych. W środowisku lokalnym pomaga wykonywać requesty, oglądać indeksy i analizować dashboardy.

Kibana nie zastępuje API ani monitoringu. Jest narzędziem operatorskim i developerskim; produkcyjny system wymaga także alertów, logów, metryk oraz procedur odtwarzania.

## Storage i bezpieczeństwo

Kontener bez trwałego volume może utracić dane po usunięciu kontenera. W środowisku trwałym skonfiguruj storage, limity pamięci, backupy i TLS.

Nie wystawiaj niezabezpieczonego Elasticsearch do publicznej sieci. Dane dostępowe trzymaj poza plikiem obrazu i ogranicz uprawnienia klientów.

## Co zapamiętać

- Docker upraszcza lokalny start, ale nie jest konfiguracją produkcyjną.
- `/_cluster/health` jest podstawowym testem stanu klastra.
- `green`, `yellow` i `red` opisują stan przydziału shardów.
- W klastrze jedno-węzłowym `yellow` może wynikać z braku miejsca dla repliki.
- Kibana pomaga eksplorować dane, ale nie zastępuje API i monitoringu.
- Produkcja wymaga trwałego storage, security, backupu i kontroli zasobów.
