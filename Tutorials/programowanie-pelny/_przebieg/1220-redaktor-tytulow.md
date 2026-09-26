# Krok 1220 · redaktor_tytułów

Węzeł: `titles` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem tytułów tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.

Nadaj tytułom jeden styl: Krótkie polecenie do czytelnika w trybie rozkazującym, zaczynające się od czasownika, 2-5 słów, bez znaku zapytania i bez dwukropka, np. 'Rozłóż problem na kroki', 'Poznaj swój pierwszy błąd'. Nie zaczynaj więcej niż dwóch tytułów tym samym czasownikiem; poprawna polszczyzna (przecinki przed 'czym', 'jak')..
Zasady niezależne od stylu:
- Tytuł mówi, co naprawdę dzieje się w sekcji; opieraj się na opisie „o czym” (pytanie i główna myśl), nie tylko na starym tytule.
  Sekcja, która porównuje dwie rzeczy, ma tytuł o porównaniu; sekcja, która definiuje, ma tytuł o definicji.
- Wybieraj słowa jednoznaczne w tym kontekście. Unikaj słów o kilku znaczeniach, gdy czytelnik może odczytać je źle
  (np. „zestaw” jako złóż zamiast porównaj).
- Tytuł ma brzmieć naturalnie, jak napisany przez dobrego redaktora, a nie jak mechaniczne przekształcenie pytania.
  Poprawna gramatyka i interpunkcja.
- Nie wymyślaj treści, której w sekcji nie ma. Tytuły sekcji w jednym dziale muszą być różne.
Tytuł, który już pasuje do stylu i zasad, zostaw bez zmian. Zwróć items z id i title dla KAŻDEJ pozycji.

TYTUŁY (id: tytuł; „dział-N” to tytuł działu, reszta to sekcje):
- dział-1: Czym jest programowanie
  (o czym: Czym jest program komputerowy? / Czym jest programowanie? / Kim jest programista i czym się zajmuje?)
- dział-2: Algorytmy i myślenie krokowe
  (o czym: Czym jest algorytm? / Jak przepis kulinarny przypomina algorytm? / Dlaczego kolejność kroków w algorytmie ma znaczenie?)
- dział-3: Kod i jego uruchamianie
  (o czym: Czym jest kod źródłowy? / Do czego służy edytor kodu? / Co to znaczy uruchomić program?)
- dział-4: Dane i zmienne
  (o czym: Czym jest dana w programie? / Czym jest zmienna? / Jak można porównać zmienną do pudełka z etykietą?)
- dział-5: Operacje i decyzje
  (o czym: Jakie podstawowe działania matematyczne może wykonać program? / Jak program łączy ze sobą teksty? / Jak program porównuje dwie wartości?)
- dział-6: Powtarzanie i kolekcje
  (o czym: Czym jest pętla? / Kiedy warto użyć pętli zamiast pisać to samo wiele razy? / Czym jest pętla nieskończona i dlaczego jest problemem?)
- dział-7: Funkcje i porządek w kodzie
  (o czym: Czym jest funkcja? / Po co dzielić program na funkcje? / Czym są argumenty funkcji?)
- dział-8: Współpraca programu z użytkownikiem
  (o czym: Czym są dane wejściowe programu? / Czym są dane wyjściowe programu? / Jak program może zapytać użytkownika o informację?)
- dział-9: Błędy i dobre praktyki
  (o czym: Czym różni się błąd składni od błędu logicznego? / Jak przeczytać komunikat o błędzie? / Czym jest testowanie programu?)
- dział-10: Programowanie w praktyce
  (o czym: Jakie są przykłady programów używanych na co dzień? / Czym różni się strona internetowa od aplikacji mobilnej? / Jak od pomysłu dojść do działającego programu?)
- sec-01-czym-jest-program-komputerowy: Czym jest program komputerowy
  (o czym: Czym jest program komputerowy? / Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.)
- sec-01-czym-jest-programowanie: Czym jest programowanie
  (o czym: Czym jest programowanie? / Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.)
- sec-01-kim-jest-programista: Kim jest programista
  (o czym: Kim jest programista i czym się zajmuje? / Programista zamienia potrzebę na działający program, a pisanie kodu to tylko jeden z etapów tej pracy.)
