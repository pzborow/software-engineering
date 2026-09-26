# Krok 1059 · autor_dodatków

Węzeł: `layers` · dział: 9 · pytanie: 54 · próba: —

## Prompt

````text
Dodajesz opcjonalne dodatki do sekcji tutorialu: Programowanie od podstaw.
Czytelnik: osoba spoza IT, poziom: początkujący.

Dodatki nie są potrzebne do zrozumienia sekcji; są dla przyjemności i pamięci. Każdy moduł ma cel: około tylu wpisów na dział, ile wynosi jego limit, rozłożonych na sekcje. Dodaj wpis, gdy ta sekcja daje dobrą okazję; kod pilnuje odstępów i limitów, weryfikator jakości. Nie wymyślaj na siłę: słaby dodatek zostanie odrzucony.
Każdy dodatek musi wynikać z treści TEJ sekcji i być poprawny: logicznie spójny, zgodny z faktami.
Nazwy z kodu pisz w backtickach.

Włączone moduły:
- module="dowcipy" (Z przymrużeniem oka): krótki żart, gra słów albo zabawna puenta o pojęciu z tej sekcji, najlepiej pomagająca je zapamiętać; 1-2 zdania. Ton dopasuj do czytelnika. Bez żartów z ludzi i grup. (w dziale jest już 1 z 2, zostało sekcji: 1).
- module="dygresje" (Na marginesie): ciekawostka, historia albo „a gdyby…” związane z sekcją; 2-4 zdania. Tylko gdy wnosi coś spoza głównego toku i nie jest potrzebna do zrozumienia sekcji. (w dziale jest już 0 z 2, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji). Podaj w sources wiarygodne źródło (encyklopedia, publikacja, oficjalna strona) z adresem; bez źródła nie dodawaj.
- module="dykteryjki" (Z życia wzięte): krótka historia z pracy opowiedziana w pierwszej osobie przez narratora z ustawień: realistyczna sytuacja, w której pojęcie z tej sekcji miało znaczenie, jaki był skutek i czego nauczyła; 3-5 zdań. To ilustracja typowej sytuacji, nie reportaż: bez nazw firm, ludzi i dat. (w dziale jest już 1 z 2, zostało sekcji: 1). Ustawienia: narrator: doświadczony Python developer, kilkanaście lat w projektach backendowych i automatyzacji; ton: poważny, rzeczowy, bez żartów.
- module="rysunki" (Ilustracja): pomysł na zabawny, prosty rysunek oparty na metaforze z tej sekcji. body: prompt dla generatora obrazów (scena, postacie, co ma być widać, bez tekstu na obrazku); caption: podpis pod rysunkiem; alt: opis dla osób niewidzących. Styl rysunku jest wspólny dla tutorialu. (w tej sekcji NIE dodawaj: za blisko rysunki „Mostek próbowany różnymi zabawkami” w sekcji „Czym jest testowanie programu” (odstęp 2, wymagany 3)). Ustawienia: styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.. W body opisz tylko scenę; styl dopisuje renderer.
- module="wtręty" (Wtręt): krótki wtręt (2-4 zdania), który demonstruje pojęcie z tej sekcji humorystycznie albo kontrprzykładem: co się stanie, gdy zrobić odwrotnie albo źle. Może nawiązywać do wcześniejszych wtrętów (ta sama postać, rozwinięcie sytuacji), żeby czytelnik czuł ciągłość; nie kopiuj ich. (w tym dziale limit jest wyczerpany: nie dodawaj). Ustawienia: bohater: Marta, 34-letnia specjalistka ds. kadr, która w arkuszu kalkulacyjnym radzi sobie świetnie, ale kodu nigdy nie pisała. Co miesiąc rozlicza wspólne wydatki z współlokatorami (czynsz, zakupy, wyjazdy) i chce zastąpić ręczne formuły programem, który policzy podział z napiwkiem i rabatem oraz zapisze wynik do pliku; kłopoty jej sprawiają błędy w składni, niezrozumiałe komunikaty i obawa, że zepsuje coś w komputerze..

