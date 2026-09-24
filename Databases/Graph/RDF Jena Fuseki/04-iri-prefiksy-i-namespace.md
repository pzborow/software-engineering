# IRI, prefiksy i namespace

## Opis

IRI nadaje zasobom identyfikatory. Prefiksy i namespace skracają zapis oraz pomagają utrzymać spójne nazewnictwo, ale nie zmieniają znaczenia pełnego IRI.

## Kluczowe koncepty

- **IRI** — Internationalized Resource Identifier.
- **Namespace** — wspólna przestrzeń nazw.
- **Prefix** — skrót namespace.
- **Vocabularium** — zbiór nazw używanych do opisu danych.
- **Pełny IRI** — jednoznaczny identyfikator zasobu.

## Key points

- Prefiks jest tylko skrótem dla czytelnika.
- Dwa różne prefiksy mogą wskazywać ten sam namespace.
- Stabilne IRI są ważniejsze niż ładne skróty.
- Warto wybierać nazwy opisujące znaczenie.
- Namespace pomaga unikać kolizji nazw.

## Example

```turtle
@prefix ex: <https://example.org/> .
ex:alice ex:name "Alice" .
```

To odpowiada pełnemu zapisowi `https://example.org/alice` i `https://example.org/name`.

## Dodatkowe wyjaśnienie

Prefiks nie zmienia semantyki zasobu — tylko skraca zapis. Kluczowe jest to, że pełne IRI pozostaje stabilne i jednoznaczne. Namespace pomaga unikać kolizji nazw, ale nie zastępuje sensownego projektowania identyfikatorów. Gdy w różnych zbiorach danych pojawia się ten sam fragment nazwy, to przestrzeń nazw rozdziela je i pozwala zachować spójność połączeń między grafami.

## Pełny flow

1. Wybieramy namespace.
2. Nadajemy mu prefiks.
3. Używamy prefiksu w Turtle i SPARQL.
4. Zachowujemy spójność nazw.
5. Dokumentujemy używane vocabularia.

## Pytania

1. Do czego służy IRI?
2. Czym jest namespace?
3. Czym jest prefiks?
4. Czy prefiks zmienia znaczenie IRI?
5. Po co unikać kolizji nazw?
6. Czy dwa prefiksy mogą wskazywać ten sam namespace?
7. Co jest ważniejsze: prefiks czy pełne IRI?
8. Czym jest vocabularium?
9. Gdzie często definiuje się prefiksy?
10. Jaki jest cel spójnego nazewnictwa?

## Odpowiedzi

1. Do jednoznacznego identyfikowania zasobu.
2. Wspólną przestrzenią nazw.
3. Skrótem namespace.
4. Nie.
5. Aby różne pojęcia nie miały przypadkiem tej samej nazwy.
6. Tak.
7. Pełne IRI.
8. Zbiorem nazw i pojęć.
9. W Turtle i zapytaniach SPARQL.
10. Czytelność i jednoznaczność danych.

[Powrót do spisu treści](README.md)
