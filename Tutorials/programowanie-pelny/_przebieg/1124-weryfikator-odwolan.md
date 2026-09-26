# Krok 1124 · weryfikator_odwołań

Węzeł: `review` · dział: 10 · pytanie: 58 · próba: 1

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
- wstecz: „zapisywaniu wersji kodu” → sec-09-po-co-zapisywac-wersje-kodu (commit jako punkt powrotu)

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
- blad-skladni: błąd składni
- blad-logiczny: błąd logiczny
- traceback: Traceback
- komunikat-o-bledzie: komunikat o błędzie
- testowanie: testowanie
- assert: assert
- debugowanie: debugowanie
- git: Git
- commit: commit
- repozytorium: repozytorium
- serwer: serwer
- przegladarka: przeglądarka

PÓŹNIEJSZE PYTANIA:
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
- 60. Od czego zacząć samodzielną naukę programowania?
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

PUNKTY ZACZEPIENIA (ten i poprzedni dział):
- [lm-60] zły dzielnik: 39.0 zamiast 26.0 (dział 09): „Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.”
- [lm-61] start nie wypisany (dział 09): „Słowo „start” się nie pojawiło, a komunikat wskazuje linię i miejsce.”
- [lm-62] czytaj od dołu (dział 09): „Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak”
- [lm-63] start się wypisał (dział 09): „tu „Start” się wypisał, bo program ruszył i padł dopiero w środku”
- [lm-64] cisza po assert (dział 09): „Cisza po `assert` znaczy „zgadza się”.”
- [lm-65] print pokazuje złą liczbę osób (dział 09): „Suma się zgadza, a liczba osób nie: mają być trzy.”
- [lm-66] cofnięcie do wczorajszego commita (dział 09): „wracasz do wczorajszego commita zamiast szukać własnych zmian”
- [lm-67] kopiuj ostatnią linię bez ścieżek (dział 09): „Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych”
- [lm-68] Kasa jako strona lub aplikacja (dział 10): „wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-09-blad-skladni-a-blad-logiczny] Błąd składni a błąd logiczny (dział 09): Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.
- [sec-09-jak-czytac-komunikat-o-bledzie] Jak czytać komunikat o błędzie (dział 09): Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.
- [sec-09-czym-jest-testowanie-programu] Czym jest testowanie programu (dział 09): Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.
- [sec-09-czym-jest-debugowanie] Czym jest debugowanie (dział 09): Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.
- [sec-09-po-co-zapisywac-wersje-kodu] Po co zapisywać wersje kodu (dział 09): Commit zapisuje działającą wersję kodu z opisem, dzięki czemu zawsze możesz do niej wrócić i sprawdzić, kiedy coś się zepsuło.
- [sec-09-szukanie-rozwiazan-w-internecie] Szukanie rozwiązań w internecie (dział 09): Szukaj po ostatniej linii komunikatu i nazwie języka, oceniaj źródła i nigdy nie wklejaj skopiowanego kodu bez zrozumienia.
- [sec-10-programy-uzywane-na-co-dzien] Programy używane na co dzień (dział 10): Programy, których używasz codziennie, to te same proste klocki (dane, decyzje, pętle, funkcje, pliki) w większej skali i z ładniejszym interfejsem.
- [sec-10-strona-internetowa-a-aplikacja-mobilna] Strona internetowa a aplikacja mobilna (dział 10): Strona otwiera się w przeglądarce bez instalacji, a aplikacja mobilna jest zainstalowana w telefonie i lepiej korzysta z jego możliwości, ale obie działają według schematu wejście, przetwarzanie, wyjście.

NOWA SEKCJA "Od pomysłu do działającego programu":
Od pomysłu do programu dochodzi się małymi krokami: opisujesz zadanie zwykłymi słowami, piszesz najmniejszy kawałek, który coś robi, sprawdzasz go i dopiero wtedy dokładasz następny. Cały program naraz zwykle nie działa, a szukanie błędu w stu liniach jest męczące.

```text
pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit
              ↑                                                            |
              └──────────────────── następny kawałek ←─────────────────────┘
```

Weźmy pomysł: „chcę wiedzieć, kto komu ile jest winien”. Opis krokowy (jak przy podziale problemu na części) brzmi: dla każdej osoby zsumuj to, co zapłaciła, odejmij jej równy udział i wypisz wynik. Z tego wychodzi jedna mała [[funkcja]]:

```python
def saldo_osoby(wydatki, osoba, liczba_osob):
    # ile osoba zapłaciła minus jej równy udział
    ...
```

Funkcję sprawdzasz na danych, których wynik znasz z kartki. Dopiero gdy się zgadza, zapisujesz [[commit]] (zapisaną wersję kodu z opisem) i myślisz o kolejnym kawałku, np. wczytaniu wydatków z pliku.

Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, o którym była mowa przy [[sec-09-po-co-zapisywac-wersje-kodu|zapisywaniu wersji kodu]]. Za chwilę zrobisz to u siebie, w warsztacie.
````

## Odpowiedź

````json
{
  "ok": false,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "jak przy podziale problemu na części",
      "about": "wcześniejsze omówienie dzielenia problemu na mniejsze części",
      "target": "",
      "quote": ""
    },
    {
      "direction": "wstecz",
      "phrase": "o którym była mowa przy zapisywaniu wersji kodu",
      "about": "commit jako działający punkt powrotu",
      "target": "lm-66",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "Za chwilę zrobisz to u siebie, w warsztacie.",
      "about": "praktyczne ćwiczenie budowania programu małymi krokami",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "odwołanie",
      "severity": "blokująca",
      "target": "jak przy podziale problemu na części",
      "detail": "Nawiązanie do wcześniejszego omówienia dzielenia problemu na części nie ma celu na liście punktów zaczepienia ani sekcji z tego i poprzedniego działu ani w glosariuszu. Czytelnik nie ma dokąd wrócić. Usuń nawiązanie albo wyjaśnij na miejscu jednym zdaniem, np. „rozbij zadanie na kroki, z których każdy da się zrobić osobno”.",
      "source": "nawiązanie bez celu"
    }
  ]
}
````
