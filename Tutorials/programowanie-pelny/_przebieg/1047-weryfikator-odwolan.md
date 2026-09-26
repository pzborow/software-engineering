# Krok 1047 · weryfikator_odwołań

Węzeł: `review` · dział: 9 · pytanie: 54 · próba: 1

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
- wstecz: „gdy testy przechodzą” → sec-09-czym-jest-testowanie-programu (testy jako sygnał, że wersja działa)

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

PÓŹNIEJSZE PYTANIA:
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
- [lm-60] zły dzielnik: 39.0 zamiast 26.0 (dział 09): „Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.”
- [lm-61] start nie wypisany (dział 09): „Słowo „start” się nie pojawiło, a komunikat wskazuje linię i miejsce.”
- [lm-62] czytaj od dołu (dział 09): „Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak”
- [lm-63] start się wypisał (dział 09): „tu „Start” się wypisał, bo program ruszył i padł dopiero w środku”
- [lm-64] cisza po assert (dział 09): „Cisza po `assert` znaczy „zgadza się”.”
- [lm-65] print pokazuje złą liczbę osób (dział 09): „Suma się zgadza, a liczba osób nie: mają być trzy.”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-08-dane-wejsciowe-programu] Dane wejściowe programu (dział 08): Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.
- [sec-08-dane-wyjsciowe-programu] Dane wyjściowe programu (dział 08): Dane wyjściowe to wynik, który program oddaje na zewnątrz (ekran, plik, inny program), a dobre wyjście jest opisane tak, by zrozumiał je człowiek.
- [sec-08-pytanie-uzytkownika-o-informacje] Pytanie użytkownika o informację (dział 08): Funkcja input wypisuje pytanie i zwraca odpowiedź użytkownika zawsze jako tekst, więc liczbę trzeba zamienić przez float().
- [sec-08-czym-jest-plik] Czym jest plik (dział 08): Plik przechowuje dane na dysku po zakończeniu programu, a program otwiera go przez open (najlepiej z with) w trybie czytania, zapisu lub dopisywania i pamięta, że dostaje z niego tekst.
- [sec-08-czym-jest-interfejs-uzytkownika] Czym jest interfejs użytkownika (dział 08): Interfejs użytkownika to wszystko, przez co człowiek rozmawia z programem: pytania, które program zadaje, i wyniki, które pokazuje, więc powinny być jasne dla kogoś, kto nie zna kodu.
- [sec-08-po-co-sprawdzac-dane-uzytkownika] Po co sprawdzać dane użytkownika (dział 08): Sprawdzaj dane od użytkownika zaraz po wpisaniu, bo człowiek może wpisać coś nieoczekiwanego, a zły wpis powinien dostać komunikat i drugą szansę.
- [sec-09-blad-skladni-a-blad-logiczny] Błąd składni a błąd logiczny (dział 09): Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.
- [sec-09-jak-czytac-komunikat-o-bledzie] Jak czytać komunikat o błędzie (dział 09): Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.
- [sec-09-czym-jest-testowanie-programu] Czym jest testowanie programu (dział 09): Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.
- [sec-09-czym-jest-debugowanie] Czym jest debugowanie (dział 09): Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.

NOWA SEKCJA "Po co zapisywać wersje kodu":
Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast pamiętać, co dokładnie zmieniłeś.

Robi to [[git|Git]], program do zapisywania historii plików. Zapis jednej wersji to [[commit|commit]]: migawka wybranych plików z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię projektu, to [[repozytorium|repozytorium]]. Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.

Wersje przydają się w trzech sytuacjach:

- Po nieudanej zmianie wracasz do ostatniej działającej wersji.
- Historia pokazuje, kiedy pojawił się błąd, co przy szukaniu przyczyny oszczędza sporo czasu.
- Możesz śmiało eksperymentować, bo stara wersja i tak jest bezpieczna.

Dobry moment na commit to chwila, gdy testy przechodzą. Opis pisz tak, żeby po miesiącu dało się z niego coś zrozumieć. Wiele małych commitów jest lepsze niż jeden wielki.

Sam zapis wygląda tak:

```text
git init -b main
git add funkcje.py test_kasa.py
git commit -m "Funkcje Wspolnej Kasy i testy"
```

`init` zakłada repozytorium, `add` wybiera pliki do zapisu, a `commit` zapisuje wersję. Wybór plików przez `add` sprawia, że do historii trafia tylko to, co chcesz. Wykonasz to u siebie w warsztacie.
````

## Odpowiedź

````json
{
  "ok": false,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "gdy testy przechodzą",
      "about": "testy jako sygnał, że wersja działa",
      "target": "sec-09-czym-jest-testowanie-programu",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "Wykonasz to u siebie w warsztacie.",
      "about": "praktyczne wykonanie poleceń Git w warsztacie",
      "target": "",
      "quote": ""
    },
    {
      "direction": "wstecz",
      "phrase": "Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.",
      "about": "projekt Wspólna Kasa z wcześniejszych działów",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "wyjaśnienie",
      "severity": "blokująca",
      "target": "git",
      "detail": "Git, commit i repozytorium to kluczowe pojęcia sekcji, a nie mają haseł w glosariuszu. Są zdefiniowane w tekście jednym zdaniem każde, więc to wystarcza. Trzeba jednak dodać hasła do glosariusza albo zostawić definicje w tekście. Uwaga: 'migawka wybranych plików' jest metaforą i wymaga krótkiego dopowiedzenia, co to znaczy dla osoby spoza IT.",
      "source": "glosariusz"
    },
    {
      "kind": "odwołanie",
      "severity": "blokująca",
      "target": "Wykonasz to u siebie w warsztacie.",
      "detail": "Obietnica odsyła do 'warsztatu', którego czytelnik może nie znać jako elementu tutorialu, i nie mówi o temacie. Zastąp zdaniem o temacie, np. 'Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym', albo usuń."
    },
    {
      "kind": "odwołanie",
      "severity": "blokująca",
      "target": "Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.",
      "detail": "'Wspólna Kasa' to nawiązanie do projektu z wcześniejszych działów, ale żaden punkt zaczepienia ani sekcja tego nie potwierdza. Wyjaśnij na miejscu, że to przykładowy program do dzielenia wydatków, albo usuń nawiązanie."
    },
    {
      "kind": "przykład",
      "severity": "blokująca",
      "target": "git init -b main",
      "detail": "Polecenia w bloku kodu nie mają pokazanego wyniku ani opisu, gdzie je wpisać (terminal, w folderze projektu). Czytelnik spoza IT nie wie, co zobaczy po każdym poleceniu. Dodaj, że wpisuje się je w terminalu w folderze projektu, i krótko, co Git odpowie. Wyjaśnij też, czym jest `-b main` (nazwa głównej gałęzi) albo usuń tę opcję."
    },
    {
      "kind": "wyjaśnienie",
      "severity": "sugestia",
      "target": "add",
      "detail": "Nie wyjaśniono, że commit obejmuje tylko pliki wybrane przez add (tzw. poczekalnia). Zdanie 'do historii trafia tylko to, co chcesz' jest poprawne, ale przydałby się przykład pliku, którego nie chcemy zapisać."
    },
    {
      "kind": "przykład",
      "severity": "sugestia",
      "target": "Opis pisz tak, żeby po miesiącu dało się z niego coś zrozumieć.",
      "detail": "Dobry i zły opis commita (np. 'poprawka' vs 'Naprawa dzielnika w podziale rachunku') ułatwiłyby zrozumienie rady."
    }
  ]
}
````
