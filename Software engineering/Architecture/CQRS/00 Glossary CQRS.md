# Glosariusz CQRS

## Spis haseł

- [CQRS](#cqrs)
- [CQS](#cqs)
- [Model zapisu](#write-model)
- [Model odczytu](#read-model)
- [Event sourcing](#event-sourcing)
- [Komenda](#command)
- [Zdarzenie domenowe](#domain-event)
- [Task-based UI](#task-based-ui)
- [Handler komendy](#command-handler)
- [Agregat](#aggregate)
- [Idempotencja](#idempotency)
- [Klucz idempotencji](#idempotency-key)
- [Optymistyczna kontrola współbieżności](#optimistic-concurrency)
- [Zapytanie](#query)
- [Denormalizacja](#denormalization)
- [Handler zapytania](#query-handler)
- [Widok zmaterializowany](#materialized-view)
- [Bounded context](#bounded-context)
- [Kompozycja API](#api-composition)
- [Projekcja](#projection)
- [Projekcja synchroniczna](#sync-projection)
- [Projekcja asynchroniczna](#async-projection)
- [Checkpoint](#checkpoint)
- [Replay](#replay)
- [Przebudowa blue-green](#blue-green-rebuild)
- [Zatruta wiadomość](#poison-message)
- [Kolejka martwych wiadomości](#dead-letter-queue)
- [Eventual consistency](#eventual-consistency)
- [Opóźnienie projekcji](#projection-lag)
- [Read-your-writes](#read-your-writes)
- [Token spójności](#consistency-token)
- [Optymistyczny UI](#optimistic-ui)
- [Silna spójność](#strong-consistency)
- [Dual write](#dual-write)
- [Transactional outbox](#outbox)
- [Relay](#message-relay)
- [Inbox](#inbox)
- [At-least-once](#at-least-once)
- [Klucz partycji](#partition-key)
- [Change Data Capture](#cdc)
- [Schema registry](#schema-registry)
- [Event store](#event-store)
- [Strumień zdarzeń](#event-stream)
- [Oczekiwana wersja](#expected-version)
- [Snapshot](#snapshot)
- [Upcasting](#upcasting)
- [Crypto-shredding](#crypto-shredding)
- [Saga](#saga)
- [Kompensacja](#compensation)
- [Process manager](#process-manager)
- [Choreografia](#choreography)
- [Orkiestracja](#orchestration)
- [Given–when–then](#given-when-then)
- [Correlation ID](#correlation-id)
- [Causation ID](#causation-id)
- [Komenda CRUD](#crud-command)
- [Strangler fig](#strangler-fig)

<a id="cqrs"></a>
## CQRS

Command Query Responsibility Segregation: wzorzec, w którym zapis i odczyt mają osobne modele. Spopularyzowany przez Grega Younga.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20CQRS.md#term-cqrs).

<a id="cqs"></a>
## CQS

Command Query Separation Bertranda Meyera: metoda albo zmienia stan i nic nie zwraca, albo zwraca wynik i nic nie zmienia.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20CQRS.md#term-cqs).

<a id="write-model"></a>
## Model zapisu

Model strony zapisu, skupiony na regułach biznesowych i niezmiennikach, zwykle zbudowany z agregatów.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20CQRS.md#term-write-model).

<a id="read-model"></a>
## Model odczytu

Read model: dane w kształcie przygotowanym pod konkretny ekran lub zapytanie, bez reguł biznesowych.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20CQRS.md#term-read-model).

<a id="event-sourcing"></a>
## Event sourcing

Przechowywanie stanu jako niezmiennej listy zdarzeń, z której bieżący stan wylicza się przez odtworzenie.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20CQRS.md#term-event-sourcing).

<a id="command"></a>
## Komenda

Prośba o wykonanie operacji w trybie rozkazującym, z jednym adresatem. Może zostać odrzucona.

Pierwsza wzmianka: [rozdział 02](02%20Strona%20zapisu.md#term-command).

<a id="domain-event"></a>
## Zdarzenie domenowe

Fakt, który już się wydarzył, w czasie przeszłym. Może mieć wielu odbiorców i nie może zostać odrzucony.

Pierwsza wzmianka: [rozdział 02](02%20Strona%20zapisu.md#term-domain-event).

<a id="task-based-ui"></a>
## Task-based UI

Interfejs oferujący akcje biznesowe („Rozwiąż”, „Eskaluj”) zamiast formularzy edycji wszystkich pól.

Pierwsza wzmianka: [rozdział 02](02%20Strona%20zapisu.md#term-task-based-ui).

<a id="command-handler"></a>
## Handler komendy

Kod obsługujący jedną komendę: ładuje agregat, wywołuje regułę, zapisuje zmiany i zdarzenia.

Pierwsza wzmianka: [rozdział 02](02%20Strona%20zapisu.md#term-command-handler).

<a id="aggregate"></a>
## Agregat

Grupa obiektów pilnowana przez jeden korzeń i zapisywana w jednej transakcji. Granica spójności.

Pierwsza wzmianka: [rozdział 02](02%20Strona%20zapisu.md#term-aggregate).

<a id="idempotency"></a>
## Idempotencja

Właściwość operacji, której wielokrotne wykonanie daje ten sam efekt co jednokrotne.

Pierwsza wzmianka: [rozdział 02](02%20Strona%20zapisu.md#term-idempotency).

<a id="idempotency-key"></a>
## Klucz idempotencji

Identyfikator żądania (np. nagłówek `Idempotency-Key`), po którym serwer rozpoznaje powtórzenie i zwraca zapamiętany wynik.

Pierwsza wzmianka: [rozdział 02](02%20Strona%20zapisu.md#term-idempotency-key).

<a id="optimistic-concurrency"></a>
## Optymistyczna kontrola współbieżności

Zapis warunkowy względem oczekiwanej wersji agregatu. Konflikt wykrywa się przy zapisie, bez blokowania rekordu.

Pierwsza wzmianka: [rozdział 02](02%20Strona%20zapisu.md#term-optimistic-concurrency).

<a id="query"></a>
## Zapytanie

Operacja zwracająca dane bez zmiany stanu, obsługiwana przez stronę odczytu.

Pierwsza wzmianka: [rozdział 03](03%20Strona%20odczytu.md#term-query).

<a id="denormalization"></a>
## Denormalizacja

Celowe powielanie danych w modelu odczytu, żeby zapytanie wymagało odczytu jednej tabeli zamiast wielu JOIN-ów.

Pierwsza wzmianka: [rozdział 03](03%20Strona%20odczytu.md#term-denormalization).

<a id="query-handler"></a>
## Handler zapytania

Kod obsługujący zapytanie: czyta model odczytu i sprawdza uprawnienia, bez agregatów i reguł biznesowych.

Pierwsza wzmianka: [rozdział 03](03%20Strona%20odczytu.md#term-query-handler).

<a id="materialized-view"></a>
## Widok zmaterializowany

Wynik zapytania zapisany fizycznie w bazie i odświeżany na żądanie lub okresowo.

Pierwsza wzmianka: [rozdział 03](03%20Strona%20odczytu.md#term-materialized-view).

<a id="bounded-context"></a>
## Bounded context

Część systemu z własnym modelem, językiem i zwykle własnym zespołem.

Pierwsza wzmianka: [rozdział 03](03%20Strona%20odczytu.md#term-bounded-context).

<a id="api-composition"></a>
## Kompozycja API

Składanie odpowiedzi z kilku źródeł w czasie odczytu, przez wywołania ich API.

Pierwsza wzmianka: [rozdział 03](03%20Strona%20odczytu.md#term-api-composition).

<a id="projection"></a>
## Projekcja

Kod przekładający zdarzenia na model odczytu, bez reguł biznesowych.

Pierwsza wzmianka: [rozdział 04](04%20Projekcje.md#term-projection).

<a id="sync-projection"></a>
## Projekcja synchroniczna

Projekcja wykonywana w transakcji zapisu. Daje natychmiastową spójność kosztem wolniejszego zapisu.

Pierwsza wzmianka: [rozdział 04](04%20Projekcje.md#term-sync-projection).

<a id="async-projection"></a>
## Projekcja asynchroniczna

Projekcja działająca w osobnym procesie po commicie. Daje niezależność i skalowanie kosztem opóźnienia.

Pierwsza wzmianka: [rozdział 04](04%20Projekcje.md#term-async-projection).

<a id="checkpoint"></a>
## Checkpoint

Zapisana pozycja projekcji w strumieniu zdarzeń, od której wznawia przetwarzanie.

Pierwsza wzmianka: [rozdział 04](04%20Projekcje.md#term-checkpoint).

<a id="replay"></a>
## Replay

Ponowne przetworzenie wszystkich zdarzeń od początku w celu zbudowania modelu odczytu.

Pierwsza wzmianka: [rozdział 04](04%20Projekcje.md#term-replay).

<a id="blue-green-rebuild"></a>
## Przebudowa blue-green

Budowa nowej wersji modelu odczytu obok starej i przełączenie odczytów po dogonieniu bieżących zdarzeń.

Pierwsza wzmianka: [rozdział 04](04%20Projekcje.md#term-blue-green-rebuild).

<a id="poison-message"></a>
## Zatruta wiadomość

Wiadomość, której nie da się przetworzyć mimo ponowień i która blokuje dalsze przetwarzanie.

Pierwsza wzmianka: [rozdział 04](04%20Projekcje.md#term-poison-message).

<a id="dead-letter-queue"></a>
## Kolejka martwych wiadomości

Dead letter queue: miejsce, do którego trafiają wiadomości niemożliwe do przetworzenia, do analizy i ponownego wprowadzenia.

Pierwsza wzmianka: [rozdział 04](04%20Projekcje.md#term-dead-letter-queue).

<a id="eventual-consistency"></a>
## Eventual consistency

Spójność ostateczna: gwarancja, że modele odczytu w końcu pokażą aktualny stan, bez określenia kiedy.

Pierwsza wzmianka: [rozdział 05](05%20Sp%C3%B3jno%C5%9B%C4%87%20ostateczna.md#term-eventual-consistency).

<a id="projection-lag"></a>
## Opóźnienie projekcji

Czas między commitem po stronie zapisu a widocznością zmiany w modelu odczytu.

Pierwsza wzmianka: [rozdział 05](05%20Sp%C3%B3jno%C5%9B%C4%87%20ostateczna.md#term-projection-lag).

<a id="read-your-writes"></a>
## Read-your-writes

Gwarancja, że użytkownik widzi skutki własnych zapisów w kolejnych odczytach.

Pierwsza wzmianka: [rozdział 05](05%20Sp%C3%B3jno%C5%9B%C4%87%20ostateczna.md#term-read-your-writes).

<a id="consistency-token"></a>
## Token spójności

Wersja lub pozycja zwracana przez komendę, na której osiągnięcie przez projekcję czeka zapytanie.

Pierwsza wzmianka: [rozdział 05](05%20Sp%C3%B3jno%C5%9B%C4%87%20ostateczna.md#term-consistency-token).

<a id="optimistic-ui"></a>
## Optymistyczny UI

Interfejs pokazujący przewidywany skutek komendy przed potwierdzeniem i cofający go przy odrzuceniu.

Pierwsza wzmianka: [rozdział 05](05%20Sp%C3%B3jno%C5%9B%C4%87%20ostateczna.md#term-optimistic-ui).

<a id="strong-consistency"></a>
## Silna spójność

Gwarancja, że odczyt widzi wszystkie zakończone zapisy. Wymagana przy decyzjach krytycznych.

Pierwsza wzmianka: [rozdział 05](05%20Sp%C3%B3jno%C5%9B%C4%87%20ostateczna.md#term-strong-consistency).

<a id="dual-write"></a>
## Dual write

Zapis do dwóch systemów bez wspólnej transakcji, np. baza i broker. Przy awarii zawsze grozi niespójnością.

Pierwsza wzmianka: [rozdział 06](06%20Messaging%20i%20niezawodno%C5%9B%C4%87.md#term-dual-write).

<a id="outbox"></a>
## Transactional outbox

Zapis zdarzeń do tabeli w tej samej transakcji co zmiana stanu i ich późniejsza publikacja przez relay lub CDC.

Pierwsza wzmianka: [rozdział 06](06%20Messaging%20i%20niezawodno%C5%9B%C4%87.md#term-outbox).

<a id="message-relay"></a>
## Relay

Proces czytający outbox i publikujący wiadomości na brokerze, zwykle z gwarancją at-least-once.

Pierwsza wzmianka: [rozdział 06](06%20Messaging%20i%20niezawodno%C5%9B%C4%87.md#term-message-relay).

<a id="inbox"></a>
## Inbox

Tabela ID przetworzonych wiadomości u odbiorcy, aktualizowana w transakcji ze skutkiem przetworzenia.

Pierwsza wzmianka: [rozdział 06](06%20Messaging%20i%20niezawodno%C5%9B%C4%87.md#term-inbox).

<a id="at-least-once"></a>
## At-least-once

Gwarancja dostarczenia wiadomości co najmniej raz, z możliwymi duplikatami.

Pierwsza wzmianka: [rozdział 06](06%20Messaging%20i%20niezawodno%C5%9B%C4%87.md#term-at-least-once).

<a id="partition-key"></a>
## Klucz partycji

Wartość (zwykle ID agregatu), według której broker przydziela wiadomości do partycji i zachowuje ich kolejność.

Pierwsza wzmianka: [rozdział 06](06%20Messaging%20i%20niezawodno%C5%9B%C4%87.md#term-partition-key).

<a id="cdc"></a>
## Change Data Capture

Odczyt zmian z logu transakcji bazy (np. Debezium) i publikacja ich na brokerze.

Pierwsza wzmianka: [rozdział 06](06%20Messaging%20i%20niezawodno%C5%9B%C4%87.md#term-cdc).

<a id="schema-registry"></a>
## Schema registry

Rejestr schematów zdarzeń, który pilnuje zgodności wersji i odrzuca niezgodne publikacje.

Pierwsza wzmianka: [rozdział 06](06%20Messaging%20i%20niezawodno%C5%9B%C4%87.md#term-schema-registry).

<a id="event-store"></a>
## Event store

Magazyn zoptymalizowany pod dopisywanie i odczyt zdarzeń, pogrupowanych w strumienie.

Pierwsza wzmianka: [rozdział 07](07%20Event%20sourcing%20a%20CQRS.md#term-event-store).

<a id="event-stream"></a>
## Strumień zdarzeń

Uporządkowana lista zdarzeń jednego agregatu w event storze.

Pierwsza wzmianka: [rozdział 07](07%20Event%20sourcing%20a%20CQRS.md#term-event-stream).

<a id="expected-version"></a>
## Oczekiwana wersja

Wersja strumienia, którą zakłada zapis. Niezgodność oznacza konflikt współbieżności.

Pierwsza wzmianka: [rozdział 07](07%20Event%20sourcing%20a%20CQRS.md#term-expected-version).

<a id="snapshot"></a>
## Snapshot

Zapisany stan agregatu z określonej wersji, skracający odtwarzanie długich strumieni.

Pierwsza wzmianka: [rozdział 07](07%20Event%20sourcing%20a%20CQRS.md#term-snapshot).

<a id="upcasting"></a>
## Upcasting

Przekształcanie starych wersji zdarzeń do nowej postaci w momencie odczytu, bez zmiany zapisanych danych.

Pierwsza wzmianka: [rozdział 07](07%20Event%20sourcing%20a%20CQRS.md#term-upcasting).

<a id="crypto-shredding"></a>
## Crypto-shredding

Szyfrowanie danych osobowych kluczem per osoba i usunięcie klucza, żeby dane stały się nieczytelne.

Pierwsza wzmianka: [rozdział 07](07%20Event%20sourcing%20a%20CQRS.md#term-crypto-shredding).

<a id="saga"></a>
## Saga

Proces z lokalnych transakcji, w którym niepowodzenie kroku uruchamia kompensacje wcześniejszych kroków.

Pierwsza wzmianka: [rozdział 08](08%20Procesy%20mi%C4%99dzy%20agregatami.md#term-saga).

<a id="compensation"></a>
## Kompensacja

Operacja biznesowa odwracająca skutek wcześniejszego kroku sagi. Nie jest rollbackiem.

Pierwsza wzmianka: [rozdział 08](08%20Procesy%20mi%C4%99dzy%20agregatami.md#term-compensation).

<a id="process-manager"></a>
## Process manager

Komponent ze stanem, który na podstawie zdarzeń decyduje o kolejnych komendach procesu i obsługuje timeouty.

Pierwsza wzmianka: [rozdział 08](08%20Procesy%20mi%C4%99dzy%20agregatami.md#term-process-manager).

<a id="choreography"></a>
## Choreografia

Koordynacja procesu bez centralnego koordynatora: uczestnicy reagują na zdarzenia innych.

Pierwsza wzmianka: [rozdział 08](08%20Procesy%20mi%C4%99dzy%20agregatami.md#term-choreography).

<a id="orchestration"></a>
## Orkiestracja

Koordynacja procesu przez centralny komponent, który wysyła komendy do uczestników.

Pierwsza wzmianka: [rozdział 08](08%20Procesy%20mi%C4%99dzy%20agregatami.md#term-orchestration).

<a id="given-when-then"></a>
## Given–when–then

Format testu: zdarzenia z przeszłości, komenda, oczekiwane zdarzenia lub błąd.

Pierwsza wzmianka: [rozdział 09](09%20Testy%20i%20operacje.md#term-given-when-then).

<a id="correlation-id"></a>
## Correlation ID

Identyfikator wspólny dla całego łańcucha wiadomości wywołanego jedną akcją.

Pierwsza wzmianka: [rozdział 09](09%20Testy%20i%20operacje.md#term-correlation-id).

<a id="causation-id"></a>
## Causation ID

ID wiadomości, która bezpośrednio spowodowała powstanie danej wiadomości.

Pierwsza wzmianka: [rozdział 09](09%20Testy%20i%20operacje.md#term-causation-id).

<a id="crud-command"></a>
## Komenda CRUD

Komenda typu `UpdateX` z pełnym zestawem pól, która ukrywa intencję biznesową.

Pierwsza wzmianka: [rozdział 10](10%20Pu%C5%82apki%20i%20migracja.md#term-crud-command).

<a id="strangler-fig"></a>
## Strangler fig

Wzorzec stopniowej migracji, w którym nowa struktura przejmuje kolejne funkcje starej.

Pierwsza wzmianka: [rozdział 10](10%20Pu%C5%82apki%20i%20migracja.md#term-strangler-fig).
