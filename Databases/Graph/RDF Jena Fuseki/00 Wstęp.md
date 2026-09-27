# Jena Fuseki i grafy RDF w praktyce

Jena Fuseki to serwer HTTP, który przechowuje dane jako proste fakty typu „Ala – pracuje w – Firma X” zamiast wierszy w tabelach, więc łatwo połączyć informacje z wielu źródeł i wychwycić sprzeczności, które w relacyjnej bazie giną między kluczami obcymi. W tym dziale uruchomisz serwer, zobaczysz na przykładowych tabelach, jakie pytania zadaje fikcyjne biuro analizujące dane, i przeniesiesz wiersze do modelu faktów; te trzy wątki spina jedna droga od tabeli do zapytań przez HTTP. Po tym dziale uruchomisz Fuseki na Javie 17, utworzysz w przeglądarce osobną bazę zapisywaną na dysku, która przetrwa restart serwera, i wskażesz adresy URL, pod którymi serwer przyjmuje odczyt, modyfikację i wgrywanie danych.

## Dla kogo

- Perspektywa: programista Python (backend), poziom: mid.
- Zakładamy, że znasz: Python: klasy, funkcje, moduły, with; HTTP, REST i JSON; relacyjna baza i SQL.
- Przykłady kodu: python, bash, sparql, turtle.

## Czego się nauczysz

Działy: 7 · pytania: 45. Na końcu każdego działu są „Co zapamiętać” i pytania sprawdzające z ukrytymi odpowiedziami.

1. [Serwer Fuseki i pytania Biura](01%20Serwer%20Fuseki%20i%20pytania%20Biura.md): sekcje: 5, pytania: 4
2. [Podstawy RDF, RDFS i słowników](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md): sekcje: 10, pytania: 8
3. [Model danych Biura](03%20Model%20danych%20Biura.md): sekcje: 8, pytania: 8
4. [Konwersja CSV do TriG](04%20Konwersja%20CSV%20do%20TriG.md): sekcje: 9, pytania: 8
5. [SPARQL SELECT i wzorce trójek](05%20SPARQL%20SELECT%20i%20wzorce%20tr%C3%B3jek.md): sekcje: 8, pytania: 8
6. [Analizy paradoksów w SPARQL](06%20Analizy%20paradoks%C3%B3w%20w%20SPARQL.md): sekcje: 6, pytania: 6
7. [Graf wiedzy Biura Paradoksów Czasowych](07%20Graf%20wiedzy%20Biura%20Paradoks%C3%B3w%20Czasowych.md): sekcje: 3, pytania: 3

## Przykład przewodni

**Biuro Paradoksów Czasowych.** Fikcyjne Biuro Paradoksów Czasowych zbiera dane o podróżnikach, wizytach, epokach, artefaktach, spotkaniach i raportach agentów z wielu linii czasu. Dane z CSV trafiają jako RDF do datasetu Fuseki, a sześć analiz SPARQL wykrywa w nich sprzeczności. [Stan i plan przyrostów](99%20Przyk%C5%82ad%20przewodni.md).

## Wersje

Przykłady opierają się na: Apache Jena Fuseki 5.x, Java 17, SPARQL 1.1, rdflib 7.x, Python 3.12. Szczegóły i źródła: [Wersje i źródła](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md).

## Pomocnicze strony

- [Ściągawka](96%20%C5%9Aci%C4%85gawka.md): najważniejsze rzeczy na jednej stronie.
- [Glosariusz](00%20Glosariusz.md): krótkie definicje pojęć z linkami do miejsc użycia.
- [Pułapki](98%20Pu%C5%82apki.md): nieoczywiste zachowania z przykładów.
- [Wersje i źródła](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md): od czego zależą przykłady i gdzie to potwierdzono.
- [Przykład przewodni](99%20Przyk%C5%82ad%20przewodni.md): cały wątek w jednym miejscu.
- [Raport pokrycia](raport-pokrycia.md): jak powstał tutorial i co zostało do redakcji.
