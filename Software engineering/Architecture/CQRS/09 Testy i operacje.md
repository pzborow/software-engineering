# Testy i operacje

System CQRS składa się z wielu elementów działających niezależnie: handlerów komend, projekcji, relaya, konsumentów i process managerów. Każdy z nich trzeba przetestować osobno, a na produkcji trzeba widzieć, czy razem działają poprawnie. Ten rozdział pokazuje, jak testować każdą część i co monitorować.

```text
element             test                                    na produkcji monitoruj
──────────────────  ──────────────────────────────────────  ─────────────────────────────
agregat, handler    given zdarzenia, when komenda, then ... odrzucone komendy, konflikty
projekcja           given zdarzenia, then model odczytu     opóźnienie, pozycja, błędy
outbox i relay      test integracyjny z bazą i brokerem     liczba niewysłanych, wiek najstarszego
konsument           duplikaty, kolejność, zatruta wiadomość rozmiar DLQ
proces              scenariusze z kompensacjami             procesy utknięte, wymagające interwencji
```

## Testy w języku zdarzeń

Strona zapisu przyjmuje komendę i produkuje zdarzenia. Najbardziej czytelne testy opisują to wprost, w formacie <a id="term-given-when-then"></a>[given–when–then](00%20Glossary%20CQRS.md#given-when-then): mając te zdarzenia z przeszłości, gdy przyjdzie ta komenda, powinny powstać te zdarzenia albo ten błąd.

```python
NOW = datetime(2026, 9, 24, 10, 0, tzinfo=UTC)


def test_assigning_open_ticket_emits_assigned():
    given(TicketOpened("T-1", "C-1", "Drukarka", "high", NOW))
    when(AssignTicket("T-1", agent_id="A-7", expected_version=1))
    then(TicketAssigned("T-1", "A-7", NOW))


def test_resolved_ticket_cannot_be_assigned():
    given(TicketOpened("T-1", "C-1", "Drukarka", "high", NOW),
          TicketResolved("T-1", "replaced", NOW))
    when(AssignTicket("T-1", agent_id="A-7", expected_version=2))
    then_rejected(TicketError)


def test_assigning_to_same_agent_is_idempotent():
    given(TicketOpened("T-1", "C-1", "Drukarka", "high", NOW),
          TicketAssigned("T-1", "A-7", NOW))
    when(AssignTicket("T-1", agent_id="A-7", expected_version=2))
    then()                                             # brak nowych zdarzeń
```

Funkcje `given`, `when` i `then` to mały fixture. `given` wkłada zdarzenia do event store'u w pamięci (albo buduje z nich agregat), `when` uruchamia prawdziwy handler, a `then` porównuje nowe zdarzenia z oczekiwanymi. Test nie zna wewnętrznych pól agregatu, więc przeżywa refaktoryzację.

Projekcje testuje się tym samym językiem, ale na wyjściu jest stan modelu odczytu:

```python
def test_queue_shows_assigned_ticket_and_hides_resolved(projection_db):
    project(projection_db,
            TicketOpened("T-1", "C-1", "Drukarka", "high", NOW, customer_name="ACME"),
            TicketOpened("T-2", "C-2", "Monitor", "low", NOW, customer_name="Beta"),
            TicketAssigned("T-1", "A-7", NOW),
            TicketAssigned("T-2", "A-7", NOW),
            TicketResolved("T-2", "fixed", NOW))

    assert AgentQueueQuery(projection_db)("A-7") == [
        QueueItem("T-1", "Drukarka", "ACME", "high", NOW + SLA["high"], 0),
    ]


def test_projection_ignores_duplicated_event(projection_db):
    e = TicketOpened("T-1", "C-1", "Drukarka", "high", NOW, customer_name="ACME")
    project(projection_db, e, e)
    assert count(projection_db, "agent_queue") == 1
```

Każda projekcja powinna mieć testy na duplikaty i na zdarzenia, które przyszły za późno, bo w produkcji oba przypadki się zdarzają (rozdziały 04 i 06).

## Testy przepływów i kontraktów

Process managery testuje się jako maszyny stanów: dla każdej pary „stan i zdarzenie” sprawdza się stan docelowy i wysłane komendy. Szczególnie ważne są ścieżki kompensacji, bo na produkcji wykonują się rzadko i łatwo w nich o błąd.

```python
def test_declined_fee_cancels_courier_and_releases_device():
    p = ReplacementProcess("T-1", state="courier_scheduled", reservation_id="R-1", shipment_id="S-1")
    commands = p.on(FeeDeclined("T-1"))
    assert p.state == "compensating"
    assert commands == [CancelCourier("S-1"), ReleaseDevice("R-1")]
```

Zdarzenia integracyjne są kontraktem między zespołami, więc testuje się je jak API. Producent ma test, który serializuje każde zdarzenie i sprawdza zgodność z zarejestrowanym schematem. Konsumenci utrzymują przykładowe wiadomości, które muszą umieć przetworzyć. W podejściu consumer-driven contracts (np. Pact dla wiadomości) konsumenci publikują swoje oczekiwania, a CI producenta sprawdza, czy ich nie łamie.

| Rodzaj testu | Co wykrywa | Gdzie działa |
|---|---|---|
| given–when–then na agregacie | złe reguły, złe zdarzenia | testy jednostkowe, milisekundy |
| test projekcji | zły model odczytu, brak idempotencji | z prawdziwą bazą odczytu (Testcontainers) |
| test process managera | złe przejścia stanów, brakujące kompensacje | testy jednostkowe |
| test kontraktu zdarzeń | niezgodne zmiany schematu | CI producenta i konsumentów |
| test end-to-end | złe połączenie elementów, konfiguracja | kilka scenariuszy, z czekaniem na projekcje |

Testy end-to-end muszą uwzględniać spójność ostateczną. Zamiast `sleep(2)` stosuje się czekanie na warunek z timeoutem albo na checkpoint projekcji, tak jak w tokenie spójności z rozdziału 05.

## Śledzenie przyczyn

Jedno kliknięcie użytkownika uruchamia łańcuch: komenda, zdarzenie, projekcja, process manager, kolejne komendy w innych serwisach. Gdy coś pójdzie źle, trzeba umieć odtworzyć cały łańcuch. Służą do tego dwa identyfikatory w metadanych każdej wiadomości.

<a id="term-correlation-id"></a>[Correlation ID](00%20Glossary%20CQRS.md#correlation-id) jest wspólny dla całego łańcucha. Nadaje go pierwsze żądanie, a każda kolejna komenda i zdarzenie go przepisuje.

<a id="term-causation-id"></a>[Causation ID](00%20Glossary%20CQRS.md#causation-id) wskazuje bezpośrednią przyczynę, czyli ID wiadomości, która spowodowała powstanie tej wiadomości.

```text
wiadomość                     message_id   correlation_id   causation_id
HTTP POST /resolve            req-1        req-1            -
ResolveTicket (komenda)       cmd-1        req-1            req-1
TicketResolved (zdarzenie)    evt-1        req-1            cmd-1
ReserveDevice (komenda)       cmd-2        req-1            evt-1
DeviceReserved (zdarzenie)    evt-2        req-1            cmd-2
ScheduleCourier (komenda)     cmd-3        req-1            evt-2
```

Po correlation ID można wyszukać w logach wszystko, co dotyczy jednej akcji użytkownika. Po causation ID można zbudować drzewo przyczyn i zobaczyć, która wiadomość wywołała którą. Oba identyfikatory przekazuje się też do trace'ów OpenTelemetry, dzięki czemu łańcuch asynchroniczny widać w jednym widoku, obok wywołań synchronicznych.

## Co monitorować

Najważniejsze metryki systemu CQRS:

| Metryka | Co oznacza wzrost | Przykładowy próg alertu |
|---|---|---|
| opóźnienie projekcji (p99) | projekcja nie nadąża albo stoi | powyżej celu uzgodnionego z biznesem, np. 5 s |
| różnica pozycji: strumień minus checkpoint | rośnie kolejka nieprzetworzonych zdarzeń | rośnie przez 10 minut |
| liczba niewysłanych w outboxie i wiek najstarszego | relay nie działa lub broker jest niedostępny | najstarszy powyżej 1 min |
| rozmiar dead letter queue | pojawiają się zatrute wiadomości | każdy nowy wpis |
| odrzucone komendy według przyczyny | błąd w UI lub zmiana zachowania użytkowników | nagły skok |
| konflikty współbieżności | wiele osób edytuje te same obiekty | trend rosnący |
| procesy w stanie „wymaga interwencji” | nieudane kompensacje | każdy nowy wpis |
| slot replikacji CDC (rozmiar zatrzymanego WAL) | Debezium nie czyta logu | powyżej kilku GB |

Do tego dochodzą standardowe metryki: czas obsługi komend i zapytań, błędy, zużycie zasobów. Kluczowa różnica wobec zwykłego systemu jest taka, że „wszystko zwraca 200” nie oznacza, że działa poprawnie. Komendy mogą przechodzić, a projekcja od godziny stać. Dlatego metryki opóźnienia i kolejek są w CQRS równie ważne jak dostępność API.

## Co zapamiętać

- Stronę zapisu testuje się w formacie given–when–then: zdarzenia z przeszłości, komenda, oczekiwane zdarzenia lub błąd.
- Projekcje testuje się zdarzeniami na wejściu i stanem modelu na wyjściu, w tym na duplikaty i spóźnione zdarzenia.
- Process managery testuje się jak maszyny stanów, ze szczególnym naciskiem na kompensacje.
- Zdarzenia integracyjne mają testy kontraktowe w CI producenta i konsumentów.
- Testy end-to-end czekają na warunek lub checkpoint zamiast używać `sleep`.
- Correlation ID łączy cały łańcuch wiadomości, a causation ID wskazuje bezpośrednią przyczynę.
- Monitoruj opóźnienie projekcji, outbox, DLQ i procesy wymagające interwencji, bo sukces API nie oznacza poprawnego działania całości.

## Pytania sprawdzające

### 42. Jak testować handlery komend, projekcje i całe przepływy (given–when–then na zdarzeniach, testy kontraktowe zdarzeń)?

<details>
<summary>Odpowiedź</summary>

Handlery i agregaty testuje się w formacie given–when–then: zdarzenia z przeszłości, komenda, oczekiwane nowe zdarzenia lub odrzucenie. Test nie zna wewnętrznych pól, więc przeżywa refaktoryzację. Projekcje testuje się zdarzeniami na wejściu i stanem modelu na wyjściu, obowiązkowo z duplikatami i spóźnionymi zdarzeniami. Process managery testuje się jak maszyny stanów, z naciskiem na kompensacje. Zdarzenia integracyjne mają testy kontraktowe (zgodność ze schematem, consumer-driven contracts). Nieliczne testy end-to-end czekają na warunek lub checkpoint zamiast `sleep`.

Zobacz: sekcje „Testy w języku zdarzeń” i „Testy przepływów i kontraktów”.

</details>

### 43. Co monitorować w systemie CQRS (opóźnienie projekcji, rozmiar outboxa, dead letter, correlation ID i causation ID)?

<details>
<summary>Odpowiedź</summary>

Należy monitorować opóźnienie projekcji (p99 wobec celu biznesowego), różnicę między pozycją strumienia a checkpointem, liczbę i wiek niewysłanych wpisów w outboxie, rozmiar DLQ, odrzucone komendy i konflikty współbieżności, procesy wymagające interwencji oraz slot replikacji CDC. Każda wiadomość niesie correlation ID (wspólny dla całego łańcucha od akcji użytkownika) i causation ID (ID bezpośredniej przyczyny), przekazywane do logów i trace'ów OpenTelemetry. Sukces API nie oznacza, że projekcje działają.

Zobacz: sekcje „Śledzenie przyczyn” i „Co monitorować”.

</details>
