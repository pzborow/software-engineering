# Walidacja i utrzymanie grafu

## Opis

Graf RDF może być elastyczny, ale dane nadal trzeba sprawdzać. Walidacja wykrywa brakujące, błędne lub niezgodne informacje, a utrzymanie obejmuje wersjonowanie vocabulariów, importy i monitorowanie endpointu.

## Kluczowe koncepty

- **SHACL** — język opisu ograniczeń grafu RDF.
- **Shape** — zestaw reguł walidacyjnych.
- **Constraint** — pojedyncze ograniczenie.
- **Data quality** — zgodność danych z oczekiwaniami.
- **Provenance** — informacja o pochodzeniu danych.

## Key points

- RDF bez schematu nie oznacza RDF bez jakości.
- SHACL może sprawdzać typy, kardynalność i wartości.
- Dane z wielu źródeł wymagają informacji o pochodzeniu.
- Import powinien być powtarzalny i możliwy do zweryfikowania.
- Endpoint trzeba monitorować tak jak inne usługi.

## Example

Shape może wymagać, aby każdy zasób typu `Person` miał dokładnie jedną nazwę tekstową.

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Definiujemy oczekiwania wobec grafu.
2. Zapisujemy je jako shapes.
3. Uruchamiamy walidację danych.
4. Naprawiamy lub oznaczamy naruszenia.
5. Monitorujemy importy i endpoint.
6. Wersjonujemy reguły oraz vocabularia.

## Pytania

1. Czy elastyczny RDF wymaga walidacji?
2. Czym jest SHACL?
3. Czym jest shape?
4. Co sprawdza constraint?
5. Czym jest provenance?
6. Co może sprawdzać SHACL?
7. Dlaczego import powinien być powtarzalny?
8. Co zrobić z naruszeniem reguły?
9. Co należy monitorować?
10. Po co wersjonować vocabularia?

## Odpowiedzi

1. Tak, jeśli zależy nam na jakości.
2. Językiem ograniczeń dla RDF.
3. Zestawem reguł walidacyjnych.
4. Pojedyncze wymaganie.
5. Informacją o pochodzeniu danych.
6. Typy, kardynalność i wartości.
7. Dla przewidywalności i odtwarzalności.
8. Naprawić albo świadomie oznaczyć.
9. Importy, błędy, czas odpowiedzi i zdrowie serwera.
10. Aby zmiany znaczenia były kontrolowane.

[Powrót do spisu treści](README.md)
