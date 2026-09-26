# Krok 0173 · weryfikator_pojęć

Węzeł: `review` · dział: 2 · pytanie: 12 · próba: 2

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
NOWE HASŁA Z TEJ SEKCJI: specyfikacja wyniku, przypadek brzegowy

SEKCJA "Poprawny algorytm":
[[algorytm|Algorytm]] jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny z tym, czego od niego wymagamy. Nie wystarczy, że zadziałał raz na jednym przykładzie.

Najpierw trzeba więc ustalić, co znaczy „zgodny”. To [[specyfikacja-wyniku|specyfikacja wyniku]]: krótki opis, jaki wynik ma wyjść z jakich danych. Dla rozliczenia może brzmieć tak: suma wszystkich sald wynosi 0 zł, a nikomu nie znika ani nie przybywa grosza. Bez takiego opisu nie ma czego sprawdzać.

Potem sprawdzasz dwie rzeczy: czy algorytm zawsze dochodzi do [[warunek-zakonczenia|warunku zakończenia]] i czy wynik spełnia specyfikację. Ważne są zwłaszcza [[przypadek-brzegowy|przypadki brzegowe]], czyli dane na skraju dozwolonego zakresu: jedna osoba, brak wydatków, kwota, która nie dzieli się równo.

Ten ostatni przypadek łatwo przeoczyć. W kodzie kwoty liczymy w groszach, a znak `//` dzieli i odrzuca resztę: `10000 // 3` daje `3333`, nie `3333,33`.

```python
# poza kanonem: udział w groszach, dzielenie całkowite
def udzial(suma_gr, osoby):
    return suma_gr // osoby

print(udzial(12000, 4) * 4)
print(udzial(10000, 3) * 3)
```

```text
12000
9999
```

Dla 120 zł na czworo wszystko się zgadza. Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza. Dlatego w naszej liście kroków jest zdanie „Resztę groszy dopisz pierwszej osobie.”: bez niego algorytm byłby niepoprawny, choć pierwszy przykład by przeszedł.

Konsekwencja: poprawność sprawdzasz na wielu danych, w tym celowo niewygodnych. Do systematycznego sprawdzania wrócimy przy testowaniu programu.

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [wyjaśnienie] dzielenie całkowite: Wystarczy jedno zdanie; pełne omówienie w pytaniu 26. Czytelnik nie wie, że znak // dzieli i odrzuca resztę (10000 // 3 daje 3333, nie 3333,33). Bez tego nie zrozumie, dlaczego wychodzi 9999, a to sedno przykładu.
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
