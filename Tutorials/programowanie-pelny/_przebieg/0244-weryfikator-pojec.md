# Krok 0244 · weryfikator_pojęć

Węzeł: `review` · dział: 3 · pytanie: 16 · próba: 1

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
- 17. Co to jest błąd w programie?
- 18. Do czego służą komentarze w kodzie?
- 19. Czym jest dana w programie?
- 20. Czym jest zmienna?
- 21. Jak można porównać zmienną do pudełka z etykietą?
- 22. Czym różni się liczba od tekstu w programie?
- 23. Czym jest typ danych?
- 24. Co to jest wartość logiczna prawda/fałsz?
- 25. Do czego służy przypisanie wartości do zmiennej?
- 26. Jakie podstawowe działania matematyczne może wykonać program?
- 27. Jak program łączy ze sobą teksty?
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
NOWE HASŁA Z TEJ SEKCJI: kompilator, interpreter

SEKCJA "Kompilator i interpreter":
Kompilator i interpreter to programy, które przekładają [[kod-zrodlowy|kod źródłowy]] na działanie komputera, bo procesor sam nie rozumie tekstu z pliku. [[kompilator|Kompilator]] tłumaczy cały kod naraz na osobny, gotowy do uruchomienia plik. [[interpreter|Interpreter]] czyta kod i wykonuje go na bieżąco, instrukcja po instrukcji.

To ten wykonawca, o którym była mowa przy uruchamianiu programu. Gdy wpisujesz `python kasa.py`, [[python|Python]] działa jako interpreter: bierze plik i wykonuje go od góry.

| | Kompilator | Interpreter |
|---|---|---|
| Co robi | tłumaczy całość przed startem | wykonuje kod w trakcie czytania |
| Wynik | osobny plik do uruchomienia | brak pliku, od razu efekt |
| Uruchomienie po zmianie | najpierw kompilacja, potem start | zapisz i uruchom |

```text
kompilator:   kod źródłowy --> [kompilator] --> plik programu --> uruchomienie
interpreter:  kod źródłowy --> [interpreter] --> uruchomienie
```

Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania. Zmieniasz `kasa.py`, zapisujesz i uruchamiasz ponownie. W praktyce Python najpierw przekłada plik na pośredni zapis, ale z Twojej strony to jedno polecenie.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "target": "procesor",
      "detail": "Pojęcie pada w uzasadnieniu, po co w ogóle jest tłumaczenie kodu, a nie ma go w glosariuszu ani wyjaśnienia w tekście. Wystarczy krótkie zdanie: procesor to układ, który wykonuje działania komputera i rozumie tylko bardzo proste polecenia w własnym zapisie.",
      "severity": "sugestia",
      "source": "Kompilator i interpreter to programy, które przekładają kod źródłowy na działanie komputera, bo procesor sam nie rozumie tekstu z pliku."
    },
    {
      "kind": "wyjaśnienie",
      "target": "kroku budowania",
      "detail": "„Budowanie” nie jest wyjaśnione. Można dopisać, że chodzi o kompilację, czyli osobny etap przygotowania pliku do uruchomienia opisany wyżej.",
      "severity": "sugestia",
      "source": "nie ma osobnego kroku budowania"
    }
  ]
}
````
