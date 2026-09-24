# Elasticsearch

## Ogólnie

Silnik wyszukiwarki, oparty o pełno tekstowe wyszykiwanie. Jest to baza NoSQL która przechowuje JSONy.

## Wyszukiwanie pełnotekstowe

Z ang. full-text search. Umożliwia sprawne przeszukanie zbioru dokumentów w oparciu o zadane przez użytkownika kryteria z uwzględnianiem literówek, odmian wyrazów, synonimów i zwracanie ich według oceny.

## Instalalcja

https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html
`docker pull docker.elastic.co/elasticsearch/elasticsearch:8.10.4`

```.bash
docker run --name es01 -p 9200:9200 -it -e "ES_JAVA_OPTS=-Xms2g -Xmx2g" -e "bootstrap.memory_lock=true" -e "discovery.type=single-node" -e "xpack.security.enabled=false" -e "xpack.security.enrollment.enabled=false" docker.elastic.co/elasticsearch/elasticsearch:8.10.4
```

W przypadku błędu `sudo sysctl -w vm.max_map_count=262144` [To pomogło](https://stackoverflow.com/questions/56937171/efk-elasticsearch-1-exited-with-code-78-when-install-elasticsearch)
[Wyłączenie uwieżytelniania](https://discuss.elastic.co/t/using-elasticserach-8-via-docker-without-certificate/303617)

Sprawdzenie `curl -XGET http://localhost:9200`

## Początki

Dane są w zwykłym JSON.
Zapis danych `curl -XPUT localhost:9200/party/party/1?pretty -d '{}'`

Odczyt j.w. ale GET zamiast PUT 

Kolejny PUT powoduje podbicie wersji i zapisanie nowych danych pod nową wersję

Można usunąć dokumnt o danym ID albo cały typ dokumentów, można usunąć cały index (party/party/1, party/party, /party)

## Definicje

**Index** Jest zbiór dokumentów danych, które są podobne. Są one przechowywane w Shards. 
**Shard** Jest to pudełko na dane. Kaźdy z nich jest przeszukiwany niezależnie i każdy z nich może mieć replikę. Elastic wysyła do każdego z nich zapytanie, wyniki są scalane. Pozwalają na horyzontalne skalowanie.
**Replika** Jest to kopia shardów. Nie powinny być porzechowywane na tym samym nodzie. Można z nich czytać, nigdy nie zapisujemy
**Typ** Służy do przechowywanie różnych ale podobnych danych w ramach indeksu. Jest deprecated
**Nody** Instancje elastica w clastrze

## Narzędzia

Kibana - Służy do wizualizacji danych
DevTools - Służy do pisania zapytań

## Jak szukać

Curl z GET na `party/party/_search`  po indeksie party po typie party albo na `party/_sarch` aby szukać po całym indeksie. Na końcu można szukać pośród wszystkich indeksów `p*/_search`

`_score` mówi jak bardzo dane pasują do zapytania.

Przykład zapytania `../_search?q=name:Kowalski` (`URI Searc`)
Przy większych zapytania Elastic zachęca do  `Request Body Search` czyli `get` na `{"query": {"match: {"name": "Kowalski"}}}`

## Analiza
Składa się ona z tokenizacji i normalizacji. Standardowy na początku tokenizuje, tworzy termy, lowercase, usuwa stopwordsy

## Schema
Mapowanie, jakie dane, jakie typy danych znadują się w dokumencie. Uzyskanie `_mapping`. Jak wrzucamy dane, on sobie sam próbuje ogarnąć mapowania. Przykłady: `text`, `long`, `keyword`, `date`, `ip`, `goo_point`.
Szukanie fulltext, po typie `string - analized`, `text`
Szukanie dokładne `keyword`, `string - not analized`
Możemy dodać mapowanie, ale nie możemy zmienić istniejących.

## Autocomplete
N-gram - okienko na słówko, tekst. N-gram długości jeden poszatkuje po literach, a długości dwa, po dwóch literach itd.
Przykład "Jan Kowalski" -> 1-gram j,a,n,k,o,w,a,l,s,k,i, 2-gram ja,an,nk ....
Aby włączyć trzeba zdefiniować filtr, typu `nGram`, następnie dwa analizatory
`search_analyzer` type keyword z `lowercase` i `autocomplete_analyzer` z filtrami `lowercase` i `nGramFilter`
Na końcu w opisie pola `name` tworzymy podpole np.: `autocomplete`, gdzie `analyzer` korzysta z `autocomplete_analyzer` i wskasuje na  to w jaki sposób analizowane w czasie indeksowania. `search_analyzer` kożysta z `search_analizer` i wskazuje w jaki sposób dane o które pytamy mają być analizowane.

## Polskie litery
Użyli dodatkowej biblioteki `iq analyzer`

## Synchronizacja z Django

Biblioteka `django_elasticsearch_dsl`

[Django Elasticsearch DSL](https://django-elasticsearch-dsl.readthedocs.io/en/latest/quickstart.html#declare-data-to-index)

## Zasoby internetowe
[prezentacja dla początkujących](https://www.youtube.com/watch?v=1Nt2lZFbkbg)
[Tu w formie pisanej](https://programistanaswoim.pl/uczymy-sie-elasticsearch-007-przygotowanie-tekstu-do-optymalnego-wyszukiwania/)
[Ty więcej o autocomplete](https://it.esky.pl/elasticsearch/serwis-autocomplete-z-uzyciem-elasticsearch-krok-po-kroku-czesc-33/)