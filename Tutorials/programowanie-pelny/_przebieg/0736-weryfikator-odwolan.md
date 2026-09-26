# Krok 0736 · weryfikator_odwołań

Węzeł: `review` · dział: 7 · pytanie: 39 · próba: 1

## Prompt

````text
Jesteś weryfikatorem odwołań w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.

Znajdź w nowej sekcji WSZYSTKIE odwołania, także te, których autor nie zadeklarował:
- nawiązania do czegoś wcześniejszego („jak widzieliśmy”, „ten błąd z napiwkiem”, „wspomniany wcześniej”),
- obietnice czegoś późniejszego („powiemy osobno”, „wrócimy do tego”, „w dziale o pętlach”).
Zwykłe użycie pojęcia (np. „programu”, „listy”) NIE jest odwołaniem; nawiązanie odsyła do konkretnego miejsca albo zdarzenia,
a obietnica zapowiada, że temat wróci.

Dla każdego podaj w references: direction, phrase (dokładny fragment zdania z sekcji), about, target i quote:
- wstecz: target = id punktu zaczepienia (lm-N), a gdy żaden nie pasuje: id sekcji z listy niżej albo "glosariusz:<id>";
  quote puste (cytat punktu zaczepienia jest znany).
- w przód: target = numer późniejszego pytania, jeśli któreś wyraźnie to omówi, inaczej puste; quote puste.
- poza tutorialem: target i quote puste.
Wolno nawiązywać tylko do punktów i sekcji z list (ten i poprzedni dział) albo do haseł glosariusza. Nawiązanie, którego cel
nie istnieje albo mówi co innego, zgłoś jako potrzebę kind="odwołanie", severity="blokująca", detail = jak poprawić
(wyjaśnić na miejscu albo usunąć). Obietnicę, która odwołuje się do „pytań”, numerów albo list wewnętrznych,
zgłoś jako blokującą: czytelnik ich nie zna, zdanie ma mówić o temacie.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

ZADEKLAROWANE PRZEZ AUTORA:
- wstecz: „Sumę wydatków wydzieliliśmy już do funkcji” → lm-45 (suma jako funkcja z poprzedniej sekcji)
- w przód: „do czego wrócimy przy testowaniu programu” → 52 (testowanie małych funkcji)

HASŁA GLOSARIUSZA (id: termin):
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
- definicja-funkcji: definicja funkcji
- wywolanie-funkcji: wywołanie funkcji

PÓŹNIEJSZE PYTANIA:
- 40. Czym są argumenty funkcji?
- 41. Co to znaczy, że funkcja zwraca wynik?
- 42. Dlaczego nazwy zmiennych i funkcji powinny być czytelne?
- 43. Czym jest ponowne użycie kodu?
- 44. Czym są dane wejściowe programu?
- 45. Czym są dane wyjściowe programu?
- 46. Jak program może zapytać użytkownika o informację?
- 47. Czym jest plik i jak program może z niego korzystać?
- 48. Czym jest interfejs użytkownika?
- 49. Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?
- 50. Czym różni się błąd składni od błędu logicznego?
- 51. Jak przeczytać komunikat o błędzie?
- 52. Czym jest testowanie programu?
- 53. Czym jest debugowanie?
- 54. Dlaczego warto zapisywać kolejne wersje kodu?
- 55. Jak szukać rozwiązań problemów programistycznych w internecie?
- 56. Jakie są przykłady programów używanych na co dzień?
- 57. Czym różni się strona internetowa od aplikacji mobilnej?
- 58. Jak od pomysłu dojść do działającego programu?
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
- 60. Od czego zacząć samodzielną naukę programowania?
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

