# Glosariusz DDD

## Spis haseł

- [Domain-Driven Design](#ddd)
- [Domena](#domain)
- [Model domeny](#domain-model)
- [Projektowanie strategiczne](#strategic-design)
- [Projektowanie taktyczne](#tactical-design)
- [DDD lite](#ddd-lite)
- [Ubiquitous language](#ubiquitous-language)
- [Ekspert domenowy](#domain-expert)
- [Knowledge crunching](#knowledge-crunching)
- [Refaktoryzacja w stronę głębszego wglądu](#deeper-insight)
- [Subdomena](#subdomain)
- [Core domain](#core-domain)
- [Supporting subdomain](#supporting-subdomain)
- [Generic subdomain](#generic-subdomain)
- [Przestrzeń problemu](#problem-space)
- [Bounded context](#bounded-context)
- [Przestrzeń rozwiązania](#solution-space)
- [Destylacja](#distillation)
- [Domain vision statement](#domain-vision-statement)
- [Segregated core](#segregated-core)
- [Model korporacyjny](#enterprise-model)
- [Zdarzenie przełomowe](#pivotal-event)
- [Mikroserwis](#microservice)
- [Modularny monolit](#modular-monolith)
- [Context map](#context-map)
- [Upstream](#upstream)
- [Downstream](#downstream)
- [Partnership](#partnership)
- [Shared Kernel](#shared-kernel)
- [Customer–Supplier](#customer-supplier)
- [Conformist](#conformist)
- [Anti-Corruption Layer](#anti-corruption-layer)
- [Open Host Service](#open-host-service)
- [Published Language](#published-language)
- [Separate Ways](#separate-ways)
- [Big Ball of Mud](#big-ball-of-mud)
- [Event Storming](#event-storming)
- [Hotspot](#hotspot)
- [Big Picture](#big-picture)
- [Design Level](#design-level)
- [Domain Storytelling](#domain-storytelling)
- [Encja](#entity)
- [Value object](#value-object)
- [Primitive obsession](#primitive-obsession)
- [Serwis domenowy](#domain-service)
- [Fabryka](#factory)
- [Repozytorium](#repository)
- [DAO](#dao)
- [Agregat](#aggregate)
- [Korzeń agregatu](#aggregate-root)
- [Niezmiennik](#invariant)
- [Spójność ostateczna](#eventual-consistency)
- [Zdarzenie domenowe](#domain-event)
- [Modelowanie od zdarzeń](#event-first)
- [Zdarzenie integracyjne](#integration-event)
- [Saga](#saga)
- [CQRS](#cqrs)
- [Event sourcing](#event-sourcing)
- [Architektura heksagonalna](#hexagonal-architecture)
- [Prawo Conwaya](#conways-law)
- [Odwrotny manewr Conwaya](#inverse-conway)
- [Team Topologies](#team-topologies)
- [Anemiczny model domeny](#anemic-domain-model)
- [Transaction script](#transaction-script)
- [Bubble context](#bubble-context)
- [Autonomous bubble](#autonomous-bubble)
- [Strangler fig](#strangler-fig)

<a id="ddd"></a>
## Domain-Driven Design

Podejście Erica Evansa (2003) do tworzenia oprogramowania dla złożonych dziedzin, z modelem domeny budowanym z ekspertami i odzwierciedlonym w kodzie.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20DDD.md#term-ddd).

<a id="domain"></a>
## Domena

Obszar działalności, którym zajmuje się system, np. wynajem samochodów. Główne źródło złożoności oprogramowania.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20DDD.md#term-domain).

<a id="domain-model"></a>
## Model domeny

Uproszczona, celowa reprezentacja wiedzy o domenie: pojęcia, reguły i relacje, obecne w rozmowach i w kodzie.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20DDD.md#term-domain-model).

<a id="strategic-design"></a>
## Projektowanie strategiczne

Część DDD dotycząca podziału systemu i organizacji: subdomeny, bounded contexts, mapa kontekstów, język.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20DDD.md#term-strategic-design).

<a id="tactical-design"></a>
## Projektowanie taktyczne

Część DDD dotycząca budowy modelu w kodzie w obrębie kontekstu: encje, value objects, agregaty, repozytoria, zdarzenia.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20DDD.md#term-tactical-design).

<a id="ddd-lite"></a>
## DDD lite

Stosowanie samych wzorców taktycznych bez języka wszechobecnego, kontekstów i decyzji strategicznych. Termin Vaughna Vernona.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20DDD.md#term-ddd-lite).

<a id="ubiquitous-language"></a>
## Ubiquitous language

Język wszechobecny: wspólny, precyzyjny słownik zespołu i biznesu, używany wszędzie w obrębie jednego modelu, także w kodzie.

Pierwsza wzmianka: [rozdział 02](02%20J%C4%99zyk%20wszechobecny.md#term-ubiquitous-language).

<a id="domain-expert"></a>
## Ekspert domenowy

Osoba znająca domenę z praktyki, która wyjaśnia biznes i weryfikuje model, ale nie projektuje systemu.

Pierwsza wzmianka: [rozdział 02](02%20J%C4%99zyk%20wszechobecny.md#term-domain-expert).

<a id="knowledge-crunching"></a>
## Knowledge crunching

Iteracyjne budowanie modelu z ekspertami na konkretnych przykładach, trwające przez całe życie systemu.

Pierwsza wzmianka: [rozdział 02](02%20J%C4%99zyk%20wszechobecny.md#term-knowledge-crunching).

<a id="deeper-insight"></a>
## Refaktoryzacja w stronę głębszego wglądu

Zmiana modelu po lepszym zrozumieniu domeny, często przez uczynienie ukrytego pojęcia jawnym.

Pierwsza wzmianka: [rozdział 02](02%20J%C4%99zyk%20wszechobecny.md#term-deeper-insight).

<a id="subdomain"></a>
## Subdomena

Obszar działalności biznesu z własnymi problemami i ekspertami: core, supporting albo generic.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-subdomain).

<a id="core-domain"></a>
## Core domain

Subdomena dająca przewagę konkurencyjną: złożona, zmienna, budowana samodzielnie z pełnym DDD.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-core-domain).

<a id="supporting-subdomain"></a>
## Supporting subdomain

Subdomena potrzebna i specyficzna dla firmy, ale niedająca przewagi, zwykle prosta.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-supporting-subdomain).

<a id="generic-subdomain"></a>
## Generic subdomain

Subdomena rozwiązana wszędzie tak samo, np. płatności czy logowanie. Kupowana i integrowana.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-generic-subdomain).

<a id="problem-space"></a>
## Przestrzeń problemu

Obszar biznesu istniejący niezależnie od oprogramowania, opisywany subdomenami.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-problem-space).

<a id="bounded-context"></a>
## Bounded context

Jawna granica, w której obowiązuje jeden model i jeden język. Każde pojęcie ma w niej jedno znaczenie.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-bounded-context).

<a id="solution-space"></a>
## Przestrzeń rozwiązania

Obszar oprogramowania, w którym projektuje się bounded contexty i modele.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-solution-space).

<a id="distillation"></a>
## Destylacja

Wyodrębnianie core domain z kodu pomocniczego, żeby była czytelna i łatwa do zmiany.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-distillation).

<a id="domain-vision-statement"></a>
## Domain vision statement

Krótki opis, czym jest core domain i jaką wartość daje biznesowi.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-domain-vision-statement).

<a id="segregated-core"></a>
## Segregated core

Przeniesienie elementów rdzenia do osobnego modułu i usunięcie z niego elementów pomocniczych.

Pierwsza wzmianka: [rozdział 03](03%20Subdomeny%20i%20destylacja.md#term-segregated-core).

<a id="enterprise-model"></a>
## Model korporacyjny

Próba stworzenia jednego kanonicznego modelu danych dla całej firmy. Zwykle blokuje zmiany i przegrywa z rzeczywistością.

Pierwsza wzmianka: [rozdział 04](04%20Bounded%20contexts.md#term-enterprise-model).

<a id="pivotal-event"></a>
## Zdarzenie przełomowe

Pivotal event: zdarzenie, po którym proces przechodzi do innej fazy, dobry kandydat na granicę kontekstu.

Pierwsza wzmianka: [rozdział 04](04%20Bounded%20contexts.md#term-pivotal-event).

<a id="microservice"></a>
## Mikroserwis

Osobno wdrażana jednostka z własną bazą danych. Często odpowiada jednemu bounded contextowi, ale nie jest z nim tożsama.

Pierwsza wzmianka: [rozdział 04](04%20Bounded%20contexts.md#term-microservice).

<a id="modular-monolith"></a>
## Modularny monolit

Jedno wdrożenie podzielone na moduły z wyraźnymi granicami, np. bounded contexts pilnowane testami architektury.

Pierwsza wzmianka: [rozdział 04](04%20Bounded%20contexts.md#term-modular-monolith).

<a id="context-map"></a>
## Context map

Mapa kontekstów: przedstawienie bounded contextów i relacji między nimi, technicznych i organizacyjnych, w stanie faktycznym.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-context-map).

<a id="upstream"></a>
## Upstream

Kontekst, którego decyzje wpływają na inny kontekst.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-upstream).

<a id="downstream"></a>
## Downstream

Kontekst zależny od upstreamu, który musi dostosować się do jego zmian.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-downstream).

<a id="partnership"></a>
## Partnership

Relacja dwóch zespołów ze wspólnym celem, wspólnym planowaniem i koordynacją wydań.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-partnership).

<a id="shared-kernel"></a>
## Shared Kernel

Mały, stabilny fragment modelu współdzielony jako kod przez dwa konteksty i zmieniany za zgodą obu.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-shared-kernel).

<a id="customer-supplier"></a>
## Customer–Supplier

Relacja, w której downstream ma realny wpływ na plan i kontrakt upstreamu.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-customer-supplier).

<a id="conformist"></a>
## Conformist

Relacja, w której downstream bez wpływu przyjmuje model upstreamu bez tłumaczenia.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-conformist).

<a id="anti-corruption-layer"></a>
## Anti-Corruption Layer

Warstwa w kontekście downstream tłumacząca obcy model na własny i chroniąca go przed obcymi pojęciami.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-anti-corruption-layer).

<a id="open-host-service"></a>
## Open Host Service

Jedno, dobrze zdefiniowane i udokumentowane API upstreamu dla wszystkich klientów.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-open-host-service).

<a id="published-language"></a>
## Published Language

Udokumentowany, wersjonowany format wymiany danych między kontekstami.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-published-language).

<a id="separate-ways"></a>
## Separate Ways

Świadoma rezygnacja z integracji dwóch kontekstów, bo koszt przewyższa korzyść.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-separate-ways).

<a id="big-ball-of-mud"></a>
## Big Ball of Mud

System bez rozpoznawalnej struktury i granic (Foote i Yoder). Na mapie izoluje się go ACL.

Pierwsza wzmianka: [rozdział 05](05%20Mapa%20kontekst%C3%B3w.md#term-big-ball-of-mud).

<a id="event-storming"></a>
## Event Storming

Warsztat Alberta Brandoliniego, w którym uczestnicy budują model ze zdarzeń domenowych na osi czasu.

Pierwsza wzmianka: [rozdział 06](06%20Modelowanie%20wsp%C3%B3lne.md#term-event-storming).

<a id="hotspot"></a>
## Hotspot

Oznaczenie problemu, pytania lub konfliktu na warsztacie Event Stormingu.

Pierwsza wzmianka: [rozdział 06](06%20Modelowanie%20wsp%C3%B3lne.md#term-hotspot).

<a id="big-picture"></a>
## Big Picture

Poziom Event Stormingu obejmujący całą domenę i wszystkich interesariuszy, służący do szukania granic i problemów.

Pierwsza wzmianka: [rozdział 06](06%20Modelowanie%20wsp%C3%B3lne.md#term-big-picture).

<a id="design-level"></a>
## Design Level

Poziom Event Stormingu, na którym zespół z ekspertem wyznacza agregaty i niezmienniki.

Pierwsza wzmianka: [rozdział 06](06%20Modelowanie%20wsp%C3%B3lne.md#term-design-level).

<a id="domain-storytelling"></a>
## Domain Storytelling

Technika Hofera i Schwentnera: ekspert opowiada historię, a moderator rysuje ją językiem obrazkowym.

Pierwsza wzmianka: [rozdział 06](06%20Modelowanie%20wsp%C3%B3lne.md#term-domain-storytelling).

<a id="entity"></a>
## Encja

Obiekt z tożsamością trwającą mimo zmian stanu, porównywany po tożsamości.

Pierwsza wzmianka: [rozdział 07](07%20Wzorce%20taktyczne.md#term-entity).

<a id="value-object"></a>
## Value object

Niezmienny obiekt bez tożsamości, porównywany po wartości, np. `Money`, `RentalPeriod`.

Pierwsza wzmianka: [rozdział 07](07%20Wzorce%20taktyczne.md#term-value-object).

<a id="primitive-obsession"></a>
## Primitive obsession

Przedstawianie pojęć domeny typami prostymi, co prowadzi do pomyłek, rozproszonej walidacji i niejasnych jednostek.

Pierwsza wzmianka: [rozdział 07](07%20Wzorce%20taktyczne.md#term-primitive-obsession).

<a id="domain-service"></a>
## Serwis domenowy

Bezstanowa operacja domeny, która nie należy naturalnie do żadnej encji ani value objectu.

Pierwsza wzmianka: [rozdział 07](07%20Wzorce%20taktyczne.md#term-domain-service).

<a id="factory"></a>
## Fabryka

Obiekt lub metoda tworząca złożony obiekt domeny w poprawnym stanie.

Pierwsza wzmianka: [rozdział 07](07%20Wzorce%20taktyczne.md#term-factory).

<a id="repository"></a>
## Repozytorium

Interfejs udający kolekcję agregatów w pamięci, z metodami z języka domeny, tylko dla korzeni agregatów.

Pierwsza wzmianka: [rozdział 07](07%20Wzorce%20taktyczne.md#term-repository).

<a id="dao"></a>
## DAO

Data Access Object: obiekt dostępu do jednej tabeli z operacjami na wierszach.

Pierwsza wzmianka: [rozdział 07](07%20Wzorce%20taktyczne.md#term-dao).

<a id="aggregate"></a>
## Agregat

Grupa encji i value objectów zmieniana jako całość w jednej transakcji. Granica spójności.

Pierwsza wzmianka: [rozdział 08](08%20Projektowanie%20agregat%C3%B3w.md#term-aggregate).

<a id="aggregate-root"></a>
## Korzeń agregatu

Encja będąca jedynym punktem wejścia do agregatu, przez którą przechodzą wszystkie zmiany.

Pierwsza wzmianka: [rozdział 08](08%20Projektowanie%20agregat%C3%B3w.md#term-aggregate-root).

<a id="invariant"></a>
## Niezmiennik

Reguła biznesowa, która musi być prawdziwa po każdej operacji na agregacie.

Pierwsza wzmianka: [rozdział 08](08%20Projektowanie%20agregat%C3%B3w.md#term-invariant).

<a id="eventual-consistency"></a>
## Spójność ostateczna

Gwarancja, że inne agregaty lub konteksty zobaczą skutek zmiany z opóźnieniem.

Pierwsza wzmianka: [rozdział 08](08%20Projektowanie%20agregat%C3%B3w.md#term-eventual-consistency).

<a id="domain-event"></a>
## Zdarzenie domenowe

Niezmienny fakt ważny dla ekspertów, nazwany w czasie przeszłym, część modelu kontekstu.

Pierwsza wzmianka: [rozdział 09](09%20Zdarzenia%20i%20integracja.md#term-domain-event).

<a id="event-first"></a>
## Modelowanie od zdarzeń

Event-first: budowanie modelu od pytania, co się dzieje w domenie, zamiast od struktury danych.

Pierwsza wzmianka: [rozdział 09](09%20Zdarzenia%20i%20integracja.md#term-event-first).

<a id="integration-event"></a>
## Zdarzenie integracyjne

Stabilne, wersjonowane zdarzenie będące kontraktem między kontekstami, z minimalnym zakresem danych.

Pierwsza wzmianka: [rozdział 09](09%20Zdarzenia%20i%20integracja.md#term-integration-event).

<a id="saga"></a>
## Saga

Proces z lokalnych transakcji w wielu agregatach lub kontekstach, z kompensacjami przy niepowodzeniu.

Pierwsza wzmianka: [rozdział 09](09%20Zdarzenia%20i%20integracja.md#term-saga).

<a id="cqrs"></a>
## CQRS

Command Query Responsibility Segregation: rozdzielenie modelu zapisu (agregaty) od modeli odczytu.

Pierwsza wzmianka: [rozdział 09](09%20Zdarzenia%20i%20integracja.md#term-cqrs).

<a id="event-sourcing"></a>
## Event sourcing

Przechowywanie stanu agregatu jako ciągu jego zdarzeń domenowych.

Pierwsza wzmianka: [rozdział 09](09%20Zdarzenia%20i%20integracja.md#term-event-sourcing).

<a id="hexagonal-architecture"></a>
## Architektura heksagonalna

Ports and Adapters: izolacja modelu domeny od technologii przez porty i adaptery, z zależnościami skierowanymi do środka.

Pierwsza wzmianka: [rozdział 10](10%20Architektura%20i%20organizacja.md#term-hexagonal-architecture).

<a id="conways-law"></a>
## Prawo Conwaya

Obserwacja Melvina Conwaya (1968): organizacje projektują systemy odwzorowujące ich strukturę komunikacji.

Pierwsza wzmianka: [rozdział 10](10%20Architektura%20i%20organizacja.md#term-conways-law).

<a id="inverse-conway"></a>
## Odwrotny manewr Conwaya

Kształtowanie zespołów pod pożądane granice systemu, zamiast pozwalać, by struktura zespołów wyznaczała granice.

Pierwsza wzmianka: [rozdział 10](10%20Architektura%20i%20organizacja.md#term-inverse-conway).

<a id="team-topologies"></a>
## Team Topologies

Model Skeltona i Paisa (2019): zespoły stream-aligned, platform, enabling i complicated-subsystem oraz obciążenie poznawcze.

Pierwsza wzmianka: [rozdział 10](10%20Architektura%20i%20organizacja.md#term-team-topologies).

<a id="anemic-domain-model"></a>
## Anemiczny model domeny

Model z danymi bez zachowań i logiką w serwisach (Martin Fowler). Błąd w złożonej domenie.

Pierwsza wzmianka: [rozdział 11](11%20Pu%C5%82apki%20i%20legacy.md#term-anemic-domain-model).

<a id="transaction-script"></a>
## Transaction script

Procedura obsługująca jedno żądanie od początku do końca na prostych strukturach danych. Wystarcza w prostych subdomenach.

Pierwsza wzmianka: [rozdział 11](11%20Pu%C5%82apki%20i%20legacy.md#term-transaction-script).

<a id="bubble-context"></a>
## Bubble context

Mały, czysty bounded context przy legacy, bez własnej bazy, połączony z nim przez ACL (Evans, 2013).

Pierwsza wzmianka: [rozdział 11](11%20Pu%C5%82apki%20i%20legacy.md#term-bubble-context).

<a id="autonomous-bubble"></a>
## Autonomous bubble

Bubble context z własnymi danymi, synchronizowany z legacy asynchronicznie.

Pierwsza wzmianka: [rozdział 11](11%20Pu%C5%82apki%20i%20legacy.md#term-autonomous-bubble).

<a id="strangler-fig"></a>
## Strangler fig

Wzorzec Martina Fowlera: nowe konteksty stopniowo przejmują funkcje legacy, aż można je usunąć.

Pierwsza wzmianka: [rozdział 11](11%20Pu%C5%82apki%20i%20legacy.md#term-strangler-fig).
