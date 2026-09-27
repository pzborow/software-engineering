# Ściągawka: Jena Fuseki i grafy RDF w praktyce

Najważniejsze rzeczy z tutorialu na jednej stronie. Każda pozycja prowadzi do sekcji, która ją wyjaśnia.

## 01. Serwer Fuseki i pytania Biura

**Uruchomić Fuseki i sprawdzić ping**: Wymaga Javy 17; 200 z /$/ping i log ze startem potwierdzają działanie serwera. → [Start Fuseki na Javie 17](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#start-fuseki-na-javie-17)

```bash
./fuseki-server
# ... w logu: Started ... on port 3030
curl -i http://localhost:3030/$/ping
```

**Zapytanie i wgranie danych przez curl**: Dataset biuro wystawia endpointy query, update i data; wgranie idzie POST-em na /data z odpowiednim Content-Type. → [Dataset biuro w przeglądarce](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce)

```bash
curl -X POST http://localhost:3030/biuro/query \
  -H "Content-Type: application/sparql-query" \
  -d "ASK { ?s ?p ?o }"
```

## 02. Podstawy RDF, RDFS i słowników

**Typ i język literału**: Znacznik języka tylko dla tekstu dla ludzi i wyklucza typ; daty zawsze z xsd:date. → [Literały: typ i język](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język)

**Grafy nazwane w TriG**: Przynależność do linii niesie nazwa grafu, w którym leży trójka. → [Dataset i grafy nazwane w TriG](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#dataset-i-grafy-nazwane-w-trig)

```turtle
ex:linia_a {
  ex:p1 bpc:odwiedzil ex:w1 .
}
```

**Domain i range nie walidują**: To przesłanki do wnioskowania, nic nie odrzucają, więc poprawność danych sprawdzaj osobno. → [Typy, etykiety, domain i range](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range)

```turtle
bpc:odwiedzil a rdf:Property ;
  rdfs:domain bpc:Podroznik ;
  rdfs:range  bpc:Wizyta .
```

**Rozdział słownika bpc od instancji**: Klasy i własności trzymaj w bpc:, instancje w osobnej przestrzeni ex:; owl:sameAs tylko dla potwierdzonej tożsamości. → [Słownik bpc a IRI instancji](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#słownik-bpc-a-iri-instancji)

**Pobrać URI terminów PROV-O**: Przestrzeń nazw to http://www.w3.org/ns/prov# z # na końcu. → [Pełne URI terminów PROV-O](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#pełne-uri-terminów-prov-o)

```bash
curl -sL -H 'Accept: text/turtle' http://www.w3.org/ns/prov \
  | grep -A3 'prov:wasGeneratedBy'
```

## 03. Model danych Biura

**Wizyta jako węzeł czy trójka**: Węzeł, gdy zdarzenie ma własne atrybuty lub inne zasoby się do niego odwołują; stałą cechę zapisz jedną trójką. → [Wizyta jako węzeł, nie trójka](03%20Model%20danych%20Biura.md#wizyta-jako-węzeł-nie-trójka)

**Układ grafów w modelu Biura**: Wspólne fakty w grafie domyślnym, wizyty w grafach linii, metadane w provenance. → [Słowniki, przestrzenie i grafy modelu](03%20Model%20danych%20Biura.md#słowniki-przestrzenie-i-grafy-modelu)

```turtle
ex:linia_a { ex:w1 a bpc:Wizyta ; bpc:linia ex:linia_a ; ... }
ex:linia_b { ex:w2 a bpc:Wizyta ; bpc:linia ex:linia_b ; ... }
ex:provenance { ... }
```

**Po jednym zepsutym wierszu CSV na analizę**: Brak (pusta komórka) to osobny przypadek niż błąd; bez zepsutych wierszy analizy nie mają wyniku. → [Wiersze CSV dla sześciu analiz](03%20Model%20danych%20Biura.md#wiersze-csv-dla-sześciu-analiz)

**Klucz główny i obcy jako IRI**: Klucz obcy to to samo IRI zbudowane z komórki innego wiersza; etykiety osobno w rdfs:label. → [Klucze jako IRI i połączenia](03%20Model%20danych%20Biura.md#klucze-jako-iri-i-połączenia)

```python
def iri_for(key, kind=""):
    return EX + (f"{kind}_{key}" if kind else key)
```

**Tabela mapowania kolumn**: Wiersz: subject, predicate, object, typ RDF, słownik, uzasadnienie; daty dostają xsd:date. → [Wiersz mapowania kolumn wizyty](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty)

```python
"od":        ("ex:{id}", "bpc:od", "{od}", "xsd:date", "bpc", "analizy porównują daty"),
```

## 04. Konwersja CSV do TriG

**Ile trójek daje wiersz CSV**: Liczbę trójek wyznacza tabela mapowania, nie liczba komórek; kolumna linia wybiera graf. → [Jeden wiersz wizyty do TriG](04%20Konwersja%20CSV%20do%20TriG.md#jeden-wiersz-wizyty-do-trig)

**Konwersja jako prov:Activity**: Opisuj ją w osobnym grafie ex:provenance; wyniki dostają prov:wasGeneratedBy i prov:wasDerivedFrom. → [Konwersja CSV w PROV-O](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o)

```turtle
ex:konwersja_wizyty a prov:Activity ;
    prov:used ex:wizyty_csv ;
    prov:wasAssociatedWith ex:konwerter ;
```

**Dataset rdflib i zapis TriG**: Trójki dodawaj do grafu zwróconego przez ds.graph(iri); instalacja: pip install "rdflib>=7,<8". → [Dataset rdflib i zapis TriG](04%20Konwersja%20CSV%20do%20TriG.md#dataset-rdflib-i-zapis-trig)

```python
g = ds.graph(EX.linia_a)
g.add((EX.p1, BPC.odwiedzil, EX.w1))
ds.serialize("biuro.trig", format="trig")
```

**Warunki identycznego TriG**: Potrzeba: deterministyczne IRI, stała kolejność, brak węzłów pustych i czas jako parametr. → [Identyczny TriG w dwóch przebiegach](04%20Konwersja%20CSV%20do%20TriG.md#identyczny-trig-w-dwóch-przebiegach)

```python
def convert(src, dst, started="2026-09-26T10:00:00Z"):
    ...
    rows = sorted(rows, key=lambda r: r["id"])
```

**Walidacja: błędy a ostrzeżenia**: Wgranie blokują tylko errors (duplikat klucza, zły typ); klucz obcy bez rekordu to warning. → [Walidacja wynikowego grafu](04%20Konwersja%20CSV%20do%20TriG.md#walidacja-wynikowego-grafu)

```python
if getattr(o, "datatype", None) != XSD.date:
    errors.append(f"zły typ: {s} bpc:od {o!r}")
```

## 05. SPARQL SELECT i wzorce trójek

**SELECT wizyt podróżnika (union graph)**: Bez FROM z UnionGraph zapytanie widzi tylko graf domyślny; średnik łączy trójki o tym samym podmiocie. → [Wizyty podróżnika w SELECT](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#wizyty-podróżnika-w-select)

```sparql
SELECT ?wizyta ?od ?do
FROM <urn:x-arq:UnionGraph>
WHERE {
```

**Porównanie dat w FILTER**: Napis lub zły typ daje błąd typu i wiersz znika po cichu. → [Daty w FILTER i literały o złym typie](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#daty-w-filter-i-literały-o-złym-typie)

```sparql
FILTER (?od >= "0027-03-03"^^xsd:date)
```

**Szukanie braków: NOT EXISTS**: Do samych braków; OPTIONAL z !BOUND, gdy obok braków chcesz też wiersze z wartością. → [OPTIONAL a FILTER NOT EXISTS](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#optional-a-filter-not-exists)

```sparql
?wizyta a bpc:Wizyta .
FILTER NOT EXISTS { ?wizyta bpc:do ?do }
```

**Zliczanie po grafach: GRAPH ?g**: Stałe IRI w GRAPH albo FROM NAMED ogranicza zapytanie do wskazanego grafu. → [Zapytania w wybranym grafie](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zapytania-w-wybranym-grafie)

```sparql
SELECT ?g (COUNT(?w) AS ?n) WHERE {
  GRAPH ?g { ?w a bpc:Wizyta }
} GROUP BY ?g
```

**HAVING po agregacji**: HAVING filtruje grupy, FILTER wiersze przed agregacją; w HAVING powtarzasz wyrażenie, nie alias. → [Zliczanie zdarzeń w grafach i HAVING](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zliczanie-zdarzeń-w-grafach-i-having)

```sparql
GROUP BY ?g
HAVING (COUNT(DISTINCT ?w) > 1)
```

## 06. Analizy paradoksów w SPARQL

**Brak a błąd danych: UNION + NOT EXISTS**: Brak to nieobecna trójka klucza obcego, błąd to klucz wskazujący IRI bez opisu; ?s wiąż w każdej gałęzi osobno. → [Spotkanie bez wizyty i wizyta bez powiązania](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#spotkanie-bez-wizyty-i-wizyta-bez-powiązania)

```sparql
{ ?s a bpc:Spotkanie .
  FILTER NOT EXISTS { ?s bpc:naWizycie ?w }
  BIND("brak" AS ?rodzaj) }
```

**Wspólne i tylko w jednej linii**: Trzy gałęzie UNION (wspólne, tylko A, tylko B); działa przy tym samym IRI wizyty w obu liniach. → [Wspólne i tylko w jednej linii](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#wspólne-i-tylko-w-jednej-linii)

```sparql
{ GRAPH ex:linia_a { ?p bpc:odwiedzil ?w }
  FILTER NOT EXISTS { GRAPH ex:linia_b { ?p bpc:odwiedzil ?w } }
  BIND("tylko A" AS ?rodzaj) }
```

**Grafy nazwane czy UnionGraph w analizach**: Analizy ze śladem linii (1, 3, 5, 6) czytają grafy nazwane; 2 i 4 czytają sumę przez FROM <urn:x-arq:UnionGraph>. → [Grafy nazwane czy jeden graf](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#grafy-nazwane-czy-jeden-graf)

## 07. Graf wiedzy Biura Paradoksów Czasowych

**Wynik SELECT/ASK przez HTTP w Pythonie**: Wartości są napisami, a niezwiązane zmienne nie mają klucza w wierszu. → [Zapytanie SPARQL przez HTTP](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#zapytanie-sparql-przez-http)

```python
if "boolean" in data:
    return data["boolean"]
return [{k: v["value"] for k, v in row.items()}
```

**Porównać liczby trójek z pliku i Fuseki**: Kod 200 przy wgraniu nie dowodzi trafienia do grafów; dodaj próbkę ASK dla konkretnej trójki. → [Kontrola grafów linii z Pythona](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#kontrola-grafów-linii-z-pythona)

```python
fuseki = {r["g"]: int(r["n"]) for r in run_query(kontrola)}
assert fuseki == oczekiwane, (fuseki, oczekiwane)
```

**Gdzie szukać błędu interpretacji**: IRI, grafy i słowniki ustala konwersja CSV, więc błąd w wynikach szukaj najpierw tam. → [Od CSV do sześciu analiz](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#od-csv-do-sześciu-analiz)
