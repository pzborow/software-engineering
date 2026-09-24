# Messaging i niezawodność

Asynchroniczne projekcje, powiadomienia i integracje z innymi systemami zależą od tego, czy zdarzenie dotrze z bazy strony zapisu do odbiorców. Po drodze są sieć, broker, restarty procesów i awarie. Ten rozdział opisuje wzorce, które sprawiają, że zdarzenie nie zginie i nie zostanie przetworzone w szkodliwy sposób.

```text
handler ──► [tickets + outbox] ──► relay / CDC ──► broker ──► [inbox + model] ──► odbiorca
             jedna transakcja                                  jedna transakcja
```

## Dwa zapisy bez wspólnej transakcji

Handler komendy musi zrobić dwie rzeczy: zapisać zmianę w bazie i opublikować zdarzenie na brokerze. To dwa systemy bez wspólnej transakcji. Taka sytuacja to <a id="term-dual-write"></a>[dual write](00%20Glossary%20CQRS.md#dual-write) i zawsze prowadzi do niespójności przy awarii:

| Kolejność | Awaria pomiędzy | Skutek |
|---|---|---|
| commit, potem publikacja | proces pada po commicie | zmiana jest, zdarzenia nie ma, projekcje i inne systemy nie wiedzą |
| publikacja, potem commit | commit się nie udaje | zdarzenie opisuje zmianę, której nie ma |
| publikacja w środku transakcji | rollback po publikacji | jak wyżej |

Nie pomaga ponawianie ani `try/except`, bo proces może zginąć w dowolnym momencie, na przykład przez OOM killer albo restart poda.

Rozwiązaniem jest <a id="term-outbox"></a>[transactional outbox](00%20Glossary%20CQRS.md#outbox). Zdarzenia zapisuje się do tabeli `outbox` w tej samej transakcji co zmianę agregatu. Osobny proces, <a id="term-message-relay"></a>[relay](00%20Glossary%20CQRS.md#message-relay), czyta outbox i publikuje wiadomości na brokerze:

```sql
CREATE TABLE outbox (
    id            bigserial PRIMARY KEY,           -- kolejność zapisu
    event_id      uuid NOT NULL UNIQUE,
    aggregate_id  uuid NOT NULL,
    event_type    text NOT NULL,
    payload       jsonb NOT NULL,
    recorded_at   timestamptz NOT NULL DEFAULT now(),
    published_at  timestamptz
);
```

```python
class OutboxRelay:
    def run_once(self, batch: int = 100) -> None:
        with self._db.begin():
            rows = self._db.execute(text("""
                SELECT id, event_id, aggregate_id, event_type, payload FROM outbox
                WHERE published_at IS NULL ORDER BY id LIMIT :n
                FOR UPDATE SKIP LOCKED
            """), {"n": batch}).all()
            for r in rows:
                self._producer.send(topic=r.event_type, key=str(r.aggregate_id),
                                    value=r.payload, headers={"event_id": str(r.event_id)})
            self._producer.flush()
            self._db.execute(text("UPDATE outbox SET published_at = now() WHERE id = ANY(:ids)"),
                             {"ids": [r.id for r in rows]})
```

Relay może opublikować wiadomość i paść przed oznaczeniem jej jako wysłanej. Po restarcie opublikuje ją ponownie. Outbox gwarantuje więc, że zdarzenie zostanie wysłane co najmniej raz, ale nie dokładnie raz. Tym zajmują się odbiorcy.

Dwie subtelności warto znać. Po pierwsze, `bigserial` nadaje numery w chwili wstawienia, a nie commitu. Dłuższa transakcja może więc zatwierdzić wiersz o niższym `id` później niż krótsza, a relay przeskoczy go przy odpytywaniu, jeśli filtruje po `id > ostatni`. Warunek `published_at IS NULL` tego unika. Po drugie, kilka instancji relaya z `SKIP LOCKED` przyspiesza publikację, ale może zamienić kolejność zdarzeń tego samego agregatu. Kolejność per agregat zapewnia wtedy wersja w zdarzeniu, opisana niżej.

## Deduplikacja u odbiorcy

<a id="term-inbox"></a>[Inbox](00%20Glossary%20CQRS.md#inbox) to lustrzany wzorzec po stronie odbiorcy. Odbiorca zapisuje ID przetworzonych wiadomości w tabeli `inbox`, w tej samej transakcji co skutek przetworzenia. Powtórzona wiadomość trafia na istniejący wpis i jest pomijana:

```python
class InboxConsumer:
    def handle(self, message) -> None:
        event_id = message.headers["event_id"]
        with self._db.begin():
            inserted = self._db.execute(text("""
                INSERT INTO inbox (event_id, consumer, processed_at)
                VALUES (:id, :c, now()) ON CONFLICT DO NOTHING
            """), {"id": event_id, "c": "agent_queue"}).rowcount
            if inserted == 0:
                return                                  # już przetworzone
            self._projection.handle(deserialize(message))
        message.ack()
```

Outbox po stronie nadawcy i inbox po stronie odbiorcy dają razem efekt „dokładnie raz” dla skutków w bazie odbiorcy. Wiadomość może przejść przez sieć wiele razy, ale jej skutek zostanie zapisany raz.

Tabela `inbox` rośnie, więc stare wpisy trzeba usuwać. Okres przechowywania musi być dłuższy niż maksymalny czas, po którym broker może ponownie dostarczyć wiadomość.

## Gwarancje dostarczenia

Systemy messagingu oferują trzy poziomy gwarancji. W praktyce najważniejszy jest środkowy, <a id="term-at-least-once"></a>[at-least-once](00%20Glossary%20CQRS.md#at-least-once), bo daje go outbox i większość brokerów:

| Poziom | Znaczenie | Ryzyko |
|---|---|---|
| at-most-once | wiadomość dotrze raz albo wcale | utrata wiadomości |
| at-least-once | wiadomość dotrze co najmniej raz | duplikaty |
| exactly-once | wiadomość zostanie przetworzona dokładnie raz | w ogólnym przypadku nieosiągalne |

W systemach rozproszonych, w których odbiorca wykonuje efekty uboczne poza brokerem (zapis do bazy, wywołanie API, wysłanie e-maila), exactly-once nie istnieje jako gwarancja infrastruktury. Odbiorca może przetworzyć wiadomość i paść przed potwierdzeniem, a broker nie ma jak się o tym dowiedzieć. Kafka oferuje transakcje exactly-once, ale tylko dla przepływu „czytaj z Kafki, pisz do Kafki”. Nie obejmują one zapisu do PostgreSQL ani wysłania e-maila.

Praktyczna reguła: zakładaj at-least-once i buduj odbiorców idempotentnych. W połączeniu z inboxem albo idempotentną projekcją daje to efekt nazywany effectively-once. Dla efektów zewnętrznych, takich jak e-mail albo płatność, idempotencję musi zapewnić odbiorca efektu, na przykład przez klucz idempotencji w API płatności.

## Kolejność zdarzeń

Projekcja `agent_queue` musi dostać `TicketOpened` przed `TicketAssigned` dla tego samego zgłoszenia. Kolejność dla różnych zgłoszeń nie ma znaczenia.

Brokery gwarantują kolejność tylko w obrębie partycji (Kafka) lub kolejki z jednym konsumentem. Dlatego zdarzenia wysyła się z <a id="term-partition-key"></a>[kluczem partycji](00%20Glossary%20CQRS.md#partition-key) równym ID agregatu. Wszystkie zdarzenia jednego zgłoszenia trafiają do jednej partycji i są przetwarzane po kolei, a zdarzenia różnych zgłoszeń mogą być przetwarzane równolegle.

```text
partycja 0:  T-17 Opened → T-17 Assigned → T-17 Resolved
partycja 1:  T-42 Opened → T-42 Assigned
partycja 2:  T-99 Opened
```

Kolejność może się mimo to zaburzyć przy ponowieniach, zmianie liczby partycji albo gdy zdarzenia jednego agregatu przechodzą przez różne tematy. Dlatego odporna projekcja nie polega wyłącznie na brokerze, tylko sprawdza wersję agregatu w zdarzeniu. Rozdział 04 pokazuje warunek `WHERE version < :v`.

Kolejność nie ma znaczenia dla zdarzeń niezależnych od siebie: liczników, statystyk, powiadomień. Takie projekcje można przetwarzać dowolnie równolegle.

## Zdarzenia z logu bazy

Zamiast pisać relay samodzielnie, można użyć <a id="term-cdc"></a>[Change Data Capture](00%20Glossary%20CQRS.md#cdc) (CDC). Narzędzie takie jak Debezium czyta log transakcji bazy (WAL w PostgreSQL, binlog w MySQL) i publikuje zmiany na Kafkę. Debezium ma gotowy tryb outbox (Outbox Event Router), który zamienia wiersze tabeli `outbox` na wiadomości z właściwym tematem i kluczem.

| | Relay w aplikacji | CDC (Debezium) |
|---|---|---|
| Opóźnienie | interwał odpytywania | niemal natychmiast po commicie |
| Obciążenie bazy | zapytania `SELECT ... FOR UPDATE` | czytanie logu, bez zapytań |
| Kolejność | według `id` w outboxie | według kolejności w logu transakcji |
| Operacje | zwykły proces aplikacji | Kafka Connect, slot replikacji, monitoring |
| Ryzyko | prosty kod, łatwy do debugowania | zapomniany slot replikacji zapełnia dysk bazy |

CDC na surowych tabelach, bez outboxa, publikuje zmiany wierszy, a nie zdarzenia domenowe. Odbiorcy widzą wtedy `UPDATE tickets SET status='resolved'` zamiast `TicketResolved` i zależą od schematu tabel. Dlatego CDC łączy się z outboxem: aplikacja decyduje o treści zdarzenia, a CDC zajmuje się niezawodnym transportem.

## Kontrakt zdarzeń

Zdarzenie opublikowane na zewnątrz staje się kontraktem, tak jak publiczne API. Inne zespoły budują na nim projekcje i procesy. Zmiana nazwy pola psuje ich kod.

Zasady projektowania kontraktu:

- rozdziel zdarzenia wewnętrzne (dla własnych projekcji) od integracyjnych (dla innych zespołów), bo te drugie zmieniają się rzadziej i z większą ostrożnością,
- zdarzenie integracyjne zawiera dane potrzebne odbiorcom, a nie cały stan agregatu,
- każde zdarzenie ma metadane: `event_id`, `event_type`, `schema_version`, `occurred_at`, `aggregate_id`, `correlation_id`,
- zmiany są zgodne wstecz: dodawanie pól opcjonalnych jest bezpieczne, a usuwanie lub zmiana znaczenia pola wymaga nowej wersji zdarzenia.

<a id="term-schema-registry"></a>[Schema registry](00%20Glossary%20CQRS.md#schema-registry), na przykład Confluent Schema Registry albo Apicurio, przechowuje schematy zdarzeń (Avro, Protobuf, JSON Schema) i odrzuca publikację zdarzenia, którego schemat łamie ustaloną zgodność.

```json
{
  "event_id": "5f0c1a7e-8c1b-4b8e-9d0a-2f7e5f3c9a11",
  "event_type": "TicketResolved",
  "schema_version": 2,
  "occurred_at": "2026-09-24T10:15:00Z",
  "aggregate_id": "b7e4c2d0-1a2b-4c3d-8e9f-0a1b2c3d4e5f",
  "correlation_id": "req-8812",
  "data": {
    "resolution": "replaced",
    "resolved_by": "agent-7",
    "customer_id": "c-311"
  }
}
```

| Zmiana | Zgodna wstecz | Postępowanie |
|---|---|---|
| nowe pole opcjonalne | tak | publikuj od razu |
| nowe pole wymagane | nie | wartość domyślna albo nowa wersja |
| zmiana nazwy pola | nie | nowa wersja, przez okres przejściowy publikuj obie |
| zmiana znaczenia pola | nie | nowe pole albo nowe zdarzenie |
| usunięcie pola | nie | najpierw upewnij się, że nikt go nie czyta |

## Co zapamiętać

- Zapis do bazy i publikacja na brokerze bez wspólnej transakcji to dual write, który zawsze grozi niespójnością.
- Transactional outbox zapisuje zdarzenia w transakcji zapisu, a relay publikuje je co najmniej raz.
- Inbox u odbiorcy deduplikuje wiadomości w transakcji ze skutkiem przetworzenia.
- Exactly-once w ogólnym przypadku nie istnieje. Zakładaj at-least-once i buduj odbiorców idempotentnych.
- Klucz partycji równy ID agregatu zachowuje kolejność w obrębie agregatu. Wersja w zdarzeniu chroni przed resztą przypadków.
- CDC z outboxem daje niskie opóźnienie i niezawodny transport, ale wymaga utrzymania Kafka Connect i slotów replikacji.
- Zdarzenia integracyjne są kontraktem: metadane, zgodność wstecz, schema registry.

## Pytania sprawdzające

### 28. Dlaczego zapis do bazy i publikacja zdarzenia w dwóch krokach to problem (dual write)? Jak rozwiązuje go transactional outbox?

<details>
<summary>Odpowiedź</summary>

Baza i broker nie mają wspólnej transakcji, a proces może paść w dowolnym momencie. Commit bez publikacji oznacza zmianę bez zdarzenia, a publikacja bez commitu oznacza zdarzenie o nieistniejącej zmianie. Retry tego nie naprawia. Outbox zapisuje zdarzenia w tabeli w tej samej transakcji co zmianę, a osobny relay (lub CDC) czyta je i publikuje, oznaczając wysłane. Zdarzenie zostaje wysłane co najmniej raz.

Zobacz: sekcja „Dwa zapisy bez wspólnej transakcji”.

</details>

### 29. Czym jest wzorzec inbox i jak razem z outboxem daje efektywnie jednokrotne przetwarzanie?

<details>
<summary>Odpowiedź</summary>

Inbox to tabela u odbiorcy z ID przetworzonych wiadomości, uzupełniana w tej samej transakcji co skutek przetworzenia (`INSERT ... ON CONFLICT DO NOTHING`). Powtórzona wiadomość jest pomijana. Outbox gwarantuje, że wiadomość zostanie wysłana co najmniej raz, a inbox, że jej skutek zostanie zapisany raz. Razem dają effectively-once dla zmian w bazie odbiorcy. Stare wpisy usuwa się po okresie dłuższym niż maksymalne opóźnienie ponownego dostarczenia.

Zobacz: sekcja „Deduplikacja u odbiorcy”.

</details>

### 30. Co oznacza dostarczenie at-least-once i dlaczego exactly-once w praktyce jest iluzją?

<details>
<summary>Odpowiedź</summary>

At-least-once: wiadomość dotrze co najmniej raz, więc możliwe są duplikaty. Exactly-once jest iluzją, bo odbiorca może wykonać efekt uboczny (zapis do bazy, e-mail, płatność) i paść przed potwierdzeniem, a broker nie ma jak tego wykryć. Transakcje Kafki obejmują tylko przepływ Kafka → Kafka. W praktyce zakłada się at-least-once i idempotentnych odbiorców (inbox, idempotentne projekcje, klucze idempotencji w zewnętrznych API), co daje effectively-once.

Zobacz: sekcja „Gwarancje dostarczenia”.

</details>

### 31. Jak zachować kolejność zdarzeń (partycjonowanie po ID agregatu, numery sekwencyjne) i kiedy kolejność nie ma znaczenia?

<details>
<summary>Odpowiedź</summary>

Brokery gwarantują kolejność tylko w partycji, więc zdarzenia publikuje się z kluczem partycji równym ID agregatu. Wszystkie zdarzenia jednego agregatu idą wtedy po kolei, a różne agregaty równolegle. Ponieważ kolejność może się zaburzyć przy ponowieniach, zmianie liczby partycji lub wielu tematach, projekcja sprawdza dodatkowo wersję agregatu w zdarzeniu. Kolejność nie ma znaczenia dla zdarzeń niezależnych: liczników, statystyk, powiadomień.

Zobacz: sekcja „Kolejność zdarzeń”.

</details>

### 32. Czym jest Change Data Capture (np. Debezium) i kiedy jest lepszy od outboxa w kodzie aplikacji?

<details>
<summary>Odpowiedź</summary>

CDC czyta log transakcji bazy (WAL, binlog) i publikuje zmiany na brokera. Nie zastępuje outboxa, tylko relay. Debezium z Outbox Event Router publikuje wiersze outboxa jako zdarzenia. Jest lepszy przy wymaganiu niskiego opóźnienia, dużym ruchu i gdy odpytywanie outboxa obciąża bazę. Kosztem jest utrzymanie Kafka Connect i slotów replikacji, bo zapomniany slot zapełnia dysk. CDC na surowych tabelach publikuje zmiany wierszy zamiast zdarzeń domenowych, co wiąże odbiorców ze schematem.

Zobacz: sekcja „Zdarzenia z logu bazy”.

</details>

### 33. Jak projektować kontrakt zdarzeń między zespołami (wersjonowanie schematu, zgodność wstecz, schema registry)?

<details>
<summary>Odpowiedź</summary>

Należy oddzielić zdarzenia wewnętrzne od integracyjnych, a w integracyjnych umieszczać tylko dane potrzebne odbiorcom. Każde zdarzenie dostaje metadane (`event_id`, `event_type`, `schema_version`, `occurred_at`, `aggregate_id`, `correlation_id`). Zmiany muszą być zgodne wstecz: nowe pola opcjonalne są bezpieczne, a zmiana nazwy lub znaczenia oraz usunięcie pola wymagają nowej wersji i okresu przejściowego. Schema registry (Confluent, Apicurio) przechowuje schematy i blokuje publikację niezgodnych.

Zobacz: sekcja „Kontrakt zdarzeń”.

</details>
