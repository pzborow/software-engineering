# Krok 0449 · autor_wstępu

Węzeł: `open_chapter` · dział: 5 · pytanie: — · próba: 2

## Prompt

````text
Jesteś autorem tutorialu. Piszesz wprowadzenie do działu 05: "Operacje i decyzje".
Tutorial: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Napisz 3-6 zdań, najwyżej 150 słów: po co jest ten dział (jaki problem czytelnika rozwiązuje), co czytelnik będzie umiał po jego przeczytaniu i jak dział łączy się z poprzednimi. Nie wyliczaj sekcji, spis sekcji dołączamy pod wstępem. Definicje i przykłady należą do sekcji, wstęp tylko zapowiada. Możesz dodać mały diagram tekstowy.
Przykład przewodni (Rozliczenie wspólnych wydatków „Wspólna Kasa”) w tym dziale: Program liczy udział jednej osoby, skleja tekst podsumowania i decyduje if/else oraz operatorami and/or, czy ktoś jest winien pieniądze, czy ma dostać zwrot.. Możesz to zapowiedzieć jednym zdaniem.
Warsztat (Wspólna Kasa krok po kroku) w tym dziale: Program liczy koszt na osobę (dzielenie kwoty przez liczbę osób), skleja teksty w zdanie i za pomocą if/else oraz operatorów and/or ocenia, czy wydatek jest duży.. Możesz to zapowiedzieć jednym zdaniem.

Diagram (opcjonalny): maks. 10 linii, znaki ASCII/strzałki, bez ogrodzenia ```.

Pytania, na które odpowie ten dział:
- 26. Jakie podstawowe działania matematyczne może wykonać program?
- 27. Jak program łączy ze sobą teksty?
- 28. Jak program porównuje dwie wartości?
- 29. Czym jest instrukcja warunkowa „jeśli… to…”?
- 30. Do czego służy część „w przeciwnym razie”?
- 31. Do czego służą operatory „i” oraz „lub”?

Dotychczasowe działy i sekcje:
Dział 01. Czym jest programowanie
  - Czym jest program komputerowy: Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
  - Czym jest programowanie: Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.
  - Kim jest programista: Programista zamienia potrzebę na działający program, a pisanie kodu to tylko jeden z etapów tej pracy.
  - Czym jest język programowania: Język programowania to ścisły zestaw słów i reguł zapisu, dzięki któremu człowiek wyraża instrukcje tak, by komputer wykonał je jednoznacznie.
  - Po co komputerowi precyzja: Komputer wykonuje dokładnie to, co zapisano, więc każdy szczegół, który człowiek by sobie dopowiedział, trzeba podać wprost.
  - Program a aplikacja: Aplikacja to program z oprawą dla użytkownika, więc każda aplikacja jest programem, ale nie odwrotnie.
Dział 02. Algorytmy i myślenie krokowe
  - Czym jest algorytm: Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
  - Przepis jako algorytm: Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
  - Kolejność kroków algorytmu: Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.
  - Czym jest schemat blokowy: Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, dzięki czemu rozgałęzienia, powroty i koniec widać, zanim powstanie kod.
  - Podział problemu na części: Dziel problem na części z jasnym wejściem i wynikiem, aż każdą da się opisać jednym zdaniem i sprawdzić osobno.
  - Poprawny algorytm: Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, także w przypadkach brzegowych.
Dział 03. Kod i jego uruchamianie
  - Czym jest kod źródłowy: Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
  - Do czego służy edytor: Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.
  - Co znaczy uruchomić program: Uruchomienie programu to polecenie, by Python wykonał instrukcje z pliku po kolei, a sam plik pozostaje bez zmian.
  - Kompilator i interpreter: Kompilator tłumaczy cały kod na osobny plik przed startem, a interpreter wykonuje kod na bieżąco, dlatego w Pythonie wystarczy zapisać i uruchomić.
  - Co to jest błąd w programie: Błąd to rozbieżność między zamiarem a działaniem programu: czasem zatrzymuje go komunikat, a czasem zły wynik pojawia się po cichu.
  - Do czego służą komentarze: Komentarz zaczyna się od `#`, jest pomijany przez Pythona i ma wyjaśniać powód, a nie powtarzać kod; po zmianie kodu trzeba go zaktualizować.
Dział 04. Dane i zmienne
  - Czym jest dana: Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.
  - Czym jest zmienna: Zmienna to nazwa, pod którą program przechowuje daną, żeby móc jej użyć wielokrotnie i w razie potrzeby zmienić.
  - Zmienna jako pudełko z etykietą: Zmienna to pudełko z etykietą: nazwa zostaje, w środku jest jedna wartość, którą można podmienić, a kopie są niezależne.
  - Liczba a tekst: Cudzysłów zmienia rodzaj danych: 45.5 to liczba, którą można dzielić, a "45.5" to tekst, którego dzielić się nie da.
  - Czym jest typ danych: Typ danych to rodzaj wartości (str, int, float, bool), który decyduje o tym, jakie działania są na niej możliwe.
  - Wartość logiczna prawda/fałsz: Wartość logiczna (`bool`) to `True` albo `False`, zapisywane z wielkiej litery i bez cudzysłowu, a program używa jej do podejmowania decyzji.
  - Przypisanie wartości do zmiennej: Przypisanie `=` to polecenie zapisania wartości z prawej strony pod nazwą z lewej, a o wartości zmiennej decyduje ostatnie wykonane przypisanie.

