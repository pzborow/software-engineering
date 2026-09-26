# Krok 0683 · weryfikator_odwołań

Węzeł: `review` · dział: 6 · pytanie: 37 · próba: 1

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
- wstecz: „tak jak w sekcji o liście” → sec-06-czym-jest-lista-danych (kolejność elementów listy)
- wstecz: „Kolejność ma znaczenie” → lm-42 ()

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

PÓŹNIEJSZE PYTANIA:
- 38. Czym jest funkcja?
- 39. Po co dzielić program na funkcje?
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
- [lm-33] nieścisłość ułamka (dział 05): „Końcówka `...336` to drobna nieścisłość: komputer trzyma ułamki w przybliżeniu.”
- [lm-34] zlepione słowa (dział 05): „W drugiej linii zabrakło spacji, więc słowa się zlepiły.”
- [lm-35] tekst nie równa się liczbie (dział 05): „Tekst `"45.5"` i liczba 45.5 to różne typy, więc też nie są równe”
- [lm-36] wcięcie i ostatni print (dział 05): „Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.”
- [lm-37] dwie drogi if/else (dział 05): „Warunek `kwota > 100` jest fałszywy, więc Python pominął pierwszy wcięty blok i wykonał ten pod `else`.”
- [lm-38] kwota duża lub dzielona przez wielu (dział 05): „kwotę można uznać za dużą, gdy jest wysoka **lub** dzieli ją dużo osób”
- [lm-39] pętla po osobach (dział 06): „Ciało wykonało się trzy razy, bo na liście są trzy osoby.”
- [lm-40] zmienia się tylko imię (dział 06): „Zmienia się tylko `imie`, więc reszta linii jest zapisana jeden raz.”
- [lm-41] pytanie przy while (dział 06): „co sprawi, że warunek w końcu stanie się fałszywy?”
- [lm-42] kolejność na liście (dział 06): „Kolejność ma znaczenie: „Ania” jest pierwsza i tak zostaje.”
- [lm-43] liczenie od zera (dział 06): „indeks mówi, o ile miejsc od początku listy się przesunąć”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-05-dzialania-matematyczne-w-programie] Działania matematyczne w programie (dział 05): Python zna siedem podstawowych operatorów arytmetycznych (`+ - * / // % **`); na tekście dzielić się nie da, a `+` i `*` znaczą tam sklejanie i powtarzanie.
- [sec-05-laczenie-tekstow] Łączenie tekstów (dział 05): Plus skleja tylko tekst z tekstem, bez dodawania spacji, a liczbę trzeba przed sklejeniem zamienić funkcją str() albo użyć zapisu z f.
- [sec-05-porownywanie-wartosci] Porównywanie wartości (dział 05): Operatory porównania (`==`, `!=`, `<`, `>`, `<=`, `>=`) dają `True` albo `False`, a `==` pyta o równość, w przeciwieństwie do `=`, które przypisuje.
- [sec-05-instrukcja-warunkowa-jesli-to] Instrukcja warunkowa „jeśli… to…” (dział 05): Instrukcja `if` wykonuje wcięte pod nią linie tylko wtedy, gdy warunek daje `True`; w przeciwnym razie Python je pomija.
- [sec-05-czesc-w-przeciwnym-razie] Część „w przeciwnym razie” (dział 05): `else` to droga „w przeciwnym razie”: wykonuje się tylko wtedy, gdy warunek z `if` jest fałszywy, więc program zawsze wybiera dokładnie jedną z dwóch dróg.
- [sec-05-operatory-i-oraz-lub] Operatory „i” oraz „lub” (dział 05): `and` wymaga prawdziwości obu warunków, a `or` wystarczy jeden prawdziwy, żeby całość dała `True`.
- [sec-06-czym-jest-petla] Czym jest pętla (dział 06): Pętla powtarza wcięty fragment kodu, a `for` robi to raz dla każdego elementu zestawu danych, po czym kończy pracę.
- [sec-06-kiedy-siegnac-po-petle] Kiedy sięgnąć po pętlę (dział 06): Gdy kopiujesz linię i zmieniasz w niej tylko jedną wartość, użyj pętli: jeden zapis obsłuży dowolną liczbę elementów.
- [sec-06-petla-nieskonczona] Pętla nieskończona (dział 06): Pętla nieskończona nigdy nie osiąga warunku zakończenia, więc program się „zawiesza”; zatrzymasz go Ctrl+C, a przy każdym `while` pytaj, co w końcu zmieni warunek na fałsz.
- [sec-06-czym-jest-lista-danych] Czym jest lista danych (dział 06): Lista to jedna zmienna z wieloma wartościami w ustalonej kolejności, zapisana w nawiasach kwadratowych, z elementami rozdzielonymi przecinkami.
- [sec-06-odczyt-elementu-listy] Odczyt elementu listy (dział 06): Element listy pobierasz indeksem w nawiasach kwadratowych, licząc od zera, a `-1` oznacza ostatni element.

