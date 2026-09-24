# Ładowanie danych do Fuseki

## Opis

Dane RDF można ładować do Fuseki z plików albo przez endpoint Graph Store/SPARQL Update. Sposób zależy od tego, czy dataset jest tylko do odczytu, czy ma przyjmować trwałe zmiany.

## Kluczowe koncepty

- **Upload** — przesłanie pliku RDF.
- **Graph Store** — protokół odczytu i zapisu grafu.
- **SPARQL Update** — dodawanie, usuwanie i modyfikacja trójek.
- **Default graph** — graf domyślny datasetu.
- **Named graph** — graf wskazany nazwą.

## Key points

- Najprostszy start to `--file`, ale jest read-only.
- Dataset zarządzany pozwala ładować dane po uruchomieniu.
- Trzeba znać format pliku i docelowy graf.
- Duże importy wymagają planu wydajności i weryfikacji.
- Po imporcie warto sprawdzić liczbę trójek.

## Example

```bash
curl -X POST -H 'Content-Type: text/turtle' \
  --data-binary @data.ttl \
  'http://localhost:3030/ds/data'
```

Dokładny endpoint zależy od konfiguracji datasetu.

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Przygotowujemy poprawny plik RDF.
2. Uruchamiamy dataset z możliwością zapisu.
3. Wybieramy default graph lub named graph.
4. Wysyłamy dane przez Graph Store albo Update.
5. Sprawdzamy odpowiedź serwera.
6. Wykonujemy zapytanie kontrolne.

## Pytania

1. Jak można ładować RDF do Fuseki?
2. Czy `--file` pozwala później zapisywać dane?
3. Czym jest Graph Store?
4. Do czego służy SPARQL Update?
5. Co oznacza default graph?
6. Czym jest named graph?
7. Co trzeba znać przed importem?
8. Co sprawdzić po imporcie?
9. Dlaczego duży import wymaga planu?
10. Czy endpoint jest zawsze taki sam?

## Odpowiedzi

1. Z pliku, przez Graph Store albo SPARQL Update.
2. W prostym trybie nie, jest read-only.
3. Protokołem odczytu i zapisu grafu.
4. Do modyfikacji trójek.
5. Podstawowy graf datasetu.
6. Grafem wskazanym nazwą.
7. Format, endpoint i docelowy graf.
8. Odpowiedź i liczbę lub obecność danych.
9. Dla kontroli czasu, zasobów i poprawności.
10. Nie, zależy od konfiguracji.

[Powrót do spisu treści](README.md)
