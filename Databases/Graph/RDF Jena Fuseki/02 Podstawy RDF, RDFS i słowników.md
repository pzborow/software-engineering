# Podstawy RDF, RDFS i słowników

W dziale 01 trójki trafiły do [datasetu](00%20Glosariusz.md#dataset) biuro jako surowe podmioty, orzeczenia i dopełnienia. Teraz nadajemy im znaczenie: dopełnienie dostaje typ (napis, data, język), a podmiot klasę i etykietę, po czym dane trafiają do [grafów nazwanych](00%20Glosariusz.md#graf-nazwany). Po lekturze zaprojektujesz [słownik](00%20Glosariusz.md#słownik) Biura Paradoksów Czasowych (własne klasy i właściwości w przestrzeni nazw bpc), oddzielisz go od IRI instancji w domenie example i wybierzesz terminy z [RDFS](00%20Glosariusz.md#rdfs), XSD, PROV-O i OWL-Time, a część świadomie odrzucisz. Dziedziny łączą się tak: RDF daje strukturę trójek, RDFS i XSD nadają jej typy, a PROV-O i OWL-Time podpowiadają, jak opisać pochodzenie danych i czas wizyt.

```text
IRI instancji (example)      słownik Biura (bpc)
  wizyta, linia czasu          klasy i właściwości
        |                             |
        |   używa terminów z:  RDFS, XSD, PROV-O, OWL-Time
        v                             v
        +-----------+-----------------+
                    |
                    v
                  trójki
                    |  zapisane w
                    v
   graf nazwany (np. linia czasu) w datasecie biuro
```

**W tym dziale:**

- [Literały: typ i język](#literały-typ-i-język)
- [Dataset i grafy nazwane w TriG](#dataset-i-grafy-nazwane-w-trig)
- [Typy, etykiety, domain i range](#typy-etykiety-domain-i-range)
- [IRI grafu a IRI wizyty](#iri-grafu-a-iri-wizyty)
- [Słownik bpc a IRI instancji](#słownik-bpc-a-iri-instancji)
- [Pełne URI terminów PROV-O](#pełne-uri-terminów-prov-o)
- [Przedział czasu czy zwykła data](#przedział-czasu-czy-zwykła-data)
- [Kryterium wyboru terminów](#kryterium-wyboru-terminów)
- [Kiedy zewnętrzny URI, a kiedy sameAs](#kiedy-zewnętrzny-uri-a-kiedy-sameas)
- [Terminy przyjęte i odrzucone](#terminy-przyjęte-i-odrzucone)

## Literały: typ i język

Dane w `wizyty.csv` to tekst, ale RDF pozwala zapisać, czym ten tekst jest. <a id="lm-5"></a>`"2024-05-01"^^xsd:date` to data, a `"2024-05-01"` to tylko napis o tych samych znakach. Dlatego <a id="ref-9"></a>[pozostałe kolumny wiersza `w1` zapiszemy teraz jako literały](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#lm-4).

[Literał](00%20Glosariusz.md#literał) to wartość w dopełnieniu trójki, a nie zasób z IRI. Ma postać napisu, czyli tzw. formy leksykalnej, i towarzyszy mu jedno z dwóch: [typ danych](00%20Glosariusz.md#typ-danych) albo [znacznik języka](00%20Glosariusz.md#znacznik-języka). Typ danych to IRI z biblioteki XSD, np. `xsd:date`, który mówi, jak interpretować napis. Znacznik języka, np. `@pl`, mówi, w jakim języku napisano tekst.

```turtle
@prefix xsd:  <http://www.w3.org/2001/XMLSchema#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

ex:w1 bpc:epoka "rzym" ;
      bpc:linia "linia_a" ;
      bpc:od "2024-05-05"^^xsd:date ;
      bpc:do "2024-05-10"^^xsd:date .
ex:rzym rdfs:label "Rzym"@pl .
```

Napis bez typu i bez znacznika ma w RDF 1.1 typ `xsd:string`, więc nic o nim nie wiadomo poza znakami. Literał z `xsd:date` da się porównywać jako daty. Zwykły napis porównuje się jako tekst, a błędnej daty nie wykryje nikt.

Znacznik `@pl` stosuje się do tekstu dla ludzi w konkretnym języku, np. etykiety `"Rzym"@pl`. Nie stosuje się go do dat, kluczy ani kodów, bo nie mają języka. Literał ma typ albo znacznik, nigdy oba naraz. [Porównywanie dat w zapytaniach pokażemy przy filtrach](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#ref-12).

_Wersje: RDF 1.1 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-podstawy-rdf-rdfs-i-słowników)_

> **Pułapka: Niepoprawna data w xsd:date nie jest odrzucana.** Literał `"2024-02-30"^^xsd:date` jest przyjmowany przez Fuseki jako ill-typed: zapis się udaje, a błąd wychodzi dopiero w filtrach (porównanie daje błąd/brak wyniku). Tekst sekcji sugeruje, że typ chroni dane; trzeba walidować np. SHACL-em albo przed wczytaniem.

## Dataset i grafy nazwane w TriG

Do tej pory wszystkie trójki `w1` leżały w jednym worku. Biuro chce jednak trzymać dane osobno dla każdej linii czasu, więc potrzebujemy grafów nazwanych i formatu, który je zapisze.

Ten sam podmiot w dwóch grafach zapisujesz w [TriG](00%20Glosariusz.md#trig), czyli w Turtle rozszerzonym o bloki `<IRI grafu> { ... }`. Każdy blok to osobny graf, a podmiot może wystąpić w wielu blokach z różnymi trójkami. Dataset to zbiór złożony z jednego grafu domyślnego i dowolnej liczby grafów nazwanych. Graf to tylko zbiór trójek.

```turtle
@prefix bpc: <http://example.org/bpc#> .
@prefix ex:  <http://example.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

ex:linia_a {
  ex:p1 bpc:odwiedzil ex:w1 .
  ex:w1 bpc:epoka ex:rzym ; bpc:od "2024-05-05"^^xsd:date .
}
ex:linia_b {
  ex:p1 bpc:odwiedzil ex:w2 .
  ex:w2 bpc:epoka ex:edo ; bpc:od "2024-05-05"^^xsd:date .
}
```

<a id="lm-6"></a>Tu `ex:p1` występuje w obu grafach, ale każdy mówi o nim co innego: w linii A był w Rzymie, w linii B w Edo. Dopiero taki podział pozwala pokazać sprzeczność, [którą widzieliśmy jako to, że „`p1` jest 5–10 maja jednocześnie w Rzymie i w Edo”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#lm-2), jako różnicę między grafami, a nie pomyłkę w danych.

Czwarty element trójki, nazwa grafu, nie należy do samej trójki. Ta sama trójka może leżeć w kilku grafach i to są osobne wpisy w datasecie. [Zapytania o konkretny graf pokażemy później](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#ref-15), a [wgranie TriG do `/biuro` przy ładowaniu danych](04%20Konwersja%20CSV%20do%20TriG.md#ref-16).

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-podstawy-rdf-rdfs-i-słowników)_

> **Pułapka: Zapytanie bez FROM widzi tylko graf domyślny.** Dane z `ex:linia_a` i `ex:linia_b` leżą w grafach nazwanych, więc zapytanie SELECT bez `GRAPH`/`FROM` na dataset Fuseki zwróci pusty wynik (domyślnie graf domyślny nie jest sumą grafów nazwanych). Trzeba użyć `GRAPH ?g { ... }` albo włączyć `tdb:unionDefaultGraph`.

> **Pułapka: Wgranie TriG do /biuro bez grafu ogranicza dane.** Format TriG niesie nazwy grafów tylko przy wgraniu do endpointu datasetu (`/biuro`); wysłanie go do endpointu grafu (`/biuro/data?graph=...`) albo jako Turtle gubi lub spłaszcza podział na grafy. Trzeba użyć poprawnego Content-Type `application/trig`.

## Typy, etykiety, domain i range

Skoro `ex:p1` bywa w różnych grafach, trzeba jeszcze powiedzieć, czym jest `p1` i czym jest `w1`. Do tego służą `rdf:type` i RDFS, czyli słownik W3C z klasami, etykietami, domain i range do opisu danych RDF. Opisują one dane, ale ich nie pilnują.

`rdf:type` (w Turtle skrót `a`) mówi, że zasób należy do klasy: `ex:p1 a bpc:Podroznik`. Klasa to nazwany zbiór zasobów, deklarowany jako `bpc:Podroznik a rdfs:Class`. `rdfs:label` dodaje czytelną dla ludzi nazwę, zwykle literał ze znacznikiem języka. Etykieta nie jest identyfikatorem: zasób identyfikuje IRI.

`rdfs:domain` i `rdfs:range` opisują własność: domain to klasa podmiotu, range to klasa (albo typ literału) dopełnienia.

```turtle
bpc:odwiedzil a rdf:Property ;
  rdfs:domain bpc:Podroznik ;
  rdfs:range  bpc:Wizyta .
bpc:od a rdf:Property ;
  rdfs:range xsd:date .

ex:p1 a bpc:Podroznik ; rdfs:label "Podróżnik 1"@pl .
ex:x bpc:odwiedzil ex:y .
```

Domain i range to nie ograniczenia jak `CHECK` czy `FOREIGN KEY` w SQL, tylko przesłanki [wnioskowania](00%20Glosariusz.md#wnioskowanie), czyli automatycznego dopisywania trójek wynikających z reguł. Z ostatniej linii silnik wnioskujący dopisze `ex:x a bpc:Podroznik` oraz `ex:y a bpc:Wizyta`, choć nikt tego nie zapisał i `ex:y` może być czymkolwiek. Fuseki bez włączonego wnioskowania nie dopisze niczego, a i tak niczego nie odrzuci.

RDFS nie waliduje też literałów: `"5 maja"` przy `bpc:od` przejdzie bez błędu. Nie sprawdzi więc, czy data jest datą, czy klucz obcy ma rekord, ani czy `p1` ma typ. Takie kontrole zrobi [walidator w Pythonie, który dopiszemy do konwertera](04%20Konwersja%20CSV%20do%20TriG.md#ref-18).

_Wersje: RDFS 1.1 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-podstawy-rdf-rdfs-i-słowników)_

## IRI grafu a IRI wizyty

Wizyty z `wizyty.csv` trzeba nazwać i przypiąć do linii czasu, zanim napiszemy konwerter. Do opisu używamy prefiksu `bpc:`, czyli słownika Biura, z którego pochodzą własności takie jak `bpc:odwiedzil`, oraz prefiksu `ex:` dla samych danych.

IRI wizyty identyfikuje **zasób**: jedną wizytę, czyli wiersz z `wizyty.csv`. IRI grafu linii czasu identyfikuje **kontener**: graf nazwany, w którym leży zbiór trójek tej linii. Oba to zwykłe [IRI](00%20Glosariusz.md#iri), różnią się rolą. Pierwsze stoi na pozycji podmiotu lub dopełnienia trójki, drugie jest nazwą grafu, w którym trójka się znajduje.

Wiąże je kolumna `linia` z CSV. Wartość `a` daje graf `ex:linia_a`, a wiersz `w1` daje zasób `ex:w1`, wpisany do tego grafu. Sama trójka nie mówi, do której linii należy, bo to niesie nazwa grafu.

```turtle
ex:linia_a { ex:p1 bpc:odwiedzil ex:w1 . }
ex:linia_b { ex:p1 bpc:odwiedzil ex:w2 . }
```

Konsekwencja: `ex:w1` nie potrzebuje własności `bpc:linia`, by wiadomo było, do której linii należy. Kolumnę `linia` można też zachować jako trójkę `bpc:linia`, ale to osobna informacja w danych, a nie to samo co nazwa grafu. Zapytanie o „wszystko z linii A” wskazuje graf, a zapytanie o „wizytę w1” wskazuje zasób.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-podstawy-rdf-rdfs-i-słowników)_

> **Pułapka: Ten sam zasób w wielu grafach nazwanych.** IRI `ex:w1` jest globalne, więc może wystąpić w trójkach kilku grafów (np. `ex:linia_a` i `ex:linia_b`). Opisy wizyty rozproszą się po grafach, a zapytanie o `ex:w1` w jednym `GRAPH` zobaczy tylko część faktów. Trzeba pilnować, by trójki o zasobie trafiały do jednego grafu, albo pytać przez `GRAPH ?g`.

## Słownik bpc a IRI instancji

Słownik Biura i dane trzymamy w osobnych przestrzeniach nazw, bo opisują różne rzeczy i mają różny cykl życia. Zewnętrzny URI wolno użyć, gdy ktoś już zdefiniował dokładnie to pojęcie. [`owl:sameAs`](00%20Glosariusz.md#owlsameas) to własność OWL o pełnym URI `http://www.w3.org/2002/07/owl#sameAs`, która twierdzi, że dwa IRI wskazują tę samą rzecz. Wolno jej użyć tylko przy pewnej tożsamości.

`bpc:` zawiera klasy i własności, `ex:` instancje z wierszy CSV. Zmieniają się w różnym tempie: słownik rzadko, dane przy każdym przebiegu konwertera.

```turtle
@prefix bpc: <http://example.org/bpc#> .
@prefix ex:  <http://example.org/id/> .

ex:p1 a bpc:Podroznik .
ex:w1 a bpc:Wizyta .
# poza kanonem, źle: instancja w słowniku
bpc:Podroznik bpc:odwiedzil bpc:w1 .
```

Kolizja jest realna. Gdyby CSV miał podróżnika o kluczu `Podroznik`, IRI `bpc:Podroznik` byłoby jednocześnie klasą i osobą. Wiersz „dodany do słownika” zmieniałby też sam słownik. Przy `ex:` taki klucz daje `ex:Podroznik`, czyli inne IRI.

### Kiedy sięgnąć na zewnątrz

| Sytuacja | Decyzja |
|---|---|
| Pojęcie ma ustaloną definicję w cudzym słowniku (`rdfs:label`, `xsd:date`) | zewnętrzny URI |
| Pojęcie specyficzne dla Biura (`bpc:Wizyta`) | własne w `bpc:` |
| Ten sam obiekt ma drugie IRI w cudzym zbiorze | `owl:sameAs`, przy pewnej tożsamości |

Skutek `owl:sameAs` to wnioskowanie: wszystko prawdziwe o jednym IRI staje się prawdziwe o drugim. Weźmy `ex:p1` z dwóch linii czasu, w Rzymie i w Edo. Gdyby ktoś dodał `ex:p1 owl:sameAs ex:p1_edo`, wnioskowanie przypisałoby obie wizyty obu IRI i zlało fakty, które linie mają trzymać osobno. Dlatego zostawiamy `owl:sameAs` na potwierdzone tożsamości.

> **Pułapka: Fuseki domyślnie nie stosuje owl:sameAs.** Sam trójkąt `owl:sameAs` nie zlewa faktów, dopóki dataset nie ma modelu wnioskującego (np. reguł OWL w konfiguracji Fuseki). Bez niego zapytania SPARQL widzą wizyty osobno przy każdym IRI, więc test na czystym TDB przejdzie, a po włączeniu wnioskowania na produkcji dane się zleją. Trzeba sprawdzić konfigurację datasetu.

## Pełne URI terminów PROV-O

Przed chwilą rozdzieliliśmy własne IRI od cudzych. Teraz sięgamy po pierwszy cudzy słownik, PROV-O, [którym opiszemy pochodzenie danych z konwersji CSV](04%20Konwersja%20CSV%20do%20TriG.md#ref-21). Najpierw trzeba wiedzieć, jak te terminy naprawdę się nazywają.

PROV-O to słownik W3C do opisu pochodzenia danych: kto, czym i z czego je wytworzył. Wszystkie pięć terminów leży w przestrzeni nazw `http://www.w3.org/ns/prov#`, a pełne URI to ten prefiks plus nazwa lokalna.

| Skrót | Pełne URI | Rodzaj |
|---|---|---|
| `prov:Entity` | `http://www.w3.org/ns/prov#Entity` | klasa: rzecz, np. wygenerowany plik |
| `prov:Activity` | `http://www.w3.org/ns/prov#Activity` | klasa: działanie, np. konwersja |
| `prov:Agent` | `http://www.w3.org/ns/prov#Agent` | klasa: ten, kto odpowiada |
| `prov:wasGeneratedBy` | `http://www.w3.org/ns/prov#wasGeneratedBy` | własność: Entity → Activity |
| `prov:wasAttributedTo` | `http://www.w3.org/ns/prov#wasAttributedTo` | własność: Entity → Agent |

Uwaga: przestrzeń nazw kończy się `#`, a nie `/`. Prefiks `@prefix prov: <http://www.w3.org/ns/prov#> .` zapisany bez `#` da inne, nieistniejące IRI i zapytanie po cichu nic nie zwróci.

### Gdzie zweryfikujesz

Źródłem jest specyfikacja PROV-O (Recommendation W3C z 2013 r.) pod `https://www.w3.org/TR/prov-o/`. Sam słownik serwer zwraca zależnie od nagłówka `Accept`, więc możesz go pobrać i wyszukać termin:

```bash
curl -sL -H 'Accept: text/turtle' http://www.w3.org/ns/prov \
  | grep -A3 'prov:wasGeneratedBy'
```

Wynik zawiera definicję własności, w tym jej dziedzinę i zakres.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-podstawy-rdf-rdfs-i-słowników)_

## Przedział czasu czy zwykła data

Wizyta w Biurze ma już kolumny `od` i `do` w wizyty.csv, więc pora zdecydować, jak zapisać czas: zostajemy przy zwykłych datach, a przedział z OWL-Time wprowadzamy dopiero wtedy, gdy sam czas jest przedmiotem opisu.

OWL-Time to słownik W3C do opisu czasu. Jego klasa `time:Interval` to przedział jako osobny zasób, który ma początek (`time:hasBeginning`) i koniec (`time:hasEnd`), a te są instantami (`time:Instant`), zwykle z datą w `time:inXSDDate`.

| Potrzeba | Wybór |
|---|---|
| porównać granice (`FILTER(?od < ?do2)`) | daty xsd |
| jedna wizyta, jedna para dat | daty xsd |
| o przedziale trzeba coś powiedzieć (źródło, niepewność, relacja do epoki) | `time:Interval` |
| relacje Allena (`time:intervalBefore`, `time:intervalOverlaps`) | `time:Interval` |

Domyślnie wystarczą daty: `bpc:od` i `bpc:do` z typem `xsd:date` to dwie trójki na wizytę, a porównanie w SPARQL jest natychmiastowe.

Przedział kosztuje więcej: <a id="lm-8"></a>trzy węzły (przedział, początek i koniec) zamiast dwóch trójek z datami, a do tego dłuższe zapytania.

```turtle
ex:w1 bpc:od "2024-05-05"^^xsd:date ;
      bpc:do "2024-05-10"^^xsd:date .

# wariant z przedziałem
ex:w1_czas a time:Interval ;
  time:hasBeginning [ time:inXSDDate "2024-05-05"^^xsd:date ] ;
  time:hasEnd       [ time:inXSDDate "2024-05-10"^^xsd:date ] .
```

Sięgnij po przedział, gdy wizyta i epoka mają być porównywane jako przedziały albo gdy granice są niepewne. Tu wystarczą daty, a [przedziały zostawiamy epokom](#lm-9).

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-podstawy-rdf-rdfs-i-słowników)_

> **Pułapka: Węzły puste w przedziale mnożą się przy ponownym wgraniu.** Dla `time:hasBeginning [ ... ]` i `time:hasEnd [ ... ]` każde wgranie pliku tworzy nowe węzły puste. Powtórny POST nie jest więc idempotentny: `ex:w1_czas` dostaje kolejne początki i końce, a zapytanie zwraca zdublowane lub sprzeczne granice. Nadaj instantom stałe IRI (np. `ex:w1_start`) albo przed wgraniem zastąp graf.

## Kryterium wyboru terminów

[Wybór dat mamy za sobą](#przedział-czasu-czy-zwykła-data), więc domykamy słowniki: do modelu Biura wchodzi tylko termin, który czyta lub zapisuje któraś analiza albo konwerter. Resztę odrzucamy, żeby model nie rósł na zapas.

OWL-Time to słownik W3C do opisu czasu. `time:Interval` to przedział jako osobny zasób, a jego granice są instantami (`time:Instant`), czyli punktami na osi czasu, zwykle z datą w `time:inXSDDate`.

| Słownik | Używamy | Odrzucamy | Dlaczego |
|---|---|---|---|
| RDFS | `rdfs:Class`, `rdfs:label`, `rdfs:domain`, `rdfs:range` | `rdfs:subClassOf`, `rdfs:seeAlso` | klasy Biura są płaskie |
| XSD | `xsd:date`, `xsd:string`; `xsd:dateTime` tylko dla śladu konwersji | `xsd:gYear` | dane z CSV to same daty; dateTime dotyczy znacznika czasu przebiegu |
| PROV-O | `prov:Activity`, `prov:Agent`, `prov:wasGeneratedBy`, `prov:wasAssociatedWith`, `prov:startedAtTime` | `prov:Plan`, `prov:Bundle`, `prov:Delegation` | opisujemy tylko konwersję i jej agenta |
| OWL-Time | `time:Interval`, `time:hasBeginning`, `time:hasEnd`, `time:inXSDDate` tylko dla epok | `time:Interval` dla wizyt, `time:before` | wizyty mają zwykłe `bpc:od` i `bpc:do` |

<a id="ref-23"></a><a id="lm-9"></a>Tak dotrzymujemy obietnicy: przedziały zostawiamy epokom. Epoka jest zasobem, o którym mówimy coś jeszcze (nazwę, źródło granic), a wizyta zostaje przy dwóch datach.

```turtle
ex:epoka_rzym a time:Interval ;
  rdfs:label "Rzym" ;
  time:hasBeginning [ time:inXSDDate "0027-01-01"^^xsd:date ] ;
  time:hasEnd       [ time:inXSDDate "0476-09-04"^^xsd:date ] .

ex:w1 bpc:od "2024-05-05"^^xsd:date ;
      bpc:do "2024-05-10"^^xsd:date .
```

Odrzucony termin można dodać później, bo dopisanie trójek niczego nie psuje. Usunięcie użytego terminu z danych jest kosztowne. Podróżnik i wizyta zostają w `bpc:`, a z PROV-O bierzemy tylko ślad pochodzenia, który trafi do [osobnego grafu provenance](04%20Konwersja%20CSV%20do%20TriG.md#ref-26).

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-podstawy-rdf-rdfs-i-słowników)_

> **Pułapka: Data z xsd:date bez ostrzeżenia zmienia sens dla lat starożytnych.** Literał `"0027-01-01"^^xsd:date` jest poprawny w XSD 1.0, ale w XSD 1.1 rok 0000 istnieje, a przed naszą erą wymaga znaku minus. Fuseki/Jena nie ostrzeże, więc granice epoki `ex:epoka_rzym` mogą być porównywane inaczej w różnych narzędziach. Dla epok trzeba jawnie ustalić konwencję lat.

## Kiedy zewnętrzny URI, a kiedy sameAs

Konwerter i analizy już działają, więc czas uzasadnić, po co [w `mapping` są osobne przestrzenie `bpc:` i `ex:`](#słownik-bpc-a-iri-instancji) oraz kiedy wolno użyć cudzego terminu albo połączyć dwa IRI.

Przestrzenie rozdzielamy, bo słownik (klasy i własności) i instancje (wizyty, podróżnicy) mają różny cykl życia: słownik zmienia się rzadko i świadomie, a instancje powstają przy każdej konwersji CSV. W jednej przestrzeni wiersz CSV o kluczu `Wizyta` dałby IRI równe klasie `bpc:Wizyta`. RDFS i wnioskowanie potraktowałyby je naraz jako klasę i jako zasób.

### Zewnętrzny URI

Cudzy termin bierzemy, gdy jego definicja w specyfikacji pasuje do naszego znaczenia, a nie tylko brzmi podobnie: `rdfs:label` to „nazwa czytelna dla człowieka”, [`time:Interval` i `prov:Activity` też mają ścisły sens](#przedział-czasu-czy-zwykła-data). Przy niepasującym znaczeniu zdefiniuj własny termin w `bpc:`. Cudzych terminów nie redefiniujemy.

### owl:sameAs

Tożsamość wizyty między liniami daje to samo IRI z `iri_for`, więc `owl:sameAs` zwykle zbędne. `owl:sameAs` oznacza, że dwa IRI wskazują ten sam zasób. Używaj jej wyłącznie po potwierdzeniu tożsamości; nie zgaduj zewnętrznych identyfikatorów. Przy wnioskowaniu fakty obu IRI zlewają się, także sprzeczne:

```turtle
# poza kanonem: celowo błędne powiązanie dwóch lokalnych IRI
ex:podroznik_jan bpc:odwiedzil ex:w1 .          # linia_a, w1: 2024-05-01
ex:podroznik_jan_kopia bpc:odwiedzil ex:w2 .    # linia_b, w2: 2024-05-08
ex:podroznik_jan owl:sameAs ex:podroznik_jan_kopia .
```

Po zlaniu [`analiza_1.rq` widzi jednego podróżnika](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#ślady-paradoksów-w-csv) w dwóch wizytach i może zgłosić fałszywy kandydat na nakładanie się, a `kontrola.rq` zlicza trójki obu IRI razem. Cofnięcie wymaga ustalenia, które fakty były czyje. W tym fikcyjnym przykładzie można użyć `rdfs:seeAlso` bez deklarowania tożsamości: `ex:podroznik_jan rdfs:seeAlso ex:podroznik_jan_kopia`.

_[źródła: 3](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-podstawy-rdf-rdfs-i-słowników)_

## Terminy przyjęte i odrzucone

[Konwerter dopiero powstanie](04%20Konwersja%20CSV%20do%20TriG.md#ref-21) (to program zamieniający wiersze CSV na trójki i zapisujący ślad), więc już teraz spisujemy, które terminy zostają, a które odpadają. Kryterium jest jedno: czy termin czyta analiza albo zapisuje konwerter.

| Termin | Decyzja | Uzasadnienie |
|---|---|---|
| `rdfs:Class`, `rdfs:label` | bierzemy | klasy typują węzły, a etykiety niosą nazwy, których nie wolno wpisywać w IRI |
| `rdfs:domain`, `rdfs:range` | bierzemy | opisują własności; nic nie odrzucają, więc poprawność typów sprawdzamy osobnym krokiem |
| `xsd:date`, `xsd:string` | bierzemy | analizy porównują daty w FILTER, a napis to zwykły tekst |
| `xsd:dateTime` | tylko ślad | potrzebny w `prov:startedAtTime` i `prov:endedAtTime`; wizyty mają dni, nie godziny |
| `prov:Activity`, `prov:SoftwareAgent`, `prov:used`, `prov:wasGeneratedBy`, `prov:wasDerivedFrom` | bierzemy | konwerter zapisuje z nich, który plik i przebieg dały graf linii |
| `prov:wasAssociatedWith`, `prov:startedAtTime` | bierzemy | wskazują `ex:konwerter` i odróżniają przebiegi |
| `time:Interval` | tylko epoki | [epoka ma początek i koniec](#lm-9); [wizyta wystarczy z `bpc:od` i `bpc:do`](#przedział-czasu-czy-zwykła-data) |
| `owl:sameAs` | warunkowo | tylko po potwierdzeniu tożsamości; w przykładowych danych Biura nie ma takiego przypadku |
| `rdfs:seeAlso` | odrzucamy | sameAs wskazuje tożsamość, seeAlso to tylko odsyłacz, a żadna analiza go nie czyta |
| `rdfs:subClassOf` | odrzucamy | klasy są płaskie, a nikt nie pyta o podklasy |
| `prov:Plan`, `prov:Bundle` | odrzucamy | nie mamy planów, a [`ex:provenance` jest już grafem nazwanym](#dataset-i-grafy-nazwane-w-trig) |
| `time:intervalBefore`, `time:intervalOverlaps` | odrzucamy | nakładanie liczymy przez FILTER na datach; model przedziałów nie jest potrzebny analizom |

Gdy analiza zacznie wymagać terminu, dodajesz go razem z konwerterem, który go zapisze.

## Co zapamiętać

- Literał z xsd:date jest datą, zwykły napis to xsd:string, a znacznik języka, np. @pl, dotyczy tylko tekstu dla ludzi i wyklucza typ.
- TriG zapisuje grafy nazwane jako bloki `IRI { ... }`, a dataset to graf domyślny plus grafy nazwane, w których ten sam podmiot może mieć różne trójki.
- Domain i range w RDFS to przesłanki do wnioskowania, a nie walidacja: nic nie odrzucają, więc poprawność danych trzeba sprawdzać osobno.
- IRI wizyty wskazuje zasób, IRI grafu wskazuje kontener trójek, a przynależność do linii czasu niesie nazwa grafu, w którym leży trójka.
- Klasy i własności trzymaj w bpc:, instancje w osobnej przestrzeni ex:, a owl:sameAs stosuj tylko dla potwierdzonej tożsamości.
- Terminy PROV-O mają URI w przestrzeni http://www.w3.org/ns/prov# (z # na końcu), a sprawdzisz je w specyfikacji W3C albo pobierając słownik curlem z nagłówkiem Accept.
- Domyślnie zapisuj czas wizyty datami xsd:date, a time:Interval stosuj tylko wtedy, gdy sam przedział wymaga opisu lub relacji czasowych.
- Do modelu trafia tylko termin, który czyta lub zapisuje analiza albo konwerter; przedziały OWL-Time dostają epoki, wizyty zostają przy datach xsd:date.
- Cudzy termin bierz, gdy jego definicja pasuje, a owl:sameAs dawaj tylko przy pewnej tożsamości; przy wątpliwościach użyj rdfs:seeAlso, bo sameAs zlewa też sprzeczne fakty.
- Termin wchodzi do modelu tylko wtedy, gdy czyta go analiza albo zapisuje konwerter; owl:sameAs bierzemy dla potwierdzonej tożsamości, seeAlso odrzucamy.

## Pytania sprawdzające

### 5. Czym różni się "2024-05-01"^^xsd:date od zwykłego napisu i kiedy stosuje się znacznik języka @pl?

<details>
<summary>Odpowiedź</summary>

"2024-05-01"^^xsd:date to literał z typem danych, więc narzędzia interpretują go jako datę i mogą porównywać chronologicznie. Zwykły napis ma typ xsd:string i jest tylko tekstem. Znacznik @pl dodaje się do tekstu czytelnego dla ludzi w danym języku, np. etykiet; nie stosuje się go do dat, kluczy i kodów.

Zobacz: [sekcja „Literały: typ i język”](#literały-typ-i-język).

</details>

### 6. Jak w TriG zapisać ten sam podmiot w dwóch grafach nazwanych i czym dataset różni się od grafu?

<details>
<summary>Odpowiedź</summary>

W TriG każdy graf nazwany to blok `<IRI grafu> { ... }`, więc ten sam podmiot, np. `ex:p1`, zapisujesz w dwóch blokach z różnymi trójkami. Graf jest zbiorem trójek, a dataset zbiorem złożonym z jednego grafu domyślnego i dowolnej liczby grafów nazwanych. Nazwa grafu nie należy do trójki, więc ta sama trójka w dwóch grafach to dwa osobne wpisy w datasecie.

Zobacz: [sekcja „Dataset i grafy nazwane w TriG”](#dataset-i-grafy-nazwane-w-trig).

</details>

### 7. Jak użyć rdf:type, rdfs:Class, rdfs:label, rdfs:domain i rdfs:range i czego one nie walidują?

<details>
<summary>Odpowiedź</summary>

rdf:type przypisuje zasób do klasy zadeklarowanej jako rdfs:Class, rdfs:label daje czytelną nazwę, a rdfs:domain i rdfs:range opisują, jakiego typu są podmiot i dopełnienie własności. Nie są to ograniczenia: służą wnioskowaniu, które z użycia własności dopisuje typy zasobom, nawet błędnie. RDFS ani Fuseki nie sprawdzą poprawności literałów, kluczy obcych ani obecności typu.

Zobacz: [sekcja „Typy, etykiety, domain i range”](#typy-etykiety-domain-i-range).

</details>

### 8. Czym różni się IRI grafu linii czasu od IRI wizyty i jak graf nazwany wiąże dane z linią czasu?

<details>
<summary>Odpowiedź</summary>

IRI wizyty (np. ex:w1) identyfikuje zasób, czyli jedną wizytę z wiersza CSV, a IRI grafu (np. ex:linia_a) identyfikuje graf nazwany, czyli kontener na trójki jednej linii czasu. Oba są zwykłymi IRI, różnią się rolą w zapisie. Dane wiąże z linią czasu kolumna linia: jej wartość wyznacza graf, w którym konwerter umieszcza trójki wizyty. Przynależność wynika więc z nazwy grafu, a nie z trójki.

Zobacz: [sekcja „IRI grafu a IRI wizyty”](#iri-grafu-a-iri-wizyty).

</details>

### 9. Dlaczego rozdzielasz namespace słownika Biura od IRI instancji w domenie example i kiedy wolno użyć zewnętrznego URI lub owl:sameAs?

<details>
<summary>Odpowiedź</summary>

Słownik bpc: i instancje ex: rozdzielamy, bo mają różny cykl życia, a klucz z danych (np. „Wizyta”) mógłby dać IRI równe klasie i zderzyć się z modelem. Zewnętrzny URI wolno użyć, gdy jego definicja pasuje do naszego znaczenia (rdfs:label, time:Interval, prov:Activity); przy innym sensie definiujemy własny termin w bpc: i cudzych nie redefiniujemy. owl:sameAs dodajemy tylko przy potwierdzonej tożsamości dwóch różnych IRI, bo wnioskowanie zlewa wszystkie ich fakty, także sprzeczne, co fałszuje wyniki analiz, np. analiza_1.rq, i trudno to cofnąć. Przy wątpliwościach użyj rdfs:seeAlso, które niczego nie zlewa.

Zobacz: [sekcja „Słownik bpc a IRI instancji”](#słownik-bpc-a-iri-instancji), [sekcja „Kiedy zewnętrzny URI, a kiedy sameAs”](#kiedy-zewnętrzny-uri-a-kiedy-sameas).

</details>

### 10. Jakie pełne URI mają prov:Entity, prov:Activity, prov:Agent, prov:wasGeneratedBy, prov:wasAttributedTo i gdzie je zweryfikujesz?

<details>
<summary>Odpowiedź</summary>

Wszystkie pięć terminów ma URI z przestrzeni `http://www.w3.org/ns/prov#`: `prov:Entity`, `prov:Activity` i `prov:Agent` to klasy, a `prov:wasGeneratedBy` i `prov:wasAttributedTo` to własności. Prefiks musi kończyć się `#`. Zweryfikujesz je w specyfikacji PROV-O na w3.org/TR/prov-o/ albo pobierając słownik z `http://www.w3.org/ns/prov` poleceniem curl z nagłówkiem `Accept: text/turtle`.

Zobacz: [sekcja „Pełne URI terminów PROV-O”](#pełne-uri-terminów-prov-o).

</details>

### 11. Kiedy wizytę modelujesz przez time:Interval z time:hasBeginning/hasEnd, a kiedy wystarczą proste daty xsd?

<details>
<summary>Odpowiedź</summary>

Gdy wizyta ma jedną parę dat i trzeba je tylko porównywać, wystarczą proste daty xsd:date w bpc:od i bpc:do. time:Interval z time:hasBeginning i time:hasEnd wybierasz, gdy o przedziale trzeba coś powiedzieć (źródło, niepewność, relacja do epoki) albo użyć relacji Allena. Przedział kosztuje trzy węzły zamiast dwóch trójek i dłuższe zapytania.

Zobacz: [sekcja „Przedział czasu czy zwykła data”](#przedział-czasu-czy-zwykła-data).

</details>

### 12. Które terminy PROV-O, OWL-Time, RDFS i XSD użyjesz w Biurze, które odrzucisz i dlaczego?

<details>
<summary>Odpowiedź</summary>

Do Biura wchodzą tylko terminy, które czyta analiza albo zapisuje konwerter: z RDFS klasy, etykiety, domain i range; z XSD date i string, a dateTime tylko w śladzie; z PROV-O aktywność, agent i powiązania śladu; z OWL-Time przedziały tylko dla epok; oraz owl:sameAs dla potwierdzonej tożsamości podróżnika. Odrzucamy subClassOf, Plan, Bundle, przedziały dla wizyt, relacje czasowe i rdfs:seeAlso, bo żadna analiza ich nie potrzebuje. Domain i range niczego nie walidują, więc typy sprawdza osobny krok.

Zobacz: [sekcja „Kryterium wyboru terminów”](#kryterium-wyboru-terminów), [sekcja „Terminy przyjęte i odrzucone”](#terminy-przyjęte-i-odrzucone).

</details>
