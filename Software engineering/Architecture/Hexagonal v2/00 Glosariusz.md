# Glosariusz: Architektura heksagonalna (Ports & Adapters)

## Spis haseł

- [logika domenowa](#logika-domenowa)
- [port](#port)
- [adapter](#adapter)
- [encja](#encja)
- [obiekt wartości](#obiekt-wartości)
- [przypadek użycia](#przypadek-użycia)
- [zasada odwrócenia zależności](#zasada-odwrócenia-zależności)
- [rdzeń](#rdzeń)
- [port wejściowy (driving)](#port-wejściowy-driving)
- [port wyjściowy (driven)](#port-wyjściowy-driven)
- [klasa abstrakcyjna (ABC)](#klasa-abstrakcyjna-abc)
- [typowanie nominalne](#typowanie-nominalne)
- [typowanie strukturalne](#typowanie-strukturalne)
- [model trwałości](#model-trwałości)
- [błąd rdzenia](#błąd-rdzenia)
- [logika aplikacyjna](#logika-aplikacyjna)
- [fake](#fake)
- [port repozytorium](#port-repozytorium)
- [DAO (Data Access Object)](#dao-data-access-object)
- [obiekt wyniku](#obiekt-wyniku)
- [wstrzykiwanie zależności](#wstrzykiwanie-zależności)
- [composition root](#composition-root)
- [kontener DI](#kontener-di)
- [test kontraktowy](#test-kontraktowy)
- [Unit of Work](#unit-of-work)
- [zdarzenie domenowe](#zdarzenie-domenowe)
- [Outbox](#outbox)
- [idempotentny konsument](#idempotentny-konsument)
- [import-linter](#import-linter)
- [CQRS](#cqrs)

## logika domenowa

Reguły biznesowe systemu, np. limit jednego aktywnego wypożyczenia czy cennik, niezależne od sposobu ich wywołania i przechowywania danych.

Pierwsza wzmianka: [rozdział 01, sekcja „Problem: logika uwięziona w infrastrukturze”](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze).
Występuje w: [01 › Problem: logika uwięziona w infrastrukturze](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze), [01 › Sześciokąt to tylko metafora](01%20Podstawy%20i%20motywacja.md#sześciokąt-to-tylko-metafora), [01 › Heksagon a architektura warstwowa](01%20Podstawy%20i%20motywacja.md#heksagon-a-architektura-warstwowa), [04 › Logika domenowa a aplikacyjna](04%20Domena%20i%20warstwa%20aplikacji.md#logika-domenowa-a-aplikacyjna).
Pytania: [1](01%20Podstawy%20i%20motywacja.md#1-jaki-główny-problem-projektowy-rozwiązuje-architektura-heksagonalna), [3](01%20Podstawy%20i%20motywacja.md#3-dlaczego-sześciokąt-jest-tylko-metaforą-i-nie-oznacza-sześciu-portów), [5](01%20Podstawy%20i%20motywacja.md#5-czym-architektura-heksagonalna-różni-się-od-klasycznej-architektury-warstwowej), [18](04%20Domena%20i%20warstwa%20aplikacji.md#18-czym-różni-się-logika-domenowa-od-logiki-aplikacyjnej).

## port

Interfejs należący do rdzenia, opisujący, jak rdzeń komunikuje się z otoczeniem, bez wskazywania technologii.

Pierwsza wzmianka: [rozdział 01, sekcja „Problem: logika uwięziona w infrastrukturze”](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze).
Występuje w: [01 › Problem: logika uwięziona w infrastrukturze](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze), [01 › Wnętrze i zewnętrze heksagonu](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu), [01 › Sześciokąt to tylko metafora](01%20Podstawy%20i%20motywacja.md#sześciokąt-to-tylko-metafora), [02 › Czym jest port](02%20Porty.md#czym-jest-port), [03 › Czym jest adapter](03%20Adaptery.md#czym-jest-adapter), [07 › Unit of Work jako port](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#unit-of-work-jako-port), [07 › Asynchroniczność na brzegu, nie w domenie](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#asynchroniczność-na-brzegu-nie-w-domenie), [08 › Struktura pakietów projektu](08%20Praktyka%20i%20kompromisy.md#struktura-pakietów-projektu), [08 › Kiedy heksagon to nadmiar](08%20Praktyka%20i%20kompromisy.md#kiedy-heksagon-to-nadmiar).
Pytania: [1](01%20Podstawy%20i%20motywacja.md#1-jaki-główny-problem-projektowy-rozwiązuje-architektura-heksagonalna), [2](01%20Podstawy%20i%20motywacja.md#2-co-znajduje-się-wewnątrz-heksagonu-a-co-na-zewnątrz), [3](01%20Podstawy%20i%20motywacja.md#3-dlaczego-sześciokąt-jest-tylko-metaforą-i-nie-oznacza-sześciu-portów), [6](02%20Porty.md#6-czym-jest-port-w-architekturze-heksagonalnej), [11](03%20Adaptery.md#11-czym-jest-adapter-i-jaką-pełni-rolę-względem-portu), [35](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#35-czym-jest-wzorzec-unit-of-work-i-jak-wyrazić-go-jako-port), [40](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#40-jak-zaprojektować-porty-asynchroniczne-by-nie-wymuszać-asyncawait-w-samej-domenie), [41](08%20Praktyka%20i%20kompromisy.md#41-jak-zorganizować-strukturę-pakietów-projektu-w-pythonie-domain-application-adapters), [43](08%20Praktyka%20i%20kompromisy.md#43-kiedy-architektura-heksagonalna-jest-nadmiarowa-over-engineering).

## adapter

Kod tłumaczący konkretną technologię (HTTP, SQL, Stripe) na port lub port na technologię.

Pierwsza wzmianka: [rozdział 01, sekcja „Problem: logika uwięziona w infrastrukturze”](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze).
Występuje w: [01 › Problem: logika uwięziona w infrastrukturze](01%20Podstawy%20i%20motywacja.md#problem-logika-uwięziona-w-infrastrukturze), [01 › Wnętrze i zewnętrze heksagonu](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu), [01 › Sześciokąt to tylko metafora](01%20Podstawy%20i%20motywacja.md#sześciokąt-to-tylko-metafora), [03 › Czym jest adapter](03%20Adaptery.md#czym-jest-adapter), [04 › Port repozytorium a DAO (uzupełnienie)](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao-uzupełnienie), [06 › Testowanie endpointu HTTP](06%20Testowanie.md#testowanie-endpointu-http), [07 › Granica transakcji: use case czy adapter](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#granica-transakcji-use-case-czy-adapter), [08 › Kiedy heksagon to nadmiar](08%20Praktyka%20i%20kompromisy.md#kiedy-heksagon-to-nadmiar), [08 › Migracja monolitu krok po kroku](08%20Praktyka%20i%20kompromisy.md#migracja-monolitu-krok-po-kroku).
Pytania: [1](01%20Podstawy%20i%20motywacja.md#1-jaki-główny-problem-projektowy-rozwiązuje-architektura-heksagonalna), [2](01%20Podstawy%20i%20motywacja.md#2-co-znajduje-się-wewnątrz-heksagonu-a-co-na-zewnątrz), [3](01%20Podstawy%20i%20motywacja.md#3-dlaczego-sześciokąt-jest-tylko-metaforą-i-nie-oznacza-sześciu-portów), [11](03%20Adaptery.md#11-czym-jest-adapter-i-jaką-pełni-rolę-względem-portu), [21](04%20Domena%20i%20warstwa%20aplikacji.md#21-czym-jest-port-repozytorium-i-czym-różni-się-od-dao), [34](06%20Testowanie.md#34-jak-przetestować-adapter-wejściowy-np-endpoint-http-bez-realnej-infrastruktury), [36](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#36-gdzie-powinna-leżeć-granica-transakcji-w-use-case-czy-w-adapterze), [43](08%20Praktyka%20i%20kompromisy.md#43-kiedy-architektura-heksagonalna-jest-nadmiarowa-over-engineering), [44](08%20Praktyka%20i%20kompromisy.md#44-jak-stopniowo-wprowadzić-architekturę-heksagonalną-do-monolitu-z-logiką-w-widokach-i-modelach-orm).

## encja

Obiekt domenowy z własną tożsamością, którego stan zmienia się w czasie, np. Rental albo Bike.

Pierwsza wzmianka: [rozdział 01, sekcja „Wnętrze i zewnętrze heksagonu”](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu).
Występuje w: [01 › Wnętrze i zewnętrze heksagonu](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu), [04 › Encje bez dziedziczenia po ORM](04%20Domena%20i%20warstwa%20aplikacji.md#encje-bez-dziedziczenia-po-orm), [04 › Port repozytorium a DAO](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao).
Pytania: [2](01%20Podstawy%20i%20motywacja.md#2-co-znajduje-się-wewnątrz-heksagonu-a-co-na-zewnątrz), [20](04%20Domena%20i%20warstwa%20aplikacji.md#20-dlaczego-encje-domenowe-nie-powinny-dziedziczyć-po-modelach-orm), [21](04%20Domena%20i%20warstwa%20aplikacji.md#21-czym-jest-port-repozytorium-i-czym-różni-się-od-dao).

## obiekt wartości

Niezmienny obiekt domenowy bez tożsamości, porównywany przez wartość, np. PricingPolicy.

Pierwsza wzmianka: [rozdział 01, sekcja „Wnętrze i zewnętrze heksagonu”](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu).
Występuje w: [01 › Wnętrze i zewnętrze heksagonu](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu), [07 › Zdarzenia domenowe i port publikacji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji), [08 › Migracja monolitu krok po kroku](08%20Praktyka%20i%20kompromisy.md#migracja-monolitu-krok-po-kroku), [08 › Odczyty CQRS a porty domeny](08%20Praktyka%20i%20kompromisy.md#odczyty-cqrs-a-porty-domeny).
Pytania: [2](01%20Podstawy%20i%20motywacja.md#2-co-znajduje-się-wewnątrz-heksagonu-a-co-na-zewnątrz), [37](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#37-czym-są-zdarzenia-domenowe-i-jak-publikować-je-przez-port), [44](08%20Praktyka%20i%20kompromisy.md#44-jak-stopniowo-wprowadzić-architekturę-heksagonalną-do-monolitu-z-logiką-w-widokach-i-modelach-orm), [45](08%20Praktyka%20i%20kompromisy.md#45-czy-odczyty-w-podejściu-cqrs-muszą-przechodzić-przez-porty-domeny).

## przypadek użycia

Jeden scenariusz aplikacji, który koordynuje encje i porty, np. rozpoczęcie wypożyczenia.

Pierwsza wzmianka: [rozdział 01, sekcja „Wnętrze i zewnętrze heksagonu”](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu).
Występuje w: [01 › Wnętrze i zewnętrze heksagonu](01%20Podstawy%20i%20motywacja.md#wnętrze-i-zewnętrze-heksagonu), [01 › Sześciokąt to tylko metafora](01%20Podstawy%20i%20motywacja.md#sześciokąt-to-tylko-metafora), [02 › Czym jest port](02%20Porty.md#czym-jest-port), [03 › Adaptery wejściowe w Pythonie](03%20Adaptery.md#adaptery-wejściowe-w-pythonie), [03 › Zakres adaptera wejściowego](03%20Adaptery.md#zakres-adaptera-wejściowego), [04 › Rola use case'u w heksagonie](04%20Domena%20i%20warstwa%20aplikacji.md#rola-use-caseu-w-heksagonie), [06 › Testowanie endpointu HTTP](06%20Testowanie.md#testowanie-endpointu-http), [07 › Granica transakcji: use case czy adapter](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#granica-transakcji-use-case-czy-adapter), [07 › Asynchroniczność na brzegu, nie w domenie](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#asynchroniczność-na-brzegu-nie-w-domenie), [08 › Kiedy heksagon to nadmiar](08%20Praktyka%20i%20kompromisy.md#kiedy-heksagon-to-nadmiar), [08 › Migracja monolitu krok po kroku](08%20Praktyka%20i%20kompromisy.md#migracja-monolitu-krok-po-kroku).
Pytania: [2](01%20Podstawy%20i%20motywacja.md#2-co-znajduje-się-wewnątrz-heksagonu-a-co-na-zewnątrz), [3](01%20Podstawy%20i%20motywacja.md#3-dlaczego-sześciokąt-jest-tylko-metaforą-i-nie-oznacza-sześciu-portów), [6](02%20Porty.md#6-czym-jest-port-w-architekturze-heksagonalnej), [12](03%20Adaptery.md#12-podaj-przykłady-adapterów-wejściowych-w-backendzie-pythona), [14](03%20Adaptery.md#14-za-co-odpowiada-adapter-wejściowy-a-czego-nie-powinien-robić), [17](04%20Domena%20i%20warstwa%20aplikacji.md#17-jaką-rolę-pełni-use-case-serwis-aplikacyjny-w-heksagonie), [34](06%20Testowanie.md#34-jak-przetestować-adapter-wejściowy-np-endpoint-http-bez-realnej-infrastruktury), [36](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#36-gdzie-powinna-leżeć-granica-transakcji-w-use-case-czy-w-adapterze), [40](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#40-jak-zaprojektować-porty-asynchroniczne-by-nie-wymuszać-asyncawait-w-samej-domenie), [43](08%20Praktyka%20i%20kompromisy.md#43-kiedy-architektura-heksagonalna-jest-nadmiarowa-over-engineering), [44](08%20Praktyka%20i%20kompromisy.md#44-jak-stopniowo-wprowadzić-architekturę-heksagonalną-do-monolitu-z-logiką-w-widokach-i-modelach-orm).

## zasada odwrócenia zależności

Moduły wysokiego poziomu nie zależą od modułów niskiego poziomu; oba zależą od abstrakcji, którą posiada moduł wysokiego poziomu. W heksagonie tą abstrakcją jest port.

Pierwsza wzmianka: [rozdział 01, sekcja „Kierunek zależności: do rdzenia”](01%20Podstawy%20i%20motywacja.md#kierunek-zależności-do-rdzenia).
Występuje w: [01 › Kierunek zależności: do rdzenia](01%20Podstawy%20i%20motywacja.md#kierunek-zależności-do-rdzenia), [02 › Czym jest port](02%20Porty.md#czym-jest-port), [02 › Właściciel interfejsu portu](02%20Porty.md#właściciel-interfejsu-portu), [04 › Use case i porty wyjściowe](04%20Domena%20i%20warstwa%20aplikacji.md#use-case-i-porty-wyjściowe), [05 › DI a porty i adaptery](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#di-a-porty-i-adaptery).
Pytania: [4](01%20Podstawy%20i%20motywacja.md#4-jaki-kierunek-powinny-mieć-zależności-między-rdzeniem-a-infrastrukturą), [6](02%20Porty.md#6-czym-jest-port-w-architekturze-heksagonalnej), [10](02%20Porty.md#10-kto-powinien-być-właścicielem-interfejsu-portu-rdzeń-czy-adapter), [19](04%20Domena%20i%20warstwa%20aplikacji.md#19-jak-use-case-zależy-od-portów-wyjściowych), [23](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#23-jak-wstrzykiwanie-zależności-wiąże-się-z-portami-i-adapterami).

## rdzeń

Wnętrze heksagonu: logika domenowa, encje, obiekty wartości, przypadki użycia i porty. Nie zależy od żadnej technologii; to na niego wskazują importy adapterów.

Pierwsza wzmianka: [rozdział 01, sekcja „Heksagon a architektura warstwowa”](01%20Podstawy%20i%20motywacja.md#heksagon-a-architektura-warstwowa).
Występuje w: [01 › Heksagon a architektura warstwowa](01%20Podstawy%20i%20motywacja.md#heksagon-a-architektura-warstwowa), [02 › Czym jest port](02%20Porty.md#czym-jest-port), [03 › Mapowanie modeli zewnętrznych](03%20Adaptery.md#mapowanie-modeli-zewnętrznych), [08 › Struktura pakietów projektu](08%20Praktyka%20i%20kompromisy.md#struktura-pakietów-projektu), [08 › Migracja monolitu krok po kroku](08%20Praktyka%20i%20kompromisy.md#migracja-monolitu-krok-po-kroku).
Pytania: [5](01%20Podstawy%20i%20motywacja.md#5-czym-architektura-heksagonalna-różni-się-od-klasycznej-architektury-warstwowej), [6](02%20Porty.md#6-czym-jest-port-w-architekturze-heksagonalnej), [15](03%20Adaptery.md#15-dlaczego-adapter-powinien-mapować-modele-zewnętrzne-orm-dto-na-obiekty-domenowe), [41](08%20Praktyka%20i%20kompromisy.md#41-jak-zorganizować-strukturę-pakietów-projektu-w-pythonie-domain-application-adapters), [44](08%20Praktyka%20i%20kompromisy.md#44-jak-stopniowo-wprowadzić-architekturę-heksagonalną-do-monolitu-z-logiką-w-widokach-i-modelach-orm).

## port wejściowy (driving)

Port, przez który świat zewnętrzny steruje rdzeniem; implementuje go rdzeń (przypadek użycia), a woła adapter.

Pierwsza wzmianka: [rozdział 02, sekcja „Porty wejściowe i wyjściowe”](02%20Porty.md#porty-wejściowe-i-wyjściowe).
Występuje w: [02 › Porty wejściowe i wyjściowe](02%20Porty.md#porty-wejściowe-i-wyjściowe), [03 › Czym jest adapter](03%20Adaptery.md#czym-jest-adapter), [03 › Adaptery wejściowe w Pythonie](03%20Adaptery.md#adaptery-wejściowe-w-pythonie), [03 › Zakres adaptera wejściowego](03%20Adaptery.md#zakres-adaptera-wejściowego), [04 › Rola use case'u w heksagonie](04%20Domena%20i%20warstwa%20aplikacji.md#rola-use-caseu-w-heksagonie), [04 › Use case zwraca wynik, nie HTTP](04%20Domena%20i%20warstwa%20aplikacji.md#use-case-zwraca-wynik-nie-http), [08 › Odczyty CQRS a porty domeny](08%20Praktyka%20i%20kompromisy.md#odczyty-cqrs-a-porty-domeny).
Pytania: [7](02%20Porty.md#7-czym-różnią-się-porty-wejściowe-driving-od-wyjściowych-driven), [11](03%20Adaptery.md#11-czym-jest-adapter-i-jaką-pełni-rolę-względem-portu), [12](03%20Adaptery.md#12-podaj-przykłady-adapterów-wejściowych-w-backendzie-pythona), [14](03%20Adaptery.md#14-za-co-odpowiada-adapter-wejściowy-a-czego-nie-powinien-robić), [17](04%20Domena%20i%20warstwa%20aplikacji.md#17-jaką-rolę-pełni-use-case-serwis-aplikacyjny-w-heksagonie), [22](04%20Domena%20i%20warstwa%20aplikacji.md#22-dlaczego-use-case-powinien-zwracać-obiekty-domenowe-lub-dedykowane-wyniki-a-nie-odpowiedzi-http), [45](08%20Praktyka%20i%20kompromisy.md#45-czy-odczyty-w-podejściu-cqrs-muszą-przechodzić-przez-porty-domeny).

## port wyjściowy (driven)

Port, przez który rdzeń korzysta ze świata zewnętrznego; definiuje go rdzeń, a implementuje adapter.

Pierwsza wzmianka: [rozdział 02, sekcja „Porty wejściowe i wyjściowe”](02%20Porty.md#porty-wejściowe-i-wyjściowe).
Występuje w: [02 › Porty wejściowe i wyjściowe](02%20Porty.md#porty-wejściowe-i-wyjściowe), [03 › Czym jest adapter](03%20Adaptery.md#czym-jest-adapter), [03 › Adaptery wyjściowe w Pythonie](03%20Adaptery.md#adaptery-wyjściowe-w-pythonie), [04 › Rola use case'u w heksagonie](04%20Domena%20i%20warstwa%20aplikacji.md#rola-use-caseu-w-heksagonie), [04 › Use case i porty wyjściowe](04%20Domena%20i%20warstwa%20aplikacji.md#use-case-i-porty-wyjściowe), [04 › Port repozytorium a DAO](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao), [04 › Port repozytorium a DAO (uzupełnienie)](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao-uzupełnienie), [06 › Testy use case'ów bez infrastruktury](06%20Testowanie.md#testy-use-caseów-bez-infrastruktury), [06 › Kiedy fake, a kiedy mock](06%20Testowanie.md#kiedy-fake-a-kiedy-mock), [07 › Zdarzenia domenowe i port publikacji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji), [07 › Asynchroniczność na brzegu, nie w domenie](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#asynchroniczność-na-brzegu-nie-w-domenie).
Pytania: [7](02%20Porty.md#7-czym-różnią-się-porty-wejściowe-driving-od-wyjściowych-driven), [11](03%20Adaptery.md#11-czym-jest-adapter-i-jaką-pełni-rolę-względem-portu), [13](03%20Adaptery.md#13-podaj-przykłady-adapterów-wyjściowych-w-backendzie-pythona), [17](04%20Domena%20i%20warstwa%20aplikacji.md#17-jaką-rolę-pełni-use-case-serwis-aplikacyjny-w-heksagonie), [19](04%20Domena%20i%20warstwa%20aplikacji.md#19-jak-use-case-zależy-od-portów-wyjściowych), [21](04%20Domena%20i%20warstwa%20aplikacji.md#21-czym-jest-port-repozytorium-i-czym-różni-się-od-dao), [29](06%20Testowanie.md#29-jak-architektura-heksagonalna-ułatwia-testy-jednostkowe-use-caseów), [31](06%20Testowanie.md#31-kiedy-preferować-fakei-zamiast-unittestmock), [37](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#37-czym-są-zdarzenia-domenowe-i-jak-publikować-je-przez-port), [40](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#40-jak-zaprojektować-porty-asynchroniczne-by-nie-wymuszać-asyncawait-w-samej-domenie).

## klasa abstrakcyjna (ABC)

Klasa dziedzicząca po abc.ABC, z metodami oznaczonymi @abstractmethod; nie można jej instancjonować, dopóki podklasa nie zaimplementuje wszystkich metod abstrakcyjnych.

Pierwsza wzmianka: [rozdział 02, sekcja „Port jako klasa ABC”](02%20Porty.md#port-jako-klasa-abc).
Występuje w: [02 › Port jako klasa ABC](02%20Porty.md#port-jako-klasa-abc).
Pytania: [8](02%20Porty.md#8-jak-zdefiniować-port-w-pythonie-za-pomocą-abcabc).

## typowanie nominalne

Zgodność typów wynika z jawnej deklaracji dziedziczenia, a nie z samego kształtu metod klasy.

Pierwsza wzmianka: [rozdział 02, sekcja „Port jako klasa ABC”](02%20Porty.md#port-jako-klasa-abc).
Występuje w: [02 › Port jako klasa ABC](02%20Porty.md#port-jako-klasa-abc).
Pytania: [8](02%20Porty.md#8-jak-zdefiniować-port-w-pythonie-za-pomocą-abcabc).

## typowanie strukturalne

Zgodność typu z interfejsem wynika z posiadania wymaganych metod o pasujących sygnaturach, a nie z jawnej deklaracji dziedziczenia.

Pierwsza wzmianka: [rozdział 02, sekcja „Protocol zamiast ABC”](02%20Porty.md#protocol-zamiast-abc).
Występuje w: [02 › Protocol zamiast ABC](02%20Porty.md#protocol-zamiast-abc).
Pytania: [9](02%20Porty.md#9-jakie-zalety-ma-typingprotocol-względem-abc-przy-definiowaniu-portów).

## model trwałości

Klasa (np. wiersz ORM) opisująca, jak dane są zapisane w bazie; jest kształtowana przez schemat i technologię, a nie przez domenę.

Pierwsza wzmianka: [rozdział 03, sekcja „Mapowanie modeli zewnętrznych”](03%20Adaptery.md#mapowanie-modeli-zewnętrznych).
Występuje w: [03 › Mapowanie modeli zewnętrznych](03%20Adaptery.md#mapowanie-modeli-zewnętrznych), [04 › Encje bez dziedziczenia po ORM](04%20Domena%20i%20warstwa%20aplikacji.md#encje-bez-dziedziczenia-po-orm).
Pytania: [15](03%20Adaptery.md#15-dlaczego-adapter-powinien-mapować-modele-zewnętrzne-orm-dto-na-obiekty-domenowe), [20](04%20Domena%20i%20warstwa%20aplikacji.md#20-dlaczego-encje-domenowe-nie-powinny-dziedziczyć-po-modelach-orm).

## błąd rdzenia

Wyjątek zdefiniowany w rdzeniu obok portu, nazwany według znaczenia dla domeny, a nie technologii. Adapter rzuca go w miejsce wyjątków biblioteki.

Pierwsza wzmianka: [rozdział 03, sekcja „Tłumaczenie wyjątków w adapterze”](03%20Adaptery.md#tłumaczenie-wyjątków-w-adapterze).
Występuje w: [03 › Tłumaczenie wyjątków w adapterze](03%20Adaptery.md#tłumaczenie-wyjątków-w-adapterze), [04 › Use case zwraca wynik, nie HTTP](04%20Domena%20i%20warstwa%20aplikacji.md#use-case-zwraca-wynik-nie-http).
Pytania: [16](03%20Adaptery.md#16-jak-adapter-powinien-tłumaczyć-wyjątki-technologii-na-wyjątki-zrozumiałe-dla-rdzenia), [22](04%20Domena%20i%20warstwa%20aplikacji.md#22-dlaczego-use-case-powinien-zwracać-obiekty-domenowe-lub-dedykowane-wyniki-a-nie-odpowiedzi-http).

## logika aplikacyjna

Koordynacja jednego scenariusza: pobranie danych przez porty, wywołanie reguł domenowych w określonej kolejności, zapis i skutki uboczne. Nie definiuje reguł biznesu, tylko ich użycie.

Pierwsza wzmianka: [rozdział 04, sekcja „Logika domenowa a aplikacyjna”](04%20Domena%20i%20warstwa%20aplikacji.md#logika-domenowa-a-aplikacyjna).
Występuje w: [04 › Logika domenowa a aplikacyjna](04%20Domena%20i%20warstwa%20aplikacji.md#logika-domenowa-a-aplikacyjna).
Pytania: [18](04%20Domena%20i%20warstwa%20aplikacji.md#18-czym-różni-się-logika-domenowa-od-logiki-aplikacyjnej).

## fake

Prosta, działająca implementacja portu, np. w pamięci, podstawiana w testach zamiast prawdziwego adaptera.

Pierwsza wzmianka: [rozdział 04, sekcja „Use case i porty wyjściowe”](04%20Domena%20i%20warstwa%20aplikacji.md#use-case-i-porty-wyjściowe).
Występuje w: [04 › Use case i porty wyjściowe](04%20Domena%20i%20warstwa%20aplikacji.md#use-case-i-porty-wyjściowe), [05 › DI a porty i adaptery](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#di-a-porty-i-adaptery), [05 › Wstrzykiwanie przez konstruktor](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#wstrzykiwanie-przez-konstruktor), [06 › Testy use case'ów bez infrastruktury](06%20Testowanie.md#testy-use-caseów-bez-infrastruktury), [06 › Fake a mock](06%20Testowanie.md#fake-a-mock), [06 › Testy kontraktowe portów](06%20Testowanie.md#testy-kontraktowe-portów).
Pytania: [19](04%20Domena%20i%20warstwa%20aplikacji.md#19-jak-use-case-zależy-od-portów-wyjściowych), [23](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#23-jak-wstrzykiwanie-zależności-wiąże-się-z-portami-i-adapterami), [25](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#25-jak-wstrzykiwać-zależności-przez-konstruktor-bez-użycia-frameworka-di), [29](06%20Testowanie.md#29-jak-architektura-heksagonalna-ułatwia-testy-jednostkowe-use-caseów), [30](06%20Testowanie.md#30-czym-jest-fake-adapter-in-memory-i-czym-różni-się-od-mocka), [33](06%20Testowanie.md#33-czym-są-testy-kontraktowe-portów-i-jak-uruchomić-ten-sam-zestaw-na-fakeu-i-prawdziwym-adapterze-w-pytest).

## port repozytorium

Port wyjściowy w rdzeniu, który udostępnia encje jak kolekcję w pamięci (dodaj, znajdź) i ukrywa sposób ich przechowywania.

Pierwsza wzmianka: [rozdział 04, sekcja „Port repozytorium a DAO”](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao).
Występuje w: [04 › Port repozytorium a DAO](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao), [04 › Port repozytorium a DAO (uzupełnienie)](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao-uzupełnienie), [06 › Testy kontraktowe portów](06%20Testowanie.md#testy-kontraktowe-portów), [07 › Unit of Work jako port](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#unit-of-work-jako-port), [08 › Migracja monolitu krok po kroku](08%20Praktyka%20i%20kompromisy.md#migracja-monolitu-krok-po-kroku), [08 › Odczyty CQRS a porty domeny](08%20Praktyka%20i%20kompromisy.md#odczyty-cqrs-a-porty-domeny).
Pytania: [21](04%20Domena%20i%20warstwa%20aplikacji.md#21-czym-jest-port-repozytorium-i-czym-różni-się-od-dao), [33](06%20Testowanie.md#33-czym-są-testy-kontraktowe-portów-i-jak-uruchomić-ten-sam-zestaw-na-fakeu-i-prawdziwym-adapterze-w-pytest), [35](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#35-czym-jest-wzorzec-unit-of-work-i-jak-wyrazić-go-jako-port), [44](08%20Praktyka%20i%20kompromisy.md#44-jak-stopniowo-wprowadzić-architekturę-heksagonalną-do-monolitu-z-logiką-w-widokach-i-modelach-orm), [45](08%20Praktyka%20i%20kompromisy.md#45-czy-odczyty-w-podejściu-cqrs-muszą-przechodzić-przez-porty-domeny).

## DAO (Data Access Object)

Obiekt opakowujący dostęp do jednej tabeli lub źródła danych, zwykle z operacjami CRUD na wierszach; jego kształt wyznacza schemat, nie domena.

Pierwsza wzmianka: [rozdział 04, sekcja „Port repozytorium a DAO”](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao).
Występuje w: [04 › Port repozytorium a DAO](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao), [04 › Port repozytorium a DAO (uzupełnienie)](04%20Domena%20i%20warstwa%20aplikacji.md#port-repozytorium-a-dao-uzupełnienie).
Pytania: [21](04%20Domena%20i%20warstwa%20aplikacji.md#21-czym-jest-port-repozytorium-i-czym-różni-się-od-dao).

## obiekt wyniku

Niezmienna struktura w rdzeniu opisująca rezultat scenariusza w języku domeny, gdy nie mieści się on w jednej encji ani wartości.

Pierwsza wzmianka: [rozdział 04, sekcja „Use case zwraca wynik, nie HTTP”](04%20Domena%20i%20warstwa%20aplikacji.md#use-case-zwraca-wynik-nie-http).
Występuje w: [04 › Use case zwraca wynik, nie HTTP](04%20Domena%20i%20warstwa%20aplikacji.md#use-case-zwraca-wynik-nie-http).
Pytania: [22](04%20Domena%20i%20warstwa%20aplikacji.md#22-dlaczego-use-case-powinien-zwracać-obiekty-domenowe-lub-dedykowane-wyniki-a-nie-odpowiedzi-http).

## wstrzykiwanie zależności

Technika, w której obiekt dostaje potrzebne zależności z zewnątrz (np. przez konstruktor), zamiast samodzielnie je tworzyć.

Pierwsza wzmianka: [rozdział 05, sekcja „DI a porty i adaptery”](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#di-a-porty-i-adaptery).
Występuje w: [05 › DI a porty i adaptery](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#di-a-porty-i-adaptery), [05 › FastAPI Depends w okablowaniu](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#fastapi-depends-w-okablowaniu).
Pytania: [23](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#23-jak-wstrzykiwanie-zależności-wiąże-się-z-portami-i-adapterami), [26](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#26-jak-fastapi-depends-pomaga-wiązać-adaptery-i-jakie-ryzyko-niesie-jego-użycie-w-rdzeniu).

## composition root

Jedno miejsce w aplikacji, na jej krawędzi, w którym tworzy się adaptery i przypadki użycia oraz łączy je w całość.

Pierwsza wzmianka: [rozdział 05, sekcja „DI a porty i adaptery”](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#di-a-porty-i-adaptery).
Występuje w: [05 › DI a porty i adaptery](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#di-a-porty-i-adaptery), [05 › Composition root: gdzie go umieścić](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#composition-root-gdzie-go-umieścić), [05 › Wstrzykiwanie przez konstruktor](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#wstrzykiwanie-przez-konstruktor), [05 › Kontener DI czy ręczne okablowanie](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#kontener-di-czy-ręczne-okablowanie), [08 › Struktura pakietów projektu](08%20Praktyka%20i%20kompromisy.md#struktura-pakietów-projektu).
Pytania: [23](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#23-jak-wstrzykiwanie-zależności-wiąże-się-z-portami-i-adapterami), [24](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#24-czym-jest-composition-root-i-gdzie-go-umieścić-w-aplikacji-w-pythonie), [25](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#25-jak-wstrzykiwać-zależności-przez-konstruktor-bez-użycia-frameworka-di), [27](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#27-kiedy-warto-użyć-kontenera-di-zamiast-ręcznego-okablowania), [41](08%20Praktyka%20i%20kompromisy.md#41-jak-zorganizować-strukturę-pakietów-projektu-w-pythonie-domain-application-adapters).

## kontener DI

Narzędzie, które automatycznie tworzy obiekty i rozwiązuje ich zależności na podstawie konfiguracji lub typów.

Pierwsza wzmianka: [rozdział 05, sekcja „Kontener DI czy ręczne okablowanie”](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#kontener-di-czy-ręczne-okablowanie).
Występuje w: [05 › Kontener DI czy ręczne okablowanie](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#kontener-di-czy-ręczne-okablowanie).
Pytania: [27](05%20Wstrzykiwanie%20zale%C5%BCno%C5%9Bci%20i%20kompozycja.md#27-kiedy-warto-użyć-kontenera-di-zamiast-ręcznego-okablowania).

## test kontraktowy

Zestaw testów opisujący zachowanie portu, uruchamiany na każdej jego implementacji (fake'u i prawdziwym adapterze), by potwierdzić, że zachowują się tak samo.

Pierwsza wzmianka: [rozdział 06, sekcja „Fake a mock”](06%20Testowanie.md#fake-a-mock).
Występuje w: [06 › Fake a mock](06%20Testowanie.md#fake-a-mock), [06 › Kiedy fake, a kiedy mock](06%20Testowanie.md#kiedy-fake-a-kiedy-mock), [06 › Testowanie adaptera repozytorium SQL](06%20Testowanie.md#testowanie-adaptera-repozytorium-sql), [06 › Testy kontraktowe portów](06%20Testowanie.md#testy-kontraktowe-portów).
Pytania: [30](06%20Testowanie.md#30-czym-jest-fake-adapter-in-memory-i-czym-różni-się-od-mocka), [31](06%20Testowanie.md#31-kiedy-preferować-fakei-zamiast-unittestmock), [32](06%20Testowanie.md#32-jak-testować-adapter-wyjściowy-np-repozytorium-sql), [33](06%20Testowanie.md#33-czym-są-testy-kontraktowe-portów-i-jak-uruchomić-ten-sam-zestaw-na-fakeu-i-prawdziwym-adapterze-w-pytest).

## Unit of Work

Wzorzec grupujący zmiany w jedną transakcję i zatwierdzający je razem albo wcale; w heksagonie wyrażany jako port wyjściowy.

Pierwsza wzmianka: [rozdział 07, sekcja „Unit of Work jako port”](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#unit-of-work-jako-port).
Występuje w: [07 › Unit of Work jako port](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#unit-of-work-jako-port), [07 › Zdarzenia domenowe i port publikacji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji), [08 › Odczyty CQRS a porty domeny](08%20Praktyka%20i%20kompromisy.md#odczyty-cqrs-a-porty-domeny).
Pytania: [35](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#35-czym-jest-wzorzec-unit-of-work-i-jak-wyrazić-go-jako-port), [37](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#37-czym-są-zdarzenia-domenowe-i-jak-publikować-je-przez-port), [45](08%20Praktyka%20i%20kompromisy.md#45-czy-odczyty-w-podejściu-cqrs-muszą-przechodzić-przez-porty-domeny).

## zdarzenie domenowe

Niezmienny fakt z przeszłości istotny dla biznesu, np. RentalFinished, publikowany przez rdzeń przez port.

Pierwsza wzmianka: [rozdział 07, sekcja „Zdarzenia domenowe i port publikacji”](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji).
Występuje w: [07 › Zdarzenia domenowe i port publikacji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji), [07 › Asynchroniczność na brzegu, nie w domenie](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#asynchroniczność-na-brzegu-nie-w-domenie).
Pytania: [37](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#37-czym-są-zdarzenia-domenowe-i-jak-publikować-je-przez-port), [40](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#40-jak-zaprojektować-porty-asynchroniczne-by-nie-wymuszać-asyncawait-w-samej-domenie).

## Outbox

Wzorzec zapisujący zdarzenia w tej samej transakcji co zmiany danych, a wysyłanego do brokera osobno, by nie zgubić ani nie rozjechać zdarzeń.

Pierwsza wzmianka: [rozdział 07, sekcja „Zdarzenia domenowe i port publikacji”](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji).
Występuje w: [07 › Zdarzenia domenowe i port publikacji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#zdarzenia-domenowe-i-port-publikacji), [07 › Outbox: zdarzenia w tej samej transakcji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#outbox-zdarzenia-w-tej-samej-transakcji), [07 › Asynchroniczność na brzegu, nie w domenie](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#asynchroniczność-na-brzegu-nie-w-domenie).
Pytania: [37](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#37-czym-są-zdarzenia-domenowe-i-jak-publikować-je-przez-port), [38](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#38-czym-jest-wzorzec-outbox-i-jaki-problem-rozwiązuje), [40](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#40-jak-zaprojektować-porty-asynchroniczne-by-nie-wymuszać-asyncawait-w-samej-domenie).

## idempotentny konsument

Konsument, który wielokrotne dostarczenie tej samej wiadomości przetwarza z efektem takim jak jednokrotne.

Pierwsza wzmianka: [rozdział 07, sekcja „Outbox: zdarzenia w tej samej transakcji”](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#outbox-zdarzenia-w-tej-samej-transakcji).
Występuje w: [07 › Outbox: zdarzenia w tej samej transakcji](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#outbox-zdarzenia-w-tej-samej-transakcji), [07 › Idempotentny konsument wiadomości](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#idempotentny-konsument-wiadomości).
Pytania: [38](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#38-czym-jest-wzorzec-outbox-i-jaki-problem-rozwiązuje), [39](07%20Transakcje%2C%20zdarzenia%20i%20asynchroniczno%C5%9B%C4%87.md#39-jak-zapewnić-idempotentność-w-adapterze-wejściowym-konsumującym-wiadomości).

## import-linter

Narzędzie sprawdzające w CI, czy importy między pakietami zgadzają się z zadeklarowanymi kontraktami, np. że domena nie importuje adapterów.

Pierwsza wzmianka: [rozdział 08, sekcja „Struktura pakietów projektu”](08%20Praktyka%20i%20kompromisy.md#struktura-pakietów-projektu).
Występuje w: [08 › Struktura pakietów projektu](08%20Praktyka%20i%20kompromisy.md#struktura-pakietów-projektu), [08 › Wymuszanie kierunku importów](08%20Praktyka%20i%20kompromisy.md#wymuszanie-kierunku-importów), [08 › Migracja monolitu krok po kroku](08%20Praktyka%20i%20kompromisy.md#migracja-monolitu-krok-po-kroku), [08 › Odczyty CQRS a porty domeny](08%20Praktyka%20i%20kompromisy.md#odczyty-cqrs-a-porty-domeny).
Pytania: [41](08%20Praktyka%20i%20kompromisy.md#41-jak-zorganizować-strukturę-pakietów-projektu-w-pythonie-domain-application-adapters), [42](08%20Praktyka%20i%20kompromisy.md#42-jak-automatycznie-wymusić-kierunek-zależności-np-za-pomocą-import-linter), [44](08%20Praktyka%20i%20kompromisy.md#44-jak-stopniowo-wprowadzić-architekturę-heksagonalną-do-monolitu-z-logiką-w-widokach-i-modelach-orm), [45](08%20Praktyka%20i%20kompromisy.md#45-czy-odczyty-w-podejściu-cqrs-muszą-przechodzić-przez-porty-domeny).

## CQRS

Podział modelu na zapisy (komendy) i odczyty (zapytania), które mogą korzystać z osobnych ścieżek i modeli.

Pierwsza wzmianka: [rozdział 08, sekcja „Odczyty CQRS a porty domeny”](08%20Praktyka%20i%20kompromisy.md#odczyty-cqrs-a-porty-domeny).
Występuje w: [08 › Odczyty CQRS a porty domeny](08%20Praktyka%20i%20kompromisy.md#odczyty-cqrs-a-porty-domeny).
Pytania: [45](08%20Praktyka%20i%20kompromisy.md#45-czy-odczyty-w-podejściu-cqrs-muszą-przechodzić-przez-porty-domeny).
