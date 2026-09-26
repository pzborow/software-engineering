# Krok 0851 · weryfikator_pojęć

Węzeł: `review` · dział: 8 · pytanie: 44 · próba: 1

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
NOWE HASŁA Z TEJ SEKCJI: dane wejściowe

SEKCJA "Dane wejściowe programu":
[[dane-wejsciowe|Dane wejściowe]] to wszystko, co program dostaje z zewnątrz, żeby mieć na czym pracować: wpisane słowo, liczba, zawartość pliku. Sam z siebie nie wie, kto zapłacił za zakupy ani ile, więc ktoś musi mu to podać.

Źródła są różne, ale idea ta sama: wartość pojawia się w programie, choć nie została zapisana w kodzie.

| Źródło | Przykład we „Wspólnej Kasie” |
|---|---|
| użytkownik | wpisuje imię i kwotę nowego wydatku |
| plik | `wydatki.csv` z listą dotychczasowych wydatków |
| inny program | dane wyeksportowane z aplikacji banku |

Do tej pory kwoty wpisywaliśmy w kodzie, np. `mazury = [45.5, 20, 12.5]`. Wtedy każda zmiana danych wymagała edycji programu. Dane wejściowe rozdzielają obie sprawy: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne.

Tak mogłoby wyglądać pobranie danych od użytkownika (szkic, do którego wrócimy przy pytaniu użytkownika):

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    ...
```

Ważna konsekwencja: program nie kontroluje, co dostanie. Ktoś może wpisać „abc” zamiast kwoty, a plik może być pusty. Dlatego dane wejściowe trzeba traktować ostrożnie i sprawdzać, a o wyniku, który program oddaje na zewnątrz, opowiemy przy [[dane-wejsciowe|danych wyjściowych]].
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "wystarczy jedno zdanie; pełne omówienie w pytaniu 46. Przy pierwszym użyciu w szkicu warto dodać, że input(...) to polecenie, które wyświetla podany tekst, czeka, aż użytkownik coś wpisze i zatwierdzi Enterem, po czym oddaje to jako wartość.",
      "severity": "sugestia",
      "source": "kto = input(\"Kto zapłacił? \")",
      "target": "input",
      "status": "nowa"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Format .csv nie jest znany początkującemu. Wystarczy pół zdania, np. że to zwykły plik tekstowy z danymi w wierszach, otwierany też w arkuszu kalkulacyjnym.",
      "severity": "sugestia",
      "source": "`wydatki.csv` z listą dotychczasowych wydatków",
      "target": "wydatki.csv",
      "status": "nowa"
    }
  ]
}
````