- sec-01-czym-jest-jezyk-programowania: Czym jest język programowania
  (o czym: Czym jest język programowania? / Język programowania to ścisły zestaw słów i reguł zapisu, dzięki któremu człowiek wyraża instrukcje tak, by komputer wykonał je jednoznacznie.)
- sec-01-po-co-komputerowi-precyzja: Po co komputerowi precyzja
  (o czym: Dlaczego komputer potrzebuje precyzyjnych instrukcji? / Komputer wykonuje dokładnie to, co zapisano, więc każdy szczegół, który człowiek by sobie dopowiedział, trzeba podać wprost.)
- sec-01-program-a-aplikacja: Program a aplikacja
  (o czym: Czym różni się program od aplikacji? / Aplikacja to program z oprawą dla użytkownika, więc każda aplikacja jest programem, ale nie odwrotnie.)
- sec-02-czym-jest-algorytm: Czym jest algorytm
  (o czym: Czym jest algorytm? / Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.)
- sec-02-przepis-jako-algorytm: Przepis jako algorytm
  (o czym: Jak przepis kulinarny przypomina algorytm? / Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.)
- sec-02-kolejnosc-krokow-algorytmu: Kolejność kroków algorytmu
  (o czym: Dlaczego kolejność kroków w algorytmie ma znaczenie? / Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.)
- sec-02-czym-jest-schemat-blokowy: Czym jest schemat blokowy
  (o czym: Czym jest schemat blokowy? / Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, dzięki czemu rozgałęzienia, powroty i koniec widać, zanim powstanie kod.)
- sec-02-podzial-problemu-na-czesci: Podział problemu na części
  (o czym: Jak podzielić duży problem na mniejsze części? / Dziel problem na części z jasnym wejściem i wynikiem, aż każdą da się opisać jednym zdaniem i sprawdzić osobno.)
- sec-02-poprawny-algorytm: Poprawny algorytm
  (o czym: Co to znaczy, że algorytm jest poprawny? / Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, także w przypadkach brzegowych.)
- sec-03-czym-jest-kod-zrodlowy: Czym jest kod źródłowy
  (o czym: Czym jest kod źródłowy? / Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.)
- sec-03-do-czego-sluzy-edytor: Do czego służy edytor
  (o czym: Do czego służy edytor kodu? / Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.)
- sec-03-co-znaczy-uruchomic-program: Co znaczy uruchomić program
  (o czym: Co to znaczy uruchomić program? / Uruchomienie programu to polecenie, by Python wykonał instrukcje z pliku po kolei, a sam plik pozostaje bez zmian.)
- sec-03-kompilator-i-interpreter: Kompilator i interpreter
  (o czym: Czym jest kompilator lub interpreter? / Kompilator tłumaczy cały kod na osobny plik przed startem, a interpreter wykonuje kod na bieżąco, dlatego w Pythonie wystarczy zapisać i uruchomić.)
- sec-03-co-to-jest-blad-w-programie: Co to jest błąd w programie
  (o czym: Co to jest błąd w programie? / Błąd to rozbieżność między zamiarem a działaniem programu: czasem zatrzymuje go komunikat, a czasem zły wynik pojawia się po cichu.)
- sec-03-do-czego-sluza-komentarze: Do czego służą komentarze
  (o czym: Do czego służą komentarze w kodzie? / Komentarz zaczyna się od `#`, jest pomijany przez Pythona i ma wyjaśniać powód, a nie powtarzać kod; po zmianie kodu trzeba go zaktualizować.)
- sec-04-czym-jest-dana: Czym jest dana
  (o czym: Czym jest dana w programie? / Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.)
- sec-04-czym-jest-zmienna: Czym jest zmienna
  (o czym: Czym jest zmienna? / Zmienna to nazwa, pod którą program przechowuje daną, żeby móc jej użyć wielokrotnie i w razie potrzeby zmienić.)
- sec-04-zmienna-jako-pudelko-z-etykieta: Zmienna jako pudełko z etykietą
  (o czym: Jak można porównać zmienną do pudełka z etykietą? / Zmienna to pudełko z etykietą: nazwa zostaje, w środku jest jedna wartość, którą można podmienić, a kopie są niezależne.)
