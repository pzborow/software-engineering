# Mapa kontekstów

Konteksty nie żyją osobno. Rezerwacje potrzebują ceny z wyceny, umowa najmu potrzebuje danych z rezerwacji, a rozliczenia potrzebują danych z umowy. Każde takie połączenie to relacja między dwoma modelami i często między dwoma zespołami. DDD daje nazwy dla typowych relacji i narzędzie do ich przedstawienia. Ten rozdział przechodzi przez wszystkie wzorce i pokazuje, kiedy który wybrać.

```text
                    ┌──────────┐
                    │ Identity │ (SaaS)
                    └────┬─────┘
                         │ Conformist
┌─────────┐   OHS/PL     ▼          ACL   ┌───────────────────┐
│ Pricing │──────►┌──────────────┐◄───────│ Legacy Fleet (ERP)│
└─────────┘  U  D │ Reservations │        └───────────────────┘
                  └──────┬───────┘
                         │ Customer–Supplier
                         ▼
                   ┌──────────┐   Partnership   ┌────────┐
                   │  Rental  │◄───────────────►│ Claims │
                   └────┬─────┘                 └────────┘
                        │ Published Language (zdarzenia)
                        ▼
                   ┌──────────┐
                   │ Billing  │
                   └──────────┘
```

## Mapa jako obraz rzeczywistości

