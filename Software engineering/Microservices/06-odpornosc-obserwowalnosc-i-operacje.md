# Odporność, obserwowalność i operacje

W mikroserwisach awaria części systemu jest normalnym stanem, nie wyjątkiem. Sieć może być wolna, usługa może być przeciążona, a zależność może odpowiedzieć błędem. Architektura musi zakładać częściową awarię od początku.

<a id="term-timeout"></a>[Timeout](00-glosariusz.md#timeout) ogranicza czas oczekiwania na zależność. Bez timeoutu jeden wolny serwis może zużyć wątki, połączenia i pamięć w wielu innych miejscach. Timeout powinien wynikać z oczekiwań biznesowych i budżetu czasu całego żądania.

<a id="term-retry"></a>[Retry](00-glosariusz.md#retry) pomaga przy błędach chwilowych, ale może też pogorszyć awarię, jeśli wszystkie usługi ponawiają żądania jednocześnie. Retry wymaga limitu prób, opóźnienia, jittera i <a id="term-idempotencja"></a>[idempotencji](00-glosariusz.md#idempotencja), aby duplikaty nie zmieniły stanu kilka razy.

<a id="term-circuit-breaker"></a>[Circuit breaker](00-glosariusz.md#circuit-breaker) zatrzymuje wywołania do zależności, która seryjnie zawodzi. Dzięki temu system szybciej odpowiada błędem lub fallbackiem, zamiast czekać na kolejne timeouty.

<a id="term-obserwowalnosc"></a>[Obserwowalność](00-glosariusz.md#obserwowalnosc) jest warunkiem utrzymania mikroserwisów. Bez niej problem w jednej usłudze wygląda jak losowe błędy w wielu miejscach. Potrzebne są <a id="term-logi"></a>[logi](00-glosariusz.md#logi), <a id="term-metryki"></a>[metryki](00-glosariusz.md#metryki) i <a id="term-tracing"></a>[tracing](00-glosariusz.md#tracing).

<a id="term-correlation-id"></a>[Correlation ID](00-glosariusz.md#correlation-id) pozwala połączyć logi z wielu usług dotyczące jednego żądania. Bez wspólnego identyfikatora analiza problemu przypomina składanie historii z niepowiązanych fragmentów.

## Przykład

Jeśli `Recommendations` nie działa, sklep nadal powinien pokazywać produkt i pozwolić złożyć zamówienie. Rekomendacje mogą zniknąć, ale podstawowy zakup nie powinien zależeć od pomocniczej funkcji.

## Co zapamiętać

- Każde wywołanie sieciowe powinno mieć timeout.
- Retry bez idempotencji i limitów bywa niebezpieczne.
- Obserwowalność trzeba projektować razem z usługą.
- System powinien umieć działać w trybie zdegradowanym.
