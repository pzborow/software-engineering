# Glosariusz Hexagonal

## Spis haseł

- [Architektura heksagonalna](#hexagonal-architecture)
- [Rdzeń aplikacji](#application-core)
- [Domena](#domain)
- [Infrastruktura](#infrastructure)
- [Port](#port)
- [Adapter](#adapter)
- [Architektura warstwowa](#layered-architecture)
- [Reguła zależności](#dependency-rule)
- [Port wejściowy](#driving-port)
- [Port wyjściowy](#driven-port)
- [Use case](#use-case)
- [Repozytorium](#repository)
- [Adapter wejściowy](#driving-adapter)
- [Adapter wyjściowy](#driven-adapter)
- [DTO](#dto)
- [Mapper](#mapper)
- [Protocol](#protocol)
- [Serwis aplikacyjny](#application-service)
- [Serwis domenowy](#domain-service)
- [Odwrócenie zależności](#dependency-inversion)
- [Composition root](#composition-root)
- [Kontener DI](#di-container)
- [Test architektury](#architecture-test)
- [Niezmiennik](#invariant)
- [Unit of Work](#unit-of-work)
- [Wyjątek domenowy](#domain-exception)
- [Dubler testowy](#test-double)
- [Stub](#stub)
- [Fake](#fake)
- [Adapter w pamięci](#in-memory-adapter)
- [Mock](#mock)
- [Test kontraktowy](#contract-test)
- [Onion Architecture](#onion-architecture)
- [Clean Architecture](#clean-architecture)
- [Domain-Driven Design](#ddd)
- [Bounded context](#bounded-context)
- [Encja](#entity)
- [Value object](#value-object)
- [Agregat](#aggregate)
- [CQRS](#cqrs)
- [Model odczytu](#read-model)
- [Zdarzenie domenowe](#domain-event)
- [Broker wiadomości](#message-broker)
- [Transactional outbox](#outbox)
- [Mikroserwis](#microservice)
- [Modularny monolit](#modular-monolith)
- [Anemiczny model domeny](#anemic-domain-model)
- [Model persystencji](#persistence-model)
- [Eksplozja interfejsów](#interface-explosion)
- [Wyciek logiki](#logic-leak)
- [N+1](#n-plus-one)
- [Strangler fig](#strangler-fig)
- [Anti-corruption layer](#anti-corruption-layer)

<a id="hexagonal-architecture"></a>
## Architektura heksagonalna

Architektura (Ports and Adapters, Alistair Cockburn, 2005), w której rdzeń aplikacji jest odizolowany od technologii przez porty i adaptery. Zależności w kodzie wskazują do środka.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Hexagonal.md#term-hexagonal-architecture).

<a id="application-core"></a>
## Rdzeń aplikacji

Wnętrze heksagonu: domena i scenariusze aplikacji. Nie zależy od frameworka, bazy ani innych technologii.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Hexagonal.md#term-application-core).

<a id="domain"></a>
## Domena

Model pojęć i reguł biznesowych, na przykład zamówienie, pozycja, kwota. Najbardziej wewnętrzna część rdzenia.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Hexagonal.md#term-domain).

<a id="infrastructure"></a>
## Infrastruktura

Kod techniczny łączący aplikację z konkretnymi narzędziami: bazą, frameworkiem HTTP, brokerem, zewnętrznymi API.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Hexagonal.md#term-infrastructure).

<a id="port"></a>
## Port

Interfejs na granicy rdzenia, zdefiniowany przez rdzeń i wyrażony w pojęciach domeny. Opisuje, co aplikacja oferuje albo czego potrzebuje.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Hexagonal.md#term-port).

<a id="adapter"></a>
## Adapter

Konkretna klasa, która tłumaczy port na technologię: wywołuje port wejściowy albo implementuje port wyjściowy.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Hexagonal.md#term-adapter).

<a id="layered-architecture"></a>
## Architektura warstwowa

Układ prezentacja → logika → dostęp do danych, w którym zależności płyną w dół, więc logika biznesowa zależy od warstwy danych.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Hexagonal.md#term-layered-architecture).

<a id="dependency-rule"></a>
## Reguła zależności

Zasada, że zależności w kodzie wskazują zawsze do środka: adapter importuje rdzeń, rdzeń nigdy nie importuje adaptera.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Hexagonal.md#term-dependency-rule).

<a id="driving-port"></a>
## Port wejściowy

Port po stronie driving (primary): opisuje, co aplikacja potrafi zrobić. Wywoływany przez świat zewnętrzny, zwykle realizowany przez use case.

Pierwsza wzmianka: [rozdział 02](02%20Porty%20i%20adaptery.md#term-driving-port).

<a id="driven-port"></a>
## Port wyjściowy

Port po stronie driven (secondary): opisuje, czego aplikacja potrzebuje od świata. Wywoływany przez rdzeń, implementowany przez adapter.

Pierwsza wzmianka: [rozdział 02](02%20Porty%20i%20adaptery.md#term-driven-port).

<a id="use-case"></a>
## Use case

Klasa albo funkcja realizująca jeden scenariusz biznesowy, na przykład złożenie zamówienia. Najczęstsza realizacja portu wejściowego.

Pierwsza wzmianka: [rozdział 02](02%20Porty%20i%20adaptery.md#term-use-case).

<a id="repository"></a>
## Repozytorium

Port wyjściowy udający kolekcję obiektów domeny, z operacjami typu `get` i `save`. W DDD operuje na całych agregatach.

Pierwsza wzmianka: [rozdział 02](02%20Porty%20i%20adaptery.md#term-repository).

<a id="driving-adapter"></a>
## Adapter wejściowy

Adapter, który tłumaczy żądanie z zewnątrz (HTTP, CLI, wiadomość z kolejki) na wywołanie portu wejściowego.

Pierwsza wzmianka: [rozdział 02](02%20Porty%20i%20adaptery.md#term-driving-adapter).

<a id="driven-adapter"></a>
## Adapter wyjściowy

Adapter implementujący port wyjściowy przy użyciu konkretnej technologii, na przykład repozytorium SQL albo klient płatności.

Pierwsza wzmianka: [rozdział 02](02%20Porty%20i%20adaptery.md#term-driven-adapter).

<a id="dto"></a>
## DTO

Data Transfer Object: prosty obiekt bez zachowania, służący do przenoszenia danych przez granicę, na przykład model żądania HTTP.

Pierwsza wzmianka: [rozdział 02](02%20Porty%20i%20adaptery.md#term-dto).

<a id="mapper"></a>
## Mapper

Kod przepisujący dane między DTO lub modelem persystencji a obiektami domeny. Żyje w adapterze.

Pierwsza wzmianka: [rozdział 02](02%20Porty%20i%20adaptery.md#term-mapper).

<a id="protocol"></a>
## Protocol

Typ z modułu `typing`, który opisuje interfejs strukturalnie: klasa spełnia go, jeśli ma pasujące metody, bez dziedziczenia.

Pierwsza wzmianka: [rozdział 03](03%20Struktura%20kodu.md#term-protocol).

<a id="application-service"></a>
## Serwis aplikacyjny

Inna nazwa use case'u: orkiestruje scenariusz przez porty i domenę, ale sam nie zawiera reguł biznesowych.

Pierwsza wzmianka: [rozdział 03](03%20Struktura%20kodu.md#term-application-service).

<a id="domain-service"></a>
## Serwis domenowy

Obiekt w domenie zawierający regułę biznesową, która nie pasuje do jednej encji. Nie używa portów.

Pierwsza wzmianka: [rozdział 03](03%20Struktura%20kodu.md#term-domain-service).

<a id="dependency-inversion"></a>
## Odwrócenie zależności

Dependency Inversion Principle: moduł wysokiego i niskiego poziomu zależą od abstrakcji należącej do modułu wysokiego poziomu.

Pierwsza wzmianka: [rozdział 03](03%20Struktura%20kodu.md#term-dependency-inversion).

<a id="composition-root"></a>
## Composition root

Jedyne miejsce przy starcie aplikacji, które zna wszystkie klasy, tworzy adaptery i wstrzykuje je do use case'ów.

Pierwsza wzmianka: [rozdział 03](03%20Struktura%20kodu.md#term-composition-root).

<a id="di-container"></a>
## Kontener DI

Biblioteka automatyzująca tworzenie grafu obiektów na podstawie rejestracji implementacji portów. Opcjonalna.

Pierwsza wzmianka: [rozdział 03](03%20Struktura%20kodu.md#term-di-container).

<a id="architecture-test"></a>
## Test architektury

Automatyczny test, na przykład `import-linter` albo ArchUnit, który pada, gdy kod łamie regułę zależności.

Pierwsza wzmianka: [rozdział 04](04%20Granice%2C%20walidacja%20i%20transakcje.md#term-architecture-test).

<a id="invariant"></a>
## Niezmiennik

Warunek, który obiekt domeny musi spełniać zawsze, niezależnie od tego, kto go wywołał.

Pierwsza wzmianka: [rozdział 04](04%20Granice%2C%20walidacja%20i%20transakcje.md#term-invariant).

<a id="unit-of-work"></a>
## Unit of Work

Port grupujący zmiany w jedną transakcję. Use case wyznacza jej granice, a adapter realizuje ją na konkretnej bazie.

Pierwsza wzmianka: [rozdział 04](04%20Granice%2C%20walidacja%20i%20transakcje.md#term-unit-of-work).

<a id="domain-exception"></a>
## Wyjątek domenowy

Wyjątek nazwany w języku biznesu, na przykład `OrderNotFound`. Adapter wejściowy tłumaczy go na kod protokołu.

Pierwsza wzmianka: [rozdział 04](04%20Granice%2C%20walidacja%20i%20transakcje.md#term-domain-exception).

<a id="test-double"></a>
## Dubler testowy

Obiekt zajmujący w teście miejsce prawdziwej implementacji portu. Ogólna nazwa dla stubów, fake'ów i mocków.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie.md#term-test-double).

<a id="stub"></a>
## Stub

Dubler zwracający przygotowane odpowiedzi, bez stanu i bez nagrywania wywołań.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie.md#term-stub).

<a id="fake"></a>
## Fake

Działająca, uproszczona implementacja portu, zwykle trzymająca dane w pamięci.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie.md#term-fake).

<a id="in-memory-adapter"></a>
## Adapter w pamięci

Implementacja portu wyjściowego na strukturach w pamięci, na przykład słowniku. Używana w testach i prototypach.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie.md#term-in-memory-adapter).

<a id="mock"></a>
## Mock

Dubler nagrywający wywołania, pozwalający sprawdzić, czy i z jakimi argumentami wywołano metodę.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie.md#term-mock).

<a id="contract-test"></a>
## Test kontraktowy

Zestaw testów opisujący zachowanie portu, uruchamiany na każdej implementacji, w tym na fake'u i prawdziwym adapterze.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie.md#term-contract-test).

<a id="onion-architecture"></a>
## Onion Architecture

Architektura Jeffreya Palermo z koncentrycznymi warstwami: model domeny w środku, dalej serwisy, infrastruktura na zewnątrz.

Pierwsza wzmianka: [rozdział 06](06%20Hexagonal%20na%20tle%20innych%20architektur.md#term-onion-architecture).

<a id="clean-architecture"></a>
## Clean Architecture

Architektura Roberta C. Martina z kręgami Entities, Use Cases, Interface Adapters, Frameworks & Drivers i jawną regułą zależności.

Pierwsza wzmianka: [rozdział 06](06%20Hexagonal%20na%20tle%20innych%20architektur.md#term-clean-architecture).

<a id="ddd"></a>
## Domain-Driven Design

Podejście Erica Evansa do modelowania złożonej logiki biznesowej wokół języka i reguł ekspertów domeny.

Pierwsza wzmianka: [rozdział 06](06%20Hexagonal%20na%20tle%20innych%20architektur.md#term-ddd).

<a id="bounded-context"></a>
## Bounded context

Wydzielona część systemu z własnym modelem i językiem. Często odpowiada jednemu heksagonowi.

Pierwsza wzmianka: [rozdział 06](06%20Hexagonal%20na%20tle%20innych%20architektur.md#term-bounded-context).

<a id="entity"></a>
## Encja

Obiekt domeny z tożsamością, która trwa mimo zmian stanu.

Pierwsza wzmianka: [rozdział 06](06%20Hexagonal%20na%20tle%20innych%20architektur.md#term-entity).

<a id="value-object"></a>
## Value object

Niezmienny obiekt bez tożsamości, porównywany po wartości, na przykład `Money`.

Pierwsza wzmianka: [rozdział 06](06%20Hexagonal%20na%20tle%20innych%20architektur.md#term-value-object).

<a id="aggregate"></a>
## Agregat

Grupa obiektów zmienianych tylko przez korzeń. Jednostka spójności zapisywana w całości.

Pierwsza wzmianka: [rozdział 06](06%20Hexagonal%20na%20tle%20innych%20architektur.md#term-aggregate).

<a id="cqrs"></a>
## CQRS

Command Query Responsibility Segregation: rozdzielenie operacji zmieniających stan od operacji odczytu, także na poziomie portów.

Pierwsza wzmianka: [rozdział 07](07%20Hexagonal%20w%20wi%C4%99kszym%20systemie.md#term-cqrs).

<a id="read-model"></a>
## Model odczytu

Płaski obiekt przygotowany pod konkretny ekran lub endpoint, dostarczany przez port odczytu z pominięciem domeny.

Pierwsza wzmianka: [rozdział 07](07%20Hexagonal%20w%20wi%C4%99kszym%20systemie.md#term-read-model).

<a id="domain-event"></a>
## Zdarzenie domenowe

Fakt biznesowy w czasie przeszłym, na przykład `OrderPlaced`, tworzony przez domenę.

Pierwsza wzmianka: [rozdział 07](07%20Hexagonal%20w%20wi%C4%99kszym%20systemie.md#term-domain-event).

<a id="message-broker"></a>
## Broker wiadomości

System pośredniczący w przesyłaniu wiadomości między aplikacjami, na przykład Kafka albo RabbitMQ.

Pierwsza wzmianka: [rozdział 07](07%20Hexagonal%20w%20wi%C4%99kszym%20systemie.md#term-message-broker).

<a id="outbox"></a>
## Transactional outbox

Zapis zdarzeń do tabeli w tej samej transakcji co agregat i osobna publikacja na broker. Zapewnia spójność zapisu i publikacji.

Pierwsza wzmianka: [rozdział 07](07%20Hexagonal%20w%20wi%C4%99kszym%20systemie.md#term-outbox).

<a id="microservice"></a>
## Mikroserwis

Osobno wdrażana aplikacja z własną bazą, komunikująca się z innymi przez sieć.

Pierwsza wzmianka: [rozdział 07](07%20Hexagonal%20w%20wi%C4%99kszym%20systemie.md#term-microservice).

<a id="modular-monolith"></a>
## Modularny monolit

Jedna wdrażana aplikacja podzielona na moduły o wyraźnych granicach. Każdy moduł może być osobnym heksagonem.

Pierwsza wzmianka: [rozdział 07](07%20Hexagonal%20w%20wi%C4%99kszym%20systemie.md#term-modular-monolith).

<a id="anemic-domain-model"></a>
## Anemiczny model domeny

Obiekty domeny z samymi danymi i logiką w serwisach, więc rdzeń nie chroni reguł.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-anemic-domain-model).

<a id="persistence-model"></a>
## Model persystencji

Klasa odwzorowująca tabelę bazy, oddzielona od modelu domeny i tłumaczona przez mapper.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-persistence-model).

<a id="interface-explosion"></a>
## Eksplozja interfejsów

Nadmiar portów, interfejsów i DTO bez drugiej implementacji, przez który proste zmiany dotykają wielu plików.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-interface-explosion).

<a id="logic-leak"></a>
## Wyciek logiki

Reguła biznesowa umieszczona w adapterze, na przykład w kontrolerze albo zapytaniu SQL, zamiast w domenie.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-logic-leak).

<a id="n-plus-one"></a>
## N+1

Problem wydajności: jedno zapytanie po listę i osobne zapytanie dla każdego elementu.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-n-plus-one).

<a id="strangler-fig"></a>
## Strangler fig

Wzorzec stopniowej migracji, w którym nowy kod przejmuje kolejne funkcje starego, aż stary można usunąć.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-strangler-fig).

<a id="anti-corruption-layer"></a>
## Anti-corruption layer

Adapter tłumaczący pojęcia obcego lub starego systemu na język własnej domeny.

Pierwsza wzmianka: [rozdział 08](08%20Pu%C5%82apki%20i%20decyzje.md#term-anti-corruption-layer).
