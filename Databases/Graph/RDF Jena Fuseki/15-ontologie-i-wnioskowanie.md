# Ontologie i wnioskowanie

## Opis

Ontologia opisuje pojęcia, klasy, właściwości i reguły w danym obszarze. Wnioskowanie pozwala wyprowadzać nowe fakty na podstawie zapisanych relacji i reguł, ale nie jest tym samym co zwykłe zapytanie.

## Kluczowe koncepty

- **Ontologia** — formalny opis pojęć i relacji.
- **Klasa** — typ zasobu.
- **Podklasa** — specjalizacja klasy.
- **Domain/range** — oczekiwany subject i object właściwości.
- **Inferencja** — wyprowadzanie nowych faktów.

## Key points

- Ontologia nadaje danym dodatkowe znaczenie.
- RDFS i OWL oferują różne poziomy opisu.
- Inferencja może zwiększyć wynik zapytania i koszt obliczeń.
- Trzeba rozróżniać fakty zapisane od wywnioskowanych.
- Reguły powinny być udokumentowane.

## Example

Jeśli `Student` jest podklasą `Person`, system wnioskujący może uznać zasób typu `Student` za `Person`.

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Opisujemy klasy i właściwości.
2. Dodajemy relacje podklas i ograniczenia.
3. Wybieramy RDFS lub OWL stosownie do potrzeb.
4. Włączamy wnioskowanie w kontrolowany sposób.
5. Sprawdzamy wynik i koszt zapytań.
6. Dokumentujemy, które fakty są wywnioskowane.

## Pytania

1. Czym jest ontologia?
2. Czym jest inferencja?
3. Czym jest podklasa?
4. Do czego służy domain?
5. Do czego służy range?
6. Czym różni się fakt zapisany od wywnioskowanego?
7. Co oferują RDFS i OWL?
8. Czy inferencja jest darmowa obliczeniowo?
9. Po co dokumentować reguły?
10. Kiedy używać wnioskowania?

## Odpowiedzi

1. Formalnym opisem pojęć i relacji.
2. Wyprowadzaniem nowych faktów.
3. Specjalizacją klasy.
4. Do określenia typu subject.
5. Do określenia typu object.
6. Jeden jest zapisany, drugi wynika z reguł.
7. Mechanizmy opisu semantyki.
8. Nie, może zwiększyć koszt.
9. Aby rozumieć pochodzenie wyników.
10. Gdy reguły semantyczne dają realną wartość.

[Powrót do spisu treści](README.md)