Glosariusz (id: termin):
- program-komputerowy: program komputerowy
- instrukcja: instrukcja
- programista: programista
- programowanie: programowanie
- jezyk-programowania: język programowania
- kod: kod
- skladnia: składnia
- aplikacja: aplikacja
- algorytm: algorytm
- warunek-zakonczenia: warunek zakończenia
- schemat-blokowy: schemat blokowy
- funkcja: funkcja
- specyfikacja-wyniku: specyfikacja wyniku
- przypadek-brzegowy: przypadek brzegowy
- kod-zrodlowy: kod źródłowy
- edytor-kodu: edytor kodu
- podswietlanie-skladni: podświetlanie składni
- python: Python
- terminal: terminal
- kompilator: kompilator
- interpreter: interpreter
- blad-w-programie: błąd w programie
- print: print
- komentarz: komentarz
- dana: dana
- zmienna: zmienna
- wartosc-zmiennej: wartość zmiennej
- typ-danych: typ danych
- wartosc-logiczna: wartość logiczna
- przypisanie: przypisanie

POPRZEDNIA WERSJA (wstęp i diagram):
Dotąd program tylko przechowywał dane w zmiennych; w tym dziale nauczy się z nimi coś robić. Po jego przeczytaniu policzysz wynik z liczb, sklejisz z tekstów zdanie, porównasz dwie wartości i sprawisz, że program wybierze jedną z dróg, zamiast zawsze robić to samo. Wykorzystasz zmienne i typy z poprzedniego działu oraz rozgałęzienia ze schematów blokowych z działu 2. W przykładzie „Wspólna Kasa” program policzy koszt na osobę i zdecyduje, czy ktoś jest winien pieniądze, czy ma dostać zwrot, a w warsztacie oceni, czy wydatek jest duży.

Diagram:
dane (zmienne) → działania → porównanie → decyzja
 kwota, osoby     kwota / osoby   > ?      if / else

POTRZEBY DO SPEŁNIENIA:
- [diagram] diagram: „> ?” pod „porównanie” i „if / else” pod „decyzja”: Diagram używa skrótów, których czytelnik jeszcze nie zna: „if / else” (angielskie słowa, w tekście wstępu w ogóle nie padają) i „> ?”. Zastąp je opisami po polsku, spójnymi z pytaniami działu, np. „jeśli… to… / w przeciwnym razie”, a porównanie zapisz zrozumiale, np. „czy kwota jest większa niż…?”. Ukośnik w „kwota / osoby” może się kojarzyć z „albo”; lepiej użyć „kwota ÷ osoby” lub „kwota podzielona na osoby”.
- [diagram] diagram: układ etykiet pod strzałkami: Przykładowe wartości („kwota, osoby”, „kwota / osoby”, „> ?”, „if / else”) są ustawione w drugiej linii bez jasnego przypisania do etapów; w terminalu spacje łatwo się rozjadą i nie widać, która etykieta należy do którego pola. Narysuj pionowo albo w pudełkach, tak by każdy przykład był bezpośrednio pod swoim etapem. Dodaj też, co wynika z porównania (dwie ścieżki: tak/nie), bo dziś „decyzja” wisi bez wyniku.
````

## Odpowiedź

````json
{
  "intro": "Dotąd program tylko przechowywał dane w zmiennych; w tym dziale nauczy się z nimi coś robić. Po jego przeczytaniu policzysz wynik z liczb, sklejisz z tekstów zdanie, porównasz dwie wartości i sprawisz, że program wybierze jedną z dróg, zamiast zawsze robić to samo. Wykorzystasz zmienne i typy z poprzedniego działu oraz rozgałęzienia ze schematów blokowych z działu 2. W przykładzie „Wspólna Kasa” program policzy udział jednej osoby i zdecyduje, czy ktoś jest winien pieniądze, czy ma dostać zwrot, a w warsztacie oceni, czy wydatek jest duży.",
  "diagram": "1. Dane (zmienne):        kwota, liczba osób\n          ↓\n2. Działanie:            kwota podzielona przez liczbę osób\n          ↓\n3. Porównanie:           czy koszt jest większy niż limit?\n          ↓\n4. Decyzja:              jeśli tak → jedna droga\n                         w przeciwnym razie → druga droga"
}
````