- sec-04-liczba-a-tekst: Liczba a tekst
  (o czym: Czym różni się liczba od tekstu w programie? / Cudzysłów zmienia rodzaj danych: 45.5 to liczba, którą można dzielić, a "45.5" to tekst, którego dzielić się nie da.)
- sec-04-czym-jest-typ-danych: Czym jest typ danych
  (o czym: Czym jest typ danych? / Typ danych to rodzaj wartości (str, int, float, bool), który decyduje o tym, jakie działania są na niej możliwe.)
- sec-04-wartosc-logiczna-prawda-falsz: Wartość logiczna prawda/fałsz
  (o czym: Co to jest wartość logiczna prawda/fałsz? / Wartość logiczna (`bool`) to `True` albo `False`, zapisywane z wielkiej litery i bez cudzysłowu, a program używa jej do podejmowania decyzji.)
- sec-04-przypisanie-wartosci-do-zmiennej: Przypisanie wartości do zmiennej
  (o czym: Do czego służy przypisanie wartości do zmiennej? / Przypisanie `=` to polecenie zapisania wartości z prawej strony pod nazwą z lewej, a o wartości zmiennej decyduje ostatnie wykonane przypisanie.)
- sec-05-dzialania-matematyczne-w-programie: Działania matematyczne w programie
  (o czym: Jakie podstawowe działania matematyczne może wykonać program? / Python zna siedem podstawowych operatorów arytmetycznych (`+ - * / // % **`); na tekście dzielić się nie da, a `+` i `*` znaczą tam sklejanie i powtarzanie.)
- sec-05-laczenie-tekstow: Łączenie tekstów
  (o czym: Jak program łączy ze sobą teksty? / Plus skleja tylko tekst z tekstem, bez dodawania spacji, a liczbę trzeba przed sklejeniem zamienić funkcją str() albo użyć zapisu z f.)
- sec-05-porownywanie-wartosci: Porównywanie wartości
  (o czym: Jak program porównuje dwie wartości? / Operatory porównania (`==`, `!=`, `<`, `>`, `<=`, `>=`) dają `True` albo `False`, a `==` pyta o równość, w przeciwieństwie do `=`, które przypisuje.)
- sec-05-instrukcja-warunkowa-jesli-to: Instrukcja warunkowa „jeśli… to…”
  (o czym: Czym jest instrukcja warunkowa „jeśli… to…”? / Instrukcja `if` wykonuje wcięte pod nią linie tylko wtedy, gdy warunek daje `True`; w przeciwnym razie Python je pomija.)
- sec-05-czesc-w-przeciwnym-razie: Część „w przeciwnym razie”
  (o czym: Do czego służy część „w przeciwnym razie”? / `else` to droga „w przeciwnym razie”: wykonuje się tylko wtedy, gdy warunek z `if` jest fałszywy, więc program zawsze wybiera dokładnie jedną z dwóch dróg.)
- sec-05-operatory-i-oraz-lub: Operatory „i” oraz „lub”
  (o czym: Do czego służą operatory „i” oraz „lub”? / `and` wymaga prawdziwości obu warunków, a `or` wystarczy jeden prawdziwy, żeby całość dała `True`.)
- sec-06-czym-jest-petla: Czym jest pętla
  (o czym: Czym jest pętla? / Pętla powtarza wcięty fragment kodu, a `for` robi to raz dla każdego elementu zestawu danych, po czym kończy pracę.)
- sec-06-kiedy-siegnac-po-petle: Kiedy sięgnąć po pętlę
  (o czym: Kiedy warto użyć pętli zamiast pisać to samo wiele razy? / Gdy kopiujesz linię i zmieniasz w niej tylko jedną wartość, użyj pętli: jeden zapis obsłuży dowolną liczbę elementów.)
- sec-06-petla-nieskonczona: Pętla nieskończona
  (o czym: Czym jest pętla nieskończona i dlaczego jest problemem? / Pętla nieskończona nigdy nie osiąga warunku zakończenia, więc program się „zawiesza”; zatrzymasz go Ctrl+C, a przy każdym `while` pytaj, co w końcu zmieni warunek na fałsz.)
