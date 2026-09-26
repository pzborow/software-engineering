# Krok 0491 · weryfikator_odwołań

Węzeł: `review` · dział: 5 · pytanie: 27 · próba: 2

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
- wstecz: „Obiecaliśmy w poprzedniej sekcji” → sec-05-dzialania-matematyczne-w-programie (sklejanie tekstów plusem zapowiedziane przy działaniach matematycznych)

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

PÓŹNIEJSZE PYTANIA:
- 28. Jak program porównuje dwie wartości?
- 29. Czym jest instrukcja warunkowa „jeśli… to…”?
- 30. Do czego służy część „w przeciwnym razie”?
- 31. Do czego służą operatory „i” oraz „lub”?
- 32. Czym jest pętla?
- 33. Kiedy warto użyć pętli zamiast pisać to samo wiele razy?
- 34. Czym jest pętla nieskończona i dlaczego jest problemem?
- 35. Czym jest lista danych?
- 36. Jak odczytać konkretny element listy?
- 37. Jak przejść przez wszystkie elementy listy?
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
- [lm-24] imienia nie da się podzielić (dział 04): „Imienia „Ania” nie da się podzielić przez 2, bo to nie ma sensu”
- [lm-25] zmiana kwoty (dział 04): „po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce”
- [lm-26] pudełko i kopia (dział 04): „Zmiana `kwota` nie ruszyła `kwota_stara`, bo do drugiego pudełka trafiła kopia wartości.”
- [lm-27] cztery znaki zamiast kwoty (dział 04): „`"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5”
- [lm-28] type() pokazuje typ (dział 04): „Typ sprawdzisz funkcją `type()`.”
- [lm-29] tabela typów Pythona (dział 04): „Oto podstawowe typy Pythona:”
- [lm-30] pole wyboru (dział 04): „W arkuszu to odpowiednik pola wyboru: zaznaczone albo nie.”
- [lm-31] True w cudzysłowie (dział 04): „`"True"` w cudzysłowie to tylko tekst z czterech liter”
- [lm-32] zmiana kwoty i kopia (dział 04): „Linia `kwota_stara = kwota` skopiowała 45.5 w chwili wykonania.”
- [lm-33] nieścisłość ułamka (dział 05): „Końcówka `...336` to drobna nieścisłość: komputer trzyma ułamki w przybliżeniu.”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-04-czym-jest-dana] Czym jest dana (dział 04): Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.
- [sec-04-czym-jest-zmienna] Czym jest zmienna (dział 04): Zmienna to nazwa, pod którą program przechowuje daną, żeby móc jej użyć wielokrotnie i w razie potrzeby zmienić.
- [sec-04-zmienna-jako-pudelko-z-etykieta] Zmienna jako pudełko z etykietą (dział 04): Zmienna to pudełko z etykietą: nazwa zostaje, w środku jest jedna wartość, którą można podmienić, a kopie są niezależne.
- [sec-04-liczba-a-tekst] Liczba a tekst (dział 04): Cudzysłów zmienia rodzaj danych: 45.5 to liczba, którą można dzielić, a "45.5" to tekst, którego dzielić się nie da.
- [sec-04-czym-jest-typ-danych] Czym jest typ danych (dział 04): Typ danych to rodzaj wartości (str, int, float, bool), który decyduje o tym, jakie działania są na niej możliwe.
- [sec-04-wartosc-logiczna-prawda-falsz] Wartość logiczna prawda/fałsz (dział 04): Wartość logiczna (`bool`) to `True` albo `False`, zapisywane z wielkiej litery i bez cudzysłowu, a program używa jej do podejmowania decyzji.
- [sec-04-przypisanie-wartosci-do-zmiennej] Przypisanie wartości do zmiennej (dział 04): Przypisanie `=` to polecenie zapisania wartości z prawej strony pod nazwą z lewej, a o wartości zmiennej decyduje ostatnie wykonane przypisanie.
- [sec-05-dzialania-matematyczne-w-programie] Działania matematyczne w programie (dział 05): Python zna siedem podstawowych operatorów arytmetycznych (`+ - * / // % **`); na tekście dzielić się nie da, a `+` i `*` znaczą tam sklejanie i powtarzanie.

NOWA SEKCJA "Łączenie tekstów":
Program łączy teksty operatorem `+`, który skleja je w jeden, dokładnie w takiej kolejności i z takimi znakami, jakie mu podasz. Ta operacja nazywa się [[konkatenacja|sklejaniem tekstów]] (konkatenacją). Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono.

Python niczego nie dopowiada. Nie doda spacji ani przecinka, więc odstępy musisz wstawić sam, jako część tekstu w cudzysłowie:

```python
imie = "Ania"
kwota = 45.5
print(imie + " zapłaciła " + str(kwota) + " zł")
print(imie + "zapłaciła")
```

```text
Ania zapłaciła 45.5 zł
Aniazapłaciła
```

W drugiej linii zabrakło spacji, więc słowa się zlepiły.

Sklejać można tylko tekst z tekstem. Zapis `"Kwota: " + kwota` zatrzyma program błędem `TypeError`, bo liczby 45.5 nie da się dokleić do napisu. Zamienia ją na tekst funkcja `str()`: `str(kwota)` daje `"45.5"`. Nie zmienia to samej zmiennej `kwota`, która dalej jest liczbą.

Wygodniejszy bywa zapis z literą `f` przed cudzysłowem: `f"{imie} zapłaciła {kwota} zł"`. Nazwy w nawiasach klamrowych Python podmienia na wartości, także liczbowe.

Ten błąd możesz wywołać od razu: w warsztacie poniżej dopisujesz do swojego skryptu linię, która skleja tekst z liczbą.

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [odwołanie] kasa.py: Zdanie „U siebie zobaczysz ten błąd za chwilę w `kasa.py`” zapowiada plik i ćwiczenie, których czytelnik nie zna, a żaden punkt ani sekcja tego nie wprowadza. Usuń zdanie albo zastąp je tym, co czytelnik może zrobić od razu, np. „Wpisz `"Kwota: " + 45.5` w terminalu, a zobaczysz ten błąd”.
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": false,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno",
      "about": "sklejanie tekstów plusem zapowiedziane przy działaniach matematycznych",
      "target": "sec-05-dzialania-matematyczne-w-programie",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "w warsztacie poniżej dopisujesz do swojego skryptu linię",
      "about": "zapowiedź warsztatu i skryptu, w którym czytelnik wywoła błąd TypeError",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "odwołanie",
      "detail": "Poprawka nie została wprowadzona w istocie: zdanie o „kasa.py” zniknęło, ale zastąpiło je „w warsztacie poniżej dopisujesz do swojego skryptu linię…”. To nadal zapowiedź ćwiczenia i skryptu, których czytelnik nie zna, a żaden punkt ani sekcja ich nie wprowadza. Usuń zdanie albo zastąp je czymś do zrobienia od razu, np. „Wpisz w terminalu `\"Kwota: \" + 45.5`, a zobaczysz ten błąd.”",
      "severity": "blokująca",
      "source": "kasa.py",
      "status": "niespełniona",
      "target": "kasa.py"
    }
  ]
}
````
