# Transakcje, zdarzenia i asynchroniczność

Dotąd rdzeń rozmawiał z bazą wyłącznie przez porty; teraz spinamy te rozmowy w spójną całość: transakcję, zdarzenia i pracę asynchroniczną. W „Rowerku” dodamy UnitOfWork, zdarzenie RentalFinished z Outboxem, idempotentny LockEventConsumer i porty async bez async w domenie.

```text
Use case -> UnitOfWork -> repozytorium + Outbox (jedna transakcja)
                                  |
                          relay -> broker -> LockEventConsumer (idempotentny)
```

## Unit of Work jako port

[Unit of Work](00%20Glosariusz.md#unit-of-work) to obiekt, który obejmuje jeden scenariusz biznesowy i zatwierdza wszystkie jego zmiany razem albo żadnej. Jako [port](00%20Glosariusz.md#port) jest to abstrakcja rdzenia: context manager, który udostępnia [porty repozytoriów](00%20Glosariusz.md#port-repozytorium) oraz metody `commit` i `rollback`.

Po co to komuś, kto ma już repozytorium? Repozytorium modeluje kolekcję, ale nie mówi, kiedy zmiany stają się trwałe. Gdy scenariusz dotyka kilku repozytoriów, ktoś musi je spiąć w jedną granicę spójności. Ten obiekt to robi, a rdzeń nie widzi sesji ani `BEGIN`.

```python
# core/ports.py · port
class UnitOfWork(ABC):
    rentals: RentalRepository
    def __enter__(self) -> "UnitOfWork": return self
    def __exit__(self, exc_type, exc, tb) -> None: self.rollback()
    @abstractmethod
    def commit(self) -> None: ...
    @abstractmethod
    def rollback(self) -> None: ...
```

`__exit__` domyślnie cofa zmiany. Jeśli scenariusz nie wywoła `commit`, nic nie trafi do bazy, a wyjątek nadal się propaguje.

Use case przyjmuje port w konstruktorze zamiast osobnych repozytoriów:

```python
# core/use_cases.py · przypadek użycia
class StartRental:
    def __init__(self, uow: UnitOfWork) -> None: ...
    def __call__(self, user_id: str, bike_id: str) -> Rental:
        with self.uow:
            ...
            self.uow.rentals.add(rental)
            self.uow.commit()
        return rental
```

Adapter `SqlAlchemyUnitOfWork` tworzy sesję w `__enter__`, buduje na niej `SqlAlchemyRentalRepository` i mapuje `commit`/`rollback` na sesję. Fake w testach robi to samo na słownikach w pamięci. Konsekwencja: atomowość jest częścią kontraktu rdzenia, a to, czy granicę wyznacza use case, czy adapter, rozstrzygnie następna sekcja.

## Granica transakcji: use case czy adapter

Granicę transakcji wyznacza [przypadek użycia](00%20Glosariusz.md#przypadek-użycia), bo tylko on wie, co jest jednym scenariuszem biznesowym. [Adapter](00%20Glosariusz.md#adapter) wie, *jak* zatwierdzić zmiany (sesja, `COMMIT`), ale nie wie, *kiedy* scenariusz jest kompletny.

Gdyby granicę stawiał adapter, np. repozytorium robiące `commit` po każdym `add`, jeden scenariusz rozpadłby się na kilka transakcji. Awaria w połowie zostawiłaby stan, którego reguły biznesowe nie dopuszczają. Podobnie middleware HTTP z `commit` po każdym żądaniu wiąże atomowość z protokołem: ten sam scenariusz wywołany z konsumenta kolejki albo CLI nie miałby granicy.

| Miejsce granicy | Kto decyduje o `commit` | Skutek |
|---|---|---|
| Use case | scenariusz | atomowość niezależna od kanału wejścia |
| Adapter (repozytorium, middleware) | technologia | granica przypadkowa, zależna od kanału |

Podział pracy: use case otwiera `with self.uow` i woła `commit`, a adapter `SqlAlchemyUnitOfWork` tylko realizuje te wywołania na sesji.

```python
# core/use_cases.py · przypadek użycia
class FinishRental:
    def __init__(self, uow: UnitOfWork, payments: PaymentGateway) -> None: ...
    def __call__(self, rental_id: str) -> Money:
        with self.uow:
            ...  # zamknij wypożyczenie, policz opłatę
            self.payments.charge(user_id, fee)
            self.uow.commit()
        return fee
```

Odrzucona płatność (`PaymentDeclined`) przerywa blok przed `commit`, więc `__exit__` cofa zmiany. Uwaga: wywołanie bramki wewnątrz transakcji trzyma połączenie z bazą na czas żądania sieciowego, a płatności nie da się cofnąć rollbackiem. Tę lukę zamyka Outbox, omówiony w kolejnych sekcjach.

## Zdarzenia domenowe i port publikacji

[Zdarzenie domenowe](00%20Glosariusz.md#zdarzenie-domenowe) to niezmienny fakt z przeszłości, wyrażony językiem domeny, np. `RentalFinished`. Rdzeń publikuje go przez [port wyjściowy](00%20Glosariusz.md#port-wyjściowy-driven), a nie przez wywołanie konkretnej kolejki, SMS-a czy e-maila.

Zdarzenie opisuje, *co się stało*, a nie *co ma zrobić odbiorca*. Dzięki temu `FinishRental` nie zna powiadomień ani rozliczeń: zgłasza fakt, a nowy odbiorca to nowy adapter bez zmiany use case'u. Zdarzenie jest [obiektem wartości](00%20Glosariusz.md#obiekt-wartości) (`frozen=True`) i niesie dane wystarczające do reakcji bez odpytywania bazy.

Portem publikacji jest tu istniejący Unit of Work, rozszerzony o metodę `publish`. Nie wprowadzamy osobnego `EventPublisher`, bo zdarzenie ma należeć do tej samej transakcji co zmiana stanu: UoW przyjmuje je w trakcie scenariusza, a adapter decyduje, co z nim zrobić po `commit`. Zapis zdarzeń w tej samej transakcji do tabeli to [Outbox](00%20Glosariusz.md#outbox), omówiony w następnej sekcji.

```python
# core/events.py · obiekt wartości
@dataclass(frozen=True)
class RentalFinished:
    rental_id: str
    user_id: str
    fee: Money

# core/ports.py · UnitOfWork
@abstractmethod
def publish(self, event: DomainEvent) -> None: ...

# core/use_cases.py · FinishRental
with self.uow:
    ...
    self.uow.publish(RentalFinished(rental_id, user_id, fee))
    self.uow.commit()
```

Konsekwencja: zdarzenie wychodzi na zewnątrz dopiero po udanym `commit`. Przy `PaymentDeclined` blok się przerywa i nikt nie dowie się o zwrocie, który się nie odbył. W testach fake UoW zbiera zdarzenia w liście, więc asertujesz na niej bez kolejki.

## Outbox: zdarzenia w tej samej transakcji

Outbox to tabela zdarzeń do wysłania, zapisywana w tej samej transakcji co zmiana stanu. Rozwiązuje problem podwójnego zapisu: baza i kolejka nie dzielą transakcji, więc jedna operacja może się udać bez drugiej.

### Problem

Załóżmy, że adapter publikuje `RentalFinished` do kolejki po `commit`. Jeśli proces padnie między nimi, wypożyczenie jest zamknięte i opłacone, ale nikt nie dostał zdarzenia. Odwrócenie kolejności jest gorsze: zdarzenie wyszło, a `commit` się nie udał.

### Mechanizm

Adapter `UnitOfWork` w `publish` nie wysyła niczego, tylko dodaje wiersz do tabeli `outbox` w tej samej sesji. `commit` zatwierdza atomowo zmianę stanu i zdarzenie. Osobny proces, nazywany relayem, odczytuje niewysłane wiersze, publikuje je i oznacza jako wysłane.

```text
FinishRental -> uow.publish -> INSERT outbox ┐
             -> uow.commit  ─────────────────┴─> jedna transakcja
relay: SELECT niewysłane -> kolejka -> UPDATE wysłane
```

```python
# infra/sqlalchemy_uow.py · adapter
def publish(self, event: DomainEvent) -> None:
    self.session.add(OutboxRow(
        type=type(event).__name__,
        payload=serialize(event),
        sent_at=None,
    ))
```

Sygnatura portu i kod `FinishRental` się nie zmieniają: to adapter wybiera Outbox.

### Konsekwencja

Relay może paść po publikacji, a przed oznaczeniem wiersza, więc zdarzenie wyjdzie dwa razy. Dostarczanie jest więc co najmniej jednokrotne, a odbiorca musi być [idempotentnym konsumentem](00%20Glosariusz.md#idempotentny-konsument), czyli bezpiecznie przetwarzać duplikaty. Płacisz też opóźnieniem relaya i dodatkową tabelą.

## Idempotentny konsument wiadomości

Kolejka i relay z Outboxa gwarantują dostarczenie co najmniej raz, więc idempotentny konsument (taki, który przetworzenie duplikatu kończy bez skutków ubocznych) to obowiązek adaptera wejściowego. Zamek roweru może wysłać to samo zdarzenie „rower zwrócony" dwa razy, a Rowerek nie może dwa razy naliczyć opłaty.

### Mechanizm

Konsument wstawia wiersz z identyfikatorem wiadomości do tabeli `processed_messages` z unikalnym kluczem, w tej samej sesji, na której działa use case. Naruszenie unikalności oznacza duplikat: wiadomość potwierdzamy i pomijamy. Jeśli use case rzuci wyjątek, rollback usuwa też znacznik, więc ponowna próba przejdzie normalnie.

```python
# infra/lock_consumer.py · adapter
def handle(self, message: bytes) -> None:
    event = parse_lock_event(message)
    with self._session_factory() as session:
        try:
            session.add(ProcessedMessageRow(message_id=event.message_id))
            session.flush()
        except IntegrityError:
            return  # duplikat: potwierdź i pomiń
        self._build_finish_rental(session)(event.rental_id)
```

`build_finish_rental(session)` składa `SqlAlchemyUnitOfWork` na tej samej sesji, na której dodano znacznik, i od tego zależy atomowość. `FinishRental` wywołuje `uow.commit()` na tej sesji, więc zatwierdza znacznik razem ze zmianą stanu.

Sam znacznik nie wystarczy, jeśli wiadomość nie ma stabilnego identyfikatora. Wtedy use case musi być naturalnie idempotentny, np. zamknięcie już zamkniętego wypożyczenia nic nie robi.

### Konsekwencja

Deduplikacja mieszka w adapterze i jest testowana przez dwukrotne wywołanie `handle` z tą samą wiadomością. Płacisz dodatkową tabelą, którą trzeba okresowo czyścić.

## Asynchroniczność na brzegu, nie w domenie

Zostaw porty synchroniczne i przenieś asynchroniczność do adapterów. Rdzeń mówi „naliczyć opłatę", a to, czy adapter zrobi to przez `await`, wątek czy kolejkę, jest szczegółem technologii.

### Trzy strategie

| Sytuacja | Rozwiązanie | Async w rdzeniu |
|---|---|---|
| Wejście async (np. serwer async) | adapter wywołuje synchroniczny przypadek użycia w wątku roboczym | nie |
| Port wyjściowy z klientem async | adapter mostkuje korutynę do wywołania blokującego | nie |
| Wolna operacja, której wynik nie jest potrzebny od razu (SMS) | zdarzenie z Outboxa, dostarczane asynchronicznie | nie |

Trzecia strategia usuwa async ze scenariusza tam, gdzie się da. `FinishRental` nadal synchronicznie pobiera opłatę przez `PaymentGateway`, bo potrzebuje jej wyniku. Dodatkowo zgłasza `RentalFinished` przez `uow.publish`, a z tego zdarzenia wynika SMS, który relay dostarcza asynchronicznie.

### Most w adapterze

Gdy bramka płatności ma tylko klienta async, adapter spełnia synchroniczny `PaymentGateway` i sam zarządza pętlą zdarzeń.

```python
# infra/async_payment_gateway.py · adapter
class AsyncStripePaymentGateway:
    def __init__(self, client, loop: asyncio.AbstractEventLoop) -> None:
        self._client, self._loop = client, loop

    def charge(self, user_id: str, amount: Money) -> None:
        future = asyncio.run_coroutine_threadsafe(
            self._client.charge(user_id, amount.amount, amount.currency),
            self._loop,
        )
        future.result(timeout=10)  # blokuje wątek use case'u, nie pętlę
```

### Konsekwencja

Use case musi działać w wątku roboczym, nigdy w wątku pętli, inaczej `future.result()` zablokuje ją na zawsze. W FastAPI zapewnia to adapter wejściowy: endpoint w `rentals_router` jest zwykłym `def`, więc Starlette uruchamia go w puli wątków. Composition root nie wybiera wątku, tylko składa zależności. Dla `LockEventConsumer` wątek zapewnia sam konsument. Płacisz blokowanym wątkiem na czas wywołania.

## Co zapamiętać

- Unit of Work jako port to context manager z repozytoriami, commit i rollback, który czyni atomowość scenariusza częścią kontraktu rdzenia.
- Use case decyduje, kiedy scenariusz jest kompletny i wywołuje commit; adapter tylko wykonuje commit i rollback na sesji.
- Zdarzenie domenowe to niezmienny fakt z przeszłości, który use case zgłasza przez port (tu UnitOfWork.publish), a adapter dostarcza go odbiorcom dopiero po commit.
- Outbox zapisuje zdarzenie w tej samej transakcji co zmianę stanu, a osobny relay dostarcza je później, więc nie ginie, ale może się zdublować.
- Idempotentność konsumenta zapewnia adapter: unikalny znacznik wiadomości zapisany w tej samej transakcji co zmiana stanu, a duplikat jest potwierdzany i pomijany.
- Trzymaj porty synchroniczne, a async zamykaj w adapterach: mostem do korutyn, wątkiem roboczym dla use case'u albo zdarzeniem z Outboxa.

## Pytania sprawdzające

### 35. Czym jest wzorzec Unit of Work i jak wyrazić go jako port?

<details>
<summary>Odpowiedź</summary>

Unit of Work to obiekt obejmujący jeden scenariusz biznesowy, który zatwierdza wszystkie jego zmiany razem albo żadnej. Wyrażasz go jako port rdzenia: context manager udostępniający repozytoria oraz metody commit i rollback. Domyślnie wyjście z bloku bez commit cofa zmiany. Dzięki temu rdzeń gwarantuje atomowość, nie znając sesji ani transakcji bazy.

Zobacz: [sekcja „Unit of Work jako port”](#unit-of-work-jako-port).

</details>

### 36. Gdzie powinna leżeć granica transakcji: w use case czy w adapterze?

<details>
<summary>Odpowiedź</summary>

Granica transakcji powinna leżeć w use case, bo tylko on wie, co stanowi jeden kompletny scenariusz biznesowy. Use case otwiera Unit of Work i decyduje o wywołaniu commit, a adapter tylko technicznie realizuje commit i rollback na sesji. Granica w adapterze (commit w repozytorium albo w middleware HTTP) uzależnia atomowość od kanału wejścia lub pojedynczej operacji i może rozbić scenariusz na kilka transakcji.

Zobacz: [sekcja „Granica transakcji: use case czy adapter”](#granica-transakcji-use-case-czy-adapter).

</details>

### 37. Czym są zdarzenia domenowe i jak publikować je przez port?

<details>
<summary>Odpowiedź</summary>

Zdarzenie domenowe to niezmienny fakt z przeszłości, wyrażony w języku domeny, np. RentalFinished, który mówi, co się stało, a nie co ma zrobić odbiorca. Rdzeń publikuje je przez port wyjściowy, w tym przykładzie metodę publish w Unit of Work, dzięki czemu use case nie zna kolejki ani kanałów powiadomień. Zdarzenie trafia na zewnątrz dopiero po udanym commit, więc jest częścią tego samego scenariusza co zmiana stanu.

Zobacz: [sekcja „Zdarzenia domenowe i port publikacji”](#zdarzenia-domenowe-i-port-publikacji).

</details>

### 38. Czym jest wzorzec Outbox i jaki problem rozwiązuje?

<details>
<summary>Odpowiedź</summary>

Outbox to wzorzec, w którym zdarzenie zapisujesz do tabeli w tej samej transakcji bazy co zmianę stanu, a osobny proces dostarcza je później na zewnątrz. Rozwiązuje problem podwójnego zapisu: bez niego commit w bazie i wysyłka do kolejki to dwie operacje, z których jedna może się udać bez drugiej. Outbox daje gwarancję co najmniej jednego dostarczenia, więc odbiorcy muszą tolerować duplikaty.

Zobacz: [sekcja „Outbox: zdarzenia w tej samej transakcji”](#outbox-zdarzenia-w-tej-samej-transakcji).

</details>

### 39. Jak zapewnić idempotentność w adapterze wejściowym konsumującym wiadomości?

<details>
<summary>Odpowiedź</summary>

Adapter wejściowy zapisuje identyfikator każdej wiadomości w tabeli z unikalnym kluczem, w tej samej transakcji co zmiana stanu. Naruszenie unikalności oznacza duplikat, który adapter potwierdza i pomija. Rollback usuwa znacznik razem ze zmianą, więc nieudane przetwarzanie można powtórzyć. Gdy wiadomość nie ma stabilnego identyfikatora, idempotentny musi być sam use case.

Zobacz: [sekcja „Idempotentny konsument wiadomości”](#idempotentny-konsument-wiadomości).

</details>

### 40. Jak zaprojektować porty asynchroniczne, by nie wymuszać async/await w samej domenie?

<details>
<summary>Odpowiedź</summary>

Porty rdzenia zostają synchroniczne, a asynchroniczność przenosisz do adapterów. Adapter async-owy mostkuje korutynę do wywołania blokującego, a adapter wejściowy uruchamia synchroniczny use case w wątku roboczym. Wolne operacje, których wynik nie jest potrzebny od razu, jak SMS, wychodzą jako zdarzenia z Outboxa dostarczane asynchronicznie. Płacisz blokowanym wątkiem na czas wywołania.

Zobacz: [sekcja „Asynchroniczność na brzegu, nie w domenie”](#asynchroniczność-na-brzegu-nie-w-domenie).

</details>
