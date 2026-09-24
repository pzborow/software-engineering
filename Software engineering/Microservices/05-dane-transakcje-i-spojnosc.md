# Dane, transakcje i spójność

<a id="term-wlasnosc-danych"></a>[Własność danych](00-glosariusz.md#wlasnosc-danych) oznacza, że jeden serwis odpowiada za konkretny stan i reguły jego zmiany. Inne usługi mogą pytać, subskrybować zdarzenia albo utrzymywać kopie odczytowe, ale nie powinny samodzielnie modyfikować cudzych tabel.

Wspólna baza danych jest jednym z najczęstszych sposobów utraty autonomii. Na początku wydaje się wygodna, bo ułatwia joiny i transakcje. Później sprawia, że każda zmiana schematu staje się zmianą kontraktu dla wielu usług, często niejawnego i niekontrolowanego.

<a id="term-spojnosc-natychmiastowa"></a>[Spójność natychmiastowa](00-glosariusz.md#spojnosc-natychmiastowa) jest naturalna w jednej transakcji w jednej bazie. W mikroserwisach operacja biznesowa często przechodzi przez kilka usług, więc jedna globalna transakcja staje się kosztowna, krucha albo nierealistyczna.

<a id="term-spojnosc-ostateczna"></a>[Spójność ostateczna](00-glosariusz.md#spojnosc-ostateczna) zakłada, że system przez chwilę może mieć różne widoki tego samego procesu, ale po czasie osiągnie poprawny stan. To nie jest wymówka dla chaosu. To świadomy model, który wymaga komunikatów dla użytkownika, retry, idempotencji i obsługi wyjątków.

<a id="term-saga"></a>[Saga](00-glosariusz.md#saga) to sposób prowadzenia procesu przez wiele usług bez jednej transakcji rozproszonej. Każdy krok wykonuje lokalną zmianę, a w razie problemu system uruchamia kroki kompensujące albo oznacza proces do obsługi.

Nie wszystkie dane muszą być natychmiast aktualne wszędzie. Koszyk, płatność i wysyłka mają różne wymagania. Architektura powinna rozróżniać dane krytyczne, dane pomocnicze i dane raportowe.

## Przykład

Po złożeniu zamówienia `Orders` zapisuje zamówienie jako `PendingPayment`. `Payments` później potwierdza płatność. Przez chwilę zamówienie istnieje, ale nie jest jeszcze opłacone. To poprawny stan procesu, jeśli system jasno go modeluje.

## Co zapamiętać

- Każdy ważny stan powinien mieć jednego właściciela.
- Wspólna baza zwykle oznacza ukryty kontrakt i ukryte sprzężenie.
- Spójność ostateczna musi być zaprojektowana, nie przypadkowa.
- Saga zastępuje jedną wielką transakcję procesem kroków i kompensacji.
