# Serwer Fuseki i pytania Biura

Jena [Fuseki](00%20Glosariusz.md#fuseki) to serwer HTTP, który przechowuje dane jako proste fakty typu „Ala – pracuje w – Firma X” zamiast wierszy w tabelach, więc łatwo połączyć informacje z wielu źródeł i wychwycić sprzeczności, które w relacyjnej bazie giną między kluczami obcymi. W tym dziale uruchomisz serwer, zobaczysz na przykładowych tabelach, jakie pytania zadaje fikcyjne biuro analizujące dane, i przeniesiesz wiersze do modelu faktów; te trzy wątki spina jedna droga od tabeli do zapytań przez HTTP. Po tym dziale uruchomisz Fuseki na Javie 17, utworzysz w przeglądarce osobną bazę zapisywaną na dysku, która przetrwa restart serwera, i wskażesz adresy URL, pod którymi serwer przyjmuje odczyt, modyfikację i wgrywanie danych.

```text
tabele (wiersze) --> fakty: podmiot - relacja - wartość --> Fuseki (HTTP)
                                                        |-- odczyt
                                                        |-- modyfikacja
                                                        '-- wgrywanie
```

**W tym dziale:**

- [Start Fuseki na Javie 17](#start-fuseki-na-javie-17)
- [Pytania Biura o paradoksy](#pytania-biura-o-paradoksy)
- [Dataset biuro w przeglądarce](#dataset-biuro-w-przeglądarce)
- [Trójka, wiersz i prefiksy](#trójka-wiersz-i-prefiksy)
- [Ślady paradoksów w CSV](#ślady-paradoksów-w-csv)

## Start Fuseki na Javie 17

Fuseki uruchamiasz jednym poleceniem `fuseki-server` z rozpakowanej dystrybucji, a to, że działa pod właściwym portem, poznasz po linii `Started ... on port 3030` w logu i po odpowiedzi HTTP na `/$/ping`. Fuseki to serwer HTTP wystawiający dane przez [SPARQL](00%20Glosariusz.md#sparql), czyli język zapytań do grafów, którego użyjemy później. Dla czytelnika z backendu to odpowiednik uruchomienia serwera bazy: proces, port i endpoint sprawdzający żywotność.

Fuseki 5.x wymaga Javy 17 lub nowszej, więc najpierw sprawdź `java -version`. Potem pobierz archiwum `apache-jena-fuseki-5.x.y.tar.gz` ze strony projektu Apache Jena, rozpakuj je i uruchom serwer z jego katalogu:

<a id="lm-1"></a>

```bash
java -version                 # oczekiwane: 17.x
tar xzf apache-jena-fuseki-5.*.tar.gz
cd apache-jena-fuseki-5.*
./fuseki-server
# ... w logu: Start Fuseki (5.x.y)
# ... w logu: Started ... on port 3030
curl -i http://localhost:3030/$/ping
```

Domyślnie serwer słucha na porcie 3030 i startuje bez żadnego [datasetu](00%20Glosariusz.md#dataset). Log nie kłamie o porcie, ale dopiero `curl` potwierdza, że coś odpowiada na tym adresie. Kod 200 z `/$/ping` znaczy, że to żywy Fuseki. Znak `$` w URL-u jest częścią ścieżki administracyjnej, więc w powłoce zostaw go w adresie w pojedynczych cudzysłowach, jeśli powłoka próbuje go rozwinąć.

Zajęty port 3030 kończy się błędem `Address already in use`. Wtedy zatrzymaj drugi proces albo uruchom serwer z `--port=3031` i dalej używaj tego numeru. Otwórz też `http://localhost:3030/` w przeglądarce: zobaczysz panel administracyjny, w którym [w dalszych sekcjach powstanie dataset `/biuro`](#ref-2).

_Wersje: Apache Jena Fuseki 5.x, Java 17 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-serwer-fuseki-i-pytania-biura)_

## Pytania Biura o paradoksy

Skoro Fuseki już odpowiada, warto ustalić, czego będziemy się od niego domagać. Biuro Paradoksów Czasowych zadaje sześć pytań o sprzeczności w danych, a każde ma ślad w zwykłych tabelach CSV.

Każde pytanie [stanie się później osobnym zapytaniem](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#ref-4) SPARQL, czyli plikiem od `analiza_1.rq` do `analiza_6.rq`:

| # | Pytanie Biura | Gdzie widać ślad |
|---|---|---|
| 1 | Który podróżnik ma nakładające się wizyty w dwóch liniach czasu? | `w1` i `w2` |
| 2 | Jaki łańcuch spotkań łączy dwóch podróżników? | `s1`, `s2` |
| 3 | Który artefakt pojawia się przed datą powstania? | `a1` |
| 4 | Które spotkanie nie ma wizyty albo wizyta powiązania? | `s2` i brak `p3` w `wizyty.csv` |
| 5 | Co różni zdarzenia dwóch linii czasu? | `w1` tylko w `L1`, `w2` tylko w `L2` |
| 6 | Który raport agenta przeczy danym? | `r1` |

Oto fragmenty pliku `wizyty.csv` i pozostałych tabel:

```text
# wizyty.csv
id,podroznik,epoka,linia,od,do
w1,p1,rzym,L1,2024-05-01,2024-05-10
w2,p1,edo,L2,2024-05-05,2024-05-12
# artefakty.csv
id,nazwa,powstal,widziany_w
a1,Astrolabium,1450,rzym-100
# spotkania.csv
id,kto,z_kim,epoka
s1,p1,p2,rzym
s2,p2,p3,edo
# raporty.csv
r1,agent7,w1,p1 w rzymie 2024-05-20
```

Co pokazują te wiersze:

- **1:** <a id="lm-2"></a>`p1` jest 5–10 maja jednocześnie w Rzymie i w Edo.
- **2:** `s1` i `s2` tworzą łańcuch `p1`–`p2`–`p3`, którego żaden pojedynczy wiersz nie pokazuje.
- **3:** Astrolabium z 1450 roku widziano w Rzymie w roku 100.
- **4:** `s2` mówi, że `p3` był w Edo, ale `wizyty.csv` nie ma wizyty `p3`.
- **5:** Wizyty tego samego `p1` rozchodzą się: `w1` jest tylko w `L1`, a `w2` tylko w `L2`.
- **6:** Raport `r1` umieszcza `p1` w Rzymie 20 maja, choć `w1` kończy się 10 maja.

Żadna tabela nie wykryje tego sama: to relacje między wierszami, a nie błędy w pojedynczej kolumnie. Dlatego dane trafią do grafu.

## Dataset biuro w przeglądarce

Serwer działa, ale `./fuseki-server` wystartował bez datasetu, więc nie ma gdzie trzymać danych. Utworzymy dataset w panelu przeglądarki, a Fuseki sam dołoży do niego endpointy.

Dataset to w Fuseki kontener na grafy RDF, pod którym serwer wystawia usługi HTTP. Odpowiednik z SQL to baza danych, a nie tabela.

### Kroki w panelu

1. Otwórz `http://localhost:3030` i wybierz **Manage datasets**, potem **New dataset**.
2. <a id="ref-2"></a>W polu **Dataset name** wpisz `biuro`.
3. W **Dataset type** wybierz **Persistent (TDB2)**. Wariant *In-memory* znika po restarcie serwera.
4. Kliknij **Create dataset**. Na liście pojawi się `/biuro`.

TDB2 zapisuje dane na dysku, w katalogu `databases/biuro` obok `fuseki-server`, więc przetrwają restart.

### Endpointy datasetu

| Endpoint | URL | Do czego |
|---|---|---|
| query | `/biuro/query` | zapytania SPARQL (SELECT, ASK, CONSTRUCT) |
| update | `/biuro/update` | zmiany SPARQL Update (INSERT, DELETE) |
| data | `/biuro/data` | odczyt i wgrywanie całych grafów, bez SPARQL |

Endpoint `data` działa według [Graph Store Protocol](00%20Glosariusz.md#graph-store-protocol): zwykłe GET, PUT, POST i DELETE na grafie. [Graf nazwany](00%20Glosariusz.md#graf-nazwany) to osobny podgraf datasetu, wskazywany parametrem `?graph=`; bez niego operacja dotyczy grafu domyślnego.

```bash
curl -X POST http://localhost:3030/biuro/query \
  -H "Content-Type: application/sparql-query" \
  -d "ASK { ?s ?p ?o }"

curl -X POST "http://localhost:3030/biuro/data" \
  -H "Content-Type: text/turtle" \
  --data-binary @plik.ttl
```

Zapytanie idzie z typem `application/sparql-query`, a wgrywany plik z typem jego formatu. Pusty dataset odpowie na ASK `{"boolean":false}`. Wgrywanie TriG z grafami nazwanymi, zwykle na `/data`, [omówimy przy ładowaniu danych](04%20Konwersja%20CSV%20do%20TriG.md#ref-7).

_Wersje: Apache Jena Fuseki 5.x · [źródła: 3](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-serwer-fuseki-i-pytania-biura)_

> **Pułapka: POST na /data dokłada dane zamiast zastępować graf.** `POST` na `/biuro/data` dopisuje trójki do grafu domyślnego. Ponowne wgranie tego samego `plik.ttl` nie zdubluje identycznych trójek, ale zmienione lub usunięte w pliku trójki zostaną w grafie. Do podmiany całego grafu służy `PUT`, który usuwa jego dotychczasową zawartość, więc trzeba go użyć świadomie.

## Trójka, wiersz i prefiksy

[Dataset jest pusty](#dataset-biuro-w-przeglądarce), więc czas zobaczyć, co w nim zapiszemy. Podstawową jednostką danych w RDF jest [trójka](00%20Glosariusz.md#trójka): zdanie złożone z podmiotu (subject), orzeczenia (predicate) i dopełnienia (object).

Weźmy jeden wiersz z `wizyty.csv`, o kolumnach `id,podroznik,epoka,linia,od,do`. <a id="lm-4"></a>Podmiotem nie jest kolumna, tylko IRI zbudowany z wartości klucza `id`. Orzeczeniem jest własność odpowiadająca kolumnie, a dopełnieniem komórka. Odpowiednik z SQL: jedna komórka to jedna trójka, a wiersz to zbiór trójek o wspólnym podmiocie. Nie ma stałej listy kolumn, więc kolejny podmiot może mieć inne własności.

```text
w1,p1,rzym,linia_a,2024-05-05,2024-05-10
        ↓
ex:w1  a              bpc:Wizyta .
ex:p1  bpc:odwiedzil  ex:w1 .
```

Podróżnik `p1` z kolumny `podroznik` staje się osobnym zasobem, więc klucz obcy zamienia się w połączenie między podmiotami. [Pozostałe kolumny pokażemy przy literałach](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#ref-9), bo daty i napisy wymagają typów.

Podmiot i orzeczenie to [IRI](00%20Glosariusz.md#iri), czyli globalnie unikalny identyfikator zasobu, zapisywany w `<...>`. Dopełnieniem bywa IRI albo literał (zwykła wartość). Ponieważ IRI są długie, [prefiks](00%20Glosariusz.md#prefiks) skraca wspólny początek adresu: `bpc:odwiedzil` rozwija się do pełnego IRI. Prefiks to tylko zapis, w grafie siedzi pełne IRI.

Powyższe trójki w [Turtle](00%20Glosariusz.md#turtle), czytelnym zapisie tekstowym RDF:

```turtle
@prefix bpc: <http://example.org/bpc#> .
@prefix ex:  <http://example.org/biuro/> .

ex:p1 a bpc:Podroznik ;
      bpc:odwiedzil ex:w1 .
ex:w1 a bpc:Wizyta .
```

Średnik powtarza podmiot, kropka kończy zdanie, a `a` znaczy „jest typu”. Powstają trzy trójki.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-serwer-fuseki-i-pytania-biura)_

> **Pułapka: Prefiks @prefix nie łączy się z IRI automatycznie.** Prefiks to zwykłe doklejenie tekstu: `bpc:` kończy się na `#`, a `ex:` na `/`. Literówka albo brak końcowego separatora w `@prefix` daje inne IRI (np. `bpcodwiedzil`), więc dane po wczytaniu nie pasują do zapytań, a serwer nie zgłasza błędu. Trzeba pilnować identycznych deklaracji prefiksów w danych i zapytaniach.

## Ślady paradoksów w CSV

Skoro serwer i dataset działają, sprawdźmy, o co Biuro pyta i gdzie w tabelach widać pierwsze sprzeczności. Sześć pytań dotyczy relacji między wierszami wielu tabel, a nie błędów w jednej kolumnie.

| Nr | Pytanie Biura | Ślad w CSV |
|---|---|---|
| 1 | Czy podróżnik ma nakładające się wizyty w dwóch liniach czasu? | `w1` i `w2` p1 nakładają się 8–10 maja |
| 2 | Czy istnieje łańcuch spotkań między podróżnikami? | `s1` (p1, p2) i `s2` (p2, p3) dają łańcuch p1–p2–p3 |
| 3 | Czy artefakt pojawił się przed datą powstania? | `a1`: `powstal` późniejsze niż `od` wizyty `w1` |
| 4 | Czy jest spotkanie bez wizyty albo wizyta bez spotkania? | pusta komórka `wizyta` w `s2`; `w2` bez spotkania |
| 5 | Czym różnią się zdarzenia dwóch linii? | `w1` tylko w `linia_a`, `w2` tylko w `linia_b` |
| 6 | Czy raport przeczy danym wizyty? | `r1` ma inne `od`/`do` niż `w1` |

Przykładowe wiersze (skrócone, nie pełne pliki w `dane/`):

```text
wizyty.csv     w1,p1,rzym,a,0027-05-05,0027-05-10
               w2,p1,edo,b,0027-05-08,0027-05-12
podroznicy.csv p1,Ala   p3,Ola
epoki.csv      rzym,Rzym,0027-01-01,0476-09-04
artefakty.csv  a1,Amfora,0100-01-01,w1
spotkania.csv  s1,w1,p1,p2   s2,,p2,p3
raporty.csv    r1,agent7,w1,0027-05-06,0027-05-09
```

Tabele podróżników i epok nie są osobnym pytaniem, ale dają wspólne klucze: `p1`–`p3` łączą wizyty i spotkania, `epoka` wiąże wizytę z przedziałem czasu. Że `p3` nie ma żadnej wizyty, widać dopiero po zestawieniu z `spotkania.csv`.

Pytanie 4 ma dwa kierunki: spotkanie bez `wizyta` i wizyta bez spotkania. Pytanie 5 liczy się tylko przy tym samym IRI wizyty w obu grafach.

Każdy ślad to kandydat do sprawdzenia, nie werdykt.

## Co zapamiętać

- Fuseki 5.x na Javie 17 startuje poleceniem ./fuseki-server na porcie 3030, a jego działanie potwierdza log oraz odpowiedź 200 z /$/ping.
- Sześć pytań Biura dotyczy relacji między wierszami wielu tabel CSV, a nie błędów w pojedynczej kolumnie.
- Trwały dataset TDB2 o nazwie biuro tworzy się w panelu, a Fuseki wystawia dla niego endpointy query, update i data.
- Trójka to podmiot, orzeczenie i dopełnienie; wiersz tabeli to zbiór trójek o wspólnym podmiocie, a prefiks tylko skraca zapis IRI.
- Sześć pytań Biura dotyczy relacji między wierszami wielu tabel CSV, a ślady, np. nakładanie się wizyt 8–10 maja, to kandydaci do sprawdzenia.

## Pytania sprawdzające

### 1. Jak uruchomisz Fuseki na Javie 17 i po czym poznasz, że serwer działa pod właściwym portem?

<details>
<summary>Odpowiedź</summary>

Sprawdź `java -version` (ma być 17), rozpakuj dystrybucję Fuseki 5.x i uruchom `./fuseki-server`. Serwer domyślnie słucha na porcie 3030. Poznasz to po linii `Started ... on port 3030` w logu, po odpowiedzi 200 z `curl -i http://localhost:3030/$/ping` i po panelu pod `http://localhost:3030/` w przeglądarce.

Zobacz: [sekcja „Start Fuseki na Javie 17”](#start-fuseki-na-javie-17).

</details>

### 2. Jakie sześć pytań o paradoksy zadaje Biuro i jakie fragmenty tabel podróżników, wizyt, epok, artefaktów, spotkań i raportów już pokazują sprzeczności?

<details>
<summary>Odpowiedź</summary>

Biuro pyta o: nakładające się wizyty podróżnika w dwóch liniach czasu, łańcuch spotkań między podróżnikami, artefakt widziany przed datą powstania, spotkanie bez wizyty lub odwrotnie, różnice zdarzeń między liniami oraz raport przeczący danym wizyty. Ślady są już w CSV: wizyty w1 (5–10 maja) i w2 (8–12 maja) nakładają się 8–10 maja; s1 i s2 łączą p1–p2–p3; a1 ma powstal późniejsze niż początek wizyty w1; s2 nie ma wizyty, a p3 żadnej wizyty; w1 i w2 leżą w różnych liniach; r1 podaje inne daty niż w1. To kandydaci do sprawdzenia, nie werdykty.

Zobacz: [sekcja „Pytania Biura o paradoksy”](#pytania-biura-o-paradoksy), [sekcja „Ślady paradoksów w CSV”](#ślady-paradoksów-w-csv).

</details>

### 3. Jak w przeglądarce utworzyć trwały dataset i jakie endpointy (query, update, data) do niego przybywają?

<details>
<summary>Odpowiedź</summary>

Dataset tworzysz w panelu na http://localhost:3030: Manage datasets, New dataset, nazwa `biuro`, typ Persistent (TDB2), więc dane leżą na dysku. Fuseki dodaje wtedy trzy endpointy: `/biuro/query` (SPARQL do odczytu), `/biuro/update` (SPARQL Update) i `/biuro/data` (Graph Store Protocol, czyli całe grafy przez HTTP). Każdy woła się osobno, z właściwym Content-Type.

Zobacz: [sekcja „Dataset biuro w przeglądarce”](#dataset-biuro-w-przeglądarce).

</details>

### 4. Czym jest trójka subject-predicate-object, jak ma się do wiersza tabeli i po co są prefiksy?

<details>
<summary>Odpowiedź</summary>

Trójka to zdanie: podmiot, orzeczenie, dopełnienie. Wiersz tabeli odpowiada zbiorowi trójek o wspólnym podmiocie, a jedna komórka to jedna trójka; podmiotem jest IRI zbudowany z klucza, nie nazwa kolumny. Prefiksy skracają długie IRI w zapisie, ale w grafie zawsze jest pełne IRI.

Zobacz: [sekcja „Trójka, wiersz i prefiksy”](#trójka-wiersz-i-prefiksy).

</details>