Wcześniejsze wpisy, które widzi moduł "dowcipy" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta czeka, aż plik sam zadziała: Marta wpisała w `kasa.py` cały podział wydatków, zapisała plik i patrzyła w ekran, czekając na wynik. Nic się nie działo, więc uznała, że komputer jest wolny, a
  - [dowcipy] Tłumacz książki i tłumacz symultaniczny: Kompilator to tłumacz, który zabiera całą książkę i oddaje ją przetłumaczoną dopiero na końcu. Interpreter to tłumacz symultaniczny: mówi na bieżąco, więc o błę
  - [wtręty] Marta widzi komunikat i odsuwa się od klawiatury: Marta zamiast `print` wpisała `prnt`, uruchomiła plik i zobaczyła czerwony komunikat o nieznanej nazwie. Cofnęła ręce z klawiatury jak spod gorącego piekarnika,
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo
  - [dowcipy] Program bez danych jak kuchnia bez produktów: Program bez danych to kucharz bez produktów: piec rozgrzany, fartuch wyprasowany, a obiadu i tak nie będzie.
  - [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech mie
  - [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamó
  - [wtręty] Marta bierze kwotę w cudzysłów: Marta wpisała kwotę jako `"45.5"`, bo w arkuszu tak oznaczała tekstowe komórki, i kazała programowi podzielić ją przez 2. Zamiast `22.75` dostała czerwony `Type
  - [dowcipy] Odpowiedź „no, prawie”: Zapytany, czy współlokator zwrócił pieniądze, program odpowiada `True` albo `False`. Odpowiedź „no, prawie oddał” nie należy do typu `bool`, choć w prawdziwych 
  - [dykteryjki] Cena brutto, która nie nadążała: W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach l
  - [dowcipy] Reszta z dzielenia to ostatni kawałek pizzy: Operator `%` to ten, kto liczy, ile kawałków pizzy zostanie, gdy każdy wziął po równo. Ludzie się wahają, czy sięgnąć po ostatni, ale Python nigdy nie ma z tym 
  - [wtręty] Marta skleja jak w arkuszu: W arkuszu Marta łączyła tekst z liczbą znakiem `&` i nigdy nie miała z tym kłopotu. Napisała więc w Pythonie `"Do zapłaty: " + udzial`, gdzie `udzial` było licz
  - [dykteryjki] Status zapisany małą literą: W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze sta
  - [wtręty] Marta wcina tylko jedną linię: Marta napisała: `if kwota > 100:`, pod spodem wcięte `print("Duża kwota")`, a linię `print("Sprawdź paragon")` zostawiła bez wcięcia, bo chciała ją pokazać tylk
  - [wtręty] Marta kopiuje linię dla każdej osoby: Marta chciała wypisać komunikat dla każdego współlokatora, więc trzy razy wkleiła linię `print("Cześć,", imie)`, za każdym razem z innym imieniem. Gdy w mieszka
  - [dykteryjki] Ponawianie, które nigdy się nie kończyło: Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciel
  - [dowcipy] Pusta lista to torba przed sklepem: Pusta lista `[]` to torba na zakupy przed wejściem do sklepu: już istnieje, ale nic w niej nie ma. `len()` odpowie uczciwie: 0.
  - [wtręty] Marta prosi o czwartego, którego nie ma: Marta miała listę czterech współlokatorów i chciała pokazać ostatniego, więc napisała `osoby[4]`, bo liczyła po ludzku: pierwszy, drugi, trzeci, czwarty. Progra
  - [dowcipy] Lista obecności bez wołania w próżnię: Pętla `for` działa jak nauczyciel z dziennikiem: woła każdego z listy po kolei i na ostatnim nazwisku kończy. Nie stoi potem w drzwiach z pytaniem „a nie ma tu 
  - [dowcipy] Formularz nie zna Twojego nazwiska: Parametr to rubryka w formularzu, argument to to, co do niej wpiszesz. Formularz nie sprawdzi, czy w polu „imię” nie wylądowało nazwisko, a `na_osobe(4, 300)` t
  - [wtręty] Marta dostaje z funkcji „nic”: Marta napisała funkcję `na_osobe`, która na końcu robiła `print(suma / osoby)`, i uznała, że wynik jest gotowy. Próbując dodać do niego napiwek, wpisała `na_oso
  - [dykteryjki] Raport z wartością None: Napisałem funkcję liczącą sumę zamówień klienta. Na końcu wypisywała wynik przez `print`, bo podczas testów tylko na niego patrzyłem na ekranie. Potem inny frag
  - [dowcipy] Program jak drzewo w lesie: Program, który wszystko policzył, ale niczego nie wypisał, przypomina drzewo przewracające się w lesie: nikt tego nie słyszał, więc trudno dowieść, że w ogóle c
  - [dykteryjki] Suma, która wyszła jako sklejenie: W małym skrypcie do zestawień pytałem operatora o dwie liczby przez `input` i dodawałem je do siebie. Przy wartościach 10 i 5 wynik brzmiał 105, bo obie odpowie
  - [wtręty] Marta dopisuje wydatek i kasuje resztę: Marta miała w `wydatki.txt` rozliczenie z trzech miesięcy. Żeby dodać jeszcze jeden zakup, otworzyła plik w trybie `"w"`, bo tak robiła w poprzednim przykładzie
  - [dowcipy] Interfejs to lada w sklepie: Interfejs to lada w sklepie: klient nie widzi magazynu ani zaplecza, widzi tylko ladę i sprzedawcę. Jeśli lada jest zawalona kartonami, nikt nie zapyta, jak świ
  - [wtręty] Marta ufa ciszy zamiast rachunkowi: Marta uruchomiła program, nie zobaczyła żadnego czerwonego komunikatu i uznała, że skoro Python milczy, to wszystko się zgadza. Wysłała współlokatorom wynik `39
  - [dykteryjki] Raport, który wyglądał wiarygodnie: Napisałem skrypt liczący średni czas realizacji zamówień, ale dzieliłem sumę czasów przez liczbę wszystkich zamówień, a sumowałem tylko zrealizowane. Skrypt dzi
  - [dowcipy] Ślad wywołań jako „to nie ja”: Traceback to łańcuszek „to nie ja, to on”: każda funkcja z góry przyznaje tylko, że wywołała następną. Dopiero ostatnia, ta z `ZeroDivisionError`, mówi uczciwie
  - [wtręty] Marta testuje tylko jedną, ulubioną liczbę: Marta dopisała jeden `assert na_osobe(78, 3) == 26`, zobaczyła „Wszystkie testy przeszły” i uznała sprawę za zamkniętą. W następnym miesiącu wyjazd rozliczała s
Wcześniejsze wpisy, które widzi moduł "dygresje" (nie powtarzaj ich tematów, puent ani motywów):
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
  - [dygresje] Skąd Python wziął swoją nazwę: Polecenie `python`, którego używamy do uruchamiania plików, ma nazwę nie od węża, lecz od brytyjskiego programu komediowego. Twórca języka, Guido van Rossum, cz
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo
  - [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamó
  - [dygresje] Rakieta, która pomyliła typy liczb: W 1996 roku pierwsza rakieta Ariane 5 rozpadła się po niespełna 40 sekundach lotu. Komisja badająca wypadek wskazała, że oprogramowanie zamieniało liczbę z ułam
  - [dykteryjki] Cena brutto, która nie nadążała: W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach l
  - [dykteryjki] Status zapisany małą literą: W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze sta
  - [dykteryjki] Ponawianie, które nigdy się nie kończyło: Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciel
  - [dygresje] Dlaczego liczenie zaczyna się od zera: Holenderski informatyk Edsger Dijkstra w krótkiej notatce z 1982 roku przekonywał, że numerację warto zaczynać od zera, a zakresy zapisywać tak, by początek był
  - [dykteryjki] Raport z wartością None: Napisałem funkcję liczącą sumę zamówień klienta. Na końcu wypisywała wynik przez `print`, bo podczas testów tylko na niego patrzyłem na ekranie. Potem inny frag
  - [dygresje] Podprogramy: pomysł z pierwszych komputerów: Pomysł, by raz napisany fragment programu wywoływać wielokrotnie, jest starszy niż większość języków programowania. Za sformalizowanie go uważa się zwykle Mauri
  - [dykteryjki] Suma, która wyszła jako sklejenie: W małym skrypcie do zestawień pytałem operatora o dwie liczby przez `input` i dodawałem je do siebie. Przy wartościach 10 i 5 wynik brzmiał 105, bo obie odpowie
  - [dygresje] Mysz i okna na pokazie z 1968 roku: 9 grudnia 1968 roku Douglas Engelbart pokazał w San Francisco system, w którym po raz pierwszy publicznie użyto myszy do sterowania komputerem. Na jednym ekrani
  - [dykteryjki] Raport, który wyglądał wiarygodnie: Napisałem skrypt liczący średni czas realizacji zamówień, ale dzieliłem sumę czasów przez liczbę wszystkich zamówień, a sumowałem tylko zrealizowane. Skrypt dzi
Wcześniejsze wpisy, które widzi moduł "dykteryjki" (nie powtarzaj ich tematów, puent ani motywów):
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [wtręty] Marta odejmuje udział, zanim go policzy: Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wyno
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [wtręty] Marta zleca całe rozliczenie jednym zdaniem: Marta wpisała jedną instrukcję: „rozlicz wyjazd”. Kiedy wynik się nie zgadzał, nie umiała powiedzieć, czy zawiodła suma, udział, czy porównanie z wpłatą, bo wsz
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
  - [wtręty] Marta czeka, aż plik sam zadziała: Marta wpisała w `kasa.py` cały podział wydatków, zapisała plik i patrzyła w ekran, czekając na wynik. Nic się nie działo, więc uznała, że komputer jest wolny, a
  - [dygresje] Skąd Python wziął swoją nazwę: Polecenie `python`, którego używamy do uruchamiania plików, ma nazwę nie od węża, lecz od brytyjskiego programu komediowego. Twórca języka, Guido van Rossum, cz
  - [wtręty] Marta widzi komunikat i odsuwa się od klawiatury: Marta zamiast `print` wpisała `prnt`, uruchomiła plik i zobaczyła czerwony komunikat o nieznanej nazwie. Cofnęła ręce z klawiatury jak spod gorącego piekarnika,
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo
  - [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech mie
  - [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamó
  - [wtręty] Marta bierze kwotę w cudzysłów: Marta wpisała kwotę jako `"45.5"`, bo w arkuszu tak oznaczała tekstowe komórki, i kazała programowi podzielić ją przez 2. Zamiast `22.75` dostała czerwony `Type
  - [dygresje] Rakieta, która pomyliła typy liczb: W 1996 roku pierwsza rakieta Ariane 5 rozpadła się po niespełna 40 sekundach lotu. Komisja badająca wypadek wskazała, że oprogramowanie zamieniało liczbę z ułam
  - [dykteryjki] Cena brutto, która nie nadążała: W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach l
  - [wtręty] Marta skleja jak w arkuszu: W arkuszu Marta łączyła tekst z liczbą znakiem `&` i nigdy nie miała z tym kłopotu. Napisała więc w Pythonie `"Do zapłaty: " + udzial`, gdzie `udzial` było licz
  - [dykteryjki] Status zapisany małą literą: W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze sta
  - [wtręty] Marta wcina tylko jedną linię: Marta napisała: `if kwota > 100:`, pod spodem wcięte `print("Duża kwota")`, a linię `print("Sprawdź paragon")` zostawiła bez wcięcia, bo chciała ją pokazać tylk
  - [wtręty] Marta kopiuje linię dla każdej osoby: Marta chciała wypisać komunikat dla każdego współlokatora, więc trzy razy wkleiła linię `print("Cześć,", imie)`, za każdym razem z innym imieniem. Gdy w mieszka
  - [dykteryjki] Ponawianie, które nigdy się nie kończyło: Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciel
  - [dygresje] Dlaczego liczenie zaczyna się od zera: Holenderski informatyk Edsger Dijkstra w krótkiej notatce z 1982 roku przekonywał, że numerację warto zaczynać od zera, a zakresy zapisywać tak, by początek był
  - [wtręty] Marta prosi o czwartego, którego nie ma: Marta miała listę czterech współlokatorów i chciała pokazać ostatniego, więc napisała `osoby[4]`, bo liczyła po ludzku: pierwszy, drugi, trzeci, czwarty. Progra
  - [wtręty] Marta dostaje z funkcji „nic”: Marta napisała funkcję `na_osobe`, która na końcu robiła `print(suma / osoby)`, i uznała, że wynik jest gotowy. Próbując dodać do niego napiwek, wpisała `na_oso
  - [dykteryjki] Raport z wartością None: Napisałem funkcję liczącą sumę zamówień klienta. Na końcu wypisywała wynik przez `print`, bo podczas testów tylko na niego patrzyłem na ekranie. Potem inny frag
  - [dygresje] Podprogramy: pomysł z pierwszych komputerów: Pomysł, by raz napisany fragment programu wywoływać wielokrotnie, jest starszy niż większość języków programowania. Za sformalizowanie go uważa się zwykle Mauri
  - [dykteryjki] Suma, która wyszła jako sklejenie: W małym skrypcie do zestawień pytałem operatora o dwie liczby przez `input` i dodawałem je do siebie. Przy wartościach 10 i 5 wynik brzmiał 105, bo obie odpowie
  - [wtręty] Marta dopisuje wydatek i kasuje resztę: Marta miała w `wydatki.txt` rozliczenie z trzech miesięcy. Żeby dodać jeszcze jeden zakup, otworzyła plik w trybie `"w"`, bo tak robiła w poprzednim przykładzie
  - [dygresje] Mysz i okna na pokazie z 1968 roku: 9 grudnia 1968 roku Douglas Engelbart pokazał w San Francisco system, w którym po raz pierwszy publicznie użyto myszy do sterowania komputerem. Na jednym ekrani
  - [wtręty] Marta ufa ciszy zamiast rachunkowi: Marta uruchomiła program, nie zobaczyła żadnego czerwonego komunikatu i uznała, że skoro Python milczy, to wszystko się zgadza. Wysłała współlokatorom wynik `39
  - [dykteryjki] Raport, który wyglądał wiarygodnie: Napisałem skrypt liczący średni czas realizacji zamówień, ale dzieliłem sumę czasów przez liczbę wszystkich zamówień, a sumowałem tylko zrealizowane. Skrypt dzi
  - [wtręty] Marta testuje tylko jedną, ulubioną liczbę: Marta dopisała jeden `assert na_osobe(78, 3) == 26`, zobaczyła „Wszystkie testy przeszły” i uznała sprawę za zamkniętą. W następnym miesiącu wyjazd rozliczała s
Wcześniejsze wpisy, które widzi moduł "rysunki" (nie powtarzaj ich tematów, puent ani motywów):
  - [rysunki] Pętla poprawek przy stole: Przy drewnianym stole siedzi uśmiechnięta kobieta z ołówkiem i gumką. Przed nią kartka z ręcznie narysowanymi kółkami połączonymi strzałkami, które tworzą zamkn
  - [rysunki] Przepis dla kogoś, kto nigdy nie gotował: Jasna kuchnia. Początkujący kucharz w fartuchu stoi przy piekarniku z otwartymi drzwiczkami i ostrożnie wbija cienki termometr w złocisty placek na blasze. Na b
  - [rysunki] Pomocnik z zakreślaczami: Ciepła scena przy biurku: uśmiechnięta osoba siedzi przed laptopem, na którego ekranie widać kilka linii abstrakcyjnego kodu jako kolorowe paski i kropki, bez c
  - [rysunki] Dwa pudełka, dwie etykiety: Jasny pokój z drewnianą półką. Na półce stoją obok siebie dwa kartonowe pudełka z doczepionymi papierowymi etykietami (puste kartki, bez tekstu). Uśmiechnięta o
  - [rysunki] Rozwidlenie drogi bez trzeciej ścieżki: Wiejska droga rozwidla się na dwie ścieżki: jedna prowadzi do niebieskiego domku z ogródkiem, druga na łąkę z drzewem. Przy rozwidleniu stoi uśmiechnięty wędrow
  - [rysunki] Chomik w kole bez wyjścia: Ciepła scena w pokoju: puszysty chomik biegnie w kole w klatce, z determinacją na pyszczku. Z boku koła widać wyraźnie otwarte małe drzwiczki, ale chomik patrzy
  - [rysunki] Jedna foremka, wiele ciastek: Jasna kuchnia. Uśmiechnięta piekarka trzyma jedną metalową foremkę w kształcie gwiazdki. Na blacie leżą trzy płaty ciasta w różnych kolorach: jasne, kakaowe i r
  - [rysunki] Tablica się kończy, zeszyt zostaje: Jasna klasa po lekcjach. Uśmiechnięty woźny w granatowym fartuchu ściera gąbką kredowe napisy z dużej zielonej tablicy, na której widać tylko abstrakcyjne bazgr
  - [rysunki] Mostek próbowany różnymi zabawkami: Jasny pokój z dywanem. Uśmiechnięta osoba klęczy przy małym drewnianym mostku zbudowanym z klocków nad niebieskim kocem udającym rzekę. Po mostku jedzie kolejno
Wcześniejsze wpisy, które widzi moduł "wtręty" (możesz do nich nawiązać, rozwijając postać albo sytuację; nie kopiuj):
  - [wtręty] Marta czeka, aż plik sam zadziała: Marta wpisała w `kasa.py` cały podział wydatków, zapisała plik i patrzyła w ekran, czekając na wynik. Nic się nie działo, więc uznała, że komputer jest wolny, a
  - [dowcipy] Tłumacz książki i tłumacz symultaniczny: Kompilator to tłumacz, który zabiera całą książkę i oddaje ją przetłumaczoną dopiero na końcu. Interpreter to tłumacz symultaniczny: mówi na bieżąco, więc o błę
  - [wtręty] Marta widzi komunikat i odsuwa się od klawiatury: Marta zamiast `print` wpisała `prnt`, uruchomiła plik i zobaczyła czerwony komunikat o nieznanej nazwie. Cofnęła ręce z klawiatury jak spod gorącego piekarnika,
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo
  - [dowcipy] Program bez danych jak kuchnia bez produktów: Program bez danych to kucharz bez produktów: piec rozgrzany, fartuch wyprasowany, a obiadu i tak nie będzie.
  - [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech mie
  - [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamó
  - [wtręty] Marta bierze kwotę w cudzysłów: Marta wpisała kwotę jako `"45.5"`, bo w arkuszu tak oznaczała tekstowe komórki, i kazała programowi podzielić ją przez 2. Zamiast `22.75` dostała czerwony `Type
  - [dowcipy] Odpowiedź „no, prawie”: Zapytany, czy współlokator zwrócił pieniądze, program odpowiada `True` albo `False`. Odpowiedź „no, prawie oddał” nie należy do typu `bool`, choć w prawdziwych 
  - [dykteryjki] Cena brutto, która nie nadążała: W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach l
  - [dowcipy] Reszta z dzielenia to ostatni kawałek pizzy: Operator `%` to ten, kto liczy, ile kawałków pizzy zostanie, gdy każdy wziął po równo. Ludzie się wahają, czy sięgnąć po ostatni, ale Python nigdy nie ma z tym 
  - [wtręty] Marta skleja jak w arkuszu: W arkuszu Marta łączyła tekst z liczbą znakiem `&` i nigdy nie miała z tym kłopotu. Napisała więc w Pythonie `"Do zapłaty: " + udzial`, gdzie `udzial` było licz
  - [dykteryjki] Status zapisany małą literą: W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze sta
  - [wtręty] Marta wcina tylko jedną linię: Marta napisała: `if kwota > 100:`, pod spodem wcięte `print("Duża kwota")`, a linię `print("Sprawdź paragon")` zostawiła bez wcięcia, bo chciała ją pokazać tylk
  - [wtręty] Marta kopiuje linię dla każdej osoby: Marta chciała wypisać komunikat dla każdego współlokatora, więc trzy razy wkleiła linię `print("Cześć,", imie)`, za każdym razem z innym imieniem. Gdy w mieszka
  - [dykteryjki] Ponawianie, które nigdy się nie kończyło: Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciel
  - [dowcipy] Pusta lista to torba przed sklepem: Pusta lista `[]` to torba na zakupy przed wejściem do sklepu: już istnieje, ale nic w niej nie ma. `len()` odpowie uczciwie: 0.
  - [wtręty] Marta prosi o czwartego, którego nie ma: Marta miała listę czterech współlokatorów i chciała pokazać ostatniego, więc napisała `osoby[4]`, bo liczyła po ludzku: pierwszy, drugi, trzeci, czwarty. Progra
  - [dowcipy] Lista obecności bez wołania w próżnię: Pętla `for` działa jak nauczyciel z dziennikiem: woła każdego z listy po kolei i na ostatnim nazwisku kończy. Nie stoi potem w drzwiach z pytaniem „a nie ma tu 
  - [dowcipy] Formularz nie zna Twojego nazwiska: Parametr to rubryka w formularzu, argument to to, co do niej wpiszesz. Formularz nie sprawdzi, czy w polu „imię” nie wylądowało nazwisko, a `na_osobe(4, 300)` t
  - [wtręty] Marta dostaje z funkcji „nic”: Marta napisała funkcję `na_osobe`, która na końcu robiła `print(suma / osoby)`, i uznała, że wynik jest gotowy. Próbując dodać do niego napiwek, wpisała `na_oso
  - [dykteryjki] Raport z wartością None: Napisałem funkcję liczącą sumę zamówień klienta. Na końcu wypisywała wynik przez `print`, bo podczas testów tylko na niego patrzyłem na ekranie. Potem inny frag
  - [dowcipy] Program jak drzewo w lesie: Program, który wszystko policzył, ale niczego nie wypisał, przypomina drzewo przewracające się w lesie: nikt tego nie słyszał, więc trudno dowieść, że w ogóle c
  - [dykteryjki] Suma, która wyszła jako sklejenie: W małym skrypcie do zestawień pytałem operatora o dwie liczby przez `input` i dodawałem je do siebie. Przy wartościach 10 i 5 wynik brzmiał 105, bo obie odpowie
  - [wtręty] Marta dopisuje wydatek i kasuje resztę: Marta miała w `wydatki.txt` rozliczenie z trzech miesięcy. Żeby dodać jeszcze jeden zakup, otworzyła plik w trybie `"w"`, bo tak robiła w poprzednim przykładzie
  - [dowcipy] Interfejs to lada w sklepie: Interfejs to lada w sklepie: klient nie widzi magazynu ani zaplecza, widzi tylko ladę i sprzedawcę. Jeśli lada jest zawalona kartonami, nikt nie zapyta, jak świ
  - [wtręty] Marta ufa ciszy zamiast rachunkowi: Marta uruchomiła program, nie zobaczyła żadnego czerwonego komunikatu i uznała, że skoro Python milczy, to wszystko się zgadza. Wysłała współlokatorom wynik `39
  - [dykteryjki] Raport, który wyglądał wiarygodnie: Napisałem skrypt liczący średni czas realizacji zamówień, ale dzieliłem sumę czasów przez liczbę wszystkich zamówień, a sumowałem tylko zrealizowane. Skrypt dzi
  - [dowcipy] Ślad wywołań jako „to nie ja”: Traceback to łańcuszek „to nie ja, to on”: każda funkcja z góry przyznaje tylko, że wywołała następną. Dopiero ostatnia, ta z `ZeroDivisionError`, mówi uczciwie
  - [wtręty] Marta testuje tylko jedną, ulubioną liczbę: Marta dopisała jeden `assert na_osobe(78, 3) == 26`, zobaczyła „Wszystkie testy przeszły” i uznała sprawę za zamkniętą. W następnym miesiącu wyjazd rozliczała s

W jednej sekcji najwyżej 2 dodatki łącznie; nie łącz w jednej sekcji modułów, które się nie lubią.
Dla każdego dodatku: module, title (maks. 8 słów), body; dla ilustracji także caption i alt.

SEKCJA "Po co zapisywać wersje kodu" (dział 09. Błędy i dobre praktyki):
Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast szukać własnych zmian z pamięci.

Robi to [[git|Git]], program do zapisywania historii plików. Zapis jednej wersji to [[commit|commit]]: zdjęcie wybranych plików z danej chwili, z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię, to [[repozytorium|repozytorium]]. W przykładowym programie do dzielenia wydatków, „Wspólnej Kasie”, będzie nim folder `wspolna_kasa`, w którym leżą pliki programu.

Wersje przydają się w trzech sytuacjach:

- Dopisujesz do „Wspólnej Kasy” nową funkcję, [[sec-09-czym-jest-testowanie-programu|testy]] przestają przechodzić, a Ty wracasz do wczorajszego commita zamiast szukać własnych zmian.
- Historia pokazuje, kiedy pojawił się błąd, co przy szukaniu przyczyny oszczędza sporo czasu.
- Każdy commit ma opis, więc po miesiącu wiesz, dlaczego kod wygląda tak, a nie inaczej.

Dobry moment na commit to chwila, gdy testy przechodzą. Wiele małych commitów jest lepsze niż jeden wielki.

Sam zapis wygląda tak:

```text
git init -b main
git add funkcje.py test_rozlicz.py
git commit -m "Funkcje i testy Wspolnej Kasy"
```

`init` zakłada repozytorium w bieżącym folderze, `add` wybiera pliki do zapisu, a `commit` zapisuje wersję. Git trzeba mieć zainstalowanym (sprawdzisz to poleceniem `git --version`, a instalator jest na stronie git-scm.com). Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym.
````

## Odpowiedź

````json
{
  "items": [
    {
      "module": "dygresje",
      "title": "Git powstał w kilka tygodni z konfliktu",
      "body": "Git stworzył w 2005 roku Linus Torvalds, autor jądra Linuksa. Wcześniej projekt korzystał z komercyjnego programu do wersjonowania, ale gdy współpraca z jego producentem się załamała, darmowy dostęp do niego cofnięto. Torvalds napisał więc własne narzędzie, szybkie i przystosowane do pracy wielu osób naraz. Dziś tym samym programem, który powstał na potrzeby jednego projektu, zapisujemy historię niemal wszystkich.",
      "sources": [
        {
          "title": "Pro Git: Getting Started – A Short History of Git",
          "url": "https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git",
          "supports": "Git powstał w 2005 roku, gdy społeczność jądra Linuksa straciła darmowy dostęp do poprzedniego narzędzia, a Linus Torvalds stworzył nowe."
        }
      ]
    },
    {
      "module": "dykteryjki",
      "title": "Poprawka, której nie dało się cofnąć",
      "body": "Przed wdrożeniem drobnej poprawki w skrypcie do automatyzacji nie zapisałem poprzedniej wersji, bo zmiana wydawała się banalna. Następnego dnia skrypt zaczął zwracać błędne dane, a ja nie potrafiłem odtworzyć z pamięci, które linie zmieniłem. Zajęło mi to kilka godzin porównywania z kopią z innego folderu, która na dodatek była nieaktualna. Od tamtej pory zapisuję commit za każdym razem, gdy testy przechodzą, bo wtedy powrót do działającego stanu trwa chwilę."
    }
  ]
}
````
