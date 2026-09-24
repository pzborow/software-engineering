# Czym jest RDF

## Opis

RDF (Resource Description Framework) to model opisywania informacji jako relacji między zasobami. Zamiast myśleć wyłącznie o tabelach lub dokumentach, opisujemy fakty w postaci trójek.

## Kluczowe koncepty

- **RDF** — model danych oparty na relacjach.
- **Zasób** — rzecz, którą można opisać.
- **Trójka** — subject, predicate, object.
- **Graf** — zbiór połączonych trójek.
- **SPARQL** — język zapytań do grafów RDF.

## Key points

- RDF opisuje fakty, a nie tylko strukturę przechowywania.
- Relacja jest jawnie zapisana jako predicate.
- Zasoby mogą być łączone także między systemami.
- RDF jest modelem; Fuseki jest serwerem, który może go udostępniać.

## Example

```text
<https://example.org/alice> <https://example.org/knows> <https://example.org/bob> .
```

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Wybieramy zasoby.
2. Nadajemy relacjom nazwy.
3. Zapisujemy fakty jako trójki.
4. Łączymy trójki w graf.
5. Odpy­tujemy graf przez SPARQL.

## Pytania

1. Czym jest RDF?
2. Co opisuje RDF?
3. Z czego składa się podstawowy fakt RDF?
4. Czym jest graf RDF?
5. Do czego służy SPARQL?
6. Czy RDF jest bazą danych?
7. Czym jest zasób?
8. Co daje jawne zapisanie relacji?
9. Czym różni się RDF od Fuseki?
10. Jaki jest podstawowy cel RDF?

## Odpowiedzi

1. Modelem opisu informacji jako relacji.
2. Zasoby i związki między nimi.
3. Z subject, predicate i object.
4. Zbiorem połączonych trójek.
5. Do zapytań i modyfikacji grafów.
6. Nie, jest modelem danych.
7. Rzeczą, którą można opisać.
8. Możliwość jednoznacznego odpytywania i łączenia informacji.
9. RDF jest modelem, a Fuseki serwerem.
10. Reprezentowanie faktów i relacji w sposób maszynowo interpretowalny.

[Powrót do spisu treści](README.md)
