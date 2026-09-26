# Krok 1106 · weryfikator_odwołań

Węzeł: `review` · dział: 10 · pytanie: 57 · próba: 1

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
- wstecz: „aplikacjami” → glosariusz:aplikacja (aplikacja jako program z oprawą)
- wstecz: „funkcje liczące” → sec-10-programy-uzywane-na-co-dzien (funkcje Wspólnej Kasy)

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

PÓŹNIEJSZE PYTANIA:
- 58. Jak od pomysłu dojść do działającego programu?
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

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-09-blad-skladni-a-blad-logiczny] Błąd składni a błąd logiczny (dział 09): Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.
- [sec-09-jak-czytac-komunikat-o-bledzie] Jak czytać komunikat o błędzie (dział 09): Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.
- [sec-09-czym-jest-testowanie-programu] Czym jest testowanie programu (dział 09): Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.
- [sec-09-czym-jest-debugowanie] Czym jest debugowanie (dział 09): Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.
- [sec-09-po-co-zapisywac-wersje-kodu] Po co zapisywać wersje kodu (dział 09): Commit zapisuje działającą wersję kodu z opisem, dzięki czemu zawsze możesz do niej wrócić i sprawdzić, kiedy coś się zepsuło.
- [sec-09-szukanie-rozwiazan-w-internecie] Szukanie rozwiązań w internecie (dział 09): Szukaj po ostatniej linii komunikatu i nazwie języka, oceniaj źródła i nigdy nie wklejaj skopiowanego kodu bez zrozumienia.
- [sec-10-programy-uzywane-na-co-dzien] Programy używane na co dzień (dział 10): Programy, których używasz codziennie, to te same proste klocki (dane, decyzje, pętle, funkcje, pliki) w większej skali i z ładniejszym interfejsem.

NOWA SEKCJA "Strona internetowa a aplikacja mobilna":
Strona internetowa działa w przeglądarce i otwierasz ją przez adres, a aplikacja mobilna to program zainstalowany w telefonie, pobrany ze sklepu. Obie są [[aplikacja|aplikacjami]] w sensie oprawy dla użytkownika, ale trafiają do niego inaczej.

Strona leży na cudzym komputerze, czyli [[serwer|serwerze]] (komputerze w internecie, który przechowuje stronę i odpowiada na zapytania). Przeglądarka pobiera ją za każdym razem, więc nic nie instalujesz, a autor może ją poprawić dla wszystkich naraz. Ta sama strona działa na komputerze, tablecie i telefonie.

Aplikacja mobilna jest zainstalowana na urządzeniu. Ma łatwiejszy dostęp do aparatu, powiadomień czy czujników i często działa bez internetu. Za to wymaga pobrania, aktualizacji i osobnej wersji dla każdego systemu, np. Androida i iOS.

| Cecha | Strona internetowa | Aplikacja mobilna |
|---|---|---|
| Uruchomienie | adres w przeglądarce | ikona na telefonie |
| Instalacja | brak | ze sklepu |
| Aktualizacja | automatyczna, u autora | pobierasz nową wersję |
| Dostęp do aparatu i czujników | ograniczony | szeroki |
| Bez internetu | zwykle nie działa | często działa |

Zasada pod spodem jest ta sama: dane wejściowe, przetwarzanie, dane wyjściowe. Zmienia się miejsce uruchomienia i sposób dostarczenia.

Konsekwencja dla „Wspólnej Kasy”: jej rachunki możesz kiedyś udostępnić jako stronę, którą znajomi otworzą przez link, albo jako aplikację w telefonie. Na razie masz wersję w terminalu, a jej logika (funkcje liczące) przydałaby się w obu wariantach.
````

## Odpowiedź

````json
{
  "ok": false,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "aplikacjami",
      "about": "aplikacja jako program z oprawą dla użytkownika",
      "target": "glosariusz:aplikacja",
      "quote": ""
    },
    {
      "direction": "wstecz",
      "phrase": "funkcje liczące",
      "about": "funkcje Wspólnej Kasy z poprzedniej sekcji o programach na co dzień",
      "target": "sec-10-programy-uzywane-na-co-dzien",
      "quote": ""
    },
    {
      "direction": "wstecz",
      "phrase": "dane wejściowe, przetwarzanie, dane wyjściowe",
      "about": "zasada wejście–przetwarzanie–wyjście, pojęcia z glosariusza",
      "target": "glosariusz:dane-wejsciowe",
      "quote": ""
    },
    {
      "direction": "wstecz",
      "phrase": "wersję w terminalu",
      "about": "Wspólna Kasa uruchamiana w terminalu",
      "target": "glosariusz:terminal",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "„Przeglądarka” jest kluczowym pojęciem sekcji (strona działa w przeglądarce), a nie ma jej w glosariuszu ani definicji w tekście. Dodaj krótkie wyjaśnienie na miejscu, np. „przeglądarka (program do otwierania stron, np. Chrome czy Firefox)”.",
      "severity": "blokująca",
      "target": "przeglądarka"
    },
    {
      "kind": "przykład",
      "detail": "Zdanie „Zasada pod spodem jest ta sama: dane wejściowe, przetwarzanie, dane wyjściowe” to teza bez przykładu. Dodaj krótki przykład dla Wspólnej Kasy: wejście to kwoty wpisane przez znajomych, przetwarzanie to podział rachunku, wyjście to wynik na ekranie strony albo aplikacji.",
      "severity": "blokująca",
      "target": "Zasada pod spodem jest ta sama"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "„Serwer” ma definicję w nawiasie, ale „zapytania”, na które odpowiada, nie są wyjaśnione. Sugestia: „gdy przeglądarka o coś poprosi”.",
      "severity": "sugestia",
      "target": "zapytania"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "„System” (Android, iOS) jest użyty bez wyjaśnienia; sugestia: „system operacyjny telefonu, czyli program zarządzający urządzeniem, np. Android lub iOS”.",
      "severity": "sugestia",
      "target": "osobnej wersji dla każdego systemu"
    }
  ]
}
````
