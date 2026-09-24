# Integracja

Elasticsearch jest osobnym serwisem, więc aplikacja komunikuje się z nim przez <a id="term-rest-api"></a>[REST API](00%20Glossary%20Elasticsearch.md#rest-api) albo klienta języka programowania. Integracja powinna rozdzielać konfigurację połączenia, operacje na indeksach i logikę wyszukiwania.

## REST jako kontrakt

REST API udostępnia operacje Elasticsearch przez endpointy HTTP. Ten sam model URL i body można później odwzorować w kliencie Python:

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

REST jest dobry do nauki, debugowania i sprawdzania dokładnej treści żądania. W aplikacji produkcyjnej klient biblioteczny może dodać obsługę połączeń, serializację i typowanie, ale nie zmienia semantyki query.

## Klient Python

<a id="term-elasticsearch-python-client"></a>[Elasticsearch Python client](00%20Glossary%20Elasticsearch.md#elasticsearch-python-client) jest biblioteką, która mapuje operacje REST na metody Pythona. Połączenie powinno mieć jawny adres, timeout i bezpieczny sposób uwierzytelniania:

```python
from elasticsearch import Elasticsearch

client = Elasticsearch(
    "https://localhost:9200",
    api_key="${ELASTIC_API_KEY}",
    request_timeout=10,
)

print(client.info())
```

`client.info()` jest prostym testem, ale nie zastępuje testu właściwego query. Aplikacja powinna obsługiwać błędy połączenia, timeouty i odpowiedzi częściowo nieudanych operacji bulk.

## Query w Pythonie

Query DSL można przekazać jako słownik Pythona. Dzięki temu aplikacja może budować filtry na podstawie parametrów użytkownika, ale nadal powinna kontrolować, jakie pola i operatory są dozwolone:

```python
response = client.search(
    index="products",
    query={
        "bool": {
            "must": [
                {"match": {"title": "elasticsearch"}},
            ],
            "filter": [
                {"term": {"available": True}},
            ],
        },
    },
)

for hit in response["hits"]["hits"]:
    print(hit["_source"])
```

Nie należy przyjmować dowolnego fragmentu query od użytkownika bez walidacji. Aplikacja powinna kontrolować indeks, pola, limity rozmiaru odpowiedzi i maksymalny koszt zapytania.

## Dokument Django

<a id="term-django-elasticsearch-dsl"></a>[Django Elasticsearch DSL](00%20Glossary%20Elasticsearch.md#django-elasticsearch-dsl) opisuje, jak synchronizować modele Django z dokumentami Elasticsearch. Dokument jest projekcją modelu albo kilku modeli, przygotowaną pod wyszukiwanie:

```python
from django_elasticsearch_dsl import Document, fields
from django_elasticsearch_dsl.registries import registry

from .models import Article


@registry.register_document
class ArticleDocument(Document):
    title = fields.TextField()
    category = fields.KeywordField()

    class Index:
        name = "articles"

    class Django:
        model = Article
        fields = ["id", "published_at"]
```

Dokument Elasticsearch nie zastępuje automatycznie modelu Django. Zwykle baza relacyjna pozostaje źródłem prawdy, a indeks Elasticsearch jest projekcją zoptymalizowaną pod wyszukiwanie.

## Synchronizacja i spójność

Synchronizacja może działać przez sygnały aplikacyjne, zadania asynchroniczne albo okresowy import. Trzeba zdecydować, co dzieje się po zmianie lub usunięciu modelu oraz jak obsłużyć opóźnienie między bazą a indeksem.

Aplikacja powinna mieć możliwość odbudowania indeksu ze źródła prawdy. To ogranicza ryzyko, że chwilowy błąd synchronizacji zostanie utrwalony jako brak danych w wyszukiwaniu.

## Bezpieczna konfiguracja

Adres serwera, certyfikaty, API key i timeouty nie powinny być zaszyte w kodzie. Trzymaj je w konfiguracji środowiska, ogranicz uprawnienia klucza i nie loguj sekretów ani pełnych dokumentów zawierających dane wrażliwe.

## Co zapamiętać

- REST jest podstawowym kontraktem, a klient Python wygodniejszą warstwą nad tym samym API.
- Query DSL można przekazać jako słownik Pythona.
- Klient powinien mieć timeout, obsługę błędów i bezpieczne uwierzytelnianie.
- Dokument Django jest zwykle projekcją danych, nie zamiennikiem modelu i źródła prawdy.
- Indeks powinno dać się odbudować ze źródła prawdy.
