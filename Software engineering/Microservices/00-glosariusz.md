# Glosariusz mikroserwisów

## Spis pojęć

- [Mikroserwis](#mikroserwis)
- [Monolit](#monolit)
- [Modularny monolit](#modularny-monolit)
- [Domena](#domena)
- [Bounded context](#bounded-context)
- [Granica serwisu](#granica-serwisu)
- [Autonomia](#autonomia)
- [Własność danych](#wlasnosc-danych)
- [Kontrakt](#kontrakt)
- [API](#api)
- [Zdarzenie domenowe](#zdarzenie-domenowe)
- [Komunikacja synchroniczna](#komunikacja-synchroniczna)
- [Komunikacja asynchroniczna](#komunikacja-asynchroniczna)
- [Spójność natychmiastowa](#spojnosc-natychmiastowa)
- [Spójność ostateczna](#spojnosc-ostateczna)
- [Saga](#saga)
- [Idempotencja](#idempotencja)
- [Timeout](#timeout)
- [Retry](#retry)
- [Circuit breaker](#circuit-breaker)
- [Obserwowalność](#obserwowalnosc)
- [Logi](#logi)
- [Metryki](#metryki)
- [Tracing](#tracing)
- [Correlation ID](#correlation-id)
- [Deployment pipeline](#deployment-pipeline)
- [Canary release](#canary-release)
- [Blue-green deployment](#blue-green-deployment)
- [Contract test](#contract-test)
- [Test end-to-end](#test-end-to-end)
- [Strangler fig pattern](#strangler-fig-pattern)
- [Rozproszony monolit](#rozproszony-monolit)

<a id="mikroserwis"></a>
## Mikroserwis

Mała, samodzielnie rozwijana usługa realizująca konkretną zdolność biznesową. Ważniejsza od rozmiaru jest odpowiedzialność, autonomia i jasna granica. Pierwsza wzmianka: [01](01-czym-sa-mikroserwisy.md#term-mikroserwis).

<a id="monolit"></a>
## Monolit

System wdrażany jako jedna całość. Może być uporządkowany albo chaotyczny; sam fakt bycia monolitem nie jest błędem. Pierwsza wzmianka: [02](02-monolit-modularny-i-mikroserwisy.md#term-monolit).

<a id="modularny-monolit"></a>
## Modularny monolit

Monolit z wyraźnymi modułami, granicami i zasadami zależności wewnątrz jednej aplikacji. Często jest lepszym pierwszym krokiem niż mikroserwisy. Pierwsza wzmianka: [02](02-monolit-modularny-i-mikroserwisy.md#term-modularny-monolit).

<a id="domena"></a>
## Domena

Obszar problemu biznesowego, dla którego system dostarcza wartość. Domena pomaga rozumieć, gdzie powinny przebiegać granice odpowiedzialności. Pierwsza wzmianka: [01](01-czym-sa-mikroserwisy.md#term-domena).

<a id="bounded-context"></a>
## Bounded context

Granica znaczenia modelu domenowego: w jej obrębie pojęcia, reguły i nazwy mają spójne znaczenie. Pierwsza wzmianka: [03](03-granice-serwisow-i-domena.md#term-bounded-context).

<a id="granica-serwisu"></a>
## Granica serwisu

Linia oddzielająca odpowiedzialność jednej usługi od reszty systemu. Dobra granica ogranicza wspólne zmiany i ukryte zależności. Pierwsza wzmianka: [03](03-granice-serwisow-i-domena.md#term-granica-serwisu).

<a id="autonomia"></a>
## Autonomia

Możliwość zmiany, wdrożenia, skalowania i utrzymania usługi bez ciągłej koordynacji z innymi zespołami. Pierwsza wzmianka: [01](01-czym-sa-mikroserwisy.md#term-autonomia).

<a id="wlasnosc-danych"></a>
## Własność danych

Zasada, że konkretna usługa jest właścicielem określonego stanu i tylko ona decyduje o jego zmianie. Pierwsza wzmianka: [05](05-dane-transakcje-i-spojnosc.md#term-wlasnosc-danych).

<a id="kontrakt"></a>
## Kontrakt

Uzgodniony sposób współpracy między usługą a jej odbiorcami: format, znaczenie danych, błędy i gwarancje. Pierwsza wzmianka: [04](04-komunikacja-i-kontrakty.md#term-kontrakt).

<a id="api"></a>
## API

Publiczny punkt współpracy usługi z innymi klientami lub usługami. W mikroserwisach API jest granicą odpowiedzialności, nie tylko technicznym endpointem. Pierwsza wzmianka: [04](04-komunikacja-i-kontrakty.md#term-api).

<a id="zdarzenie-domenowe"></a>
## Zdarzenie domenowe

Informacja, że w domenie zaszło coś istotnego, na przykład `OrderPlaced` albo `PaymentAccepted`. Pierwsza wzmianka: [04](04-komunikacja-i-kontrakty.md#term-zdarzenie-domenowe).

<a id="komunikacja-synchroniczna"></a>
## Komunikacja synchroniczna

Model, w którym nadawca czeka na odpowiedź odbiorcy, na przykład przez HTTP. Prosty do zrozumienia, ale zwiększa zależność czasową. Pierwsza wzmianka: [04](04-komunikacja-i-kontrakty.md#term-komunikacja-synchroniczna).

<a id="komunikacja-asynchroniczna"></a>
## Komunikacja asynchroniczna

Model, w którym nadawca publikuje wiadomość lub zdarzenie i nie czeka na natychmiastową odpowiedź. Pierwsza wzmianka: [04](04-komunikacja-i-kontrakty.md#term-komunikacja-asynchroniczna).

<a id="spojnosc-natychmiastowa"></a>
## Spójność natychmiastowa

Stan, w którym zmiana jest od razu widoczna i potwierdzona w całym wymaganym zakresie. Pierwsza wzmianka: [05](05-dane-transakcje-i-spojnosc.md#term-spojnosc-natychmiastowa).

<a id="spojnosc-ostateczna"></a>
## Spójność ostateczna

Stan, w którym dane mogą być chwilowo niespójne, ale system dąży do poprawnego rezultatu po czasie. Pierwsza wzmianka: [05](05-dane-transakcje-i-spojnosc.md#term-spojnosc-ostateczna).

<a id="saga"></a>
## Saga

Proces biznesowy podzielony na kroki wykonywane przez różne usługi, zwykle z kompensacją zamiast jednej transakcji rozproszonej. Pierwsza wzmianka: [05](05-dane-transakcje-i-spojnosc.md#term-saga).

<a id="idempotencja"></a>
## Idempotencja

Cecha operacji, w której wielokrotne wykonanie tego samego żądania daje ten sam efekt końcowy. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-idempotencja).

<a id="timeout"></a>
## Timeout

Limit czasu oczekiwania na odpowiedź zależności. Chroni system przed nieskończonym blokowaniem zasobów. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-timeout).

<a id="retry"></a>
## Retry

Ponowienie operacji po błędzie chwilowym. Wymaga limitów, odstępów i idempotencji. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-retry).

<a id="circuit-breaker"></a>
## Circuit breaker

Mechanizm czasowo odcinający wywołania do zawodnej zależności, aby nie przeciążać systemu kolejnymi próbami. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-circuit-breaker).

<a id="obserwowalnosc"></a>
## Obserwowalność

Możliwość rozumienia stanu systemu na podstawie logów, metryk i śladów. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-obserwowalnosc).

<a id="logi"></a>
## Logi

Zapis istotnych zdarzeń w systemie. Pomagają odtworzyć, co się wydarzyło. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-logi).

<a id="metryki"></a>
## Metryki

Liczbowe sygnały opisujące zachowanie systemu, na przykład czas odpowiedzi, liczba błędów i obciążenie. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-metryki).

<a id="tracing"></a>
## Tracing

Śledzenie przebiegu żądania przez wiele usług. Pozwala zobaczyć, gdzie powstało opóźnienie lub błąd. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-tracing).

<a id="correlation-id"></a>
## Correlation ID

Identyfikator łączący logi i ślady dotyczące jednego żądania lub procesu. Pierwsza wzmianka: [06](06-odpornosc-obserwowalnosc-i-operacje.md#term-correlation-id).

<a id="deployment-pipeline"></a>
## Deployment pipeline

Zautomatyzowany przepływ od zmiany kodu do wdrożenia, obejmujący build, testy, publikację i rollout. Pierwsza wzmianka: [07](07-wdrazanie-testowanie-i-bezpieczenstwo.md#term-deployment-pipeline).

<a id="canary-release"></a>
## Canary release

Wdrożenie nowej wersji najpierw dla małej części ruchu lub użytkowników. Pierwsza wzmianka: [07](07-wdrazanie-testowanie-i-bezpieczenstwo.md#term-canary-release).

<a id="blue-green-deployment"></a>
## Blue-green deployment

Strategia z dwoma środowiskami, gdzie ruch przełącza się między starą i nową wersją. Pierwsza wzmianka: [07](07-wdrazanie-testowanie-i-bezpieczenstwo.md#term-blue-green-deployment).

<a id="contract-test"></a>
## Contract test

Test sprawdzający, czy dostawca i konsument usługi rozumieją kontrakt w ten sam sposób. Pierwsza wzmianka: [07](07-wdrazanie-testowanie-i-bezpieczenstwo.md#term-contract-test).

<a id="test-end-to-end"></a>
## Test end-to-end

Test przechodzący przez wiele części systemu. Daje pewność przepływu, ale bywa wolny i kruchy. Pierwsza wzmianka: [07](07-wdrazanie-testowanie-i-bezpieczenstwo.md#term-test-end-to-end).

<a id="strangler-fig-pattern"></a>
## Strangler fig pattern

Wzorzec migracji, w którym nowy system stopniowo przejmuje fragmenty odpowiedzialności starego systemu. Pierwsza wzmianka: [10](10-migracja-i-roadmapa.md#term-strangler-fig-pattern).

<a id="rozproszony-monolit"></a>
## Rozproszony monolit

System podzielony technicznie na usługi, ale wymagający wspólnych zmian, wspólnych wdrożeń lub jednej bazy. Pierwsza wzmianka: [09](09-antywzorce-i-pulapki.md#term-rozproszony-monolit).
