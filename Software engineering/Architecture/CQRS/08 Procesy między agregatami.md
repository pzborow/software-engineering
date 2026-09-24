# Procesy między agregatami

Agregat to granica transakcji: jedna komenda zmienia jeden agregat. Wiele procesów biznesowych obejmuje jednak kilka agregatów, a czasem kilka systemów. W helpdesku rozwiązanie „wymiana urządzenia” oznacza rezerwację urządzenia w magazynie, zamówienie kuriera i pobranie opłaty od klienta. Nie da się tego zrobić w jednej transakcji, a każdy krok może się nie udać.

```text
TicketResolved(resolution=replacement)
      │
      ▼
ReserveDevice (magazyn) ──ok──► ScheduleCourier (logistyka) ──ok──► ChargeFee (płatności) ──ok──► koniec
      │                               │                                  │
     błąd                            błąd                               błąd
      ▼                               ▼                                  ▼
  ReopenTicket              ReleaseDevice                     CancelCourier + ReleaseDevice
```

## Lokalne transakcje zamiast rozproszonej

<a id="term-saga"></a>[Saga](00%20Glossary%20CQRS.md#saga) to proces złożony z sekwencji lokalnych transakcji. Każdy krok zmienia jeden agregat albo jeden system i publikuje zdarzenie. Jeśli któryś krok się nie uda, wcześniejsze kroki są wycofywane. Nie robi tego rollback, tylko <a id="term-compensation"></a>[kompensacja](00%20Glossary%20CQRS.md#compensation), czyli osobna operacja biznesowa odwracająca skutek kroku.

Pojęcie pochodzi z artykułu Garcii-Moliny i Salem z 1987 roku o długotrwałych transakcjach w bazach danych. W architekturze rozproszonej zastępuje transakcje rozproszone (2PC), które wymagają blokad we wszystkich uczestnikach i nie działają z brokerami ani zewnętrznymi API.

Saga nie daje izolacji. Po zarezerwowaniu urządzenia, a przed pobraniem opłaty, inne procesy widzą urządzenie jako zarezerwowane, choć saga może się jeszcze wycofać. Skutki tego stanu pośredniego trzeba zaprojektować, na przykład przez status „wstępnie zarezerwowane”.

## Kto prowadzi proces

<a id="term-process-manager"></a>[Process manager](00%20Glossary%20CQRS.md#process-manager) to obiekt ze stanem, który śledzi przebieg procesu. Odbiera zdarzenia, zapamiętuje, na którym kroku jest proces, i decyduje, jaką komendę wysłać dalej. Wzorzec pochodzi z książki „Enterprise Integration Patterns” Hohpego i Woolfa.

W praktyce nazwy „saga” i „process manager” są często używane zamiennie. Rozróżnienie, które warto przedstawić na rozmowie:

| | Saga (w ścisłym znaczeniu) | Process manager |
|---|---|---|
| Czym jest | wzorzec zarządzania błędami: sekwencja kroków z kompensacjami | komponent ze stanem sterujący przebiegiem |
| Stan | nie wymaga centralnego stanu | ma trwały stan procesu |
| Logika | liniowa, „krok albo kompensacja” | dowolna: rozgałęzienia, oczekiwanie, timeouty |
| Realizacja | choreografia lub orkiestracja | zawsze centralny koordynator |

Innymi słowy, saga opisuje, co ma się stać przy błędzie, a process manager to jeden ze sposobów, żeby to zrealizować.

```python
@dataclass
class ReplacementProcess:                         # process manager, zapisywany jak agregat
    ticket_id: str
    state: str = "started"                        # started → device_reserved → courier_scheduled → done
    reservation_id: str | None = None
    shipment_id: str | None = None
    deadline: datetime | None = None

    def on(self, event) -> list:                  # zwraca komendy do wysłania
        match (self.state, event):
            case ("started", DeviceReserved(reservation_id=r)):
                self.state, self.reservation_id = "device_reserved", r
                return [ScheduleCourier(self.ticket_id, r)]
            case ("started", DeviceUnavailable()):
                self.state = "failed"
                return [ReopenTicket(self.ticket_id, reason="brak urządzenia")]
            case ("device_reserved", CourierScheduled(shipment_id=s)):
                self.state, self.shipment_id = "courier_scheduled", s
                return [ChargeFee(self.ticket_id, idempotency_key=f"fee-{self.ticket_id}")]
            case ("device_reserved", CourierUnavailable()):
                self.state = "compensating"
                return [ReleaseDevice(self.reservation_id)]
            case ("courier_scheduled", FeeCharged()):
                self.state = "done"
                return []
            case ("courier_scheduled", FeeDeclined()):
                self.state = "compensating"
                return [CancelCourier(self.shipment_id), ReleaseDevice(self.reservation_id)]
        return []                                 # zdarzenie nieistotne albo powtórzone
```

Process manager zapisuje się jak agregat: z wersją, w transakcji z outboxem, z którego wychodzą komendy. Obsługuje też timeouty. Jeśli odpowiedź z magazynu nie przyjdzie w ciągu godziny, zaplanowane zdarzenie `ReplacementTimedOut` uruchomi kompensację.

## Dwa sposoby koordynacji

Proces można koordynować na dwa sposoby.

W <a id="term-choreography"></a>[choreografii](00%20Glossary%20CQRS.md#choreography) nie ma centralnego koordynatora. Każdy uczestnik nasłuchuje zdarzeń innych i sam wie, co zrobić. Magazyn reaguje na `TicketResolved`, logistyka na `DeviceReserved`, a płatności na `CourierScheduled`.

W <a id="term-orchestration"></a>[orkiestracji](00%20Glossary%20CQRS.md#orchestration) jeden komponent, czyli process manager albo silnik workflow, wysyła komendy do uczestników i reaguje na ich odpowiedzi. Uczestnicy nie wiedzą o sobie nawzajem.

```text
Choreografia:                                Orkiestracja:

Helpdesk ──TicketResolved──►                 Helpdesk ──TicketResolved──► Orkiestrator
    Magazyn ──DeviceReserved──►                  Orkiestrator ──ReserveDevice──► Magazyn
        Logistyka ──CourierScheduled──►          Magazyn ──DeviceReserved──► Orkiestrator
            Płatności ──FeeCharged               Orkiestrator ──ScheduleCourier──► Logistyka
                                                 ...
```

| | Choreografia | Orkiestracja |
|---|---|---|
| Sprzężenie | uczestnicy znają zdarzenia innych | uczestnicy znają tylko orkiestratora |
| Widoczność procesu | rozproszona, trudno odpowiedzieć „na jakim etapie jest wymiana” | w jednym miejscu, łatwy podgląd i monitoring |
| Zmiana procesu | zmiany w wielu serwisach | zmiana w orkiestratorze |
| Pojedynczy punkt awarii | brak | orkiestrator, który trzeba uczynić odpornym |
| Dobre dla | krótkich procesów z 2–3 krokami, luźno powiązanych reakcji | długich procesów, rozgałęzień, timeoutów, kompensacji |

Praktyczna reguła: choreografia dla prostych reakcji („po rozwiązaniu zgłoszenia wyślij ankietę”), orkiestracja dla procesów z kompensacjami i więcej niż trzema krokami. W złożonych procesach choreografia prowadzi do sytuacji, w której nikt nie wie, jak naprawdę przebiega proces, bo jego logika jest rozsiana po kilku serwisach. Do orkiestracji można użyć własnego process managera albo silnika workflow, np. Temporal, Camunda albo AWS Step Functions.

## Projektowanie kompensacji

Kompensacja nie jest rollbackiem. Nie przywraca stanu sprzed kroku, tylko wykonuje nową operację biznesową o przeciwnym skutku. Zwrot płatności to nowa transakcja, która pojawia się na wyciągu obok pierwotnej. Wysłanego maila z potwierdzeniem nie da się cofnąć, można tylko wysłać drugi z wyjaśnieniem.

Zasady projektowania:

- każdy krok, który może wymagać wycofania, musi mieć zdefiniowaną kompensację, zanim proces trafi na produkcję,
- kompensacje są idempotentne, bo mogą być ponawiane: `ReleaseDevice` dla już zwolnionego urządzenia nic nie robi,
- kompensacje nie mogą zależeć od stanu, który mógł się zmienić, więc zapamiętuj w procesie ID rezerwacji i przesyłki,
- kroki nieodwracalne (wysłanie paczki, pobranie opłaty bez możliwości zwrotu) umieszcza się jak najpóźniej; krok, po którym proces idzie już tylko do przodu, nazywa się pivot transaction,
- kroki po pivot transaction muszą dać się ponawiać aż do skutku, bo nie ma już odwrotu.

Co, jeśli kompensacja się nie powiedzie? Magazyn nie odpowiada, a urządzenie zostaje zarezerwowane. Postępowanie:

1. Ponawiaj kompensację z rosnącym odstępem. Jest idempotentna, więc powtórzenia są bezpieczne.
2. Po wyczerpaniu prób przenieś proces w stan „wymaga interwencji” i utwórz zadanie dla człowieka z pełnym kontekstem: które kroki się udały, które kompensacje nie, jakie ID są zaangażowane.
3. Uruchom alert i monitoruj liczbę procesów w tym stanie.
4. Zapewnij narzędzie do ręcznego domknięcia procesu, np. panel administracyjny z akcją „oznacz jako zwolnione”.

Nie da się zaprojektować systemu, w którym kompensacje nigdy nie zawodzą. Da się zaprojektować system, w którym każdy taki przypadek jest widoczny i ma właściciela.

## Co zapamiętać

- Saga to sekwencja lokalnych transakcji z kompensacjami zamiast transakcji rozproszonej.
- Saga nie daje izolacji, więc stany pośrednie trzeba zaprojektować jawnie.
- Process manager to komponent ze stanem, który na podstawie zdarzeń decyduje o kolejnych komendach i obsługuje timeouty.
- Choreografia pasuje do prostych reakcji, orkiestracja do długich procesów z kompensacjami.
- Kompensacja to nowa operacja biznesowa, a nie rollback. Musi być idempotentna i ponawialna.
- Kroki nieodwracalne umieszcza się jak najpóźniej, a nieudane kompensacje trafiają do człowieka z pełnym kontekstem.

## Pytania sprawdzające

### 39. Czym jest saga i czym różni się od process managera?

<details>
<summary>Odpowiedź</summary>

Saga to proces złożony z lokalnych transakcji, w którym niepowodzenie kroku uruchamia kompensacje wcześniejszych kroków. Zastępuje 2PC i nie daje izolacji. Process manager to komponent ze stanem (np. z Enterprise Integration Patterns), który odbiera zdarzenia, pamięta etap procesu i decyduje o kolejnych komendach, obsługując też rozgałęzienia i timeouty. Saga opisuje, co ma się stać przy błędzie, a process manager to jeden ze sposobów realizacji. W praktyce nazwy bywają używane zamiennie.

Zobacz: sekcje „Lokalne transakcje zamiast rozproszonej” i „Kto prowadzi proces”.

</details>

### 40. Choreografia czy orkiestracja: jak wybrać sposób koordynacji długiego procesu?

<details>
<summary>Odpowiedź</summary>

W choreografii uczestnicy reagują na zdarzenia innych bez koordynatora: luźne powiązanie i brak pojedynczego punktu awarii, ale logika procesu jest rozproszona i trudno ją obserwować oraz zmieniać. W orkiestracji jeden koordynator (process manager, Temporal, Camunda, Step Functions) wysyła komendy: proces jest widoczny w jednym miejscu i łatwy do zmiany, ale koordynator musi być odporny na awarie. Choreografia pasuje do prostych reakcji, orkiestracja do procesów z więcej niż trzema krokami, kompensacjami i timeoutami.

Zobacz: sekcja „Dwa sposoby koordynacji”.

</details>

### 41. Jak projektować kompensacje i co zrobić, gdy sama kompensacja się nie powiedzie?

<details>
<summary>Odpowiedź</summary>

Kompensacja to nowa operacja biznesowa o przeciwnym skutku, a nie rollback. Każdy odwracalny krok ma ją zdefiniowaną z góry. Kompensacje są idempotentne i opierają się na zapamiętanych ID. Kroki nieodwracalne umieszcza się jak najpóźniej (pivot transaction), a kroki po nich muszą dać się ponawiać do skutku. Gdy kompensacja zawodzi: ponawianie z backoffem, potem stan „wymaga interwencji” z pełnym kontekstem, alert, monitoring i narzędzie do ręcznego domknięcia.

Zobacz: sekcja „Projektowanie kompensacji”.

</details>
