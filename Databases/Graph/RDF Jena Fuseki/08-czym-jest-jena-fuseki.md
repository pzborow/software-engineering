# Czym jest Jena Fuseki

## Opis

Apache Jena Fuseki to serwer SPARQL dla danych RDF. Udostępnia protokoły SPARQL Query, SPARQL Update i Graph Store, a dane może przechowywać w pamięci lub trwale przez mechanizmy Jeny.

## Kluczowe koncepty

- **Fuseki server** — serwer udostępniający dataset.
- **Dataset** — dane dostępne pod nazwą usługi.
- **SPARQL endpoint** — adres przyjmujący zapytania.
- **Graph Store Protocol** — protokół pracy z grafem.
- **TDB** — trwałe przechowywanie danych Jeny.

## Key points

- Fuseki nie jest samym modelem RDF.
- Serwer może działać samodzielnie lub być osadzony w aplikacji.
- Endpoint zapytań i endpoint aktualizacji mogą być rozdzielone.
- Dataset może być pamięciowy albo trwały.
- Adres datasetu jest punktem wejścia dla klienta.

## Example

Dla datasetu `ds` zapytanie może być dostępne pod `http://localhost:3030/ds/sparql`, a aktualizacja pod `http://localhost:3030/ds/update`.

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Instalujemy Apache Jena Fuseki.
2. Uruchamiamy serwer.
3. Tworzymy lub wskazujemy dataset.
4. Ładujemy dane RDF.
5. Wykonujemy zapytania SPARQL.
6. Zarządzamy trwałością i dostępem.

## Pytania

1. Czym jest Fuseki?
2. Czy Fuseki jest modelem danych?
3. Co udostępnia serwer Fuseki?
4. Czym jest dataset?
5. Czym jest endpoint SPARQL?
6. Do czego służy Graph Store Protocol?
7. Czy Fuseki może działać bez aplikacji Java?
8. Czym jest TDB?
9. Gdzie znajduje się dataset `ds`?
10. Jaki jest podstawowy przepływ pracy?

## Odpowiedzi

1. Serwerem SPARQL dla RDF.
2. Nie, jest serwerem.
3. Zapytania, aktualizacje i operacje na grafach.
4. Zbiorem danych udostępnianym jako usługa.
5. Adresem przyjmującym zapytania.
6. Do pracy z grafem przez protokół HTTP.
7. Tak, może działać jako samodzielny serwer.
8. Mechanizmem trwałego przechowywania Jeny.
9. Pod ścieżką datasetu, np. `/ds`.
10. Uruchomienie, ładowanie, zapytanie i utrzymanie danych.

[Powrót do spisu treści](README.md)
