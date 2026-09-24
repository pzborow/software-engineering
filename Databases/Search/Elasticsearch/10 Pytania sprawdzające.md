# Pytania sprawdzające

## 1. Czym Elasticsearch różni się od klasycznej relacyjnej bazy danych?

<details>
<summary>Odpowiedź</summary>

Elasticsearch jest silnikiem wyszukiwania i analizy danych, a nie główną relacyjną bazą transakcyjną. Przechowuje dokumenty JSON w indeksach i przygotowuje je pod szybkie wyszukiwanie, filtrowanie, sortowanie oraz agregacje. Najczęściej działa jako projekcja danych z systemu źródłowego, na przykład z bazy aplikacyjnej.

Linki: [01 Czym jest Elasticsearch](01%20Czym%20jest%20Elasticsearch.md#term-document), [09 Pułapki i decyzje](09%20Pu%C5%82apki%20i%20decyzje.md#term-data-projection).

</details>

## 2. Co oznacza, że Elasticsearch przechowuje dokumenty?

<details>
<summary>Odpowiedź</summary>

Dokument to pojedynczy obiekt JSON opisujący jeden byt, na przykład produkt, zamówienie albo wpis. Dokument składa się z pól, które mogą mieć różne typy i różny sposób indeksowania. Dokumenty są zapisywane w indeksie.

Linki: [01 Czym jest Elasticsearch](01%20Czym%20jest%20Elasticsearch.md#term-document), [03 Jak Elasticsearch rozumie dane](03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-mapping).

</details>

## 3. Po co jest mapping?

<details>
<summary>Odpowiedź</summary>

Mapping mówi Elasticsearchowi, jak interpretować pola dokumentu: czy pole jest tekstem do wyszukiwania pełnotekstowego, dokładną wartością do filtrowania, liczbą, datą albo strukturą zagnieżdżoną. Od mappingu zależy, jakie query, sortowanie i agregacje będą działały poprawnie.

Linki: [03 Jak Elasticsearch rozumie dane](03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-mapping), [03 Typ pola wynika z pytania](03%20Jak%20Elasticsearch%20rozumie%20dane.md#typ-pola-wynika-z-pytania).

</details>

## 4. Kiedy użyć `text`, a kiedy `keyword`?

<details>
<summary>Odpowiedź</summary>

`text` służy do wyszukiwania po treści, gdzie tekst jest analizowany i dzielony na tokeny. `keyword` służy do dokładnych wartości: filtrów, sortowania, agregacji i identyfikatorów. Tytuł produktu często jest `text`, a status, kategoria albo kod produktu często są `keyword`.

Linki: [03 Typ pola wynika z pytania](03%20Jak%20Elasticsearch%20rozumie%20dane.md#typ-pola-wynika-z-pytania), [03 `text` i `keyword`](03%20Jak%20Elasticsearch%20rozumie%20dane.md#text-i-keyword).

</details>

## 5. Co robi analyzer?

<details>
<summary>Odpowiedź</summary>

Analyzer przygotowuje tekst do indeksowania i wyszukiwania. Zwykle dzieli tekst na tokeny, normalizuje je i może usuwać albo przekształcać wybrane elementy. Ten sam lub kompatybilny proces powinien być użyty przy indeksowaniu i przy zapytaniu.

Linki: [02 Jak działa wyszukiwanie](02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#term-analyzer), [02 Analiza tekstu](02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#analiza-tekstu).

</details>

## 6. Dlaczego `match` i `term` to nie to samo?

<details>
<summary>Odpowiedź</summary>

`match` jest przeznaczony głównie do pól analizowanych, takich jak `text`; zapytanie przechodzi przez analyzer. `term` porównuje dokładną wartość i zwykle pasuje do pól `keyword`, liczb, dat albo wartości logicznych. Użycie `term` na polu `text` często daje zaskakujące wyniki.

Linki: [02 Wyszukiwanie analizowane](02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#term-match-query), [02 Dokładne dopasowanie wartości](02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#dokładne-dopasowanie-wartości), [04 Typy zapytań](04%20Typy%20zapyta%C5%84.md#wyszukiwanie-analizowanego-tekstu).

</details>

## 7. Do czego służy bool query?

<details>
<summary>Odpowiedź</summary>

Bool query łączy warunki `must`, `should`, `filter` i `must_not`. Pozwala zbudować zapytanie z wielu części, na przykład wyszukiwanie tekstowe w `must` oraz ograniczenie kategorii w `filter`. `filter` zwykle nie wpływa na `_score`.

Linki: [02 Łączenie warunków przez `bool`](02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#term-bool-query), [04 Łączenie warunków](04%20Typy%20zapyta%C5%84.md#łączenie-warunków).

</details>

## 8. Czym jest `_score`?

<details>
<summary>Odpowiedź</summary>

`_score` to ocena dopasowania dokumentu do zapytania. Nie jest oceną jakości dokumentu ani wartością biznesową. Zależy od query, analizowanego tekstu, częstości termów i konfiguracji rankingu.

Linki: [02 Score nie jest oceną biznesową](02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#score-nie-jest-oceną-biznesową), [02 Przepływ zapytania](02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#przepływ-zapytania).

</details>

## 9. Co oznacza near real-time?

<details>
<summary>Odpowiedź</summary>

Near real-time oznacza, że zapisany albo usunięty dokument nie musi być widoczny w wyszukiwaniu natychmiast. Staje się widoczny po odświeżeniu indeksu, czyli po refreshu. To ważne przy testach i przy workflow, które oczekują natychmiastowych wyników po zapisie.

Linki: [05 Przepływ danych](05%20Przep%C5%82yw%20danych.md#term-refresh), [09 Pułapki i decyzje](09%20Pu%C5%82apki%20i%20decyzje.md#term-eventual-visibility).

</details>

## 10. Po co są shardy i repliki?

<details>
<summary>Odpowiedź</summary>

Shard dzieli indeks na części, aby rozłożyć dane i pracę. Replica shard jest kopią primary shardu, zwiększa odporność na awarię i może obsługiwać odczyty. Replika nie jest jednak backupem; do odtwarzania po błędach służą snapshoty.

Linki: [01 Architektura klastra](01%20Czym%20jest%20Elasticsearch.md#architektura-klastra), [06 Shardy i repliki](06%20Praca%20produkcyjna.md#shardy-i-repliki), [06 Snapshot](06%20Praca%20produkcyjna.md#snapshot).

</details>

## 11. Kiedy potrzebny jest reindex?

<details>
<summary>Odpowiedź</summary>

Reindex jest potrzebny, gdy trzeba zmienić sposób indeksowania danych, na przykład mapping pola z `text` na `keyword`, dodać inny analyzer albo przebudować projekcję. Wiele zmian mappingu nie działa wstecz na już zaindeksowane dokumenty, więc trzeba utworzyć nowy indeks i skopiować dane.

Linki: [06 Reindex](06%20Praca%20produkcyjna.md#reindex), [06 Alias i zmiana wersji indeksu](06%20Praca%20produkcyjna.md#alias-i-zmiana-wersji-indeksu).

</details>

## 12. Dlaczego Elasticsearch często jest projekcją, a nie źródłem prawdy?

<details>
<summary>Odpowiedź</summary>

Elasticsearch jest zoptymalizowany pod odczyt, wyszukiwanie i agregacje. Dane biznesowe zwykle mają swoje źródło prawdy w systemie transakcyjnym, na przykład w relacyjnej bazie danych. Elasticsearch przechowuje wersję przygotowaną pod konkretne zapytania i można ją odbudować ze źródła.

Linki: [09 Pułapki i decyzje](09%20Pu%C5%82apki%20i%20decyzje.md#term-data-projection), [07 Integracja](07%20Integracja.md#term-django-elasticsearch-dsl).

</details>

## 13. Co jest ryzykowne w deep pagination?

<details>
<summary>Odpowiedź</summary>

Deep pagination wymaga od Elasticsearcha policzenia i utrzymania wielu kandydatów, nawet jeśli użytkownik chce zobaczyć dopiero odległą stronę wyników. Im głębsza strona, tym większy koszt pamięci i pracy shardów. Do głębokiego przeglądania lepiej używać mechanizmów takich jak `search_after`.

Linki: [09 Deep pagination](09%20Pu%C5%82apki%20i%20decyzje.md#term-deep-pagination), [04 Wybór query](04%20Typy%20zapyta%C5%84.md#wybór-query).

</details>

## 14. Kiedy autocomplete powinien mieć osobne pole albo multi-field?

<details>
<summary>Odpowiedź</summary>

Autocomplete zwykle wymaga innego sposobu indeksowania niż normalne wyszukiwanie, na przykład n-gramów albo `search_as_you_type`. Warto użyć osobnego pola lub multi-field, żeby nie pogorszyć zwykłego wyszukiwania i nie mieszać różnych celów w jednym mappingu.

Linki: [08 Autocomplete](08%20Autocomplete.md#term-edge-ngram), [08 `search_as_you_type`](08%20Autocomplete.md#term-search-as-you-type), [03 Multi-field](03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-multi-field).

</details>

## 15. Co sprawdzić, gdy wyniki wyszukiwania są zaskakujące?

<details>
<summary>Odpowiedź</summary>

Najpierw sprawdź mapping pola, analyzer, typ query oraz przykładowe tokeny. Potem sprawdź, czy pytasz właściwy indeks lub alias, czy dokumenty są widoczne po refreshu i czy filtry nie odrzucają wyników. W problemach rankingowych sprawdź także `_score` i strukturę bool query.

Linki: [02 Gdy wynik jest pusty](02%20Jak%20dzia%C5%82a%20wyszukiwanie.md#gdy-wynik-jest-pusty), [03 Jak Elasticsearch rozumie dane](03%20Jak%20Elasticsearch%20rozumie%20dane.md#term-mapping), [09 Mapping drift](09%20Pu%C5%82apki%20i%20decyzje.md#term-mapping-drift).

</details>