- sec-06-czym-jest-lista-danych: Czym jest lista danych
  (o czym: Czym jest lista danych? / Lista to jedna zmienna z wieloma wartościami w ustalonej kolejności, zapisana w nawiasach kwadratowych, z elementami rozdzielonymi przecinkami.)
- sec-06-odczyt-elementu-listy: Odczyt elementu listy
  (o czym: Jak odczytać konkretny element listy? / Element listy pobierasz indeksem w nawiasach kwadratowych, licząc od zera, a `-1` oznacza ostatni element.)
- sec-06-petla-po-elementach-listy: Pętla po elementach listy
  (o czym: Jak przejść przez wszystkie elementy listy? / Pętla `for element in lista:` wykonuje blok raz dla każdego elementu, w kolejności listy, i sama kończy pracę po ostatnim.)
- sec-07-czym-jest-funkcja: Czym jest funkcja
  (o czym: Czym jest funkcja? / Funkcję definiujesz raz przez def, a uruchamiasz każdym wywołaniem jej nazwy z nawiasami.)
- sec-07-po-co-dzielic-program-na-funkcje: Po co dzielić program na funkcje
  (o czym: Po co dzielić program na funkcje? / Funkcje dają kodowi nazwy i jedno miejsce na każdą logikę, więc program jest czytelniejszy, a poprawki robisz raz.)
- sec-07-czym-sa-argumenty-funkcji: Czym są argumenty funkcji
  (o czym: Czym są argumenty funkcji? / Argumenty to wartości podane przy wywołaniu, które trafiają do parametrów funkcji według kolejności lub nazwy, a ich liczba musi pasować do definicji.)
- sec-07-zwracanie-wyniku-przez-funkcje: Zwracanie wyniku przez funkcję
  (o czym: Co to znaczy, że funkcja zwraca wynik? / Return oddaje wartość wywołującemu, po czym kończy funkcję, a print tylko pokazuje tekst i niczego nie zwraca (funkcja bez return daje None).)
- sec-07-czytelne-nazwy-zmiennych-i-funkcji: Czytelne nazwy zmiennych i funkcji
  (o czym: Dlaczego nazwy zmiennych i funkcji powinny być czytelne? / Nazywaj funkcję według tego, co robi, a zmienną według tego, co trzyma, bo kod czyta się częściej, niż pisze.)
- sec-07-ponowne-uzycie-kodu: Ponowne użycie kodu
  (o czym: Czym jest ponowne użycie kodu? / Funkcję piszesz raz, a wywołujesz z różnymi danymi, więc poprawka w jednym miejscu naprawia wszystkie użycia.)
- sec-08-dane-wejsciowe-programu: Dane wejściowe programu
  (o czym: Czym są dane wejściowe programu? / Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.)
- sec-08-dane-wyjsciowe-programu: Dane wyjściowe programu
  (o czym: Czym są dane wyjściowe programu? / Dane wyjściowe to wynik, który program oddaje na zewnątrz (ekran, plik, inny program), a dobre wyjście jest opisane tak, by zrozumiał je człowiek.)
- sec-08-pytanie-uzytkownika-o-informacje: Pytanie użytkownika o informację
  (o czym: Jak program może zapytać użytkownika o informację? / Funkcja input wypisuje pytanie i zwraca odpowiedź użytkownika zawsze jako tekst, więc liczbę trzeba zamienić przez float().)
- sec-08-czym-jest-plik: Czym jest plik
  (o czym: Czym jest plik i jak program może z niego korzystać? / Plik przechowuje dane na dysku po zakończeniu programu, a program otwiera go przez open (najlepiej z with) w trybie czytania, zapisu lub dopisywania i pamięta, że dostaje z niego tekst.)
- sec-08-czym-jest-interfejs-uzytkownika: Czym jest interfejs użytkownika
  (o czym: Czym jest interfejs użytkownika? / Interfejs użytkownika to wszystko, przez co człowiek rozmawia z programem: pytania, które program zadaje, i wyniki, które pokazuje, więc powinny być jasne dla kogoś, kto nie zna kodu.)