PUNKTY ZACZEPIENIA (ten i poprzedni dział):
- [lm-39] pętla po osobach (dział 06): „Ciało wykonało się trzy razy, bo na liście są trzy osoby.”
- [lm-40] zmienia się tylko imię (dział 06): „Zmienia się tylko `imie`, więc reszta linii jest zapisana jeden raz.”
- [lm-41] pytanie przy while (dział 06): „co sprawi, że warunek w końcu stanie się fałszywy?”
- [lm-42] kolejność na liście (dział 06): „Kolejność ma znaczenie: „Ania” jest pierwsza i tak zostaje.”
- [lm-43] liczenie od zera (dział 06): „indeks mówi, o ile miejsc od początku listy się przesunąć”
- [lm-44] suma zbierana w pętli (dział 06): „Suma zaczyna od zera, rośnie w każdej iteracji, a wynik pokazujesz dopiero po pętli”
- [lm-45] suma jako funkcja (dział 07): „Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-06-czym-jest-petla] Czym jest pętla (dział 06): Pętla powtarza wcięty fragment kodu, a `for` robi to raz dla każdego elementu zestawu danych, po czym kończy pracę.
- [sec-06-kiedy-siegnac-po-petle] Kiedy sięgnąć po pętlę (dział 06): Gdy kopiujesz linię i zmieniasz w niej tylko jedną wartość, użyj pętli: jeden zapis obsłuży dowolną liczbę elementów.
- [sec-06-petla-nieskonczona] Pętla nieskończona (dział 06): Pętla nieskończona nigdy nie osiąga warunku zakończenia, więc program się „zawiesza”; zatrzymasz go Ctrl+C, a przy każdym `while` pytaj, co w końcu zmieni warunek na fałsz.
- [sec-06-czym-jest-lista-danych] Czym jest lista danych (dział 06): Lista to jedna zmienna z wieloma wartościami w ustalonej kolejności, zapisana w nawiasach kwadratowych, z elementami rozdzielonymi przecinkami.
- [sec-06-odczyt-elementu-listy] Odczyt elementu listy (dział 06): Element listy pobierasz indeksem w nawiasach kwadratowych, licząc od zera, a `-1` oznacza ostatni element.
- [sec-06-petla-po-elementach-listy] Pętla po elementach listy (dział 06): Pętla `for element in lista:` wykonuje blok raz dla każdego elementu, w kolejności listy, i sama kończy pracę po ostatnim.
- [sec-07-czym-jest-funkcja] Czym jest funkcja (dział 07): Funkcję definiujesz raz przez def, a uruchamiasz każdym wywołaniem jej nazwy z nawiasami.

NOWA SEKCJA "Po co dzielić program na funkcje":
Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach.

Zobacz to na „Wspólnej Kasie”. Sumę wydatków wydzieliliśmy już do funkcji, a teraz dokładamy drugą, która z niej korzysta:

```python
def suma_wydatkow(wydatki):
    suma = 0
    for wydatek in wydatki:
        suma = suma + wydatek["kwota"]
    return suma

def udzial_na_osobe(wydatki, liczba_osob):
    return suma_wydatkow(wydatki) / liczba_osob

mazury = [{"kto": "Ania", "kwota": 120.5}, {"kto": "Bartek", "kwota": 79.5}]
tatry = [{"kto": "Celina", "kwota": 450}]
print(udzial_na_osobe(mazury, 2))
print(udzial_na_osobe(tatry, 3))
```

```text
100.0
150.0
```

Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz. Gdyby liczenie sumy trzeba było kiedyś zmienić, poprawiasz jedną funkcję, a oba wyniki będą poprawne.

Druga korzyść to czytelność: `udzial_na_osobe(mazury, 2)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, do czego wrócimy przy testowaniu programu.

U siebie masz już `funkcje.py` z jedną funkcją. Za chwilę dopiszesz drugą i użyjesz obu dla dwóch wyjazdów.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "Sumę wydatków wydzieliliśmy już do funkcji",
      "about": "suma wydatków jako funkcja z poprzedniej sekcji",
      "target": "lm-45",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "do czego wrócimy przy testowaniu programu",
      "about": "testowanie małych funkcji",
      "target": "52",
      "quote": ""
    },
    {
      "direction": "wstecz",
      "phrase": "U siebie masz już `funkcje.py` z jedną funkcją",
      "about": "plik z funkcją sumy z poprzedniej sekcji",
      "target": "lm-45",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "Za chwilę dopiszesz drugą i użyjesz obu",
      "about": "zapowiedź ćwiczenia w tej samej sekcji/dziale",
      "target": "",
      "quote": ""
    },
    {
      "direction": "poza tutorialem",
      "phrase": "Zobacz to na „Wspólnej Kasie”",
      "about": "wspólny przykład przewodni tutoriala, bez punktu zaczepienia",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "W kodzie pojawia się `wydatek[\"kwota\"]` i zapis w nawiasach klamrowych (słownik), których nie ma w glosariuszu ani w tej sekcji. Dodaj jedno zdanie, że każdy wydatek to zestaw opisanych pól (kto, kwota) i że `[\"kwota\"]` pobiera kwotę.",
      "severity": "sugestia",
      "target": "wydatek[\"kwota\"]"
    },
    {
      "kind": "odwołanie",
      "detail": "„Wspólna Kasa” to przykład przewodni bez punktu zaczepienia; dodaj krótkie przypomnienie, czym jest (np. „program do rozliczania wspólnych wydatków z wyjazdów”).",
      "severity": "sugestia",
      "target": "Wspólna Kasa"
    }
  ]
}
````
