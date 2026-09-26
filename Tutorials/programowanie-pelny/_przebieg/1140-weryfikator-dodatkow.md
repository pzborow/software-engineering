# Krok 1140 · weryfikator_dodatków

Węzeł: `layers` · dział: 10 · pytanie: 58 · próba: —

## Prompt

````text
Jesteś weryfikatorem dodatków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.
Sprawdź każdy dodatek (dygresję, żart, pomysł na ilustrację) do sekcji poniżej:
1. Logika: czy puenta, porównanie albo scena mają sens i są wewnętrznie spójne (np. żart mówi o literówce,
   a w jego przykładzie żadnej literówki nie ma, to błąd).
2. Zgodność z sekcją: czy dodatek naprawdę dotyczy tego, co sekcja mówi, i nie przeczy jej.
3. Fakty: daty, nazwiska, historie. Odrzuć, jeśli fakt jest błędny albo nie masz pewności, że jest prawdziwy.
4. Ton: bez żartów z ludzi i grup.
5. Rejestr: dodatek, który powtarza temat, puentę albo motyw wcześniejszego wpisu z zakazem powtórzeń, jest błędny;
   nawiązanie do wcześniejszego wpisu jest dobre tylko wtedy, gdy zgadza się z pierwowzorem.
6. Źródła: dodatek oznaczony [źródło wymagane] musi mieć źródło, które faktycznie otworzysz (WebFetch) i które
   potwierdza jego twierdzenia. Potwierdzone źródło podaj w source (title, url, supports). Bez potwierdzenia: ok=false.
Dla każdego podaj index, ok i przy ok=false jednozdaniowe problem.
Wcześniejsze wpisy, które widzi moduł "dowcipy" (nie powtarzaj ich tematów, puent ani motywów):
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
  - [dowcipy] Alarm: wejście godzina, wyjście irytacja: Alarm w telefonie to wzorowy program: bierze dane wejściowe (godzinę), porównuje je z zegarem i bez wahania oddaje dane wyjściowe, czyli dzwonek. Że wyjściem by
  - [dykteryjki] Strona, która nie działała w magazynie: Zbudowałem prostą stronę do odnotowywania stanów w magazynie i przez biurowe Wi-Fi działała bez zarzutu. W piwnicznej hali zasięgu prawie nie było, więc strona 
  - [wtręty] Marta rozsyła program mailem: Marta uznała, że „aplikacją” jest plik `kasa.py` wysłany współlokatorom mailem. Gdy poprawiła w nim liczenie napiwku, wysłała nową wersję, ale jedna osoba dalej
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
  - [dykteryjki] Strona, która nie działała w magazynie: Zbudowałem prostą stronę do odnotowywania stanów w magazynie i przez biurowe Wi-Fi działała bez zarzutu. W piwnicznej hali zasięgu prawie nie było, więc strona 
Wcześniejsze wpisy, które widzi moduł "dykteryjki" (nie powtarzaj ich tematów, puent ani motywów):
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
  - [dykteryjki] Strona, która nie działała w magazynie: Zbudowałem prostą stronę do odnotowywania stanów w magazynie i przez biurowe Wi-Fi działała bez zarzutu. W piwnicznej hali zasięgu prawie nie było, więc strona 
  - [wtręty] Marta rozsyła program mailem: Marta uznała, że „aplikacją” jest plik `kasa.py` wysłany współlokatorom mailem. Gdy poprawiła w nim liczenie napiwku, wysłała nową wersję, ale jedna osoba dalej
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
  - [dowcipy] Alarm: wejście godzina, wyjście irytacja: Alarm w telefonie to wzorowy program: bierze dane wejściowe (godzinę), porównuje je z zegarem i bez wahania oddaje dane wyjściowe, czyli dzwonek. Że wyjściem by
  - [dykteryjki] Strona, która nie działała w magazynie: Zbudowałem prostą stronę do odnotowywania stanów w magazynie i przez biurowe Wi-Fi działała bez zarzutu. W piwnicznej hali zasięgu prawie nie było, więc strona 
  - [wtręty] Marta rozsyła program mailem: Marta uznała, że „aplikacją” jest plik `kasa.py` wysłany współlokatorom mailem. Gdy poprawiła w nim liczenie napiwku, wysłała nową wersję, ale jedna osoba dalej

DODATKI:
0. [rysunki] Haki co kilka kroków: Ciepła scena na łagodnej skalnej ścianie w górach. Uśmiechnięta wspinaczka w kasku i uprzęży pnie się w górę i właśnie wbija kolejny hak z liną. Poniżej niej, w równych odstępach, widać rządek już wbitych haków z karabinkami, połączonych jedną liną aż do ziemi. Na dole stoi drugi, zadowolony człowiek z termosem i trzyma koniec liny. Za skałą wschodzące słońce, w oddali łąka i kilka drzew.
1. [dowcipy] Skarpetka w szufladzie, nie w mieszkaniu: Szukanie błędu w stu nowych liniach to szukanie zgubionej skarpetki w całym mieszkaniu. Po jednym małym kroku szukasz jej tylko w szufladzie, do której przed chwilą zaglądałeś.

SEKCJA "Od pomysłu do działającego programu":
Od pomysłu do programu dochodzi się małymi krokami: opisujesz zadanie zwykłymi słowami, piszesz najmniejszy kawałek, który coś robi, sprawdzasz go i dopiero wtedy dokładasz następny. Cały program naraz zwykle nie działa, a szukanie błędu w stu liniach jest męczące.

```text
pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit
              ↑                                                            |
              └──────────────────── następny kawałek ←─────────────────────┘
```

Weźmy pomysł: „chcę wiedzieć, kto komu ile jest winien”. Opis krokowy to rozbicie zadania na kroki, z których każdy da się zrobić osobno: dla każdej osoby zsumuj to, co zapłaciła, odejmij jej równy udział i wypisz wynik. Z tego wychodzi jedna mała [[funkcja]]:

```python
def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...
```

Funkcję sprawdzasz na danych, których wynik znasz z kartki. Dopiero gdy się zgadza, zapisujesz [[commit]] (zapisaną wersję kodu z opisem) i myślisz o kolejnym kawałku, np. wczytaniu wydatków z pliku.

Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, jak w sekcji o zapisywaniu wersji kodu. Dzięki temu nie zgadujesz, gdzie szukać błędu.
````

## Odpowiedź

````json
{
  "verdicts": [
    {
      "index": 0,
      "ok": true
    },
    {
      "index": 1,
      "ok": true
    }
  ]
}
````
