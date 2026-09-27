# Pułapki

Nieoczywiste zachowania kodu z przykładów, które prowadzą do błędów w produkcji albo w testach. Łowca pułapek sprawdza tylko sekcje z kodem i nie wypisuje niczego na siłę.

Sekcje z kodem: 43 · sprawdzone: 43 · pułapki tematu: 19 · poboczne: 2

## Pułapki tematu

Ilustrują zagadnienia, których dotyczy tutorial. Te same uwagi są w ramkach pod sekcjami.

### 01. Serwer Fuseki i pytania Biura

- **Graph Store Protocol (POST vs PUT na grafie):** **POST na /data dokłada dane zamiast zastępować graf.** `POST` na `/biuro/data` dopisuje trójki do grafu domyślnego. Ponowne wgranie tego samego `plik.ttl` nie zdubluje identycznych trójek, ale zmienione lub usunięte w pliku trójki zostaną w grafie. Do podmiany całego grafu służy `PUT`, który usuwa jego dotychczasową zawartość, więc trzeba go użyć świadomie.
  Dotyczy: `curl -X POST "http://localhost:3030/biuro/data" -H "Content-Type: text/turtle" --data-binary @plik.ttl` · [sekcja „Dataset biuro w przeglądarce”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce)

- **prefiksy i IRI w Turtle:** **Prefiks @prefix nie łączy się z IRI automatycznie.** Prefiks to zwykłe doklejenie tekstu: `bpc:` kończy się na `#`, a `ex:` na `/`. Literówka albo brak końcowego separatora w `@prefix` daje inne IRI (np. `bpcodwiedzil`), więc dane po wczytaniu nie pasują do zapytań, a serwer nie zgłasza błędu. Trzeba pilnować identycznych deklaracji prefiksów w danych i zapytaniach.
  Dotyczy: `@prefix bpc: <http://example.org/bpc#> .` · [sekcja „Trójka, wiersz i prefiksy”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy)

### 02. Podstawy RDF, RDFS i słowników

- **literał z typem danych (xsd:date):** **Niepoprawna data w xsd:date nie jest odrzucana.** Literał `"2024-02-30"^^xsd:date` jest przyjmowany przez Fuseki jako ill-typed: zapis się udaje, a błąd wychodzi dopiero w filtrach (porównanie daje błąd/brak wyniku). Tekst sekcji sugeruje, że typ chroni dane; trzeba walidować np. SHACL-em albo przed wczytaniem.
  Dotyczy: `bpc:od "2024-05-05"^^xsd:date` · [sekcja „Literały: typ i język”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język)

