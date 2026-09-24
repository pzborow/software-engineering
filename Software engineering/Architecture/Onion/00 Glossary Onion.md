# Glosariusz Onion

## Spis haseł

- [Architektura cebulowa](#onion-architecture)
- [Model domeny](#domain-model)
- [Rdzeń aplikacji](#application-core)
- [Infrastruktura](#infrastructure)
- [Architektura warstwowa](#layered-architecture)
- [Reguła zależności](#dependency-rule)
- [Domain Services](#domain-services)
- [Application Services](#application-services)
- [Pierścień zewnętrzny](#outer-ring)
- [Ścisłe warstwowanie](#strict-layering)
- [Luźne warstwowanie](#relaxed-layering)
- [Repozytorium](#repository)
- [Protocol](#protocol)
- [Dependency Inversion Principle](#dependency-inversion)
- [Composition root](#composition-root)
- [Kontener DI](#di-container)
- [DTO](#dto)
- [View model](#view-model)
- [Mapper](#mapper)
- [Referencja projektu](#project-reference)
- [Test architektury](#architecture-test)
- [Niezmiennik](#invariant)
- [Unit of Work](#unit-of-work)
- [Wyjątek domenowy](#domain-exception)
- [Dubler testowy](#test-double)
- [Fake](#fake)
- [Test kontraktowy](#contract-test)
- [Domain-Driven Design](#ddd)
- [Język wszechobecny](#ubiquitous-language)
- [Encja](#entity)
- [Value object](#value-object)
- [Agregat](#aggregate)
- [Architektura heksagonalna](#hexagonal-architecture)
- [Port](#port)
- [Adapter](#adapter)
- [Clean Architecture](#clean-architecture)
- [CQRS](#cqrs)
- [Model odczytu](#read-model)
- [Anemiczny model domeny](#anemic-domain-model)
- [Model persystencji](#persistence-model)
- [Warstwa przelotowa](#pass-through-layer)
- [Eksplozja interfejsów](#interface-explosion)
- [Gruby serwis aplikacyjny](#fat-application-service)
- [Strangler fig](#strangler-fig)
- [Test charakteryzujący](#characterization-test)
- [Anti-corruption layer](#anti-corruption-layer)

<a id="onion-architecture"></a>
## Architektura cebulowa

Onion Architecture Jeffreya Palermo (2008): koncentryczne warstwy z modelem domeny w środku i infrastrukturą na zewnątrz. Zależności wskazują do środka.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Onion.md#term-onion-architecture).

<a id="domain-model"></a>
## Model domeny

Domain Model: najbardziej wewnętrzny pierścień z obiektami biznesowymi, które mają stan i zachowanie. Nie zależy od niczego.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Onion.md#term-domain-model).

<a id="application-core"></a>
## Rdzeń aplikacji

Wszystkie warstwy wewnętrzne cebuli: Domain Model, Domain Services i Application Services. Musi dać się uruchomić bez infrastruktury.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Onion.md#term-application-core).

<a id="infrastructure"></a>
## Infrastruktura

Kod techniczny w pierścieniu zewnętrznym: implementacje repozytoriów, klienci usług, dostęp do plików i kolejek.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Onion.md#term-infrastructure).

<a id="layered-architecture"></a>
## Architektura warstwowa

N-tier: warstwy ułożone w stos (prezentacja, logika, dane), w którym zależności płyną w dół, a baza jest fundamentem.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Onion.md#term-layered-architecture).

<a id="dependency-rule"></a>
## Reguła zależności

Zasada, że kod może zależeć tylko od warstw bliższych środka, a warstwa wewnętrzna nigdy nie importuje zewnętrznej.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20Onion.md#term-dependency-rule).

<a id="domain-services"></a>
## Domain Services

Drugi pierścień: reguły biznesowe obejmujące wiele obiektów domeny oraz, u Palermo, interfejsy repozytoriów.

Pierwsza wzmianka: [rozdział 02](02%20Warstwy%20cebuli.md#term-domain-services).

<a id="application-services"></a>
## Application Services

Trzeci pierścień: przypadki użycia, które orkiestrują kroki scenariusza i wyznaczają transakcje, bez własnych reguł biznesowych.

Pierwsza wzmianka: [rozdział 02](02%20Warstwy%20cebuli.md#term-application-services).

<a id="outer-ring"></a>
## Pierścień zewnętrzny

Najbardziej zewnętrzna warstwa cebuli: UI, API, infrastruktura i testy, traktowane jako wymienni klienci lub dostawcy rdzenia.

Pierwsza wzmianka: [rozdział 02](02%20Warstwy%20cebuli.md#term-outer-ring).

<a id="strict-layering"></a>
## Ścisłe warstwowanie

Układ, w którym warstwa może korzystać tylko z warstwy leżącej bezpośrednio pod nią.

Pierwsza wzmianka: [rozdział 02](02%20Warstwy%20cebuli.md#term-strict-layering).

<a id="relaxed-layering"></a>
## Luźne warstwowanie

Układ, w którym warstwa może korzystać z każdej warstwy bliższej środka. Tak działa Onion w wersji Palermo.

Pierwsza wzmianka: [rozdział 02](02%20Warstwy%20cebuli.md#term-relaxed-layering).

<a id="repository"></a>
## Repozytorium

Obiekt dający dostęp do obiektów domeny jak do kolekcji. Interfejs leży w rdzeniu, implementacja w infrastrukturze.

Pierwsza wzmianka: [rozdział 03](03%20Interfejsy%20i%20odwr%C3%B3cenie%20zale%C5%BCno%C5%9Bci.md#term-repository).

<a id="protocol"></a>
## Protocol

Typ z modułu `typing`, który opisuje interfejs strukturalnie: klasa spełnia go, jeśli ma pasujące metody, bez dziedziczenia.

Pierwsza wzmianka: [rozdział 03](03%20Interfejsy%20i%20odwr%C3%B3cenie%20zale%C5%BCno%C5%9Bci.md#term-protocol).

<a id="dependency-inversion"></a>
## Dependency Inversion Principle

Zasada odwrócenia zależności: moduły wysokiego i niskiego poziomu zależą od abstrakcji należącej do modułu wysokiego poziomu.

Pierwsza wzmianka: [rozdział 03](03%20Interfejsy%20i%20odwr%C3%B3cenie%20zale%C5%BCno%C5%9Bci.md#term-dependency-inversion).

<a id="composition-root"></a>
## Composition root

Jedyne miejsce w pierścieniu zewnętrznym, które zna wszystkie klasy, tworzy implementacje i wstrzykuje je do rdzenia.

Pierwsza wzmianka: [rozdział 03](03%20Interfejsy%20i%20odwr%C3%B3cenie%20zale%C5%BCno%C5%9Bci.md#term-composition-root).

<a id="di-container"></a>
## Kontener DI

Biblioteka automatyzująca tworzenie grafu obiektów na podstawie rejestracji implementacji interfejsów. Opcjonalna.

Pierwsza wzmianka: [rozdział 03](03%20Interfejsy%20i%20odwr%C3%B3cenie%20zale%C5%BCno%C5%9Bci.md#term-di-container).

<a id="dto"></a>
## DTO

Data Transfer Object: prosty obiekt bez zachowania, przenoszący dane przez granicę warstw.

Pierwsza wzmianka: [rozdział 03](03%20Interfejsy%20i%20odwr%C3%B3cenie%20zale%C5%BCno%C5%9Bci.md#term-dto).

<a id="view-model"></a>
## View model

DTO przygotowane pod konkretny ekran lub odpowiedź API, z danymi sformatowanymi do wyświetlenia.

Pierwsza wzmianka: [rozdział 03](03%20Interfejsy%20i%20odwr%C3%B3cenie%20zale%C5%BCno%C5%9Bci.md#term-view-model).

<a id="mapper"></a>
## Mapper

Kod tłumaczący obiekty domeny na DTO, view modele lub wiersze bazy i z powrotem. Leży w warstwie, która zna oba formaty.

Pierwsza wzmianka: [rozdział 03](03%20Interfejsy%20i%20odwr%C3%B3cenie%20zale%C5%BCno%C5%9Bci.md#term-mapper).

<a id="project-reference"></a>
## Referencja projektu

Jawna zależność jednego projektu od innego, np. `ProjectReference` w .NET. Bez niej kompilator nie pozwoli użyć klas.

Pierwsza wzmianka: [rozdział 04](04%20Struktura%20projektu%20i%20granice.md#term-project-reference).

<a id="architecture-test"></a>
## Test architektury

Automatyczny test, np. `import-linter`, ArchUnit lub NetArchTest, który pada, gdy kod łamie regułę zależności.

Pierwsza wzmianka: [rozdział 04](04%20Struktura%20projektu%20i%20granice.md#term-architecture-test).

<a id="invariant"></a>
## Niezmiennik

Warunek, który obiekt domeny musi spełniać zawsze, niezależnie od tego, kto go wywołał.

Pierwsza wzmianka: [rozdział 04](04%20Struktura%20projektu%20i%20granice.md#term-invariant).

<a id="unit-of-work"></a>
## Unit of Work

Interfejs w rdzeniu grupujący repozytoria i zatwierdzający zmiany jedną transakcją. Implementacja leży w infrastrukturze.

Pierwsza wzmianka: [rozdział 04](04%20Struktura%20projektu%20i%20granice.md#term-unit-of-work).

<a id="domain-exception"></a>
## Wyjątek domenowy

Wyjątek nazwany językiem biznesu, np. `BookAlreadyLent`, tłumaczony na kod protokołu w pierścieniu zewnętrznym.

Pierwsza wzmianka: [rozdział 04](04%20Struktura%20projektu%20i%20granice.md#term-domain-exception).

<a id="test-double"></a>
## Dubler testowy

Obiekt zajmujący w teście miejsce prawdziwej implementacji interfejsu: stub, fake albo mock.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie%20i%20model%20domeny.md#term-test-double).

<a id="fake"></a>
## Fake

Działająca, uproszczona implementacja interfejsu, zwykle trzymająca dane w pamięci.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie%20i%20model%20domeny.md#term-fake).

<a id="contract-test"></a>
## Test kontraktowy

Zestaw testów opisujący zachowanie interfejsu, uruchamiany na każdej implementacji, w tym na fake'u i SQL.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie%20i%20model%20domeny.md#term-contract-test).

<a id="ddd"></a>
## Domain-Driven Design

Podejście Erica Evansa do modelowania złożonej logiki biznesowej wokół języka i reguł ekspertów.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie%20i%20model%20domeny.md#term-ddd).

<a id="ubiquitous-language"></a>
## Język wszechobecny

Ubiquitous language: wspólny słownik zespołu i ekspertów domeny, używany wprost w nazwach w kodzie.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie%20i%20model%20domeny.md#term-ubiquitous-language).

<a id="entity"></a>
## Encja

Obiekt domeny z tożsamością, która trwa mimo zmian stanu.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie%20i%20model%20domeny.md#term-entity).

<a id="value-object"></a>
## Value object

Niezmienny obiekt bez tożsamości, porównywany po wartości, np. okres wypożyczenia.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie%20i%20model%20domeny.md#term-value-object).

<a id="aggregate"></a>
## Agregat

Grupa obiektów zmienianych tylko przez korzeń. Jednostka spójności zapisywana w całości.

Pierwsza wzmianka: [rozdział 05](05%20Testowanie%20i%20model%20domeny.md#term-aggregate).

<a id="hexagonal-architecture"></a>
## Architektura heksagonalna

Ports and Adapters Alistaira Cockburna (2005): rdzeń oddzielony od świata portami, z technologią podłączaną przez adaptery.

Pierwsza wzmianka: [rozdział 06](06%20Onion%20na%20tle%20innych%20architektur.md#term-hexagonal-architecture).

<a id="port"></a>
## Port

W hexagonal: interfejs na granicy rdzenia, zdefiniowany przez rdzeń. W Onion odpowiada interfejsowi w warstwie wewnętrznej.

Pierwsza wzmianka: [rozdział 06](06%20Onion%20na%20tle%20innych%20architektur.md#term-port).

<a id="adapter"></a>
## Adapter

W hexagonal: implementacja portu dla konkretnej technologii. W Onion odpowiada implementacji w pierścieniu zewnętrznym.

Pierwsza wzmianka: [rozdział 06](06%20Onion%20na%20tle%20innych%20architektur.md#term-adapter).

<a id="clean-architecture"></a>
## Clean Architecture

Architektura Roberta C. Martina (2012) z kręgami Entities, Use Cases, Interface Adapters oraz Frameworks & Drivers.

Pierwsza wzmianka: [rozdział 06](06%20Onion%20na%20tle%20innych%20architektur.md#term-clean-architecture).

<a id="cqrs"></a>
## CQRS

Command Query Responsibility Segregation: rozdzielenie operacji zmieniających stan od operacji odczytu.

Pierwsza wzmianka: [rozdział 06](06%20Onion%20na%20tle%20innych%20architektur.md#term-cqrs).

<a id="read-model"></a>
## Model odczytu

Płaskie DTO przygotowane pod ekran, dostarczane przez interfejs odczytu z pominięciem warstw domenowych.

Pierwsza wzmianka: [rozdział 06](06%20Onion%20na%20tle%20innych%20architektur.md#term-read-model).

<a id="anemic-domain-model"></a>
## Anemiczny model domeny

Domain Model złożony z klas z samymi danymi, gdzie logika siedzi w Application Services.

Pierwsza wzmianka: [rozdział 07](07%20Pu%C5%82apki%20i%20decyzje.md#term-anemic-domain-model).

<a id="persistence-model"></a>
## Model persystencji

Klasa odwzorowująca tabelę, oddzielona od modelu domeny i tłumaczona przez mapper w repozytorium.

Pierwsza wzmianka: [rozdział 07](07%20Pu%C5%82apki%20i%20decyzje.md#term-persistence-model).

<a id="pass-through-layer"></a>
## Warstwa przelotowa

Warstwa, która tylko przekazuje wywołanie dalej i nie podejmuje żadnej decyzji.

Pierwsza wzmianka: [rozdział 07](07%20Pu%C5%82apki%20i%20decyzje.md#term-pass-through-layer).

<a id="interface-explosion"></a>
## Eksplozja interfejsów

Nadmiar interfejsów i DTO bez drugiej implementacji, przez który proste zmiany dotykają wielu plików.

Pierwsza wzmianka: [rozdział 07](07%20Pu%C5%82apki%20i%20decyzje.md#term-interface-explosion).

<a id="fat-application-service"></a>
## Gruby serwis aplikacyjny

Application Service, który przejął reguły biznesowe i urósł do setek linii z wieloma `if`-ami.

Pierwsza wzmianka: [rozdział 07](07%20Pu%C5%82apki%20i%20decyzje.md#term-fat-application-service).

<a id="strangler-fig"></a>
## Strangler fig

Wzorzec stopniowej migracji, w którym nowa struktura przejmuje kolejne funkcje starego kodu, aż stary można usunąć.

Pierwsza wzmianka: [rozdział 07](07%20Pu%C5%82apki%20i%20decyzje.md#term-strangler-fig).

<a id="characterization-test"></a>
## Test charakteryzujący

Test opisujący obecne zachowanie systemu, łącznie z dziwactwami. Zabezpiecza refaktoryzację.

Pierwsza wzmianka: [rozdział 07](07%20Pu%C5%82apki%20i%20decyzje.md#term-characterization-test).

<a id="anti-corruption-layer"></a>
## Anti-corruption layer

Implementacja w pierścieniu zewnętrznym, która tłumaczy pojęcia obcego lub starego systemu na język domeny.

Pierwsza wzmianka: [rozdział 07](07%20Pu%C5%82apki%20i%20decyzje.md#term-anti-corruption-layer).
