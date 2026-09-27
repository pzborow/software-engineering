# Analizy paradoksów w SPARQL

W dziale 05 składałeś zapytania SELECT z osobnych klocków: filtrów, braków, grafów, agregacji i ścieżek. Tu użyjesz ich razem, by odpowiedzieć na sześć pytań Biura Paradoksów Czasowych, i zapiszesz każdą odpowiedź jako osobną analizę w queries/, wskazując, które z nich korzystają z [grafów nazwanych](00%20Glosariusz.md#graf-nazwany). Po lekturze odróżnisz w wynikach brak danych od błędu danych. Zapytania działają na TriG wgranym w dziale 04, zbudowanym według modelu z działu 03.

```text
TriG w Fuseki
  graf domyślny | graf linii A | graf linii B
        |
        | porównanie linii: graf A i graf B
        | pozostałe analizy: dane z jednego grafu
        v
  queries/ (6 analiz SPARQL)
        |
        v
  wyniki
```

**W tym dziale:**

- [Łańcuch spotkań między podróżnikami](#łańcuch-spotkań-między-podróżnikami)
- [Artefakt przed datą powstania](#artefakt-przed-datą-powstania)
- [Spotkanie bez wizyty i wizyta bez powiązania](#spotkanie-bez-wizyty-i-wizyta-bez-powiązania)
- [Wspólne i tylko w jednej linii](#wspólne-i-tylko-w-jednej-linii)
- [Raport sprzeczny z danymi wizyty](#raport-sprzeczny-z-danymi-wizyty)
- [Grafy nazwane czy jeden graf](#grafy-nazwane-czy-jeden-graf)

## Łańcuch spotkań między podróżnikami

Łańcuch spotkań łączący dwóch podróżników znajdziesz [ścieżką własności](00%20Glosariusz.md#ścieżka-własności) z `+`, która idzie od jednego do drugiego przez wizyty i spotkania. Ścieżka potwierdza tylko, że połączenie istnieje. Nie zwraca ogniw ani ich kolejności w czasie.

Podróżnik trafia do spotkania przez swoją wizytę, a ze spotkania do innego uczestnika. [To ta sama grupa kroków co w ścieżce po spotkaniach](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#lm-36). Zapis `analiza_2.rq` pyta o konkretną parę:

```sparql
ASK
FROM <urn:x-arq:UnionGraph>
{ ex:p1 (bpc:odwiedzil/^bpc:naWizycie/bpc:uczestnik)+ ex:p2 }
```

Wzorzec bez `GRAPH` jest dopasowywany do jednego aktywnego grafu. Wizyty `bpc:odwiedzil` leżą w grafach linii (`ex:linia_a`, `ex:linia_b`), a spotkania z `bpc:naWizycie` i `bpc:uczestnik` w [grafie domyślnym](00%20Glosariusz.md#graf-domyślny), jako fakty wspólne dla linii. `urn:x-arq:UnionGraph` to nazwa specjalna Fuseki: suma wszystkich grafów nazwanych. Klauzula `FROM` robi z niej jeden aktywny graf, więc ścieżka może przejść z wizyty do spotkania. Zamiast `ASK` możesz użyć `SELECT ?kto` z `ex:p1` po lewej stronie, ale dostaniesz tylko końce tras.

### Czego ścieżka nie powie

Ścieżka nie pamięta pośredników ani dat. Łańcuch p1 → A → p2 przejdzie także wtedy, gdy p1 spotkał A w 1200 roku, a A spotkał p2 w 300. Kolejność wyznaczają daty wizyt, a ścieżka ich nie porównuje.

<a id="ref-95"></a>Kolejność sprawdzisz zapytaniem o stałej długości, z jawnymi zmiennymi i [FILTER](00%20Glosariusz.md#filter):

```sparql
SELECT ?x ?d1 ?d2
FROM <urn:x-arq:UnionGraph>
WHERE {
  ?m1 bpc:uczestnik ex:p1, ?x ; bpc:naWizycie/bpc:od ?d1 .
  ?m2 bpc:uczestnik ?x, ex:p2 ; bpc:naWizycie/bpc:od ?d2 .
  FILTER (?x != ex:p1 && ?x != ex:p2 && ?d1 <= ?d2)
}
```

Ten wzorzec obejmuje jeden pośrednik. Dłuższe łańcuchy wymagają kolejnych bloków i nie da się ich zapisać jednym `+`.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-analizy-paradoksów-w-sparql)_

## Artefakt przed datą powstania

Artefakt przed własną datą powstania wykryjesz, łącząc go z wizytą i porównując `bpc:od` wizyty z `bpc:powstal` artefaktu w FILTER. Sprzeczne linie czasu wykryjesz [jak nakładające się wizyty z sekcji o dwóch liniach](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#nakładające-się-wizyty-w-dwóch-liniach): dwoma blokami `GRAPH`, tym razem ze wspólnym artefaktem zamiast podróżnika.

Kolumna `wizyta` z `artefakty.csv` daje własność `bpc:pojawilSie`. Zakładamy, że artefakt i jego data leżą w grafie domyślnym jako fakty wspólne, a daty wizyt w grafach nazwanych linii. Wzorzec poza `GRAPH` czyta graf domyślny, a nazwę linii dostajemy ze zmiennej `?g`:

```sparql
SELECT ?a ?powstal ?w ?g ?od WHERE {
  ?a bpc:powstal ?powstal ; bpc:pojawilSie ?w .
  GRAPH ?g { ?w bpc:od ?od }
  FILTER (?od < ?powstal)
}
```

Wiersz mówi, który artefakt, w której wizycie i w której linii pojawił się za wcześnie. Data równa `powstal` nie jest błędem, dlatego jest `<`, a nie `<=`.

### Dwie linie naraz

Ten sam artefakt w dwóch liniach jest podejrzany, gdy wizyty się nakładają. To kolejna analiza korzystająca z grafów nazwanych:

```sparql
SELECT ?a ?w1 ?w2 WHERE {
  ?a bpc:pojawilSie ?w1, ?w2 .
  GRAPH ex:linia_a { ?w1 bpc:od ?od1 ; bpc:do ?do1 }
  GRAPH ex:linia_b { ?w2 bpc:od ?od2 ; bpc:do ?do2 }
  FILTER (?od1 <= ?do2 && ?od2 <= ?do1)
}
```

Artefakt istnieje raz, więc dwa nakładające się miejsca to kandydat na paradoks, nie pewnik.

[Oba zapytania po cichu gubią wiersze bez `powstal`, `od` albo `do`](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#lm-29). [Ten sam skutek ma data bez `^^xsd:date`](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#lm-30). Pusty wynik znaczy więc „nic nie znaleziono w kompletnych danych".

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-analizy-paradoksów-w-sparql)_

## Spotkanie bez wizyty i wizyta bez powiązania

Braki znajdziesz przez [FILTER NOT EXISTS](00%20Glosariusz.md#filter-not-exists), a brak odróżnisz od błędu danych tym, czy klucz obcy w ogóle istnieje. <a id="ref-70"></a>Spotkanie bez `bpc:naWizycie` to **brak**: pusta komórka `wizyta` nie dała trójki. Spotkanie wskazujące IRI, pod którym nie ma opisanej wizyty, <a id="ref-89"></a>to **błąd danych**: klucz obcy prowadzi donikąd, zwykle przez literówkę.

Oba przypadki łapie jedno zapytanie z `UNION`. Każda gałąź `UNION` jest oceniana osobno, więc `?s a bpc:Spotkanie` trzeba związać w każdej z nich. Te zapytania nie potrzebują nazw linii, więc czytają sumę grafów przez `FROM <urn:x-arq:UnionGraph>`, [jak analiza łańcucha spotkań](#łańcuch-spotkań-między-podróżnikami). Nie łącz tego z `GRAPH ?g`: `FROM` podmienia zestaw danych i grafów nazwanych by wtedy nie było widać. Zakładamy, że spotkania i wizyty leżą w grafach linii; gdyby leżały w grafie domyślnym, pomiń `FROM`.

```sparql
SELECT ?s ?rodzaj
FROM <urn:x-arq:UnionGraph>
WHERE {
  { ?s a bpc:Spotkanie .
    FILTER NOT EXISTS { ?s bpc:naWizycie ?w }
    BIND("brak" AS ?rodzaj) }
  UNION
  { ?s a bpc:Spotkanie ; bpc:naWizycie ?w .
    FILTER NOT EXISTS { ?w a bpc:Wizyta }
    BIND("błąd danych" AS ?rodzaj) }
}
```

Etykieta `brak` bywa dopuszczalna, `błąd danych` wymaga poprawki źródła.

### Wizyta bez powiązania

Wizyta jest osierocona, gdy nic na nią nie wskazuje: ani spotkanie, ani raport, ani artefakt. Ścieżka alternatywna `|` skraca warunek:

```sparql
SELECT ?w
FROM <urn:x-arq:UnionGraph>
WHERE {
  ?w a bpc:Wizyta .
  FILTER NOT EXISTS { ?x bpc:naWizycie|bpc:opisuje|bpc:pojawilSie ?w }
}
```

<a id="ref-102"></a>[Wizyty bez daty końca, które odpadały z analiz](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#lm-29), szukaj tak samo: `?w a bpc:Wizyta . FILTER NOT EXISTS { ?w bpc:do ?d }`. Pusty wynik znaczy „nic nie znaleziono”, więc [najpierw sprawdź typy i daty](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#lm-31).

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-analizy-paradoksów-w-sparql)_

> **Pułapka: Wizyta bez typu wygląda jak błąd danych.** Gałąź „błąd danych” sprawdza `FILTER NOT EXISTS { ?w a bpc:Wizyta }`, więc wizyta opisana, ale bez `a bpc:Wizyta` (literówka w typie, inny prefiks), też zostanie oznaczona jako błąd danych. Skutek: fałszywe alarmy o „literówce w kluczu obcym”, choć błąd jest w typie. Sprawdzaj obie możliwości (brak jakichkolwiek trójek o `?w` vs brak typu).

## Wspólne i tylko w jednej linii

Zdarzenia dwóch linii porównasz jednym zapytaniem z trzema gałęziami `UNION`: wspólne to ta sama trójka w obu grafach, a „tylko w jednej” to trójka w jednym grafie i FILTER NOT EXISTS na drugim. Zdarzenie utożsamiasz tu po parze podróżnik + IRI wizyty.

Wspólne dają dwa bloki `GRAPH` z tymi samymi zmiennymi `?p` i `?w`, [tak jak w analizie nakładających się wizyt](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#nakładające-się-wizyty-w-dwóch-liniach), tylko że tam wspólny był sam podróżnik. Różnicę daje `FILTER NOT EXISTS` z drugim grafem w środku: `?p` i `?w` są już związane, więc filtr sprawdza dokładnie tę trójkę. Każdą gałąź `UNION` wiążesz osobno, więc [BIND](00%20Glosariusz.md#bind) stoi w każdej z nich. `BIND(wyrażenie AS ?zmienna)` przypisuje wartość nowej zmiennej, podobnie jak stała kolumna w SELECT; tu daje etykietę wiersza.

```sparql
SELECT ?rodzaj ?p ?w WHERE {
  { GRAPH ex:linia_a { ?p bpc:odwiedzil ?w }
    GRAPH ex:linia_b { ?p bpc:odwiedzil ?w }
    BIND("wspólne" AS ?rodzaj) }
  UNION
  { GRAPH ex:linia_a { ?p bpc:odwiedzil ?w }
    FILTER NOT EXISTS { GRAPH ex:linia_b { ?p bpc:odwiedzil ?w } }
    BIND("tylko A" AS ?rodzaj) }
  UNION
  { GRAPH ex:linia_b { ?p bpc:odwiedzil ?w }
    FILTER NOT EXISTS { GRAPH ex:linia_a { ?p bpc:odwiedzil ?w } }
    BIND("tylko B" AS ?rodzaj) }
}
ORDER BY ?rodzaj ?p ?w
```

Nie dodawaj `FROM <urn:x-arq:UnionGraph>`: <a id="lm-43"></a>suma grafów zatarłaby granicę między liniami i nic nie byłoby „tylko w jednej”.

### Pułapka: różne IRI tego samego zdarzenia

Porównanie działa, gdy obie linie używają tego samego IRI wizyty. Przy danych `ex:linia_a { ex:p1 bpc:odwiedzil ex:w1 }` i `ex:linia_b { ex:p1 bpc:odwiedzil ex:w2 }` wyjdą dwa wiersze: „tylko A” dla `ex:w1` i „tylko B” dla `ex:w2`, nawet jeśli to jedno zdarzenie w dwóch wersjach. Wtedy porównuj po innym kluczu, np. podróżniku i epoce, zamiast po `?w`.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-analizy-paradoksów-w-sparql)_

## Raport sprzeczny z danymi wizyty

Raport jest sprzeczny z danymi, gdy jego `od` i `do` różnią się od dat wizyty wskazanej przez `bpc:opisuje`. [PROV-O](00%20Glosariusz.md#prov-o) (słownik pochodzenia danych, którym konwerter opisał swój przebieg w grafie `ex:provenance`) nie powie, kto ma rację, ale wskaże przebieg i plik, z którego wczytano wizytę.

Zakładam, że raporty leżą w grafie domyślnym, a wizyty w grafach linii. Wizytę czytasz przez `GRAPH ?g`, więc każda linia z rozbieżnymi datami daje osobny wiersz. Do tego wiersza dokładasz opis grafu `?g` z `ex:provenance`.

```sparql
SELECT ?r ?w ?g ?zrodlo ?akt ?rod ?od ?rdo ?do WHERE {
  ?r bpc:opisuje ?w ; bpc:od ?rod ; bpc:do ?rdo .
  GRAPH ?g { ?w bpc:od ?od ; bpc:do ?do }
  FILTER (?rod != ?od || ?rdo != ?do)
  GRAPH ex:provenance { ?g prov:wasDerivedFrom ?zrodlo ;
                           prov:wasGeneratedBy ?akt }
}
ORDER BY ?r ?g
```

Przykład: raport opisuje `ex:w1`, a wynik ma dwa wiersze, dla `ex:linia_a` i `ex:linia_b`, oba z `?zrodlo` = `ex:wizyty_csv` i `?akt` = `ex:konwersja_wizyty`. Obie kopie wizyty pochodzą więc z jednego pliku i jednego przebiegu, więc rozjazd nie wynika z pomyłki między liniami. Sprawdź wiersz `w1` w `wizyty.csv` i wiersz raportu w `raporty.csv`.

Wniosek jest ostrożny. Raport leży w grafie domyślnym bez opisu pochodzenia, więc PROV-O nie rozstrzygnie, czy zawinił raport. Jeśli obie linie mają te same daty, a różni się tylko raport, wizyta może być błędnie wczytana albo raport błędny. Dopiero porównanie z plikami to rozstrzyga.

Słabość znasz: [jak przy wizycie bez daty końca](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#lm-29), brak `do` nie daje trójki i wiersz po cichu odpada. Braki wyłap osobno przez `FILTER NOT EXISTS`.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-analizy-paradoksów-w-sparql)_

> **Pułapka: FILTER != na różnych typach daje błąd, nie true.** Jeśli `?rod` jest `xsd:string` albo `xsd:dateTime`, a `?od` to `xsd:date`, `!=` zgłasza błąd typu, a nie „różne”. Gdy druga strona `||` nie jest true, cały `FILTER` odrzuca wiersz, więc największe rozbieżności znikają po cichu. Porównuj po ujednoliceniu typów, np. `STR(?rod) != STR(?od)` albo `xsd:date(...)`, lub osobno wyłap pary o różnych `DATATYPE`.

## Grafy nazwane czy jeden graf

Cztery analizy czytają grafy nazwane osobno (1, 3, 5 i 6), a dwie widzą dane jako jeden graf (2 i 4). Wynik pierwszych czterech niesie ślad linii: zmienną `?g`, etykietę albo osobne kolumny. Wynik pozostałych dwóch nie wskaże linii.

| Analiza | Widok danych | Ślad grafu w wyniku |
|---|---|---|
| 1. nakładające się wizyty | `GRAPH ex:linia_a` i `GRAPH ex:linia_b` | kolumny `?w1`/`?od1` to linia A, `?w2`/`?od2` to linia B |
| 2. łańcuch spotkań | suma grafów | brak |
| 3. artefakt przed datą | wizyty przez `GRAPH ?g` | `?g` |
| 4. spotkanie bez wizyty | suma grafów | brak |
| 5. wspólne i tylko w jednej | bloki `GRAPH` | etykieta z `BIND` |
| 6. raport sprzeczny z wizytą | `GRAPH ?g` | `?g` |

Suma grafów to wirtualny graf, w którym Jena łączy graf domyślny ze wszystkimi grafami nazwanymi. Nie jest to osobna konfiguracja: zapytanie prosi o nią samo, klauzulą `FROM` z nazwą `urn:x-arq:UnionGraph`, [jak w analizie 2](#łańcuch-spotkań-między-podróżnikami):

```sparql
ASK
FROM <urn:x-arq:UnionGraph>
{ ex:p1 (bpc:odwiedzil/^bpc:naWizycie/bpc:uczestnik)+ ex:p2 }
```

Bez tej klauzuli wzorzec bez `GRAPH` widzi tylko graf domyślny, który nie zawiera wizyt z grafów linii. Suma jest tu celowa: łańcuch spotkań i klucz obcy nie zależą od linii. Za to [w analizach 3 i 5 zatarłaby granicę między liniami](#lm-43).

[Etykietę w analizie 5 daje `BIND`](#wspólne-i-tylko-w-jednej-linii) w gałęzi UNION, np. `BIND("tylko A" AS ?gdzie)`. Otwierając wynik, sprawdź najpierw, czy jest kolumna z grafem albo etykietą. <a id="lm-46"></a>Jeśli jej nie ma, analiza użyła sumy i o linii nie wnioskuj.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-analizy-paradoksów-w-sparql)_

> **Pułapka: UnionGraph to tylko grafy nazwane, tylko w TDB.** W Jena TDB/TDB2 `urn:x-arq:UnionGraph` łączy wyłącznie grafy nazwane; graf domyślny nie wchodzi do sumy, wbrew opisowi. Na zbiorze w pamięci `FROM` z tą nazwą jest traktowane jak zwykły URI do wczytania i nie daje sumy. Dane z grafu domyślnego trzeba dodać jawnie albo użyć `tdb:unionDefaultGraph`.

## Co zapamiętać

- Ścieżka z `+` potwierdza istnienie łańcucha spotkań, ale kolejność w czasie trzeba sprawdzić osobno, porównując daty wizyt.
- Artefakt przed datą powstania wykryjesz filtrem `?od < ?powstal`, a sprzeczne linie dwoma blokami GRAPH ze wspólnym artefaktem; brakujące lub źle otypowane daty po cichu gubią wiersze.
- Brak to nieobecna trójka klucza obcego, błąd danych to klucz wskazujący IRI bez opisu; odróżnisz je gałęziami UNION z FILTER NOT EXISTS, a ?s wiążesz w każdej gałęzi osobno.
- Wspólne i „tylko w jednej” zdarzenia dwóch linii dają trzy gałęzie UNION: dwa bloki GRAPH albo jeden GRAPH z FILTER NOT EXISTS na drugim, z BIND jako etykietą, przy tym samym IRI wizyty w obu liniach.
- Rozbieżność raportu z wizytą wykryjesz filtrem różnic dat, a PROV-O wskazuje plik i przebieg, z których pochodzi wizyta, ale nie rozstrzyga winy.
- Analizy 1, 3, 5 i 6 czytają grafy nazwane i zostawiają ślad linii w wyniku, a 2 i 4 czytają sumę grafów zamawianą przez FROM <urn:x-arq:UnionGraph> i śladu linii nie mają.

## Pytania sprawdzające

### 37. Jak zapytaniem znajdziesz łańcuch spotkań łączący dwóch podróżników i czego ścieżka nie powie o kolejności?

<details>
<summary>Odpowiedź</summary>

Łańcuch spotkań znajdziesz ścieżką własności z `+`, np. `ex:p1 (bpc:odwiedzil/^bpc:naWizycie/bpc:uczestnik)+ ex:p2`, w zapytaniu ASK na sumie grafów (UnionGraph). Ścieżka mówi tylko, że połączenie istnieje: nie zwraca pośredników ani dat, więc nie wskaże kolejności spotkań. Kolejność sprawdzisz zapytaniem o stałej długości, które porównuje daty wizyt filtrem.

Zobacz: [sekcja „Łańcuch spotkań między podróżnikami”](#łańcuch-spotkań-między-podróżnikami).

</details>

### 38. Jak wykryjesz artefakt pojawiający się przed datą powstania lub w sprzecznych liniach czasu?

<details>
<summary>Odpowiedź</summary>

Artefakt przed datą powstania znajdziesz, łącząc go przez bpc:pojawilSie z wizytą w grafie linii i filtrując wiersze, w których od wizyty jest wcześniejsze niż powstal. Sprzeczne linie czasu wykryjesz dwoma blokami GRAPH (ex:linia_a i ex:linia_b) ze wspólnym artefaktem i filtrem nakładania się przedziałów. Wynik to kandydaci, a wiersze z brakującą lub źle otypowaną datą po cichu odpadają.

Zobacz: [sekcja „Artefakt przed datą powstania”](#artefakt-przed-datą-powstania).

</details>

### 39. Jak zapytaniem znajdziesz spotkanie bez odpowiadającej wizyty lub wizytę bez powiązania i jak odróżnić brak od błędu danych?

<details>
<summary>Odpowiedź</summary>

Spotkanie bez wizyty znajdziesz przez FILTER NOT EXISTS na bpc:naWizycie, a wizytę bez powiązania przez NOT EXISTS na ścieżce bpc:naWizycie|bpc:opisuje|bpc:pojawilSie. Brak to nieobecna trójka (pusta komórka), a błąd danych to klucz obcy wskazujący IRI bez opisanej wizyty; drugą gałąź UNION łapie ten drugi przypadek. Zapytania czytają sumę grafów przez FROM z UnionGraph, bo nie potrzebują nazwy linii.

Zobacz: [sekcja „Spotkanie bez wizyty i wizyta bez powiązania”](#spotkanie-bez-wizyty-i-wizyta-bez-powiązania).

</details>

### 40. Jak porównasz zdarzenia dwóch linii czasu, wskazując wspólne i występujące tylko w jednej?

<details>
<summary>Odpowiedź</summary>

Użyj jednego zapytania z trzema gałęziami UNION: wspólne to ta sama trójka (podróżnik, wizyta) w obu grafach linii, a „tylko w jednej” to trójka w jednym grafie z FILTER NOT EXISTS na drugim. BIND w każdej gałęzi nadaje etykietę wiersza. Nie używaj sumy grafów, bo zatarłaby granicę między liniami. Porównanie zakłada to samo IRI wizyty w obu liniach.

Zobacz: [sekcja „Wspólne i tylko w jednej linii”](#wspólne-i-tylko-w-jednej-linii).

</details>

### 41. Jak wykryjesz raport agenta, który opisuje wizytę lub spotkanie sprzecznie z danymi, i jak PROV-O pomaga ustalić źródło?

<details>
<summary>Odpowiedź</summary>

Porównaj daty raportu (`bpc:opisuje`, `bpc:od`, `bpc:do`) z datami wizyty w każdym grafie linii i weź wiersze, w których się różnią. Do każdego wiersza dołącz z grafu `ex:provenance` `prov:wasDerivedFrom` i `prov:wasGeneratedBy` dla grafu z wizytą. Dostajesz plik i przebieg konwersji, z których wczytano wizytę, więc wiesz, gdzie szukać. PROV-O nie rozstrzyga jednak, kto się myli, bo raport nie ma tu własnej proweniencji.

Zobacz: [sekcja „Raport sprzeczny z danymi wizyty”](#raport-sprzeczny-z-danymi-wizyty).

</details>

### 42. Które z sześciu analiz użyją grafów nazwanych, a które danych z jednego grafu i jak je odróżnisz w wynikach?

<details>
<summary>Odpowiedź</summary>

Grafy nazwane czytają analizy 1, 3, 5 i 6, a sumę grafów (jeden widok całego datasetu) analizy 2 i 4. Sumę zapytanie zamawia klauzulą FROM z nazwą urn:x-arq:UnionGraph; graf domyślny sam wizyt z grafów linii nie zawiera. W wynikach analiz grafowych szukaj kolumny ?g, etykiety z BIND albo osobnych kolumn dla linii A i B; w analizach na sumie takiego śladu nie ma.

Zobacz: [sekcja „Grafy nazwane czy jeden graf”](#grafy-nazwane-czy-jeden-graf).

</details>
