# Pułapki i decyzje

Elasticsearch daje dużą elastyczność, ale każda decyzja wpływa na koszt zapisu, wyszukiwania i utrzymania. Najbezpieczniej traktować go jako zaprojektowany silnik wyszukiwania, a nie jako bezrefleksyjny zamiennik całej bazy aplikacji.

## Elasticsearch jako projekcja

<a id="term-data-projection"></a>[Projekcja danych](00%20Glossary%20Elasticsearch.md#data-projection) to kopia danych przygotowana pod konkretny odczyt. W typowej architekturze relacyjna baza pozostaje source of truth, a Elasticsearch przechowuje projekcję zoptymalizowaną pod wyszukiwanie.

Taki podział pozwala odbudować indeks, gdy dane zostaną usunięte albo mapping okaże się błędny. Wymaga jednak procesu synchronizacji, obsługi opóźnień i decyzji, co aplikacja robi, gdy baza i indeks chwilowo pokazują różne stany.

## Niekontrolowane zmiany mappingu

<a id="term-mapping-drift"></a>[Mapping drift](00%20Glossary%20Elasticsearch.md#mapping-drift) oznacza niekontrolowane rozjeżdżanie się struktury danych i mappingu. Dynamiczne dodawanie pól może być wygodne, ale literówka albo nieprzemyślany typ utrwala się w indeksie.

Zmiana typu istniejącego pola zwykle wymaga nowego indeksu i reindex. Dlatego ważne indeksy powinny mieć jawny mapping, kontrolę zmian i testy zapytań wykonywane przed wdrożeniem.

## Koszt shardów

Każdy shard ma narzut pamięci, plików i zarządzania. <a id="term-shard-cost"></a>[Shard cost](00%20Glossary%20Elasticsearch.md#shard-cost) rośnie, gdy indeksów lub shardów jest zbyt wiele w stosunku do ilości danych.

Więcej shardów nie oznacza automatycznie większej wydajności. Zbyt małe shardy zwiększają narzut, a zbyt duże mogą utrudnić równoległość i odtwarzanie. Liczbę shardów dobierz na podstawie pomiarów, przewidywanego rozmiaru i wzrostu danych.

## Odległe strony wyników

<a id="term-deep-pagination"></a>[Deep pagination](00%20Glossary%20Elasticsearch.md#deep-pagination) oznacza pobieranie odległej strony wyników przez wysokie `from`. Każdy shard musi zebrać i utrzymać więcej kandydatów, zanim koordynator wybierze właściwy fragment.

Dla głębokiej paginacji użyj `search_after` ze stabilnym sortowaniem albo mechanizmu scroll przeznaczonego do przetwarzania dużych zbiorów. Zwykłe strony numerowane są wygodne dla małych zakresów, ale nie skalują się bez końca.

```http
GET products/_search
Content-Type: application/json

{
  "size": 20,
  "query": { "match_all": {} },
  "sort": [
    { "created_at": "desc" },
    { "_id": "asc" }
  ],
  "search_after": ["2026-09-21T10:00:00Z", "book-42"]
}
```

## Widoczność po odświeżeniu

<a id="term-eventual-visibility"></a>[Eventual visibility](00%20Glossary%20Elasticsearch.md#eventual-visibility) oznacza, że zapis lub usunięcie może nie być widoczne w search natychmiast. To konsekwencja near real-time i refreshu, niekoniecznie błąd utraty danych.

Jeżeli workflow wymaga odczytu zaraz po zapisie, użyj `refresh=wait_for` tylko tam, gdzie koszt i opóźnienie są akceptowalne. Nie rozwiązuj każdego problemu widoczności przez wymuszanie refresh po każdej operacji.

## Bulk i idempotencja

Bulk przyspiesza import, ale retry może ponowić część operacji. <a id="term-idempotency"></a>[Idempotency](00%20Glossary%20Elasticsearch.md#idempotency) oznacza, że powtórzenie tej samej operacji prowadzi do tego samego stanu.

Jawne ID i rozdzielenie operacji indeksowania od generowania danych pomagają bezpiecznie ponawiać import. Każdą odpowiedź bulk trzeba sprawdzić osobno, ponieważ sukces żądania nie oznacza sukcesu każdej operacji.

## Kiedy wybrać inne rozwiązanie

Elasticsearch pasuje do wyszukiwania tekstowego, rankingu i analityki po indeksowanych danych. Nie jest automatycznie najlepszym miejscem dla silnych transakcji, relacji referencyjnych ani jedynej kopii stanu biznesowego.

Decyzję podejmij na podstawie wymagań: opóźnienia, dokładności, kosztu, spójności, sposobu odtworzenia i kompetencji zespołu. Sam fakt, że można zindeksować dane w Elasticsearch, nie oznacza jeszcze, że należy to zrobić.

## Co zapamiętać

- Elasticsearch często jest projekcją danych, a nie source of truth.
- Mapping drift utrudnia zapytania i może wymusić reindex.
- Nadmiar shardów zwiększa koszt utrzymania.
- Deep pagination wymaga `search_after` albo scroll.
- Near real-time oznacza eventual visibility po refreshu.
- Bulk wymaga idempotencji i analizy częściowych błędów.
- Wybór Elasticsearch powinien wynikać z wymagań, nie z samej dostępności technologii.
