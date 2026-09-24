# Projekcje

Model odczytu nie aktualizuje się sam. Musi go zasilać kod, który reaguje na zmiany po stronie zapisu i przekłada je na kształt potrzebny odczytowi. Ten kod jest najczęstszym źródłem problemów w systemach CQRS, bo działa w tle, przetwarza każde zdarzenie i musi przetrwać awarie, ponowienia oraz zmiany schematu.

```text
TicketOpened    ──►  ┌──────────────────────┐  ──►  agent_queue
TicketAssigned  ──►  │ AgentQueueProjection │  ──►  (INSERT / UPDATE / DELETE)
TicketResolved  ──►  └──────────────────────┘
                              │
                              └──► checkpoint: pozycja 18 452
```

## Zdarzenie na wejściu, model na wyjściu

<a id="term-projection"></a>[Projekcja](00%20Glossary%20CQRS.md#projection) to kod, który przyjmuje zdarzenia domenowe i aktualizuje na ich podstawie model odczytu. Każdy model odczytu ma zwykle własną projekcję:

```python
class AgentQueueProjection:
    def __init__(self, db):
        self._db = db

    def handle(self, event) -> None:
        match event:
            case TicketOpened():
                self._db.execute(text("""
                    INSERT INTO agent_queue (ticket_id, agent_id, title, customer_name,
                                             priority, priority_rank, sla_deadline, last_activity_at)
                    VALUES (:id, NULL, :title, :customer, :prio, :rank, :sla, :at)
                """), {"id": event.ticket_id, "title": event.title, "customer": event.customer_name,
                       "prio": event.priority, "rank": RANK[event.priority],
                       "sla": event.opened_at + SLA[event.priority], "at": event.opened_at})
            case TicketAssigned():
                self._db.execute(text(
                    "UPDATE agent_queue SET agent_id = :a, last_activity_at = :at WHERE ticket_id = :id"
                ), {"a": event.agent_id, "at": event.assigned_at, "id": event.ticket_id})
            case TicketResolved():
                self._db.execute(text("DELETE FROM agent_queue WHERE ticket_id = :id"),
                                 {"id": event.ticket_id})
```

W porównaniu z rozdziałem 02 zdarzenie `TicketOpened` ma tu dodatkowe pole `customer_name`. Projekcja nie powinna sięgać do innych tabel, żeby ustalić nazwę klienta. Zdarzenia projektuje się tak, żeby projekcje miały wszystko, czego potrzebują, albo żeby mogły to wziąć z własnych, wcześniej zbudowanych modeli.

Projekcja nie zawiera reguł biznesowych. Nie decyduje, czy zgłoszenie można zamknąć, bo tę decyzję podjęła już strona zapisu. Przekłada tylko fakty na dane do odczytu.

## W transakcji czy w tle

Projekcja może działać na dwa sposoby.

<a id="term-sync-projection"></a>[Projekcja synchroniczna](00%20Glossary%20CQRS.md#sync-projection) działa w tej samej transakcji co zapis. Handler komendy zapisuje agregat, a przed commitem te same zdarzenia trafiają do projekcji:

```python
class SqlUnitOfWork:
    def commit(self):
        for ticket in self.tickets.seen:
            for event in ticket.events:
                for projection in self._sync_projections:
                    projection.handle(event)          # ta sama sesja, ta sama transakcja
            ticket.events.clear()
        self._session.commit()
```

<a id="term-async-projection"></a>[Projekcja asynchroniczna](00%20Glossary%20CQRS.md#async-projection) działa w osobnym procesie. Czyta zdarzenia z outboxa, kolejki albo event store'a i aktualizuje model odczytu po zakończeniu transakcji zapisu.

| | Synchroniczna | Asynchroniczna |
|---|---|---|
| Spójność | natychmiastowa | ostateczna, z opóźnieniem |
| Magazyn odczytu | ta sama baza | dowolny, np. Elasticsearch |
| Wpływ na zapis | wolniejszy commit, błąd projekcji wycofuje komendę | brak, zapis kończy się szybciej |
| Skalowanie | razem z zapisem | niezależne |
| Odbudowa | wymaga osobnego mechanizmu | ten sam kod co bieżące przetwarzanie |

Rozsądny podział: projekcje w tej samej bazie, potrzebne od razu po zapisie (np. kolejka agenta), mogą być synchroniczne. Projekcje do innych magazynów, raporty i wszystko, co jest ciężkie, powinno być asynchroniczne. Błąd w projekcji raportu nie powinien uniemożliwiać zamknięcia zgłoszenia.

## Ta sama wiadomość dwa razy

Projekcja asynchroniczna prawie zawsze dostaje zdarzenia w trybie „co najmniej raz”, co opisuje rozdział 06. To samo zdarzenie może więc przyjść dwa razy. Projekcja musi dawać ten sam wynik bez względu na liczbę powtórzeń. Jest kilka technik:

- operacje z natury powtarzalne: `UPSERT` z pełnym stanem wiersza zamiast `UPDATE count = count + 1`,
- zapamiętywanie ostatniej przetworzonej wersji agregatu w wierszu i pomijanie starszych zdarzeń,
- tabela przetworzonych ID zdarzeń, sprawdzana i uzupełniana w tej samej transakcji co zmiana modelu.

```python
def on_message_added(self, event: MessageAdded) -> None:
    self._db.execute(text("""
        UPDATE agent_queue
        SET message_count = message_count + 1, last_activity_at = :at, ticket_version = :v
        WHERE ticket_id = :id AND ticket_version < :v          -- starsze lub powtórzone zdarzenie nic nie zmieni
    """), {"at": event.at, "v": event.ticket_version, "id": event.ticket_id})
```

Warunek `ticket_version < :v` rozwiązuje dwa problemy naraz: powtórzone zdarzenie niczego nie zmienia, a zdarzenie, które przyszło za późno, nie nadpisze nowszego stanu.

## Gdzie skończyłem

Projekcja asynchroniczna musi pamiętać, które zdarzenia już przetworzyła. Służy do tego <a id="term-checkpoint"></a>[checkpoint](00%20Glossary%20CQRS.md#checkpoint): zapisana pozycja w strumieniu zdarzeń, np. numer w outboxie, offset w Kafce albo pozycja w event storze.

Kolejność zapisu zmian i checkpointu decyduje o zachowaniu przy awarii:

| Kolejność | Awaria pomiędzy | Efekt |
|---|---|---|
| najpierw model, potem checkpoint | zdarzenie przetworzone, pozycja nie | zdarzenie zostanie przetworzone drugi raz |
| najpierw checkpoint, potem model | pozycja zapisana, zdarzenie nie | zdarzenie zostanie pominięte, model jest błędny |
| model i checkpoint w jednej transakcji | nie ma „pomiędzy” | dokładnie raz dla tego magazynu |

Drugi wariant jest niedopuszczalny, bo gubi dane po cichu. Pierwszy wymaga idempotentnej projekcji. Trzeci jest najlepszy, ale możliwy tylko wtedy, gdy checkpoint i model odczytu leżą w tej samej bazie:

```python
def process_batch(self, events: list[StoredEvent]) -> None:
    with self._db.begin():                               # jedna transakcja
        for e in events:
            self._projection.handle(e.payload)
        self._db.execute(text(
            "UPDATE projection_checkpoints SET position = :p WHERE name = :n"
        ), {"p": events[-1].position, "n": "agent_queue"})
```

Dla Elasticsearch albo Redis nie ma wspólnej transakcji z checkpointem. Wtedy stosuje się pierwszy wariant z idempotentną projekcją.

## Odbudowa od zera

Model odczytu można w każdej chwili usunąć i zbudować ponownie, bo źródłem prawdy jest strona zapisu. Ponowne przetworzenie wszystkich zdarzeń od początku to <a id="term-replay"></a>[replay](00%20Glossary%20CQRS.md#replay). Jest potrzebny, gdy pojawia się nowy model odczytu, gdy poprawiono błąd w projekcji albo gdy zmieniono schemat modelu.

Replay wymaga źródła wszystkich zdarzeń od początku. Przy event sourcingu jest nim event store. Bez event sourcingu trzeba albo trzymać zdarzenia w trwałym logu (Kafka z długą retencją, tabela zdarzeń), albo odbudować model bezpośrednio z tabel strony zapisu jednorazowym zapytaniem.

Odbudowa bez przestoju przebiega jak <a id="term-blue-green-rebuild"></a>[przebudowa blue-green](00%20Glossary%20CQRS.md#blue-green-rebuild):

```text
1. stara projekcja działa dalej i obsługuje odczyty z agent_queue_v1
2. nowa projekcja buduje agent_queue_v2 od pozycji 0
3. v2 dogania bieżące zdarzenia (opóźnienie spada do sekund)
4. przełączenie odczytów: widok, alias albo konfiguracja wskazuje na v2
5. stara projekcja zostaje zatrzymana, v1 usunięta po okresie obserwacji
```

W Elasticsearch przełączenie robi się aliasem indeksu. W PostgreSQL widokiem `agent_queue`, który wskazuje na właściwą tabelę, albo zmianą nazw tabel w jednej transakcji.

## Zmiana schematu i logiki

Projekcje trzeba wersjonować jak kod, bo z czasem zmieniają się i one, i model odczytu. Są trzy rodzaje zmian:

- dodanie kolumny, którą można wyliczyć z istniejących danych: migracja SQL, bez replayu,
- dodanie kolumny, której wartość jest tylko w zdarzeniach: replay do nowej wersji modelu,
- zmiana logiki, np. inny sposób liczenia terminu SLA: replay, bo stare wiersze mają wynik starej logiki.

Praktyczna konwencja: nazwa projekcji zawiera wersję (`agent_queue_v2`), a checkpoint jest zapisany per wersja. Zmiana wersji w kodzie automatycznie uruchamia budowę od zera obok starej, zgodnie z procedurą blue-green. Dzięki temu wdrożenie nowej logiki projekcji nie wymaga ręcznych kroków.

## Zdarzenie, którego nie da się przetworzyć

Czasem projekcja nie potrafi przetworzyć zdarzenia: brakuje wymaganego pola, serializacja się zmieniła albo kod ma błąd. Takie zdarzenie to <a id="term-poison-message"></a>[zatruta wiadomość](00%20Glossary%20CQRS.md#poison-message). Ponawianie w nieskończoność blokuje całą projekcję, bo kolejne zdarzenia czekają.

Strategie:

1. Ponów kilka razy z rosnącym odstępem, bo błąd może być chwilowy (timeout bazy).
2. Po wyczerpaniu prób przenieś zdarzenie do <a id="term-dead-letter-queue"></a>[kolejki martwych wiadomości](00%20Glossary%20CQRS.md#dead-letter-queue) (dead letter queue) i przetwarzaj dalej.
3. Uruchom alert. Ktoś musi przeanalizować zdarzenie, poprawić kod i ponownie wprowadzić wiadomość.

Przeniesienie do DLQ i dalsze przetwarzanie jest bezpieczne tylko wtedy, gdy kolejność nie ma znaczenia albo kolejne zdarzenia dotyczą innych agregatów. Jeśli zdarzenie `TicketOpened` trafi do DLQ, późniejsze `TicketAssigned` dla tego samego zgłoszenia zaktualizuje nieistniejący wiersz. Dlatego przy zależnościach kolejności lepiej zatrzymać projekcję dla danego agregatu (albo całą) i podnieść alarm, niż budować błędny model.

| Strategia | Kiedy |
|---|---|
| retry z backoffem | błędy przejściowe: sieć, timeout, blokada |
| DLQ i przetwarzanie dalej | zdarzenia niezależne, np. statystyki, powiadomienia |
| zatrzymanie projekcji i alert | kolejność ma znaczenie, błąd psułby model |

## Co zapamiętać

- Projekcja zamienia zdarzenia na model odczytu i nie zawiera reguł biznesowych.
- Projekcja synchroniczna daje natychmiastową spójność kosztem zapisu, a asynchroniczna niezależność kosztem opóźnienia.
- Projekcja asynchroniczna musi być idempotentna. Wersja agregatu w wierszu chroni też przed zdarzeniami, które przyszły za późno.
- Checkpoint i zmiana modelu w jednej transakcji dają przetwarzanie dokładnie raz. Checkpoint przed zmianą gubi dane.
- Replay odbudowuje model od zera, a blue-green pozwala zrobić to bez przestoju.
- Wersja projekcji w nazwie i checkpoint per wersja automatyzują zmiany logiki.
- Zatruta wiadomość trafia do DLQ, chyba że kolejność ma znaczenie. Wtedy lepiej zatrzymać projekcję.

## Pytania sprawdzające

### 17. Czym jest projekcja i czym różni się projekcja synchroniczna (w tej samej transakcji) od asynchronicznej?

<details>
<summary>Odpowiedź</summary>

Projekcja to kod, który przyjmuje zdarzenia i aktualizuje model odczytu, bez reguł biznesowych. Synchroniczna działa w transakcji zapisu: spójność jest natychmiastowa, ale commit jest wolniejszy, a błąd projekcji wycofuje komendę. Do tego działa tylko w tej samej bazie. Asynchroniczna działa w osobnym procesie po commicie: dowolny magazyn, niezależne skalowanie, ten sam kod do odbudowy, ale spójność ostateczna. Szybkie projekcje w tej samej bazie mogą być synchroniczne, a reszta asynchroniczna.

Zobacz: sekcje „Zdarzenie na wejściu, model na wyjściu” i „W transakcji czy w tle”.

</details>

### 18. Jak zbudować projekcję odporną na ponowne dostarczenie zdarzenia (idempotentny handler, pozycja, wersja)?

<details>
<summary>Odpowiedź</summary>

Przez operacje z natury powtarzalne (UPSERT pełnego stanu zamiast inkrementacji), zapamiętywanie wersji agregatu w wierszu z warunkiem `WHERE version < :v` albo tabelę przetworzonych ID zdarzeń aktualizowaną w tej samej transakcji. Warunek na wersji chroni jednocześnie przed powtórzeniami i przed nadpisaniem nowszego stanu przez spóźnione zdarzenie.

Zobacz: sekcja „Ta sama wiadomość dwa razy”.

</details>

### 19. Jak odbudować read model od zera (replay) i jak zrobić to bez przestoju (blue-green, podwójny zapis, alias)?

<details>
<summary>Odpowiedź</summary>

Replay to ponowne przetworzenie wszystkich zdarzeń od początku. Wymaga ich źródła: event store'u, trwałego logu (Kafka z długą retencją, tabela zdarzeń) albo jednorazowego zapytania do tabel zapisu. Bez przestoju: stara projekcja obsługuje odczyty z v1, nowa buduje v2 od zera i dogania bieżące zdarzenia, potem odczyty przełącza się aliasem (Elasticsearch), widokiem lub zmianą nazw tabel (PostgreSQL), a starą wersję usuwa się po okresie obserwacji.

Zobacz: sekcja „Odbudowa od zera”.

</details>

### 20. Co zrobić, gdy zmienia się schemat read modelu albo logika projekcji? Jak wersjonować projekcje?

<details>
<summary>Odpowiedź</summary>

Kolumnę wyliczalną z istniejących danych dodaje się migracją. Kolumna z danymi obecnymi tylko w zdarzeniach i zmiana logiki wymagają replayu, bo stare wiersze mają wynik starej logiki. Konwencja: wersja w nazwie projekcji i modelu (`agent_queue_v2`) oraz checkpoint per wersja. Nowa wersja w kodzie automatycznie buduje się obok starej, po czym następuje przełączenie w stylu blue-green.

Zobacz: sekcja „Zmiana schematu i logiki”.

</details>

### 21. Jak śledzić pozycję projekcji (checkpoint) i co się stanie, gdy projekcja przetworzy zdarzenie, ale nie zapisze pozycji?

<details>
<summary>Odpowiedź</summary>

Checkpoint to zapisana pozycja w strumieniu (numer outboxa, offset Kafki, pozycja event store'u). Jeśli projekcja przetworzy zdarzenie, ale nie zapisze pozycji, po restarcie przetworzy je drugi raz, więc musi być idempotentna. Zapis checkpointu przed zmianą modelu jest niedopuszczalny, bo przy awarii zdarzenie zostanie pominięte. Najlepiej zapisywać model i checkpoint w jednej transakcji, co jest możliwe, gdy leżą w tej samej bazie.

Zobacz: sekcja „Gdzie skończyłem”.

</details>

### 22. Jak obsłużyć zdarzenie, którego projekcja nie potrafi przetworzyć (poison message, retry, dead letter, zatrzymanie)?

<details>
<summary>Odpowiedź</summary>

Najpierw kilka ponowień z rosnącym odstępem na wypadek błędu przejściowego. Potem przeniesienie do dead letter queue i dalsze przetwarzanie z alertem, co jest bezpieczne tylko przy zdarzeniach niezależnych (np. statystyki). Gdy kolejność ma znaczenie, na przykład utracony `TicketOpened` psułby kolejne zdarzenia zgłoszenia, lepiej zatrzymać projekcję dla agregatu albo całą i podnieść alarm. Po naprawie kodu wiadomość wprowadza się ponownie.

Zobacz: sekcja „Zdarzenie, którego nie da się przetworzyć”.

</details>
