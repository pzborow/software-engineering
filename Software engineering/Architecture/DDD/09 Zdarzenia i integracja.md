# Zdarzenia i integracja

Evans w oryginalnej książce z 2003 roku ledwie wspomniał o zdarzeniach. Dziś są jednym z centralnych elementów DDD: łączą agregaty bez wspólnych transakcji, łączą konteksty bez wspólnego modelu i pozwalają modelować domenę od strony tego, co się w niej dzieje. Ten rozdział opisuje zdarzenia z perspektywy modelowania i integracji. Techniczne szczegóły (outbox, inbox, kolejność, projekcje) są w tutorialu [cqrs](../CQRS/).

```text
agregat RentalAgreement ──► VehicleReturned (zdarzenie domenowe, wewnątrz kontekstu Rental)
                                 │
                                 ├──► polityka w Rental: zamknij protokół zwrotu
                                 │
                                 └──► tłumaczenie ──► rental.vehicle-returned.v1 (zdarzenie integracyjne)
                                                          │
                                                          ├──► Fleet: auto dostępne w oddziale
                                                          ├──► Billing: rozlicz najem
                                                          └──► Claims: jeśli szkody, otwórz sprawę
```

## Zdarzenie jako część modelu

<a id="term-domain-event"></a>[Zdarzenie domenowe](00%20Glossary%20DDD.md#domain-event) to zapis czegoś, co wydarzyło się w domenie i ma znaczenie dla ekspertów. Nazywa się je w czasie przeszłym językiem wszechobecnym: `VehicleReturned`, `RentalExtended`, `DamageReported`. Zdarzenie jest faktem, więc jest niezmienne i nie da się go odrzucić.

Zdarzenia zmieniają sposób modelowania. Zamiast zaczynać od struktury danych („jakie tabele i pola ma umowa?”), zaczyna się od pytania „co się dzieje w tym procesie?”. Takie podejście nazywa się <a id="term-event-first"></a>[modelowaniem od zdarzeń](00%20Glossary%20DDD.md#event-first) (event-first) i jest podstawą Event Stormingu z rozdziału 06.

Co zmienia modelowanie od zdarzeń:

- ujawnia ukryte pojęcia. Ekspert mówi „auto zwrócone po czasie”, więc pojawia się pytanie, czy to osobne zdarzenie i jaka reguła za nim stoi,
- skupia się na zachowaniu, a nie na danych. Agregat jest definiowany przez to, jakie zdarzenia produkuje i jakie reguły je warunkują,
- oddziela skutki od przyczyn. Agregat publikuje fakt, a o reakcjach decydują inne części systemu,
- odzwierciedla czas. Kolejność zdarzeń pokazuje proces biznesowy, którego struktura danych nie pokazuje.

```python
class RentalAgreement:
    def return_vehicle(self, at: BranchId, fuel: FuelLevel, mileage: int,
                       damages: list[Damage], now: datetime) -> None:
        if self.return_protocol is not None:
            raise RentalError("Auto już zwrócone")
        self.return_protocol = ReturnProtocol(at, fuel, mileage, damages, now)
        self._record(VehicleReturned(
            agreement_id=self.id, vin=self.vin, branch=at,
            late=now > self.period.end, damages=tuple(damages), returned_at=now,
        ))
```

Agregat zbiera zdarzenia w trakcie operacji, a repozytorium albo Unit of Work publikuje je po zapisie, w tej samej transakcji przez outbox.

## Zdarzenie wewnętrzne i integracyjne

Zdarzenie domenowe jest częścią modelu kontekstu. Zawiera jego pojęcia i typy, zmienia się razem z modelem i jest przeznaczone dla kodu wewnątrz kontekstu. <a id="term-integration-event"></a>[Zdarzenie integracyjne](00%20Glossary%20DDD.md#integration-event) jest częścią kontraktu z innymi kontekstami: opublikowanym językiem z rozdziału 05, stabilnym, wersjonowanym i zawierającym tylko to, czego potrzebują odbiorcy.

| | Zdarzenie domenowe | Zdarzenie integracyjne |
|---|---|---|
| Odbiorcy | kod w tym samym kontekście | inne konteksty, inne zespoły |
| Typy | value objects i encje kontekstu | proste typy i schemat (JSON, Avro, Protobuf) |
| Zmienność | zmienia się z modelem | stabilne, wersjonowane, zgodne wstecz |
| Zawartość | wszystko, co potrzebne w kontekście | tylko to, czego potrzebują odbiorcy |
| Transport | w pamięci albo przez outbox wewnątrz kontekstu | broker z kontraktem i schema registry |
| Nazwa | `VehicleReturned` | `rental.vehicle-returned.v1` |

Dlaczego nie publikować zdarzeń domenowych bezpośrednio innym kontekstom:

- odbiorcy uzależniają się od wewnętrznego modelu, więc każda refaktoryzacja modelu łamie ich kod,
- zdarzenie domenowe może zawierać dane wrażliwe albo wewnętrzne, których inne konteksty nie powinny widzieć,
- zdarzenia domenowe są drobne i częste. Inne konteksty zwykle potrzebują mniej, ale bardziej znaczących faktów,
- kontekst traci możliwość swobodnego zmieniania swojego modelu, a to jest główny powód, dla którego istnieje granica.

Tłumaczenie odbywa się w kontekście nadawcy, w warstwie publikującej:

```python
class RentalIntegrationPublisher:                    # handler zdarzeń domenowych w Rental
    def on_vehicle_returned(self, e: VehicleReturned) -> None:
        self._outbox.add(IntegrationMessage(
            type="rental.vehicle-returned",
            version=1,
            key=str(e.vin),
            data={
                "agreement_id": str(e.agreement_id),
                "vin": str(e.vin),
                "branch_code": e.branch.code,
                "returned_at": e.returned_at.isoformat(),
                "has_damages": bool(e.damages),
                "late": e.late,
            },
        ))
```

Szczegóły szkód nie trafiają do zdarzenia integracyjnego. Kontekst `Claims`, jeśli ich potrzebuje, pobiera je przez API albo dostaje osobne, przeznaczone dla niego zdarzenie.

## Spójność między kontekstami

Kontekst `Rental` zamyka umowę, `Fleet` musi oznaczyć auto jako dostępne, `Billing` wystawić fakturę, a `Claims` otworzyć sprawę szkody. Każdy kontekst ma własną bazę i własny model. Transakcja rozproszona (2PC) obejmująca wszystkie byłaby wolna, krucha i niemożliwa z brokerami i zewnętrznymi API.

DDD rozwiązuje to spójnością ostateczną między kontekstami, zbudowaną z trzech elementów:

- zdarzenia integracyjne publikowane przez transactional outbox, żeby zapis stanu i publikacja były atomowe,
- idempotentni odbiorcy, którzy znoszą ponowne dostarczenie tej samej wiadomości (inbox albo naturalna idempotencja),
- <a id="term-saga"></a>[sagi](00%20Glossary%20DDD.md#saga) albo process managery dla procesów, które obejmują kilka kontekstów i wymagają kompensacji, gdy któryś krok się nie uda.

```text
Rental: VehicleReturned ──outbox──► broker
    Fleet:   oznacz auto jako dostępne w oddziale                  (idempotentnie po agreement_id)
    Billing: wystaw fakturę końcową, zwolnij kaucję, jeśli brak szkód
    Claims:  jeśli has_damages, otwórz sprawę szkody
             └── ClaimOpened ──► Billing: wstrzymaj zwrot kaucji do rozstrzygnięcia
```

Ekspert domenowy powinien wiedzieć, gdzie system jest ostatecznie spójny, i zaakceptować to w konkretnych miejscach: „faktura pojawi się po kilku sekundach”, „auto będzie widoczne jako dostępne po minucie”. Szczegóły techniczne, takie jak outbox, inbox, kolejność zdarzeń i sagi z kompensacjami, opisują rozdziały 06 i 08 tutorialu [cqrs](../CQRS/).

## Miejsce CQRS i event sourcingu

DDD często pojawia się razem z dwoma innymi wzorcami, ale żadnego z nich nie wymaga.

<a id="term-cqrs"></a>[Command Query Responsibility Segregation](00%20Glossary%20DDD.md#cqrs) (CQRS) rozdziela model zapisu od modelu odczytu. W DDD model zapisu to agregaty z niezmiennikami, a model odczytu to projekcje dopasowane do ekranów. Połączenie jest naturalne: agregaty projektowane według reguł Vernona są małe i nie nadają się do zapytań przekrojowych („wszystkie auta dostępne w oddziale w weekend”), więc zapytania trafiają do osobnych modeli odczytu.

<a id="term-event-sourcing"></a>[Event sourcing](00%20Glossary%20DDD.md#event-sourcing) przechowuje stan agregatu jako ciąg jego zdarzeń domenowych. Połączenie z DDD też jest naturalne, bo zdarzenia są już częścią modelu. Event sourcing to jednak osobna decyzja z własnymi kosztami (wersjonowanie zdarzeń, RODO, raporty ad hoc), podejmowana per agregat albo per kontekst.

| | Wymagane w DDD | Kiedy warto |
|---|---|---|
| Zdarzenia domenowe | praktycznie tak, jako część modelu | prawie zawsze w core domain |
| CQRS | nie | gdy zapytania są przekrojowe albo mają inne wymagania niż zapis |
| Event sourcing | nie | gdy historia i audyt są wartością biznesową, np. rozliczenia, umowy |

W wypożyczalni rozsądny wybór to: zdarzenia domenowe w każdym kontekście core i supporting, CQRS w `Reservations` i `Fleet` (wyszukiwanie dostępności), event sourcing tylko w `Billing` dla rozliczeń kaucji, gdzie historia każdej operacji ma znaczenie prawne. Szczegóły są w tutorialu [cqrs](../CQRS/).

## Co zapamiętać

- Zdarzenie domenowe to fakt z języka ekspertów w czasie przeszłym, niezmienny i częścią modelu.
- Modelowanie od zdarzeń ujawnia ukryte pojęcia i skupia model na zachowaniu, a nie na danych.
- Zdarzenia domenowe są wewnętrzne, a integracyjne są kontraktem: stabilne, wersjonowane, z minimalnym zakresem danych.
- Publikowanie zdarzeń domenowych innym kontekstom wiąże je z wewnętrznym modelem i odbiera swobodę zmian.
- Spójność między kontekstami daje outbox, idempotentni odbiorcy i sagi, a nie transakcje rozproszone.
- CQRS i event sourcing dobrze łączą się z DDD, ale nie są wymagane. Decyzję podejmuje się per kontekst.

## Pytania sprawdzające

### 41. Czym są zdarzenia domenowe w DDD i jak zmieniają sposób modelowania (event-first)?

<details>
<summary>Odpowiedź</summary>

Zdarzenie domenowe to zapis czegoś ważnego dla ekspertów, nazwany w czasie przeszłym językiem wszechobecnym, niezmienny i nie do odrzucenia. Modelowanie od zdarzeń zaczyna od pytania „co się dzieje”, a nie „jakie są dane”. Ujawnia ukryte pojęcia (np. zwrot po czasie), skupia model na zachowaniu i regułach, oddziela skutki od przyczyn i pokazuje proces w czasie. Agregat zbiera zdarzenia w operacji, a zapis publikuje je przez outbox.

Zobacz: sekcja „Zdarzenie jako część modelu”.

</details>

### 42. Czym różni się zdarzenie domenowe od integracyjnego i dlaczego nie publikować zdarzeń domenowych bezpośrednio innym kontekstom?

<details>
<summary>Odpowiedź</summary>

Zdarzenie domenowe jest wewnętrzną częścią modelu: używa typów kontekstu, zmienia się z modelem i służy kodowi w tym kontekście. Zdarzenie integracyjne jest kontraktem (published language): prosty schemat, wersjonowane, zgodne wstecz, zawiera tylko to, czego potrzebują odbiorcy. Publikowanie zdarzeń domenowych na zewnątrz uzależnia odbiorców od wewnętrznego modelu, może ujawniać dane wewnętrzne, zalewa ich drobnymi faktami i odbiera kontekstowi swobodę zmian. Tłumaczenie odbywa się w kontekście nadawcy.

Zobacz: sekcja „Zdarzenie wewnętrzne i integracyjne”.

</details>

### 43. Jak zapewnić spójność między kontekstami (zdarzenia, sagi, outbox) bez transakcji rozproszonych?

<details>
<summary>Odpowiedź</summary>

Przez spójność ostateczną zbudowaną ze zdarzeń integracyjnych publikowanych przez transactional outbox (atomowy zapis stanu i zdarzenia), idempotentnych odbiorców (inbox albo naturalna idempotencja) i sag lub process managerów dla procesów obejmujących kilka kontekstów, z kompensacjami przy niepowodzeniu. Transakcje rozproszone (2PC) są wolne, kruche i nie działają z brokerami. Ekspert powinien świadomie zaakceptować, gdzie system jest ostatecznie spójny.

Zobacz: sekcja „Spójność między kontekstami”.

</details>

### 44. Jak DDD łączy się z CQRS i event sourcingiem? Czy któreś z nich jest wymagane?

<details>
<summary>Odpowiedź</summary>

Żadne nie jest wymagane. CQRS łączy się naturalnie, bo małe agregaty nie nadają się do zapytań przekrojowych, więc zapytania trafiają do modeli odczytu. Event sourcing łączy się naturalnie, bo zdarzenia domenowe już są częścią modelu, ale ma własne koszty (wersjonowanie zdarzeń, RODO, raporty). Decyzje podejmuje się per kontekst: zdarzenia domenowe prawie zawsze w core, CQRS przy zapytaniach przekrojowych, event sourcing tam, gdzie historia ma wartość biznesową lub prawną.

Zobacz: sekcja „Miejsce CQRS i event sourcingu”.

</details>
