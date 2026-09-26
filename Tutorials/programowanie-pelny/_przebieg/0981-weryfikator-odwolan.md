# Krok 0981 · weryfikator_odwołań

Węzeł: `review` · dział: 9 · pytanie: 50 · próba: 2

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
- w przód: „Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach” → 51 (czytanie komunikatów o błędach i debugowanie)

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
- argument-funkcji: argument funkcji
- parametr: parametr
- typeerror: TypeError
- none: None
- wartosc-zwracana: wartość zwracana
- dane-wejsciowe: dane wejściowe
- dane-wyjsciowe: dane wyjściowe
- input: input
- plik: plik
- tryb-otwarcia-pliku: tryb otwarcia pliku
- interfejs-uzytkownika: interfejs użytkownika
- interfejs-tekstowy: interfejs tekstowy
- walidacja-danych: walidacja danych

PÓŹNIEJSZE PYTANIA:
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
- [lm-52] kod stały, dane zmienne (dział 08): „kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne”
- [lm-53] wynik bez opisu (dział 08): „Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu”
- [lm-54] input zwraca tekst (dział 08): „`input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`.”
- [lm-55] tryb w kasuje (dział 08): „Pułapką jest tryb `"w"`, który kasuje starą zawartość.”
- [lm-56] plik zostaje (dział 08): „Zmienne żyją tylko podczas pracy programu i znikają wraz z jego zakończeniem, a plik zostaje.”
- [lm-57] interfejs to jedyne, co widzi użytkownik (dział 08): „Użytkownik nie widzi kodu, widzi tylko interfejs.”
- [lm-58] cichy błąd z minusem (dział 08): „A gdy wpisze `-5`, program nie zgłosi żadnego błędu i po cichu policzy złe saldo.”
- [lm-59] zły wpis dostaje drugą szansę (dział 08): „zły wpis nie kończy programu, tylko dostaje komunikat i kolejną szansę”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-08-dane-wejsciowe-programu] Dane wejściowe programu (dział 08): Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.
- [sec-08-dane-wyjsciowe-programu] Dane wyjściowe programu (dział 08): Dane wyjściowe to wynik, który program oddaje na zewnątrz (ekran, plik, inny program), a dobre wyjście jest opisane tak, by zrozumiał je człowiek.
- [sec-08-pytanie-uzytkownika-o-informacje] Pytanie użytkownika o informację (dział 08): Funkcja input wypisuje pytanie i zwraca odpowiedź użytkownika zawsze jako tekst, więc liczbę trzeba zamienić przez float().
- [sec-08-czym-jest-plik] Czym jest plik (dział 08): Plik przechowuje dane na dysku po zakończeniu programu, a program otwiera go przez open (najlepiej z with) w trybie czytania, zapisu lub dopisywania i pamięta, że dostaje z niego tekst.
- [sec-08-czym-jest-interfejs-uzytkownika] Czym jest interfejs użytkownika (dział 08): Interfejs użytkownika to wszystko, przez co człowiek rozmawia z programem: pytania, które program zadaje, i wyniki, które pokazuje, więc powinny być jasne dla kogoś, kto nie zna kodu.
- [sec-08-po-co-sprawdzac-dane-uzytkownika] Po co sprawdzać dane użytkownika (dział 08): Sprawdzaj dane od użytkownika zaraz po wpisaniu, bo człowiek może wpisać coś nieoczekiwanego, a zły wpis powinien dostać komunikat i drugą szansę.

NOWA SEKCJA "Błąd składni a błąd logiczny":
Błąd składni łamie zasady zapisu, więc Python zatrzymuje się, zanim cokolwiek wykona. Błąd logiczny ma zapis poprawny, ale robi coś innego, niż zamierzałeś, więc program działa i po cichu podaje zły wynik.

[[blad-skladni|Błąd składni]] to naruszenie [[skladnia|składni]], czyli reguł zapisu: brakujący dwukropek, niedomknięty cudzysłów, źle wcięta linia. Python czyta cały plik przed startem, więc nie wykona nawet linii sprzed błędu:

```python
print("start")
suma = 45.5 + 20
if suma > 10
    print("dużo")
```

```text
  File "blad.py", line 3
    if suma > 10
                ^
SyntaxError: expected ':'
```

Słowo „start” się nie pojawiło, a komunikat wskazuje linię i miejsce.

[[blad-logiczny|Błąd logiczny]] to pomyłka w pomyśle: zły wzór, dzielnik albo warunek. Python jej nie zauważy, bo każda instrukcja jest poprawna. Trzy osoby dzielą wydatki 45.5, 20 i 12.5 zł:

```python
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)
```

```text
Na osobę: 39.0
```

Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.

Konsekwencja: błędy składni są uciążliwe, ale łatwe, bo wskaże je Python. Za błędy logiczne odpowiadasz Ty, więc wynik porównuj z rachunkiem na kartce. Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "w przód",
      "phrase": "Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu",
      "about": "czytanie komunikatów o błędach i debugowanie",
      "target": "51",
      "quote": ""
    }
  ]
}
````
