# Krok 1103 · weryfikator_pojęć

Węzeł: `review` · dział: 10 · pytanie: 57 · próba: 1

## Prompt

````text
Jesteś weryfikatorem pojęć. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dziedzina: Programowanie od podstaw.

Przeczytaj sekcję i wskaż pojęcia z dziedziny, które DOSŁOWNIE występują w tekście, czytelnik musi je znać,
żeby zrozumieć sekcję, a które NIE są w glosariuszu, NIE są oznaczone [[id|...]] i NIE są wyjaśnione w tekście.
Nie zgłaszaj pojęć, których w tekście nie ma (to nie jest recenzja kompletności), ani pojęć, które czytelnik zna.
Zgłaszaj najwyżej 3 najważniejsze braki: kind="wyjaśnienie", target=pojęcie dokładnie w brzmieniu z tekstu,
detail=czego czytelnikowi brakuje.

ODWOŁANIA W PRZÓD: jeśli pojęcie jest tematem jednego z późniejszych pytań (lista niżej), tutaj wystarczy
jedno zdanie wyjaśnienia przy pierwszym użyciu. Gdy takie zdanie jest, nie zgłaszaj pojęcia. Gdy go brak,
zgłoś je z detail="wystarczy jedno zdanie; pełne omówienie w pytaniu N".

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

PÓŹNIEJSZE PYTANIA:
- 58. Jak od pomysłu dojść do działającego programu?
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
- 60. Od czego zacząć samodzielną naukę programowania?
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

GLOSARIUSZ:
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
NOWE HASŁA Z TEJ SEKCJI: serwer

SEKCJA "Strona internetowa a aplikacja mobilna":
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
  "ok": true,
  "needs": []
}
````
