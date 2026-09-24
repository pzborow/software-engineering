# Strona zapisu

Strona zapisu przyjmuje intencje użytkownika, sprawdza, czy są dozwolone, i zmienia stan systemu. Jest mała, ale to w niej leżą wszystkie reguły biznesowe. Ten rozdział pokazuje, jak projektować komendy i handlery, co zwracać po zapisie oraz jak obsłużyć ponowienia i współbieżność.

```text
HTTP / kolejka ──► komenda ──► handler ──► agregat (reguły) ──► repozytorium ──► baza
                                                  │
                                                  └──► zdarzenia (dla strony odczytu)
```

## Prośba i fakt

<a id="term-command"></a>[Komenda](00%20Glossary%20CQRS.md#command) to prośba o wykonanie operacji, wyrażona w trybie rozkazującym: `OpenTicket`, `AssignTicket`, `ResolveTicket`. Ma jednego adresata i może zostać odrzucona.

<a id="term-domain-event"></a>[Zdarzenie domenowe](00%20Glossary%20CQRS.md#domain-event) to fakt, który już się wydarzył, wyrażony w czasie przeszłym: `TicketOpened`, `TicketAssigned`, `TicketResolved`. Może mieć wielu odbiorców i nie da się go odrzucić, bo przeszłości nie można zmienić.

```python
# commands.py
from dataclasses import dataclass


@dataclass(frozen=True)
class OpenTicket:
    ticket_id: str
    customer_id: str
    title: str
    priority: str


@dataclass(frozen=True)
class AssignTicket:
    ticket_id: str
    agent_id: str
    expected_version: int


# events.py
@dataclass(frozen=True)
class TicketOpened:
    ticket_id: str
    customer_id: str
    title: str
    priority: str
    opened_at: datetime


@dataclass(frozen=True)
class TicketAssigned:
    ticket_id: str
    agent_id: str
    assigned_at: datetime
```

| | Komenda | Zdarzenie |
|---|---|---|
| Czas | przyszły, rozkaz | przeszły, fakt |
| Odbiorcy | dokładnie jeden handler | zero lub wielu subskrybentów |
| Może być odrzucona | tak | nie |
| Kto tworzy | klient (UI, API, inny system) | model zapisu po udanej zmianie |

Nazwa komendy powinna wyrażać intencję biznesową, a nie operację na danych. `UpdateTicket(status="resolved")` ukrywa, co się stało, i zmusza handler do zgadywania. `ResolveTicket(resolution="replaced")` mówi dokładnie, czego chce użytkownik, więc handler wie, które reguły sprawdzić, a zdarzenie `TicketResolved` jest czytelne dla wszystkich odbiorców. Takie podejście nazywa się <a id="term-task-based-ui"></a>[task-based UI](00%20Glossary%20CQRS.md#task-based-ui): interfejs oferuje akcje („Rozwiąż”, „Przekaż”, „Eskaluj”), a nie formularz edycji wszystkich pól.

## Obsługa komendy krok po kroku

<a id="term-command-handler"></a>[Handler komendy](00%20Glossary%20CQRS.md#command-handler) obsługuje jedną komendę. Jego przebieg jest prawie zawsze taki sam:

1. załaduj agregat z repozytorium,
2. wywołaj na nim metodę, która sprawdzi reguły i zmieni stan,
3. zapisz agregat razem z wygenerowanymi zdarzeniami,
4. zakończ transakcję.

Reguły decydujące o tym, czy operacja jest dozwolona, należą do <a id="term-aggregate"></a>[agregatu](00%20Glossary%20CQRS.md#aggregate), czyli grupy obiektów pilnowanej przez jeden korzeń, zapisywanej w jednej transakcji:

```python
# domain/ticket.py
class TicketError(Exception):
    pass


@dataclass
class Ticket:
    id: str
    customer_id: str
    title: str
    priority: str
    status: str = "open"
    assignee_id: str | None = None
    version: int = 0
    events: list = field(default_factory=list)

    @classmethod
    def open(cls, cmd: OpenTicket, now: datetime) -> "Ticket":
        if cmd.priority not in ("low", "normal", "high", "critical"):
            raise TicketError(f"Nieznany priorytet {cmd.priority}")
        ticket = cls(cmd.ticket_id, cmd.customer_id, cmd.title, cmd.priority)
        ticket.events.append(TicketOpened(cmd.ticket_id, cmd.customer_id, cmd.title, cmd.priority, now))
        return ticket

    def assign(self, agent_id: str, now: datetime) -> None:
        if self.status != "open":
            raise TicketError("Można przypisać tylko otwarte zgłoszenie")
        if self.assignee_id == agent_id:
            return                                    # nic się nie zmienia, brak zdarzenia
        self.assignee_id = agent_id
        self.events.append(TicketAssigned(self.id, agent_id, now))
```

```python
# application/assign_ticket.py
class AssignTicketHandler:
    def __init__(self, uow: UnitOfWork, clock: Clock):
        self._uow = uow
        self._clock = clock

    def __call__(self, cmd: AssignTicket) -> int:
        with self._uow as uow:
            ticket = uow.tickets.get(cmd.ticket_id)
            ticket.assign(cmd.agent_id, self._clock.now())
            uow.tickets.save(ticket, expected_version=cmd.expected_version)
            uow.commit()
        return ticket.version                     # metadane zapisu, patrz „Co zwraca komenda”
```

Handler nie zawiera reguł biznesowych, nie buduje odpowiedzi HTTP, nie aktualizuje read modeli ręcznie i nie wysyła e-maili. Read modele i powiadomienia reagują na zdarzenia, co opisują rozdziały 04 i 06. Handler, który robi coś więcej niż cztery kroki powyżej, zwykle przejął cudzą odpowiedzialność.

## Co zwraca komenda

W czystym CQRS komenda nic nie zwraca: kod, który chce wiedzieć, co się stało, wysyła zapytanie. W praktyce API potrzebuje odpowiedzi. Przyjęte kompromisy:

| Zwraca | Kiedy | Czy łamie CQRS |
|---|---|---|
| nic (`202 Accepted`) | komenda przetwarzana asynchronicznie | nie |
| ID nowego zasobu | tworzenie, gdy ID nadaje serwer | praktycznie nie, ID nie jest odczytem stanu |
| nową wersję agregatu | klient chce odczytać własny zapis lub wysłać kolejną komendę | nie, to metadane zapisu |
| wynik obliczenia | np. naliczona kwota zwrotu | granica, akceptowalne, jeśli wynik powstał przy zmianie |
| pełny stan obiektu | wygoda frontendu | tak, strona zapisu staje się stroną odczytu |

Dobrym wzorcem jest nadawanie ID przez klienta (UUID w komendzie `OpenTicket`). Komenda wtedy nie musi nic zwracać, a klient zna ID zasobu przed wysłaniem. Zwracanie wersji przydaje się przy spójności odczytu, opisanej w rozdziale 05.

```python
@router.post("/tickets/{ticket_id}/assignment", status_code=200)
def assign(ticket_id: str, body: AssignBody, handler=Depends(get_assign_handler)):
    version = handler(AssignTicket(ticket_id, body.agent_id, body.expected_version))
    return {"version": version}                   # metadane zapisu, a nie stan zgłoszenia
```

## Walidacja na trzech poziomach

Komenda może zostać odrzucona na trzech etapach:

- format: czy pola istnieją i mają poprawny typ, co sprawdza API (Pydantic) jeszcze przed utworzeniem komendy,
- reguły aplikacji: czy agent istnieje, czy użytkownik ma uprawnienia, co sprawdza handler, zwykle przez inne repozytoria lub usługi,
- niezmienniki: czy zgłoszenie jest otwarte, czy priorytet jest dozwolony, co sprawdza agregat.

Odrzucenie jest wyjątkiem albo wynikiem typu „błąd”, który API zamienia na `400`, `403`, `404` lub `409`. Odrzucona komenda nie zmienia stanu i nie generuje zdarzeń. To ważne: po stronie odczytu nie ma czego cofać.

Część walidacji wymaga danych z read modelu, na przykład „czy agent nie ma więcej niż 20 otwartych zgłoszeń”. Read model może być nieaktualny. Jeśli reguła jest krytyczna, musi opierać się na danych zapisu, np. na liczniku w agregacie `Agent`. Jeśli jest miękka, może użyć read modelu z tolerancją na drobne przekroczenia.

## Ponowione komendy

Sieć zawodzi. Klient wysyła `OpenTicket`, serwer ją wykonuje, ale odpowiedź się gubi. Klient ponawia żądanie. Bez zabezpieczenia powstają dwa zgłoszenia.

Rozwiązaniem jest <a id="term-idempotency"></a>[idempotencja](00%20Glossary%20CQRS.md#idempotency), czyli sytuacja, w której wielokrotne wykonanie komendy daje ten sam efekt co jednokrotne. Są trzy sposoby:

- naturalna idempotencja: ID nadaje klient, a drugi `OpenTicket` z tym samym ID trafia na istniejący rekord i zostaje zignorowany albo zwraca ten sam wynik,
- idempotentna operacja: `assign(agent_id)` na zgłoszeniu już przypisanym temu agentowi nic nie zmienia, co widać w kodzie agregatu,
- <a id="term-idempotency-key"></a>[klucz idempotencji](00%20Glossary%20CQRS.md#idempotency-key): klient wysyła nagłówek `Idempotency-Key`, a serwer zapamiętuje wynik pierwszego wykonania i zwraca go przy powtórce.

```python
class IdempotentHandler:
    def __init__(self, inner, store: IdempotencyStore):
        self._inner = inner
        self._store = store

    def __call__(self, cmd, key: str):
        with self._store.lock(key):
            if (saved := self._store.get(key)) is not None:
                return saved                       # powtórka: ten sam wynik, bez ponownego wykonania
            result = self._inner(cmd)
            self._store.put(key, result, ttl=timedelta(hours=24))
            return result
```

Zapis wyniku do `IdempotencyStore` powinien odbywać się w tej samej transakcji co zmiana agregatu. Inaczej awaria między nimi zostawi komendę wykonaną, ale niezapamiętaną.

## Dwie zmiany naraz

Dwóch agentów otwiera to samo zgłoszenie. Obaj widzą je jako nieprzypisane i obaj klikają „Przejmij”. Bez kontroli wygrywa ten, kto zapisze później, a pierwszy agent nie wie, że jego zmiana zniknęła.

<a id="term-optimistic-concurrency"></a>[Optymistyczna kontrola współbieżności](00%20Glossary%20CQRS.md#optimistic-concurrency) rozwiązuje to przez wersję agregatu. Klient wysyła wersję, którą widział. Zapis powiedzie się tylko wtedy, gdy wersja w bazie nadal jest taka sama:

```python
class SqlTicketRepository:
    def save(self, ticket: Ticket, expected_version: int) -> None:
        result = self._session.execute(
            update(TicketRow)
            .where(TicketRow.id == ticket.id, TicketRow.version == expected_version)
            .values(assignee_id=ticket.assignee_id, status=ticket.status, version=expected_version + 1)
        )
        if result.rowcount == 0:
            raise ConcurrencyConflict(ticket.id, expected_version)
        ticket.version = expected_version + 1
```

W HTTP wersja zwykle podróżuje jako `ETag` w odpowiedzi i `If-Match` w żądaniu, a konflikt kończy się statusem `409 Conflict` albo `412 Precondition Failed`. Klient pokazuje wtedy komunikat „Zgłoszenie zostało zmienione przez kogoś innego” i odświeża dane.

Nazwa „optymistyczna” oznacza, że system zakłada rzadkie konflikty i nie blokuje rekordu na czas edycji. Blokada pesymistyczna (`SELECT ... FOR UPDATE`) ma sens przy krótkich operacjach z częstymi konfliktami, na przykład przy liczniku miejsc.

## Co zapamiętać

- Komenda to prośba w trybie rozkazującym z jednym adresatem, zdarzenie to fakt w czasie przeszłym z wieloma odbiorcami.
- Nazwa komendy wyraża intencję biznesową, a nie aktualizację pól.
- Handler ładuje agregat, wywołuje regułę, zapisuje i kończy transakcję. Reguły są w agregacie.
- Komenda może zwrócić ID lub wersję, ale nie powinna zwracać pełnego stanu.
- Walidacja ma trzy poziomy, a odrzucona komenda nie generuje zdarzeń.
- Ponowienia obsługuje się naturalną idempotencją albo kluczem idempotencji zapisanym w tej samej transakcji.
- Współbieżne zmiany wykrywa optymistyczna kontrola wersji, w HTTP przez `ETag` i `If-Match`.

## Pytania sprawdzające

### 6. Czym jest komenda i czym różni się od zdarzenia? Jak nazywać komendy i dlaczego nazwa ma znaczenie?

<details>
<summary>Odpowiedź</summary>

Komenda to prośba o operację w trybie rozkazującym (`ResolveTicket`), z jednym adresatem, która może zostać odrzucona. Zdarzenie to fakt w czasie przeszłym (`TicketResolved`), może mieć wielu odbiorców i nie da się go odrzucić. Komendy nazywa się intencją biznesową, a nie operacją CRUD. `ResolveTicket` mówi handlerowi, jakie reguły sprawdzić, i daje czytelne zdarzenie, a `UpdateTicket(status=...)` ukrywa intencję.

Zobacz: sekcja „Prośba i fakt”.

</details>

### 7. Co powinien zawierać handler komendy, a czego nie? Jak wygląda jego typowy przebieg?

<details>
<summary>Odpowiedź</summary>

Przebieg: załaduj agregat, wywołaj metodę z regułami, zapisz agregat ze zdarzeniami, zakończ transakcję. Handler nie powinien zawierać reguł biznesowych (należą do agregatu), budować odpowiedzi HTTP, ręcznie aktualizować read modeli ani wysyłać powiadomień, bo te reagują na zdarzenia. Handler robiący więcej przejął cudzą odpowiedzialność.

Zobacz: sekcja „Obsługa komendy krok po kroku”.

</details>

### 8. Co może zwrócić komenda: nic, ID, wersję, wynik? Jak pogodzić czysty CQRS z potrzebami API?

<details>
<summary>Odpowiedź</summary>

Czysty CQRS: nic, a stan odczytuje się zapytaniem. W praktyce akceptowalne jest zwracanie ID nowego zasobu, nowej wersji agregatu albo wyniku obliczenia powstałego przy zmianie, bo to metadane zapisu, a nie odczyt stanu. Pełny stan obiektu łamie podział. Dobry wzorzec to ID nadawane przez klienta, dzięki czemu komenda nic nie musi zwracać, oraz zwracanie wersji do spójności odczytu.

Zobacz: sekcja „Co zwraca komenda”.

</details>

### 9. Gdzie odbywa się walidacja komendy (format, reguły aplikacji, niezmienniki agregatu) i jak odrzucać komendy?

<details>
<summary>Odpowiedź</summary>

Format sprawdza API przed utworzeniem komendy, reguły aplikacji (uprawnienia, istnienie agenta) sprawdza handler, a niezmienniki sprawdza agregat. Odrzucenie to wyjątek albo wynik-błąd mapowany na 400, 403, 404 lub 409. Odrzucona komenda nie zmienia stanu i nie generuje zdarzeń. Reguły krytyczne nie mogą opierać się na read modelu, bo może być nieaktualny, a miękkie mogą.

Zobacz: sekcja „Walidacja na trzech poziomach”.

</details>

### 10. Jak zapewnić idempotencję komend przy ponowieniach (klucz idempotencji, deduplikacja, naturalna idempotencja)?

<details>
<summary>Odpowiedź</summary>

Naturalna idempotencja: ID nadaje klient, więc powtórzony `OpenTicket` trafia na istniejący rekord. Idempotentne operacje: przypisanie do tego samego agenta nic nie zmienia. Klucz idempotencji: klient wysyła `Idempotency-Key`, a serwer zapamiętuje wynik pierwszego wykonania i zwraca go przy powtórce. Zapis klucza musi być w tej samej transakcji co zmiana, inaczej awaria zostawi komendę wykonaną, ale niezapamiętaną.

Zobacz: sekcja „Ponowione komendy”.

</details>

### 11. Jak obsłużyć współbieżne modyfikacje tego samego agregatu (optimistic concurrency, wersja, `If-Match`)?

<details>
<summary>Odpowiedź</summary>

Optymistyczną kontrolą współbieżności: agregat ma wersję, klient wysyła wersję, którą widział, a zapis (`UPDATE ... WHERE version = :expected`) udaje się tylko, jeśli wersja się nie zmieniła. W przeciwnym razie powstaje konflikt, zwracany jako 409 lub 412. W HTTP wersja podróżuje jako `ETag` i `If-Match`. Blokada pesymistyczna ma sens przy krótkich operacjach z częstymi konfliktami.

Zobacz: sekcja „Dwie zmiany naraz”.

</details>
