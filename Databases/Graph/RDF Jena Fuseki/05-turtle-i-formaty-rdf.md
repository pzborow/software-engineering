# Turtle i formaty RDF

## Opis

RDF można zapisywać w wielu serializacjach. Turtle jest czytelny dla człowieka, a RDF/XML, N-Triples, JSON-LD i TriG służą do wymiany danych w różnych zastosowaniach.

## Kluczowe koncepty

- **Turtle** — zwięzła serializacja RDF.
- **N-Triples** — prosty zapis jednej trójki w jednej linii.
- **RDF/XML** — XML-owa serializacja RDF.
- **JSON-LD** — zapis RDF w stylu JSON.
- **TriG** — zapis grafów nazwanych i quadów.

## Key points

- Format zapisu nie zmienia modelu RDF.
- Turtle jest dobry do nauki i ręcznej edycji.
- N-Triples ułatwia proste przetwarzanie liniowe.
- JSON-LD pasuje do środowisk pracujących z JSON.
- Fuseki i RDFLib potrafią pracować z kilkoma formatami.

## Example

```turtle
@prefix ex: <https://example.org/> .
ex:alice ex:knows ex:bob ;
         ex:name "Alice" .
```

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Wybieramy format wejściowy.
2. Parsujemy dane do grafu RDF.
3. Sprawdzamy poprawność składni.
4. Pracujemy na modelu grafowym.
5. Serializujemy wynik do formatu odbiorcy.

## Pytania

1. Czym jest Turtle?
2. Czy format zmienia model RDF?
3. Do czego pasuje N-Triples?
4. Do czego pasuje JSON-LD?
5. Czym jest TriG?
6. Czy Turtle jest czytelny dla człowieka?
7. Po co serializować RDF?
8. Jaki format jest dobry do nauki?
9. Czym różni się parser od serializera?
10. Czy Fuseki obsługuje jeden format?

## Odpowiedzi

1. Czytelną serializacją RDF.
2. Nie.
3. Do prostego zapisu trójek linia po linii.
4. Do integracji z JSON i aplikacjami webowymi.
5. Formatem dla grafów nazwanych i quadów.
6. Tak.
7. Do wymiany lub zapisania danych.
8. Turtle.
9. Parser odczytuje format, a serializer go tworzy.
10. Nie, może pracować z wieloma formatami.

[Powrót do spisu treści](README.md)