- sec-08-po-co-sprawdzac-dane-uzytkownika: Po co sprawdzać dane użytkownika
  (o czym: Dlaczego program powinien sprawdzać dane wpisane przez użytkownika? / Sprawdzaj dane od użytkownika zaraz po wpisaniu, bo człowiek może wpisać coś nieoczekiwanego, a zły wpis powinien dostać komunikat i drugą szansę.)
- sec-09-blad-skladni-a-blad-logiczny: Błąd składni a błąd logiczny
  (o czym: Czym różni się błąd składni od błędu logicznego? / Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.)
- sec-09-jak-czytac-komunikat-o-bledzie: Jak czytać komunikat o błędzie
  (o czym: Jak przeczytać komunikat o błędzie? / Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.)
- sec-09-czym-jest-testowanie-programu: Czym jest testowanie programu
  (o czym: Czym jest testowanie programu? / Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.)
- sec-09-czym-jest-debugowanie: Czym jest debugowanie
  (o czym: Czym jest debugowanie? / Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.)
- sec-09-po-co-zapisywac-wersje-kodu: Po co zapisywać wersje kodu
  (o czym: Dlaczego warto zapisywać kolejne wersje kodu? / Commit zapisuje działającą wersję kodu z opisem, dzięki czemu zawsze możesz do niej wrócić i sprawdzić, kiedy coś się zepsuło.)
- sec-09-szukanie-rozwiazan-w-internecie: Szukanie rozwiązań w internecie
  (o czym: Jak szukać rozwiązań problemów programistycznych w internecie? / Szukaj po ostatniej linii komunikatu i nazwie języka, oceniaj źródła i nigdy nie wklejaj skopiowanego kodu bez zrozumienia.)
- sec-10-programy-uzywane-na-co-dzien: Programy używane na co dzień
  (o czym: Jakie są przykłady programów używanych na co dzień? / Programy, których używasz codziennie, to te same proste klocki (dane, decyzje, pętle, funkcje, pliki) w większej skali i z ładniejszym interfejsem.)
- sec-10-strona-internetowa-a-aplikacja-mobilna: Strona internetowa a aplikacja mobilna
  (o czym: Czym różni się strona internetowa od aplikacji mobilnej? / Strona otwiera się w przeglądarce bez instalacji, a aplikacja mobilna jest zainstalowana w telefonie i lepiej korzysta z jego możliwości, ale obie działają według schematu wejście, przetwarzanie, wyjście.)
- sec-10-od-pomyslu-do-dzialajacego-programu: Od pomysłu do działającego programu
  (o czym: Jak od pomysłu dojść do działającego programu? / Buduj program małymi kawałkami: opisz, napisz, sprawdź, zapisz commit, dopiero potem dokładaj następny.)
- sec-10-umiejetnosci-poza-kodowaniem: Umiejętności poza kodowaniem
  (o czym: Jakie umiejętności poza kodowaniem przydają się programiście? / Pisanie kodu to część pracy programisty; równie ważne są rozumienie problemu, komunikacja, cierpliwość i umiejętność uczenia się.)
- sec-10-od-czego-zaczac-nauke: Od czego zacząć naukę
  (o czym: Od czego zacząć samodzielną naukę programowania? / Naukę zacznij od jednego małego, własnego problemu i jednego języka, a kod pisz i uruchamiaj regularnie, po kawałku.)
