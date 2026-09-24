# Python i RDFLib

## Opis

RDFLib to biblioteka Pythona do tworzenia, parsowania, serializowania i odpytywania grafów RDF. Jest wygodna do nauki, testów oraz lokalnego przygotowywania danych.

## Kluczowe koncepty

- **Graph** — lokalny graf RDF.
- **URIRef** — zasób identyfikowany IRI.
- **Literal** — wartość RDF.
- **Namespace** — wygodna praca z prefiksami.
- **parse/serialize** — odczyt i zapis serializacji.

## Key points

- Instalacja: `pip install rdflib`.
- Trójkę dodaje się jako `(subject, predicate, object)`.
- Graf można parsować z Turtle i serializować do Turtle.
- RDFLib ma własną obsługę zapytań SPARQL.
- Lokalny graf nie jest automatycznie zdalnym Fuseki.

## Example

```python
from rdflib import Graph, Literal, Namespace

EX = Namespace("https://example.org/")
g = Graph()
g.add((EX.alice, EX.name, Literal("Alice")))
print(g.serialize(format="turtle"))
```

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Tworzymy środowisko Python.
2. Instalujemy `rdflib`.
3. Tworzymy `Graph`.
4. Dodajemy lub parsujemy trójki.
5. Wykonujemy lokalne zapytanie SPARQL.
6. Serializujemy wynik albo wysyłamy dane do Fuseki.

## Pytania

1. Czym jest RDFLib?
2. Jak ją zainstalować?
3. Czym jest Graph?
4. Jak reprezentowana jest trójka w Pythonie?
5. Do czego służy URIRef?
6. Do czego służy Literal?
7. Jak parsować plik RDF?
8. Jak serializować graf?
9. Czy RDFLib jest Fuseki?
10. Do czego używa się RDFLib?

## Odpowiedzi

1. Biblioteką Pythona do pracy z RDF.
2. `pip install rdflib`.
3. Lokalnym grafem RDF.
4. Krotką `(subject, predicate, object)`.
5. Do reprezentowania IRI.
6. Do reprezentowania wartości.
7. Przez `Graph.parse()`.
8. Przez `Graph.serialize()`.
9. Nie, jest biblioteką klienta i grafu lokalnego.
10. Do nauki, testów, konwersji i przygotowania danych.

[Powrót do spisu treści](README.md)
