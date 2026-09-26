# Krok 1263 · redaktor_linków

Węzeł: `review_links` · dział: 2 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 02 „Algorytmy i myślenie krokowe” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-15] fraza: „czworo znajomych na wyjeździe, którzy płacili na zmianę” (wstecz, przykład wspólnych wydatków z poprzedniego działu)
  zdanie: Weźmy czworo znajomych na wyjeździe, którzy płacili na zmianę. Rozliczenie da się opisać tak:
  cel: [Czym jest program komputerowy] Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

[ref-16] fraza: „Na razie nie piszemy kodu” (w przód, zapowiedź, że kod pojawi się w dalszych działach)
  zdanie: Na razie nie piszemy kodu: to celowo zwykły język. Ten sam algorytm można potem zapisać w Pythonie, w arkuszu kalkulacyjnym albo wykonać ręcznie. Właśnie dlatego warto go oddzielać od kodu.
  cel: [Do czego służą komentarze] Komentarz to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi. W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. Interpreter pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją. ```python # rozlicz.py - rozliczenie wspólnych wydatków print("Wspólna Kasa") #

[ref-17] fraza: „cztery kroki rozliczenia, które już znasz” (wstecz, algorytm rozliczenia w czterech krokach z poprzedniej sekcji)
  zdanie: Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”. Jej przepis to cztery kroki rozliczenia, które już znasz: składniki to wydatki i liczba osób, a „danie” to saldo każdego.
  cel: [Czym jest algorytm] ```text dane: lista wydatków (kto, ile) i liczba osób 1. Zsumuj wszystkie wydatki. 2. Podziel sumę przez liczbę osób: to udział jednej osoby. 3. Dla każdej osoby odejmij udział od tego, ile wydała. 4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna. wynik: saldo każdej osoby ```

[ref-19] fraza: „Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”” (w przód, zapowiedź, że Wspólna Kasa wraca w kolejnych działach)
  zdanie: Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”. Jej przepis to cztery kroki rozliczenia, które już znasz: składniki to wydatki i liczba osób, a „danie” to saldo każdego.
  cel: [Czym jest kod źródłowy] Kod źródłowy zapisujemy w pliku o rozszerzeniu zależnym od języka. Pliki Pythona kończą się na `.py`. Taki plik będzie miał nasz przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Zaczyna się od pliku `rozlicz.py`:

[ref-20] fraza: „cztery kroki rozliczenia” (wstecz, algorytm rozliczenia w czterech krokach z poprzedniego działu)
  zdanie: Weźmy cztery kroki rozliczenia we „Wspólnej Kasie”. Ala wydała 60 zł, Bartek 40 zł, Czarek 20 zł. Najpierw sumujemy: 120 zł. Potem dzielimy przez trzy osoby: udział wynosi 40 zł. Na końcu odejmujemy udział od wpłaty każdego.
  cel: [Czym jest algorytm] ```text dane: lista wydatków (kto, ile) i liczba osób 1. Zsumuj wszystkie wydatki. 2. Podziel sumę przez liczbę osób: to udział jednej osoby. 3. Dla każdej osoby odejmij udział od tego, ile wydała. 4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna. wynik: saldo każdej osoby ```

[ref-21] fraza: „we „Wspólnej Kasie”” (wstecz, przykładowy program Wspólna Kasa, rozwijany od działu 01)
  zdanie: Weźmy cztery kroki rozliczenia we „Wspólnej Kasie”. Ala wydała 60 zł, Bartek 40 zł, Czarek 20 zł. Najpierw sumujemy: 120 zł. Potem dzielimy przez trzy osoby: udział wynosi 40 zł. Na końcu odejmujemy udział od wpłaty każdego.
  cel: [Czym jest program komputerowy] Program komputerowy to zapisany z góry ciąg poleceń, które komputer wykonuje krok po kroku, żeby zamienić dane na wynik. Komputer sam nic nie wie ani nie zgaduje: robi dokładnie to, co mu zapisano. Pojedyncze polecenie to instrukcja, czyli jeden mały, jednoznaczny krok, np. „dodaj dwie liczby” albo „wypisz tekst na ekranie”. Program to wiele takich instrukcji ułożonych w określonej kolejności. Kalkulator, przeglądarka i gra działają tak samo, tylko mają in

[ref-22] fraza: „rozliczenie „Wspólnej Kasy” z trzema osobami” (wstecz, algorytm rozliczenia Wspólnej Kasy z poprzedniego działu)
  zdanie: Oto rozliczenie „Wspólnej Kasy” z trzema osobami, narysowane znakami tekstowymi:
  cel: [Czym jest algorytm] ```text dane: lista wydatków (kto, ile) i liczba osób 1. Zsumuj wszystkie wydatki. 2. Podziel sumę przez liczbę osób: to udział jednej osoby. 3. Dla każdej osoby odejmij udział od tego, ile wydała. 4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna. wynik: saldo każdej osoby ```

[ref-24] fraza: „przykład, który będzie nam towarzyszył” (w przód, Wspólna Kasa wraca w kolejnych działach)
  zdanie: Konsekwencja: schemat pozwala sprawdzić algorytm na kartce, zanim powstanie kod. Wrócimy do niego przy podziale problemu na części, a „Wspólna Kasa”, przykład, który będzie nam towarzyszył, dostanie z niego kod dopiero później.
  cel: [Do czego służą komentarze] Komentarz to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi. W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. Interpreter pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją. ```python # rozlicz.py - rozliczenie wspólnych wydatków print("Wspólna Kasa") #

