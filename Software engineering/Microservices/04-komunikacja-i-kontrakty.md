# Komunikacja i kontrakty

<a id="term-kontrakt"></a>[Kontrakt](00-glosariusz.md#kontrakt) opisuje, jak usługa współpracuje z innymi. Obejmuje nie tylko format JSON-a, ale też znaczenie pól, błędy, statusy, gwarancje, wersjonowanie i oczekiwania czasowe.

<a id="term-api"></a>[API](00-glosariusz.md#api) powinno wyrażać operacje biznesowe. `POST /orders/{id}/cancel` mówi więcej niż techniczne `PUT /orders/{id}` z magicznym statusem. Dobre API pozwala klientowi wykonać intencję bez znajomości wewnętrznego modelu usługi.

<a id="term-komunikacja-synchroniczna"></a>[Komunikacja synchroniczna](00-glosariusz.md#komunikacja-synchroniczna) jest prosta: klient wysyła żądanie i czeka na odpowiedź. Pasuje do odczytów, walidacji i działań, gdzie użytkownik potrzebuje natychmiastowego wyniku. Problem zaczyna się, gdy wiele usług musi odpowiedzieć w jednym łańcuchu, bo wtedy rośnie opóźnienie i podatność na awarie.

<a id="term-komunikacja-asynchroniczna"></a>[Komunikacja asynchroniczna](00-glosariusz.md#komunikacja-asynchroniczna) rozluźnia zależność czasową. Usługa publikuje wiadomość albo <a id="term-zdarzenie-domenowe"></a>[zdarzenie domenowe](00-glosariusz.md#zdarzenie-domenowe), a odbiorcy reagują później. To zwiększa odporność i skalowalność, ale utrudnia śledzenie przepływu i wymaga akceptacji opóźnień.

Zdarzenie domenowe powinno mówić, co zaszło w biznesie, a nie jakie pole technicznie zmieniono. `OrderPlaced` jest lepsze niż `OrderTableUpdated`, bo odbiorca reaguje na fakt biznesowy, a nie na strukturę bazy.

Kontrakty powinny ewoluować kompatybilnie. Dodanie opcjonalnego pola zwykle jest bezpieczniejsze niż zmiana znaczenia istniejącego pola. Usługa powinna dawać odbiorcom czas na migrację i nie usuwać starego kontraktu bez planu.

## Przykład

`Orders` po przyjęciu zamówienia publikuje `OrderPlaced`. `Payments` może rozpocząć płatność, `Warehouse` może zarezerwować towar, a `Notifications` może wysłać wiadomość. `Orders` nie musi znać wszystkich odbiorców, ale musi jasno opisać znaczenie zdarzenia.

## Co zapamiętać

- Kontrakt to semantyka współpracy, nie tylko schema.
- Synchroniczność jest prostsza, ale mocniej sprzęga usługi czasowo.
- Asynchroniczność daje luźniejsze powiązanie, ale wprowadza opóźnienia i trudniejsze debugowanie.
- Zdarzenia powinny opisywać fakty biznesowe.
