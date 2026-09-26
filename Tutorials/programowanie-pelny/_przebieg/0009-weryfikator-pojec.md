# Krok 0009 · weryfikator_pojęć

Węzeł: `review` · dział: 1 · pytanie: 1 · próba: 1

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
- 2. Czym jest programowanie?
- 3. Kim jest programista i czym się zajmuje?
- 4. Czym jest język programowania?
- 5. Dlaczego komputer potrzebuje precyzyjnych instrukcji?
- 6. Czym różni się program od aplikacji?
- 7. Czym jest algorytm?
- 8. Jak przepis kulinarny przypomina algorytm?
- 9. Dlaczego kolejność kroków w algorytmie ma znaczenie?
- 10. Czym jest schemat blokowy?
- 11. Jak podzielić duży problem na mniejsze części?
- 12. Co to znaczy, że algorytm jest poprawny?
- 13. Czym jest kod źródłowy?
- 14. Do czego służy edytor kodu?
- 15. Co to znaczy uruchomić program?
- 16. Czym jest kompilator lub interpreter?
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
(pusty)
NOWE HASŁA Z TEJ SEKCJI: program komputerowy, instrukcja, programista

SEKCJA "Czym jest program komputerowy":
[[program-komputerowy|Program komputerowy]] to zapisany z góry ciąg poleceń, które komputer wykonuje krok po kroku, żeby zamienić dane na wynik. Komputer sam nic nie wie ani nie zgaduje: robi dokładnie to, co mu zapisano.

Pojedyncze polecenie to [[instrukcja|instrukcja]], czyli jeden mały, jednoznaczny krok, np. „dodaj dwie liczby” albo „wypisz tekst na ekranie”. Program to wiele takich instrukcji ułożonych w określonej kolejności. Kalkulator, przeglądarka i gra działają tak samo, tylko mają instrukcji bardzo dużo.

Prosty schemat każdego programu wygląda tak:

```text
dane na wejściu  -->  program (instrukcje)  -->  wynik na wyjściu
```

Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

Program „Wspólna Kasa” zrobi to za ciebie. Na wejściu dostanie listę wydatków (kto zapłacił i ile), a na wyjściu poda rozliczenie. Napisze go [[programista|programista]], czyli osoba, która zamienia potrzebę na instrukcje zrozumiałe dla komputera. Na razie nie piszemy kodu; ważne, że raz zapisane instrukcje można uruchamiać bez końca.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "wystarczy jedno zdanie; pełne omówienie w pytaniu 13. Np. że kod to zapisane instrukcje programu, czyli tekst, który pisze programista.",
      "severity": "sugestia",
      "target": "kodu",
      "source": "Na razie nie piszemy kodu",
      "status": "nowa"
    }
  ]
}
````
