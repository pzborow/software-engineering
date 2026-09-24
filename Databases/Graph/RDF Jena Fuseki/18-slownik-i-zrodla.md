# Słownik i źródła

## Opis

Ten rozdział zbiera najważniejsze skróty i miejsca, do których warto wracać. Najlepszym źródłem standardów są materiały W3C, a dokumentacji narzędzi należy szukać u ich autorów.

## Kluczowe koncepty

- **RDF** — model trójek.
- **IRI** — identyfikator zasobu.
- **Literal** — wartość danych.
- **Turtle** — serializacja RDF.
- **SPARQL** — język zapytań.
- **Fuseki** — serwer SPARQL Apache Jena.
- **RDFLib** — biblioteka Pythona.
- **SHACL** — walidacja grafu.

## Key points

- RDF i SPARQL: standardy W3C.
- Fuseki: `jena.apache.org/documentation/fuseki2/`.
- Apache Jena: `jena.apache.org/documentation/`.
- RDFLib: `rdflib.readthedocs.io/`.
- SHACL: `w3.org/TR/shacl/`.
- Warto sprawdzać wersję dokumentacji zgodną z używanym wydaniem.

## Example

Przy problemie z zapytaniem kolejność szukania to: własny mały przykład, dokumentacja SPARQL, dokumentacja Fuseki, a następnie standard W3C.

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Nazywamy problem właściwym terminem.
2. Sprawdzamy dokumentację narzędzia.
3. Porównujemy zachowanie ze standardem.
4. Tworzymy minimalny test.
5. Zapisujemy rozwiązanie i wersję narzędzia.

## Pytania

1. Gdzie szukać standardu RDF?
2. Gdzie szukać standardu SPARQL?
3. Czym jest Fuseki?
4. Czym jest RDFLib?
5. Czym jest SHACL?
6. Gdzie szukać dokumentacji Apache Jena?
7. Gdzie szukać dokumentacji RDFLib?
8. Dlaczego ważna jest wersja dokumentacji?
9. Po co tworzyć minimalny przykład?
10. Czy słownik zastępuje praktykę?

## Odpowiedzi

1. W dokumentacji W3C.
2. W dokumentacji W3C.
3. Serwerem SPARQL Apache Jena.
4. Biblioteką Pythona do RDF.
5. Językiem walidacji RDF.
6. Na stronie Apache Jena.
7. W dokumentacji RDFLib.
8. API i zachowanie mogą się zmieniać.
9. Aby odizolować problem.
10. Nie, trzeba ćwiczyć na danych i zapytaniach.

[Powrót do spisu treści](README.md)