[ref-25] fraza: „dostanie z niego kod dopiero później” (w przód, kod Wspólnej Kasy pojawi się w dalszych działach)
  zdanie: Konsekwencja: schemat pozwala sprawdzić algorytm na kartce, zanim powstanie kod. Wrócimy do niego przy podziale problemu na części, a „Wspólna Kasa”, przykład, który będzie nam towarzyszył, dostanie z niego kod dopiero później.
  cel: [Czym jest kod źródłowy] ```python # rozlicz.py print("Wspólna Kasa") print(300 / 3) ```

[ref-26] fraza: „schematu blokowego z poprzedniej sekcji” (wstecz, schemat blokowy jako narzędzie podziału problemu na kroki-ramki)
  zdanie: Weźmy „rozlicz wyjazd”. To za dużo naraz, więc rozbijamy to na trzy części. Wracamy tu do schematu blokowego z poprzedniej sekcji: kroki w jego ramkach to gotowe kandydatki na części.
  cel: [Czym jest schemat blokowy] Schemat blokowy to rysunek algorytmu: każdy krok jest w ramce, a strzałki pokazują, w jakiej kolejności je wykonać. Działa jak mapa, po której palcem przejdziesz od początku do końca. Używa kilku umownych kształtów. Owal oznacza początek albo koniec, prostokąt to zwykły krok, a romb to pytanie, po którym droga rozwidla się na „tak” i „nie”. Krok wykonujesz, gdy dojdziesz do niego strzałką, a nie dlatego, że stoi niżej na kartce. Oto rozliczenie „Wspólnej Kasy”

[ref-27] fraza: „tak jak w sekcji o kolejności kroków” (wstecz, zależności między krokami wyznaczają kolejność)
  zdanie: Każda część ma jasne wejście i wynik. Część 3 potrzebuje wyniku części 2, a ta wyniku części 1, więc kolejność wynika z tych zależności, tak jak w sekcji o kolejności kroków.
  cel: [Kolejność kroków algorytmu] Kolejność ma znaczenie, bo prawie każdy krok korzysta z wyniku poprzedniego. Zamiana miejsc sprawia, że krok dostaje dane, których jeszcze nie ma, i algorytm daje zły wynik albo wcale nie działa. Weźmy cztery kroki rozliczenia we „Wspólnej Kasie”. Ala wydała 60 zł, Bartek 40 zł, Czarek 20 zł. Najpierw sumujemy: 120 zł. Potem dzielimy przez trzy osoby: udział wynosi 40 zł. Na końcu odejmujemy udział od wpłaty każdego. Teraz zamieńmy kroki: odejmujemy udział, zanim go policzyliśmy.

[ref-28] fraza: „takie części zamienimy w osobne” (w przód, części staną się funkcjami)
  zdanie: Konsekwencja: w programie takie części zamienimy w osobne funkcje, czyli nazwane fragmenty kodu do wielokrotnego użycia. Ich nazwy, np. `suma_wydatkow`, poznasz później, gdy zaczniemy pisać „Wspólną Kasę”, przykład, który będzie nam towarzyszył w kolejnych działach.
  cel: [Czym jest funkcja] Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:

[ref-29] fraza: „Ich nazwy, np. `suma_wydatkow`, poznasz później” (w przód, nazywanie funkcji, np. suma_wydatkow)
  zdanie: Konsekwencja: w programie takie części zamienimy w osobne funkcje, czyli nazwane fragmenty kodu do wielokrotnego użycia. Ich nazwy, np. `suma_wydatkow`, poznasz później, gdy zaczniemy pisać „Wspólną Kasę”, przykład, który będzie nam towarzyszył w kolejnych działach.
  cel: [Czytelne nazwy zmiennych i funkcji] Funkcję nazywaj tak, by opisywała, co robi (`suma_wydatkow`), a zmienną tak, by opisywała, co trzyma (`liczba_osob`). Zwykle małe litery, słowa rozdzielone podkreśleniem, bez polskich znaków, tak jak w całym tutorialu.

