# Pytania sprawdzające

## 1. Czym jest mikroserwis?

<details>
<summary>Odpowiedź</summary>

Mikroserwis to samodzielna usługa realizująca konkretną zdolność biznesową. Ważniejsza od rozmiaru jest jasna odpowiedzialność, autonomia i możliwość niezależnej zmiany.

Linki: [01 Czym są mikroserwisy](01-czym-sa-mikroserwisy.md#term-mikroserwis), [glosariusz](00-glosariusz.md#mikroserwis).

</details>

## 2. Czy mikroserwis oznacza małą usługę?

<details>
<summary>Odpowiedź</summary>

Nie. Mały rozmiar może pomagać, ale nie jest definicją. Usługa jest dobra wtedy, gdy ma spójną odpowiedzialność i sensowną granicę biznesową.

Linki: [01 Czym są mikroserwisy](01-czym-sa-mikroserwisy.md#term-mikroserwis), [03 Granice serwisów](03-granice-serwisow-i-domena.md#term-granica-serwisu).

</details>

## 3. Kiedy monolit jest lepszy niż mikroserwisy?

<details>
<summary>Odpowiedź</summary>

Gdy zespół jest mały, domena jest jeszcze niestabilna, a głównym problemem jest szybkie uczenie się i proste wdrażanie. Modularny monolit często daje lepszy stosunek prostoty do kontroli.

Linki: [02 Monolit, modularny monolit i mikroserwisy](02-monolit-modularny-i-mikroserwisy.md#term-monolit), [08 Kiedy stosować](08-kiedy-stosowac-a-kiedy-nie.md#decyzja-praktyczna).

</details>

## 4. Co to jest modularny monolit?

<details>
<summary>Odpowiedź</summary>

To jedna aplikacja wdrażana jako całość, ale z wyraźnymi modułami, granicami i kontrolą zależności. Może być etapem przed mikroserwisami albo docelową architekturą.

Linki: [02 Modularny monolit](02-monolit-modularny-i-mikroserwisy.md#term-modularny-monolit), [glosariusz](00-glosariusz.md#modularny-monolit).

</details>

## 5. Po czym poznać dobrą granicę serwisu?

<details>
<summary>Odpowiedź</summary>

Dobra granica sprawia, że większość zmian biznesowych mieści się w jednej usłudze. Dane, reguły i decyzje mają jednego właściciela, a inne usługi nie muszą znać szczegółów implementacji.

Linki: [03 Sygnały dobrej granicy](03-granice-serwisow-i-domena.md#sygnały-dobrej-granicy), [glosariusz](00-glosariusz.md#granica-serwisu).

</details>

## 6. Co to jest bounded context?

<details>
<summary>Odpowiedź</summary>

Bounded context to granica znaczenia modelu domenowego. W jej obrębie pojęcia mają spójne znaczenie. Poza nią te same słowa mogą oznaczać coś innego.

Linki: [03 Granice serwisów i domena](03-granice-serwisow-i-domena.md#term-bounded-context), [glosariusz](00-glosariusz.md#bounded-context).

</details>

## 7. Dlaczego wspólna baza danych jest problemem?

<details>
<summary>Odpowiedź</summary>

Wspólna baza tworzy ukryty kontrakt i odbiera usługom własność danych. Zmiana schematu jednej usługi może przypadkowo złamać inne.

Linki: [05 Dane, transakcje i spójność](05-dane-transakcje-i-spojnosc.md#term-wlasnosc-danych), [09 Antywzorce i pułapki](09-antywzorce-i-pulapki.md#typowe-sygnały-ostrzegawcze).

</details>

## 8. Co oznacza własność danych?

<details>
<summary>Odpowiedź</summary>

Oznacza, że jedna usługa odpowiada za określony stan i tylko ona powinna decydować o jego zmianie. Inne usługi mogą korzystać z API, zdarzeń albo kopii odczytowych.

Linki: [05 Własność danych](05-dane-transakcje-i-spojnosc.md#term-wlasnosc-danych), [glosariusz](00-glosariusz.md#wlasnosc-danych).

</details>

## 9. Czym różni się komunikacja synchroniczna od asynchronicznej?

<details>
<summary>Odpowiedź</summary>

Synchroniczna wymaga czekania na odpowiedź, więc jest prosta, ale mocniej sprzęga usługi czasowo. Asynchroniczna pozwala reagować później na wiadomości lub zdarzenia, ale wprowadza opóźnienia i trudniejsze śledzenie przepływu.

Linki: [04 Komunikacja synchroniczna](04-komunikacja-i-kontrakty.md#term-komunikacja-synchroniczna), [04 Komunikacja asynchroniczna](04-komunikacja-i-kontrakty.md#term-komunikacja-asynchroniczna).

</details>

## 10. Czym jest kontrakt usługi?

<details>
<summary>Odpowiedź</summary>

Kontrakt to uzgodniony sposób współpracy: format, znaczenie danych, błędy, gwarancje i wersjonowanie. Kontrakt obejmuje semantykę, nie tylko JSON.

Linki: [04 Kontrakt](04-komunikacja-i-kontrakty.md#term-kontrakt), [glosariusz](00-glosariusz.md#kontrakt).

</details>

## 11. Co to jest zdarzenie domenowe?

<details>
<summary>Odpowiedź</summary>

To informacja, że w domenie zaszło coś istotnego, na przykład `OrderPlaced`. Odbiorcy reagują na fakt biznesowy, a nie na zmianę tabeli.

Linki: [04 Zdarzenia domenowe](04-komunikacja-i-kontrakty.md#term-zdarzenie-domenowe), [glosariusz](00-glosariusz.md#zdarzenie-domenowe).

</details>

## 12. Co oznacza spójność ostateczna?

<details>
<summary>Odpowiedź</summary>

Oznacza, że system może być chwilowo niespójny, ale po czasie osiąga poprawny stan. To świadomy model pracy, a nie brak kontroli.

Linki: [05 Spójność ostateczna](05-dane-transakcje-i-spojnosc.md#term-spojnosc-ostateczna), [glosariusz](00-glosariusz.md#spojnosc-ostateczna).

</details>

## 13. Czym jest saga?

<details>
<summary>Odpowiedź</summary>

Saga to proces biznesowy podzielony na kroki wykonywane przez różne usługi. Zamiast jednej transakcji rozproszonej używa lokalnych zmian i ewentualnej kompensacji.

Linki: [05 Saga](05-dane-transakcje-i-spojnosc.md#term-saga), [glosariusz](00-glosariusz.md#saga).

</details>

## 14. Dlaczego timeout jest konieczny?

<details>
<summary>Odpowiedź</summary>

Timeout ogranicza czas oczekiwania na zależność. Bez niego jedna wolna usługa może blokować zasoby wielu innych usług.

Linki: [06 Timeout](06-odpornosc-obserwowalnosc-i-operacje.md#term-timeout), [glosariusz](00-glosariusz.md#timeout).

</details>

## 15. Dlaczego retry bywa niebezpieczny?

<details>
<summary>Odpowiedź</summary>

Retry bez limitów i idempotencji może zwielokrotnić obciążenie albo wykonać operację kilka razy. Powinien mieć limit, odstęp, jitter i bezpieczną semantykę.

Linki: [06 Retry](06-odpornosc-obserwowalnosc-i-operacje.md#term-retry), [idempotencja](06-odpornosc-obserwowalnosc-i-operacje.md#term-idempotencja).

</details>

## 16. Co daje obserwowalność?

<details>
<summary>Odpowiedź</summary>

Pozwala zrozumieć, co dzieje się w systemie na podstawie logów, metryk i trace'ów. Bez niej diagnoza błędu w systemie rozproszonym jest zgadywaniem.

Linki: [06 Obserwowalność](06-odpornosc-obserwowalnosc-i-operacje.md#term-obserwowalnosc), [correlation ID](06-odpornosc-obserwowalnosc-i-operacje.md#term-correlation-id).

</details>

## 17. Po co są contract testy?

<details>
<summary>Odpowiedź</summary>

Sprawdzają, czy dostawca i konsument usługi rozumieją kontrakt tak samo. Chronią przed przypadkowym złamaniem API bez uruchamiania całego systemu.

Linki: [07 Contract testy](07-wdrazanie-testowanie-i-bezpieczenstwo.md#term-contract-test), [glosariusz](00-glosariusz.md#contract-test).

</details>

## 18. Co to jest rozproszony monolit?

<details>
<summary>Odpowiedź</summary>

To system podzielony technicznie na usługi, ale wymagający wspólnych zmian, wspólnych wdrożeń albo wspólnej bazy. Ma koszty mikroserwisów bez ich autonomii.

Linki: [09 Rozproszony monolit](09-antywzorce-i-pulapki.md#term-rozproszony-monolit), [glosariusz](00-glosariusz.md#rozproszony-monolit).

</details>

## 19. Jak migrować z monolitu do mikroserwisów?

<details>
<summary>Odpowiedź</summary>

Stopniowo. Najpierw uporządkować monolit i granice, potem wybrać fragment o rozsądnym ryzyku, dodać kontrakt, obserwowalność i pipeline, a następnie przenosić ruch małymi krokami.

Linki: [10 Migracja i roadmapa](10-migracja-i-roadmapa.md#term-strangler-fig-pattern), [strangler fig pattern](10-migracja-i-roadmapa.md#term-strangler-fig-pattern).

</details>

## 20. Jak odpowiedzieć na rekrutacyjne pytanie „kiedy mikroserwisy są złym pomysłem?”

<details>
<summary>Odpowiedź</summary>

Gdy domena jest nieznana, zespół jest mały, brakuje CI/CD i obserwowalności, a problemem jest jakość kodu, nie niezależność zespołów. Wtedy lepszy jest modularny monolit i stopniowe wydzielanie granic.

Linki: [08 Kiedy stosować, a kiedy nie](08-kiedy-stosowac-a-kiedy-nie.md#decyzja-praktyczna), [02 Monolit, modularny monolit i mikroserwisy](02-monolit-modularny-i-mikroserwisy.md#term-modularny-monolit).

</details>
