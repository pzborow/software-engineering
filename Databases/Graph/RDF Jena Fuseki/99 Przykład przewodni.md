# Przykład przewodni: Biuro Paradoksów Czasowych

Fikcyjne Biuro Paradoksów Czasowych zbiera dane o podróżnikach, wizytach, epokach, artefaktach, spotkaniach i raportach agentów z wielu linii czasu. Dane z CSV trafiają jako RDF do datasetu Fuseki, a sześć analiz SPARQL wykrywa w nich sprzeczności.

**Dokąd zmierza:** Zaczynamy od pustego serwera Fuseki, sześciu pytań Biura i tabel z widocznymi sprzecznościami. Potem dodajemy słownik i model danych oraz deterministyczny konwerter CSV->TriG z PROV-O i walidacją, i wgrywamy grafy nazwane, po jednym na linię czasu. Na końcu odpowiadamy na sześć pytań zapytaniami SPARQL wysyłanymi z Pythona przez HTTP.

## Plan przyrostów

| Dział | Co przybywa |
|---|---|
| [01. Serwer Fuseki i pytania Biura](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md) | Uruchamiamy Fuseki na Javie 17, tworzymy dataset /biuro, poznajemy sześć pytań Biura i pierwsze trójki z tabel. |
| [02. Podstawy RDF, RDFS i słowników](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md) | Wybieramy typy, grafy nazwane, rozdział słownika bpc od IRI instancji i terminy PROV-O, OWL-Time, RDFS i XSD. |
| [03. Model danych Biura](03%20Model%20danych%20Biura.md) | Powstaje model Biura (klasy, własności, mapowanie kolumn), dane CSV ze sprzecznościami i funkcja iri_for z obsługą pustych i błędnych wartości. |
| [04. Konwersja CSV do TriG](04%20Konwersja%20CSV%20do%20TriG.md) | Powstaje konwerter CSV->TriG z provenance, walidacją i deterministycznym wynikiem, a plik trafia do Fuseki. |
| [05. SPARQL SELECT i wzorce trójek](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md) | Zapytania SELECT sprawdzają załadowane dane: liczby trójek, daty, braki, grafy i nakładające się wizyty. |
| [06. Analizy paradoksów w SPARQL](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md) | Powstaje sześć analiz SPARQL zapisanych w queries/, z rozróżnieniem tych, które używają grafów nazwanych. |
| [07. Graf wiedzy Biura Paradoksów Czasowych](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md) | Klient Pythona wysyła analizy do Fuseki przez HTTP, potwierdza grafy i domyka przepływ od CSV do interpretacji. |

## Stan kodu po ostatnim dziale

Szkic, nie działający kod: nazwy i sygnatury, których trzymają się przykłady w tekście.

### `(bez pliku)`

```python
@prefix bpc: <http://example.org/bpc#> .

bpc:Podroznik a rdfs:Class .

bpc:Wizyta a rdfs:Class .

bpc:odwiedzil a rdf:Property ;
  rdfs:domain bpc:Podroznik ;
  rdfs:range  bpc:Wizyta .

ex:linia_a { ex:p1 bpc:odwiedzil ex:w1 . }
ex:linia_b { ex:p1 bpc:odwiedzil ex:w2 . }

bpc:epoka a rdf:Property .

bpc:linia a rdf:Property .

bpc:od a rdf:Property ;
  rdfs:range xsd:date .

bpc:do a rdf:Property .

@prefix ex: <http://example.org/id/> .

ex:epoka_rzym a time:Interval ;
  rdfs:label "Rzym" ;
  time:hasBeginning ex:epoka_rzym_poczatek ;
  time:hasEnd ex:epoka_rzym_koniec .
ex:epoka_rzym_poczatek time:inXSDDate "0027-01-01"^^xsd:date .
ex:epoka_rzym_koniec time:inXSDDate "0476-09-04"^^xsd:date .

bpc:Epoka a rdfs:Class .

bpc:Artefakt a rdfs:Class .

bpc:Spotkanie a rdfs:Class .

bpc:Raport a rdfs:Class .

bpc:powstal a rdf:Property ;
  rdfs:domain bpc:Artefakt ;
  rdfs:range  xsd:date .

bpc:uczestnik a rdf:Property ;
  rdfs:domain bpc:Spotkanie ;
  rdfs:range  bpc:Podroznik .

bpc:naWizycie a rdf:Property ;
  rdfs:domain bpc:Spotkanie ;
  rdfs:range  bpc:Wizyta .

bpc:opisuje a rdf:Property ;
  rdfs:domain bpc:Raport ;
  rdfs:range  bpc:Wizyta .

bpc:pojawilSie a rdf:Property ;
  rdfs:domain bpc:Artefakt ;
  rdfs:range  bpc:Wizyta .

# owl:sameAs omitted: fikcyjna osoba bez zweryfikowanego IRI zewnętrznego.
```

