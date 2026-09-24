# Węzły i wartości

## Opis

W RDF elementy trójki mogą być IRI, literałami albo blank nodes. Ten wybór mówi, czy element jest identyfikowalnym zasobem, wartością danych czy zasobem bez publicznego identyfikatora.

## Kluczowe koncepty

- **IRI** — globalny identyfikator zasobu.
- **Literal** — wartość, np. tekst, liczba lub data.
- **Blank node** — anonimowy węzeł bez stabilnego IRI.
- **Datatype** — typ literału, np. integer lub date.
- **Language tag** — język tekstu, np. `@pl`.

## Key points

- Subject i predicate są zasobami, nie zwykłymi literałami.
- Object może być IRI, literalem lub blank node.
- Typ i język literału wpływają na znaczenie danych.
- Blank node służy do lokalnej struktury, nie do stabilnej identyfikacji.
- Liczby i daty warto zapisywać z właściwym typem.

## Example

```text
<https://example.org/item/1> <https://example.org/price> "12.50"^^<http://www.w3.org/2001/XMLSchema#decimal> .
<https://example.org/item/1> <https://example.org/label> "Przykład"@pl .
```

## Dodatkowe wyjaśnienie

W RDF nie ma jednej „kolumny” dla typu danych. To, czy coś jest wartością, zasobem czy anonimowym obiektem, wynika z formy węzła. Literal z datatypem ma znaczenie numeryczne lub datowe, a literal z tagiem językowym mówi, że tekst jest zapisany w danym języku. Blank node nie ma stabilnego globalnego identyfikatora, więc jest przydatny tylko do lokalnych struktur opisu wewnątrz grafu.

## Pełny flow

1. Decydujemy, czy element ma własną tożsamość.
2. Dla zasobu wybieramy IRI.
3. Dla wartości wybieramy literal.
4. Dodajemy datatype lub język, jeśli ma znaczenie.
5. Blank node stosujemy tylko tam, gdzie anonimowość jest wystarczająca.

## Pytania

1. Jakie trzy rodzaje węzłów występują w RDF?
2. Czym jest IRI?
3. Czym jest literal?
4. Czym jest blank node?
5. Gdzie może wystąpić literal?
6. Czym jest datatype?
7. Do czego służy tag językowy?
8. Czy blank node ma stabilne publiczne IRI?
9. Jak zapisać liczbę z typem?
10. Co wybrać dla zasobu wymagającego identyfikacji?

## Odpowiedzi

1. IRI, literal i blank node.
2. Identyfikatorem zasobu.
3. Wartością danych.
4. Anonimowym węzłem.
5. Jako object.
6. Informacją o typie wartości.
7. Do wskazania języka tekstu.
8. Nie.
9. Z użyciem datatype XML Schema.
10. IRI.

[Powrót do spisu treści](README.md)
