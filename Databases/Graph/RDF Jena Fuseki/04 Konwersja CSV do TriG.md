# Konwersja CSV do TriG

Model Biura z działu 03 istnieje na razie tylko na papierze, więc ten dział zamienia go w działający potok: konwerter CSV→[TriG](00%20Glosariusz.md#trig) z [provenance](00%20Glosariusz.md#prov-o), walidacją i deterministycznym wynikiem, którego plik trafia do Fuseki. Po lekturze przeprowadzisz wiersz wizyty przez mapowanie do [trójek](00%20Glosariusz.md#trójka), opiszesz konwersję w PROV-O, zapiszesz [Dataset](00%20Glosariusz.md#dataset) w [rdflib](00%20Glosariusz.md#rdflib), wykryjesz błędy danych i wgrasz TriG tak, by [grafy nazwane](00%20Glosariusz.md#graf-nazwany) zachowały nazwy. Dziedziny splatają się tak: model wyznacza, jakie trójki i w jakich grafach powstają, PROV-O opisuje, skąd się wzięły, rdflib je generuje i waliduje, a Fuseki je przyjmuje i pozwala sprawdzić wynik. Dział korzysta z serwera i datasetu z działu 01, zapisu TriG z działu 02 i mapowania kolumn z działu 03.

```text
CSV -> mapowanie -> rdflib Dataset -> walidacja -> plik TriG -> Fuseki (dataset biuro)
                        \-> graf provenance (PROV-O)
```

**W tym dziale:**

- [Jeden wiersz wizyty do TriG](#jeden-wiersz-wizyty-do-trig)
- [Konwersja CSV w PROV-O](#konwersja-csv-w-prov-o)
- [Dataset rdflib i zapis TriG](#dataset-rdflib-i-zapis-trig)
- [Identyczny TriG w dwóch przebiegach](#identyczny-trig-w-dwóch-przebiegach)
- [Walidacja wynikowego grafu](#walidacja-wynikowego-grafu)
- [Od CSV do zwalidowanego TriG](#od-csv-do-zwalidowanego-trig)
- [Wgranie TriG z nazwami grafów](#wgranie-trig-z-nazwami-grafów)
- [Kolejność przygotowania środowiska](#kolejność-przygotowania-środowiska)
- [Stabilny zapis pliku TriG](#stabilny-zapis-pliku-trig)

## Jeden wiersz wizyty do TriG

[Tabelę mapowania](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty), `iri_for` i `date_literal` znasz osobno, więc <a id="ref-45"></a>przeprowadźmy przez nie jeden prawdziwy wiersz z `wizyty.csv`: `w1,p1,rzym,linia_a,0050-03-01,0050-03-10`.

Każda niepusta komórka przechodzi przez swój [wiersz mapowania](00%20Glosariusz.md#wiersz-mapowania) i daje jedną trójkę. Wyjątkiem jest `id`: [ta komórka daje dwie trójki, bo tworzy adres wizyty i jej klasę](03%20Model%20danych%20Biura.md#lm-15), a `podroznik` łączy wizytę z podróżnikiem.

| Kolumna | Komórka | Trójka |
|---|---|---|
| `id` | `w1` | `ex:w1 a bpc:Wizyta` |
| `podroznik` | `p1` | `ex:p1 bpc:odwiedzil ex:w1` |
| `epoka` | `rzym` | `ex:w1 bpc:epoka ex:epoka_rzym` |
| `linia` | `linia_a` | `ex:w1 bpc:linia "linia_a"` |
| `od` | `0050-03-01` | `ex:w1 bpc:od "0050-03-01"^^xsd:date` |
| `do` | `0050-03-10` | `ex:w1 bpc:do "0050-03-10"^^xsd:date` |

Adresy powstają z `iri_for`: `iri_for("rzym", "epoka")` daje `ex:epoka_rzym`, czyli [ten sam IRI, który ma epoka w swoim wierszu](03%20Model%20danych%20Biura.md#lm-14). Daty przechodzą przez `date_literal`. `linia` zostaje zwykłym napisem, [jak zapisano w uzasadnieniu tabeli](03%20Model%20danych%20Biura.md#lm-16).

Kolumna `linia` wybiera też graf nazwany, w którym leżą wszystkie te trójki. Zapisane w TriG wygląda to tak:

```turtle
ex:linia_a {
  ex:p1 bpc:odwiedzil ex:w1 .
  ex:w1 a bpc:Wizyta ;
    bpc:epoka ex:epoka_rzym ;
    bpc:linia "linia_a" ;
    bpc:od "0050-03-01"^^xsd:date ;
    bpc:do "0050-03-10"^^xsd:date .
}
```

Sześć komórek dało tu sześć trójek, ale nie dlatego, że mapowanie jest 1:1: `id` daje dwie, a inne kolumny po jednej, więc liczba zależy od wierszy tabeli mapowania. <a id="lm-21"></a>Gdyby `do` było puste, w bloku zabrakłoby ostatniej linii i nic więcej by się nie zmieniło. [Metadane o samym przebiegu konwersji trafią do grafu provenance](#ref-58), a [zapis całości w kodzie pokażemy przy budowaniu datasetu w rdflib](#ref-59).

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-konwersja-csv-do-trig)_

## Konwersja CSV w PROV-O

Wiersz wizyty ma już swoje trójki, ale nie mówi, skąd się wzięły. Na to odpowiada PROV-O, czyli słownik W3C do opisu pochodzenia danych: kto, z czego i kiedy je wytworzył. <a id="ref-21"></a>Konwersję opisujesz jako `prov:Activity`, jej wykonawcę jako `prov:Agent`, a wygenerowane dane jako `prov:Entity`. <a id="ref-26"></a>Całość trafia do osobnego grafu `ex:provenance`, żeby nie mieszać metadanych z faktami o wizytach.

Cztery własności łączą te elementy. `prov:used` wskazuje wejście konwersji, `prov:wasGeneratedBy` łączy wynik z aktywnością, `prov:wasAssociatedWith` wskazuje agenta, a `prov:startedAtTime` i `prov:endedAtTime` zapisują czas przebiegu. Pełne URI to przestrzeń `http://www.w3.org/ns/prov#` plus nazwa, np. `prov:used` to `http://www.w3.org/ns/prov#used`.

`ex:wizyty_csv` to IRI opisujące plik `wizyty.csv`, czyli wejście konwersji. Wynikiem są grafy `ex:linia_a` i `ex:linia_b`: każdy jest tu encją, więc każdy dostaje własny opis. IRI aktywności budujesz stałą funkcją `iri_for` z nazwy przebiegu, a nie z losowego id, więc ten sam przebieg ma ten sam adres.

```turtle
ex:provenance {
  ex:konwersja_wizyty a prov:Activity ;
    prov:used ex:wizyty_csv ;
    prov:wasAssociatedWith ex:konwerter ;
    prov:startedAtTime "2026-09-26T10:00:00Z"^^xsd:dateTime ;
    prov:endedAtTime "2026-09-26T10:00:05Z"^^xsd:dateTime .
  ex:konwerter a prov:SoftwareAgent .
  ex:wizyty_csv a prov:Entity .
  ex:linia_a a prov:Entity ; prov:wasGeneratedBy ex:konwersja_wizyty ;
    prov:wasDerivedFrom ex:wizyty_csv .
  ex:linia_b a prov:Entity ; prov:wasGeneratedBy ex:konwersja_wizyty ;
    prov:wasDerivedFrom ex:wizyty_csv .
}
```

Skutek jest praktyczny: gdy raport agenta przeczy danym, zapytanie do `ex:provenance` wskaże, który przebieg i który agent wytworzył sporną linię. <a id="ref-58"></a>Czas przebiegu zmienia się między uruchomieniami, więc jego wpływ na powtarzalność pliku [omówimy przy identycznym wyniku dwóch przebiegów](#ref-62).

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-konwersja-csv-do-trig)_

> **Pułapka: IRI grafu jako encja PROV nie jest z nim powiązane.** `ex:linia_a` jest nazwą grafu z danymi i jednocześnie podmiotem opisu `prov:Entity` w `ex:provenance`. Fuseki nie łączy tych ról: opis to zwykłe trójki o IRI. Zastąpienie albo usunięcie grafu `ex:linia_a` nie zmieni `prov:wasGeneratedBy` ani `prov:wasDerivedFrom`, więc pochodzenie może opisywać dane, których już nie ma. Zapytanie o pochodzenie nie sięgnie też do zawartości grafu bez osobnego `GRAPH ex:linia_a`.

## Dataset rdflib i zapis TriG

Zanim cokolwiek zamienisz w trójki w Pythonie, potrzebujesz izolowanego środowiska z biblioteką rdflib. Trójki dodajesz do obiektu `Dataset`, w grafie nazwanym wybranym przez `ds.graph(iri)`, a <a id="ref-59"></a>cały dataset zapisujesz jednym `serialize` w formacie `trig`.

Środowisko tworzysz w katalogu projektu:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install "rdflib>=7,<8"
```

rdflib to biblioteka Pythona do budowania i zapisu grafów RDF. Jej `Dataset` to odpowiednik datasetu Fuseki: graf domyślny plus grafy nazwane. Metoda `ds.graph(EX.linia_a)` zwraca graf o tym IRI (tworzy go, jeśli go brak), a `add` przyjmuje krotkę podmiot, orzeczenie, dopełnienie.

```python
from rdflib import Dataset, Namespace

EX = Namespace("http://example.org/id/")
BPC = Namespace("http://example.org/bpc#")

ds = Dataset()
ds.bind("ex", EX)
ds.bind("bpc", BPC)
g = ds.graph(EX.linia_a)
g.add((EX.p1, BPC.odwiedzil, EX.w1))
ds.serialize("biuro.trig", format="trig")
print(len(g))
```

```text
1
```

Plik `biuro.trig` zawiera blok `ex:linia_a { ex:p1 bpc:odwiedzil ex:w1 . }`, czyli dokładnie [ten zapis grafu linii czasu, który znasz z TriG](00%20Glosariusz.md#trig). `bind` wiąże prefiksy, żeby wynik był czytelny zamiast pełnych IRI.

Pamiętaj o dwóch rzeczach: trójkę dodaj do grafu `g`, a nie do `ds`, bo `ds.add` trafiłoby do grafu domyślnego. I aktywuj `.venv` w każdym nowym terminalu.

_Wersje: rdflib 7.x, Python 3.12 · [źródła: 3](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-konwersja-csv-do-trig)_

## Identyczny TriG w dwóch przebiegach

Dwa przebiegi dają ten sam plik, gdy wynik zależy wyłącznie od danych wejściowych: adresy budujesz funkcją deterministyczną, wiersze i grafy dodajesz w stałej kolejności, a nic w wyniku nie pochodzi z losowości ani zegara.

Adresy zapewnia `iri_for`: `strip`, NFC i `quote` z `safe=""` dają z tego samego klucza ten sam [IRI](00%20Glosariusz.md#iri), [zgodnie z sekcją o kluczach ze spacją i polskimi znakami](03%20Model%20danych%20Biura.md#znaki-specjalne-w-kluczach-iri). Numer wiersza ani losowe id się tu nie nadają.

Kolejność zapewnia sortowanie. Czytasz wiersze przez `sorted(..., key=...)` po `id`, a graf `ex:provenance` tworzysz przed grafami linii. Serializer sam porządkuje trójki wewnątrz grafu.

Trzecie źródło różnic to [węzeł pusty](00%20Glosariusz.md#węzeł-pusty), czyli zasób bez IRI, zapisywany jako `[ ... ]`. <a id="lm-24"></a>rdflib nadaje mu przy każdym przebiegu nowy, losowy identyfikator, więc plik różni się przy każdym zapisie. Dlatego konwerter zamienia `time:hasBeginning [ ... ]` z epoki na zasób z IRI, np. `ex:epoka_rzym_poczatek`. To zabieg konwertera, model się nie zmienia.

Czwarte to czas. <a id="ref-62"></a>[Moment konwersji w `prov:startedAtTime`](#konwersja-csv-w-prov-o) nie może pochodzić z `datetime.now()`. Przekazujesz go jako parametr, a zwykły przebieg używa wartości stałej.

```python
def convert(src, dst, started="2026-09-26T10:00:00Z"):
    ds = Dataset()
    prov = ds.graph(URIRef(EX + "provenance"))
    ...
    rows = sorted(rows, key=lambda r: r["id"])
```

<a id="ref-49"></a>Dopiero to pozwala porównywać wyniki dwóch przebiegów: różnica bajtów oznacza wtedy zmianę danych albo kodu, a nie szum.

_Wersje: rdflib 7.x · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-konwersja-csv-do-trig)_

## Walidacja wynikowego grafu

<a id="ref-18"></a>Wynikowy graf sprawdzasz funkcją `validate`, która wczytuje plik TriG i zwraca dwie listy: `errors` (blokują wgranie) i `warnings` (nie blokują). Każdy z trzech problemów wykrywasz innym przeglądem grafu i każdy traktujesz inaczej.

W RDF nie ma unikalności klucza: dwa wiersze z tym samym `id` dają ten sam IRI, więc się zlewają. Duplikat widać dopiero jako podmiot z dwiema różnymi wartościami własności, która powinna mieć jedną, np. dwa `bpc:od` u jednej wizyty.

Klucz obcy bez rekordu to obiekt, który nie ma własnego `rdf:type`. Ta własność przypisuje zasób do klasy: `ex:w1 rdf:type bpc:Wizyta` odpowiada wierszowi w tabeli wizyt, więc brak takiej trójki oznacza brak wiersza.

Zły typ to [literał](00%20Glosariusz.md#literał), którego [typ danych](00%20Glosariusz.md#typ-danych) nie jest `xsd:date`, czyli typem XSD dla dat, np. `"2020-01-05"^^xsd:date`.

```python
def validate(path):
    ds = Dataset(default_union=True)
    ds.parse(path, format="trig")
    errors, warnings = [], []
    for s in set(ds.subjects(BPC.od)):
        if len(set(ds.objects(s, BPC.od))) > 1:
            errors.append(f"duplikat klucza: {s}")
    for s, o in ds.subject_objects(BPC.naWizycie):
        if (o, RDF.type, BPC.Wizyta) not in ds:
            warnings.append(f"klucz obcy bez rekordu: {s} -> {o}")
    for s, o in ds.subject_objects(BPC.od):
        if getattr(o, "datatype", None) != XSD.date:
            errors.append(f"zły typ: {s} bpc:od {o!r}")
    return errors, warnings
```

Ustawienie `default_union=True` pozwala szukać we wszystkich grafach naraz, bo wizyta może leżeć w innym grafie niż spotkanie.

| Problem | Lista | Reakcja |
|---|---|---|
| duplikat z różnymi wartościami | errors | nie ładujesz pliku, poprawiasz CSV |
| klucz obcy bez rekordu | warnings | trójka zostaje: to dane, które analizy mają pokazać |
| zły typ | errors | wiersz odrzuć już przy konwersji, [jak w sekcji o pustej komórce i złej dacie](03%20Model%20danych%20Biura.md#pusta-komórka-i-zła-data) |

Raport walidacji to te dwie listy. <a id="ref-51"></a>Zgodę na wgranie daje pusta lista `errors`; ostrzeżenia tylko zapisujesz w raporcie. Odróżnienie braku od błędu w samych danych omówimy [przy analizie spotkań bez wizyty](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#ref-70).

_Wersje: rdflib 7.x · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-konwersja-csv-do-trig)_

## Od CSV do zwalidowanego TriG

Dojdziesz jednym przebiegiem: <a id="ref-136"></a>`convert` czyta CSV i zapisuje TriG z provenance, a [`validate` sprawdza zapisany plik](#walidacja-wynikowego-grafu). [Powtórzenie z tymi samymi plikami i tym samym `started` daje bajt w bajt ten sam plik](#identyczny-trig-w-dwóch-przebiegach). <a id="ref-5"></a>Tak spełnia się obietnica, że dane trafią do grafu: IRI, mapowanie i konwerter składają się w jeden ciąg.

```text
dane/*.csv -> convert(started) -> biuro.trig -> validate -> errors puste? -> wgranie
                    |                               |
           graf ex:provenance               raport: errors, warnings
```

`convert` buduje `Dataset`, dla każdego wiersza stosuje [tabelę mapowania](00%20Glosariusz.md#tabela-mapowania) i tworzy adresy funkcją `iri_for`. [Opis konwersji (aktywność, agent, wejście CSV, wyniki)](#konwersja-csv-w-prov-o) trafia do grafu `ex:provenance`, czyli provenance. Jedynym czasem w pliku jest `started`, który wywołujący przekazuje jako parametr; zegar systemowy nie jest czytany.

### Co czyni wynik identycznym

Sam `sha256sum` zadziała tylko wtedy, gdy serializacja jest stała, a rdflib tego nie gwarantuje samo z siebie. Dlatego:

- pliki i wiersze przetwarzasz w ustalonej kolejności (`sorted`), a grafy linii tworzysz po posortowanych nazwach;
- nie używasz węzłów pustych: aktywność ma stały IRI `ex:konwersja_wizyty`, a nie losowy identyfikator;
- czas przychodzi z argumentu `--started`, a `prov:endedAtTime` liczysz z niego, np. plus 5 s.

Kanonizacja (`to_canonical_graph`) jest potrzebna dopiero przy węzłach pustych; tu ich nie ma, więc porównujesz skróty pliku.

```bash
python konwerter.py --started 2026-09-26T10:00:00Z && sha256sum biuro.trig
python konwerter.py --started 2026-09-26T10:00:00Z && sha256sum biuro.trig
```

<a id="lm-26"></a>Oba skróty muszą być równe. Jeśli się różnią, szukaj węzła pustego, nieposortowanej pętli albo czasu z zegara, a nie zmian w danych. Zmiana `started` zmieni plik, i słusznie.

Zgodę na wgranie daje pusty `errors`. Samo wgranie opisuje następna sekcja.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-konwersja-csv-do-trig)_

> **Pułapka: Stały IRI aktywności łączy różne konwersje.** Deterministyczny IRI aktywności jest ten sam w każdym przebiegu. Po wgraniu wyników dwóch konwersji z różnym `started` (POST dokłada) aktywność dostanie dwa `prov:startedAtTime` i dwa `prov:endedAtTime`, a wpisy prowokujące się mieszają. Uwzględnij `started` w IRI aktywności albo zastępuj graf `ex:provenance` przy wgraniu.

## Wgranie TriG z nazwami grafów

Masz zwalidowany `biuro.trig` i pusty dataset `biuro`, więc czas je połączyć. <a id="ref-7"></a><a id="ref-77"></a>Grafy nazwane zachowają nazwy, gdy wgrasz plik jako TriG i nie wskażesz grafu docelowego: nazwy biorą się wtedy z bloków `ex:linia_a { ... }` w pliku.

### Najpierw panel

Otwórz `http://localhost:3030`, wybierz dataset `biuro`, zakładkę *upload files*. Wskaż `biuro.trig`, pole nazwy grafu docelowego zostaw puste i kliknij *upload all*. <a id="lm-27"></a>Wpisana tam nazwa kazałaby serwerowi zapisać wszystko do jednego grafu, a podział na linie by przepadł.

### Potem HTTP

Panel robi to samo, co endpoint `/biuro/data`, czyli [Graph Store Protocol](00%20Glosariusz.md#graph-store-protocol). <a id="ref-16"></a>Wysyłasz POST z typem `application/trig` i **bez** parametru `?graph=`. Ten parametr działa jak nazwa docelowa z panelu: wskazuje jeden graf.

```python
def load_trig(path, endpoint="http://localhost:3030/biuro/data"):
    with open(path, "rb") as f:
        body = f.read()
    req = urllib.request.Request(
        endpoint, data=body, method="POST",
        headers={"Content-Type": "application/trig"})
    with urllib.request.urlopen(req) as resp:
        return resp.status, resp.read().decode()
```

Fuseki odpowiada kodem 200 i JSON-em z liczbą wczytanych trójek i czwórek. Wywołuj `load_trig` dopiero przy pustym `errors` z `validate`. Ponowne wgranie tego samego pliku nie dubluje trójek, bo zbiór trójek w grafie nie ma powtórzeń.

Że grafy trafiły pod właściwe nazwy, potwierdzą zapytania o liczby trójek w każdym grafie; opiszemy je przy sprawdzaniu załadowanych danych.

_Wersje: Apache Jena Fuseki 5.x · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-konwersja-csv-do-trig)_

## Kolejność przygotowania środowiska

Przygotuj to w kolejności: serwer, dataset, środowisko Pythona. Każdy etap sprawdź, zanim zaczniesz następny, bo błąd z niższego etapu objawia się na wyższym jako mylący komunikat.

Weźmy `load_trig`, który kończy się kodem 404. Wygląda to na błąd pliku `biuro.trig`, a przyczyną bywa brak datasetu `biuro`, więc endpoint `/biuro/data` po prostu nie istnieje. Gdy Fuseki nie wystartował, bo `java -version` pokazuje wersję starszą niż 17, Python zgłosi tylko odmowę połączenia, a problem leży zupełnie gdzie indziej.

```text
Java 17 -> ./fuseki-server -> /$/ping -> dataset biuro -> venv + rdflib -> validate -> load_trig
  java      log, port 3030     200      /biuro/query     import rdflib     errors=[]  200 + JSON
```

### Serwer

Zacznij od `java -version`: ma pokazać 17. Uruchom `./fuseki-server` i sprawdź log oraz odpowiedź 200 z `/$/ping`. Bez tego dalsze kroki nie mają sensu.

### Dataset

Utwórz `biuro` jako TDB2 w panelu i sprawdź, czy dataset ma trzy endpointy: `/biuro/query`, `/biuro/update` i `/biuro/data`. Zapytanie o zawartość powinno zwrócić zero trójek, bo dataset jest pusty.

### Python

Załóż venv, zainstaluj rdflib 7.x i sprawdź `import rdflib`. Uruchom konwerter dwa razy i [porównaj sha256 plików](#lm-26), potem `validate`. [Dopiero przy pustym `errors` wywołaj `load_trig`](#walidacja-wynikowego-grafu).

Kolejność wynika z zależności: konwerter nie potrzebuje serwera, ale wgranie potrzebuje serwera i datasetu. Dlatego te dwa etapy sprawdzasz pierwsze, a 404 albo odmowę połączenia przypiszesz od razu do właściwego etapu, nie do pliku. Same konwersja i walidacja działają też przy wyłączonym Fuseki.

## Stabilny zapis pliku TriG

Skoro konwerter CSV→TriG jest skryptem Pythona, zostaje pytanie, czy jego wynik zależy wyłącznie od danych. Dwa przebiegi dają identyczny plik, gdy o każdym bajcie decydują dane i kod, a nie środowisko uruchomienia. Dane wejściowe już ustaliliśmy: IRI z funkcji, sortowanie, brak węzłów pustych (bo rdflib [nadaje im losowe identyfikatory](#lm-24)) i czas jako parametr. Tu domykamy drugą stronę: sam zapis.

Skrypt nie może polegać na niczym, co zmienia się między uruchomieniami procesu:

- **Kolejność w serializatorze.** rdflib trzyma trójki w zbiorach, a ich kolejność może zależeć od haszy napisów, które Python losuje przy każdym starcie (`PYTHONHASHSEED`). Nie zakładaj, że serializator TriG wszystko posortuje: sprawdzaj wynik.
- **Prefiksy.** Zwiąż je jawnie przez `ds.bind`, bo nazwy nadane automatycznie (`ns1:`) mogą zależeć od kolejności napotkania.
- **Kodowanie.** Zapisuj zawsze w UTF-8, żeby wynik nie zależał od ustawień systemu.
- **Literały.** [`date_literal` zwraca postać kanoniczną](03%20Model%20danych%20Biura.md#pusta-komórka-i-zła-data): `20260508` (Python 3.11+) i `2026-05-08` dają ten sam literał. Data w złym formacie, np. `2026-5-8`, nie jest cicho poprawiana, tylko kończy się błędem `ValueError`. Napisy normalizuj do NFC, [tak jak w `iri_for`](03%20Model%20danych%20Biura.md#znaki-specjalne-w-kluczach-iri).

```python
ds = Dataset()
ds.bind("bpc", BPC)
ds.bind("ex", EX)
ds.bind("prov", PROV)
...
ds.serialize("biuro.trig", format="trig", encoding="utf-8")
```

Dowód uruchom w osobnych procesach z różnym ziarnem haszy:

```bash
PYTHONHASHSEED=1 python konwerter.py && sha256sum biuro.trig
PYTHONHASHSEED=2 python konwerter.py && sha256sum biuro.trig
```

Skróty muszą być równe, tak jak [dwa równe skróty](#lm-26) wcześniej. Jeśli się różnią, szukaj miejsca zależnego od kolejności w zbiorze, np. własnego `set` albo pominiętego sortowania. Wtedy różnica bajtów oznacza zmianę danych lub kodu, a nie przypadek serializatora.

_Wersje: rdflib 7.x, Python 3.12_

## Co zapamiętać

- Liczbę trójek z wiersza CSV wyznacza tabela mapowania, a nie liczba komórek: `id` daje dwie trójki, pusta komórka żadnej, a kolumna `linia` wybiera graf.
- Konwersja to prov:Activity z agentem, wejściem wizyty.csv i wynikami ex:linia_a oraz ex:linia_b, opisana w osobnym grafie ex:provenance.
- W venv z rdflib 7.x trójki dodajesz do grafu zwróconego przez `ds.graph(iri)`, a `ds.serialize(..., format="trig")` zapisuje cały dataset z nazwami grafów.
- Identyczny TriG dają: IRI z deterministycznej funkcji, stała kolejność wierszy i grafów, brak węzłów pustych oraz czas przekazany jako parametr.
- validate zwraca błędy blokujące (duplikat klucza, zły typ) i ostrzeżenia (klucz obcy bez rekordu); wgranie blokują tylko błędy.
- Identyczny TriG wymaga sortowania, braku węzłów pustych i czasu podanego jako parametr; wtedy dwa przebiegi mają ten sam sha256, a wgranie dopuszcza dopiero pusty errors.
- TriG zachowa nazwy grafów, gdy wgrasz go bez grafu docelowego: w panelu z pustym polem nazwy, przez HTTP bez ?graph=, z typem application/trig.
- Sprawdzaj etapy od najniższego: serwer, dataset, Python, bo brak datasetu (404) lub zła Java (odmowa połączenia) wyglądają przy wgraniu jak błąd pliku.
- Poza danymi ustabilizuj też zapis (jawne prefiksy, UTF-8, kanoniczne literały) i sprawdź równe sha256 przy różnym PYTHONHASHSEED.

## Pytania sprawdzające

### 21. Przeprowadź jeden wiersz wizyty przez mapowanie do pełnych trójek i zapisu TriG w grafie linii czasu.

<details>
<summary>Odpowiedź</summary>

Każda niepusta komórka wiersza przechodzi przez swój wiersz mapowania i daje trójkę; `id` daje dwie (adres i klasę wizyty), a `podroznik` trójkę łączącą podróżnika z wizytą. Adresy buduje `iri_for`, daty `date_literal`, a `linia` wybiera graf nazwany, w którym wszystkie trójki lądują w TriG. Pusta komórka oznacza brak odpowiedniej trójki.

Zobacz: [sekcja „Jeden wiersz wizyty do TriG”](#jeden-wiersz-wizyty-do-trig).

</details>

### 22. Jak opiszesz aktywność konwersji CSV, jej agenta i wygenerowane dane za pomocą PROV-O?

<details>
<summary>Odpowiedź</summary>

Konwersję opisujesz jako prov:Activity, konwerter jako prov:SoftwareAgent, a plik wejściowy i wygenerowane grafy linii jako prov:Entity. Łączą je prov:used, prov:wasAssociatedWith, prov:wasGeneratedBy i prov:wasDerivedFrom, a czas zapisują prov:startedAtTime i prov:endedAtTime. Całość leży w osobnym grafie ex:provenance.

Zobacz: [sekcja „Konwersja CSV w PROV-O”](#konwersja-csv-w-prov-o).

</details>

### 23. Jak w venv dodasz trójki do Dataset w grafie nazwanym i zapiszesz go jako TriG?

<details>
<summary>Odpowiedź</summary>

Tworzysz venv (`python3.12 -m venv .venv`), instalujesz rdflib 7.x, budujesz `Dataset`, bierzesz graf nazwany przez `ds.graph(iri)` i dodajesz do niego trójki metodą `add`. Całość zapisujesz przez `ds.serialize("biuro.trig", format="trig")`, co daje bloki `IRI { ... }` na każdy graf nazwany.

Zobacz: [sekcja „Dataset rdflib i zapis TriG”](#dataset-rdflib-i-zapis-trig).

</details>

### 24. Co sprawia, że dwa przebiegi konwersji dają identyczny plik TriG (kolejność, IRI, brak węzłów pustych)?

<details>
<summary>Odpowiedź</summary>

Plik jest identyczny, gdy wynik zależy tylko od danych i kodu. IRI powstają deterministyczną funkcją z klucza, wiersze i grafy są dodawane w stałej kolejności (sortowanie po id), w wyniku nie ma węzłów pustych, a czas konwersji w provenance jest parametrem, nie odczytem zegara. Uzupełnienie dotyczy samego zapisu: prefiksy wiąże się jawnie, kodowanie ustala na UTF-8, literały przechodzą przez kanoniczny date_literal (zła data to błąd, nie cicha poprawka), a nie polega się na kolejności zbiorów zależnej od PYTHONHASHSEED. Dowodem są równe sha256 z przebiegów z różnym ziarnem haszy; wtedy różnica bajtów oznacza zmianę danych lub kodu.

Zobacz: [sekcja „Identyczny TriG w dwóch przebiegach”](#identyczny-trig-w-dwóch-przebiegach), [sekcja „Stabilny zapis pliku TriG”](#stabilny-zapis-pliku-trig).

</details>

### 25. Jak wykryjesz duplikaty kluczy, klucze obce bez rekordu i złe typy w wynikowym grafie i co zrobisz z każdym?

<details>
<summary>Odpowiedź</summary>

Wynikowy TriG wczytujesz do datasetu i przeglądasz trzy rzeczy. Duplikat klucza to podmiot z dwiema różnymi wartościami własności jednowartościowej; jest błędem i blokuje wgranie. Klucz obcy bez rekordu to obiekt bez rdf:type; zostaje jako ostrzeżenie, bo analizy mają takie przypadki pokazać. Zły typ literału (inny niż xsd:date) to błąd, a wiersz odrzucasz już przy konwersji.

Zobacz: [sekcja „Walidacja wynikowego grafu”](#walidacja-wynikowego-grafu).

</details>

### 26. Jak od CSV dojdziesz do zwalidowanego TriG z provenance i jak powtórzysz przebieg z identycznym wynikiem?

<details>
<summary>Odpowiedź</summary>

Uruchamiasz convert na plikach CSV z jawnym czasem startu, co zapisuje TriG z grafem provenance, a potem validate na zapisanym pliku; wgranie dopuszcza pusta lista błędów. Powtórzenie daje identyczny plik, bo pliki, wiersze i grafy są sortowane, nie ma węzłów pustych, a czas jest parametrem, nie zegarem. Zgodność potwierdzasz porównaniem sha256 pliku z dwóch przebiegów.

Zobacz: [sekcja „Od CSV do zwalidowanego TriG”](#od-csv-do-zwalidowanego-trig).

</details>

### 27. Jak wgrasz TriG do datasetu (najpierw UI, potem HTTP) tak, by grafy nazwane zachowały nazwy?

<details>
<summary>Odpowiedź</summary>

W panelu Fuseki wybierasz dataset biuro, zakładkę upload files, wskazujesz biuro.trig i zostawiasz puste pole grafu docelowego. Przez HTTP wysyłasz POST na /biuro/data z Content-Type application/trig i bez parametru ?graph=. W obu przypadkach nazwy grafów biorą się z bloków w pliku; wskazanie grafu docelowego zapisałoby wszystko w jednym grafie.

Zobacz: [sekcja „Wgranie TriG z nazwami grafów”](#wgranie-trig-z-nazwami-grafów).

</details>

### 28. W jakiej kolejności przygotujesz serwer, dataset i środowisko Pythona i co sprawdzisz na każdym etapie?

<details>
<summary>Odpowiedź</summary>

Najpierw serwer (Java 17, log, 200 z /$/ping), potem dataset biuro (trzy endpointy i zero trójek), na końcu venv z rdflib, dwa przebiegi konwertera z równym sha256 i validate. Kolejność chroni przed mylącymi objawami: brak datasetu daje 404 przy wgraniu, które wygląda na błąd pliku, a zła Java kończy się odmową połączenia. Konwersja i walidacja nie potrzebują serwera, wgranie potrzebuje serwera i datasetu.

Zobacz: [sekcja „Kolejność przygotowania środowiska”](#kolejność-przygotowania-środowiska).

</details>
