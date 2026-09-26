# Krok 0525 · weryfikator_pojęć

Węzeł: `review` · dział: 5 · pytanie: 29 · próba: 2

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
NOWE HASŁA Z TEJ SEKCJI: instrukcja warunkowa, wcięcie

SEKCJA "Instrukcja warunkowa „jeśli… to…”":
[[instrukcja-warunkowa|Instrukcja warunkowa]] to polecenie, które wykonuje wybrany fragment kodu tylko wtedy, gdy warunek jest prawdziwy. W Pythonie zapisujemy ją słowem `if`, czyli „jeśli”.

Warunek to zwykle porównanie z poprzedniej sekcji, bo daje `True` albo `False`. Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej.

Które linie należą do warunku, pokazuje [[wciecie|wcięcie]]: przesunięcie linii o cztery spacje w prawo. Po warunku stawiamy dwukropek.

```python
kwota = 45.5
if kwota > 40:
    print("Kwota do sprawdzenia")
if kwota > 100:
    print("Bardzo duża kwota")
print("Koniec")
```

```text
Kwota do sprawdzenia
Koniec
```

Pierwszy warunek jest prawdziwy, więc jego linia się wykonała. Drugi jest fałszywy, więc jego wcięta linia została pominięta. Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.

Program przestaje więc biegnąć wszystkimi liniami po kolei: to, co wykona, zależy od danych. Co zrobić, gdy warunek jest fałszywy, pokażemy w następnej sekcji.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