[ref-30] fraza: „przykład, który będzie nam towarzyszył w kolejnych działach” (w przód, Wspólna Kasa wraca w kolejnych działach)
  zdanie: Konsekwencja: w programie takie części zamienimy w osobne funkcje, czyli nazwane fragmenty kodu do wielokrotnego użycia. Ich nazwy, np. `suma_wydatkow`, poznasz później, gdy zaczniemy pisać „Wspólną Kasę”, przykład, który będzie nam towarzyszył w kolejnych działach.
  cel: [Kompilator i interpreter] Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania. Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie. W praktyce Python najpierw przekłada plik na pośredni zapis, ale z Twojej strony to jedno polecenie.

[ref-31] fraza: „w naszej liście kroków jest zdanie „Resztę groszy dopisz pierwszej osobie.”” (wstecz, krok listy rozliczenia, który rozdziela niepodzielną resztę groszy)
  zdanie: Dla 120 zł na czworo wszystko się zgadza. Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza. Dlatego w naszej liście kroków jest zdanie „Resztę groszy dopisz pierwszej osobie.”: bez niego algorytm byłby niepoprawny, choć pierwszy przykład by przeszedł.
  cel: [Po co komputerowi precyzja] ```text 1. Weź kwoty wydatków z listy wpisanej przez użytkownika. 2. Dodaj je do siebie. 3. Podziel sumę przez 4, bo tyle jest osób. 4. Zaokrąglij w dół do pełnych groszy. 5. Resztę groszy dopisz pierwszej osobie. 6. Wypisz wynik na ekranie. ```

[ref-32] fraza: „Do systematycznego sprawdzania wrócimy przy testowaniu programu” (w przód, testowanie programu jako systematyczne sprawdzanie na wielu danych)
  zdanie: Konsekwencja: poprawność sprawdzasz na wielu danych, w tym celowo niewygodnych. Do systematycznego sprawdzania wrócimy przy testowaniu programu.
  cel: [Czym jest testowanie programu] Testowanie to systematyczne sprawdzanie programu na wielu danych, dla których z góry znasz poprawny wynik. Zamiast raz spojrzeć na ekran i uznać, że „wygląda dobrze”, zapisujesz oczekiwania i pozwalasz komputerowi je porównać.
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-15",
      "keep": true,
      "reason": "Cel opisuje dokładnie ten przykład wyjazdu ze wspólnymi wydatkami."
    },
    {
      "id": "ref-16",
      "keep": false,
      "reason": "Zapowiedź ramowa; cel (komentarze) nie mówi nic o tym, że kod pojawi się później."
    },
    {
      "id": "ref-17",
      "keep": true,
      "reason": "Cel zawiera listę czterech kroków rozliczenia, o której mówi fraza."
    },
    {
      "id": "ref-19",
      "keep": false,
      "reason": "Zapowiedź ramowa; cel o kodzie źródłowym tylko wspomina przykład, nie wyjaśnia go."
    },
    {
      "id": "ref-20",
      "keep": true,
      "reason": "Cel pokazuje pełną listę czterech kroków, do której fraza się odwołuje."
    },
    {
      "id": "ref-21",
      "keep": false,
      "reason": "Cel to ogólna definicja programu, nie opisuje Wspólnej Kasy; fraza to ogólnik."
    },
    {
      "id": "ref-22",
      "keep": true,
      "reason": "Cel zawiera algorytm rozliczenia, który schemat ilustruje."
    },
    {
      "id": "ref-24",
      "keep": false,
      "reason": "Zapowiedź ramowa; cel (komentarze) jest przypadkowy."
    },
    {
      "id": "ref-25",
      "keep": false,
      "reason": "Zapowiedź kodu na później; cel pokazuje tylko trywialny fragment, nie kod Wspólnej Kasy."
    },
    {
      "id": "ref-26",
      "keep": true,
      "reason": "Cel to sekcja o schemacie blokowym, o której mowa we frazie."
    },
    {
      "id": "ref-27",
      "keep": true,
      "reason": "Cel to sekcja o kolejności kroków, wprost wskazana we frazie."
    },
    {
      "id": "ref-28",
      "keep": false,
      "reason": "Cel to funkcja z pętlą sumującą, a fraza jest zapowiedzią; czytelnik dostałby za dużo za wcześnie."
    },
    {
      "id": "ref-29",
      "keep": true,
      "reason": "Cel wyjaśnia nazywanie funkcji na przykładzie suma_wydatkow."
    },
    {
      "id": "ref-30",
      "keep": false,
      "reason": "Zapowiedź ramowa; cel o kompilatorze i interpreterze jest przypadkowy."
    },
    {
      "id": "ref-31",
      "keep": true,
      "reason": "Cel pokazuje listę kroków z omawianym zdaniem o resztce groszy."
    },
    {
      "id": "ref-32",
      "keep": true,
      "reason": "Cel to sekcja o testowaniu programu, dokładnie to, o czym mówi fraza."
    }
  ]
}
````
