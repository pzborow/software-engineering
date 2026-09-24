# Wdrożenie i architektura środowiska

## Opis

ArangoDB może działać jako pojedynczy serwer albo klaster. Wybór środowiska powinien wynikać z wymagań dostępności, skali, utrzymania i odporności, a nie z samej chęci użycia klastra.

## Kluczowe koncepty

- **Single server** — pojedyncza instancja bazy.
- **Klaster** — współpracujące komponenty zapewniające skalowanie i dostępność.
- **Coordinator** — komponent kierujący żądania w środowisku klastrowym.
- **DB-Server** — komponent przechowujący dane w klastrze.
- **Agency** — komponent przechowujący i uzgadniający stan klastra.

## Key points

- Pojedynczy serwer jest prostszy w uruchomieniu i utrzymaniu.
- Klaster zwiększa możliwości, ale też złożoność operacyjną.
- Architektura środowiska powinna być dopasowana do wymagań.
- Zdrowie komponentów i komunikacja między nimi wymagają monitorowania.
- Środowisko testowe powinno odzwierciedlać istotne cechy produkcji.

## Example

Środowisko lokalne może używać pojedynczej instancji, a środowisko wymagające wysokiej dostępności może używać klastra z rozdzielonymi rolami.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Określamy wymagania dostępności i skali.
2. Wybieramy single server albo klaster.
3. Rozdzielamy odpowiedzialności komponentów.
4. Przygotowujemy konfigurację i monitoring.
5. Sprawdzamy zdrowie środowiska oraz odtwarzanie po awarii.
6. Dokumentujemy sposób utrzymania.

## Pytania

1. Jakie podstawowe warianty wdrożenia oferuje ArangoDB?
2. Kiedy wystarczy single server?
3. Po co używa się klastra?
4. Czym jest Coordinator?
5. Czym jest DB-Server?
6. Czym jest Agency?
7. Jaki koszt ma klaster?
8. Dlaczego środowisko trzeba monitorować?
9. Czy środowisko testowe musi być identyczne z produkcją?
10. Od czego zależy wybór architektury?

## Odpowiedzi

1. Pojedynczy serwer i klaster.
2. Gdy wymagania skali i dostępności są ograniczone.
3. Dla większej dostępności, skalowania i odporności.
4. Komponentem kierującym żądania w klastrze.
5. Komponentem przechowującym dane.
6. Komponentem uzgadniającym stan klastra.
7. Większą złożoność konfiguracji i utrzymania.
8. Aby wykrywać problemy komponentów i komunikacji.
9. Nie, ale musi odzwierciedlać istotne ryzyka.
10. Od dostępności, skali, kosztu i możliwości utrzymania.

[Powrót do spisu treści](README.md)