- **graf nazwany a graf domyślny w datasecie:** **Zapytanie bez FROM widzi tylko graf domyślny.** Dane z `ex:linia_a` i `ex:linia_b` leżą w grafach nazwanych, więc zapytanie SELECT bez `GRAPH`/`FROM` na dataset Fuseki zwróci pusty wynik (domyślnie graf domyślny nie jest sumą grafów nazwanych). Trzeba użyć `GRAPH ?g { ... }` albo włączyć `tdb:unionDefaultGraph`.
  Dotyczy: `ex:linia_a { ex:p1 bpc:odwiedzil ex:w1 . ... }` · [sekcja „Dataset i grafy nazwane w TriG”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#dataset-i-grafy-nazwane-w-trig)

- **TriG i ładowanie datasetu:** **Wgranie TriG do /biuro bez grafu ogranicza dane.** Format TriG niesie nazwy grafów tylko przy wgraniu do endpointu datasetu (`/biuro`); wysłanie go do endpointu grafu (`/biuro/data?graph=...`) albo jako Turtle gubi lub spłaszcza podział na grafy. Trzeba użyć poprawnego Content-Type `application/trig`.
  Dotyczy: `` wgranie TriG do `/biuro` `` · [sekcja „Dataset i grafy nazwane w TriG”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#dataset-i-grafy-nazwane-w-trig)

- **IRI zasobu a IRI grafu nazwanego:** **Ten sam zasób w wielu grafach nazwanych.** IRI `ex:w1` jest globalne, więc może wystąpić w trójkach kilku grafów (np. `ex:linia_a` i `ex:linia_b`). Opisy wizyty rozproszą się po grafach, a zapytanie o `ex:w1` w jednym `GRAPH` zobaczy tylko część faktów. Trzeba pilnować, by trójki o zasobie trafiały do jednego grafu, albo pytać przez `GRAPH ?g`.
  Dotyczy: `ex:linia_a { ex:p1 bpc:odwiedzil ex:w1 . }` · [sekcja „IRI grafu a IRI wizyty”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#iri-grafu-a-iri-wizyty)

- **owl:sameAs i wnioskowanie:** **Fuseki domyślnie nie stosuje owl:sameAs.** Sam trójkąt `owl:sameAs` nie zlewa faktów, dopóki dataset nie ma modelu wnioskującego (np. reguł OWL w konfiguracji Fuseki). Bez niego zapytania SPARQL widzą wizyty osobno przy każdym IRI, więc test na czystym TDB przejdzie, a po włączeniu wnioskowania na produkcji dane się zleją. Trzeba sprawdzić konfigurację datasetu.
  Dotyczy: `ex:p1 owl:sameAs ex:p1_edo` · [sekcja „Słownik bpc a IRI instancji”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#słownik-bpc-a-iri-instancji)

- **time:Interval z instantami jako węzłami pustymi:** **Węzły puste w przedziale mnożą się przy ponownym wgraniu.** Dla `time:hasBeginning [ ... ]` i `time:hasEnd [ ... ]` każde wgranie pliku tworzy nowe węzły puste. Powtórny POST nie jest więc idempotentny: `ex:w1_czas` dostaje kolejne początki i końce, a zapytanie zwraca zdublowane lub sprzeczne granice. Nadaj instantom stałe IRI (np. `ex:w1_start`) albo przed wgraniem zastąp graf.
  Dotyczy: `time:hasBeginning [ time:inXSDDate "2024-05-05"^^xsd:date ]` · [sekcja „Przedział czasu czy zwykła data”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#przedział-czasu-czy-zwykła-data)

- **typy literałów xsd:date:** **Data z xsd:date bez ostrzeżenia zmienia sens dla lat starożytnych.** Literał `"0027-01-01"^^xsd:date` jest poprawny w XSD 1.0, ale w XSD 1.1 rok 0000 istnieje, a przed naszą erą wymaga znaku minus. Fuseki/Jena nie ostrzeże, więc granice epoki `ex:epoka_rzym` mogą być porównywane inaczej w różnych narzędziach. Dla epok trzeba jawnie ustalić konwencję lat.
  Dotyczy: `time:inXSDDate "0027-01-01"^^xsd:date` · [sekcja „Kryterium wyboru terminów”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kryterium-wyboru-terminów)

### 03. Model danych Biura

- **klucz obcy jako połączenie IRI:** **Brak referencji: IRI bez węzła docelowego.** Trójka `ex:w1 bpc:epoka ex:epoka_rzym` powstaje z samej komórki, a RDF nie ma kluczy obcych. Literówka w kolumnie `epoka` (np. `rzm`) daje poprawną trójkę wskazującą na zasób bez żadnych własności. Fuseki tego nie zgłosi, a zapytania po cichu gubią wiersz. Trzeba to wyłapać osobnym zapytaniem kontrolnym albo walidacją (SHACL).
  Dotyczy: `iri_for(row['epoka'], 'epoka')` · [sekcja „Klucze jako IRI i połączenia”](03%20Model%20danych%20Biura.md#klucze-jako-iri-i-połączenia)

- **typowane literały RDF (xsd:date):** **Literał bez jawnego typu to xsd:string.** Szablon `{od}` jest tylko tekstem; jeśli generator zapisze go jako zwykły literał (`"2020-01-01"`) bez `^^xsd:date`, w RDF to `xsd:string`. Porównania i `FILTER` po dacie nie zadziałają jak na datach, a literały o różnych typach nie są sobie równe. Typ z kolumny „typ RDF” musi trafić do serializacji.
  Dotyczy: `"od": ("ex:{id}", "bpc:od", "{od}", "xsd:date", "bpc", "analizy porównują daty")` · [sekcja „Wiersz mapowania kolumn wizyty”](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty)

### 04. Konwersja CSV do TriG

- **graf nazwany a opis pochodzenia PROV-O:** **IRI grafu jako encja PROV nie jest z nim powiązane.** `ex:linia_a` jest nazwą grafu z danymi i jednocześnie podmiotem opisu `prov:Entity` w `ex:provenance`. Fuseki nie łączy tych ról: opis to zwykłe trójki o IRI. Zastąpienie albo usunięcie grafu `ex:linia_a` nie zmieni `prov:wasGeneratedBy` ani `prov:wasDerivedFrom`, więc pochodzenie może opisywać dane, których już nie ma. Zapytanie o pochodzenie nie sięgnie też do zawartości grafu bez osobnego `GRAPH ex:linia_a`.
  Dotyczy: `ex:linia_a a prov:Entity ; prov:wasGeneratedBy ex:konwersja_wizyty ;` · [sekcja „Konwersja CSV w PROV-O”](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o)

- **provenance PROV-O ze stałym IRI zamiast węzła pustego:** **Stały IRI aktywności łączy różne konwersje.** Deterministyczny IRI aktywności jest ten sam w każdym przebiegu. Po wgraniu wyników dwóch konwersji z różnym `started` (POST dokłada) aktywność dostanie dwa `prov:startedAtTime` i dwa `prov:endedAtTime`, a wpisy prowokujące się mieszają. Uwzględnij `started` w IRI aktywności albo zastępuj graf `ex:provenance` przy wgraniu.
  Dotyczy: `` aktywność ma stały IRI `ex:konwersja_wizyty` `` · [sekcja „Od CSV do zwalidowanego TriG”](04%20Konwersja%20CSV%20do%20TriG.md#od-csv-do-zwalidowanego-trig)

### 05. SPARQL SELECT i wzorce trójek

- **Wzorzec trójek jako złączenie:** **Wzorzec trójek gubi wiersze z brakującą właściwością.** Wizyta bez `bpc:do` znika z wyniku bez żadnego ostrzeżenia, więc wizyta trwająca lub z niekompletnymi danymi wygląda, jakby nie istniała. Jeśli takie wiersze mają zostać, trzeba objąć `bpc:do` w `OPTIONAL`.
  Dotyczy: `?wizyta bpc:od ?od ; bpc:do ?do .` · [sekcja „Wizyty podróżnika w SELECT”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#wizyty-podróżnika-w-select)

- **Widok sumy grafów nazwanych:** **Union graph zwielokrotnia wiersze przy duplikatach.** Ta sama trójka zapisana w kilku grafach nazwanych w widoku `urn:x-arq:UnionGraph` jest zwracana jako jedno podstawienie, ale `SELECT` bez `DISTINCT` nie pokazuje, z którego grafu pochodzi. Przy różnych trójkach o tej samej wizycie wynik miesza dane z różnych linii bez śladu źródła.
  Dotyczy: `FROM <urn:x-arq:UnionGraph>` · [sekcja „Wizyty podróżnika w SELECT”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#wizyty-podróżnika-w-select)

- **FROM NAMED i dataset opisany w zapytaniu:** **FROM NAMED razem z FROM wyłącza graf domyślny.** Fuseki po wskazaniu w zapytaniu `FROM NAMED` buduje własny dataset z klauzul. Jeśli zapytanie nie ma `FROM`, graf domyślny jest wtedy pusty, więc wzorce poza `GRAPH` nic nie zwrócą, mimo że dane leżą w grafie domyślnym magazynu. Trzeba dodać `FROM` albo umieścić cały wzorzec w `GRAPH`.
  Dotyczy: `SELECT ?g ?w FROM NAMED ex:linia_a WHERE {` · [sekcja „Zapytania w wybranym grafie”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zapytania-w-wybranym-grafie)

### 06. Analizy paradoksów w SPARQL

- **Wykrywanie braków i osieroconych zasobów w RDF (open-world, FILTER NOT EXISTS):** **Wizyta bez typu wygląda jak błąd danych.** Gałąź „błąd danych” sprawdza `FILTER NOT EXISTS { ?w a bpc:Wizyta }`, więc wizyta opisana, ale bez `a bpc:Wizyta` (literówka w typie, inny prefiks), też zostanie oznaczona jako błąd danych. Skutek: fałszywe alarmy o „literówce w kluczu obcym”, choć błąd jest w typie. Sprawdzaj obie możliwości (brak jakichkolwiek trójek o `?w` vs brak typu).
  Dotyczy: `FILTER NOT EXISTS { ?w a bpc:Wizyta }` · [sekcja „Spotkanie bez wizyty i wizyta bez powiązania”](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#spotkanie-bez-wizyty-i-wizyta-bez-powiązania)

- **Semantyka porównań literałów w SPARQL (błąd typu w FILTER):** **FILTER != na różnych typach daje błąd, nie true.** Jeśli `?rod` jest `xsd:string` albo `xsd:dateTime`, a `?od` to `xsd:date`, `!=` zgłasza błąd typu, a nie „różne”. Gdy druga strona `||` nie jest true, cały `FILTER` odrzuca wiersz, więc największe rozbieżności znikają po cichu. Porównuj po ujednoliceniu typów, np. `STR(?rod) != STR(?od)` albo `xsd:date(...)`, lub osobno wyłap pary o różnych `DATATYPE`.
  Dotyczy: `FILTER (?rod != ?od || ?rdo != ?do)` · [sekcja „Raport sprzeczny z danymi wizyty”](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#raport-sprzeczny-z-danymi-wizyty)

- **Suma grafów (urn:x-arq:UnionGraph):** **UnionGraph to tylko grafy nazwane, tylko w TDB.** W Jena TDB/TDB2 `urn:x-arq:UnionGraph` łączy wyłącznie grafy nazwane; graf domyślny nie wchodzi do sumy, wbrew opisowi. Na zbiorze w pamięci `FROM` z tą nazwą jest traktowane jak zwykły URI do wczytania i nie daje sumy. Dane z grafu domyślnego trzeba dodać jawnie albo użyć `tdb:unionDefaultGraph`.
  Dotyczy: `FROM <urn:x-arq:UnionGraph>` · [sekcja „Grafy nazwane czy jeden graf”](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#grafy-nazwane-czy-jeden-graf)

## Pułapki poboczne (Python i narzędzia przykładów)

Wynikają z narzędzi użytych do pokazania przykładów, a nie z tematu. Nie ma ich w tekście, żeby nie rozpraszały czytania.

### 03. Model danych Biura

- **Tożsamość zasobu jako IRI / mintowanie stabilnych IRI:** **Prefiks kind_ koliduje z kluczem zawierającym podkreślnik.** `quote` z `safe=""` zostawia `_` bez zmian, więc `iri_for("epoka_rzym")` i `iri_for("rzym", "epoka")` dają ten sam adres `.../epoka_rzym`. W RDF IRI to tożsamość, więc dwa różne zasoby po cichu zleją się w jeden węzeł ze wspólnymi trójkami. Unikaj tego, używając separatora, który `quote` koduje (np. `/` lub `#` w ścieżce), albo osobnych przestrzeni nazw dla każdego `kind`.
  Dotyczy: `f"{kind}_{local}" if kind else local` · [sekcja „Znaki specjalne w kluczach IRI”](03%20Model%20danych%20Biura.md#znaki-specjalne-w-kluczach-iri)

### 07. Graf wiedzy Biura Paradoksów Czasowych

- **application/sparql-results+json:** **Spłaszczenie wiersza gubi typ i datatype.** `{k: v["value"] ...}` odrzuca `type`, `datatype` i `xml:lang`. IRI, literał, węzeł pusty (`bnode`, wartość w rodzaju `b0`) i `"1"` kontra `"1"^^xsd:integer` dają ten sam napis. Węzła pustego nie da się też użyć w kolejnym zapytaniu. Zachowaj cały słownik albo `type` i `datatype` tam, gdzie mają znaczenie, np. dla dat.
  Dotyczy: `{k: v["value"] for k, v in row.items()}` · [sekcja „Zapytanie SPARQL przez HTTP”](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#zapytanie-sparql-przez-http)
