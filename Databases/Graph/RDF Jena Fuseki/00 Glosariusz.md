# Glosariusz: Jena Fuseki i grafy RDF w praktyce

## Spis haseł

- [Fuseki](#fuseki)
- [SPARQL](#sparql)
- [dataset](#dataset)
- [Graph Store Protocol](#graph-store-protocol)
- [graf nazwany](#graf-nazwany)
- [trójka](#trójka)
- [IRI](#iri)
- [prefiks](#prefiks)
- [Turtle](#turtle)
- [literał](#literał)
- [typ danych](#typ-danych)
- [znacznik języka](#znacznik-języka)
- [TriG](#trig)
- [RDFS](#rdfs)
- [wnioskowanie](#wnioskowanie)
- [owl:sameAs](#owlsameas)
- [słownik](#słownik)
- [OWL-Time](#owl-time)
- [węzeł zdarzenia](#węzeł-zdarzenia)
- [relacja wielostronna](#relacja-wielostronna)
- [wiersz mapowania](#wiersz-mapowania)
- [tabela mapowania](#tabela-mapowania)
- [kodowanie procentowe](#kodowanie-procentowe)
- [PROV-O](#prov-o)
- [rdflib](#rdflib)
- [węzeł pusty](#węzeł-pusty)
- [graf domyślny](#graf-domyślny)
- [FILTER](#filter)
- [błąd typu](#błąd-typu)
- [OPTIONAL](#optional)
- [FILTER NOT EXISTS](#filter-not-exists)
- [GROUP BY](#group-by)
- [funkcja agregująca](#funkcja-agregująca)
- [HAVING](#having)
- [ścieżka własności](#ścieżka-własności)
- [BIND](#bind)
- [application/sparql-results+json](#applicationsparql-resultsjson)
- [ASK](#ask)

## Fuseki

Serwer HTTP z projektu Apache Jena, który przechowuje dane RDF w datasetach i udostępnia je przez SPARQL.

Pierwsza wzmianka: [rozdział 01, sekcja „Start Fuseki na Javie 17”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#start-fuseki-na-javie-17).
Występuje w: [01 › Start Fuseki na Javie 17](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#start-fuseki-na-javie-17).
Pytania: [1](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#1-jak-uruchomisz-fuseki-na-javie-17-i-po-czym-poznasz-że-serwer-działa-pod-właściwym-portem).

## SPARQL

Język zapytań do danych RDF, odpowiednik SQL dla grafów; Fuseki przyjmuje je przez HTTP.

Pierwsza wzmianka: [rozdział 01, sekcja „Start Fuseki na Javie 17”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#start-fuseki-na-javie-17).
Występuje w: [01 › Start Fuseki na Javie 17](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#start-fuseki-na-javie-17), [01 › Pytania Biura o paradoksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#pytania-biura-o-paradoksy), [05 › Wizyty podróżnika w SELECT](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#wizyty-podróżnika-w-select).
Pytania: [1](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#1-jak-uruchomisz-fuseki-na-javie-17-i-po-czym-poznasz-że-serwer-działa-pod-właściwym-portem), [2](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#2-jakie-sześć-pytań-o-paradoksy-zadaje-biuro-i-jakie-fragmenty-tabel-podróżników-wizyt-epok-artefaktów-spotkań-i-raportów-już-pokazują-sprzeczności), [29](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#29-jak-zapytasz-o-wizyty-podróżnika-ze-zmiennymi-wspólnym-podmiotem-i-prefix).

## dataset

Kontener na graf domyślny i grafy nazwane, pod którym Fuseki wystawia endpointy.

Pierwsza wzmianka: [rozdział 01, sekcja „Dataset biuro w przeglądarce”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce).
Występuje w: [01 › Dataset biuro w przeglądarce](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce), [02 › Dataset i grafy nazwane w TriG](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#dataset-i-grafy-nazwane-w-trig), [03 › Słowniki, przestrzenie i grafy modelu](03%20Model%20danych%20Biura.md#słowniki-przestrzenie-i-grafy-modelu), [04 › Dataset rdflib i zapis TriG](04%20Konwersja%20CSV%20do%20TriG.md#dataset-rdflib-i-zapis-trig).
Pytania: [3](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#3-jak-w-przeglądarce-utworzyć-trwały-dataset-i-jakie-endpointy-query-update-data-do-niego-przybywają), [6](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#6-jak-w-trig-zapisać-ten-sam-podmiot-w-dwóch-grafach-nazwanych-i-czym-dataset-różni-się-od-grafu), [15](03%20Model%20danych%20Biura.md#15-jak-z-wybranych-słowników-własnego-namespace-i-podziału-na-grafy-złożysz-spójny-model-biura), [23](04%20Konwersja%20CSV%20do%20TriG.md#23-jak-w-venv-dodasz-trójki-do-dataset-w-grafie-nazwanym-i-zapiszesz-go-jako-trig).

## Graph Store Protocol

Protokół HTTP do zarządzania całymi grafami: GET, PUT, POST i DELETE na grafie wskazanym parametrem ?graph=.

Pierwsza wzmianka: [rozdział 01, sekcja „Dataset biuro w przeglądarce”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce).
Występuje w: [01 › Dataset biuro w przeglądarce](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce), [04 › Wgranie TriG z nazwami grafów](04%20Konwersja%20CSV%20do%20TriG.md#wgranie-trig-z-nazwami-grafów), [07 › Zapytanie SPARQL przez HTTP](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#zapytanie-sparql-przez-http).
Pytania: [3](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#3-jak-w-przeglądarce-utworzyć-trwały-dataset-i-jakie-endpointy-query-update-data-do-niego-przybywają), [27](04%20Konwersja%20CSV%20do%20TriG.md#27-jak-wgrasz-trig-do-datasetu-najpierw-ui-potem-http-tak-by-grafy-nazwane-zachowały-nazwy), [43](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#43-jak-wyślesz-zapytanie-do-endpointu-fuseki-i-odczytasz-wiązania-z-applicationsparql-resultsjson).

## graf nazwany

Osobny podgraf w datasecie, identyfikowany własnym IRI.

Pierwsza wzmianka: [rozdział 01, sekcja „Dataset biuro w przeglądarce”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce).
Występuje w: [01 › Dataset biuro w przeglądarce](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#dataset-biuro-w-przeglądarce), [02 › Dataset i grafy nazwane w TriG](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#dataset-i-grafy-nazwane-w-trig), [02 › IRI grafu a IRI wizyty](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#iri-grafu-a-iri-wizyty), [03 › Słowniki, przestrzenie i grafy modelu](03%20Model%20danych%20Biura.md#słowniki-przestrzenie-i-grafy-modelu), [04 › Jeden wiersz wizyty do TriG](04%20Konwersja%20CSV%20do%20TriG.md#jeden-wiersz-wizyty-do-trig), [05 › Zapytania w wybranym grafie](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zapytania-w-wybranym-grafie), [05 › Kontrola grafów po załadowaniu](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#kontrola-grafów-po-załadowaniu), [06 › Artefakt przed datą powstania](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#artefakt-przed-datą-powstania), [06 › Grafy nazwane czy jeden graf](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#grafy-nazwane-czy-jeden-graf), [07 › Kontrola grafów linii z Pythona](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#kontrola-grafów-linii-z-pythona), [07 › Od CSV do sześciu analiz](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#od-csv-do-sześciu-analiz).
Pytania: [3](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#3-jak-w-przeglądarce-utworzyć-trwały-dataset-i-jakie-endpointy-query-update-data-do-niego-przybywają), [6](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#6-jak-w-trig-zapisać-ten-sam-podmiot-w-dwóch-grafach-nazwanych-i-czym-dataset-różni-się-od-grafu), [8](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#8-czym-różni-się-iri-grafu-linii-czasu-od-iri-wizyty-i-jak-graf-nazwany-wiąże-dane-z-linią-czasu), [15](03%20Model%20danych%20Biura.md#15-jak-z-wybranych-słowników-własnego-namespace-i-podziału-na-grafy-złożysz-spójny-model-biura), [21](04%20Konwersja%20CSV%20do%20TriG.md#21-przeprowadź-jeden-wiersz-wizyty-przez-mapowanie-do-pełnych-trójek-i-zapisu-trig-w-grafie-linii-czasu), [32](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#32-jak-w-sparql-związać-nazwę-grafu-ze-zmienną-i-wykonać-zapytanie-w-jednym-wskazanym-grafie), [35](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#35-jakimi-zapytaniami-sprawdzisz-liczby-trójek-w-grafach-typy-i-obecność-metadanych-po-załadowaniu), [38](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#38-jak-wykryjesz-artefakt-pojawiający-się-przed-datą-powstania-lub-w-sprzecznych-liniach-czasu), [42](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#42-które-z-sześciu-analiz-użyją-grafów-nazwanych-a-które-danych-z-jednego-grafu-i-jak-je-odróżnisz-w-wynikach), [44](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#44-jak-potwierdzisz-że-wszystkie-linie-czasu-trafiły-do-właściwych-grafów-nazwanych), [45](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#45-opisz-cały-przepływ-od-csv-do-sześciu-interpretowanych-analiz-i-wskaż-gdzie-zapadają-decyzje-o-iri-grafach-i-słownikach).

## trójka

Podstawowa jednostka danych RDF: podmiot, orzeczenie i dopełnienie, czyli jedno zdanie o zasobie.

Pierwsza wzmianka: [rozdział 01, sekcja „Trójka, wiersz i prefiksy”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
Występuje w: [01 › Trójka, wiersz i prefiksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy), [04 › Jeden wiersz wizyty do TriG](04%20Konwersja%20CSV%20do%20TriG.md#jeden-wiersz-wizyty-do-trig), [05 › Wizyty podróżnika w SELECT](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#wizyty-podróżnika-w-select).
Pytania: [4](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#4-czym-jest-trójka-subject-predicate-object-jak-ma-się-do-wiersza-tabeli-i-po-co-są-prefiksy), [21](04%20Konwersja%20CSV%20do%20TriG.md#21-przeprowadź-jeden-wiersz-wizyty-przez-mapowanie-do-pełnych-trójek-i-zapisu-trig-w-grafie-linii-czasu), [29](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#29-jak-zapytasz-o-wizyty-podróżnika-ze-zmiennymi-wspólnym-podmiotem-i-prefix).

## IRI

Globalnie unikalny identyfikator zasobu, zapisywany w nawiasach <...>.

Pierwsza wzmianka: [rozdział 01, sekcja „Trójka, wiersz i prefiksy”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
Występuje w: [01 › Trójka, wiersz i prefiksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy), [02 › IRI grafu a IRI wizyty](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#iri-grafu-a-iri-wizyty), [02 › Kiedy zewnętrzny URI, a kiedy sameAs](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kiedy-zewnętrzny-uri-a-kiedy-sameas), [03 › Klucze jako IRI i połączenia](03%20Model%20danych%20Biura.md#klucze-jako-iri-i-połączenia), [03 › Znaki specjalne w kluczach IRI](03%20Model%20danych%20Biura.md#znaki-specjalne-w-kluczach-iri), [04 › Jeden wiersz wizyty do TriG](04%20Konwersja%20CSV%20do%20TriG.md#jeden-wiersz-wizyty-do-trig), [04 › Identyczny TriG w dwóch przebiegach](04%20Konwersja%20CSV%20do%20TriG.md#identyczny-trig-w-dwóch-przebiegach), [04 › Walidacja wynikowego grafu](04%20Konwersja%20CSV%20do%20TriG.md#walidacja-wynikowego-grafu), [07 › Od CSV do sześciu analiz](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#od-csv-do-sześciu-analiz).
Pytania: [4](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#4-czym-jest-trójka-subject-predicate-object-jak-ma-się-do-wiersza-tabeli-i-po-co-są-prefiksy), [8](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#8-czym-różni-się-iri-grafu-linii-czasu-od-iri-wizyty-i-jak-graf-nazwany-wiąże-dane-z-linią-czasu), [9](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#9-dlaczego-rozdzielasz-namespace-słownika-biura-od-iri-instancji-w-domenie-example-i-kiedy-wolno-użyć-zewnętrznego-uri-lub-owlsameas), [17](03%20Model%20danych%20Biura.md#17-jak-klucz-główny-zamieniasz-na-iri-zasobu-a-klucz-obcy-na-połączenie-i-dlaczego-nie-z-etykiety), [19](03%20Model%20danych%20Biura.md#19-jak-zakodujesz-w-iri-klucz-ze-spacją-lub-znakami-spoza-ascii-i-co-zapewnia-stabilność-identyfikatorów-między-przebiegami), [21](04%20Konwersja%20CSV%20do%20TriG.md#21-przeprowadź-jeden-wiersz-wizyty-przez-mapowanie-do-pełnych-trójek-i-zapisu-trig-w-grafie-linii-czasu), [24](04%20Konwersja%20CSV%20do%20TriG.md#24-co-sprawia-że-dwa-przebiegi-konwersji-dają-identyczny-plik-trig-kolejność-iri-brak-węzłów-pustych), [25](04%20Konwersja%20CSV%20do%20TriG.md#25-jak-wykryjesz-duplikaty-kluczy-klucze-obce-bez-rekordu-i-złe-typy-w-wynikowym-grafie-i-co-zrobisz-z-każdym), [45](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#45-opisz-cały-przepływ-od-csv-do-sześciu-interpretowanych-analiz-i-wskaż-gdzie-zapadają-decyzje-o-iri-grafach-i-słownikach).

## prefiks

Skrót przestrzeni nazw w zapisie, np. bpc: zastępuje wspólny początek IRI; w grafie zawsze jest pełne IRI.

Pierwsza wzmianka: [rozdział 01, sekcja „Trójka, wiersz i prefiksy”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
Występuje w: [01 › Trójka, wiersz i prefiksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy), [05 › Wizyty podróżnika w SELECT](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#wizyty-podróżnika-w-select).
Pytania: [4](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#4-czym-jest-trójka-subject-predicate-object-jak-ma-się-do-wiersza-tabeli-i-po-co-są-prefiksy), [29](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#29-jak-zapytasz-o-wizyty-podróżnika-ze-zmiennymi-wspólnym-podmiotem-i-prefix).

## Turtle

Czytelny tekstowy zapis trójek RDF z prefiksami, średnikiem i kropką.

Pierwsza wzmianka: [rozdział 01, sekcja „Trójka, wiersz i prefiksy”](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
Występuje w: [01 › Trójka, wiersz i prefiksy](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#trójka-wiersz-i-prefiksy).
Pytania: [4](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md#4-czym-jest-trójka-subject-predicate-object-jak-ma-się-do-wiersza-tabeli-i-po-co-są-prefiksy).

## literał

Wartość w dopełnieniu trójki: napis (forma leksykalna) z typem danych albo znacznikiem języka, a nie zasób z IRI.

Pierwsza wzmianka: [rozdział 02, sekcja „Literały: typ i język”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język).
Występuje w: [02 › Literały: typ i język](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język), [03 › Pusta komórka i zła data](03%20Model%20danych%20Biura.md#pusta-komórka-i-zła-data), [04 › Walidacja wynikowego grafu](04%20Konwersja%20CSV%20do%20TriG.md#walidacja-wynikowego-grafu).
Pytania: [5](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#5-czym-różni-się-2024-05-01xsddate-od-zwykłego-napisu-i-kiedy-stosuje-się-znacznik-języka-pl), [20](03%20Model%20danych%20Biura.md#20-jak-obsłużysz-pustą-komórkę-i-niepoprawną-datę-by-nie-powstał-literał-none-ani-zły-typ), [25](04%20Konwersja%20CSV%20do%20TriG.md#25-jak-wykryjesz-duplikaty-kluczy-klucze-obce-bez-rekordu-i-złe-typy-w-wynikowym-grafie-i-co-zrobisz-z-każdym).

## typ danych

IRI (zwykle z XSD, np. xsd:date) określający, jak interpretować napis literału.

Pierwsza wzmianka: [rozdział 02, sekcja „Literały: typ i język”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język).
Występuje w: [02 › Literały: typ i język](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język), [03 › Pusta komórka i zła data](03%20Model%20danych%20Biura.md#pusta-komórka-i-zła-data), [04 › Walidacja wynikowego grafu](04%20Konwersja%20CSV%20do%20TriG.md#walidacja-wynikowego-grafu).
Pytania: [5](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#5-czym-różni-się-2024-05-01xsddate-od-zwykłego-napisu-i-kiedy-stosuje-się-znacznik-języka-pl), [20](03%20Model%20danych%20Biura.md#20-jak-obsłużysz-pustą-komórkę-i-niepoprawną-datę-by-nie-powstał-literał-none-ani-zły-typ), [25](04%20Konwersja%20CSV%20do%20TriG.md#25-jak-wykryjesz-duplikaty-kluczy-klucze-obce-bez-rekordu-i-złe-typy-w-wynikowym-grafie-i-co-zrobisz-z-każdym).

## znacznik języka

Oznaczenie języka tekstu literału, np. @pl; literał ma typ albo znacznik, nigdy oba.

Pierwsza wzmianka: [rozdział 02, sekcja „Literały: typ i język”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język).
Występuje w: [02 › Literały: typ i język](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#literały-typ-i-język), [02 › Typy, etykiety, domain i range](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range).
Pytania: [5](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#5-czym-różni-się-2024-05-01xsddate-od-zwykłego-napisu-i-kiedy-stosuje-się-znacznik-języka-pl), [7](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#7-jak-użyć-rdftype-rdfsclass-rdfslabel-rdfsdomain-i-rdfsrange-i-czego-one-nie-walidują).

## TriG

Serializacja RDF będąca rozszerzeniem Turtle o bloki `<IRI grafu> { ... }`, które zapisują grafy nazwane w jednym pliku.

Pierwsza wzmianka: [rozdział 02, sekcja „Dataset i grafy nazwane w TriG”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#dataset-i-grafy-nazwane-w-trig).
Występuje w: [02 › Dataset i grafy nazwane w TriG](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#dataset-i-grafy-nazwane-w-trig), [03 › Słowniki, przestrzenie i grafy modelu](03%20Model%20danych%20Biura.md#słowniki-przestrzenie-i-grafy-modelu), [04 › Jeden wiersz wizyty do TriG](04%20Konwersja%20CSV%20do%20TriG.md#jeden-wiersz-wizyty-do-trig), [04 › Wgranie TriG z nazwami grafów](04%20Konwersja%20CSV%20do%20TriG.md#wgranie-trig-z-nazwami-grafów), [04 › Stabilny zapis pliku TriG](04%20Konwersja%20CSV%20do%20TriG.md#stabilny-zapis-pliku-trig).
Pytania: [6](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#6-jak-w-trig-zapisać-ten-sam-podmiot-w-dwóch-grafach-nazwanych-i-czym-dataset-różni-się-od-grafu), [15](03%20Model%20danych%20Biura.md#15-jak-z-wybranych-słowników-własnego-namespace-i-podziału-na-grafy-złożysz-spójny-model-biura), [21](04%20Konwersja%20CSV%20do%20TriG.md#21-przeprowadź-jeden-wiersz-wizyty-przez-mapowanie-do-pełnych-trójek-i-zapisu-trig-w-grafie-linii-czasu), [24](04%20Konwersja%20CSV%20do%20TriG.md#24-co-sprawia-że-dwa-przebiegi-konwersji-dają-identyczny-plik-trig-kolejność-iri-brak-węzłów-pustych), [27](04%20Konwersja%20CSV%20do%20TriG.md#27-jak-wgrasz-trig-do-datasetu-najpierw-ui-potem-http-tak-by-grafy-nazwane-zachowały-nazwy).

## RDFS

Słownik W3C z klasami, etykietami, domain i range do opisu danych RDF.

Pierwsza wzmianka: [rozdział 02, sekcja „Typy, etykiety, domain i range”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range).
Występuje w: [02 › Typy, etykiety, domain i range](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range), [02 › Kryterium wyboru terminów](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kryterium-wyboru-terminów), [02 › Kiedy zewnętrzny URI, a kiedy sameAs](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kiedy-zewnętrzny-uri-a-kiedy-sameas).
Pytania: [7](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#7-jak-użyć-rdftype-rdfsclass-rdfslabel-rdfsdomain-i-rdfsrange-i-czego-one-nie-walidują), [9](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#9-dlaczego-rozdzielasz-namespace-słownika-biura-od-iri-instancji-w-domenie-example-i-kiedy-wolno-użyć-zewnętrznego-uri-lub-owlsameas), [12](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#12-które-terminy-prov-o-owl-time-rdfs-i-xsd-użyjesz-w-biurze-które-odrzucisz-i-dlaczego).

## wnioskowanie

Automatyczne dopisywanie nowych trójek wynikających z reguł, np. typu zasobu z domain lub range własności.

Pierwsza wzmianka: [rozdział 02, sekcja „Typy, etykiety, domain i range”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range).
Występuje w: [02 › Typy, etykiety, domain i range](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range), [02 › Słownik bpc a IRI instancji](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#słownik-bpc-a-iri-instancji), [02 › Kiedy zewnętrzny URI, a kiedy sameAs](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kiedy-zewnętrzny-uri-a-kiedy-sameas).
Pytania: [7](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#7-jak-użyć-rdftype-rdfsclass-rdfslabel-rdfsdomain-i-rdfsrange-i-czego-one-nie-walidują), [9](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#9-dlaczego-rozdzielasz-namespace-słownika-biura-od-iri-instancji-w-domenie-example-i-kiedy-wolno-użyć-zewnętrznego-uri-lub-owlsameas).

## owl:sameAs

Własność OWL (http://www.w3.org/2002/07/owl#sameAs) twierdząca, że dwa IRI oznaczają tę samą rzecz; wnioskowanie przenosi wtedy fakty między nimi.

Pierwsza wzmianka: [rozdział 02, sekcja „Słownik bpc a IRI instancji”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#słownik-bpc-a-iri-instancji).
Występuje w: [02 › Słownik bpc a IRI instancji](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#słownik-bpc-a-iri-instancji).
Pytania: [9](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#9-dlaczego-rozdzielasz-namespace-słownika-biura-od-iri-instancji-w-domenie-example-i-kiedy-wolno-użyć-zewnętrznego-uri-lub-owlsameas).

## słownik

Zestaw klas i własności pod wspólnym prefiksem, np. bpc: jako własny słownik projektu.

Pierwsza wzmianka: [rozdział 02, sekcja „Kiedy zewnętrzny URI, a kiedy sameAs”](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kiedy-zewnętrzny-uri-a-kiedy-sameas).
Występuje w: [02 › Kiedy zewnętrzny URI, a kiedy sameAs](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#kiedy-zewnętrzny-uri-a-kiedy-sameas), [03 › Wiersz mapowania kolumn wizyty](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty), [07 › Od CSV do sześciu analiz](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#od-csv-do-sześciu-analiz).
Pytania: [9](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#9-dlaczego-rozdzielasz-namespace-słownika-biura-od-iri-instancji-w-domenie-example-i-kiedy-wolno-użyć-zewnętrznego-uri-lub-owlsameas), [18](03%20Model%20danych%20Biura.md#18-jak-dla-kolumn-wizyty-zapisać-wiersz-mapowania-subject-predicate-object-typ-rdf-słownik-i-uzasadnienie), [45](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#45-opisz-cały-przepływ-od-csv-do-sześciu-interpretowanych-analiz-i-wskaż-gdzie-zapadają-decyzje-o-iri-grafach-i-słownikach).

## OWL-Time

Słownik W3C do opisu czasu; time:Interval to przedział z początkiem i końcem, które są punktami na osi czasu.

Pierwsza wzmianka: [rozdział 03, sekcja „Klasy i własności Biura”](03%20Model%20danych%20Biura.md#klasy-i-własności-biura).
Występuje w: [03 › Klasy i własności Biura](03%20Model%20danych%20Biura.md#klasy-i-własności-biura), [03 › Słowniki, przestrzenie i grafy modelu](03%20Model%20danych%20Biura.md#słowniki-przestrzenie-i-grafy-modelu).
Pytania: [13](03%20Model%20danych%20Biura.md#13-jakie-klasy-i-własności-biura-zdefiniujesz-dla-podróżnika-wizyty-epoki-artefaktu-spotkania-i-raportu), [15](03%20Model%20danych%20Biura.md#15-jak-z-wybranych-słowników-własnego-namespace-i-podziału-na-grafy-złożysz-spójny-model-biura).

## węzeł zdarzenia

Zasób z własnym IRI reprezentujący zdarzenie (np. wizytę), który zbiera jego atrybuty i do którego mogą się odwoływać inne zasoby.

Pierwsza wzmianka: [rozdział 03, sekcja „Wizyta jako węzeł, nie trójka”](03%20Model%20danych%20Biura.md#wizyta-jako-węzeł-nie-trójka).
Występuje w: [03 › Wizyta jako węzeł, nie trójka](03%20Model%20danych%20Biura.md#wizyta-jako-węzeł-nie-trójka).
Pytania: [14](03%20Model%20danych%20Biura.md#14-kiedy-wizyta-lub-raport-mają-być-osobnym-zasobem-zamiast-pojedynczej-trójki-i-co-daje-taki-węzeł).

## relacja wielostronna

Fakt łączący więcej niż dwa elementy, którego nie da się zapisać jedną trójką.

Pierwsza wzmianka: [rozdział 03, sekcja „Wizyta jako węzeł, nie trójka”](03%20Model%20danych%20Biura.md#wizyta-jako-węzeł-nie-trójka).
Występuje w: [03 › Wizyta jako węzeł, nie trójka](03%20Model%20danych%20Biura.md#wizyta-jako-węzeł-nie-trójka).
Pytania: [14](03%20Model%20danych%20Biura.md#14-kiedy-wizyta-lub-raport-mają-być-osobnym-zasobem-zamiast-pojedynczej-trójki-i-co-daje-taki-węzeł).

## wiersz mapowania

Opis tego, co powstaje z jednej kolumny CSV: subject, predicate, object, typ RDF, słownik i uzasadnienie.

Pierwsza wzmianka: [rozdział 03, sekcja „Wiersz mapowania kolumn wizyty”](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty).
Występuje w: [03 › Wiersz mapowania kolumn wizyty](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty), [04 › Jeden wiersz wizyty do TriG](04%20Konwersja%20CSV%20do%20TriG.md#jeden-wiersz-wizyty-do-trig), [07 › Od CSV do sześciu analiz](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#od-csv-do-sześciu-analiz).
Pytania: [18](03%20Model%20danych%20Biura.md#18-jak-dla-kolumn-wizyty-zapisać-wiersz-mapowania-subject-predicate-object-typ-rdf-słownik-i-uzasadnienie), [21](04%20Konwersja%20CSV%20do%20TriG.md#21-przeprowadź-jeden-wiersz-wizyty-przez-mapowanie-do-pełnych-trójek-i-zapisu-trig-w-grafie-linii-czasu), [45](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#45-opisz-cały-przepływ-od-csv-do-sześciu-interpretowanych-analiz-i-wskaż-gdzie-zapadają-decyzje-o-iri-grafach-i-słownikach).

## tabela mapowania

Lista wierszy mapowania dla jednego pliku CSV, z której konwerter buduje trójki.

Pierwsza wzmianka: [rozdział 03, sekcja „Wiersz mapowania kolumn wizyty”](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty).
Występuje w: [03 › Wiersz mapowania kolumn wizyty](03%20Model%20danych%20Biura.md#wiersz-mapowania-kolumn-wizyty), [04 › Od CSV do zwalidowanego TriG](04%20Konwersja%20CSV%20do%20TriG.md#od-csv-do-zwalidowanego-trig).
Pytania: [18](03%20Model%20danych%20Biura.md#18-jak-dla-kolumn-wizyty-zapisać-wiersz-mapowania-subject-predicate-object-typ-rdf-słownik-i-uzasadnienie), [26](04%20Konwersja%20CSV%20do%20TriG.md#26-jak-od-csv-dojdziesz-do-zwalidowanego-trig-z-provenance-i-jak-powtórzysz-przebieg-z-identycznym-wynikiem).

## kodowanie procentowe

Zapis bajtu jako % i dwóch cyfr szesnastkowych, którym w IRI oznacza się znaki spoza bezpiecznego zestawu, np. spację jako %20.

Pierwsza wzmianka: [rozdział 03, sekcja „Znaki specjalne w kluczach IRI”](03%20Model%20danych%20Biura.md#znaki-specjalne-w-kluczach-iri).
Występuje w: [03 › Znaki specjalne w kluczach IRI](03%20Model%20danych%20Biura.md#znaki-specjalne-w-kluczach-iri).
Pytania: [19](03%20Model%20danych%20Biura.md#19-jak-zakodujesz-w-iri-klucz-ze-spacją-lub-znakami-spoza-ascii-i-co-zapewnia-stabilność-identyfikatorów-między-przebiegami).

## PROV-O

Słownik W3C do opisu pochodzenia danych: kto, z czego i kiedy je wytworzył, za pomocą klas Activity, Agent i Entity.

Pierwsza wzmianka: [rozdział 04, sekcja „Konwersja CSV w PROV-O”](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o).
Występuje w: [04 › Konwersja CSV w PROV-O](04%20Konwersja%20CSV%20do%20TriG.md#konwersja-csv-w-prov-o), [04 › Od CSV do zwalidowanego TriG](04%20Konwersja%20CSV%20do%20TriG.md#od-csv-do-zwalidowanego-trig), [06 › Raport sprzeczny z danymi wizyty](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#raport-sprzeczny-z-danymi-wizyty).
Pytania: [22](04%20Konwersja%20CSV%20do%20TriG.md#22-jak-opiszesz-aktywność-konwersji-csv-jej-agenta-i-wygenerowane-dane-za-pomocą-prov-o), [26](04%20Konwersja%20CSV%20do%20TriG.md#26-jak-od-csv-dojdziesz-do-zwalidowanego-trig-z-provenance-i-jak-powtórzysz-przebieg-z-identycznym-wynikiem), [41](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#41-jak-wykryjesz-raport-agenta-który-opisuje-wizytę-lub-spotkanie-sprzecznie-z-danymi-i-jak-prov-o-pomaga-ustalić-źródło).

## rdflib

Biblioteka Pythona do budowania, parsowania i zapisu grafów RDF oraz datasetów, także w formacie TriG.

Pierwsza wzmianka: [rozdział 04, sekcja „Dataset rdflib i zapis TriG”](04%20Konwersja%20CSV%20do%20TriG.md#dataset-rdflib-i-zapis-trig).
Występuje w: [04 › Dataset rdflib i zapis TriG](04%20Konwersja%20CSV%20do%20TriG.md#dataset-rdflib-i-zapis-trig), [04 › Stabilny zapis pliku TriG](04%20Konwersja%20CSV%20do%20TriG.md#stabilny-zapis-pliku-trig).
Pytania: [23](04%20Konwersja%20CSV%20do%20TriG.md#23-jak-w-venv-dodasz-trójki-do-dataset-w-grafie-nazwanym-i-zapiszesz-go-jako-trig), [24](04%20Konwersja%20CSV%20do%20TriG.md#24-co-sprawia-że-dwa-przebiegi-konwersji-dają-identyczny-plik-trig-kolejność-iri-brak-węzłów-pustych).

## węzeł pusty

Zasób RDF bez IRI, zapisywany w Turtle i TriG jako [ ... ]; rdflib nadaje mu przy każdym przebiegu nowy identyfikator.

Pierwsza wzmianka: [rozdział 04, sekcja „Identyczny TriG w dwóch przebiegach”](04%20Konwersja%20CSV%20do%20TriG.md#identyczny-trig-w-dwóch-przebiegach).
Występuje w: [04 › Identyczny TriG w dwóch przebiegach](04%20Konwersja%20CSV%20do%20TriG.md#identyczny-trig-w-dwóch-przebiegach), [04 › Od CSV do zwalidowanego TriG](04%20Konwersja%20CSV%20do%20TriG.md#od-csv-do-zwalidowanego-trig), [04 › Stabilny zapis pliku TriG](04%20Konwersja%20CSV%20do%20TriG.md#stabilny-zapis-pliku-trig).
Pytania: [24](04%20Konwersja%20CSV%20do%20TriG.md#24-co-sprawia-że-dwa-przebiegi-konwersji-dają-identyczny-plik-trig-kolejność-iri-brak-węzłów-pustych), [26](04%20Konwersja%20CSV%20do%20TriG.md#26-jak-od-csv-dojdziesz-do-zwalidowanego-trig-z-provenance-i-jak-powtórzysz-przebieg-z-identycznym-wynikiem).

## graf domyślny

Graf datasetu bez nazwy, do którego trafiają trójki załadowane bez wskazania grafu; zapytanie bez FROM i GRAPH widzi w Fuseki tylko jego.

Pierwsza wzmianka: [rozdział 05, sekcja „Wizyty podróżnika w SELECT”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#wizyty-podróżnika-w-select).
Występuje w: [05 › Wizyty podróżnika w SELECT](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#wizyty-podróżnika-w-select), [05 › Zapytania w wybranym grafie](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zapytania-w-wybranym-grafie), [06 › Łańcuch spotkań między podróżnikami](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#łańcuch-spotkań-między-podróżnikami), [06 › Artefakt przed datą powstania](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#artefakt-przed-datą-powstania), [06 › Grafy nazwane czy jeden graf](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#grafy-nazwane-czy-jeden-graf), [07 › Kontrola grafów linii z Pythona](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#kontrola-grafów-linii-z-pythona).
Pytania: [29](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#29-jak-zapytasz-o-wizyty-podróżnika-ze-zmiennymi-wspólnym-podmiotem-i-prefix), [32](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#32-jak-w-sparql-związać-nazwę-grafu-ze-zmienną-i-wykonać-zapytanie-w-jednym-wskazanym-grafie), [37](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#37-jak-zapytaniem-znajdziesz-łańcuch-spotkań-łączący-dwóch-podróżników-i-czego-ścieżka-nie-powie-o-kolejności), [38](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#38-jak-wykryjesz-artefakt-pojawiający-się-przed-datą-powstania-lub-w-sprzecznych-liniach-czasu), [42](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#42-które-z-sześciu-analiz-użyją-grafów-nazwanych-a-które-danych-z-jednego-grafu-i-jak-je-odróżnisz-w-wynikach), [44](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#44-jak-potwierdzisz-że-wszystkie-linie-czasu-trafiły-do-właściwych-grafów-nazwanych).

## FILTER

Warunek w klauzuli WHERE zapytania SPARQL, który odrzuca podstawienia, dla których wyrażenie daje fałsz albo błąd.

Pierwsza wzmianka: [rozdział 05, sekcja „Daty w FILTER i literały o złym typie”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#daty-w-filter-i-literały-o-złym-typie).
Występuje w: [05 › Daty w FILTER i literały o złym typie](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#daty-w-filter-i-literały-o-złym-typie), [05 › Nakładające się wizyty w dwóch liniach](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#nakładające-się-wizyty-w-dwóch-liniach), [06 › Łańcuch spotkań między podróżnikami](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#łańcuch-spotkań-między-podróżnikami), [06 › Artefakt przed datą powstania](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#artefakt-przed-datą-powstania).
Pytania: [30](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#30-jak-porównasz-daty-typu-xsddate-w-filter-i-co-się-dzieje-z-literałem-o-złym-typie), [36](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#36-jak-zapytaniem-znajdziesz-podróżnika-który-w-dwóch-liniach-czasu-ma-nakładające-się-wizyty-i-jak-zinterpretujesz-wynik), [37](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#37-jak-zapytaniem-znajdziesz-łańcuch-spotkań-łączący-dwóch-podróżników-i-czego-ścieżka-nie-powie-o-kolejności), [38](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#38-jak-wykryjesz-artefakt-pojawiający-się-przed-datą-powstania-lub-w-sprzecznych-liniach-czasu).

## błąd typu

Wynik operacji na wartościach niepasujących typów, np. porównania daty z napisem; w FILTER działa jak fałsz, bez komunikatu.

Pierwsza wzmianka: [rozdział 05, sekcja „Daty w FILTER i literały o złym typie”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#daty-w-filter-i-literały-o-złym-typie).
Występuje w: [05 › Daty w FILTER i literały o złym typie](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#daty-w-filter-i-literały-o-złym-typie).
Pytania: [30](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#30-jak-porównasz-daty-typu-xsddate-w-filter-i-co-się-dzieje-z-literałem-o-złym-typie).

## OPTIONAL

Wzorzec SPARQL dołączający dane, jeśli istnieją; przy braku dopasowania wiersz zostaje, a zmienne pozostają niezwiązane (jak LEFT JOIN).

Pierwsza wzmianka: [rozdział 05, sekcja „OPTIONAL a FILTER NOT EXISTS”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#optional-a-filter-not-exists).
Występuje w: [05 › OPTIONAL a FILTER NOT EXISTS](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#optional-a-filter-not-exists).
Pytania: [31](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#31-czym-różni-się-optional-od-filter-not-exists-i-kiedy-każdy-służy-do-szukania-braków).

## FILTER NOT EXISTS

Warunek odrzucający wiersze, dla których podany wzorzec ma dopasowanie; niczego nie wiąże.

Pierwsza wzmianka: [rozdział 05, sekcja „OPTIONAL a FILTER NOT EXISTS”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#optional-a-filter-not-exists).
Występuje w: [05 › OPTIONAL a FILTER NOT EXISTS](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#optional-a-filter-not-exists), [05 › Kontrola grafów po załadowaniu](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#kontrola-grafów-po-załadowaniu), [06 › Spotkanie bez wizyty i wizyta bez powiązania](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#spotkanie-bez-wizyty-i-wizyta-bez-powiązania), [06 › Wspólne i tylko w jednej linii](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#wspólne-i-tylko-w-jednej-linii).
Pytania: [31](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#31-czym-różni-się-optional-od-filter-not-exists-i-kiedy-każdy-służy-do-szukania-braków), [35](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#35-jakimi-zapytaniami-sprawdzisz-liczby-trójek-w-grafach-typy-i-obecność-metadanych-po-załadowaniu), [39](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#39-jak-zapytaniem-znajdziesz-spotkanie-bez-odpowiadającej-wizyty-lub-wizytę-bez-powiązania-i-jak-odróżnić-brak-od-błędu-danych), [40](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#40-jak-porównasz-zdarzenia-dwóch-linii-czasu-wskazując-wspólne-i-występujące-tylko-w-jednej).

## GROUP BY

Klauzula SPARQL, która skleja wiersze wyniku w grupy o tych samych wartościach wskazanych zmiennych, aby agregacje liczyły się osobno w każdej grupie.

Pierwsza wzmianka: [rozdział 05, sekcja „Zliczanie zdarzeń w grafach i HAVING”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zliczanie-zdarzeń-w-grafach-i-having).
Występuje w: [05 › Zliczanie zdarzeń w grafach i HAVING](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zliczanie-zdarzeń-w-grafach-i-having), [05 › Kontrola grafów po załadowaniu](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#kontrola-grafów-po-załadowaniu).
Pytania: [33](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#33-jak-policzysz-zdarzenia-w-każdym-grafie-i-odfiltrujesz-grupy-warunkiem-having), [35](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#35-jakimi-zapytaniami-sprawdzisz-liczby-trójek-w-grafach-typy-i-obecność-metadanych-po-załadowaniu).

## funkcja agregująca

Funkcja, np. COUNT, SUM czy MAX, która z wielu wierszy grupy wylicza jedną wartość.

Pierwsza wzmianka: [rozdział 05, sekcja „Zliczanie zdarzeń w grafach i HAVING”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zliczanie-zdarzeń-w-grafach-i-having).
Występuje w: [05 › Zliczanie zdarzeń w grafach i HAVING](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zliczanie-zdarzeń-w-grafach-i-having), [05 › Kontrola grafów po załadowaniu](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#kontrola-grafów-po-załadowaniu).
Pytania: [33](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#33-jak-policzysz-zdarzenia-w-każdym-grafie-i-odfiltrujesz-grupy-warunkiem-having), [35](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#35-jakimi-zapytaniami-sprawdzisz-liczby-trójek-w-grafach-typy-i-obecność-metadanych-po-załadowaniu).

## HAVING

Klauzula SPARQL, która po grupowaniu zostawia tylko te grupy, których wynik agregacji spełnia warunek.

Pierwsza wzmianka: [rozdział 05, sekcja „Zliczanie zdarzeń w grafach i HAVING”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zliczanie-zdarzeń-w-grafach-i-having).
Występuje w: [05 › Zliczanie zdarzeń w grafach i HAVING](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#zliczanie-zdarzeń-w-grafach-i-having).
Pytania: [33](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#33-jak-policzysz-zdarzenia-w-każdym-grafie-i-odfiltrujesz-grupy-warunkiem-having).

## ścieżka własności

Wyrażenie w miejscu orzeczenia wzorca trójek, które łączy własności operatorami, np. /, + i *, i opisuje trasę przez wiele trójek.

Pierwsza wzmianka: [rozdział 05, sekcja „Ścieżki o zmiennej długości”](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#ścieżki-o-zmiennej-długości).
Występuje w: [05 › Ścieżki o zmiennej długości](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#ścieżki-o-zmiennej-długości), [06 › Łańcuch spotkań między podróżnikami](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#łańcuch-spotkań-między-podróżnikami).
Pytania: [34](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md#34-jak-operatory--i--oraz--w-ścieżce-własności-znajdują-połączenia-o-zmiennej-długości), [37](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#37-jak-zapytaniem-znajdziesz-łańcuch-spotkań-łączący-dwóch-podróżników-i-czego-ścieżka-nie-powie-o-kolejności).

## BIND

Element wzorca SPARQL, który przypisuje wartość wyrażenia nowej zmiennej: BIND(wyrażenie AS ?zmienna). Bywa używany do nadania wierszowi stałej etykiety.

Pierwsza wzmianka: [rozdział 06, sekcja „Wspólne i tylko w jednej linii”](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#wspólne-i-tylko-w-jednej-linii).
Występuje w: [06 › Wspólne i tylko w jednej linii](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#wspólne-i-tylko-w-jednej-linii).
Pytania: [40](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md#40-jak-porównasz-zdarzenia-dwóch-linii-czasu-wskazując-wspólne-i-występujące-tylko-w-jednej).

## application/sparql-results+json

Standardowy format JSON odpowiedzi na zapytania SPARQL SELECT i ASK: SELECT ma head.vars i results.bindings, ASK pole boolean.

Pierwsza wzmianka: [rozdział 07, sekcja „Zapytanie SPARQL przez HTTP”](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#zapytanie-sparql-przez-http).
Występuje w: [07 › Zapytanie SPARQL przez HTTP](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#zapytanie-sparql-przez-http).
Pytania: [43](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#43-jak-wyślesz-zapytanie-do-endpointu-fuseki-i-odczytasz-wiązania-z-applicationsparql-resultsjson).

## ASK

Postać zapytania SPARQL, która sprawdza, czy wzorzec ma dopasowanie, i zwraca tylko true albo false.

Pierwsza wzmianka: [rozdział 07, sekcja „Zapytanie SPARQL przez HTTP”](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#zapytanie-sparql-przez-http).
Występuje w: [07 › Zapytanie SPARQL przez HTTP](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#zapytanie-sparql-przez-http).
Pytania: [43](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md#43-jak-wyślesz-zapytanie-do-endpointu-fuseki-i-odczytasz-wiązania-z-applicationsparql-resultsjson).
