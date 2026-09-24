# Zdarzenia jako źródło prawdy

Dotąd strona zapisu przechowywała bieżący stan zgłoszenia w tabeli `tickets`, a zdarzenia były produktem ubocznym zapisu. Można to odwrócić: przechowywać tylko zdarzenia, a stan wyliczać z nich na żądanie. To podejście często pojawia się razem z CQRS, ale jest osobną decyzją z własnymi kosztami.

```text
Zapis stanu:                         Zapis zdarzeń:

tickets                              stream ticket-42
id | status   | assignee | ver       1  TicketOpened     {title, priority}
42 | resolved | agent-7  | 4         2  TicketAssigned   {agent-3}
                                     3  TicketAssigned   {agent-7}
                                     4  TicketResolved   {replaced}
```

## Stan wyliczany ze zdarzeń

<a id="term-event-sourcing"></a>[Event sourcing](00%20Glossary%20CQRS.md#event-sourcing) to sposób przechowywania stanu, w którym źródłem prawdy jest niezmienna, uporządkowana lista zdarzeń. Bieżący stan agregatu nie jest nigdzie zapisany. Przy każdej komendzie agregat odtwarza się, stosując po kolei jego zdarzenia:

```python
@dataclass
class Ticket:
    id: str = ""
    status: str = "new"
    assignee_id: str | None = None
    version: int = 0
    pending: list = field(default_factory=list)

    @classmethod
    def from_history(cls, events: list) -> "Ticket":
        ticket = cls()
        for e in events:
            ticket._apply(e)
            ticket.version += 1
        return ticket

    def assign(self, agent_id: str, now: datetime) -> None:
        if self.status != "open":
            raise TicketError("Można przypisać tylko otwarte zgłoszenie")
        self._record(TicketAssigned(self.id, agent_id, now))

    def _record(self, event) -> None:
        self._apply(event)
        self.pending.append(event)

    def _apply(self, event) -> None:              # tylko zmiana stanu, bez reguł
        match event:
            case TicketOpened():
                self.id, self.status = event.ticket_id, "open"
            case TicketAssigned():
                self.assignee_id = event.agent_id
            case TicketResolved():
                self.status = "resolved"
```

Metoda `assign` sprawdza reguły i tworzy zdarzenie. Metoda `_apply` tylko zmienia stan i nie może rzucić wyjątku, bo służy też do odtwarzania historii, a historii nie wolno odrzucić.

Event sourcing naturalnie łączy się z CQRS z dwóch powodów. Stan wyliczany ze zdarzeń nie nadaje się do zapytań typu „wszystkie otwarte zgłoszenia agenta 7”, więc modele odczytu są konieczne. Zdarzenia są już zapisane w kolejności, więc projekcje mogą je czytać bezpośrednio, bez outboxa. CQRS nie wymaga jednak event sourcingu. Rozdziały 01–06 pokazują CQRS z klasycznym zapisem stanu.

## Magazyn zdarzeń

<a id="term-event-store"></a>[Event store](00%20Glossary%20CQRS.md#event-store) to baza zoptymalizowana pod dopisywanie i odczyt zdarzeń. Zdarzenia są pogrupowane w <a id="term-event-stream"></a>[strumienie](00%20Glossary%20CQRS.md#event-stream), zwykle jeden strumień na agregat (`ticket-42`). Przykłady to EventStoreDB (dziś Kurrent), Marten na PostgreSQL, Axon Server, a także zwykła tabela w PostgreSQL:

```sql
CREATE TABLE events (
    global_position bigserial PRIMARY KEY,         -- kolejność globalna, dla projekcji
    stream_id       text NOT NULL,
    stream_version  int NOT NULL,                  -- kolejność w strumieniu
    event_type      text NOT NULL,
    schema_version  int NOT NULL,
    payload         jsonb NOT NULL,
    metadata        jsonb NOT NULL,
    recorded_at     timestamptz NOT NULL DEFAULT now(),
    UNIQUE (stream_id, stream_version)             -- podstawa kontroli współbieżności
);
```

Dopisanie zdarzeń odbywa się z <a id="term-expected-version"></a>[oczekiwaną wersją](00%20Glossary%20CQRS.md#expected-version). Jeśli ktoś w międzyczasie dopisał zdarzenie do strumienia, ograniczenie `UNIQUE` odrzuci zapis. To ta sama optymistyczna kontrola współbieżności co w rozdziale 02, tylko wbudowana w magazyn:

```python
class PostgresEventStore:
    def append(self, stream_id: str, expected_version: int, events: list) -> None:
        try:
            for i, e in enumerate(events, start=1):
                self._db.execute(text("""
                    INSERT INTO events (stream_id, stream_version, event_type, schema_version, payload, metadata)
                    VALUES (:s, :v, :t, :sv, :p, :m)
                """), {"s": stream_id, "v": expected_version + i, "t": type(e).__name__,
                       "sv": SCHEMA_VERSION[type(e)], "p": serialize(e), "m": current_metadata()})
        except UniqueViolation:
            raise ConcurrencyConflict(stream_id, expected_version)

    def read(self, stream_id: str, from_version: int = 0) -> list:
        rows = self._db.execute(text("""
            SELECT event_type, schema_version, payload FROM events
            WHERE stream_id = :s AND stream_version > :v ORDER BY stream_version
        """), {"s": stream_id, "v": from_version})
        return [deserialize(r) for r in rows]
```

Projekcje korzystają z subskrypcji: czytają wszystkie zdarzenia według `global_position` od swojego checkpointu i dostają nowe, gdy się pojawią. Subskrypcja zaczynająca od zera to replay z rozdziału 04.

Pozycja globalna oparta na `bigserial` ma ten sam problem co outbox: przy równoległych transakcjach numery mogą być zatwierdzane poza kolejnością. Dedykowane event store'y rozwiązują to wewnętrznie. Przy własnej implementacji na PostgreSQL trzeba to obsłużyć, na przykład serializując zapisy globalnej pozycji albo czytając tylko do pozycji, poniżej której nie ma już otwartych transakcji.

## Długie strumienie

Zgłoszenie ma kilka lub kilkanaście zdarzeń, więc odtwarzanie jest tanie. Konto bankowe po dziesięciu latach może mieć ich dziesiątki tysięcy. Wtedy stosuje się <a id="term-snapshot"></a>[snapshot](00%20Glossary%20CQRS.md#snapshot): zapisany stan agregatu z określonej wersji. Odtwarzanie zaczyna się od snapshotu i stosuje tylko późniejsze zdarzenia.

```python
def load(self, ticket_id: str) -> Ticket:
    snap = self._snapshots.latest(f"ticket-{ticket_id}")          # np. stan z wersji 5000
    ticket = Ticket.from_snapshot(snap) if snap else Ticket()
    for e in self._store.read(f"ticket-{ticket_id}", from_version=ticket.version):
        ticket._apply(e)
        ticket.version += 1
    return ticket
```

Snapshoty to optymalizacja, a nie źródło prawdy. Można je w każdej chwili usunąć i wygenerować ponownie. Warto je dodać dopiero wtedy, gdy pomiar pokaże, że ładowanie agregatu jest wolne. Zwykle dotyczy to strumieni liczących setki lub tysiące zdarzeń. Długi strumień bywa też sygnałem, że granice agregatu są źle wyznaczone. Konto może mieć strumień per okres rozliczeniowy zamiast jednego na całe życie.

## Stare zdarzenia, nowy kod

Zdarzeń zapisanych w event storze nie wolno zmieniać, bo są historią. Kod jednak się zmienia: `TicketResolved` w wersji 1 miało pole `note`, a w wersji 2 ma `resolution` i `resolved_by`.

<a id="term-upcasting"></a>[Upcasting](00%20Glossary%20CQRS.md#upcasting) polega na przekształcaniu starej wersji zdarzenia do nowej w momencie odczytu. Stare dane zostają nietknięte, a kod domeny widzi tylko najnowszą wersję:

```python
UPCASTERS = {
    ("TicketResolved", 1): lambda p: {
        **p,
        "resolution": "other",                   # wartość domyślna dla starych zdarzeń
        "resolved_by": p.get("agent_id", "unknown"),
        "schema_version": 2,
    },
}


def deserialize(row) -> object:
    payload, version = row.payload, row.schema_version
    while (row.event_type, version) in UPCASTERS:
        payload = UPCASTERS[(row.event_type, version)](payload)
        version = payload["schema_version"]
    return EVENT_TYPES[row.event_type](**payload)
```

Strategie zmian schematu zdarzeń:

| Strategia | Jak | Kiedy |
|---|---|---|
| zmiana zgodna wstecz | nowe pole opcjonalne z wartością domyślną | proste rozszerzenia |
| upcasting | transformacja przy odczycie | zmiana nazw i struktury pól |
| nowy typ zdarzenia | `TicketResolvedV2` obok starego | zmiana znaczenia |
| kopiowanie i transformacja strumienia | nowy event store z przekształconymi zdarzeniami | duże migracje, ostateczność |

Kopiowanie strumienia narusza zasadę niezmienności historii, więc stosuje się je rzadko: przy dużych zmianach modelu, usuwaniu danych osobowych albo migracji na inny magazyn.

## Kiedy warto, a kiedy nie

Event sourcing daje:

- pełną historię zmian i audyt, bo wiadomo, kto, co i kiedy zmienił,
- możliwość zbudowania nowego modelu odczytu z danych od początku systemu,
- odtworzenie stanu z dowolnego momentu w przeszłości, co pomaga w debugowaniu i rozliczeniach,
- naturalne źródło zdarzeń dla projekcji i integracji, bez outboxa.

Koszty, o których rzadko się mówi:

- RODO i prawo do usunięcia danych: niezmiennych zdarzeń nie da się po prostu skasować. Stosuje się <a id="term-crypto-shredding"></a>[crypto-shredding](00%20Glossary%20CQRS.md#crypto-shredding), czyli szyfrowanie danych osobowych kluczem per osoba i usunięcie klucza, albo trzymanie danych osobowych poza zdarzeniami.
- Raporty ad hoc: nie da się napisać `SELECT` po bieżącym stanie. Każde nowe pytanie wymaga projekcji albo eksportu do hurtowni.
- Wersjonowanie: każda zmiana zdarzenia to upcaster, który trzeba utrzymywać bez końca.
- Onboarding: zespół musi myśleć zdarzeniami. Nowe osoby potrzebują tygodni, a nie dni.
- Narzędzia: debugowanie wymaga odtwarzania stanu, a poprawki danych robi się zdarzeniami korygującymi zamiast `UPDATE`.

| Sytuacja | Event sourcing |
|---|---|
| domena z naturalną historią: księgowość, magazyn, rezerwacje, workflow | warto rozważyć |
| audyt i odtwarzanie przeszłości jako wymaganie biznesowe | warto rozważyć |
| potrzeba wielu różnych modeli odczytu z tych samych danych | warto rozważyć |
| CRUD, katalog produktów, profil użytkownika | nie |
| zespół bez doświadczenia i napięty termin | nie |
| dużo danych osobowych, częste żądania usunięcia | ostrożnie |

Event sourcing stosuje się per agregat albo per bounded context, a nie w całym systemie. Helpdesk może trzymać zgłoszenia jako zdarzenia (historia, SLA, audyt), a profile klientów jako zwykłe tabele.

## Co zapamiętać

- Event sourcing zapisuje zdarzenia jako źródło prawdy, a stan wylicza przez ich odtworzenie.
- Metoda z regułami tworzy zdarzenie, metoda `_apply` tylko zmienia stan i nie może rzucić wyjątku.
- CQRS nie wymaga event sourcingu, ale event sourcing praktycznie wymaga modeli odczytu.
- Event store grupuje zdarzenia w strumienie per agregat, a oczekiwana wersja daje kontrolę współbieżności.
- Snapshot to optymalizacja długich strumieni, którą można w każdej chwili odtworzyć.
- Zapisanych zdarzeń się nie zmienia. Nowe wersje obsługuje upcasting przy odczycie.
- Koszty to RODO (crypto-shredding), brak raportów ad hoc, wieczne wersjonowanie i trudniejszy onboarding.

## Pytania sprawdzające

### 34. Czym jest event sourcing i dlaczego naturalnie łączy się z CQRS, choć go nie wymaga?

<details>
<summary>Odpowiedź</summary>

To przechowywanie stanu jako niezmiennej, uporządkowanej listy zdarzeń. Bieżący stan agregatu wylicza się, odtwarzając jego zdarzenia. Łączy się z CQRS, bo stan wyliczany ze zdarzeń nie nadaje się do zapytań przekrojowych, więc potrzebne są modele odczytu, a zdarzenia są gotowym, uporządkowanym źródłem dla projekcji, bez outboxa. CQRS nie wymaga event sourcingu i działa z klasycznym zapisem stanu.

Zobacz: sekcja „Stan wyliczany ze zdarzeń”.

</details>

### 35. Jak działa event store (strumień na agregat, wersja oczekiwana, subskrypcje)?

<details>
<summary>Odpowiedź</summary>

Event store przechowuje zdarzenia w strumieniach, zwykle jeden na agregat, z wersją w strumieniu i pozycją globalną. Zapis odbywa się z oczekiwaną wersją: jeśli ktoś w międzyczasie dopisał zdarzenie, zapis zostaje odrzucony (np. przez `UNIQUE (stream_id, stream_version)`). Projekcje korzystają z subskrypcji, które czytają zdarzenia według pozycji globalnej od checkpointu i dostają nowe. Własna implementacja na PostgreSQL musi uważać na zatwierdzanie pozycji globalnych poza kolejnością.

Zobacz: sekcja „Magazyn zdarzeń”.

</details>

### 36. Czym są snapshoty i kiedy są potrzebne?

<details>
<summary>Odpowiedź</summary>

Snapshot to zapisany stan agregatu z określonej wersji. Ładowanie zaczyna się od niego i stosuje tylko późniejsze zdarzenia. Jest optymalizacją, a nie źródłem prawdy, więc można go usunąć i odtworzyć. Dodaje się go, gdy pomiar pokaże wolne ładowanie, zwykle przy setkach lub tysiącach zdarzeń. Długi strumień bywa sygnałem źle wyznaczonych granic agregatu.

Zobacz: sekcja „Długie strumienie”.

</details>

### 37. Jak zmieniać schemat zdarzeń, które już są zapisane (upcasting, wersjonowanie, kopiowanie i transformacja strumienia)?

<details>
<summary>Odpowiedź</summary>

Zapisanych zdarzeń się nie zmienia. Zmiany zgodne wstecz to nowe pola opcjonalne z wartością domyślną. Upcasting przekształca starą wersję zdarzenia do nowej przy odczycie, dzięki czemu kod domeny widzi tylko najnowszą. Zmiana znaczenia to nowy typ zdarzenia. Kopiowanie i transformacja strumienia do nowego magazynu to ostateczność przy dużych migracjach lub usuwaniu danych, bo narusza niezmienność historii.

Zobacz: sekcja „Stare zdarzenia, nowy kod”.

</details>

### 38. Kiedy wybrać event sourcing, a kiedy CQRS ze zwykłym zapisem stanu? Jakie są koszty ES, o których rzadko się mówi (RODO, raporty ad hoc, onboarding zespołu)?

<details>
<summary>Odpowiedź</summary>

Event sourcing warto rozważyć w domenach z naturalną historią (księgowość, magazyn, rezerwacje, workflow), przy wymaganiu audytu i odtwarzania przeszłości oraz przy wielu modelach odczytu z tych samych danych. Nie stosuje się go do CRUD-a, katalogu czy profili, ani w zespole bez doświadczenia przy napiętym terminie. Ukryte koszty: RODO (crypto-shredding albo dane osobowe poza zdarzeniami), brak raportów ad hoc, wieczne utrzymywanie upcasterów, dłuższy onboarding, poprawki danych zdarzeniami korygującymi. Stosuje się go per agregat lub kontekst, nie w całym systemie.

Zobacz: sekcja „Kiedy warto, a kiedy nie”.

</details>
