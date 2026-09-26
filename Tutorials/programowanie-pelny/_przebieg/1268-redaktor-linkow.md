# Krok 1268 · redaktor_linków

Węzeł: `review_links` · dział: 7 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 07 „Funkcje i porządek w kodzie” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-87] fraza: „taką jak w sekcji o pętli po elementach listy” (wstecz, pętla zbierająca sumę)
  zdanie: Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:
  cel: [Pętla po elementach listy] Suma zaczyna od zera, rośnie w każdej iteracji, a wynik pokazujesz dopiero po pętli, już bez wcięcia.

[ref-88] fraza: „Oba mechanizmy omówimy osobno w kolejnych sekcjach” (w przód, argumenty funkcji (dane wchodzące))
  zdanie: Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. Oba mechanizmy omówimy osobno w kolejnych sekcjach; na razie wystarczy, że dane wchodzą, a wynik wychodzi.
  cel: [Czym są argumenty funkcji] Argumenty to dane, które przekazujesz funkcji w nawiasach przy wywołaniu, żeby miała na czym pracować. Funkcja bez argumentów robi zawsze to samo, a z argumentami to samo działanie wykonuje na różnych danych. W definicji funkcji nazwy w nawiasach to parametry: puste miejsca, które funkcja wypełnia przy każdym wywołaniu. W `na_osobe(suma, osoby)` są dwa: `suma` i `osoby`. Wartości, które wpisujesz przy wywołaniu, to argumenty. Python przypisuje je parametrom tak

[ref-89] fraza: „Oba mechanizmy omówimy osobno w kolejnych sekcjach” (w przód, zwracanie wyniku przez return)
  zdanie: Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. Oba mechanizmy omówimy osobno w kolejnych sekcjach; na razie wystarczy, że dane wchodzą, a wynik wychodzi.
  cel: [Zwracanie wyniku przez funkcję] Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał. Ta oddana wartość to wartość zwracana: wywołanie funkcji staje się w kodzie właśnie nią, więc możesz ją zapisać do zmiennej albo przekazać dalej.

[ref-91] fraza: „do czego wrócimy przy testowaniu programu” (w przód, testowanie małych funkcji)
  zdanie: Druga korzyść to czytelność: `na_osobe(suma(mazury), 3)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, do czego wrócimy przy testowaniu programu.
  cel: [Czym jest testowanie programu] Najprostszy test to jedno sprawdzenie małej funkcji. W Pythonie służy do tego assert: instrukcja, która nic nie robi, gdy warunek jest prawdziwy, a zatrzymuje program błędem `AssertionError`, gdy jest fałszywy.

[ref-92] fraza: „U siebie masz już `funkcje.py` z funkcją `suma`” (wstecz, plik z funkcją suma z poprzedniej sekcji)
  zdanie: U siebie masz już `funkcje.py` z funkcją `suma`.
  cel: [Czym jest funkcja] Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:

[ref-94] fraza: „Czytanie takich komunikatów omówimy przy błędach” (w przód, czytanie komunikatów o błędach)
  zdanie: Liczba argumentów musi zgadzać się z liczbą parametrów. Wywołanie `na_osobe(300)` kończy się komunikatem `TypeError`. To nazwa błędu, który Python zgłasza, gdy coś zrobiono w niewłaściwy sposób; tu znaczy: funkcję wywołano bez wartości dla `osoby`. Czytanie takich komunikatów omówimy przy błędach.
  cel: [Jak czytać komunikat o błędzie] Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak, a linie nad nią pokazują, gdzie to się stało. Komunikat nie jest wyrokiem, tylko wskazówką.

[ref-97] fraza: „na_osobe(suma(mazury), 3)” (wstecz, funkcja suma i lista mazury z wcześniejszego przykładu z sumą jako funkcją)
  zdanie: Konsekwencja jest praktyczna: tylko zwrócony wynik da się wykorzystać dalej. Dlatego `na_osobe(suma(mazury), 3)` działa: wynik jednej funkcji trafia jako argument do drugiej.
  cel: [Czym jest funkcja] Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:

[ref-98] fraza: „To ryzyko z zamienioną kolejnością, które znasz z argumentów funkcji” (wstecz, zamieniona kolejność argumentów daje zły wynik bez błędu)
  zdanie: Przy `f(300, 4)` trzeba zgadywać, co się dzieje i która liczba jest która. To ryzyko z zamienioną kolejnością, które znasz z argumentów funkcji: zły wynik bez błędu. Nazwa `udzial_na_osobe` mówi to od razu.
  cel: [Czym są argumenty funkcji] Kolejność też ma znaczenie: `na_osobe(4, 300)` da wynik bez błędu, ale zły, bo 4 zł podzielisz na 300 osób.

[ref-99] fraza: „przy dzieleniu programu na funkcje” (wstecz, podział programu na funkcje)
  zdanie: Ostatnią linię czyta się prawie jak zdanie. Ta czytelność przyda się przy dzieleniu programu na funkcje i przy ponownym użyciu kodu, które omówimy za chwilę.
  cel: [Po co dzielić program na funkcje] Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach. Zobacz to na „Wspólnej Kasie”. Funkcja `suma` już jest, więc dokładamy drugą, `na_osobe`, i używamy obu dla dwóch wyjazdów: ```python def suma(wydatki): razem = 0 for kwota in wydatki: razem = razem + kwota return razem def na_osobe(suma, osoby): return suma / osoby mazu

[ref-101] fraza: „U siebie w `funkcje.py` masz te same funkcje” (wstecz, plik funkcje.py z funkcjami sumy i udziału na osobę z poprzedniego działu)
  zdanie: U siebie w `funkcje.py` masz te same funkcje (pod krótszymi nazwami `suma` i `na_osobe`). Ostatnia linia wywołuje `na_osobe(300)` z jednym argumentem zamiast dwóch, stąd błąd.
  cel: [Czym jest funkcja] Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-87",
      "keep": true,
      "reason": "Cel pokazuje pętlę sumującą, o którą pyta fraza."
    },
    {
      "id": "ref-88",
      "keep": true,
      "reason": "Cel wyjaśnia argumenty, zapowiedziane w zdaniu."
    },
    {
      "id": "ref-89",
      "keep": true,
      "reason": "Cel wyjaśnia return, zapowiedziany w zdaniu."
    },
    {
      "id": "ref-91",
      "keep": true,
      "reason": "Cel pokazuje test małej funkcji przez assert."
    },
    {
      "id": "ref-92",
      "keep": false,
      "reason": "Fraza o pliku u czytelnika; cel to fragment o pętli, nie o pliku funkcje.py."
    },
    {
      "id": "ref-94",
      "keep": true,
      "reason": "Cel uczy czytać komunikaty o błędach, jak obiecuje fraza."
    },
    {
      "id": "ref-97",
      "keep": false,
      "reason": "Cel to zapowiedź wydzielenia pętli, nie przykład z suma(mazury); nie daje tego, czego fraza dotyczy."
    },
    {
      "id": "ref-98",
      "keep": true,
      "reason": "Cel zawiera dokładnie ryzyko zamienionej kolejności argumentów."
    },
    {
      "id": "ref-99",
      "keep": true,
      "reason": "Cel wyjaśnia po co dzielić program na funkcje."
    },
    {
      "id": "ref-101",
      "keep": false,
      "reason": "Cel to zapowiedź wydzielenia pętli, nie plik z suma i na_osobe."
    }
  ]
}
````
