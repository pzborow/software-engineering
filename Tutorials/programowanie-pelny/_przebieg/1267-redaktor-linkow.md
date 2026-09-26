# Krok 1267 · redaktor_linków

Węzeł: `review_links` · dział: 6 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 06 „Powtarzanie i kolekcje” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-75] fraza: „jej zapis omówimy osobno” (w przód, zapis listy danych w nawiasach kwadratowych)
  zdanie: Jedno powtórzenie fragmentu nazywamy iteracją. Pętla `for` wykonuje po jednej iteracji dla każdego elementu z zestawu danych. Taki zestaw to na razie po prostu lista wartości w nawiasach kwadratowych; jej zapis omówimy osobno.
  cel: [Czym jest lista danych] Listę zapisujesz w nawiasach kwadratowych, a wartości oddzielasz przecinkami. Każda wartość to element listy, czyli jedno miejsce w zestawie. Tekst ma cudzysłów, liczba nie, tak samo jak przy zwykłych zmiennych.

[ref-76] fraza: „tak samo jak przy `if`” (wstecz, wcięcie oznaczające ciało bloku)
  zdanie: Wcięte linie pod `for` to ciało pętli, tak samo jak przy `if`. Nazwa po słowie `for` to zmienna, która w każdej iteracji dostaje kolejny element:
  cel: [Instrukcja warunkowa „jeśli… to…”] Instrukcja warunkowa to polecenie, które wykonuje wybrany fragment kodu tylko wtedy, gdy warunek jest prawdziwy. W Pythonie zapisujemy ją słowem `if`, czyli „jeśli”. Warunek to zwykle porównanie z poprzedniej sekcji, bo daje `True` albo `False`. Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej. Które linie należą do warunku, pokazuje wcięcie: przesunięcie linii o cztery spacje w prawo. Po warunku stawi

[ref-77] fraza: „Ostatni `print` nie ma wcięcia” (wstecz, wcięcie decyduje o przynależności do bloku)
  zdanie: Ciało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. Ostatni `print` nie ma wcięcia, więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.
  cel: [Instrukcja warunkowa „jeśli… to…”] Pierwszy warunek jest prawdziwy, więc jego linia się wykonała. Drugi jest fałszywy, więc jego wcięta linia została pominięta. Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.

[ref-80] fraza: „Pętla `for`, którą znasz, kończy się sama” (wstecz, pętla for kończy się po wyczerpaniu danych)
  zdanie: Pętla `for`, którą znasz, kończy się sama, bo zestaw danych się wyczerpuje. Pętla `while` („dopóki”) działa inaczej: powtarza wcięte linie, dopóki warunek daje `True`. Jeśli warunek jest zawsze prawdziwy, każda kolejna iteracja zaczyna się od nowa.
  cel: [Czym jest pętla] Pętla to instrukcja, która każe programowi wykonać ten sam fragment kodu wielokrotnie. Zamiast pisać tę samą linię trzy razy, zapisujesz ją raz i mówisz, ile razy albo dla czego ją powtórzyć. Jedno powtórzenie fragmentu nazywamy iteracją. Pętla `for` wykonuje po jednej iteracji dla każdego elementu z zestawu danych. Taki zestaw to na razie po prostu lista wartości w nawiasach kwadratowych; jej zapis omówimy osobno. Wcięte linie pod `for` to ciało pętli, tak samo jak przy

[ref-81] fraza: „„Wspólna Kasa”, która czeka na koniec listy” (wstecz, przykład programu dzielącego wydatki po osobach, przechodzącego przez listę osób)
  zdanie: Problem jest praktyczny. Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków. Tak samo wyglądałaby „Wspólna Kasa”, która czeka na koniec listy, którego nie ma.
  cel: [Czym jest pętla] Ciało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. Ostatni `print` nie ma wcięcia, więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.

[ref-82] fraza: „wcześniej szła po imionach uczestników” (wstecz, pętla z działu 06, która przechodziła po osobach)
  zdanie: Właśnie po takim zestawie chodzi pętla `for`: wcześniej szła po imionach uczestników, a teraz przyglądamy się samej liście.
  cel: [Czym jest pętla] Ciało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. Ostatni `print` nie ma wcięcia, więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.

[ref-84] fraza: „przy przechodzeniu przez wszystkie elementy” (w przód, pętla po wszystkich elementach listy)
  zdanie: Jak sięgnąć po jeden element, omówimy osobno. To, co lista daje pętli, zobaczysz przy przechodzeniu przez wszystkie elementy.
  cel: [Pętla po elementach listy] Przez wszystkie elementy listy przechodzisz pętlą `for`: `for imie in osoby:` bierze po kolei każdy element i wykonuje dla niego wcięty blok. Przy pierwszym przebiegu (czyli iteracji) `imie` dostaje pierwszy element, przy drugim drugi, i tak do ostatniego. Gdy elementy się skończą, pętla sama przestaje, a program idzie dalej, do pierwszej linii bez wcięcia. Nie liczysz indeksów ani nie sprawdzasz długości listy. ```python osoby = ["Ania

[ref-86] fraza: „więc „Ania” jest pierwsza” (wstecz, kolejność elementów na liście)
  zdanie: Elementy przychodzą w kolejności listy, więc „Ania” jest pierwsza. Dodasz czwartą osobę, a ta sama pętla obsłuży ją bez zmian.
  cel: [Czym jest lista danych] Kolejność ma znaczenie: „Ania” jest pierwsza i tak zostaje. Lista może być też dłuższa albo pusta (`[]`), a program nie musi z góry znać jej rozmiaru. Dlatego pasuje do „Wspólnej Kasy”: `osoby` to uczestnicy wyjazdu, a `wydatki` to zapłacone rachunki, których przybywa.
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-75",
      "keep": true,
      "reason": "Cel wprost pokazuje zapis listy w nawiasach kwadratowych, tak jak obiecuje fraza."
    },
    {
      "id": "ref-76",
      "keep": true,
      "reason": "Cel wyjaśnia if i wcięcie ciała bloku; czytelnik może wrócić do tego porównania."
    },
    {
      "id": "ref-77",
      "keep": true,
      "reason": "Cel zawiera to samo zjawisko: ostatni print bez wcięcia należy do całego programu."
    },
    {
      "id": "ref-80",
      "keep": false,
      "reason": "Cel to ogólne wprowadzenie pętli; nie wyjaśnia, że for kończy się po wyczerpaniu danych. Link rozprasza."
    },
    {
      "id": "ref-81",
      "keep": false,
      "reason": "Cel to fragment o trzech powtórzeniach i wcięciu, nie o Wspólnej Kasie ani o czekaniu na koniec listy."
    },
    {
      "id": "ref-82",
      "keep": false,
      "reason": "Cel pokazuje przykład z imionami, ale fragment o wcięciu, a nie o przechodzeniu po uczestnikach. Fraza to opis, nie coś do sprawdzenia."
    },
    {
      "id": "ref-84",
      "keep": true,
      "reason": "Cel to sekcja o pętli po wszystkich elementach listy, dokładnie to, co zapowiada fraza."
    },
    {
      "id": "ref-86",
      "keep": true,
      "reason": "Cel mówi wprost, że kolejność ma znaczenie i Ania jest pierwsza."
    }
  ]
}
````