- **bpc:** (prefiks słownika): Prefiks słownika Biura. Wprowadzony: [01 › Trójka, wiersz i prefiksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
- **bpc:Podroznik** (klasa RDFS): Klasa podróżników. Wprowadzony: [01 › Trójka, wiersz i prefiksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
- **bpc:Wizyta** (klasa RDFS): Klasa wizyt. Wprowadzony: [01 › Trójka, wiersz i prefiksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
- **bpc:odwiedzil** (własność RDF): Łączy podróżnika z wizytą. Wprowadzony: [01 › Trójka, wiersz i prefiksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
  - zmiana w [02 › Typy, etykiety, domain i range](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range): Dodajemy domain i range do własności kanonu.
- **graf linii czasu** (graf nazwany): Osobny graf nazwany dla każdej linii czasu. Wprowadzony: [02 › Dataset i grafy nazwane w TriG](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#dataset-i-grafy-nazwane-w-trig).
- **bpc:epoka** (własność RDF): Kolumna epoka wizyty jako własność. Wprowadzony: [02 › Literały: typ i język](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język).
- **bpc:linia** (własność RDF): Kolumna linia wizyty jako własność. Wprowadzony: [02 › Literały: typ i język](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język).
- **bpc:od** (własność RDF): Początek wizyty jako literał xsd:date. Wprowadzony: [02 › Literały: typ i język](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język).
  - zmiana w [02 › Typy, etykiety, domain i range](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range): Dodajemy range typu xsd:date.
- **bpc:do** (własność RDF): Koniec wizyty jako literał xsd:date. Wprowadzony: [02 › Literały: typ i język](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język).
- **ex:** (prefiks danych): Przestrzeń nazw instancji, rozdzielona od słownika bpc:. Wprowadzony: [02 › Słownik bpc a IRI instancji](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#słownik-bpc-a-iri-instancji).
- **ex:epoka_rzym** (zasób time:Interval): Epoka jako przedział OWL-Time, w odróżnieniu od wizyt z bpc:od i bpc:do. Wprowadzony: [02 › Kryterium wyboru terminów](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kryterium-wyboru-terminów).
  - zmiana w [04 › Identyczny TriG w dwóch przebiegach](04%20Konwersja%20CSV%20do%20TriG.md#identyczny-trig-w-dwóch-przebiegach): Węzły puste dostają losowe identyfikatory w każdym przebiegu, więc konwerter zapisuje początek i koniec epoki jako zasoby z IRI, by plik był identyczny.
- **bpc:Epoka** (klasa RDFS): Epoka opisana przedziałem OWL-Time. Wprowadzony: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
- **bpc:Artefakt** (klasa RDFS): Przedmiot z datą powstania. Wprowadzony: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
- **bpc:Spotkanie** (klasa RDFS): Spotkanie podróżników. Wprowadzony: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
- **bpc:Raport** (klasa RDFS): Raport agenta o wizycie. Wprowadzony: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
- **bpc:powstal** (własność RDF): Data powstania artefaktu. Wprowadzony: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
- **bpc:uczestnik** (własność RDF): Uczestnik spotkania. Wprowadzony: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
- **bpc:naWizycie** (własność RDF): Wizyta, podczas której odbyło się spotkanie. Wprowadzony: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
- **bpc:opisuje** (własność RDF): Wizyta opisana w raporcie. Wprowadzony: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
- **bpc:pojawilSie** (własność RDF): Łączy artefakt z wizytą, w której się pojawił (kolumna wizyta z artefakty.csv). Wprowadzony: [06 › Artefakt przed datą powstania](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#artefakt-przed-datą-powstania).
- **ex:podroznik_jan** (zasób RDF): Nie deklarujemy owl:sameAs dla fikcyjnej osoby; brak zweryfikowanej tożsamości zewnętrznej. Wprowadzony: [02 › Kiedy zewnętrzny URI, a kiedy sameAs](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kiedy-zewnętrzny-uri-a-kiedy-sameas).

### `analiza_1.rq`

```python
SELECT ?p ?w1 ?w2 ?od1 ?do1 ?od2 ?do2 WHERE {
  GRAPH ex:linia_a { ?p bpc:odwiedzil ?w1 . ?w1 bpc:od ?od1 ; bpc:do ?do1 . }
  GRAPH ex:linia_b { ?p bpc:odwiedzil ?w2 . ?w2 bpc:od ?od2 ; bpc:do ?do2 . }
  FILTER (?od1 <= ?do2 && ?od2 <= ?do1)
}
```

- **analiza_1.rq** (zapytanie SPARQL): Pierwsza analiza Biura: podróżnik w dwóch liniach czasu w tym samym czasie. Wprowadzony: [05 › Nakładające się wizyty w dwóch liniach](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#nakładające-się-wizyty-w-dwóch-liniach).

### `analiza_2.rq`

```python
ASK
FROM <urn:x-arq:UnionGraph>
{ ex:p1 (bpc:odwiedzil/^bpc:naWizycie/bpc:uczestnik)+ ex:p2 }
```

- **analiza_2.rq** (zapytanie SPARQL): Sprawdza, czy istnieje łańcuch spotkań między dwoma podróżnikami. Wprowadzony: [06 › Łańcuch spotkań między podróżnikami](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#łańcuch-spotkań-między-podróżnikami).

### `analiza_N.rq`

```python
analiza_1.rq ... analiza_6.rq
```

- **analiza_1..6.rq** (zapytanie SPARQL): Sześć analiz odpowiadających pytaniom Biura. Wprowadzony: [01 › Pytania Biura o paradoksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#pytania-biura-o-paradoksy).

### `apache-jena-fuseki-5.x.y/`

```python
./fuseki-server            # port 3030, bez datasetu
./fuseki-server --port=3031
```

- **fuseki-server** (proces serwera): Serwer SPARQL, w którym powstanie dataset /biuro. Wprowadzony: [01 › Start Fuseki na Javie 17](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#start-fuseki-na-javie-17).

### `biuro.trig`

```python
ex:provenance { ... }

ex:wizyty_csv a prov:Entity .

ex:konwersja_wizyty a prov:Activity ;
  prov:used ex:wizyty_csv ;
  prov:wasAssociatedWith ex:konwerter ;
  prov:startedAtTime "2026-09-26T10:00:00Z"^^xsd:dateTime ;
  prov:endedAtTime "2026-09-26T10:00:05Z"^^xsd:dateTime .

ex:konwerter a prov:SoftwareAgent .

ex:linia_a a prov:Entity ;
  prov:wasGeneratedBy ex:konwersja_wizyty ;
  prov:wasDerivedFrom ex:wizyty_csv .

ex:linia_b a prov:Entity ;
  prov:wasGeneratedBy ex:konwersja_wizyty ;
  prov:wasDerivedFrom ex:wizyty_csv .
```

- **graf provenance** (graf nazwany): Graf z metadanymi konwersji CSV, osobny od grafów linii czasu. Wprowadzony: [03 › Słowniki, przestrzenie i grafy modelu](03%20Model%20danych%20Biura.md#słowniki-przestrzenie-i-grafy-modelu).
- **ex:wizyty_csv** (zasób prov:Entity): IRI opisujące plik wizyty.csv jako wejście konwersji. Wprowadzony: [04 › Konwersja CSV w PROV-O](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o).
- **ex:konwersja_wizyty** (zasób prov:Activity): Aktywność konwersji w grafie ex:provenance. Wprowadzony: [04 › Konwersja CSV w PROV-O](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o).
- **ex:konwerter** (zasób prov:SoftwareAgent): Agent wykonujący konwersję. Wprowadzony: [04 › Konwersja CSV w PROV-O](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o).
- **ex:linia_a** (graf nazwany i zasób prov:Entity): Graf linii jest też encją opisaną w ex:provenance. Wprowadzony: [04 › Konwersja CSV w PROV-O](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o).
- **ex:linia_b** (graf nazwany i zasób prov:Entity): Druga linia czasu, też wynik konwersji. Wprowadzony: [04 › Konwersja CSV w PROV-O](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o).

### `dane/artefakty.csv`

```python
id,nazwa,powstal,wizyta
```

- **artefakty.csv** (plik CSV): Artefakt a1 z datą powstania 0150. Wprowadzony: [03 › Wiersze CSV dla sześciu analiz](03%20Model%20danych%20Biura.md#wiersze-csv-dla-sześciu-analiz).

### `dane/epoki.csv`

```python
id,nazwa,od,do
```

- **epoki.csv** (plik CSV): Epoka rzym. Wprowadzony: [03 › Wiersze CSV dla sześciu analiz](03%20Model%20danych%20Biura.md#wiersze-csv-dla-sześciu-analiz).

### `dane/podroznicy.csv`

```python
id,imie
```

- **podroznicy.csv** (plik CSV): Podróżnicy p1..p4. Wprowadzony: [03 › Wiersze CSV dla sześciu analiz](03%20Model%20danych%20Biura.md#wiersze-csv-dla-sześciu-analiz).

### `dane/raporty.csv`

```python
id,agent,wizyta,od,do
```

- **raporty.csv** (plik CSV): Raport r1 z inną datą końca w1. Wprowadzony: [03 › Wiersze CSV dla sześciu analiz](03%20Model%20danych%20Biura.md#wiersze-csv-dla-sześciu-analiz).

### `dane/spotkania.csv`

```python
id,wizyta,uczestnik1,uczestnik2
```

- **spotkania.csv** (plik CSV): Spotkania s1..s4 tworzące łańcuch; s4 bez wizyty. Wprowadzony: [03 › Wiersze CSV dla sześciu analiz](03%20Model%20danych%20Biura.md#wiersze-csv-dla-sześciu-analiz).

### `databases/biuro`

```python
/biuro/query   # SPARQL query
/biuro/update  # SPARQL Update
/biuro/data    # Graph Store Protocol
```

- **/biuro** (dataset Fuseki (TDB2)): Trwały dataset, do którego trafią grafy linii czasu. Wprowadzony: [01 › Dataset biuro w przeglądarce](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce).

### `klient SPARQL (jeszcze bez pliku)`

```python
def run_query(query, endpoint="http://localhost:3030/biuro/query"):
    # POST, Content-Type: application/sparql-query, Accept: application/sparql-results+json
    ...
    return data["boolean"]  # ASK
    return [{k: v["value"] for k, v in row.items()} for row in bindings]  # SELECT
```

- **run_query** (funkcja Pythona): Wysyła zapytanie do Fuseki i zwraca boolean albo listę słowników zmienna→wartość. Wprowadzony: [07 › Zapytanie SPARQL przez HTTP](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#zapytanie-sparql-przez-http).

### `kontrola.rq`

```python
SELECT ?g (COUNT(*) AS ?n) WHERE {
  GRAPH ?g { ?s ?p ?o }
} GROUP BY ?g ORDER BY ?g
```

- **kontrola.rq** (zapytanie SPARQL): Zlicza trójki w każdym grafie nazwanym po wgraniu TriG. Wprowadzony: [07 › Od CSV do sześciu analiz](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#od-csv-do-sześciu-analiz).

### `konwerter (jeszcze bez pliku)`

```python
mapping = {
  "id": ("ex:{id}", "rdf:type", "bpc:Wizyta", "IRI", "bpc", "..."),
  "od": ("ex:{id}", "bpc:od", "{od}", "xsd:date", "bpc", "..."),
  ...
}

EX = "http://example.org/id/"
def iri_for(key, kind=""):
    local = quote(normalize("NFC", key.strip()), safe="")
    return EX + (f"{kind}_{local}" if kind else local)

def convert(csv_paths, out, started="2026-09-26T10:00:00Z"):
    ds = Dataset()
    prov = ds.graph(URIRef(EX + "provenance"))
    for path in sorted(csv_paths): ...
    # prov:startedAtTime = started, koniec = started + 5 s

def validate(path):
    ds = Dataset(default_union=True)
    ds.parse(path, format="trig")
    ...
    return errors, warnings

def load_trig(path, endpoint="http://localhost:3030/biuro/data"):
    # POST, Content-Type: application/trig, bez ?graph=
    ...
    return resp.status, resp.read().decode()

def date_literal(cell):
    cell = cell.strip()
    if not cell:
        return None
    return f'"{date.fromisoformat(cell).isoformat()}"^^xsd:date'

ds = Dataset()
g = ds.graph(EX.linia_a)
g.add((EX.p1, BPC.odwiedzil, EX.w1))
ds.serialize("biuro.trig", format="trig")
```

- **mapping** (tabela mapowania (słownik Pythona)): Szablony subject/object i typ RDF dla każdej kolumny wizyty. Wprowadzony: [03 › Wiersz mapowania kolumn wizyty](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty).
- **iri_for** (funkcja Pythona): Buduje IRI zasobu z klucza CSV, opcjonalnie z przedrostkiem rodzaju. Wprowadzony: [03 › Klucze jako IRI i połączenia](03%20Model%20danych%20Biura.md#klucze-jako-iri-i-połączenia).
  - zmiana w [03 › Znaki specjalne w kluczach IRI](03%20Model%20danych%20Biura.md#znaki-specjalne-w-kluczach-iri): Klucze ze spacją, / lub znakami spoza ASCII wymagają kodowania procentowego i normalizacji NFC; zwykłe klucze dają ten sam adres co dotąd.
- **convert** (funkcja Pythona): Deterministyczna konwersja: sortowane wiersze, stały czas, brak węzłów pustych. Wprowadzony: [04 › Identyczny TriG w dwóch przebiegach](04%20Konwersja%20CSV%20do%20TriG.md#identyczny-trig-w-dwóch-przebiegach).
  - zmiana w [04 › Od CSV do zwalidowanego TriG](04%20Konwersja%20CSV%20do%20TriG.md#od-csv-do-zwalidowanego-trig): convert przyjmuje listę plików CSV i ścieżkę wyjścia; started podawany z wiersza poleceń (--started)
- **validate** (funkcja Pythona): Wczytuje TriG i zwraca błędy blokujące oraz ostrzeżenia. Wprowadzony: [04 › Walidacja wynikowego grafu](04%20Konwersja%20CSV%20do%20TriG.md#walidacja-wynikowego-grafu).
- **load_trig** (funkcja Pythona): Wgrywa biuro.trig do datasetu biuro z zachowaniem nazw grafów. Wprowadzony: [04 › Wgranie TriG z nazwami grafów](04%20Konwersja%20CSV%20do%20TriG.md#wgranie-trig-z-nazwami-grafów).
- **date_literal** (funkcja Pythona): Zwraca None dla braku, literał xsd:date dla poprawnej daty, ValueError dla błędnej. Wprowadzony: [03 › Pusta komórka i zła data](03%20Model%20danych%20Biura.md#pusta-komórka-i-zła-data).
- **ds** (obiekt rdflib Dataset): Dataset z grafem nazwanym linii czasu zapisany jako TriG. Wprowadzony: [04 › Dataset rdflib i zapis TriG](04%20Konwersja%20CSV%20do%20TriG.md#dataset-rdflib-i-zapis-trig).

### `wizyty.csv`

```python
id,podroznik,epoka,linia,od,do
```

- **wizyty.csv** (plik CSV): Tabela wizyt z widoczną sprzecznością w1/w2. Wprowadzony: [01 › Pytania Biura o paradoksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#pytania-biura-o-paradoksy).
