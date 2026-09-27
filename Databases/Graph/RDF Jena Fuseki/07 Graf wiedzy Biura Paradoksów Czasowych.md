# Graf wiedzy Biura Paradoksów Czasowych

Zapytania SPARQL z działów 05 i 06 znasz z panelu, a w usłudze wyśle je kod, więc ten dział przenosi je do Pythona i pokazuje, jak sprawdzić, że dane trafiły do właściwych grafów. Po lekturze wyślesz zapytanie do Fuseki przez HTTP i odczytasz wiązania z JSON-a, potwierdzisz przypisanie linii czasu do [grafów nazwanych](00%20Glosariusz.md#graf-nazwany) i opiszesz cały przepływ od CSV do sześciu analiz, wskazując, gdzie zapadają decyzje o IRI, grafach i słownikach. Dział łączy dane i grafy nazwane z działów 03 i 04 (model, konwersja CSV do TriG, wgranie) z zapytaniami z działów 05 i 06, a HTTP i JSON znasz już z backendu, więc Fuseki jest tu po prostu kolejnym serwisem REST. W przykładzie Biura Paradoksów Czasowych klient wysyła analizy, potwierdza grafy i domyka drogę od CSV do interpretacji.

```text
CSV --[decyzje: IRI, grafy, słowniki]--> TriG --ładowanie--> Fuseki (dataset biuro)
                                                              ^         |
                     zapytanie SPARQL przez HTTP              |         | application/sparql-results+json
                                                              |         v
                                                       klient Pythona: kontrola grafów nazwanych
                                                                        -> sześć analiz -> interpretacja
```

**W tym dziale:**

- [Zapytanie SPARQL przez HTTP](#zapytanie-sparql-przez-http)
- [Kontrola grafów linii z Pythona](#kontrola-grafów-linii-z-pythona)
- [Od CSV do sześciu analiz](#od-csv-do-sześciu-analiz)

## Zapytanie SPARQL przez HTTP

Dotąd analizy działały w panelu, a odpowiedzi na sześć pytań Biura mają wychodzić ze skryptu. Zapytanie wysyłasz do `/biuro/query` przez HTTP, a wynik w formacie [application/sparql-results+json](00%20Glosariusz.md#applicationsparql-resultsjson) (standardowy zapis odpowiedzi SPARQL jako JSON) czytasz jak zwykły JSON.

Z `load_trig` łączy to tylko HTTP. Tamta funkcja wgrywała dane przez [Graph Store Protocol](00%20Glosariusz.md#graph-store-protocol) na `/biuro/data`, a tu mówisz do innego punktu, `/biuro/query`, protokołem zapytań SPARQL, i to serwer odsyła dane.

Zapytanie idzie jako POST z nagłówkiem `Content-Type: application/sparql-query`, a `Accept` wybiera format odpowiedzi. Wynik SELECT ma dwie części: `head.vars` (nazwy kolumn) i `results.bindings` (lista wierszy). Wiersz to [słownik](00%20Glosariusz.md#słownik) `zmienna → {"type", "value"}`, do którego literał z typem dokłada `"datatype"`, a literał z językiem `"xml:lang"`. Wartość jest zawsze napisem, więc datę zamienisz na `date` sam. Zmiennej niezwiązanej (np. w innej gałęzi UNION) w wierszu po prostu nie ma, więc używaj `row.get(...)`.

[ASK](00%20Glosariusz.md#ask) to postać zapytania, która sprawdza, czy wzorzec ma dopasowanie, i zwraca tylko prawdę albo fałsz. Tak działa zapytanie o [łańcuch spotkań między podróżnikami](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#łańcuch-spotkań-między-podróżnikami), a jego odpowiedź to `{"head": {}, "boolean": true}`, bez `bindings`.

```python
def run_query(query, endpoint="http://localhost:3030/biuro/query"):
    req = urllib.request.Request(
        endpoint, data=query.encode("utf-8"),
        headers={"Content-Type": "application/sparql-query",
                 "Accept": "application/sparql-results+json"})
    with urllib.request.urlopen(req) as resp:
        data = json.load(resp)
    if "boolean" in data:
        return data["boolean"]
    return [{k: v["value"] for k, v in row.items()}
            for row in data["results"]["bindings"]]
```

Błąd składni Fuseki zgłasza kodem 400, a `urlopen` zamienia go na `HTTPError`; 404 oznacza zły adres datasetu. Prefiksy `bpc:` i `ex:` deklaruj w pliku `.rq`, bo serwer ich nie zna.

_Wersje: SPARQL 1.1_

## Kontrola grafów linii z Pythona

[Skoro `run_query` już działa](#zapytanie-sparql-przez-http), użyj go do sprawdzenia, czy wgrany TriG trafił do właściwych grafów. <a id="ref-99"></a>Kod 200 przy wgraniu tego nie dowodzi, bo mówi tylko, że serwer przyjął plik. Dowodem jest zapytanie, które zlicza trójki w każdym grafie nazwanym i porównuje wynik z plikiem, który konwerter zapisał.

Zapytanie grupuje po nazwie grafu, tak jak zliczanie grafów w panelu tuż po załadowaniu danych. Zapisz je jako `kontrola.rq`:

```sparql
SELECT ?g (COUNT(*) AS ?n) WHERE {
  GRAPH ?g { ?s ?p ?o }
} GROUP BY ?g ORDER BY ?g
```

`GRAPH ?g` widzi tylko grafy nazwane, a grupy puste nie istnieją. Oczekiwane liczby weź więc z pliku, pomijając [graf domyślny](00%20Glosariusz.md#graf-domyślny) rdflib (`urn:x-rdflib:default`), który `ds.graphs()` zwraca zawsze, nawet pusty:

```python
ds = Dataset()
ds.parse("biuro.trig", format="trig")
oczekiwane = {str(g.identifier): len(g) for g in ds.graphs()
              if g.identifier != DATASET_DEFAULT_GRAPH_ID and len(g)}
kontrola = open("kontrola.rq", encoding="utf-8").read()
fuseki = {r["g"]: int(r["n"]) for r in run_query(kontrola)}
assert fuseki == oczekiwane, (fuseki, oczekiwane)
```

`DATASET_DEFAULT_GRAPH_ID` pochodzi z `rdflib.graph`. `run_query` spłaszcza wiersze do samych wartości, więc `r["g"]` to już napis, a `?n` zamieniasz na `int`.

Ten sam zestaw nazw i liczb oznacza, że `ex:linia_a`, `ex:linia_b` i `ex:provenance` istnieją i mają tyle trójek, ile plik. Brak `ex:linia_a` lub `ex:linia_b` wskazuje wgranie do złego endpointu albo dane w grafie domyślnym. Zaniżona liczba jednej linii wskazuje zły rozdział wierszy po kolumnie `linia`.

Liczby nie wykażą zamiany trójek między liniami, więc dodaj próbkę: `ASK { GRAPH ex:linia_b { ex:p1 bpc:odwiedzil ex:w2 } }` powinno dać `true`, a to samo w `ex:linia_a` `false`.

_Wersje: rdflib 7.x · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#07-graf-wiedzy-biura-paradoksów-czasowych)_

## Od CSV do sześciu analiz

Przepływ ma pięć etapów, a decyzje o IRI, grafach i słownikach zapadają w dwóch pierwszych: w `mapping` z `iri_for` i w `convert`. Reszta to mechanika, która te decyzje tylko odczytuje.

```text
dane/*.csv → mapping + iri_for → convert → biuro.trig
   → validate → load_trig (POST /biuro/data) → kontrola.rq
   → run_query (POST /biuro/query) → analiza_1..6.rq → interpretacja
```

### Gdzie co zapada

| Decyzja | Miejsce | Skutek dalej |
|---|---|---|
| [IRI](00%20Glosariusz.md#iri) zasobów | `iri_for` (strip, NFC, quote) | to samo IRI wizyty w obu liniach; bez tego analiza „[wspólne i tylko w jednej linii](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#wspólne-i-tylko-w-jednej-linii)” widzi dwie różne wizyty |
| graf | wartość kolumny `linia` w `wizyty.csv`; `convert` wpisuje trójki do grafu o tej nazwie (`ex:linia_a`, `ex:linia_b`) | [ślad linii w wynikach analiz 1, 3, 5 i 6](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#grafy-nazwane-czy-jeden-graf) |
| słownik | kolumna „słownik” w [wierszu mapowania](00%20Glosariusz.md#wiersz-mapowania) (`bpc:` własny, `time:`, `prov:`) | nazwy w `analiza_N.rq` |
| czas i pochodzenie | parametr `started` w `convert`, graf `ex:provenance` | identyczny plik w każdym przebiegu i ślad pliku |

Zmiana IRI, kolumny `linia` albo słownika zmienia to, co widzą analizy, dlatego mapowanie i `iri_for` trzymaj w jednym miejscu, a nie w zapytaniach.

### Co dzieje się po decyzjach

`validate` blokuje wgranie przy błędach. `load_trig` wysyła plik bez `?graph=`, więc nazwy grafów zostają. [`kontrola.rq` (liczby trójek na graf) i próbka ASK](#kontrola-grafów-linii-z-pythona) potwierdzają, że decyzje o grafach dotarły do Fuseki.

Analizy 1, 3, 5 i 6 czytają grafy nazwane, więc znają linię. Analizy 2 i 4 czytają sumę grafów: zapytanie z `FROM <urn:x-arq:UnionGraph>` widzi połączone trójki wszystkich grafów, więc nie wiadomo, z której linii pochodzi wiersz. Interpretując wynik, zacznij od pytania, [czy zapytanie miało ślad linii](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#lm-46) i jakie IRI je spięło. Wynik to kandydat do sprawdzenia w CSV, a nie werdykt.

## Co zapamiętać

- Wynik SELECT to head.vars plus results.bindings z wierszami {type, value}, a ASK zwraca samo pole boolean; wartości są napisami, a niezwiązane zmienne nie mają klucza.
- Kod 200 przy wgraniu nie dowodzi trafienia do grafów; porównaj liczby trójek na graf z Fuseki z plikiem (bez grafu domyślnego) i dodaj próbkę ASK dla konkretnej trójki.
- IRI, grafy i słowniki ustalasz przy konwersji CSV, a analizy i kontrole tylko je odczytują, więc błąd w interpretacji szukaj najpierw tam.

## Pytania sprawdzające

### 43. Jak wyślesz zapytanie do endpointu Fuseki i odczytasz wiązania z application/sparql-results+json?

<details>
<summary>Odpowiedź</summary>

Wysyłasz zapytanie POST-em na /biuro/query z nagłówkiem Content-Type: application/sparql-query i Accept: application/sparql-results+json. W odpowiedzi SELECT czytasz head.vars oraz results.bindings, gdzie każdy wiersz mapuje zmienną na obiekt z type i value (a dla literałów opcjonalnie datatype albo xml:lang). ASK zwraca zamiast tego pole boolean. Wartości są napisami, więc daty konwertujesz sam, a niezwiązanych zmiennych w wierszu po prostu brak.

Zobacz: [sekcja „Zapytanie SPARQL przez HTTP”](#zapytanie-sparql-przez-http).

</details>

### 44. Jak potwierdzisz, że wszystkie linie czasu trafiły do właściwych grafów nazwanych?

<details>
<summary>Odpowiedź</summary>

Zlicz trójki w każdym grafie nazwanym zapytaniem z GROUP BY wysłanym przez run_query i porównaj wynik ze słownikiem policzonym z pliku biuro.trig (bez grafu domyślnego rdflib). Zgodne nazwy i liczby potwierdzają, że linie i provenance są w grafach. Dodatkowe ASK z konkretną trójką w każdej linii wykrywa zamianę trójek między liniami, której liczby nie widzą.

Zobacz: [sekcja „Kontrola grafów linii z Pythona”](#kontrola-grafów-linii-z-pythona).

</details>

### 45. Opisz cały przepływ od CSV do sześciu interpretowanych analiz i wskaż, gdzie zapadają decyzje o IRI, grafach i słownikach.

<details>
<summary>Odpowiedź</summary>

Przepływ to: CSV, mapowanie z iri_for, convert do biuro.trig, validate, load_trig, kontrola grafów i analizy przez run_query. Decyzje o IRI (iri_for), grafach (kolumna linia w wizyty.csv, którą convert zamienia na graf) i słownikach (kolumna słownika w wierszu mapowania) zapadają w mapowaniu i konwerterze. Dalsze etapy je tylko odczytują, a wynik analizy jest kandydatem do sprawdzenia w CSV.

Zobacz: [sekcja „Od CSV do sześciu analiz”](#od-csv-do-sześciu-analiz).

</details>
