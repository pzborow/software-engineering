# Krok 1093 · weryfikator_pojęć

Węzeł: `review` · dział: 10 · pytanie: 56 · próba: 2

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
- 57. Czym różni się strona internetowa od aplikacji mobilnej?
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
NOWE HASŁA Z TEJ SEKCJI: (brak)

SEKCJA "Programy używane na co dzień":
Na co dzień używasz dziesiątek programów, choć rzadko o tym myślisz: komunikatora, mapy, banku w telefonie, arkusza kalkulacyjnego, przeglądarki. Każdy z nich to [[program-komputerowy|program]] albo [[aplikacja|aplikacja]], czyli program z oprawą dla użytkownika, i działa według tego samego schematu, który znasz z własnych skryptów.

Zawsze są [[dane-wejsciowe|dane wejściowe]], jakieś przetwarzanie i [[dane-wyjsciowe|dane wyjściowe]]:

| Program | Wejście | Co robi | Wyjście |
|---|---|---|---|
| Nawigacja | cel podróży, Twoja pozycja | wybiera najkrótszą trasę | trasa na mapie |
| Bank w telefonie | kwota i numer konta | sprawdza saldo, księguje przelew | potwierdzenie |
| Arkusz kalkulacyjny | liczby w komórkach | liczy wzory | sumy i wykresy |
| Wyszukiwarka | wpisane słowa | szuka i układa wyniki | lista stron |
| Alarm w telefonie | ustawiona godzina | porównuje ją z zegarem | dzwonek |

Pod spodem są te same klocki, które już budowałeś: zmienne, decyzje (`if`), pętle po listach, funkcje i pliki. Nawigacja też przegląda listę dróg i wybiera jedną, a bank też sprawdza dane od użytkownika, zanim cokolwiek zaksięguje.

Różni je skala i [[interfejs-uzytkownika|interfejs]]: przyciski i mapy zamiast pytań w terminalu. Program do dzielenia wspólnych wydatków między osoby, który budujesz w warsztacie (nazywamy go „Wspólna Kasa”), należy do tej samej rodziny: bierze wydatki, liczy i wypisuje, kto ile zapłacił. Jest po prostu mały. Czym różni się strona internetowa od aplikacji mobilnej, wyjaśnimy w następnej sekcji.

Konsekwencja: skoro gotowe programy to złożone proste kroki, da się je zrozumieć, a proste zadania z Twojej pracy da się zautomatyzować własnym małym programem.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "Słowo „skrypt” nie ma hasła w glosariuszu i nie jest wyjaśnione. Wystarczy zastąpić je słowem „program” albo dodać krótkie objaśnienie, np. „skrypt to mały program napisany do jednego zadania”.",
      "target": "własnych skryptów",
      "severity": "sugestia",
      "source": "Na co dzień używasz dziesiątek programów",
      "status": "nowa"
    }
  ]
}
````
