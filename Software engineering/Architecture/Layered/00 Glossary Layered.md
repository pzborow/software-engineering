# Glosariusz Layered

## Spis haseł

- [Architektura warstwowa](#layered-architecture)
- [Warstwa](#layer)
- [Separacja odpowiedzialności](#separation-of-concerns)
- [Tier](#tier)
- [N-tier](#n-tier)
- [Warstwa prezentacji](#presentation-layer)
- [Warstwa serwisów](#service-layer)
- [Warstwa logiki biznesowej](#business-layer)
- [Warstwa dostępu do danych](#data-access-layer)
- [Transaction script](#transaction-script)
- [Model domeny](#domain-model)
- [Granica transakcji](#transaction-boundary)
- [Ścisłe warstwowanie](#strict-layering)
- [Luźne warstwowanie](#relaxed-layering)
- [Warstwa zamknięta](#closed-layer)
- [Warstwa otwarta](#open-layer)
- [Cykl zależności](#dependency-cycle)
- [Test architektury](#architecture-test)
- [MVC](#mvc)
- [Gruby kontroler](#fat-controller)
- [Gruby model](#fat-model)
- [ORM](#orm)
- [Active Record](#active-record)
- [Data Mapper](#data-mapper)
- [Lazy loading](#lazy-loading)
- [Open Session in View](#open-session-in-view)
- [DTO](#dto)
- [Mapper](#mapper)
- [Problem N+1](#n-plus-one)
- [Mock](#mock)
- [Test integracyjny](#integration-test)
- [Anemiczny model domeny](#anemic-domain-model)
- [Sinkhole anti-pattern](#sinkhole-anti-pattern)
- [Procedura składowana](#stored-procedure)
- [Dziurawa abstrakcja](#leaky-abstraction)
- [Modularny monolit](#modular-monolith)
- [Architektura heksagonalna](#hexagonal-architecture)
- [Zasada odwrócenia zależności](#dependency-inversion)
- [Vertical slice architecture](#vertical-slice)
- [Bounded context](#bounded-context)
- [Strangler fig](#strangler-fig)
- [Package by layer](#package-by-layer)
- [Package by feature](#package-by-feature)

<a id="layered-architecture"></a>
## Architektura warstwowa

Podział aplikacji na poziome warstwy o jednym rodzaju odpowiedzialności, z zależnościami wskazującymi w dół.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20s%C4%85%20warstwy.md#term-layered-architecture).

<a id="layer"></a>
## Warstwa

Layer: logiczna grupa kodu o tym samym rodzaju odpowiedzialności, np. prezentacja albo dostęp do danych.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20s%C4%85%20warstwy.md#term-layer).

<a id="separation-of-concerns"></a>
## Separacja odpowiedzialności

Zasada, że kod o różnych odpowiedzialnościach (wyświetlanie, reguły, zapis) powinien być oddzielony.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20s%C4%85%20warstwy.md#term-separation-of-concerns).

<a id="tier"></a>
## Tier

Warstwa fizyczna: osobny proces, serwer lub maszyna, komunikująca się z innymi przez sieć.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20s%C4%85%20warstwy.md#term-tier).

<a id="n-tier"></a>
## N-tier

Układ z dowolną liczbą fizycznych poziomów. Potocznie bywa synonimem architektury warstwowej.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20s%C4%85%20warstwy.md#term-n-tier).

<a id="presentation-layer"></a>
## Warstwa prezentacji

Warstwa obsługująca żądania i odpowiedzi: parsowanie, format, HTML lub JSON, kody statusu.

Pierwsza wzmianka: [rozdział 02](02%20Odpowiedzialno%C5%9Bci%20warstw.md#term-presentation-layer).

<a id="service-layer"></a>
## Warstwa serwisów

Service Layer (Randy Stafford, PoEAA): przypadki użycia, koordynacja, transakcje i uprawnienia.

Pierwsza wzmianka: [rozdział 02](02%20Odpowiedzialno%C5%9Bci%20warstw.md#term-service-layer).

<a id="business-layer"></a>
## Warstwa logiki biznesowej

Warstwa z regułami domeny, np. grafik lekarza, limity wizyt, zasady odwołania.

Pierwsza wzmianka: [rozdział 02](02%20Odpowiedzialno%C5%9Bci%20warstw.md#term-business-layer).

<a id="data-access-layer"></a>
## Warstwa dostępu do danych

Warstwa ukrywająca zapytania, mapowanie i połączenia z bazą.

Pierwsza wzmianka: [rozdział 02](02%20Odpowiedzialno%C5%9Bci%20warstw.md#term-data-access-layer).

<a id="transaction-script"></a>
## Transaction script

Wzorzec Fowlera: procedura obsługująca jedno żądanie od początku do końca, z regułami w kodzie serwisu.

Pierwsza wzmianka: [rozdział 02](02%20Odpowiedzialno%C5%9Bci%20warstw.md#term-transaction-script).

<a id="domain-model"></a>
## Model domeny

Wzorzec Fowlera: obiekty z danymi i zachowaniem, które same pilnują reguł.

Pierwsza wzmianka: [rozdział 02](02%20Odpowiedzialno%C5%9Bci%20warstw.md#term-domain-model).

<a id="transaction-boundary"></a>
## Granica transakcji

Zakres operacji wykonywanych atomowo. W aplikacji warstwowej odpowiada przypadkowi użycia w warstwie serwisów.

Pierwsza wzmianka: [rozdział 02](02%20Odpowiedzialno%C5%9Bci%20warstw.md#term-transaction-boundary).

<a id="strict-layering"></a>
## Ścisłe warstwowanie

Układ, w którym warstwa korzysta tylko z warstwy bezpośrednio pod nią.

Pierwsza wzmianka: [rozdział 03](03%20Regu%C5%82y%20zale%C5%BCno%C5%9Bci.md#term-strict-layering).

<a id="relaxed-layering"></a>
## Luźne warstwowanie

Układ, w którym warstwa może korzystać z dowolnej niższej warstwy.

Pierwsza wzmianka: [rozdział 03](03%20Regu%C5%82y%20zale%C5%BCno%C5%9Bci.md#term-relaxed-layering).

<a id="closed-layer"></a>
## Warstwa zamknięta

Warstwa, przez którą musi przejść każde żądanie (Mark Richards).

Pierwsza wzmianka: [rozdział 03](03%20Regu%C5%82y%20zale%C5%BCno%C5%9Bci.md#term-closed-layer).

<a id="open-layer"></a>
## Warstwa otwarta

Warstwa, którą żądanie może pominąć (Mark Richards).

Pierwsza wzmianka: [rozdział 03](03%20Regu%C5%82y%20zale%C5%BCno%C5%9Bci.md#term-open-layer).

<a id="dependency-cycle"></a>
## Cykl zależności

Sytuacja, w której warstwa niższa zależy od wyższej albo moduły zależą od siebie nawzajem.

Pierwsza wzmianka: [rozdział 03](03%20Regu%C5%82y%20zale%C5%BCno%C5%9Bci.md#term-dependency-cycle).

<a id="architecture-test"></a>
## Test architektury

Automatyczny test (import-linter, ArchUnit, NetArchTest), który pada przy złamaniu reguł warstw.

Pierwsza wzmianka: [rozdział 03](03%20Regu%C5%82y%20zale%C5%BCno%C5%9Bci.md#term-architecture-test).

<a id="mvc"></a>
## MVC

Model–View–Controller: wzorzec warstwy prezentacji. W Django występuje jako MTV.

Pierwsza wzmianka: [rozdział 04](04%20Warstwy%20we%20frameworkach.md#term-mvc).

<a id="fat-controller"></a>
## Gruby kontroler

Kontroler lub widok zawierający logikę biznesową, zapytania i formatowanie naraz.

Pierwsza wzmianka: [rozdział 04](04%20Warstwy%20we%20frameworkach.md#term-fat-controller).

<a id="fat-model"></a>
## Gruby model

Klasa ORM z wieloma metodami biznesowymi, zapytaniami i efektami ubocznymi.

Pierwsza wzmianka: [rozdział 04](04%20Warstwy%20we%20frameworkach.md#term-fat-model).

<a id="orm"></a>
## ORM

Object-Relational Mapper: biblioteka mapująca tabele bazy na obiekty.

Pierwsza wzmianka: [rozdział 04](04%20Warstwy%20we%20frameworkach.md#term-orm).

<a id="active-record"></a>
## Active Record

Wzorzec Fowlera: obiekt odpowiada wierszowi tabeli i sam się zapisuje (Django ORM, Rails).

Pierwsza wzmianka: [rozdział 04](04%20Warstwy%20we%20frameworkach.md#term-active-record).

<a id="data-mapper"></a>
## Data Mapper

Wzorzec Fowlera: osobny mapper przenosi dane między obiektami domeny a tabelami (SQLAlchemy, Hibernate).

Pierwsza wzmianka: [rozdział 04](04%20Warstwy%20we%20frameworkach.md#term-data-mapper).

<a id="lazy-loading"></a>
## Lazy loading

Ładowanie powiązanych obiektów przez ORM dopiero przy pierwszym dostępie, często poza kontrolą warstwy danych.

Pierwsza wzmianka: [rozdział 05](05%20Dane%20mi%C4%99dzy%20warstwami.md#term-lazy-loading).

<a id="open-session-in-view"></a>
## Open Session in View

Utrzymywanie sesji ORM otwartej do końca renderowania widoku, żeby działało leniwe ładowanie.

Pierwsza wzmianka: [rozdział 05](05%20Dane%20mi%C4%99dzy%20warstwami.md#term-open-session-in-view).

<a id="dto"></a>
## DTO

Data Transfer Object: prosty obiekt bez zachowania, przenoszący tylko potrzebne dane między warstwami.

Pierwsza wzmianka: [rozdział 05](05%20Dane%20mi%C4%99dzy%20warstwami.md#term-dto).

<a id="mapper"></a>
## Mapper

Kod przepisujący dane między modelem ORM a DTO lub odwrotnie.

Pierwsza wzmianka: [rozdział 05](05%20Dane%20mi%C4%99dzy%20warstwami.md#term-mapper).

<a id="n-plus-one"></a>
## Problem N+1

Jedno zapytanie po listę i N dodatkowych zapytań po relacje każdego elementu.

Pierwsza wzmianka: [rozdział 05](05%20Dane%20mi%C4%99dzy%20warstwami.md#term-n-plus-one).

<a id="mock"></a>
## Mock

Obiekt zastępujący zależność w teście, zwracający przygotowane odpowiedzi i nagrywający wywołania.

Pierwsza wzmianka: [rozdział 06](06%20Testowanie.md#term-mock).

<a id="integration-test"></a>
## Test integracyjny

Test sprawdzający współpracę warstw z prawdziwą infrastrukturą, np. bazą w kontenerze.

Pierwsza wzmianka: [rozdział 06](06%20Testowanie.md#term-integration-test).

<a id="anemic-domain-model"></a>
## Anemiczny model domeny

Model z danymi bez zachowań i logiką w serwisach (Martin Fowler).

Pierwsza wzmianka: [rozdział 07](07%20Typowe%20problemy.md#term-anemic-domain-model).

<a id="sinkhole-anti-pattern"></a>
## Sinkhole anti-pattern

Żądania przechodzące przez warstwy, które nie wykonują żadnej logiki (Mark Richards). Reguła 80–20.

Pierwsza wzmianka: [rozdział 07](07%20Typowe%20problemy.md#term-sinkhole-anti-pattern).

<a id="stored-procedure"></a>
## Procedura składowana

Kod wykonywany w bazie danych. Umieszczanie w niej reguł biznesowych ukrywa je przed aplikacją.

Pierwsza wzmianka: [rozdział 07](07%20Typowe%20problemy.md#term-stored-procedure).

<a id="leaky-abstraction"></a>
## Dziurawa abstrakcja

Leaky abstraction (Joel Spolsky): abstrakcja, przez którą przeciekają szczegóły ukrywanej technologii.

Pierwsza wzmianka: [rozdział 07](07%20Typowe%20problemy.md#term-leaky-abstraction).

<a id="modular-monolith"></a>
## Modularny monolit

Jedna wdrażana aplikacja podzielona na moduły według obszarów biznesowych, z publicznym API każdego modułu.

Pierwsza wzmianka: [rozdział 08](08%20Warstwy%20na%20tle%20innych%20architektur.md#term-modular-monolith).

<a id="hexagonal-architecture"></a>
## Architektura heksagonalna

Ports and Adapters: logika definiuje interfejsy, a infrastruktura je implementuje. Zależności wskazują do środka.

Pierwsza wzmianka: [rozdział 08](08%20Warstwy%20na%20tle%20innych%20architektur.md#term-hexagonal-architecture).

<a id="dependency-inversion"></a>
## Zasada odwrócenia zależności

Dependency Inversion Principle: moduły wysokiego poziomu nie zależą od niskiego, oba zależą od abstrakcji.

Pierwsza wzmianka: [rozdział 08](08%20Warstwy%20na%20tle%20innych%20architektur.md#term-dependency-inversion).

<a id="vertical-slice"></a>
## Vertical slice architecture

Podział kodu według funkcji zamiast warstw technicznych (Jimmy Bogard).

Pierwsza wzmianka: [rozdział 08](08%20Warstwy%20na%20tle%20innych%20architektur.md#term-vertical-slice).

<a id="bounded-context"></a>
## Bounded context

Granica w DDD, w której obowiązuje jeden model i jeden język. Często odpowiada modułowi.

Pierwsza wzmianka: [rozdział 08](08%20Warstwy%20na%20tle%20innych%20architektur.md#term-bounded-context).

<a id="strangler-fig"></a>
## Strangler fig

Wzorzec Martina Fowlera: nowa struktura stopniowo przejmuje funkcje starej, aż starą można usunąć.

Pierwsza wzmianka: [rozdział 09](09%20Decyzje%20i%20migracja.md#term-strangler-fig).

<a id="package-by-layer"></a>
## Package by layer

Układ katalogów według warstw technicznych: views, services, repositories.

Pierwsza wzmianka: [rozdział 09](09%20Decyzje%20i%20migracja.md#term-package-by-layer).

<a id="package-by-feature"></a>
## Package by feature

Układ katalogów według funkcji lub obszarów biznesowych, z warstwami wewnątrz.

Pierwsza wzmianka: [rozdział 09](09%20Decyzje%20i%20migracja.md#term-package-by-feature).
