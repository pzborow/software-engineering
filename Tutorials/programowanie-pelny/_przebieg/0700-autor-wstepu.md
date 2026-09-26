# Krok 0700 · autor_wstępu

Węzeł: `open_chapter` · dział: 7 · pytanie: — · próba: 1

## Prompt

````text
Jesteś autorem tutorialu. Piszesz wprowadzenie do działu 07: "Funkcje i porządek w kodzie".
Tutorial: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Napisz 3-6 zdań, najwyżej 150 słów: po co jest ten dział (jaki problem czytelnika rozwiązuje), co czytelnik będzie umiał po jego przeczytaniu i jak dział łączy się z poprzednimi. Nie wyliczaj sekcji, spis sekcji dołączamy pod wstępem. Definicje i przykłady należą do sekcji, wstęp tylko zapowiada. Możesz dodać mały diagram tekstowy.
Przykład przewodni (Rozliczenie wspólnych wydatków „Wspólna Kasa”) w tym dziale: Kod dzieli się na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby z czytelnymi nazwami, argumentami i zwracanymi wynikami, gotowe do ponownego użycia.. Możesz to zapowiedzieć jednym zdaniem.
Warsztat (Wspólna Kasa krok po kroku) w tym dziale: Kod jest dzielony na funkcje suma(wydatki) i na_osobe(suma, osoby) z argumentami i wartością zwracaną oraz czytelnymi nazwami, a funkcje są używane ponownie dla dwóch różnych wyjazdów.. Możesz to zapowiedzieć jednym zdaniem.

Diagram (opcjonalny): maks. 10 linii, znaki ASCII/strzałki, bez ogrodzenia ```.

Pytania, na które odpowie ten dział:
- 38. Czym jest funkcja?
- 39. Po co dzielić program na funkcje?
- 40. Czym są argumenty funkcji?
- 41. Co to znaczy, że funkcja zwraca wynik?
- 42. Dlaczego nazwy zmiennych i funkcji powinny być czytelne?
- 43. Czym jest ponowne użycie kodu?

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
Dział 05. Operacje i decyzje
  - Działania matematyczne w programie: Python zna siedem podstawowych operatorów arytmetycznych (`+ - * / // % **`); na tekście dzielić się nie da, a `+` i `*` znaczą tam sklejanie i powtarzanie.
  - Łączenie tekstów: Plus skleja tylko tekst z tekstem, bez dodawania spacji, a liczbę trzeba przed sklejeniem zamienić funkcją str() albo użyć zapisu z f.
  - Porównywanie wartości: Operatory porównania (`==`, `!=`, `<`, `>`, `<=`, `>=`) dają `True` albo `False`, a `==` pyta o równość, w przeciwieństwie do `=`, które przypisuje.
  - Instrukcja warunkowa „jeśli… to…”: Instrukcja `if` wykonuje wcięte pod nią linie tylko wtedy, gdy warunek daje `True`; w przeciwnym razie Python je pomija.
  - Część „w przeciwnym razie”: `else` to droga „w przeciwnym razie”: wykonuje się tylko wtedy, gdy warunek z `if` jest fałszywy, więc program zawsze wybiera dokładnie jedną z dwóch dróg.
  - Operatory „i” oraz „lub”: `and` wymaga prawdziwości obu warunków, a `or` wystarczy jeden prawdziwy, żeby całość dała `True`.
Dział 06. Powtarzanie i kolekcje
  - Czym jest pętla: Pętla powtarza wcięty fragment kodu, a `for` robi to raz dla każdego elementu zestawu danych, po czym kończy pracę.
  - Kiedy sięgnąć po pętlę: Gdy kopiujesz linię i zmieniasz w niej tylko jedną wartość, użyj pętli: jeden zapis obsłuży dowolną liczbę elementów.
  - Pętla nieskończona: Pętla nieskończona nigdy nie osiąga warunku zakończenia, więc program się „zawiesza”; zatrzymasz go Ctrl+C, a przy każdym `while` pytaj, co w końcu zmieni warunek na fałsz.
  - Czym jest lista danych: Lista to jedna zmienna z wieloma wartościami w ustalonej kolejności, zapisana w nawiasach kwadratowych, z elementami rozdzielonymi przecinkami.
  - Odczyt elementu listy: Element listy pobierasz indeksem w nawiasach kwadratowych, licząc od zera, a `-1` oznacza ostatni element.
  - Pętla po elementach listy: Pętla `for element in lista:` wykonuje blok raz dla każdego elementu, w kolejności listy, i sama kończy pracę po ostatnim.

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
- operator-arytmetyczny: operator arytmetyczny
- konkatenacja: konkatenacja
- operator-porownania: operator porównania
- instrukcja-warunkowa: instrukcja warunkowa
- wciecie: wcięcie
- operator-logiczny: operator logiczny
- petla: pętla
- iteracja: iteracja
- petla-nieskonczona: pętla nieskończona
- lista-danych: lista danych
- element-listy: element listy
- indeks: indeks
````

## Odpowiedź

````json
{
  "intro": "Gdy program rośnie, te same obliczenia zaczynają się powtarzać, a kod trudno przeczytać i poprawić. Ten dział pokazuje, jak zamknąć kawałek pracy w funkcji: nadać jej czytelną nazwę, przekazać dane i odebrać wynik. Po lekturze będziesz umieć dzielić program na małe, nazwane części i używać ich wielokrotnie, tak jak dzielisz problem na kroki (dział 02), a pętle i listy (dział 06) trzymasz w porządku. Na przykładzie „Wspólnej Kasy” rozbijemy rozliczenie na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby, a w warsztacie użyjemy suma(wydatki) i na_osobe(suma, osoby) dla dwóch różnych wyjazdów.",
  "diagram": "wydatki ──► suma(wydatki) ──► suma\nsuma, osoby ──► na_osobe(suma, osoby) ──► kwota",
  "new_terms": []
}
````
