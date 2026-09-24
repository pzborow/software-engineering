# Glosariusz Legacy

## Spis haseł

- [Kod legacy](#legacy-code)
- [Dług techniczny](#technical-debt)
- [Kwadrant długu technicznego](#debt-quadrant)
- [Erozja oprogramowania](#software-rot)
- [Archeologia kodu](#code-archaeology)
- [Hotspot](#hotspot)
- [Złożoność cyklomatyczna](#cyclomatic-complexity)
- [Sprzężenie zmian](#change-coupling)
- [Scratch refactoring](#scratch-refactoring)
- [Szkic efektów](#effect-sketch)
- [Test charakteryzujący](#characterization-test)
- [Golden master](#golden-master)
- [Approval testing](#approval-testing)
- [Szew](#seam)
- [Punkt włączenia](#enabling-point)
- [Parametryzacja konstruktora](#parameterize-constructor)
- [Sprout method](#sprout-method)
- [Sprout class](#sprout-class)
- [Wrap method](#wrap-method)
- [Wrap class](#wrap-class)
- [Extract interface](#extract-interface)
- [Subclass and override method](#subclass-and-override)
- [Monkeypatching](#monkeypatching)
- [Refaktoryzacja](#refactoring)
- [Dwa kapelusze](#two-hats)
- [Refaktoryzacja automatyczna](#automated-refactoring)
- [Zasada skauta](#boy-scout-rule)
- [Refaktoryzacja przygotowująca](#preparatory-refactoring)
- [Strangler fig](#strangler-fig)
- [Punkt przechwycenia](#interception-point)
- [Branch by abstraction](#branch-by-abstraction)
- [Mikado Method](#mikado-method)
- [Feature toggle](#feature-toggle)
- [Parallel run](#parallel-run)
- [Expand and contract](#expand-contract)
- [Backfill](#backfill)
- [Widok zgodności](#compatibility-view)
- [Anti-corruption layer](#anti-corruption-layer)
- [Podwójny zapis](#dual-write)
- [Uzgodnienie danych](#data-reconciliation)
- [Big rewrite](#big-rewrite)
- [Parytet funkcji](#feature-parity)
- [Efekt drugiego systemu](#second-system-effect)
- [Płot Chestertona](#chestertons-fence)
- [Koszt opóźnienia](#cost-of-delay)
- [Bus factor](#bus-factor)
- [Programowanie w parach](#pair-programming)
- [Mob programming](#mob-programming)
- [ADR](#adr)
- [Budżet na dług](#debt-budget)

<a id="legacy-code"></a>
## Kod legacy

Według Michaela Feathersa: kod bez testów. Nie da się go zmieniać z pewnością, że nic się nie zepsuło.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20legacy.md#term-legacy-code).

<a id="technical-debt"></a>
## Dług techniczny

Metafora Warda Cunninghama: szybkie rozwiązanie dziś jest pożyczką, której odsetki płaci się przy każdej późniejszej zmianie.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20legacy.md#term-technical-debt).

<a id="debt-quadrant"></a>
## Kwadrant długu technicznego

Podział Martina Fowlera na dług świadomy lub nieświadomy oraz rozważny lub lekkomyślny.

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20legacy.md#term-debt-quadrant).

<a id="software-rot"></a>
## Erozja oprogramowania

Software rot: stopniowy wzrost złożoności i spadek jakości używanego systemu, jeśli nikt aktywnie nad nim nie pracuje (prawa Lehmana).

Pierwsza wzmianka: [rozdział 01](01%20Czym%20jest%20legacy.md#term-software-rot).

<a id="code-archaeology"></a>
## Archeologia kodu

Odtwarzanie kontekstu decyzji z historii repozytorium, zgłoszeń i dokumentów.

Pierwsza wzmianka: [rozdział 02](02%20Rozpoznanie%20terenu.md#term-code-archaeology).

<a id="hotspot"></a>
## Hotspot

Plik lub funkcja jednocześnie często zmieniana i złożona (Adam Tornhill). Najlepsze miejsce na inwestycję w poprawę.

Pierwsza wzmianka: [rozdział 02](02%20Rozpoznanie%20terenu.md#term-hotspot).

<a id="cyclomatic-complexity"></a>
## Złożoność cyklomatyczna

Liczba niezależnych ścieżek przez kod, rosnąca z każdym warunkiem i pętlą.

Pierwsza wzmianka: [rozdział 02](02%20Rozpoznanie%20terenu.md#term-cyclomatic-complexity).

<a id="change-coupling"></a>
## Sprzężenie zmian

Change coupling: pliki często zmieniane w tych samych commitach, co ujawnia ukryte zależności.

Pierwsza wzmianka: [rozdział 02](02%20Rozpoznanie%20terenu.md#term-change-coupling).

<a id="scratch-refactoring"></a>
## Scratch refactoring

Refaktoryzacja na osobnej gałęzi tylko po to, żeby zrozumieć kod. Gałąź się potem wyrzuca (Feathers).

Pierwsza wzmianka: [rozdział 02](02%20Rozpoznanie%20terenu.md#term-scratch-refactoring).

<a id="effect-sketch"></a>
## Szkic efektów

Effect sketch: rysunek pokazujący, które zmienne i funkcje wpływają na które (Feathers).

Pierwsza wzmianka: [rozdział 02](02%20Rozpoznanie%20terenu.md#term-effect-sketch).

<a id="characterization-test"></a>
## Test charakteryzujący

Test opisujący obecne zachowanie kodu, a nie wymagane. Wykrywa każdą zmianę zachowania (Feathers).

Pierwsza wzmianka: [rozdział 03](03%20Testy%20w%20kodzie%20bez%20test%C3%B3w.md#term-characterization-test).

<a id="golden-master"></a>
## Golden master

Nagranie wyniku kodu dla wielu kombinacji danych i porównywanie z nim każdego kolejnego uruchomienia.

Pierwsza wzmianka: [rozdział 03](03%20Testy%20w%20kodzie%20bez%20test%C3%B3w.md#term-golden-master).

<a id="approval-testing"></a>
## Approval testing

Testy porównujące wynik z zatwierdzonym plikiem, z narzędziem do świadomej akceptacji zmian (np. biblioteka approvaltests).

Pierwsza wzmianka: [rozdział 03](03%20Testy%20w%20kodzie%20bez%20test%C3%B3w.md#term-approval-testing).

<a id="seam"></a>
## Szew

Seam: miejsce, w którym można zmienić zachowanie programu bez edytowania kodu w tym miejscu (Feathers).

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-seam).

<a id="enabling-point"></a>
## Punkt włączenia

Enabling point: miejsce, w którym wybiera się zachowanie używane w szwie.

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-enabling-point).

<a id="parameterize-constructor"></a>
## Parametryzacja konstruktora

Przekazanie zależności przez konstruktor z wartością domyślną równą dotychczasowemu zachowaniu.

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-parameterize-constructor).

<a id="sprout-method"></a>
## Sprout method

Nowa logika napisana jako osobna, przetestowana funkcja i wywołana ze starego kodu jedną linią.

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-sprout-method).

<a id="sprout-class"></a>
## Sprout class

Nowa logika napisana jako osobna, przetestowana klasa, tworzona i wywoływana ze starego kodu.

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-sprout-class).

<a id="wrap-method"></a>
## Wrap method

Zmiana nazwy starej funkcji i utworzenie nowej o starej nazwie, która dodaje zachowanie przed lub po.

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-wrap-method).

<a id="wrap-class"></a>
## Wrap class

Owinięcie klasy inną klasą o tym samym interfejsie, która dodaje zachowanie (wzorzec Decorator).

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-wrap-class).

<a id="extract-interface"></a>
## Extract interface

Opisanie używanych metod konkretnej klasy jako interfejsu, żeby w teście podstawić inną implementację.

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-extract-interface).

<a id="subclass-and-override"></a>
## Subclass and override method

Wydzielenie problematycznego wywołania do metody i nadpisanie jej w podklasie testowej. Technika przejściowa.

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-subclass-and-override).

<a id="monkeypatching"></a>
## Monkeypatching

Podmiana atrybutu modułu lub klasy w czasie działania. Przydatny na start, ale jego nadmiar sygnalizuje brak szwów.

Pierwsza wzmianka: [rozdział 04](04%20Rozrywanie%20zale%C5%BCno%C5%9Bci.md#term-monkeypatching).

<a id="refactoring"></a>
## Refaktoryzacja

Zmiana wewnętrznej struktury kodu bez zmiany jego zewnętrznego zachowania (Martin Fowler).

Pierwsza wzmianka: [rozdział 05](05%20Refaktoryzacja.md#term-refactoring).

<a id="two-hats"></a>
## Dwa kapelusze

Metafora Kenta Becka: w danej chwili albo dodajesz funkcję, albo refaktoryzujesz, nigdy oba naraz.

Pierwsza wzmianka: [rozdział 05](05%20Refaktoryzacja.md#term-two-hats).

<a id="automated-refactoring"></a>
## Refaktoryzacja automatyczna

Refaktoryzacja wykonywana przez narzędzie IDE (Rename, Extract, Inline, Move), bezpieczna także bez testów.

Pierwsza wzmianka: [rozdział 05](05%20Refaktoryzacja.md#term-automated-refactoring).

<a id="boy-scout-rule"></a>
## Zasada skauta

Zostaw kod w trochę lepszym stanie, niż go zastałeś (spopularyzowana przez Roberta C. Martina).

Pierwsza wzmianka: [rozdział 05](05%20Refaktoryzacja.md#term-boy-scout-rule).

<a id="preparatory-refactoring"></a>
## Refaktoryzacja przygotowująca

Refaktoryzacja wykonywana przed zmianą, żeby zmiana była łatwa. „Najpierw spraw, żeby zmiana była łatwa, potem zrób łatwą zmianę” (Kent Beck).

Pierwsza wzmianka: [rozdział 05](05%20Refaktoryzacja.md#term-preparatory-refactoring).

<a id="strangler-fig"></a>
## Strangler fig

Wzorzec Martina Fowlera: nowy kod powstaje obok starego i przejmuje kolejne funkcje, aż stary można usunąć.

Pierwsza wzmianka: [rozdział 06](06%20Du%C5%BCe%20zmiany.md#term-strangler-fig).

<a id="interception-point"></a>
## Punkt przechwycenia

Miejsce (fasada, router, proxy), które decyduje, czy żądanie obsłuży stary, czy nowy kod.

Pierwsza wzmianka: [rozdział 06](06%20Du%C5%BCe%20zmiany.md#term-interception-point).

<a id="branch-by-abstraction"></a>
## Branch by abstraction

Wymiana komponentu przez abstrakcję z dwiema implementacjami w głównej gałęzi zamiast długiej gałęzi w gicie.

Pierwsza wzmianka: [rozdział 06](06%20Du%C5%BCe%20zmiany.md#term-branch-by-abstraction).

<a id="mikado-method"></a>
## Mikado Method

Metoda planowania dużej zmiany przez graf warunków wstępnych i cofanie nieudanych prób (Ellnestam, Brolund).

Pierwsza wzmianka: [rozdział 06](06%20Du%C5%BCe%20zmiany.md#term-mikado-method).

<a id="feature-toggle"></a>
## Feature toggle

Flaga funkcji: przełącznik oddzielający wdrożenie kodu od jego włączenia.

Pierwsza wzmianka: [rozdział 06](06%20Du%C5%BCe%20zmiany.md#term-feature-toggle).

<a id="parallel-run"></a>
## Parallel run

Uruchomienie starej i nowej implementacji dla prawdziwych żądań, porównanie wyników i zwrot wyniku starej.

Pierwsza wzmianka: [rozdział 06](06%20Du%C5%BCe%20zmiany.md#term-parallel-run).

<a id="expand-contract"></a>
## Expand and contract

Parallel change: zmiana schematu w fazach dodaj, zapisuj do obu, przełącz odczyt, usuń.

Pierwsza wzmianka: [rozdział 07](07%20Dane%20i%20integracje.md#term-expand-contract).

<a id="backfill"></a>
## Backfill

Uzupełnienie nowej struktury danymi dla istniejących wierszy, zwykle w paczkach.

Pierwsza wzmianka: [rozdział 07](07%20Dane%20i%20integracje.md#term-backfill).

<a id="compatibility-view"></a>
## Widok zgodności

Widok udostępniający starą strukturę danych pod starą nazwą dla dotychczasowych odbiorców.

Pierwsza wzmianka: [rozdział 07](07%20Dane%20i%20integracje.md#term-compatibility-view).

<a id="anti-corruption-layer"></a>
## Anti-corruption layer

Warstwa tłumacząca między nowym kodem a starym systemem, jedyne miejsce znające stare pojęcia i formaty.

Pierwsza wzmianka: [rozdział 07](07%20Dane%20i%20integracje.md#term-anti-corruption-layer).

<a id="dual-write"></a>
## Podwójny zapis

Zapis każdej zmiany do dwóch systemów bez wspólnej transakcji. Grozi rozjechaniem danych.

Pierwsza wzmianka: [rozdział 07](07%20Dane%20i%20integracje.md#term-dual-write).

<a id="data-reconciliation"></a>
## Uzgodnienie danych

Reconciliation: regularne porównanie danych w dwóch systemach, wykrywające rozbieżności.

Pierwsza wzmianka: [rozdział 07](07%20Dane%20i%20integracje.md#term-data-reconciliation).

<a id="big-rewrite"></a>
## Big rewrite

Zastąpienie systemu nowym, pisanym od zera, z przełączeniem w jednym momencie.

Pierwsza wzmianka: [rozdział 08](08%20Przepisa%C4%87%20czy%20poprawia%C4%87.md#term-big-rewrite).

<a id="feature-parity"></a>
## Parytet funkcji

Wymóg, żeby nowy system robił wszystko, co stary, łącznie z funkcjami, o których nikt nie pamięta.

Pierwsza wzmianka: [rozdział 08](08%20Przepisa%C4%87%20czy%20poprawia%C4%87.md#term-feature-parity).

<a id="second-system-effect"></a>
## Efekt drugiego systemu

Skłonność do przeprojektowania następcy systemu (Fred Brooks, „The Mythical Man-Month”).

Pierwsza wzmianka: [rozdział 08](08%20Przepisa%C4%87%20czy%20poprawia%C4%87.md#term-second-system-effect).

<a id="chestertons-fence"></a>
## Płot Chestertona

Zasada: nie usuwaj czegoś, dopóki nie wiesz, dlaczego to istnieje.

Pierwsza wzmianka: [rozdział 08](08%20Przepisa%C4%87%20czy%20poprawia%C4%87.md#term-chestertons-fence).

<a id="cost-of-delay"></a>
## Koszt opóźnienia

Cost of delay: ile firma traci za każdy okres, w którym problem nie jest rozwiązany.

Pierwsza wzmianka: [rozdział 08](08%20Przepisa%C4%87%20czy%20poprawia%C4%87.md#term-cost-of-delay).

<a id="bus-factor"></a>
## Bus factor

Liczba osób, których nagłe odejście zatrzymałoby rozwój projektu.

Pierwsza wzmianka: [rozdział 09](09%20Ludzie%20i%20proces.md#term-bus-factor).

<a id="pair-programming"></a>
## Programowanie w parach

Dwie osoby pracujące nad jednym zadaniem przy jednym komputerze, na zmianę przy klawiaturze.

Pierwsza wzmianka: [rozdział 09](09%20Ludzie%20i%20proces.md#term-pair-programming).

<a id="mob-programming"></a>
## Mob programming

Cały zespół pracuje nad jednym zadaniem przy jednym ekranie.

Pierwsza wzmianka: [rozdział 09](09%20Ludzie%20i%20proces.md#term-mob-programming).

<a id="adr"></a>
## ADR

Architecture Decision Record (Michael Nygard): krótki dokument opisujący kontekst, decyzję i konsekwencje.

Pierwsza wzmianka: [rozdział 09](09%20Ludzie%20i%20proces.md#term-adr).

<a id="debt-budget"></a>
## Budżet na dług

Stały procent pojemności zespołu przeznaczony na spłatę długu technicznego, uzgodniony z biznesem.

Pierwsza wzmianka: [rozdział 09](09%20Ludzie%20i%20proces.md#term-debt-budget).
