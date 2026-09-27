# Glosariusz: Wzorce projektowe GoF w Pythonie: kreacyjne, strukturalne i behawioralne

## Spis haseł

- [ABC (klasa abstrakcyjna)](#abc-klasa-abstrakcyjna)
- [Protocol](#protocol)
- [typowanie nominalne](#typowanie-nominalne)
- [typowanie strukturalne](#typowanie-strukturalne)
- [kompozycja](#kompozycja)
- [podwójna dyspozycja](#podwójna-dyspozycja)
- [pytest](#pytest)
- [atrapa](#atrapa)
- [mock](#mock)
- [test zachowania](#test-zachowania)
- [dataclass](#dataclass)
- [decyzję](#decyzję)
- [format kalendarza](#format-kalendarza)
- [zdarzenie domenowe](#zdarzenie-domenowe)
- [byt i wartość](#byt-i-wartość)
- [głos komisji](#głos-komisji)
- [Factory Method](#factory-method)
- [funkcja fabryczna](#funkcja-fabryczna)
- [Abstract Factory](#abstract-factory)
- [rodzina produktów](#rodzina-produktów)
- [Builder](#builder)
- [interfejs płynny](#interfejs-płynny)
- [Prototype](#prototype)
- [kopia płytka](#kopia-płytka)
- [kopia głęboka](#kopia-głęboka)
- [Singleton](#singleton)
- [wstrzykiwanie zależności](#wstrzykiwanie-zależności)
- [Adapter](#adapter)
- [Bridge](#bridge)
- [Composite](#composite)
- [Decorator](#decorator)
- [Fasada](#fasada)
- [Flyweight](#flyweight)
- [stan wewnętrzny](#stan-wewnętrzny)
- [stan zewnętrzny](#stan-zewnętrzny)
- [Proxy](#proxy)
- [leniwa inicjalizacja](#leniwa-inicjalizacja)
- [łańcuch odpowiedzialności](#łańcuch-odpowiedzialności)
- [Command](#command)
- [Interpreter](#interpreter)
- [drzewo wyrażeń](#drzewo-wyrażeń)
- [teczka](#teczka)
- [Iterator](#iterator)
- [generator](#generator)
- [Mediator](#mediator)
- [Memento](#memento)
- [migawka](#migawka)
- [Observer](#observer)
- [słaba referencja](#słaba-referencja)
- [State](#state)
- [maszyna stanów](#maszyna-stanów)
- [Strategy](#strategy)
- [Template Method](#template-method)
- [hak](#hak)
- [Visitor](#visitor)

## ABC (klasa abstrakcyjna)

Klasa z modułu abc z metodami oznaczonymi @abstractmethod; nie da się utworzyć instancji, dopóki podklasa ich nie zaimplementuje.

Pierwsza wzmianka: [rozdział 01, sekcja „ABC czy Protocol”](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
Występuje w: [01 › ABC czy Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
Pytania: [1](01%20Interfejsy%20ABC%20i%20Protocol.md#1-kiedy-wybrać-abc-a-kiedy-protocol-do-zdefiniowania-kontraktu).

## Protocol

Klasa z modułu typing opisująca wymagany kształt metod; klasy spełniają ją bez dziedziczenia, a zgodność sprawdza type checker.

Pierwsza wzmianka: [rozdział 01, sekcja „ABC czy Protocol”](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
Występuje w: [01 › ABC czy Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol), [01 › Składanie zamiast dziedziczenia](01%20Interfejsy%20ABC%20i%20Protocol.md#składanie-zamiast-dziedziczenia), [03 › Adapter obcego kalendarza](03%20Tworzenie%20wniosk%C3%B3w.md#adapter-obcego-kalendarza), [03 › Bridge powiadomienia i kanału](03%20Tworzenie%20wniosk%C3%B3w.md#bridge-powiadomienia-i-kanału), [03 › Composite i teczka wniosków](03%20Tworzenie%20wniosk%C3%B3w.md#composite-i-teczka-wniosków), [04 › Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).
Pytania: [1](01%20Interfejsy%20ABC%20i%20Protocol.md#1-kiedy-wybrać-abc-a-kiedy-protocol-do-zdefiniowania-kontraktu), [3](01%20Interfejsy%20ABC%20i%20Protocol.md#3-dlaczego-składanie-obiektów-bywa-elastyczniejsze-niż-dziedziczenie-podaj-przykład-z-urzędu), [21](03%20Tworzenie%20wniosk%C3%B3w.md#21-jak-adapter-sprowadza-obcy-kalendarz-do-wspólnego-interfejsu-bez-zmiany-jego-kodu), [22](03%20Tworzenie%20wniosk%C3%B3w.md#22-jak-bridge-rozdziela-abstrakcję-powiadomienia-od-kanału-wysyłki-by-nie-mnożyć-podklas), [23](03%20Tworzenie%20wniosk%C3%B3w.md#23-jak-composite-pozwala-traktować-pojedynczy-wniosek-i-teczkę-jednakowo), [27](04%20Struktury%20wniosku.md#27-jak-proxy-kontroluje-dostęp-do-drogiego-weryfikatora-pieczątek-cache-leniwość-ochrona).

## typowanie nominalne

Podejście, w którym obiekt spełnia kontrakt tylko przez jawne dziedziczenie po nazwanym typie.

Pierwsza wzmianka: [rozdział 01, sekcja „ABC czy Protocol”](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
Występuje w: [01 › ABC czy Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
Pytania: [1](01%20Interfejsy%20ABC%20i%20Protocol.md#1-kiedy-wybrać-abc-a-kiedy-protocol-do-zdefiniowania-kontraktu).

## typowanie strukturalne

Podejście, w którym obiekt spełnia kontrakt, gdy ma wymagane metody o zgodnych sygnaturach, niezależnie od dziedziczenia.

Pierwsza wzmianka: [rozdział 01, sekcja „ABC czy Protocol”](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol).
Występuje w: [01 › ABC czy Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol), [01 › Struktura pakietu i pierwszy test](01%20Interfejsy%20ABC%20i%20Protocol.md#struktura-pakietu-i-pierwszy-test).
Pytania: [1](01%20Interfejsy%20ABC%20i%20Protocol.md#1-kiedy-wybrać-abc-a-kiedy-protocol-do-zdefiniowania-kontraktu), [7](01%20Interfejsy%20ABC%20i%20Protocol.md#7-jak-zorganizować-pakiet-urzędu-i-uruchomić-pierwszy-test-pytest-z-terminala).

## kompozycja

Technika, w której obiekt trzyma inny obiekt jako składnik i deleguje mu część pracy, zamiast dziedziczyć to zachowanie.

Pierwsza wzmianka: [rozdział 01, sekcja „Składanie zamiast dziedziczenia”](01%20Interfejsy%20ABC%20i%20Protocol.md#składanie-zamiast-dziedziczenia).
Występuje w: [01 › Składanie zamiast dziedziczenia](01%20Interfejsy%20ABC%20i%20Protocol.md#składanie-zamiast-dziedziczenia), [03 › Adapter obcego kalendarza](03%20Tworzenie%20wniosk%C3%B3w.md#adapter-obcego-kalendarza), [03 › Decorator obiektowy kontra funkcyjny](03%20Tworzenie%20wniosk%C3%B3w.md#decorator-obiektowy-kontra-funkcyjny), [04 › Łańcuch kontroli wniosku](04%20Struktury%20wniosku.md#łańcuch-kontroli-wniosku), [06 › Wszystkie wzorce w jednym przepływie](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#wszystkie-wzorce-w-jednym-przepływie).
Pytania: [3](01%20Interfejsy%20ABC%20i%20Protocol.md#3-dlaczego-składanie-obiektów-bywa-elastyczniejsze-niż-dziedziczenie-podaj-przykład-z-urzędu), [21](03%20Tworzenie%20wniosk%C3%B3w.md#21-jak-adapter-sprowadza-obcy-kalendarz-do-wspólnego-interfejsu-bez-zmiany-jego-kodu), [24](03%20Tworzenie%20wniosk%C3%B3w.md#24-czym-obiektowy-decorator-gof-różni-się-od-dekoratora-funkcji-w-pythonie), [29](04%20Struktury%20wniosku.md#29-jak-łańcuch-kontroli-przekazuje-wniosek-dalej-albo-go-zatrzymuje), [44](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#44-jak-23-wzorce-trzech-rodzin-współpracują-w-przepływie-od-wniosku-do-cofnięcia-decyzji-i-które-zastąpiłbyś-prostszym-idiomem).

## podwójna dyspozycja

Wybór wykonywanego kodu według typów dwóch obiektów naraz, uzyskiwany w Pythonie przez dwa kolejne wywołania metod z zamienionymi rolami.

Pierwsza wzmianka: [rozdział 01, sekcja „Idea podwójnej dyspozycji”](01%20Interfejsy%20ABC%20i%20Protocol.md#idea-podwójnej-dyspozycji).
Występuje w: [01 › Idea podwójnej dyspozycji](01%20Interfejsy%20ABC%20i%20Protocol.md#idea-podwójnej-dyspozycji), [01 › Koszt podwójnej dyspozycji](01%20Interfejsy%20ABC%20i%20Protocol.md#koszt-podwójnej-dyspozycji), [05 › Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach).
Pytania: [4](01%20Interfejsy%20ABC%20i%20Protocol.md#4-na-czym-polega-podwójna-dyspozycja-i-czemu-zwykłe-wywołanie-metody-jej-nie-daje), [39](05%20Przep%C5%82yw%20komisji.md#39-jak-visitor-dodaje-operacje-do-struktury-teczek-bez-zmiany-jej-klas).

## pytest

Narzędzie testowe Pythona uruchamiane z terminala: znajduje pliki test_*.py, wykonuje funkcje test_* i używa zwykłego assert.

Pierwsza wzmianka: [rozdział 01, sekcja „Struktura pakietu i pierwszy test”](01%20Interfejsy%20ABC%20i%20Protocol.md#struktura-pakietu-i-pierwszy-test).
Występuje w: [01 › Struktura pakietu i pierwszy test](01%20Interfejsy%20ABC%20i%20Protocol.md#struktura-pakietu-i-pierwszy-test), [01 › Uruchamianie pytest w terminalu](01%20Interfejsy%20ABC%20i%20Protocol.md#uruchamianie-pytest-w-terminalu).
Pytania: [7](01%20Interfejsy%20ABC%20i%20Protocol.md#7-jak-zorganizować-pakiet-urzędu-i-uruchomić-pierwszy-test-pytest-z-terminala).

## atrapa

Prosty obiekt podstawiany zamiast prawdziwej zależności, zwracający z góry ustalone odpowiedzi.

Pierwsza wzmianka: [rozdział 01, sekcja „Struktura pakietu i pierwszy test”](01%20Interfejsy%20ABC%20i%20Protocol.md#struktura-pakietu-i-pierwszy-test).
Występuje w: [01 › Struktura pakietu i pierwszy test](01%20Interfejsy%20ABC%20i%20Protocol.md#struktura-pakietu-i-pierwszy-test), [01 › Uruchamianie pytest w terminalu](01%20Interfejsy%20ABC%20i%20Protocol.md#uruchamianie-pytest-w-terminalu), [02 › Test przez interfejs, nie implementację](02%20Model%20domeny%20wniosku.md#test-przez-interfejs-nie-implementację).
Pytania: [7](01%20Interfejsy%20ABC%20i%20Protocol.md#7-jak-zorganizować-pakiet-urzędu-i-uruchomić-pierwszy-test-pytest-z-terminala), [9](02%20Model%20domeny%20wniosku.md#9-jak-napisać-test-który-sprawdza-zachowanie-wzorca-przez-jego-interfejs-a-nie-implementację).

## mock

Atrapa z biblioteki unittest.mock, która zapamiętuje swoje wywołania, więc test może sprawdzić, czy i z jakimi argumentami ją zawołano.

Pierwsza wzmianka: [rozdział 01, sekcja „Atrapa z podglądem wywołań”](01%20Interfejsy%20ABC%20i%20Protocol.md#atrapa-z-podglądem-wywołań).
Występuje w: [01 › Atrapa z podglądem wywołań](01%20Interfejsy%20ABC%20i%20Protocol.md#atrapa-z-podglądem-wywołań).
Pytania: [8](01%20Interfejsy%20ABC%20i%20Protocol.md#8-jak-w-pytest-podmienić-zależność-atrapą-i-sprawdzić-wywołanie).

## test zachowania

Test, który wywołuje publiczny interfejs i sprawdza wynik lub wyjątek, nie zależąc od budowy wnętrza obiektu.

Pierwsza wzmianka: [rozdział 02, sekcja „Test przez interfejs, nie implementację”](02%20Model%20domeny%20wniosku.md#test-przez-interfejs-nie-implementację).
Występuje w: [02 › Test przez interfejs, nie implementację](02%20Model%20domeny%20wniosku.md#test-przez-interfejs-nie-implementację).
Pytania: [9](02%20Model%20domeny%20wniosku.md#9-jak-napisać-test-który-sprawdza-zachowanie-wzorca-przez-jego-interfejs-a-nie-implementację).

## dataclass

Klasa oznaczona @dataclass, dla której Python generuje `__init__`, `__repr__` i `__eq__` z adnotacji pól.

Pierwsza wzmianka: [rozdział 02, sekcja „Model wniosku jako dataclass”](02%20Model%20domeny%20wniosku.md#model-wniosku-jako-dataclass).
Występuje w: [02 › Model wniosku jako dataclass](02%20Model%20domeny%20wniosku.md#model-wniosku-jako-dataclass), [02 › Załącznik z obcego kalendarza](02%20Model%20domeny%20wniosku.md#załącznik-z-obcego-kalendarza).
Pytania: [10](02%20Model%20domeny%20wniosku.md#10-jak-zamodelować-wniosek-o-odzyskanie-poniedziałku-jako-dataclass-i-co-decyduje-o-jego-mutowalności), [12](02%20Model%20domeny%20wniosku.md#12-czym-różnią-się-formaty-kalendarzy-załączników-i-co-je-czyni-niezgodnymi).

## decyzję

Rozstrzygnięcie komisji o wniosku (przyznana albo odrzucona), modelowane jako niezmienna wartość.

Pierwsza wzmianka: [rozdział 02, sekcja „Model wniosku jako dataclass”](02%20Model%20domeny%20wniosku.md#model-wniosku-jako-dataclass).
Występuje w: [02 › Model wniosku jako dataclass](02%20Model%20domeny%20wniosku.md#model-wniosku-jako-dataclass), [02 › Głos i decyzja komisji](02%20Model%20domeny%20wniosku.md#głos-i-decyzja-komisji), [04 › Command i cofanie decyzji](04%20Struktury%20wniosku.md#command-i-cofanie-decyzji), [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
Pytania: [10](02%20Model%20domeny%20wniosku.md#10-jak-zamodelować-wniosek-o-odzyskanie-poniedziałku-jako-dataclass-i-co-decyduje-o-jego-mutowalności), [14](02%20Model%20domeny%20wniosku.md#14-jak-zamodelować-głos-członka-komisji-i-decyzję-przyznanaodrzucona-oraz-jakie-dane-niesie-by-dało-się-ją-cofnąć), [30](04%20Struktury%20wniosku.md#30-jak-command-opakowuje-czynność-jako-obiekt-z-execute-i-undo), [31](04%20Struktury%20wniosku.md#31-jak-drzewo-wyrażeń-interpretuje-regułę-komisji-i-kiedy-lepszy-jest-zwykły-eval-free-parser-lub-funkcja).

## format kalendarza

Umowa, jak zapisać dzień jako tekst i od którego dnia liczyć tydzień; ten sam napis może w różnych formatach oznaczać różne daty.

Pierwsza wzmianka: [rozdział 02, sekcja „Załącznik z obcego kalendarza”](02%20Model%20domeny%20wniosku.md#załącznik-z-obcego-kalendarza).
Występuje w: [02 › Załącznik z obcego kalendarza](02%20Model%20domeny%20wniosku.md#załącznik-z-obcego-kalendarza).
Pytania: [12](02%20Model%20domeny%20wniosku.md#12-czym-różnią-się-formaty-kalendarzy-załączników-i-co-je-czyni-niezgodnymi).

## zdarzenie domenowe

Niezmienny zapis faktu, który zaszedł w dziedzinie, nazwany w czasie przeszłym i niosący dane potrzebne odbiorcy.

Pierwsza wzmianka: [rozdział 02, sekcja „Zdarzenia w życiu wniosku”](02%20Model%20domeny%20wniosku.md#zdarzenia-w-życiu-wniosku).
Występuje w: [02 › Zdarzenia w życiu wniosku](02%20Model%20domeny%20wniosku.md#zdarzenia-w-życiu-wniosku), [05 › Observer i subskrybenci zdarzeń](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń), [06 › Decyzja z powiadomieniami i cofaniem](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem).
Pytania: [13](02%20Model%20domeny%20wniosku.md#13-jakie-zdarzenia-zachodzą-w-życiu-wniosku-i-jakie-dane-niesie-każde-z-nich), [35](05%20Przep%C5%82yw%20komisji.md#35-jak-observer-powiadamia-subskrybentów-o-zdarzeniu-i-jak-uniknąć-wycieku-subskrypcji), [41](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#41-jak-połączyć-command-memento-i-observer-by-decyzja-wysyłała-powiadomienia-i-dała-się-cofnąć).

## byt i wartość

Byt ma tożsamość i zmienia stan w czasie; wartość jest porównywana po zawartości i niezmienna.

Pierwsza wzmianka: [rozdział 02, sekcja „Zdarzenia w życiu wniosku”](02%20Model%20domeny%20wniosku.md#zdarzenia-w-życiu-wniosku).
Występuje w: [02 › Zdarzenia w życiu wniosku](02%20Model%20domeny%20wniosku.md#zdarzenia-w-życiu-wniosku).
Pytania: [13](02%20Model%20domeny%20wniosku.md#13-jakie-zdarzenia-zachodzą-w-życiu-wniosku-i-jakie-dane-niesie-każde-z-nich).

## głos komisji

Niezmienny zapis stanowiska jednego członka komisji: kto głosował i czy za, czy przeciw.

Pierwsza wzmianka: [rozdział 02, sekcja „Głos i decyzja komisji”](02%20Model%20domeny%20wniosku.md#głos-i-decyzja-komisji).
Występuje w: [02 › Głos i decyzja komisji](02%20Model%20domeny%20wniosku.md#głos-i-decyzja-komisji), [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
Pytania: [14](02%20Model%20domeny%20wniosku.md#14-jak-zamodelować-głos-członka-komisji-i-decyzję-przyznanaodrzucona-oraz-jakie-dane-niesie-by-dało-się-ją-cofnąć), [31](04%20Struktury%20wniosku.md#31-jak-drzewo-wyrażeń-interpretuje-regułę-komisji-i-kiedy-lepszy-jest-zwykły-eval-free-parser-lub-funkcja).

## Factory Method

Wzorzec, w którym klasa bazowa woła metodę tworzącą obiekt, a podklasa decyduje, jakiej klasy on będzie.

Pierwsza wzmianka: [rozdział 02, sekcja „Factory Method dla wniosków”](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków).
Występuje w: [02 › Factory Method dla wniosków](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków), [05 › Template Method i szablon rozpatrzenia](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia).
Pytania: [15](02%20Model%20domeny%20wniosku.md#15-jak-factory-method-deleguje-wybór-klasy-wniosku-do-podklasy-i-kiedy-wystarczy-zwykła-funkcja-fabryczna), [38](05%20Przep%C5%82yw%20komisji.md#38-jak-template-method-ustala-szkielet-procedury-i-pozwala-podklasom-zmienić-kroki).

## funkcja fabryczna

Zwykła funkcja zwracająca nowy obiekt; wariant klasy można jej przekazać jako argument.

Pierwsza wzmianka: [rozdział 02, sekcja „Factory Method dla wniosków”](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków).
Występuje w: [02 › Factory Method dla wniosków](02%20Model%20domeny%20wniosku.md#factory-method-dla-wniosków).
Pytania: [15](02%20Model%20domeny%20wniosku.md#15-jak-factory-method-deleguje-wybór-klasy-wniosku-do-podklasy-i-kiedy-wystarczy-zwykła-funkcja-fabryczna).

## Abstract Factory

Obiekt z kilkoma metodami tworzącymi, z których każda zwraca inny produkt jednej rodziny; podklasa fabryki wybiera całą rodzinę naraz.

Pierwsza wzmianka: [rozdział 02, sekcja „Abstract Factory dla kalendarzy”](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
Występuje w: [02 › Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
Pytania: [16](02%20Model%20domeny%20wniosku.md#16-jak-abstract-factory-zapewnia-spójną-rodzinę-obiektów-parser-walidator-dla-jednego-kalendarza).

## rodzina produktów

Zestaw obiektów zaprojektowanych do współpracy, np. parser i walidator tego samego formatu kalendarza.

Pierwsza wzmianka: [rozdział 02, sekcja „Abstract Factory dla kalendarzy”](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
Występuje w: [02 › Abstract Factory dla kalendarzy](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy).
Pytania: [16](02%20Model%20domeny%20wniosku.md#16-jak-abstract-factory-zapewnia-spójną-rodzinę-obiektów-parser-walidator-dla-jednego-kalendarza).

## Builder

Wzorzec kreacyjny, w którym obiekt składa się z części w kolejnych krokach, a metoda build() waliduje całość i tworzy gotowy obiekt.

Pierwsza wzmianka: [rozdział 03, sekcja „Builder składa wniosek”](03%20Tworzenie%20wniosk%C3%B3w.md#builder-składa-wniosek).
Występuje w: [03 › Builder składa wniosek](03%20Tworzenie%20wniosk%C3%B3w.md#builder-składa-wniosek).
Pytania: [17](03%20Tworzenie%20wniosk%C3%B3w.md#17-jak-builder-składa-wniosek-krok-po-kroku-i-waliduje-go-w-build).

## interfejs płynny

Styl API, w którym metody zwracają self, więc wywołania łączy się w łańcuch czytany jak opis.

Pierwsza wzmianka: [rozdział 03, sekcja „Builder składa wniosek”](03%20Tworzenie%20wniosk%C3%B3w.md#builder-składa-wniosek).
Występuje w: [03 › Builder składa wniosek](03%20Tworzenie%20wniosk%C3%B3w.md#builder-składa-wniosek).
Pytania: [17](03%20Tworzenie%20wniosk%C3%B3w.md#17-jak-builder-składa-wniosek-krok-po-kroku-i-waliduje-go-w-build).

## Prototype

Wzorzec kreacyjny, w którym nowy obiekt powstaje jako kopia istniejącego, a potem zmienia się tylko różniące się pola.

Pierwsza wzmianka: [rozdział 03, sekcja „Prototype klonuje wniosek”](03%20Tworzenie%20wniosk%C3%B3w.md#prototype-klonuje-wniosek).
Występuje w: [03 › Prototype klonuje wniosek](03%20Tworzenie%20wniosk%C3%B3w.md#prototype-klonuje-wniosek).
Pytania: [18](03%20Tworzenie%20wniosk%C3%B3w.md#18-kiedy-klonowanie-przez-copydeepcopy-jest-lepsze-od-budowania-od-zera-i-jaka-jest-różnica-między-kopią-płytką-a-głęboką).

## kopia płytka

Kopia tworzona przez copy.copy: nowy obiekt, którego pola wskazują na te same obiekty co w oryginale.

Pierwsza wzmianka: [rozdział 03, sekcja „Prototype klonuje wniosek”](03%20Tworzenie%20wniosk%C3%B3w.md#prototype-klonuje-wniosek).
Występuje w: [03 › Prototype klonuje wniosek](03%20Tworzenie%20wniosk%C3%B3w.md#prototype-klonuje-wniosek).
Pytania: [18](03%20Tworzenie%20wniosk%C3%B3w.md#18-kiedy-klonowanie-przez-copydeepcopy-jest-lepsze-od-budowania-od-zera-i-jaka-jest-różnica-między-kopią-płytką-a-głęboką).

## kopia głęboka

Kopia tworzona przez copy.deepcopy: rekurencyjnie kopiuje także zawartość pól, więc jest niezależna od oryginału.

Pierwsza wzmianka: [rozdział 03, sekcja „Prototype klonuje wniosek”](03%20Tworzenie%20wniosk%C3%B3w.md#prototype-klonuje-wniosek).
Występuje w: [03 › Prototype klonuje wniosek](03%20Tworzenie%20wniosk%C3%B3w.md#prototype-klonuje-wniosek).
Pytania: [18](03%20Tworzenie%20wniosk%C3%B3w.md#18-kiedy-klonowanie-przez-copydeepcopy-jest-lepsze-od-budowania-od-zera-i-jaka-jest-różnica-między-kopią-płytką-a-głęboką).

## Singleton

Wzorzec kreacyjny gwarantujący jedną instancję klasy i globalny punkt dostępu do niej. W Pythonie zwykle realizuje go moduł albo funkcja z cache'em.

Pierwsza wzmianka: [rozdział 03, sekcja „Singleton jako konfiguracja urzędu”](03%20Tworzenie%20wniosk%C3%B3w.md#singleton-jako-konfiguracja-urzędu).
Występuje w: [03 › Singleton jako konfiguracja urzędu](03%20Tworzenie%20wniosk%C3%B3w.md#singleton-jako-konfiguracja-urzędu).
Pytania: [19](03%20Tworzenie%20wniosk%C3%B3w.md#19-jak-zapewnić-jedną-instancję-konfiguracji-i-jak-ją-izolować-w-testach).

## wstrzykiwanie zależności

Przekazywanie obiektowi tego, czego potrzebuje, z zewnątrz (argumentem), zamiast pobierania z globalnego stanu. Ułatwia podmianę w testach.

Pierwsza wzmianka: [rozdział 03, sekcja „Singleton jako konfiguracja urzędu”](03%20Tworzenie%20wniosk%C3%B3w.md#singleton-jako-konfiguracja-urzędu).
Występuje w: [03 › Singleton jako konfiguracja urzędu](03%20Tworzenie%20wniosk%C3%B3w.md#singleton-jako-konfiguracja-urzędu).
Pytania: [19](03%20Tworzenie%20wniosk%C3%B3w.md#19-jak-zapewnić-jedną-instancję-konfiguracji-i-jak-ją-izolować-w-testach).

## Adapter

Wzorzec strukturalny: klasa opakowująca obcy obiekt tak, by spełniał oczekiwany przez klienta interfejs, bez zmiany kodu obcego obiektu.

Pierwsza wzmianka: [rozdział 03, sekcja „Adapter obcego kalendarza”](03%20Tworzenie%20wniosk%C3%B3w.md#adapter-obcego-kalendarza).
Występuje w: [03 › Adapter obcego kalendarza](03%20Tworzenie%20wniosk%C3%B3w.md#adapter-obcego-kalendarza).
Pytania: [21](03%20Tworzenie%20wniosk%C3%B3w.md#21-jak-adapter-sprowadza-obcy-kalendarz-do-wspólnego-interfejsu-bez-zmiany-jego-kodu).

## Bridge

Wzorzec strukturalny rozdzielający abstrakcję od implementacji na dwie hierarchie połączone referencją, by zmieniały się niezależnie.

Pierwsza wzmianka: [rozdział 03, sekcja „Bridge powiadomienia i kanału”](03%20Tworzenie%20wniosk%C3%B3w.md#bridge-powiadomienia-i-kanału).
Występuje w: [03 › Bridge powiadomienia i kanału](03%20Tworzenie%20wniosk%C3%B3w.md#bridge-powiadomienia-i-kanału).
Pytania: [22](03%20Tworzenie%20wniosk%C3%B3w.md#22-jak-bridge-rozdziela-abstrakcję-powiadomienia-od-kanału-wysyłki-by-nie-mnożyć-podklas).

## Composite

Wzorzec strukturalny, w którym pojedynczy obiekt i kontener obiektów spełniają ten sam kontrakt, a kontener przekazuje operację swoim elementom.

Pierwsza wzmianka: [rozdział 03, sekcja „Composite i teczka wniosków”](03%20Tworzenie%20wniosk%C3%B3w.md#composite-i-teczka-wniosków).
Występuje w: [03 › Composite i teczka wniosków](03%20Tworzenie%20wniosk%C3%B3w.md#composite-i-teczka-wniosków), [05 › Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach).
Pytania: [23](03%20Tworzenie%20wniosk%C3%B3w.md#23-jak-composite-pozwala-traktować-pojedynczy-wniosek-i-teczkę-jednakowo), [39](05%20Przep%C5%82yw%20komisji.md#39-jak-visitor-dodaje-operacje-do-struktury-teczek-bez-zmiany-jej-klas).

## Decorator

Wzorzec strukturalny: obiekt opakowuje inny obiekt o tym samym kontrakcie i dodaje zachowanie przed lub po delegowanym wywołaniu.

Pierwsza wzmianka: [rozdział 03, sekcja „Decorator obiektowy kontra funkcyjny”](03%20Tworzenie%20wniosk%C3%B3w.md#decorator-obiektowy-kontra-funkcyjny).
Występuje w: [03 › Decorator obiektowy kontra funkcyjny](03%20Tworzenie%20wniosk%C3%B3w.md#decorator-obiektowy-kontra-funkcyjny), [04 › Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora), [04 › Łańcuch kontroli wniosku](04%20Struktury%20wniosku.md#łańcuch-kontroli-wniosku).
Pytania: [24](03%20Tworzenie%20wniosk%C3%B3w.md#24-czym-obiektowy-decorator-gof-różni-się-od-dekoratora-funkcji-w-pythonie), [27](04%20Struktury%20wniosku.md#27-jak-proxy-kontroluje-dostęp-do-drogiego-weryfikatora-pieczątek-cache-leniwość-ochrona), [29](04%20Struktury%20wniosku.md#29-jak-łańcuch-kontroli-przekazuje-wniosek-dalej-albo-go-zatrzymuje).

## Fasada

Wzorzec strukturalny: jeden prosty obiekt przed grupą współpracujących klas, który ukrywa kolejność wywołań i szczegóły podsystemu, nie zamykając do niego dostępu.

Pierwsza wzmianka: [rozdział 04, sekcja „Fasada jako okienko urzędu”](04%20Struktury%20wniosku.md#fasada-jako-okienko-urzędu).
Występuje w: [04 › Fasada jako okienko urzędu](04%20Struktury%20wniosku.md#fasada-jako-okienko-urzędu), [04 › Struktura wniosku przez okienko](04%20Struktury%20wniosku.md#struktura-wniosku-przez-okienko), [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji).
Pytania: [25](04%20Struktury%20wniosku.md#25-co-ukrywa-fasada-urzędu-przed-klientem-i-czego-nie-powinna-robić), [28](04%20Struktury%20wniosku.md#28-jak-złożyć-teczki-adaptery-pieczątki-i-fasadę-w-jedną-strukturę-którą-klient-obsługuje-przez-okienko), [40](05%20Przep%C5%82yw%20komisji.md#40-jak-połączyć-kontrole-stany-głosowanie-i-reguły-by-wniosek-przeszedł-do-decyzji-komisji).

## Flyweight

Wzorzec strukturalny: współdzielone, niezmienne obiekty trzymają wspólny stan, a resztę podaje kontekst przy wywołaniu.

Pierwsza wzmianka: [rozdział 04, sekcja „Flyweight i pula pieczątek”](04%20Struktury%20wniosku.md#flyweight-i-pula-pieczątek).
Występuje w: [04 › Flyweight i pula pieczątek](04%20Struktury%20wniosku.md#flyweight-i-pula-pieczątek), [04 › Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).
Pytania: [26](04%20Struktury%20wniosku.md#26-jak-flyweight-rozdziela-stan-wewnętrzny-od-zewnętrznego-i-oszczędza-pamięć), [27](04%20Struktury%20wniosku.md#27-jak-proxy-kontroluje-dostęp-do-drogiego-weryfikatora-pieczątek-cache-leniwość-ochrona).

## stan wewnętrzny

Wspólna, niezmienna część obiektu Flyweight, taka sama dla wszystkich jego użytkowników.

Pierwsza wzmianka: [rozdział 04, sekcja „Flyweight i pula pieczątek”](04%20Struktury%20wniosku.md#flyweight-i-pula-pieczątek).
Występuje w: [04 › Flyweight i pula pieczątek](04%20Struktury%20wniosku.md#flyweight-i-pula-pieczątek).
Pytania: [26](04%20Struktury%20wniosku.md#26-jak-flyweight-rozdziela-stan-wewnętrzny-od-zewnętrznego-i-oszczędza-pamięć).

## stan zewnętrzny

Część zależna od kontekstu, której Flyweight nie przechowuje, tylko dostaje ją w argumentach.

Pierwsza wzmianka: [rozdział 04, sekcja „Flyweight i pula pieczątek”](04%20Struktury%20wniosku.md#flyweight-i-pula-pieczątek).
Występuje w: [04 › Flyweight i pula pieczątek](04%20Struktury%20wniosku.md#flyweight-i-pula-pieczątek).
Pytania: [26](04%20Struktury%20wniosku.md#26-jak-flyweight-rozdziela-stan-wewnętrzny-od-zewnętrznego-i-oszczędza-pamięć).

## Proxy

Wzorzec strukturalny: obiekt o tym samym kontrakcie co prawdziwy, który kontroluje dostęp do niego (leniwość, cache, ochrona).

Pierwsza wzmianka: [rozdział 04, sekcja „Proxy jako strażnik weryfikatora”](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).
Występuje w: [04 › Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).
Pytania: [27](04%20Struktury%20wniosku.md#27-jak-proxy-kontroluje-dostęp-do-drogiego-weryfikatora-pieczątek-cache-leniwość-ochrona).

## leniwa inicjalizacja

Utworzenie drogiego obiektu dopiero przy pierwszym faktycznym użyciu, a nie z góry.

Pierwsza wzmianka: [rozdział 04, sekcja „Proxy jako strażnik weryfikatora”](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).
Występuje w: [04 › Proxy jako strażnik weryfikatora](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora).
Pytania: [27](04%20Struktury%20wniosku.md#27-jak-proxy-kontroluje-dostęp-do-drogiego-weryfikatora-pieczątek-cache-leniwość-ochrona).

## łańcuch odpowiedzialności

Wzorzec behawioralny: ciąg obiektów, z których każdy przetwarza żądanie albo przekazuje je następnemu; ogniwo może przerwać przebieg.

Pierwsza wzmianka: [rozdział 04, sekcja „Łańcuch kontroli wniosku”](04%20Struktury%20wniosku.md#łańcuch-kontroli-wniosku).
Występuje w: [04 › Łańcuch kontroli wniosku](04%20Struktury%20wniosku.md#łańcuch-kontroli-wniosku), [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji).
Pytania: [29](04%20Struktury%20wniosku.md#29-jak-łańcuch-kontroli-przekazuje-wniosek-dalej-albo-go-zatrzymuje), [40](05%20Przep%C5%82yw%20komisji.md#40-jak-połączyć-kontrole-stany-głosowanie-i-reguły-by-wniosek-przeszedł-do-decyzji-komisji).

## Command

Wzorzec behawioralny, w którym czynność jest obiektem z metodami execute i undo, trzymającym odbiorcę i dane potrzebne do cofnięcia.

Pierwsza wzmianka: [rozdział 04, sekcja „Command i cofanie decyzji”](04%20Struktury%20wniosku.md#command-i-cofanie-decyzji).
Występuje w: [04 › Command i cofanie decyzji](04%20Struktury%20wniosku.md#command-i-cofanie-decyzji), [06 › Decyzja z powiadomieniami i cofaniem](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem), [06 › Trzy wzorce i ich prostsze idiomy](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#trzy-wzorce-i-ich-prostsze-idiomy), [06 › Test end-to-end przez Okienko](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#test-end-to-end-przez-okienko).
Pytania: [30](04%20Struktury%20wniosku.md#30-jak-command-opakowuje-czynność-jako-obiekt-z-execute-i-undo), [41](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#41-jak-połączyć-command-memento-i-observer-by-decyzja-wysyłała-powiadomienia-i-dała-się-cofnąć), [42](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#42-dla-trzech-wzorców-podaj-prostszy-idiom-pythona-i-warunek-gdy-wzorzec-nadal-jest-lepszy), [43](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#43-jak-przez-fasadę-przeprowadzić-wniosek-od-złożenia-do-decyzji-i-cofnięcia-w-jednym-teście-end-to-end).

## Interpreter

Wzorzec, w którym regułę zapisuje się jako drzewo obiektów, a każdy obiekt sam oblicza swoją wartość dla danych wejściowych.

Pierwsza wzmianka: [rozdział 04, sekcja „Interpreter reguł komisji”](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
Występuje w: [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji), [05 › Strategia jako funkcja albo klasa](05%20Przep%C5%82yw%20komisji.md#strategia-jako-funkcja-albo-klasa), [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji).
Pytania: [31](04%20Struktury%20wniosku.md#31-jak-drzewo-wyrażeń-interpretuje-regułę-komisji-i-kiedy-lepszy-jest-zwykły-eval-free-parser-lub-funkcja), [37](05%20Przep%C5%82yw%20komisji.md#37-kiedy-strategy-to-klasa-a-kiedy-zwykła-funkcja-przekazana-jako-argument), [40](05%20Przep%C5%82yw%20komisji.md#40-jak-połączyć-kontrole-stany-głosowanie-i-reguły-by-wniosek-przeszedł-do-decyzji-komisji).

## drzewo wyrażeń

Struktura węzłów, w której liście to proste testy, a węzły wewnętrzne łączą je operatorami; wartość liczy się rekurencyjnie.

Pierwsza wzmianka: [rozdział 04, sekcja „Interpreter reguł komisji”](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
Występuje w: [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
Pytania: [31](04%20Struktury%20wniosku.md#31-jak-drzewo-wyrażeń-interpretuje-regułę-komisji-i-kiedy-lepszy-jest-zwykły-eval-free-parser-lub-funkcja).

## teczka

Kontener Composite z sekcji o teczce wniosków: składnik zawierający inne składniki i wykonujący operację rekurencyjnie.

Pierwsza wzmianka: [rozdział 04, sekcja „Interpreter reguł komisji”](04%20Struktury%20wniosku.md#interpreter-reguł-komisji).
Występuje w: [04 › Interpreter reguł komisji](04%20Struktury%20wniosku.md#interpreter-reguł-komisji), [04 › Iterator po teczce](04%20Struktury%20wniosku.md#iterator-po-teczce).
Pytania: [31](04%20Struktury%20wniosku.md#31-jak-drzewo-wyrażeń-interpretuje-regułę-komisji-i-kiedy-lepszy-jest-zwykły-eval-free-parser-lub-funkcja), [32](04%20Struktury%20wniosku.md#32-jak-zaimplementować-iterator-po-teczce-i-czemu-w-pythonie-zwykle-wystarcza-generator).

## Iterator

Obiekt podający elementy kolekcji po jednym, bez ujawniania jej wewnętrznej budowy; w Pythonie protokół `__iter__`/`__next__`.

Pierwsza wzmianka: [rozdział 04, sekcja „Iterator po teczce”](04%20Struktury%20wniosku.md#iterator-po-teczce).
Występuje w: [04 › Iterator po teczce](04%20Struktury%20wniosku.md#iterator-po-teczce).
Pytania: [32](04%20Struktury%20wniosku.md#32-jak-zaimplementować-iterator-po-teczce-i-czemu-w-pythonie-zwykle-wystarcza-generator).

## generator

Funkcja z `yield`, którą Python zamienia w iterator; zachowuje stan między kolejnymi wartościami.

Pierwsza wzmianka: [rozdział 04, sekcja „Iterator po teczce”](04%20Struktury%20wniosku.md#iterator-po-teczce).
Występuje w: [04 › Iterator po teczce](04%20Struktury%20wniosku.md#iterator-po-teczce).
Pytania: [32](04%20Struktury%20wniosku.md#32-jak-zaimplementować-iterator-po-teczce-i-czemu-w-pythonie-zwykle-wystarcza-generator).

## Mediator

Wzorzec behawioralny: obiekt pośredniczący, przez który komunikują się równorzędni uczestnicy, dzięki czemu nie znają się nawzajem.

Pierwsza wzmianka: [rozdział 05, sekcja „Mediator w środku komisji”](05%20Przep%C5%82yw%20komisji.md#mediator-w-środku-komisji).
Występuje w: [05 › Mediator w środku komisji](05%20Przep%C5%82yw%20komisji.md#mediator-w-środku-komisji), [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji).
Pytania: [33](05%20Przep%C5%82yw%20komisji.md#33-jak-mediator-ogranicza-bezpośrednie-powiązania-między-członkami-komisji), [40](05%20Przep%C5%82yw%20komisji.md#40-jak-połączyć-kontrole-stany-głosowanie-i-reguły-by-wniosek-przeszedł-do-decyzji-komisji).

## Memento

Wzorzec, w którym obiekt zapisuje swój stan w nieprzejrzystej migawce i sam go z niej przywraca, nie ujawniając wnętrza reszcie kodu.

Pierwsza wzmianka: [rozdział 05, sekcja „Memento jako migawka wniosku”](05%20Przep%C5%82yw%20komisji.md#memento-jako-migawka-wniosku).
Występuje w: [05 › Memento jako migawka wniosku](05%20Przep%C5%82yw%20komisji.md#memento-jako-migawka-wniosku), [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji), [06 › Decyzja z powiadomieniami i cofaniem](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem).
Pytania: [34](05%20Przep%C5%82yw%20komisji.md#34-jak-memento-zapisuje-i-przywraca-stan-wniosku-bez-łamania-enkapsulacji), [40](05%20Przep%C5%82yw%20komisji.md#40-jak-połączyć-kontrole-stany-głosowanie-i-reguły-by-wniosek-przeszedł-do-decyzji-komisji), [41](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#41-jak-połączyć-command-memento-i-observer-by-decyzja-wysyłała-powiadomienia-i-dała-się-cofnąć).

## migawka

Niezmienny pojemnik z kopią stanu obiektu, który można przechować i oddać do przywrócenia, ale nie odczytywać z zewnątrz.

Pierwsza wzmianka: [rozdział 05, sekcja „Memento jako migawka wniosku”](05%20Przep%C5%82yw%20komisji.md#memento-jako-migawka-wniosku).
Występuje w: [05 › Memento jako migawka wniosku](05%20Przep%C5%82yw%20komisji.md#memento-jako-migawka-wniosku).
Pytania: [34](05%20Przep%C5%82yw%20komisji.md#34-jak-memento-zapisuje-i-przywraca-stan-wniosku-bez-łamania-enkapsulacji).

## Observer

Wzorzec, w którym nadawca trzyma listę obserwatorów i powiadamia ich o zdarzeniu, nie znając ich konkretnych typów.

Pierwsza wzmianka: [rozdział 05, sekcja „Observer i subskrybenci zdarzeń”](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń).
Występuje w: [05 › Observer i subskrybenci zdarzeń](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń), [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji), [06 › Decyzja z powiadomieniami i cofaniem](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem), [06 › Trzy wzorce i ich prostsze idiomy](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#trzy-wzorce-i-ich-prostsze-idiomy).
Pytania: [35](05%20Przep%C5%82yw%20komisji.md#35-jak-observer-powiadamia-subskrybentów-o-zdarzeniu-i-jak-uniknąć-wycieku-subskrypcji), [40](05%20Przep%C5%82yw%20komisji.md#40-jak-połączyć-kontrole-stany-głosowanie-i-reguły-by-wniosek-przeszedł-do-decyzji-komisji), [41](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#41-jak-połączyć-command-memento-i-observer-by-decyzja-wysyłała-powiadomienia-i-dała-się-cofnąć), [42](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#42-dla-trzech-wzorców-podaj-prostszy-idiom-pythona-i-warunek-gdy-wzorzec-nadal-jest-lepszy).

## słaba referencja

Odwołanie do obiektu, które nie podtrzymuje jego życia: gdy nikt inny go nie trzyma, odśmiecacz go usuwa, a referencja zwraca None.

Pierwsza wzmianka: [rozdział 05, sekcja „Observer i subskrybenci zdarzeń”](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń).
Występuje w: [05 › Observer i subskrybenci zdarzeń](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń).
Pytania: [35](05%20Przep%C5%82yw%20komisji.md#35-jak-observer-powiadamia-subskrybentów-o-zdarzeniu-i-jak-uniknąć-wycieku-subskrypcji).

## State

Wzorzec behawioralny, w którym każdy status obiektu jest osobną klasą znającą dozwolone przejścia i własne zachowanie.

Pierwsza wzmianka: [rozdział 05, sekcja „State zamiast ifów po statusie”](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie).
Występuje w: [05 › State zamiast ifów po statusie](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie), [05 › Od kontroli do decyzji](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji), [06 › Trzy wzorce i ich prostsze idiomy](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#trzy-wzorce-i-ich-prostsze-idiomy).
Pytania: [36](05%20Przep%C5%82yw%20komisji.md#36-jak-state-usuwa-łańcuchy-if-po-statusie-i-kiedy-wystarczy-enum-ze-słownikiem-przejść), [40](05%20Przep%C5%82yw%20komisji.md#40-jak-połączyć-kontrole-stany-głosowanie-i-reguły-by-wniosek-przeszedł-do-decyzji-komisji), [42](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#42-dla-trzech-wzorców-podaj-prostszy-idiom-pythona-i-warunek-gdy-wzorzec-nadal-jest-lepszy).

## maszyna stanów

Zbiór statusów i reguł przejść między nimi.

Pierwsza wzmianka: [rozdział 05, sekcja „State zamiast ifów po statusie”](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie).
Występuje w: [05 › State zamiast ifów po statusie](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie).
Pytania: [36](05%20Przep%C5%82yw%20komisji.md#36-jak-state-usuwa-łańcuchy-if-po-statusie-i-kiedy-wystarczy-enum-ze-słownikiem-przejść).

## Strategy

Wzorzec, w którym wymienny algorytm jest przekazywany klientowi jako obiekt lub funkcja. Klient woła go przez wspólny kontrakt i nie zna wariantu.

Pierwsza wzmianka: [rozdział 05, sekcja „Strategia jako funkcja albo klasa”](05%20Przep%C5%82yw%20komisji.md#strategia-jako-funkcja-albo-klasa).
Występuje w: [05 › Strategia jako funkcja albo klasa](05%20Przep%C5%82yw%20komisji.md#strategia-jako-funkcja-albo-klasa).
Pytania: [37](05%20Przep%C5%82yw%20komisji.md#37-kiedy-strategy-to-klasa-a-kiedy-zwykła-funkcja-przekazana-jako-argument).

## Template Method

Wzorzec, w którym metoda klasy bazowej ustala kolejność kroków procedury, a wybrane kroki nadpisują podklasy.

Pierwsza wzmianka: [rozdział 05, sekcja „Template Method i szablon rozpatrzenia”](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia).
Występuje w: [05 › Template Method i szablon rozpatrzenia](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia).
Pytania: [38](05%20Przep%C5%82yw%20komisji.md#38-jak-template-method-ustala-szkielet-procedury-i-pozwala-podklasom-zmienić-kroki).

## hak

Krok szablonu z domyślnym działaniem w bazie, który podklasa może nadpisać, ale nie musi.

Pierwsza wzmianka: [rozdział 05, sekcja „Template Method i szablon rozpatrzenia”](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia).
Występuje w: [05 › Template Method i szablon rozpatrzenia](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia).
Pytania: [38](05%20Przep%C5%82yw%20komisji.md#38-jak-template-method-ustala-szkielet-procedury-i-pozwala-podklasom-zmienić-kroki).

## Visitor

Wzorzec behawioralny, w którym operacja na strukturze obiektów jest osobną klasą (wizytatorem), a elementy struktury tylko go przyjmują metodą przyjmij.

Pierwsza wzmianka: [rozdział 05, sekcja „Visitor i raporty po teczkach”](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach).
Występuje w: [05 › Visitor i raporty po teczkach](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach), [06 › Test end-to-end przez Okienko](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#test-end-to-end-przez-okienko).
Pytania: [39](05%20Przep%C5%82yw%20komisji.md#39-jak-visitor-dodaje-operacje-do-struktury-teczek-bez-zmiany-jej-klas), [43](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#43-jak-przez-fasadę-przeprowadzić-wniosek-od-złożenia-do-decyzji-i-cofnięcia-w-jednym-teście-end-to-end).
