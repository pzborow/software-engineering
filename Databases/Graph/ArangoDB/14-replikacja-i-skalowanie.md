# Replikacja i skalowanie

## Opis

Replikacja i skalowanie służą zwiększaniu dostępności, odporności oraz możliwości obsługi większej ilości danych i ruchu. Są decyzjami architektonicznymi, które wymagają zrozumienia kosztów i sposobu rozłożenia danych.

## Kluczowe koncepty

- **Replikacja** — utrzymywanie kopii danych lub stanu.
- **Failover** — przejęcie działania przez inną instancję.
- **Sharding** — podział danych między wiele miejsc.
- **Skalowanie poziome** — dodawanie kolejnych zasobów lub instancji.
- **Dostępność** — zdolność systemu do obsługi mimo problemów.

## Key points

- Replikacja zwiększa odporność, ale wymaga zarządzania kopiami.
- Sharding może zwiększyć skalę, lecz komplikuje lokalizację danych.
- Skalowanie nie rozwiązuje złych zapytań ani złego modelu.
- Failover wymaga sprawdzenia spójności i gotowości kopii.
- Wymagania biznesowe powinny określać poziom dostępności.

## Example

Dane mogą być rozłożone między wiele serwerów, a ich kopie mogą umożliwić kontynuowanie pracy po niedostępności jednego elementu.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Określamy wymagany poziom dostępności i skalę.
2. Wskazujemy dane i obciążenia do rozłożenia.
3. Wybieramy replikację, sharding albo oba mechanizmy.
4. Sprawdzamy wpływ na zapytania i spójność.
5. Testujemy przejęcie działania po awarii.
6. Mierzymy koszt i poprawiamy rozmieszczenie danych.

## Pytania

1. Po co stosuje się replikację?
2. Czym jest failover?
3. Czym jest sharding?
4. Co oznacza skalowanie poziome?
5. Czy repliki usuwają wszystkie problemy?
6. Jaki koszt ma sharding?
7. Od czego zależy poziom dostępności?
8. Co trzeba sprawdzić podczas failover?
9. Czy skalowanie naprawia złe zapytania?
10. Jaki jest cel rozkładania danych?

## Odpowiedzi

1. Dla zwiększenia dostępności i odporności.
2. Przejęciem działania przez inną instancję.
3. Podziałem danych między wiele miejsc.
4. Dodawanie kolejnych zasobów lub instancji.
5. Nie, nadal trzeba zarządzać spójnością i kosztami.
6. Większą złożoność lokalizacji i dostępu do danych.
7. Od wymagań systemu i znaczenia niedostępności.
8. Gotowość, spójność i zachowanie kopii.
9. Nie, problem modelu lub zapytania pozostaje.
10. Obsługa większej skali i ograniczenie skutków awarii.

[Powrót do spisu treści](README.md)
