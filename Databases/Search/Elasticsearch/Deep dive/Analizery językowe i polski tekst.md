# Analizery językowe i polski tekst

Wyszukiwanie językowe zależy od tego, jak tekst zostanie podzielony, znormalizowany i sprowadzony do tokenów. Ten sam analyzer musi być oceniany na realnych przykładach, ponieważ poprawność techniczna nie gwarantuje dobrego dopasowania dla języka polskiego.

## Analyzer, tokenizer i token filter

[Analyzer](00%20Glossary%20Elasticsearch.md#analyzer) składa się z tokenizera i filtrów tokenów. Tokenizer dzieli tekst na tokeny, a [token filter](00%20Glossary%20Elasticsearch.md#token-filter) może je zmieniać, usuwać albo wzbogacać.

```json
{
  "analysis": {
    "analyzer": {
      "pl_search": {
        "type": "custom",
        "tokenizer": "standard",
        "filter": ["lowercase"]
      }
    }
  }
}
```

Podczas indeksowania analyzer przygotowuje wartość dokumentu. Podczas search analyzer przygotowuje tekst query. Te dwa etapy nie muszą używać identycznej konfiguracji, ale muszą tworzyć porównywalne tokeny.

## Lowercase i stop words

[Lowercase filter](00%20Glossary%20Elasticsearch.md#lowercase-filter) normalizuje wielkość liter. Dzięki temu `Elasticsearch` i `elasticsearch` mogą być traktowane tak samo. [Stop words](00%20Glossary%20Elasticsearch.md#stop-words) usuwają słowa uznane za mało informacyjne, ale ich dobór zależy od języka i celu wyszukiwania.

Usunięcie stop words może poprawić stosunek sygnału do szumu, ale może też usunąć słowo istotne dla domeny. Lista powinna być testowana na rzeczywistych zapytaniach, a nie przyjmowana bez sprawdzenia.

## Stemming i odmiana słów

[Stemming](00%20Glossary%20Elasticsearch.md#stemming) sprowadza odmiany słów do wspólnej postaci, dzięki czemu różne formy mogą znaleźć ten sam dokument. Dla języka polskiego trzeba użyć właściwych reguł językowych i sprawdzić, czy nie powstają fałszywe dopasowania.

Przykładowy test powinien obejmować odmiany, liczby, polskie znaki i słowa podobne znaczeniowo. Nie zakładaj, że lowercase rozwiązuje problem odmiany wyrazów.

## `_analyze` jako narzędzie diagnostyczne

Endpoint `_analyze` pokazuje tokeny dla wybranego analyzera:

```http
POST products/_analyze
Content-Type: application/json

{
  "analyzer": "standard",
  "text": "Książki o wyszukiwaniu w języku polskim"
}
```

Porównaj wynik analyzera indeksującego i search analyzera. Jeśli tokeny nie odpowiadają temu, co aplikacja chce znaleźć, problem trzeba rozwiązać w analizie lub mappingu, nie przez przypadkową zmianę query.

## Zmiana analyzera

Analyzer indeksujący jest częścią sposobu przygotowania danych. Po zmianie konfiguracji zwykle trzeba utworzyć nowy indeks i wykonać reindex, ponieważ istniejące tokeny nie zostaną przeliczone automatycznie.

## Co zapamiętać

- Analyzer łączy tokenizer i token filters.
- Indeksowanie i search mogą używać różnych analyzerów, ale tokeny muszą być porównywalne.
- Lowercase rozwiązuje wielkość liter, nie odmianę słów.
- Stop words i stemming trzeba testować na danych domenowych.
- `_analyze` jest podstawowym narzędziem diagnozowania analizy tekstu.
- Zmiana analyzera zwykle wymaga nowego indeksu i reindex.