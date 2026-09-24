# Glosariusz Elasticsearch

## Spis haseł

- [Analyzer](#analyzer)
- [Document](#document)
- [Field](#field)
- [Index](#index)
- [Mapping](#mapping)
- [Text](#text)
- [Keyword](#keyword)
- [Full-text search](#full-text-search)
- [Token](#token)
- [Tokenizer](#tokenizer)
- [Cluster](#cluster)
- [Node](#node)
- [Shard](#shard)
- [Replica shard](#replica-shard)
- [Snapshot](#snapshot)
- [Primary shard](#primary-shard)
- [Hits](#hits)
- [`_source`](#source)
- [`_score`](#score)
- [Near real-time](#near-real-time)
- [`match` query](#match-query)
- [`term` query](#term-query)
- [Agregacja](#agregacja)
- [Query](#query)
- [Bool query](#bool-query)
- [Range query](#range-query)
- [Multi-match](#multi-match)
- [Boost](#boost)
- [Multi-field](#multi-field)
- [Scaled float](#scaled-float)
- [Object](#object)
- [Nested](#nested)
- [Dynamic mapping](#dynamic-mapping)
- [Strict](#strict)
- [Reindex](#reindex)
- [Alias](#alias)

<a id="analyzer"></a>
## Analyzer

Mechanizm przygotowujący tekst do indeksowania i wyszukiwania. Zwykle składa się z tokenizera oraz filtrów.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-analyzer).

<a id="document"></a>
## Document

Pojedynczy obiekt JSON przechowywany w indeksie. Dokument opisuje jeden obiekt, na przykład produkt albo zamówienie.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-document).

<a id="field"></a>
## Field

Nazwana wartość wewnątrz dokumentu, na przykład `title`, `price` albo `available`. Typ pola określa, jak można go używać.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-field).

<a id="index"></a>
## Index

Logiczny zbiór dokumentów przeznaczonych do wspólnego wyszukiwania. Indeks ma mapping i jest podzielony na shardy.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-index).

<a id="mapping"></a>
## Mapping

Definicja pól indeksu, ich typów i sposobu indeksowania. Mapping określa, jak Elasticsearch interpretuje dane dokumentu.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-mapping).

<a id="text"></a>
## Text

Typ pola przeznaczony głównie do full-text search. Wartość jest analizowana i zwykle dzielona na tokeny.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-text).

<a id="keyword"></a>
## Keyword

Typ pola przechowujący wartość jako całość. Stosuje się go głównie do dokładnych filtrów, sortowania i agregacji.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-keyword).

<a id="full-text-search"></a>
## Full-text search

Wyszukiwanie tekstu po znaczących fragmentach, a nie tylko po dokładnej całej wartości. Wykorzystuje analizę tekstu i ranking wyników.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-full-text-search).

<a id="token"></a>
## Token

Fragment tekstu powstały w wyniku analizy, używany przez struktury wyszukiwania.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-token).

<a id="tokenizer"></a>
## Tokenizer

Element analyzera, który dzieli tekst wejściowy na tokeny.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-tokenizer).

<a id="cluster"></a>
## Cluster

Logiczna całość złożona z jednej lub wielu instancji Elasticsearch. Cluster koordynuje przechowywanie danych i operacje na indeksach.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-cluster).

<a id="node"></a>
## Node

Pojedyncza uruchomiona instancja Elasticsearch należąca do klastra. Node może przechowywać shardy i obsługiwać żądania.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-node).

<a id="shard"></a>
## Shard

Fragment indeksu. Podział na shardy pozwala rozłożyć dane i pracę między nody.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-shard).

<a id="replica-shard"></a>
## Replica shard

Kopia primary shardu. Replica zwiększa dostępność danych i może obsługiwać odczyty, ale nie zastępuje backupu.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-replica-shard).

<a id="snapshot"></a>
## Snapshot

Backup danych Elasticsearch zapisany w repozytorium snapshotów. Służy do odtworzenia danych po awarii lub błędnej operacji.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-snapshot).

<a id="primary-shard"></a>
## Primary shard

Podstawowy shard indeksu, do którego trafia główna kopia dokumentów. Replica shard jest jego kopią.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-primary-shard).

<a id="hits"></a>
## Hits

Lista dokumentów dopasowanych przez zapytanie wyszukiwania. Odpowiedź Elasticsearch umieszcza ją zwykle pod kluczem `hits`.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-hits).

<a id="source"></a>
## `_source`

Oryginalna treść dokumentu JSON przechowywana wraz z dokumentem i zwracana domyślnie w wynikach wyszukiwania.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-source).

<a id="score"></a>
## `_score`

Ocena dopasowania dokumentu do zapytania. Nie jest ogólną oceną jakości dokumentu ani wartością biznesową.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-score).

<a id="near-real-time"></a>
## Near real-time

Model, w którym zapisane dane stają się dostępne dla wyszukiwania po krótkim opóźnieniu, a niekoniecznie natychmiast po zapisie.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-near-real-time).

<a id="match-query"></a>
## `match` query

Zapytanie przeznaczone głównie do analizowanego wyszukiwania po polach `text`. Treść zapytania przechodzi przez analyzer.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-match-query).

<a id="term-query"></a>
## `term` query

Zapytanie porównujące dokładną wartość pola, najczęściej `keyword`, bez analizowania treści zapytania.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-term-query).

<a id="agregacja"></a>
## Agregacja

Operacja podsumowująca dokumenty, na przykład zliczająca produkty według kategorii albo obliczająca średnią cenę.

Powiązany temat: [rozdział 01](../01%20Czym%20jest%20Elasticsearch.md#term-agregacja).

<a id="query"></a>
## Query

Definicja warunków wyszukiwania przekazana do Elasticsearch. Query określa, które dokumenty mają zostać znalezione i jak ocenić ich dopasowanie. [Pierwsza wzmianka](../02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#term-query).

<a id="bool-query"></a>
## Bool query

Query, które łączy warunki `must`, `should`, `filter` i `must_not`. Pozwala oddzielić wyszukiwanie wpływające na ranking od filtrów zawężających wyniki. [Pierwsza wzmianka](../02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#term-bool-query).

<a id="range-query"></a>
## Range query

Query służące do porównań zakresów liczb, dat i innych uporządkowanych wartości. [Pierwsza wzmianka](../02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#term-range-query).

<a id="multi-match"></a>
## Multi-match

Query wyszukujące tę samą treść w kilku polach dokumentu, z możliwością nadania polom różnych wag. [Pierwsza wzmianka](../02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#term-multi-match).

<a id="boost"></a>
## Boost

Współczynnik zwiększający wpływ dopasowania wybranego pola lub warunku na ranking wyników. [Pierwsza wzmianka](../02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#term-boost).

<a id="multi-field"></a>
## Multi-field

Konfiguracja, w której jedno pole jest indeksowane na kilka sposobów, na przykład jako `text` i `keyword`. [Pierwsza wzmianka](../03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-multi-field).

<a id="scaled-float"></a>
## Scaled float

Typ liczbowy przechowujący wartość zmiennoprzecinkową z określonym współczynnikiem skalowania. Jest użyteczny między innymi dla kwot. [Pierwsza wzmianka](../03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-scaled-float).

<a id="object"></a>
## Object

Domyślny typ pola zawierającego obiekt JSON. W tablicach obiektów może spłaszczać relacje między polami poszczególnych elementów. [Pierwsza wzmianka](../03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-object).

<a id="nested"></a>
## Nested

Typ pola dla tablic obiektów, który zachowuje relację między polami należącymi do tego samego elementu tablicy. [Pierwsza wzmianka](../03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-nested).

<a id="dynamic-mapping"></a>
## Dynamic mapping

Mechanizm automatycznego tworzenia mappingu na podstawie danych wprowadzonych do indeksu. [Pierwsza wzmianka](../03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-dynamic-mapping).

<a id="strict"></a>
## Strict

Ustawienie mappingu `dynamic: strict`, które odrzuca dokumenty zawierające pola nieobecne w jawnym mappingu. [Pierwsza wzmianka](../03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-strict).

<a id="reindex"></a>
## Reindex

Operacja kopiowania dokumentów do innego indeksu, zwykle w celu zastosowania nowego mappingu. [Pierwsza wzmianka](../03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-reindex).

<a id="alias"></a>
## Alias

Logiczna nazwa wskazująca na indeks. Alias pozwala zmienić fizyczną wersję indeksu bez zmiany nazwy używanej przez aplikację. [Pierwsza wzmianka](../03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-alias).

<a id="exists-query"></a>
## Exists query

Query sprawdzające, czy dokument ma indeksowaną wartość pod wskazaną nazwą pola. [Pierwsza wzmianka](../04%20Typy%20zapyta%C5%84.md#term-exists-query).

<a id="prefix-query"></a>
## Prefix query

Query dopasowujące wartości zaczynające się od podanego prefiksu, najczęściej na polu `keyword`. [Pierwsza wzmianka](../04%20Typy%20zapyta%C5%84.md#term-prefix-query).

<a id="normalizer"></a>
## Normalizer

Konfiguracja normalizująca wartości pól `keyword`, na przykład zmieniająca litery na małe przed dokładnym porównaniem. [Pierwsza wzmianka](../04%20Typy%20zapyta%C5%84.md#term-normalizer).

<a id="edge-ngram"></a>
## Edge n-gram

Fragment tokenu tworzony od jego początku, używany między innymi do autocomplete po prefiksie. [Pierwsza wzmianka](../08%20Autocomplete.md#term-edge-ngram).

<a id="search-as-you-type"></a>
## `search_as_you_type`

Typ pola Elasticsearch przygotowany do wyszukiwania tekstu wpisywanego stopniowo, z pomocniczymi polami dla prefiksów i n-gramów. [Pierwsza wzmianka](../08%20Autocomplete.md#term-search-as-you-type).

<a id="refresh"></a>
## Refresh

Operacja udostępniająca ostatnie zmiany strukturom wyszukiwania. Refresh wpływa na widoczność dokumentów w search, ale nie zmienia ich źródła. [Pierwsza wzmianka](../05%20Przep%C5%82yw%20danych.md#term-refresh).

<a id="indexing"></a>
## Indexing

Proces zapisywania dokumentu i przygotowywania jego pól w strukturach używanych do wyszukiwania. [Pierwsza wzmianka](../05%20Przep%C5%82yw%20danych.md#term-indexing).

<a id="search"></a>
## Search

Operacja wyszukiwania dokumentów pasujących do query. Zwraca między innymi hits i `_source`. [Pierwsza wzmianka](../05%20Przep%C5%82yw%20danych.md#term-search).

<a id="update"></a>
## Update

Operacja modyfikująca istniejący dokument, także tylko w wybranych polach. Elasticsearch przygotowuje następnie zaktualizowaną wersję dokumentu. [Pierwsza wzmianka](../05%20Przep%C5%82yw%20danych.md#term-update).

<a id="delete"></a>
## Delete

Operacja usuwająca dokument z indeksu po jego identyfikatorze. Usunięcie staje się widoczne w search po refreshu. [Pierwsza wzmianka](../05%20Przep%C5%82yw%20danych.md#term-delete).

<a id="bulk-api"></a>
## Bulk API

Endpoint przyjmujący wiele operacji indeksowania, aktualizacji lub usuwania w jednym żądaniu. Odpowiedź może zawierać częściowe błędy. [Pierwsza wzmianka](../06%20Praca%20produkcyjna.md#term-bulk-api).

<a id="rest-api"></a>
## REST API

Interfejs HTTP Elasticsearch udostępniający operacje na indeksach, dokumentach i wynikach wyszukiwania. [Pierwsza wzmianka](../07%20Integracja.md#term-rest-api).

<a id="elasticsearch-python-client"></a>
## Elasticsearch Python client

Biblioteka Pythona mapująca operacje Elasticsearch na metody klienta, w tym indeksowanie, search i zarządzanie indeksami. [Pierwsza wzmianka](../07%20Integracja.md#term-elasticsearch-python-client).

<a id="django-elasticsearch-dsl"></a>
## Django Elasticsearch DSL

Biblioteka opisująca dokumenty Elasticsearch na podstawie modeli Django i pomagająca w ich synchronizacji. [Pierwsza wzmianka](../07%20Integracja.md#term-django-elasticsearch-dsl).

<a id="data-projection"></a>
## Projekcja danych

Kopia danych przygotowana pod konkretny sposób odczytu, na przykład wyszukiwanie. Może być odbudowana ze źródła prawdy. [Pierwsza wzmianka](../09%20Pu%C5%82apki%20i%20decyzje.md#term-data-projection).

<a id="mapping-drift"></a>
## Mapping drift

Niekontrolowane rozjeżdżanie się struktury danych i mappingu, często powodowane dynamicznym dodawaniem pól. [Pierwsza wzmianka](../09%20Pu%C5%82apki%20i%20decyzje.md#term-mapping-drift).

<a id="shard-cost"></a>
## Shard cost

Koszt pamięci, plików i zarządzania wynikający z utrzymywania shardów. [Pierwsza wzmianka](../09%20Pu%C5%82apki%20i%20decyzje.md#term-shard-cost).

<a id="deep-pagination"></a>
## Deep pagination

Pobieranie odległych stron wyników, które wymaga od shardów utrzymywania dużej liczby kandydatów. [Pierwsza wzmianka](../09%20Pu%C5%82apki%20i%20decyzje.md#term-deep-pagination).

<a id="eventual-visibility"></a>
## Eventual visibility

Opóźniona widoczność zapisu lub usunięcia w search, wynikająca z modelu near real-time i cyklu refresh. [Pierwsza wzmianka](../09%20Pu%C5%82apki%20i%20decyzje.md#term-eventual-visibility).

<a id="idempotency"></a>
## Idempotency

Właściwość operacji, przy której wielokrotne wykonanie tej samej operacji prowadzi do tego samego stanu. [Pierwsza wzmianka](../09%20Pu%C5%82apki%20i%20decyzje.md#term-idempotency).

<a id="highlighting"></a>
## Highlighting

Funkcja search zwracająca fragmenty pól tekstowych z zaznaczonymi miejscami dopasowania do query.

<a id="aggregations"></a>
## Aggregations

Operacje podsumowujące i grupujące dokumenty, zwracane obok hits w odpowiedzi search.

<a id="routing"></a>
## Routing

Mechanizm wyboru shardu dla dokumentu lub zapytania na podstawie wartości routingu.

<a id="custom-routing"></a>
## Custom routing

Własna wartość używana do kierowania dokumentów, na przykład `tenant_id`, zamiast domyślnego `_id`.

<a id="hot-shard"></a>
## Hot shard

Shard przeciążony większą ilością danych lub ruchu niż pozostałe shardy, często przez nierówny routing.

<a id="token-filter"></a>
## Token filter

Element analyzera modyfikujący tokeny po tokenizacji, na przykład przez lowercase, usuwanie stop words albo stemming.

<a id="lowercase-filter"></a>
## Lowercase filter

Filtr zamieniający litery tokenów na małe, aby ograniczyć wpływ wielkości liter na dopasowanie.

<a id="stop-words"></a>
## Stop words

Słowa uznane za mało informacyjne i usuwane przez analyzer. Ich lista powinna odpowiadać językowi oraz domenie.

<a id="stemming"></a>
## Stemming

Proces sprowadzania odmian słów do wspólnej postaci, aby mogły być porównywane jako powiązane tokeny.

<a id="ngram"></a>
## N-gram

Nakładający się fragment tokenu o określonej długości, używany między innymi do wyszukiwania fragmentów tekstu i autocomplete.

<a id="cluster-health"></a>
## Cluster health

Stan klastra opisujący między innymi przydział primary i replica shardów; najczęściej ma status `green`, `yellow` albo `red`.

<a id="kibana"></a>
## Kibana

Narzędzie do pracy z Elasticsearch, eksplorowania danych i tworzenia wizualizacji oraz dashboardów.

<a id="synchronization"></a>
## Synchronization

Utrzymywanie zgodności modelu źródłowego, na przykład Django, z dokumentem Elasticsearch.

<a id="asynchronous-indexing"></a>
## Asynchronous indexing

Indeksowanie wykonywane poza żądaniem webowym, zwykle przez worker lub kolejkę, aby zmniejszyć opóźnienie odpowiedzi.

<a id="rebuild"></a>
## Rebuild

Odbudowanie indeksu od podstaw na podstawie źródła prawdy, zwykle po zmianie mappingu, analyzera albo struktury dokumentu.
