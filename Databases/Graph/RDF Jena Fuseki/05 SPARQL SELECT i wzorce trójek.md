# SPARQL SELECT i wzorce trójek

Dane z działu 04 są już w Fuseki, ale dopóki ich nie odpytasz, nie wiesz, czy załadowały się tak, jak zakładał model. Ten dział uczy pisać zapytania SELECT, które w SQL-owym duchu zwracają tabelę wyników, ale opisują wzorce w grafie, a nie łączenia tabel. Po nim sprawdzisz w Biurze Paradoksów Czasowych liczby [trójek](00%20Glosariusz.md#trójka), daty, braki, grafy i nakładające się wizyty podróżnika, a wynik potraktujesz jak test po wgraniu TriG.

```text
TriG (dział 04) -> Fuseki (grafy nazwane) -> zapytanie SELECT -> tabela wyników
                 \_________ sprawdzenie po załadowaniu _________/
```

**W tym dziale:**

- [Wizyty podróżnika w SELECT](#wizyty-podróżnika-w-select)
- [Daty w FILTER i literały o złym typie](#daty-w-filter-i-literały-o-złym-typie)
- [OPTIONAL a FILTER NOT EXISTS](#optional-a-filter-not-exists)
- [Zapytania w wybranym grafie](#zapytania-w-wybranym-grafie)
- [Zliczanie zdarzeń w grafach i HAVING](#zliczanie-zdarzeń-w-grafach-i-having)
- [Ścieżki o zmiennej długości](#ścieżki-o-zmiennej-długości)
- [Kontrola grafów po załadowaniu](#kontrola-grafów-po-załadowaniu)
- [Nakładające się wizyty w dwóch liniach](#nakładające-się-wizyty-w-dwóch-liniach)

## Wizyty podróżnika w SELECT

Dane są już w Fuseki, więc czas zadać im pytanie w [SPARQL](00%20Glosariusz.md#sparql), języku zapytań, którego użyjemy do wszystkich sześciu analiz Biura. <a id="ref-1"></a>Zapytanie SELECT to wzorzec trójek ze zmiennymi: silnik szuka wszystkich podstawień, dla których każda trójka wzorca istnieje w danych.

Zmienna zaczyna się od `?` i zastępuje dowolny element trójki. [Prefiksy](00%20Glosariusz.md#prefiks) deklarujesz słowem `PREFIX`, jak `@prefix` w Turtle, ale bez kropki na końcu. Gdy kilka trójek ma ten sam podmiot, średnik pozwala go nie powtarzać.

```sparql
PREFIX bpc: <http://example.org/bpc#>
PREFIX ex:  <http://example.org/id/>
SELECT ?wizyta ?od ?do
FROM <urn:x-arq:UnionGraph>
WHERE {
  ex:p1 bpc:odwiedzil ?wizyta .
  ?wizyta bpc:od ?od ;
          bpc:do ?do .
}
```

Wklej to w zakładce `query` datasetu `biuro`. Pierwsza trójka wiąże `?wizyta` z każdą wizytą `ex:p1`. Druga i trzecia mają wspólny podmiot `?wizyta`, więc wizyta musi mieć i `bpc:od`, i `bpc:do`. <a id="lm-29"></a>Wizyta bez daty końca odpada, bo [pusta komórka nie dała trójki](04%20Konwersja%20CSV%20do%20TriG.md#lm-21).

```text
--------------------------------------------------------------------------------------------------------------------------------------------------
| wizyta                     | od                                                    | do                                                    |
==================================================================================================================================================
| <http://example.org/id/w1> | "0027-03-01"^^<http://www.w3.org/2001/XMLSchema#date> | "0027-03-10"^^<http://www.w3.org/2001/XMLSchema#date> |
| <http://example.org/id/w2> | "0027-03-05"^^<http://www.w3.org/2001/XMLSchema#date> | "0027-03-12"^^<http://www.w3.org/2001/XMLSchema#date> |
--------------------------------------------------------------------------------------------------------------------------------------------------
```

Kolumna na zmienną, wiersz na podstawienie; połączenia wynikają z powtórzonych zmiennych, nie z `JOIN`. Wizyta to pełne IRI, a data to literał z typem `xsd:date`.

`FROM <urn:x-arq:UnionGraph>` jest potrzebne, bo [wizyty leżą w grafach linii](04%20Konwersja%20CSV%20do%20TriG.md#jeden-wiersz-wizyty-do-trig) (w1 w `ex:linia_a`, w2 w `ex:linia_b`). Bez niego zapytanie widzi tylko [graf domyślny](00%20Glosariusz.md#graf-domyślny), czyli [graf](00%20Glosariusz.md#graf-nazwany) bez nazwy, a tam wizyt nie ma. Ta nazwa łączy wszystkie grafy nazwane w jeden widok; [świadome wybieranie grafu omówimy osobno](#ref-84).

_Wersje: SPARQL 1.1 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-sparql-select-i-wzorce-trójek)_

> **Pułapka: Wzorzec trójek gubi wiersze z brakującą właściwością.** Wizyta bez `bpc:do` znika z wyniku bez żadnego ostrzeżenia, więc wizyta trwająca lub z niekompletnymi danymi wygląda, jakby nie istniała. Jeśli takie wiersze mają zostać, trzeba objąć `bpc:do` w `OPTIONAL`.

> **Pułapka: Union graph zwielokrotnia wiersze przy duplikatach.** Ta sama trójka zapisana w kilku grafach nazwanych w widoku `urn:x-arq:UnionGraph` jest zwracana jako jedno podstawienie, ale `SELECT` bez `DISTINCT` nie pokazuje, z którego grafu pochodzi. Przy różnych trójkach o tej samej wizycie wynik miesza dane z różnych linii bez śladu źródła.

## Daty w FILTER i literały o złym typie

<a id="ref-12"></a>Daty `xsd:date` porównujesz w [FILTER](00%20Glosariusz.md#filter), czyli warunku odrzucającym wiersze wyniku, zwykłymi operatorami `<`, `>=`, `=`, ale po obu stronach muszą stać daty z typem. Literał o innym typie nie powoduje komunikatu: porównanie kończy się [błędem typu](00%20Glosariusz.md#błąd-typu), a FILTER traktuje go jak fałsz i po cichu odrzuca wiersz.

Porównanie jest wartościowe, nie tekstowe: silnik zna typ `xsd:date`, więc porównuje daty kalendarzowe. Porównanie dat w filtrze wygląda tak:

```sparql
PREFIX bpc: <http://example.org/bpc#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
SELECT ?wizyta ?od
FROM <urn:x-arq:UnionGraph>
WHERE {
  ?wizyta bpc:od ?od .
  FILTER (?od >= "0027-03-03"^^xsd:date)
}
```

```text
--------------------------------------------------------------------------------------
| wizyta                     | od                                                    |
======================================================================================
| <http://example.org/id/w2> | "0027-03-05"^^<http://www.w3.org/2001/XMLSchema#date> |
--------------------------------------------------------------------------------------
```

Wraca tylko `w2`; `w1` zaczyna się 0027-03-01, czyli przed 0027-03-03, więc odpada zgodnie z warunkiem.

Pułapka tkwi w stałej. <a id="lm-30"></a>Zapis `"0027-03-03"` bez `^^xsd:date` to zwykły napis, więc `?od >= "0027-03-03"` daje błąd typu dla każdego wiersza i wynik jest pusty. Taki sam skutek ma zły typ w danych: napis `"0027-03-05"` zamiast daty albo literał ze złą składnią daty. Wiersz znika bez ostrzeżenia, [podobnie jak wizyta bez `bpc:do`](#lm-29).

Gdy wynik jest podejrzanie pusty, <a id="lm-31"></a>wypisz `?od` razem z `DATATYPE(?od)` bez filtra i sprawdź, czy wszędzie stoi `xsd:date`. Wykrywanie braków opiszemy przy `OPTIONAL` i `FILTER NOT EXISTS`.

_Wersje: SPARQL 1.1 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-sparql-select-i-wzorce-trójek)_

## OPTIONAL a FILTER NOT EXISTS

[OPTIONAL](00%20Glosariusz.md#optional) dołącza dane, jeśli istnieją, a wiersz bez nich zostawia w wyniku z pustą zmienną. [FILTER NOT EXISTS](00%20Glosariusz.md#filter-not-exists) odrzuca wiersze, dla których podany wzorzec ma dopasowanie, i niczego nie wiąże. <a id="ref-87"></a>Do szukania braków nadają się oba, ale dają je inaczej.

Przy `OPTIONAL` brak poznajesz po zmiennej niezwiązanej, czyli odpowiedniku NULL z LEFT JOIN. Funkcja `BOUND(?x)` zwraca prawdę, gdy zmienna ma w wierszu wartość, więc `!BOUND(?do)` zostawia wiersze bez dopasowania. Przy `FILTER NOT EXISTS` warunek jest jeden: nie istnieje trójka, której szukasz. Tak znajdziesz [wizytę bez daty końca](#lm-29), która przy zwykłym wzorcu `bpc:do` po cichu odpadała.

`FROM <urn:x-arq:UnionGraph>` to specjalna nazwa Fuseki oznaczająca sumę wszystkich grafów nazwanych, więc zapytanie widzi wizyty ze wszystkich linii naraz.

```sparql
# ... PREFIX bpc
SELECT ?wizyta FROM <urn:x-arq:UnionGraph> WHERE {
  ?wizyta a bpc:Wizyta .
  OPTIONAL { ?wizyta bpc:do ?do }
  FILTER (!BOUND(?do))
}
# to samo bez OPTIONAL:
SELECT ?wizyta FROM <urn:x-arq:UnionGraph> WHERE {
  ?wizyta a bpc:Wizyta .
  FILTER NOT EXISTS { ?wizyta bpc:do ?do }
}
```

Oba zapytania zwracają te same wizyty. Różnica ujawnia się, gdy chcesz coś więcej:

| | OPTIONAL | FILTER NOT EXISTS |
|---|---|---|
| Wiersz bez dopasowania | zostaje, zmienna pusta | zostaje |
| Wiersz z dopasowaniem | zostaje z wartością | odpada |
| Wiąże zmienne z wzorca | tak | nie |
| Szukanie braków | z `!BOUND` | wprost |

Użyj `OPTIONAL`, gdy chcesz pokazać wszystkie wizyty, a brak ma być pustą komórką. Użyj `FILTER NOT EXISTS`, gdy interesują cię tylko braki. Przy wizycie z kilkoma `bpc:do` `OPTIONAL` da kilka wierszy. [Odróżnianie braku od błędu danych pokażemy przy spotkaniach bez wizyty](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#ref-89).

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-sparql-select-i-wzorce-trójek)_

## Zapytania w wybranym grafie

<a id="ref-15"></a>Nazwę grafu nazwanego wiążesz ze zmienną wzorcem `GRAPH ?g { ... }`, a zapytanie zawężasz do jednego grafu przez `GRAPH <iri> { ... }` albo przez `FROM NAMED`. [Dotąd zapytania widziały tylko graf domyślny](#wizyty-podróżnika-w-select) albo, po `FROM <urn:x-arq:UnionGraph>`, sumę wszystkich grafów nazwanych. <a id="ref-84"></a>Teraz graf wybierasz jawnie.

`GRAPH ?g` przechodzi po grafach nazwanych datasetu, szuka wzorca wewnątrz bloku, a `?g` dostaje IRI grafu, w którym trójka leży. Wynik mówi więc, z której linii czasu pochodzi wiersz. Graf domyślny nie jest przez `GRAPH` przeglądany. Gdy zamiast zmiennej wpiszesz stałe IRI, np. `GRAPH ex:linia_a`, zapytanie widzi tylko ten graf.

`FROM NAMED <iri>` nie zmienia grafu domyślnego. Ogranicza zbiór grafów nazwanych, które `GRAPH ?g` w ogóle zobaczy, więc nadal potrzebujesz `GRAPH`. Zwykłe `FROM` robi co innego: ustawia graf domyślny i gubi informację o pochodzeniu trójki, więc `?g` nie da się wtedy związać.

```sparql
# ... PREFIX bpc, ex
SELECT ?g (COUNT(?w) AS ?n) WHERE {
  GRAPH ?g { ?w a bpc:Wizyta }
} GROUP BY ?g

# tylko linia A: FROM NAMED zawęża grafy dla GRAPH
SELECT ?g ?w FROM NAMED ex:linia_a WHERE {
  GRAPH ?g { ?w a bpc:Wizyta }
}
```

Pierwsze zapytanie zwraca jeden wiersz na graf nazwany z liczbą wizyt; grupowanie omówimy dokładniej przy zliczaniu zdarzeń w grafach. Drugie zwraca wizyty wyłącznie z `ex:linia_a`, a `?g` ma w każdym wierszu tę samą wartość. Gdy graf jest jeden i znany, prościej wpisać stałe IRI.

_Wersje: SPARQL 1.1 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-sparql-select-i-wzorce-trójek)_

> **Pułapka: FROM NAMED razem z FROM wyłącza graf domyślny.** Fuseki po wskazaniu w zapytaniu `FROM NAMED` buduje własny dataset z klauzul. Jeśli zapytanie nie ma `FROM`, graf domyślny jest wtedy pusty, więc wzorce poza `GRAPH` nic nie zwrócą, mimo że dane leżą w grafie domyślnym magazynu. Trzeba dodać `FROM` albo umieścić cały wzorzec w `GRAPH`.

## Zliczanie zdarzeń w grafach i HAVING

<a id="ref-91"></a>Zdarzenia w każdym grafie policzysz przez `GRAPH ?g { ... }`, `GROUP BY ?g` i `COUNT`. Grupy odfiltrujesz przez `HAVING`, który działa na wyniku agregacji, a nie na pojedynczych wierszach.

Wzorzec `GRAPH ?g` daje jeden wiersz na każdą wizytę razem z nazwą grafu. [`GROUP BY`](00%20Glosariusz.md#group-by) skleja te wiersze w grupy o tym samym `?g`, a [funkcja agregująca](00%20Glosariusz.md#funkcja-agregująca), np. `COUNT`, liczy elementy w każdej grupie. To odpowiednik `GROUP BY` z SQL, więc mechanizm już znasz. Wynik ma jeden wiersz na graf, [jak w zapytaniu z poprzedniej sekcji](#zapytania-w-wybranym-grafie).

Różnica między `FILTER` a `HAVING` jest ta sama co między `WHERE` i `HAVING` w SQL. [`FILTER` działa przed grupowaniem](00%20Glosariusz.md#filter) i wyrzuca wiersze. Warunku na `COUNT` nie da się w nim zapisać, bo liczba istnieje dopiero po zgrupowaniu. Robi to [`HAVING`](00%20Glosariusz.md#having): zostawia tylko te grupy, których wynik agregacji spełnia warunek.

Zwróć uwagę na `COUNT(DISTINCT ?w)`. Gdy wzorzec ma więcej dopasowań na wizytę, [np. przez `OPTIONAL`](00%20Glosariusz.md#optional), zwykły `COUNT` policzy wiersze, a nie wizyty.

```sparql
# ... PREFIX bpc, ex
SELECT ?g (COUNT(DISTINCT ?w) AS ?n) WHERE {
  GRAPH ?g { ?w a bpc:Wizyta }
}
GROUP BY ?g
HAVING (COUNT(DISTINCT ?w) > 1)
ORDER BY DESC(?n)
```

Graf z jedną wizytą znika z wyniku, a graf pusty w ogóle nie występuje, bo nie ma dla niego żadnego dopasowania. Wyniku `COUNT` nie możesz użyć w `HAVING` pod aliasem `?n`. W SPARQL 1.1 alias z `SELECT` jeszcze wtedy nie istnieje, więc powtórz wyrażenie.

_Wersje: SPARQL 1.1 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-sparql-select-i-wzorce-trójek)_

## Ścieżki o zmiennej długości

[Ścieżka własności](00%20Glosariusz.md#ścieżka-własności) to wyrażenie na miejscu orzeczenia, które opisuje trasę złożoną z wielu trójek. Operator `+` oznacza jeden krok lub więcej, `*` zero lub więcej, a `/` łączy kroki w ciąg. Dzięki temu jedno zapytanie znajduje połączenia o zmiennej długości, których nie zapiszesz stałą liczbą wzorców.

`/` ma stałą długość: `?s bpc:uczestnik/bpc:odwiedzil ?w` znaczy „uczestnik spotkania, a potem jego wizyta”. Powtarzać da się tylko trasę, która wraca do tego samego rodzaju węzła. W Biuru robi to grupa w nawiasie: podróżnik, jego wizyta, spotkanie na tej wizycie (krok wstecz, `^`), inny uczestnik.

<a id="lm-36"></a>

```sparql
# ... PREFIX bpc, ex
SELECT DISTINCT ?inny WHERE {
  GRAPH ?g {
    ex:p1 (bpc:odwiedzil/^bpc:naWizycie/bpc:uczestnik)+ ?inny
  }
}
```

Ścieżka `+` zwraca każdy osiągnięty węzeł raz, więc cykle nie zapętlają zapytania. Wśród wyników może być sam `ex:p1`, jeśli wraca przez własne spotkanie. `*` dodaje do wyniku także węzeł startowy, bo zero kroków to połączenie z samym sobą.

Ścieżka nie zwraca długości trasy ani pośrednich węzłów, tylko koniec. Wewnątrz `GRAPH ?g` cała trasa musi leżeć w jednym grafie linii czasu. [Kolejnością spotkań zajmiemy się przy łańcuchu spotkań](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#ref-95).

_Wersje: SPARQL 1.1 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-sparql-select-i-wzorce-trójek)_

## Kontrola grafów po załadowaniu

Po wgraniu TriG sprawdź trzy rzeczy: <a id="ref-79"></a>ile trójek leży w każdym grafie nazwanym, jakie typy tam są i czy każdy graf ma opis w `ex:provenance`. Pierwsze dwie to zwykłe zliczenia z [zliczania zdarzeń](#zliczanie-zdarzeń-w-grafach-i-having): funkcja agregująca `COUNT` z GROUP BY po grafie.

```sparql
# 1. trójki w grafach
SELECT ?g (COUNT(*) AS ?n) WHERE { GRAPH ?g { ?s ?p ?o } } GROUP BY ?g
# 2. typy w grafach
SELECT ?g ?typ (COUNT(DISTINCT ?s) AS ?n)
WHERE { GRAPH ?g { ?s a ?typ } } GROUP BY ?g ?typ
```

Pierwsze zapytanie daje po jednym wierszu na graf: `ex:linia_a`, `ex:linia_b`, `ex:provenance`. Porównaj `?n` z liczbą trójek w `biuro.trig`, pamiętając, że [wynika ona z tabeli mapowania, a nie z liczby komórek CSV](04%20Konwersja%20CSV%20do%20TriG.md#jeden-wiersz-wizyty-do-trig). Brak wiersza grafu znaczy, że nic w nim nie wylądowało, np. [przez pole grafu docelowego przy wgraniu](04%20Konwersja%20CSV%20do%20TriG.md#lm-27). Graf domyślny liczysz osobno, bez `GRAPH`.

Drugie zapytanie pokazuje, czy `bpc:Wizyta` leży w grafach linii, a `prov:Activity` i `prov:SoftwareAgent` w `ex:provenance`.

Obecność metadanych to sprawdzenie braku, więc użyj FILTER NOT EXISTS, czyli warunku spełnionego, gdy wzorzec nie ma dopasowania:

```sparql
SELECT DISTINCT ?g WHERE {
  GRAPH ?g { ?s ?p ?o }
  FILTER (?g != ex:provenance)
  FILTER NOT EXISTS { GRAPH ex:provenance { ?g prov:wasGeneratedBy ?a } }
}
```

<a id="lm-37"></a>Pusty wynik oznacza, że każdy graf ma opis. [Czy trójki trafiły do właściwej linii, sprawdzimy osobno](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#ref-99).

## Nakładające się wizyty w dwóch liniach

Podróżnika, który w dwóch liniach czasu jest w tym samym czasie, znajdziesz zapytaniem z dwoma blokami `GRAPH`, po jednym na linię, wspólną zmienną `?p` i warunkiem nakładania się przedziałów. Wynik to lista kandydatów do sprzeczności, a nie werdykt.

Wizyty leżą w grafach `ex:linia_a` i `ex:linia_b`, więc wspólna zmienna `?p` w obu blokach wymusza tego samego podróżnika. Dwa przedziały się nakładają, gdy każdy zaczyna się nie później, niż kończy się drugi. Porównanie robi FILTER na datach `xsd:date`:

```sparql
SELECT ?p ?w1 ?w2 ?od1 ?do1 ?od2 ?do2 WHERE {
  GRAPH ex:linia_a {
    ?p bpc:odwiedzil ?w1 .
    ?w1 bpc:od ?od1 ; bpc:do ?do1 .
  }
  GRAPH ex:linia_b {
    ?p bpc:odwiedzil ?w2 .
    ?w2 bpc:od ?od2 ; bpc:do ?do2 .
  }
  FILTER (?od1 <= ?do2 && ?od2 <= ?do1)
}
```

<a id="ref-4"></a>Zapisz je jako `analiza_1.rq`: tak pytanie Biura staje się osobnym zapytaniem z pliku. Każdy wiersz to para wizyt `?w1` i `?w2` tego samego podróżnika, z obiema parami dat obok siebie, więc dane sprawdzisz bez kolejnego zapytania.

### Jak czytać wiersze

Wiersz oznacza: ten podróżnik był w obu liniach w tym samym czasie. To może być paradoks, ale też błąd daty w jednym z CSV, więc porównaj daty z epoką wizyty. Znak `<=` liczy zetknięcie, gdy jedna wizyta kończy się w dniu początku drugiej. Chcesz je pominąć, użyj `<`.

Brak wiersza nie dowodzi braku sprzeczności. Wizyta bez `do` nie ma trójki z końcem, więc wzorzec `?w1 bpc:do ?do1` się nie dopasowuje i wizyta odpada, [tak jak wcześniej wizyta bez daty końca](04%20Konwersja%20CSV%20do%20TriG.md#lm-21). [To inny mechanizm niż błąd typu](00%20Glosariusz.md#błąd-typu) (brak trójki, a nie zły literał), ale skutek jest ten sam: wiersz znika bez komunikatu. [Takie wizyty szukaj osobno.](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#ref-102)

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#05-sparql-select-i-wzorce-trójek)_

## Co zapamiętać

- SELECT to wzorzec trójek ze zmiennymi; wspólny podmiot (średnik) łączy trójki o tej samej wizycie, a bez FROM z UnionGraph zapytanie widzi tylko graf domyślny.
- W FILTER porównuj daty tylko jako literały z ^^xsd:date; napis lub zły typ daje błąd typu i wiersz po cichu znika.
- Szukając samych braków użyj FILTER NOT EXISTS, a OPTIONAL z !BOUND wtedy, gdy obok braków chcesz widzieć też wiersze z wartością.
- GRAPH ?g wiąże nazwę grafu ze zmienną, a stałe IRI w GRAPH albo FROM NAMED ogranicza zapytanie do wskazanego grafu.
- HAVING filtruje grupy po agregacji (np. `HAVING (COUNT(DISTINCT ?w) > 1)`), a FILTER wiersze przed nią; w HAVING powtarzasz wyrażenie, a nie alias.
- Ścieżka `+` lub `*` z grupą kroków połączonych `/` znajduje węzły osiągalne przez dowolną liczbę powtórzeń, ale zwraca tylko koniec trasy, a nie jej długość.
- Po załadowaniu zlicz trójki i typy grupując po grafie, a brak opisu w ex:provenance wykryj przez FILTER NOT EXISTS.
- Nakładanie się wizyt w dwóch liniach wykryjesz dwoma blokami GRAPH ze wspólnym podróżnikiem i filtrem `?od1 <= ?do2 && ?od2 <= ?do1`, ale wynik to kandydaci, a wizyty bez `do` w nim nie ma.

## Pytania sprawdzające

### 29. Jak zapytasz o wizyty podróżnika ze zmiennymi, wspólnym podmiotem i PREFIX?

<details>
<summary>Odpowiedź</summary>

Zapytasz SELECT-em z trójkami ex:p1 bpc:odwiedzil ?wizyta oraz ?wizyta bpc:od ?od ; bpc:do ?do, z PREFIX na górze. Zmienne wiążą się z każdym pasującym podstawieniem, a średnik zachowuje wspólny podmiot ?wizyta. Wizyty leżą w grafach nazwanych, więc zapytanie potrzebuje widoku łączącego grafy, tu FROM <urn:x-arq:UnionGraph>.

Zobacz: [sekcja „Wizyty podróżnika w SELECT”](#wizyty-podróżnika-w-select).

</details>

### 30. Jak porównasz daty typu xsd:date w FILTER i co się dzieje z literałem o złym typie?

<details>
<summary>Odpowiedź</summary>

Daty xsd:date porównujesz w FILTER zwykłymi operatorami (<, >=, =), pod warunkiem że obie strony to literały z typem xsd:date; porównanie jest wartościowe, kalendarzowe. Literał o innym typie, np. zwykły napis, daje błąd typu, a FILTER traktuje go jak fałsz. Wiersz znika z wyniku bez ostrzeżenia, więc pusty wynik sprawdzaj przez DATATYPE(?od) bez filtra.

Zobacz: [sekcja „Daty w FILTER i literały o złym typie”](#daty-w-filter-i-literały-o-złym-typie).

</details>

### 31. Czym różni się OPTIONAL od FILTER NOT EXISTS i kiedy każdy służy do szukania braków?

<details>
<summary>Odpowiedź</summary>

OPTIONAL dołącza dane, jeśli istnieją, a brak zostawia jako zmienną niezwiązaną, którą wykrywasz przez !BOUND. FILTER NOT EXISTS odrzuca wiersze mające dopasowanie i niczego nie wiąże. Do samych braków użyj FILTER NOT EXISTS; OPTIONAL wybierz, gdy chcesz widzieć wszystkie wiersze, także z wartością.

Zobacz: [sekcja „OPTIONAL a FILTER NOT EXISTS”](#optional-a-filter-not-exists).

</details>

### 32. Jak w SPARQL związać nazwę grafu ze zmienną i wykonać zapytanie w jednym wskazanym grafie?

<details>
<summary>Odpowiedź</summary>

Nazwę grafu wiążesz ze zmienną wzorcem GRAPH ?g { ... }: zmienna dostaje IRI grafu, w którym leży dopasowana trójka. Jeden wskazany graf odpytujesz przez GRAPH ze stałym IRI albo przez FROM NAMED, które zawęża zbiór grafów widocznych dla GRAPH. Zwykłe FROM ustawia graf domyślny i gubi informację o pochodzeniu trójki.

Zobacz: [sekcja „Zapytania w wybranym grafie”](#zapytania-w-wybranym-grafie).

</details>

### 33. Jak policzysz zdarzenia w każdym grafie i odfiltrujesz grupy warunkiem HAVING?

<details>
<summary>Odpowiedź</summary>

Zdarzenia w każdym grafie liczysz zapytaniem z `GRAPH ?g { ?w a bpc:Wizyta }`, `GROUP BY ?g` i `COUNT(DISTINCT ?w)`. Grupy odfiltrowuje `HAVING`, np. `HAVING (COUNT(DISTINCT ?w) > 1)`, bo działa po agregacji. `FILTER` działa wcześniej, na pojedynczych wierszach, więc warunku na liczbę w nim nie zapiszesz. W `HAVING` powtarzasz wyrażenie, a nie alias z `SELECT`.

Zobacz: [sekcja „Zliczanie zdarzeń w grafach i HAVING”](#zliczanie-zdarzeń-w-grafach-i-having).

</details>

### 34. Jak operatory + i * oraz / w ścieżce własności znajdują połączenia o zmiennej długości?

<details>
<summary>Odpowiedź</summary>

Operator `+` znaczy jeden krok lub więcej, `*` zero lub więcej, a `/` łączy kroki w ciąg. Powtarzana grupa w nawiasie, np. `(bpc:odwiedzil/^bpc:naWizycie/bpc:uczestnik)+`, przechodzi od podróżnika do współuczestników spotkań o dowolnej długości łańcucha. Wynik podaje tylko węzły końcowe, bez długości trasy, a `*` dodaje jeszcze węzeł startowy.

Zobacz: [sekcja „Ścieżki o zmiennej długości”](#ścieżki-o-zmiennej-długości).

</details>

### 35. Jakimi zapytaniami sprawdzisz liczby trójek w grafach, typy i obecność metadanych po załadowaniu?

<details>
<summary>Odpowiedź</summary>

Liczby trójek sprawdzasz zapytaniem COUNT z GROUP BY po grafie, typy zapytaniem o `a ?typ` grupowanym po grafie i typie. Obecność metadanych sprawdzasz przez FILTER NOT EXISTS: zapytanie zwraca grafy, które nie mają opisu `prov:wasGeneratedBy` w `ex:provenance`. Pusty wynik znaczy, że wszystkie grafy są opisane.

Zobacz: [sekcja „Kontrola grafów po załadowaniu”](#kontrola-grafów-po-załadowaniu).

</details>

### 36. Jak zapytaniem znajdziesz podróżnika, który w dwóch liniach czasu ma nakładające się wizyty, i jak zinterpretujesz wynik?

<details>
<summary>Odpowiedź</summary>

Użyj zapytania z dwoma blokami GRAPH, po jednym na linię czasu, ze wspólną zmienną podróżnika i filtrem nakładania się przedziałów: początek każdej wizyty nie później niż koniec drugiej. Każdy wiersz to para wizyt tego samego podróżnika z datami obok siebie. To kandydat do sprzeczności, bo przyczyną może być też błąd daty w CSV. Wizyta bez daty końca nie ma trójki `bpc:do`, więc nie trafi do wyniku i brak wiersza niczego nie dowodzi.

Zobacz: [sekcja „Nakładające się wizyty w dwóch liniach”](#nakładające-się-wizyty-w-dwóch-liniach).

</details>
