# Django: projekcja, synchronizacja i reindeksacja

Integracja Django z Elasticsearch polega zwykle na zbudowaniu dokumentu będącego projekcją modelu. Model Django pozostaje źródłem prawdy, a dokument jest przygotowany pod konkretne query i widoki wyszukiwania.

## Dokument jako projekcja modelu

[Django Elasticsearch DSL](00%20Glossary%20Elasticsearch.md#django-elasticsearch-dsl) pozwala zdefiniować dokument Elasticsearch na podstawie modelu Django:

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

Dokument nie musi kopiować wszystkich pól modelu. Powinien zawierać te dane, które są potrzebne do wyszukiwania, filtrowania, sortowania i prezentacji wyników.

## ID modelu i powrót do bazy

Warto przechowywać ID modelu Django w dokumencie. Wynik search może wtedy zwrócić dokument indeksu, a aplikacja może pobrać aktualny rekord ze źródła prawdy:

```json
{
  "_source": {
    "django_id": 123,
    "title": "Elasticsearch od podstaw",
    "category": "books"
  }
}
```

ID nie oznacza, że Elasticsearch przejmuje rolę bazy. Jest kluczem do powiązania projekcji z rekordem źródłowym.

## Synchronizacja zmian

[Synchronization](00%20Glossary%20Elasticsearch.md#synchronization) oznacza utrzymywanie zgodności modelu Django i dokumentu Elasticsearch. Może odbywać się przez sygnały, zadania asynchroniczne albo okresowe importy.

Każdy mechanizm musi odpowiedzieć na pytania: co dzieje się po utworzeniu modelu, zmianie pola, usunięciu rekordu i błędzie połączenia z Elasticsearch. Warto rejestrować błędne operacje i mieć możliwość ponowienia ich bez tworzenia duplikatów.

## Synchronizacja asynchroniczna

[Asynchronous indexing](00%20Glossary%20Elasticsearch.md#asynchronous-indexing) zmniejsza opóźnienie żądania webowego, bo aktualizacja indeksu jest wykonywana przez worker. Zwiększa jednak okno, w którym baza i search pokazują różne dane.

Aplikacja powinna komunikować, czy wynik wyszukiwania może być eventual, czy dana operacja wymaga potwierdzenia aktualizacji indeksu.

## Rebuild indeksu

[Rebuild](00%20Glossary%20Elasticsearch.md#rebuild) tworzy indeks od nowa na podstawie modeli Django. Jest potrzebny po zmianie mappingu, analyzera, struktury dokumentu albo po wykryciu większej niespójności.

Bezpieczny rebuild powinien:

1. utworzyć nowy indeks,
2. załadować dokumenty ze źródła prawdy,
3. sprawdzić mapping i przykładowe query,
4. przełączyć alias,
5. obserwować błędy synchronizacji.

## Testowanie

Testuj nie tylko wynik query, ale cały przepływ: zapis modelu, utworzenie dokumentu, zmianę, usunięcie i odbudowę indeksu. Warto sprawdzać także przypadki, gdy dokument jest chwilowo niewidoczny po zapisie.

## Co zapamiętać

- Dokument Django jest projekcją danych, nie zamiennikiem modelu.
- ID modelu pozwala wrócić z wyniku search do źródła prawdy.
- Synchronizacja musi obsługiwać utworzenie, zmianę, usunięcie i retry.
- Asynchroniczny indexing zmniejsza opóźnienie requestu, ale zwiększa okno niespójności.
- Rebuild pozwala odbudować indeks po zmianie mappingu lub struktury dokumentu.
