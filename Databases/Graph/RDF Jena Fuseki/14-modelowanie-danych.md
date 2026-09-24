# Modelowanie danych

## Opis

Modelowanie RDF polega na wyborze zasobów, relacji, wartości i vocabulariów. Dobre modelowanie zaczyna się od znaczenia informacji, a nie od przypadkowego kopiowania struktury tabel.

## Kluczowe koncepty

- **Vocabulary** — słownik używanych klas i właściwości.
- **Klasa** — kategoria zasobów.
- **Właściwość** — nazwana relacja lub cecha.
- **Identyfikacja** — wybór stabilnego IRI.
- **Otwarte dane** — dane możliwe do łączenia z innymi źródłami.

## Key points

- IRI powinny być stabilne i znaczące.
- Predicate powinny mieć jasno określone znaczenie.
- Nie każda kolumna musi stać się osobnym zasobem.
- Warto używać istniejących vocabulariów, gdy pasują.
- Model trzeba sprawdzać na zapytaniach.

## Example

Zamiast niejasnego `field1` używamy właściwości z opisanym znaczeniem i stabilnym IRI.

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Spisujemy pojęcia domeny bez wyboru składni.
2. Rozróżniamy zasoby, wartości i relacje.
3. Wybieramy istniejące vocabularia.
4. Nadajemy brakującym pojęciom własne IRI.
5. Zapisujemy przykładowe trójki.
6. Sprawdzamy, czy można je sensownie odpytać.

## Pytania

1. Co obejmuje modelowanie RDF?
2. Czym jest vocabulary?
3. Czym jest klasa?
4. Czym jest właściwość?
5. Dlaczego IRI powinno być stabilne?
6. Czy każda kolumna musi być zasobem?
7. Po co korzystać z istniejących vocabulariów?
8. Co powinno mieć jasno opisane znaczenie?
9. Od czego zacząć modelowanie?
10. Jak sprawdzić model?

## Odpowiedzi

1. Wybór zasobów, relacji, wartości i nazw.
2. Słownikiem klas i właściwości.
3. Kategorią zasobów.
4. Nazwaną relacją lub cechą.
5. Aby dane można było stabilnie łączyć.
6. Nie.
7. Dla interoperacyjności i wspólnego znaczenia.
8. IRI i predicate.
9. Od pojęć i faktów, nie od składni.
10. Przez przykładowe trójki i zapytania.

[Powrót do spisu treści](README.md)