<a id="term-context-map"></a>[Context map](00%20Glossary%20DDD.md#context-map) (mapa kontekstów) to przedstawienie wszystkich bounded contextów systemu i relacji między nimi. Pokazuje stan faktyczny, a nie życzeniowy. Jeśli dwa zespoły w praktyce dzielą bazę danych, mapa musi to pokazać, nawet jeśli dokumentacja twierdzi co innego.

Mapa ma dwa wymiary jednocześnie:

- techniczny: kto kogo wywołuje, jak przepływają dane, jakie są kontrakty,
- organizacyjny: które zespoły muszą się dogadywać, kto ma wpływ na kogo, gdzie są zależności w planowaniu.

Wymiar organizacyjny jest często ważniejszy. Relacja między kontekstami zespołu z tego samego pokoju wygląda inaczej niż relacja z zewnętrznym dostawcą, nawet jeśli technicznie jest to to samo wywołanie REST.

## Kto na kogo ma wpływ

Każda relacja ma kierunek. <a id="term-upstream"></a>[Upstream](00%20Glossary%20DDD.md#upstream) to kontekst, którego decyzje wpływają na drugi. <a id="term-downstream"></a>[Downstream](00%20Glossary%20DDD.md#downstream) to kontekst, który od upstreamu zależy. Na mapie oznacza się je literami U i D.

Kierunek dotyczy wpływu, a nie przepływu danych ani kierunku wywołań. `Reservations` może wywoływać `Pricing`, żeby pobrać cenę, ale to `Pricing` jest upstream: jego model i API decydują, co `Reservations` może dostać. Gdy `Pricing` zmieni kontrakt, `Reservations` musi się dostosować, a nie odwrotnie.

Wzorce relacji dzielą się według tego, jak dużo współpracy wymagają i kto ponosi koszt dostosowania.

## Ścisła współpraca

<a id="term-partnership"></a>[Partnership](00%20Glossary%20DDD.md#partnership) to relacja, w której dwa zespoły mają wspólny cel i planują zmiany razem. Sukces jednego zależy od drugiego, więc koordynują wydania, uzgadniają interfejsy i rozwiązują problemy wspólnie. W wypożyczalni `Rental` i `Claims` mogą być w partnerstwie, bo proces zwrotu auta z szkodą wymaga ich ścisłej współpracy.

Partnership jest właściwe, gdy zespoły są blisko organizacyjnie i naprawdę mają wspólne cele. Ryzyko to silne sprzężenie: żaden zespół nie może wdrożyć zmiany samodzielnie, a gdy zmieni się struktura organizacji, relacja się rozpada.

<a id="term-shared-kernel"></a>[Shared Kernel](00%20Glossary%20DDD.md#shared-kernel) to część modelu współdzielona przez dwa konteksty jako wspólny kod: biblioteka, pakiet albo moduł. Na przykład value objects `Money`, `RentalPeriod` i `VehicleClassCode` używane przez `Reservations` i `Pricing`.

```text
reservations/  ──┐
                 ├──► shared_kernel/  (Money, RentalPeriod, VehicleClassCode)
pricing/       ──┘       zmiany tylko za zgodą obu zespołów, wspólne testy
```

Shared Kernel oszczędza duplikacji, ale każda jego zmiana wymaga zgody i testów obu stron. Musi być mały i stabilny. Współdzielenie encji albo agregatów w jądrze prawie zawsze kończy się problemami, bo różne konteksty potrzebują różnych zachowań. Shared Kernel między zespołami bez relacji partnerstwa jest ryzykowny.

## Dostawca i odbiorca

<a id="term-customer-supplier"></a>[Customer–Supplier](00%20Glossary%20DDD.md#customer-supplier) to relacja, w której downstream (klient) ma realny wpływ na plan upstreamu (dostawcy). Zespół `Reservations` zgłasza zespołowi `Pricing` potrzeby, te trafiają do backlogu dostawcy, a obie strony uzgadniają kontrakt i testy akceptacyjne. Dostawca nie może zmienić API bez uwzględnienia klienta.

<a id="term-conformist"></a>[Conformist](00%20Glossary%20DDD.md#conformist) to relacja, w której downstream nie ma wpływu na upstream i przyjmuje jego model w całości, bez tłumaczenia. Typowy przykład to integracja z zewnętrznym dostawcą albo wewnętrznym zespołem, który nie ma powodu uwzględniać naszych potrzeb. `Identity` jako gotowy SaaS narzuca swoje pojęcia (`User`, `Tenant`, `Role`), a my je przyjmujemy.

O tym, czy relacja jest Customer–Supplier, czy Conformist, decyduje organizacja, a nie technika:

| Czynnik | Customer–Supplier | Conformist |
|---|---|---|
| Wpływ downstreamu | ma głos w planie upstreamu | nie ma |
| Motywacja upstreamu | cel wspólny albo rozliczany z obsługi klientów | brak, inne priorytety albo zewnętrzny dostawca |
| Kontrakt | negocjowany, z testami | narzucony |
| Koszt dla downstreamu | niski | model upstreamu wchodzi do naszego kodu |

Conformist ma sens, gdy model upstreamu jest dobry i pasuje do naszych potrzeb albo gdy dotyczy generic subdomain, na której nie budujemy przewagi. Jeśli model upstreamu jest słaby, a dotyczy naszego rdzenia, lepszy jest ACL.

## Warstwa ochronna

<a id="term-anti-corruption-layer"></a>[Anti-Corruption Layer](00%20Glossary%20DDD.md#anti-corruption-layer) (ACL) to warstwa w kontekście downstream, która tłumaczy model upstreamu na własny model. Chroni nasz model przed pojęciami, nazwami i strukturami, które do niego nie pasują.

Wypożyczalnia ma stary system ERP floty, w którym auto to wiersz tabeli `POJAZDY` z kolumnami `STAT_POJ` (kody „A”, „S”, „W”, „X”) i `KL_POJ` (klasa jako numer). Kontekst `Reservations` nie powinien znać tych kodów:

```python
# reservations/adapters/legacy_fleet_acl.py
class LegacyFleetAvailability:                          # implementuje port FleetAvailability
    STATUS = {"A": VehicleStatus.AVAILABLE, "S": VehicleStatus.IN_SERVICE,
              "W": VehicleStatus.RENTED, "X": VehicleStatus.RETIRED}
    CLASS = {1: VehicleClassCode("A"), 2: VehicleClassCode("C"), 7: VehicleClassCode("SUV")}

    def available_count(self, branch: BranchId, vehicle_class: VehicleClassCode, period: RentalPeriod) -> int:
        rows = self._erp.query(
            "SELECT KL_POJ, STAT_POJ, DT_DOST FROM POJAZDY WHERE ODDZ = :o", o=branch.legacy_code
        )
        return sum(
            1 for r in rows
            if self.CLASS.get(r["KL_POJ"]) == vehicle_class
            and self.STATUS[r["STAT_POJ"]] is VehicleStatus.AVAILABLE
            and r["DT_DOST"] <= period.start
        )
```

ACL kosztuje: kod tłumaczący, testy, utrzymanie przy każdej zmianie upstreamu. Jego koszt jest uzasadniony, gdy:

- upstream ma słaby, niezrozumiały albo niepasujący model,
- chronimy core domain albo ważną supporting subdomain,
- upstream jest przejściowy (legacy do wymiany) i chcemy móc go podmienić,
- upstream zmienia się często, a nie chcemy, żeby każda zmiana rozlewała się po naszym kodzie.

ACL nie jest potrzebny, gdy model upstreamu pasuje do naszego albo gdy chodzi o mało ważną integrację. Wtedy wystarczy relacja Conformist. W architekturze heksagonalnej ACL to po prostu adapter wyjściowy z bogatszym mapowaniem.

## Usługa dla wielu

<a id="term-open-host-service"></a>[Open Host Service](00%20Glossary%20DDD.md#open-host-service) (OHS) to sytuacja, w której upstream zamiast budować osobną integrację dla każdego klienta udostępnia jedno, dobrze zdefiniowane i udokumentowane API dla wszystkich. `Pricing` wystawia publiczny endpoint wyceny, z którego korzystają `Reservations`, aplikacja mobilna i partnerzy.

<a id="term-published-language"></a>[Published Language](00%20Glossary%20DDD.md#published-language) to udokumentowany, wspólny format wymiany danych: schemat JSON, Protobuf, Avro, standard branżowy. Często idzie w parze z OHS: usługa jest otwarta, a język jej komunikatów jest opublikowany i wersjonowany.

```json
{
  "quote_id": "q-8f2c1a",
  "vehicle_class": "SUV",
  "period": {"start": "2026-10-01T09:00:00+02:00", "end": "2026-10-05T09:00:00+02:00"},
  "components": [
    {"type": "base_rate", "amount": {"value": "720.00", "currency": "PLN"}},
    {"type": "young_driver_fee", "amount": {"value": "144.00", "currency": "PLN"}}
  ],
  "total": {"value": "864.00", "currency": "PLN"},
  "valid_until": "2026-09-24T12:30:00+02:00",
  "schema_version": 3
}
```

W praktyce OHS i Published Language to publiczne API i kontrakt zdarzeń: REST z OpenAPI, gRPC z Protobuf, zdarzenia integracyjne ze schema registry. Obowiązują te same zasady co przy kontraktach zdarzeń w tutorialu [cqrs](../CQRS/): wersjonowanie, zgodność wstecz, okres przejściowy przy zmianach. Published Language jest oddzielny od wewnętrznego modelu kontekstu. `Pricing` może zmieniać wewnętrzne klasy bez zmiany opublikowanego formatu.

## Brak relacji i brak porządku

<a id="term-separate-ways"></a>[Separate Ways](00%20Glossary%20DDD.md#separate-ways) to świadoma decyzja, że dwa konteksty nie będą zintegrowane. Integracja kosztuje więcej, niż daje: łatwiej zduplikować niewielką funkcję albo obsłużyć przypadek ręcznie. Na przykład moduł rezerwacji grupowych dla firm może mieć własną prostą listę klientów zamiast integracji z CRM, jeśli obsługuje pięćdziesiąt firm rocznie.

<a id="term-big-ball-of-mud"></a>[Big Ball of Mud](00%20Glossary%20DDD.md#big-ball-of-mud) to określenie Briana Foote'a i Josepha Yodera na system bez rozpoznawalnej struktury, w którym modele są pomieszane, a granice nie istnieją. Na mapie kontekstów oznacza się go jako jeden obszar i nie próbuje się modelować jego wnętrza. Ważne jest to, jak nowe konteksty się z nim łączą (zwykle przez ACL), żeby bałagan nie rozlał się dalej.

Objawy Big Ball of Mud na mapie:

- nie da się narysować granic, bo każdy moduł sięga do tabel każdego innego,
- to samo pojęcie ma kilka niezgodnych implementacji,
- zmiany mają nieprzewidywalne skutki w odległych miejscach,
- nikt nie potrafi powiedzieć, który moduł jest właścicielem danych.

## Wybór wzorca

| Sytuacja | Wzorzec |
|---|---|
| dwa zespoły, wspólny cel, wspólne planowanie | Partnership |
| mały, stabilny, wspólny fragment modelu, zespoły blisko siebie | Shared Kernel |
| upstream słucha potrzeb downstreamu | Customer–Supplier |
| upstream nie słucha, a jego model jest akceptowalny | Conformist |
| upstream nie słucha, a jego model szkodzi naszemu | Anti-Corruption Layer |
| upstream ma wielu klientów | Open Host Service i Published Language |
| integracja nie jest warta kosztu | Separate Ways |
| stary system bez struktury | Big Ball of Mud, a do niego ACL |

Mapa się zmienia. Customer–Supplier może zamienić się w Conformist, gdy zespół dostawcy zmieni priorytety. Partnership może się rozpaść po reorganizacji. Mapę aktualizuje się przy każdej istotnej zmianie w zespołach i integracjach.

## Co zapamiętać

- Mapa kontekstów pokazuje stan faktyczny, z wymiarem technicznym i organizacyjnym.
- Upstream wpływa na downstream. Kierunek dotyczy wpływu, a nie kierunku wywołań.
- Partnership i Shared Kernel wymagają ścisłej współpracy, a Shared Kernel musi być mały i stabilny.
- Customer–Supplier i Conformist różnią się tym, czy downstream ma wpływ na upstream. Decyduje organizacja.
- ACL tłumaczy obcy model na własny. Warto go budować, gdy chroni rdzeń przed słabym lub zmiennym modelem.
- Open Host Service i Published Language to jedno publiczne, wersjonowane API dla wielu odbiorców.
- Separate Ways to świadoma rezygnacja z integracji, a Big Ball of Mud to obszar bez struktury, który izoluje się ACL.

## Pytania sprawdzające

### 20. Czym jest context map i co przedstawia: relacje techniczne, organizacyjne czy obie?

<details>
<summary>Odpowiedź</summary>

To przedstawienie wszystkich bounded contextów i relacji między nimi, pokazujące stan faktyczny, a nie życzeniowy. Ma dwa wymiary: techniczny (wywołania, przepływ danych, kontrakty) i organizacyjny (które zespoły muszą się dogadywać, kto ma wpływ na kogo). Wymiar organizacyjny jest często ważniejszy, bo ta sama integracja REST wygląda inaczej z zespołem obok niż z zewnętrznym dostawcą.

Zobacz: sekcja „Mapa jako obraz rzeczywistości”.

</details>

### 21. Czym różnią się relacje upstream i downstream? Kto na kogo ma wpływ?

<details>
<summary>Odpowiedź</summary>

Upstream to kontekst, którego decyzje wpływają na drugi, a downstream od niego zależy i musi dostosować się do jego zmian. Kierunek dotyczy wpływu, a nie przepływu danych czy wywołań: `Reservations` wywołuje `Pricing`, ale to `Pricing` jest upstream, bo jego model i API decydują, co `Reservations` dostaje.

Zobacz: sekcja „Kto na kogo ma wpływ”.

</details>

### 22. Opisz Partnership i Shared Kernel. Kiedy są właściwe i jakie niosą ryzyko?

<details>
<summary>Odpowiedź</summary>

Partnership to dwa zespoły ze wspólnym celem, które razem planują zmiany i koordynują wydania. Pasuje, gdy są blisko organizacyjnie. Ryzyko to silne sprzężenie i rozpad przy reorganizacji. Shared Kernel to wspólny fragment modelu jako wspólny kod (np. `Money`, `RentalPeriod`), zmieniany tylko za zgodą obu stron i ze wspólnymi testami. Musi być mały i stabilny. Współdzielenie encji i agregatów zwykle kończy się źle, podobnie jak Shared Kernel bez partnerstwa.

Zobacz: sekcja „Ścisła współpraca”.

</details>

### 23. Opisz Customer–Supplier i Conformist. Co decyduje o tym, że downstream może negocjować albo musi się dostosować?

<details>
<summary>Odpowiedź</summary>

W Customer–Supplier downstream ma realny wpływ na plan upstreamu: potrzeby trafiają do backlogu dostawcy, a kontrakt i testy akceptacyjne są uzgadniane. W Conformist downstream nie ma wpływu i przyjmuje model upstreamu bez tłumaczenia (np. SaaS do tożsamości). Decyduje organizacja: motywacja upstreamu, wspólne cele, rozliczanie z obsługi klientów. Conformist ma sens, gdy model upstreamu jest dobry albo dotyczy generic subdomain. W innych przypadkach lepszy jest ACL.

Zobacz: sekcja „Dostawca i odbiorca”.

</details>

### 24. Czym jest Anti-Corruption Layer i kiedy jego koszt jest uzasadniony?

<details>
<summary>Odpowiedź</summary>

To warstwa w kontekście downstream, która tłumaczy model upstreamu na własny i chroni nasz model przed obcymi pojęciami (np. kody `STAT_POJ` z ERP zamienione na `VehicleStatus`). Koszt to kod tłumaczący, testy i utrzymanie. Jest uzasadniony, gdy model upstreamu jest słaby lub niepasujący, chronimy core albo ważną supporting subdomain, upstream jest do wymiany albo często się zmienia. Gdy model pasuje, wystarczy Conformist. W hexagonal ACL to adapter wyjściowy z bogatszym mapowaniem.

Zobacz: sekcja „Warstwa ochronna”.

</details>

### 25. Czym są Open Host Service i Published Language? Jak łączą się z kontraktami API i zdarzeń?

<details>
<summary>Odpowiedź</summary>

Open Host Service to jedno, dobrze zdefiniowane i udokumentowane API upstreamu dla wszystkich klientów zamiast osobnych integracji. Published Language to udokumentowany, wersjonowany format wymiany (JSON Schema, Protobuf, Avro, standard branżowy). W praktyce to publiczne REST z OpenAPI, gRPC albo zdarzenia integracyjne ze schema registry, z zasadami zgodności wstecz i okresu przejściowego. Published Language jest oddzielony od wewnętrznego modelu, więc kontekst może zmieniać swoje klasy bez zmiany kontraktu.

Zobacz: sekcja „Usługa dla wielu”.

</details>

### 26. Kiedy wybrać Separate Ways i jak rozpoznać Big Ball of Mud na mapie kontekstów?

<details>
<summary>Odpowiedź</summary>

Separate Ways wybiera się, gdy integracja kosztuje więcej, niż daje, i taniej jest zduplikować małą funkcję albo obsłużyć przypadek ręcznie. Big Ball of Mud to system bez struktury: nie da się narysować granic, bo moduły sięgają do cudzych tabel, pojęcia mają kilka niezgodnych implementacji, zmiany mają nieprzewidywalne skutki, a nikt nie wie, kto jest właścicielem danych. Na mapie oznacza się go jako jeden obszar i łączy z nim nowe konteksty przez ACL.

Zobacz: sekcja „Brak relacji i brak porządku”.

</details>
