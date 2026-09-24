# Backup i utrzymanie

## Opis

Utrzymanie ArangoDB obejmuje monitorowanie, backupy, aktualizacje, reagowanie na awarie i sprawdzanie możliwości odtworzenia danych. Backup istniejący tylko na papierze nie jest strategią odzyskiwania.

## Kluczowe koncepty

- **Backup** — kopia danych przeznaczona do odtworzenia.
- **Restore** — przywrócenie danych z kopii.
- **RPO** — akceptowalna utrata danych w czasie.
- **RTO** — akceptowalny czas powrotu działania.
- **Runbook** — instrukcja postępowania operacyjnego.

## Key points

- Backup trzeba regularnie testować przez odtworzenie.
- RPO i RTO wynikają z wymagań, nie z samej technologii.
- Monitoring powinien obejmować dane, zasoby i zdrowie usług.
- Aktualizacje wymagają planu kompatybilności i wycofania.
- Procedury awaryjne powinny być znane zespołowi.

## Example

Zespół ustala, ile danych może utracić i jak szybko musi przywrócić działanie, a następnie dobiera backupy i procedury do tych wymagań.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Określamy RPO i RTO.
2. Wybieramy sposób i częstotliwość backupu.
3. Chronimy kopie przed utratą i nieuprawnionym dostępem.
4. Regularnie wykonujemy restore testowy.
5. Monitorujemy zdrowie i zasoby.
6. Aktualizujemy runbooki po ćwiczeniach i incydentach.

## Pytania

1. Czym jest backup?
2. Czym różni się backup od restore?
3. Co oznacza RPO?
4. Co oznacza RTO?
5. Dlaczego trzeba testować odtworzenie?
6. Co powinien obejmować monitoring?
7. Czym jest runbook?
8. Czy replika zastępuje backup?
9. Co należy ustalić przed wyborem strategii?
10. Jaki jest cel utrzymania bazy?

## Odpowiedzi

1. Kopią danych przeznaczoną do odtworzenia.
2. Backup tworzy kopię, a restore przywraca dane.
3. Akceptowalną utratą danych w czasie.
4. Akceptowalnym czasem powrotu działania.
5. Aby potwierdzić, że kopia jest użyteczna.
6. Dane, zasoby, wydajność i zdrowie komponentów.
7. Instrukcją postępowania w konkretnej sytuacji.
8. Nie, replika służy głównie dostępności, a backup także odzyskiwaniu.
9. Wymagania RPO, RTO i ryzyka.
10. Zachowanie dostępności, bezpieczeństwa i możliwości odzyskania danych.

[Powrót do spisu treści](README.md)
