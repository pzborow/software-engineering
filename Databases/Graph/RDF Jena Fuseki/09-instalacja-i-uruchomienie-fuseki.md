# Instalacja i uruchomienie Fuseki

## Opis

Fuseki można pobrać jako dystrybucję Apache Jena i uruchomić lokalnie z linii poleceń. Na początek najłatwiejszy jest dataset z pliku, a później dataset trwały lub zarządzany.

## Kluczowe koncepty

- **Dystrybucja Fuseki** — paczka zawierająca serwer i skrypty.
- **Port 3030** — domyślny port HTTP.
- **Dataset name** — nazwa datasetu w URL.
- **`--file`** — uruchomienie z plikiem jako źródłem danych.
- **Tryb TDB** — trwałe przechowywanie datasetu.

## Key points

- Przed startem warto sprawdzić wersję Java wymaganą przez wydanie.
- Minimalny start może użyć pliku Turtle.
- `--file` służy do prostego, demonstracyjnego datasetu read-only.
- Produkcyjne przechowywanie wymaga świadomego wyboru trwałości i zabezpieczeń.

## Example

```bash
fuseki-server --file=data.ttl /ds
```

Po uruchomieniu dataset jest dostępny pod `http://localhost:3030/ds`.

## Dodatkowe wyjaśnienie

W RDF najważniejsze jest to, że fakt jest zapisany jawnie jako relacja między zasobami. Dzięki temu dane można łączyć między systemami, łatwiej sprawdzać ich sens oraz budować spójne zapytania bez ukrywania znaczenia w strukturze technicznej. Model nie mówi tylko, jak dane są zapisane, ale co one oznaczają w kontekście całego grafu.

## Pełny flow

1. Instalujemy kompatybilną Javę.
2. Pobieramy i rozpakowujemy Fuseki.
3. Przygotowujemy plik RDF, np. `data.ttl`.
4. Uruchamiamy `fuseki-server --file=data.ttl /ds`.
5. Otwieramy interfejs lub endpoint HTTP.
6. Kończymy proces i przechodzimy do trwałego datasetu, gdy potrzebujemy zapisu.

## Pytania

1. Czego potrzebuje Fuseki do uruchomienia?
2. Jaki port jest domyślny?
3. Do czego służy `--file`?
4. Co oznacza `/ds`?
5. Czy dataset z `--file` jest dobry do produkcji?
6. Jakie rozszerzenie może mieć plik RDF?
7. Gdzie dostępny jest dataset po starcie?
8. Po co sprawdzać wersję Javy?
9. Co trzeba przygotować przed startem?
10. Jaki jest pierwszy prosty sposób nauki?

## Odpowiedzi

1. Dystrybucji Fuseki i kompatybilnej Javy.
2. 3030.
3. Do wskazania pliku danych przy starcie.
4. Nazwę datasetu w adresie.
5. Nie, to głównie prosty tryb demonstracyjny.
6. Na przykład `.ttl`, `.nt`, `.rdf` lub `.trig`.
7. Pod `http://localhost:3030/ds`.
8. Dla zgodności z wydaniem Fuseki.
9. Javę, Fuseki i plik RDF.
10. Uruchomienie datasetu z pliku Turtle.

[Powrót do spisu treści](README.md)
