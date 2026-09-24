# Graf RDF

## Opis

Graf RDF składa się z węzłów i krawędzi wynikających z trójek. Węzły są zasobami lub wartościami, a predicate określa znaczenie połączenia.

## Kluczowe koncepty

- **Węzeł** — subject albo object będący zasobem.
- **Krawędź** — predicate łączący węzły.
- **Graf domyślny** — podstawowy zbiór trójek.
- **Graf nazwany** — graf mający własną nazwę.
- **Dataset** — zbiór grafów.

## Key points

- Ta sama informacja może być częścią większej sieci powiązań.
- Graf dobrze reprezentuje relacje wielopoziomowe.
- Dataset może zawierać wiele grafów.
- Graf nazwany pozwala rozdzielać źródła lub konteksty.
- SPARQL może pytać jeden graf albo cały dataset.

## Example

```text
alice --knows--> bob
bob   --worksAt--> company
```

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Zapisujemy trójki.
2. Łączymy zasoby przez predicate.
3. Grupujemy trójki w graf.
4. Rozdzielamy grafy nazwane, jeśli potrzebujemy kontekstu.
5. Odpy­tujemy graf lub dataset.

## Pytania

1. Z czego składa się graf RDF?
2. Co jest krawędzią grafu?
3. Co jest węzłem?
4. Czym jest graf domyślny?
5. Czym jest graf nazwany?
6. Czym jest dataset?
7. Po co rozdzielać grafy nazwane?
8. Czy graf RDF może mieć wiele poziomów relacji?
9. Co łączy dwa zasoby?
10. Czym różni się graf od pojedynczej trójki?

## Odpowiedzi

1. Z węzłów i relacji.
2. Predicate.
3. Zasób reprezentowany przez IRI lub blank node.
4. Podstawowy zbiór trójek.
5. Graf z własnym identyfikatorem.
6. Zbiorem grafów.
7. Dla kontekstu, źródła lub organizacji danych.
8. Tak.
9. Relacja zapisana jako predicate.
10. Graf zawiera wiele połączonych trójek.

[Powrót do spisu treści](README.md)
