# Trójka RDF

## Opis

Najmniejszą jednostką informacji w RDF jest trójka: subject opisuje, o czym mówimy, predicate nazywa relację, a object jest wartością lub innym zasobem.

## Kluczowe koncepty

- **Subject** — podmiot faktu.
- **Predicate** — właściwość lub relacja.
- **Object** — wartość albo zasób wskazany przez relację.
- **Statement** — synonim faktu RDF.
- **Kropka** — zakończenie zapisu trójki w Turtle.

## Key points

- Kolejność elementów ma znaczenie.
- Predicate jest zawsze relacją lub właściwością.
- Object może być zasobem albo literałem.
- Subject nie jest zwykłym tekstem, jeśli opisuje zasób.
- Wiele trójek może mieć ten sam subject.

## Example

```text
<https://example.org/alice> <https://example.org/name> "Alice" .
```

Subject to Alice, predicate to name, a object to literal "Alice".

## Dodatkowe wyjaśnienie

Trójka RDF jest najbardziej podstawowym zapisem faktu: „to zasób ma tę relację do tej wartości”. Model nie opisuje tabeli, tylko zdanie w formie maszynowo czytelnej. To właśnie dzięki temu można łączyć fakty z różnych źródeł, ponieważ relacja jest nazwana jawnie, a nie ukryta w strukturze kolumn lub schematu bazy.

## Pełny flow

1. Wybieramy subject.
2. Wybieramy predicate opisujące relację.
3. Wybieramy object jako zasób albo wartość.
4. Zapisujemy trójkę.
5. Dodajemy kolejne fakty dla tego samego subject.

## Pytania

1. Z ilu elementów składa się trójka?
2. Co oznacza subject?
3. Co oznacza predicate?
4. Co oznacza object?
5. Czy object może być zasobem?
6. Czy object może być tekstem?
7. Czy kolejność elementów ma znaczenie?
8. Co kończy trójkę w Turtle?
9. Czy jeden subject może mieć wiele trójek?
10. Jak nazywa się pojedynczy fakt RDF?

## Odpowiedzi

1. Z trzech.
2. Zasób, o którym mówimy.
3. Relację lub właściwość.
4. Wartość albo wskazany zasób.
5. Tak.
6. Tak, jako literal.
7. Tak.
8. Kropka.
9. Tak.
10. Statement, czyli stwierdzenie.

[Powrót do spisu treści](README.md)