- sec-10-automatyzacja-prostych-zadan: Automatyzacja prostych zadań
  (o czym: Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT? / Automatyzuj małe, częste zadania o jasnych regułach: raz opisane w pętli i funkcji działają tak samo dla trzech danych i dla tysiąca.)
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "dział-1",
      "title": "Wejdź w świat programowania"
    },
    {
      "id": "dział-2",
      "title": "Myśl krok po kroku"
    },
    {
      "id": "dział-3",
      "title": "Napisz i uruchom kod"
    },
    {
      "id": "dział-4",
      "title": "Zapamiętaj dane w zmiennych"
    },
    {
      "id": "dział-5",
      "title": "Podejmuj decyzje w programie"
    },
    {
      "id": "dział-6",
      "title": "Powtarzaj i zbieraj dane"
    },
    {
      "id": "dział-7",
      "title": "Uporządkuj kod funkcjami"
    },
    {
      "id": "dział-8",
      "title": "Porozmawiaj z użytkownikiem"
    },
    {
      "id": "dział-9",
      "title": "Oswój błędy w kodzie"
    },
    {
      "id": "dział-10",
      "title": "Zastosuj wiedzę w praktyce"
    },
    {
      "id": "sec-01-czym-jest-program-komputerowy",
      "title": "Zrozum, czym jest program"
    },
    {
      "id": "sec-01-czym-jest-programowanie",
      "title": "Odkryj sens programowania"
    },
    {
      "id": "sec-01-kim-jest-programista",
      "title": "Przyjrzyj się pracy programisty"
    },
    {
      "id": "sec-01-czym-jest-jezyk-programowania",
      "title": "Poznaj język programowania"
    },
    {
      "id": "sec-01-po-co-komputerowi-precyzja",
      "title": "Podawaj komputerowi każdy szczegół"
    },
    {
      "id": "sec-01-program-a-aplikacja",
      "title": "Odróżnij program od aplikacji"
    },
    {
      "id": "sec-02-czym-jest-algorytm",
      "title": "Zdefiniuj algorytm"
    },
    {
      "id": "sec-02-przepis-jako-algorytm",
      "title": "Porównaj przepis z algorytmem"
    },
    {
      "id": "sec-02-kolejnosc-krokow-algorytmu",
      "title": "Pilnuj kolejności kroków"
    },
    {
      "id": "sec-02-czym-jest-schemat-blokowy",
      "title": "Narysuj schemat blokowy"
    },
    {
      "id": "sec-02-podzial-problemu-na-czesci",
      "title": "Rozłóż problem na części"
    },
    {
      "id": "sec-02-poprawny-algorytm",
      "title": "Sprawdź poprawność algorytmu"
    },
    {
      "id": "sec-03-czym-jest-kod-zrodlowy",
      "title": "Poznaj kod źródłowy"
    },
    {
      "id": "sec-03-do-czego-sluzy-edytor",
      "title": "Pisz kod w edytorze"
    },
    {
      "id": "sec-03-co-znaczy-uruchomic-program",
      "title": "Uruchom swój program"
    },
    {
      "id": "sec-03-kompilator-i-interpreter",
      "title": "Odróżnij kompilator od interpretera"
    },
    {
      "id": "sec-03-co-to-jest-blad-w-programie",
      "title": "Rozpoznaj błąd w programie"
    },
    {
      "id": "sec-03-do-czego-sluza-komentarze",
      "title": "Opisuj kod komentarzami"
    },
    {
      "id": "sec-04-czym-jest-dana",
      "title": "Zobacz, czym jest dana"
    },
    {
      "id": "sec-04-czym-jest-zmienna",
      "title": "Nazwij swoją pierwszą zmienną"
    },
    {
      "id": "sec-04-zmienna-jako-pudelko-z-etykieta",
      "title": "Wyobraź sobie pudełko z etykietą"
    },
    {
      "id": "sec-04-liczba-a-tekst",
      "title": "Rozróżnij liczbę i tekst"
    },
    {
      "id": "sec-04-czym-jest-typ-danych",
      "title": "Sprawdź typ danych"
    },
    {
      "id": "sec-04-wartosc-logiczna-prawda-falsz",
      "title": "Użyj prawdy i fałszu"
    },
    {
      "id": "sec-04-przypisanie-wartosci-do-zmiennej",
      "title": "Przypisz wartość zmiennej"
    },
    {
      "id": "sec-05-dzialania-matematyczne-w-programie",
      "title": "Wykonuj działania matematyczne"
    },
    {
      "id": "sec-05-laczenie-tekstow",
      "title": "Połącz kilka tekstów"
    },
    {
      "id": "sec-05-porownywanie-wartosci",
      "title": "Porównaj dwie wartości"
    },
    {
      "id": "sec-05-instrukcja-warunkowa-jesli-to",
      "title": "Zapisz warunek z if"
    },
    {
      "id": "sec-05-czesc-w-przeciwnym-razie",
      "title": "Dodaj drugą drogę"
    },
    {
      "id": "sec-05-operatory-i-oraz-lub",
      "title": "Łącz warunki spójnikami"
    },
    {
      "id": "sec-06-czym-jest-petla",
      "title": "Powtórz kod pętlą"
    },
    {
      "id": "sec-06-kiedy-siegnac-po-petle",
      "title": "Zastąp kopiowanie pętlą"
    },
    {
      "id": "sec-06-petla-nieskonczona",
      "title": "Unikaj pętli nieskończonej"
    },
    {
      "id": "sec-06-czym-jest-lista-danych",
      "title": "Zbierz dane w liście"
    },
    {
      "id": "sec-06-odczyt-elementu-listy",
      "title": "Wybierz element z listy"
    },
    {
      "id": "sec-06-petla-po-elementach-listy",
      "title": "Przejdź przez całą listę"
    },
    {
      "id": "sec-07-czym-jest-funkcja",
      "title": "Zdefiniuj i wywołaj funkcję"
    },
    {
      "id": "sec-07-po-co-dzielic-program-na-funkcje",
      "title": "Podziel program na funkcje"
    },
    {
      "id": "sec-07-czym-sa-argumenty-funkcji",
      "title": "Przekaż funkcji argumenty"
    },
    {
      "id": "sec-07-zwracanie-wyniku-przez-funkcje",
      "title": "Odbierz wynik z funkcji"
    },
    {
      "id": "sec-07-czytelne-nazwy-zmiennych-i-funkcji",
      "title": "Nadawaj czytelne nazwy"
    },
    {
      "id": "sec-07-ponowne-uzycie-kodu",
      "title": "Wykorzystaj kod ponownie"
    },
    {
      "id": "sec-08-dane-wejsciowe-programu",
      "title": "Przyjmij dane z zewnątrz"
    },
    {
      "id": "sec-08-dane-wyjsciowe-programu",
      "title": "Pokaż wynik programu"
    },
    {
      "id": "sec-08-pytanie-uzytkownika-o-informacje",
      "title": "Zapytaj użytkownika o dane"
    },
    {
      "id": "sec-08-czym-jest-plik",
      "title": "Zapisz dane w pliku"
    },
    {
      "id": "sec-08-czym-jest-interfejs-uzytkownika",
      "title": "Zaprojektuj jasny interfejs"
    },
    {
      "id": "sec-08-po-co-sprawdzac-dane-uzytkownika",
      "title": "Weryfikuj wpisane dane"
    },
    {
      "id": "sec-09-blad-skladni-a-blad-logiczny",
      "title": "Rozróżnij dwa rodzaje błędów"
    },
    {
      "id": "sec-09-jak-czytac-komunikat-o-bledzie",
      "title": "Czytaj komunikat o błędzie"
    },
    {
      "id": "sec-09-czym-jest-testowanie-programu",
      "title": "Przetestuj swój program"
    },
    {
      "id": "sec-09-czym-jest-debugowanie",
      "title": "Wytrop błąd krok po kroku"
    },
    {
      "id": "sec-09-po-co-zapisywac-wersje-kodu",
      "title": "Zapisuj wersje kodu"
    },
    {
      "id": "sec-09-szukanie-rozwiazan-w-internecie",
      "title": "Szukaj rozwiązań w sieci"
    },
    {
      "id": "sec-10-programy-uzywane-na-co-dzien",
      "title": "Odkryj programy wokół siebie"
    },
    {
      "id": "sec-10-strona-internetowa-a-aplikacja-mobilna",
      "title": "Przeanalizuj stronę i aplikację mobilną"
    },
    {
      "id": "sec-10-od-pomyslu-do-dzialajacego-programu",
      "title": "Dojdź od pomysłu do programu"
    },
    {
      "id": "sec-10-umiejetnosci-poza-kodowaniem",
      "title": "Rozwijaj umiejętności poza kodem"
    },
    {
      "id": "sec-10-od-czego-zaczac-nauke",
      "title": "Zacznij naukę od małego problemu"
    },
    {
      "id": "sec-10-automatyzacja-prostych-zadan",
      "title": "Zautomatyzuj proste zadania"
    }
  ]
}
````
