# Glosariusz Clean

## Spis haseł

- [Clean Architecture](#clean-architecture)
- [Polityka](#policy)
- [Szczegół](#detail)
- [Dependency Rule](#dependency-rule)
- [Entities](#entities)
- [Use Cases](#use-cases)
- [Interactor](#interactor)
- [Gateway](#gateway)
- [Interface Adapters](#interface-adapters)
- [Frameworks & Drivers](#frameworks-and-drivers)
- [Input Boundary](#input-boundary)
- [Request Model](#request-model)
- [Output Boundary](#output-boundary)
- [Response Model](#response-model)
- [Kontroler](#controller)
- [Presenter](#presenter)
- [View Model](#view-model)
- [Przepływ sterowania](#flow-of-control)
- [Komponent](#component)
- [REP](#rep)
- [CCP](#ccp)
- [CRP](#crp)
- [Trójkąt napięć](#tension-triangle)
- [ADP](#adp)
- [SDP](#sdp)
- [Niestabilność](#instability)
- [SAP](#sap)
- [Abstrakcyjność](#abstractness)
- [Ciąg główny](#main-sequence)
- [Strefa bólu](#zone-of-pain)
- [Strefa bezużyteczności](#zone-of-uselessness)
- [Humble Object](#humble-object)
- [Main Component](#main-component)
- [Granica częściowa](#partial-boundary)
- [Screaming Architecture](#screaming-architecture)
- [Package by layer](#package-by-layer)
- [Package by feature](#package-by-feature)
- [Package by component](#package-by-component)
- [Test architektury](#architecture-test)
- [Testowe API](#test-api)
- [Niezmiennik](#invariant)
- [Unit of Work](#unit-of-work)
- [Architektura heksagonalna](#hexagonal-architecture)
- [Port](#port)
- [Adapter](#adapter)
- [Architektura cebulowa](#onion-architecture)
- [CQRS](#cqrs)
- [Model odczytu](#read-model)
- [Domain-Driven Design](#ddd)
- [Ceremonia](#ceremony)
- [Wyciek logiki](#logic-leak)
- [Eksplozja interfejsów](#interface-explosion)
- [Strangler fig](#strangler-fig)
- [Test charakteryzujący](#characterization-test)
- [Anti-corruption layer](#anti-corruption-layer)

<a id="clean-architecture"></a>
## Clean Architecture

Architektura Roberta C. Martina (2012, książka 2017) z koncentrycznymi kręgami Entities, Use Cases, Interface Adapters oraz Frameworks & Drivers i jawną Dependency Rule.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Clean.md#term-clean-architecture).

<a id="policy"></a>
## Polityka

Policy: reguły i procedury biznesowe, dla których system istnieje. Kod wysokiego poziomu, położony daleko od wejścia i wyjścia.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Clean.md#term-policy).

<a id="detail"></a>
## Szczegół

Detail: mechanizm komunikacji z polityką, np. baza danych, web, framework, format danych. Polityka nie może od niego zależeć.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Clean.md#term-detail).

<a id="dependency-rule"></a>
## Dependency Rule

Zasada, że zależności w kodzie wskazują wyłącznie do środka. Krąg wewnętrzny nie zna nazw ani formatów danych z kręgów zewnętrznych.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Clean.md#term-dependency-rule).

<a id="entities"></a>
## Entities

Najbardziej wewnętrzny krąg: krytyczne reguły przedsiębiorstwa, które obowiązywałyby także bez systemu. Mogą być klasami albo funkcjami.

Pierwsza wzmianka: [rozdział 02](02%20Cztery%20kr%C4%99gi.md#term-entities).

<a id="use-cases"></a>
## Use Cases

Drugi krąg: reguły specyficzne dla aplikacji, które orkiestrują encje w ramach przypadków użycia.

Pierwsza wzmianka: [rozdział 02](02%20Cztery%20kr%C4%99gi.md#term-use-cases).

<a id="interactor"></a>
## Interactor

Obiekt realizujący jeden przypadek użycia: przyjmuje Request Model, wywołuje encje i gateway'e, przekazuje wynik.

Pierwsza wzmianka: [rozdział 02](02%20Cztery%20kr%C4%99gi.md#term-interactor).

<a id="gateway"></a>
## Gateway

Interfejs dostępu do danych lub usług zewnętrznych, zdefiniowany w kręgu Use Cases i zaimplementowany w Interface Adapters. Odpowiednik repozytorium.

Pierwsza wzmianka: [rozdział 02](02%20Cztery%20kr%C4%99gi.md#term-gateway).

<a id="interface-adapters"></a>
## Interface Adapters

Trzeci krąg: kontrolery, presentery i implementacje gateway'ów, które tłumaczą formaty między przypadkami użycia a narzędziami.

Pierwsza wzmianka: [rozdział 02](02%20Cztery%20kr%C4%99gi.md#term-interface-adapters).

<a id="frameworks-and-drivers"></a>
## Frameworks & Drivers

Najbardziej zewnętrzny krąg: framework webowy, baza, sterowniki i minimalny kod łączący je z resztą.

Pierwsza wzmianka: [rozdział 02](02%20Cztery%20kr%C4%99gi.md#term-frameworks-and-drivers).

<a id="input-boundary"></a>
## Input Boundary

Interfejs wejścia do przypadku użycia, zdefiniowany w Use Cases, implementowany przez interactor i wołany przez kontroler.

Pierwsza wzmianka: [rozdział 03](03%20Przep%C5%82yw%20przez%20granic%C4%99.md#term-input-boundary).

<a id="request-model"></a>
## Request Model

Prosta struktura danych wejściowych przypadku użycia, niezależna od frameworka.

Pierwsza wzmianka: [rozdział 03](03%20Przep%C5%82yw%20przez%20granic%C4%99.md#term-request-model).

<a id="output-boundary"></a>
## Output Boundary

Interfejs wyjścia z przypadku użycia, zdefiniowany w Use Cases i implementowany przez presenter.

Pierwsza wzmianka: [rozdział 03](03%20Przep%C5%82yw%20przez%20granic%C4%99.md#term-output-boundary).

<a id="response-model"></a>
## Response Model

Prosta struktura z wynikiem przypadku użycia w postaci biznesowej, bez formatowania do wyświetlenia.

Pierwsza wzmianka: [rozdział 03](03%20Przep%C5%82yw%20przez%20granic%C4%99.md#term-response-model).

<a id="controller"></a>
## Kontroler

Klasa w Interface Adapters, która zamienia dane frameworka na Request Model i wywołuje Input Boundary.

Pierwsza wzmianka: [rozdział 03](03%20Przep%C5%82yw%20przez%20granic%C4%99.md#term-controller).

<a id="presenter"></a>
## Presenter

Klasa w Interface Adapters implementująca Output Boundary. Zamienia Response Model na View Model.

Pierwsza wzmianka: [rozdział 03](03%20Przep%C5%82yw%20przez%20granic%C4%99.md#term-presenter).

<a id="view-model"></a>
## View Model

Struktura z danymi gotowymi do wyświetlenia: napisy, sformatowane daty, kody statusu, flagi.

Pierwsza wzmianka: [rozdział 03](03%20Przep%C5%82yw%20przez%20granic%C4%99.md#term-view-model).

<a id="flow-of-control"></a>
## Przepływ sterowania

Kolejność wywołań w czasie działania, np. kontroler, interactor, presenter. Może być przeciwna do kierunku zależności w kodzie.

Pierwsza wzmianka: [rozdział 03](03%20Przep%C5%82yw%20przez%20granic%C4%99.md#term-flow-of-control).

<a id="component"></a>
## Komponent

Najmniejsza jednostka wdrożenia lub wydania: `.jar`, `.dll`, gem, a w Pythonie paczka albo pakiet najwyższego poziomu.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-component).

<a id="rep"></a>
## REP

Reuse/Release Equivalence Principle: jednostka ponownego użycia jest jednostką wydania, z wersją i wspólnym tematem.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-rep).

<a id="ccp"></a>
## CCP

Common Closure Principle: grupuj klasy zmieniające się z tych samych powodów i w tym samym czasie. SRP dla komponentów.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-ccp).

<a id="crp"></a>
## CRP

Common Reuse Principle: nie zmuszaj użytkowników komponentu do zależności od rzeczy, których nie używają. ISP dla komponentów.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-crp).

<a id="tension-triangle"></a>
## Trójkąt napięć

Relacja między REP, CCP i CRP: dwie pierwsze powiększają komponenty, trzecia je zmniejsza. Nie da się spełnić wszystkich naraz.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-tension-triangle).

<a id="adp"></a>
## ADP

Acyclic Dependencies Principle: graf zależności między komponentami nie może mieć cykli.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-adp).

<a id="sdp"></a>
## SDP

Stable Dependencies Principle: zależności wskazują w stronę komponentów stabilniejszych.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-sdp).

<a id="instability"></a>
## Niestabilność

Metryka I = Fan-out / (Fan-in + Fan-out). Wartość 0 oznacza komponent maksymalnie stabilny, 1 maksymalnie niestabilny.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-instability).

<a id="sap"></a>
## SAP

Stable Abstractions Principle: komponent powinien być tak abstrakcyjny, jak jest stabilny.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-sap).

<a id="abstractness"></a>
## Abstrakcyjność

Metryka A = Na / Nc: stosunek klas abstrakcyjnych i interfejsów do wszystkich klas komponentu.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-abstractness).

<a id="main-sequence"></a>
## Ciąg główny

Main sequence: odcinek A + I = 1, przy którym powinny leżeć komponenty. Odległość D = |A + I − 1|.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-main-sequence).

<a id="zone-of-pain"></a>
## Strefa bólu

Obszar wokół (0, 0): komponenty stabilne i konkretne, trudne do zmiany i rozszerzenia.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-zone-of-pain).

<a id="zone-of-uselessness"></a>
## Strefa bezużyteczności

Obszar wokół (1, 1): komponenty abstrakcyjne, od których nikt nie zależy.

Pierwsza wzmianka: [rozdział 04](04%20Zasady%20komponent%C3%B3w.md#term-zone-of-uselessness).

<a id="humble-object"></a>
## Humble Object

Wzorzec dzielący zachowanie na minimalną część trudną do testowania i część z logiką łatwą do testowania, np. widok i presenter.

Pierwsza wzmianka: [rozdział 05](05%20Wzorce%20Martina.md#term-humble-object).

<a id="main-component"></a>
## Main Component

Komponent tworzący, konfigurujący i łączący wszystkie inne. Najbrudniejszy szczegół systemu, od którego nic nie zależy.

Pierwsza wzmianka: [rozdział 05](05%20Wzorce%20Martina.md#term-main-component).

<a id="partial-boundary"></a>
## Granica częściowa

Tańszy wariant granicy: pominięcie ostatniego kroku, granica jednowymiarowa (Strategy) albo fasada.

Pierwsza wzmianka: [rozdział 05](05%20Wzorce%20Martina.md#term-partial-boundary).

<a id="screaming-architecture"></a>
## Screaming Architecture

Zasada, że struktura projektu pokazuje przypadki użycia i domenę, a nie użyty framework.

Pierwsza wzmianka: [rozdział 05](05%20Wzorce%20Martina.md#term-screaming-architecture).

<a id="package-by-layer"></a>
## Package by layer

Układ kodu według warstw technicznych, np. controllers, services, repositories.

Pierwsza wzmianka: [rozdział 06](06%20Struktura%2C%20testy%20i%20implementacja.md#term-package-by-layer).

<a id="package-by-feature"></a>
## Package by feature

Układ kodu według funkcji biznesowych, bez granic warstw wewnątrz funkcji.

Pierwsza wzmianka: [rozdział 06](06%20Struktura%2C%20testy%20i%20implementacja.md#term-package-by-feature).

<a id="package-by-component"></a>
## Package by component

Układ Simona Browna: logika i dostęp do danych funkcji w komponencie za wąskim publicznym API, a UI osobno.

Pierwsza wzmianka: [rozdział 06](06%20Struktura%2C%20testy%20i%20implementacja.md#term-package-by-component).

<a id="architecture-test"></a>
## Test architektury

Automatyczny test, np. `import-linter` albo ArchUnit, który pada, gdy kod łamie Dependency Rule.

Pierwsza wzmianka: [rozdział 06](06%20Struktura%2C%20testy%20i%20implementacja.md#term-architecture-test).

<a id="test-api"></a>
## Testowe API

Warstwa, przez którą testy komunikują się z systemem, chroniąca je przed kruchością przy zmianach struktury.

Pierwsza wzmianka: [rozdział 06](06%20Struktura%2C%20testy%20i%20implementacja.md#term-test-api).

<a id="invariant"></a>
## Niezmiennik

Warunek, który encja musi spełniać zawsze, niezależnie od tego, kto ją wywołał.

Pierwsza wzmianka: [rozdział 06](06%20Struktura%2C%20testy%20i%20implementacja.md#term-invariant).

<a id="unit-of-work"></a>
## Unit of Work

Interfejs w kręgu Use Cases grupujący gateway'e i zatwierdzający zmiany w jednej transakcji.

Pierwsza wzmianka: [rozdział 06](06%20Struktura%2C%20testy%20i%20implementacja.md#term-unit-of-work).

<a id="hexagonal-architecture"></a>
## Architektura heksagonalna

Ports and Adapters Alistaira Cockburna (2005): aplikacja oddzielona od świata portami, z technologią podłączaną przez adaptery.

Pierwsza wzmianka: [rozdział 07](07%20Clean%20na%20tle%20innych%20architektur.md#term-hexagonal-architecture).

<a id="port"></a>
## Port

W hexagonal: interfejs na granicy aplikacji, należący do niej. W Clean odpowiada boundaries i gateway'om.

Pierwsza wzmianka: [rozdział 07](07%20Clean%20na%20tle%20innych%20architektur.md#term-port).

<a id="adapter"></a>
## Adapter

W hexagonal: implementacja portu dla konkretnej technologii. W Clean odpowiada klasom z Interface Adapters.

Pierwsza wzmianka: [rozdział 07](07%20Clean%20na%20tle%20innych%20architektur.md#term-adapter).

<a id="onion-architecture"></a>
## Architektura cebulowa

Onion Architecture Jeffreya Palermo (2008): koncentryczne warstwy z modelem domeny w środku i infrastrukturą na zewnątrz.

Pierwsza wzmianka: [rozdział 07](07%20Clean%20na%20tle%20innych%20architektur.md#term-onion-architecture).

<a id="cqrs"></a>
## CQRS

Command Query Responsibility Segregation: rozdzielenie operacji zmieniających stan od operacji odczytu.

Pierwsza wzmianka: [rozdział 07](07%20Clean%20na%20tle%20innych%20architektur.md#term-cqrs).

<a id="read-model"></a>
## Model odczytu

Płaska struktura przygotowana pod ekran, zwracana przez gateway odczytu z pominięciem encji.

Pierwsza wzmianka: [rozdział 07](07%20Clean%20na%20tle%20innych%20architektur.md#term-read-model).

<a id="ddd"></a>
## Domain-Driven Design

Podejście Erica Evansa do modelowania złożonej logiki biznesowej. W Clean wypełnia krąg Entities.

Pierwsza wzmianka: [rozdział 07](07%20Clean%20na%20tle%20innych%20architektur.md#term-ddd).

<a id="ceremony"></a>
## Ceremonia

Kod, który spełnia formę wzorca, ale nie wnosi korzyści, np. presenter ze stanem w synchronicznym API.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-ceremony).

<a id="logic-leak"></a>
## Wyciek logiki

Reguła biznesowa umieszczona w kontrolerze, presenterze albo zapytaniu SQL zamiast w Entities lub Use Cases.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-logic-leak).

<a id="interface-explosion"></a>
## Eksplozja interfejsów

Nadmiar interfejsów i struktur danych bez drugiej implementacji ani drugiego klienta, przez który przypadek użycia ma kilka plików.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-interface-explosion).

<a id="strangler-fig"></a>
## Strangler fig

Wzorzec stopniowej migracji, w którym nowa struktura przejmuje kolejne funkcje starego kodu, aż stary można usunąć.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-strangler-fig).

<a id="characterization-test"></a>
## Test charakteryzujący

Test utrwalający obecne zachowanie systemu, łącznie z dziwactwami, przed refaktoryzacją.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-characterization-test).

<a id="anti-corruption-layer"></a>
## Anti-corruption layer

Implementacja gateway'a tłumacząca pojęcia starego lub obcego systemu na język encji.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-anti-corruption-layer).