NOWA SEKCJA "Pętla po elementach listy":
Przez wszystkie elementy [[lista-danych|listy]] przechodzisz [[petla|pętlą]] `for`: `for imie in osoby:` bierze po kolei każdy [[element-listy|element]] i wykonuje dla niego wcięty blok.

Działa to tak: przy pierwszym przebiegu (czyli [[iteracja|iteracji]]) `imie` dostaje pierwszy element, przy drugim drugi, i tak do ostatniego. Kiedy elementy się skończą, pętla sama przestaje, a program idzie dalej, do pierwszej linii bez wcięcia. Nie liczysz indeksów ani nie sprawdzasz długości listy.

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print(imie)
print("Koniec")
```

```text
Ania
Bartek
Celina
Koniec
```

Elementy przychodzą w kolejności listy, więc „Ania" jest pierwsza, tak jak w sekcji o liście. Dodasz czwartą osobę, a ta sama pętla obsłuży ją bez zmiany kodu.

Nazwa `imie` jest zwykłą zmienną: po pętli zachowuje wartość ostatniego elementu. Wybierz ją tak, by mówiła, co jest na liście, a nie „x".

Pętla może też coś zbierać, np. dodawać kolejne kwoty do sumy. Tak robi Twój `kasa.py`: wypisuje każdą kwotę, sumuje je i dopiero po pętli pokazuje wynik.
````

## Odpowiedź

````json
{
  "ok": false,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "tak jak w sekcji o liście",
      "about": "kolejność elementów listy (Ania pierwsza)",
      "target": "lm-42",
      "quote": ""
    },
    {
      "direction": "poza tutorialem",
      "phrase": "Tak robi Twój `kasa.py`",
      "about": "program kasa.py czytelnika, którego nie ma w żadnym punkcie ani sekcji z list",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "odwołanie",
      "severity": "blokująca",
      "target": "Tak robi Twój `kasa.py`",
      "detail": "Nawiązanie do `kasa.py` nie ma celu w sekcjach ani punktach zaczepienia tego i poprzedniego działu, a opisuje sumowanie kwot, którego tu nie pokazano. Usuń to zdanie albo wyjaśnij na miejscu, dając krótki przykład pętli sumującej (np. `suma = 0`, `for kwota in kwoty: suma = suma + kwota`, `print(suma)` po pętli).",
      "source": "odwołanie"
    },
    {
      "kind": "odwołanie",
      "severity": "sugestia",
      "target": "tak jak w sekcji o liście",
      "detail": "Nawiązanie jest poprawne, ale zgrabniej wskazać sam fakt: „kolejność listy jest stała, więc Ania jest pierwsza”. Fraza „Kolejność ma znaczenie” zadeklarowana przez autora nie występuje w tekście.",
      "source": "odwołanie"
    }
  ]
}
````
