# Krok 0142 · weryfikator_odwołań

Węzeł: `review` · dział: 2 · pytanie: 10 · próba: 1

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
- w przód: „Wrócimy do niego przy podziale problemu na części” → 11 (podział problemu na mniejsze części)
- w przód: „przykład, który będzie nam towarzyszył” → - (Wspólna Kasa wraca w kolejnych działach)
- w przód: „dostanie z niego kod dopiero później” → - (kod pojawi się w dalszych działach)

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

PÓŹNIEJSZE PYTANIA:
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

PUNKTY ZACZEPIENIA (ten i poprzedni dział):
- [lm-1] schemat programu (dział 01): „dane na wejściu  -->  program (instrukcje)  -->  wynik na wyjściu”
- [lm-2] czworo znajomych na wyjeździe (dział 01): „Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg.”
- [lm-3] pętla poprawek (dział 01): „Uruchamiasz program, patrzysz na wynik, znajdujesz pomyłkę i poprawiasz.”
- [lm-4] ścieżka od potrzeby do poprawek (dział 01): „potrzeba --> ustalenie, co program ma robić --> kroki --> kod --> sprawdzanie --> poprawki”
- [lm-5] pierwsza instrukcja w Pythonie (dział 01): „print("Cześć, Wspólna Kasa!")”
- [lm-6] lista precyzyjnych kroków (dział 01): „Resztę groszy dopisz pierwszej osobie.”
- [lm-7] Wspólna Kasa jako mały program (dział 01): „zacznie jako mały program: wczyta wydatki i wypisze, kto komu ile jest winien”
- [lm-8] algorytm rozliczenia w czterech krokach (dział 02): „Podziel sumę przez liczbę osób: to udział jednej osoby.”
- [lm-9] przepis dla kogoś, kto nie gotował (dział 02): „wyobraź sobie przepis dla kogoś, kto nigdy nie gotował”
- [lm-10] mierzalny warunek pieczenia (dział 02): „„Piecz 40 minut” albo „piecz, aż termometr pokaże 95°C w środku” da się zmierzyć.”
- [lm-11] odejmowanie przed policzeniem udziału (dział 02): „Źle:     udział jeszcze nieznany (0 zł) --> Ala: 60 - 0 = +60 zł”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-01-czym-jest-program-komputerowy] Czym jest program komputerowy (dział 01): Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
- [sec-01-czym-jest-programowanie] Czym jest programowanie (dział 01): Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.
- [sec-01-kim-jest-programista] Kim jest programista (dział 01): Programista zamienia potrzebę na działający program, a pisanie kodu to tylko jeden z etapów tej pracy.
- [sec-01-czym-jest-jezyk-programowania] Czym jest język programowania (dział 01): Język programowania to ścisły zestaw słów i reguł zapisu, dzięki któremu człowiek wyraża instrukcje tak, by komputer wykonał je jednoznacznie.
- [sec-01-po-co-komputerowi-precyzja] Po co komputerowi precyzja (dział 01): Komputer wykonuje dokładnie to, co zapisano, więc każdy szczegół, który człowiek by sobie dopowiedział, trzeba podać wprost.
- [sec-01-program-a-aplikacja] Program a aplikacja (dział 01): Aplikacja to program z oprawą dla użytkownika, więc każda aplikacja jest programem, ale nie odwrotnie.
- [sec-02-czym-jest-algorytm] Czym jest algorytm (dział 02): Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
- [sec-02-przepis-jako-algorytm] Przepis jako algorytm (dział 02): Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
- [sec-02-kolejnosc-krokow-algorytmu] Kolejność kroków algorytmu (dział 02): Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.

NOWA SEKCJA "Czym jest schemat blokowy":
[[schemat-blokowy|Schemat blokowy]] to rysunek [[algorytm|algorytmu]]: każdy krok jest w ramce, a strzałki pokazują, w jakiej kolejności je wykonać. Działa jak mapa, po której palcem przejdziesz od początku do końca.

Używa kilku umownych kształtów. Owal oznacza początek albo koniec, prostokąt to zwykły krok, a romb to pytanie, po którym droga rozwidla się na „tak” i „nie”. Krok wykonujesz, gdy dojdziesz do niego strzałką, a nie dlatego, że stoi niżej na kartce.

Oto rozliczenie „Wspólnej Kasy” z trzema osobami, narysowane znakami tekstowymi:

```text
( Start )
    |
    v
[ Zsumuj wydatki ]
    |
    v
[ Podziel sumę przez liczbę osób = udział ]
    |
    v
[ Weź kolejną osobę ]
    |
    v
< Wpłaciła więcej niż udział? > --tak--> [ Ma zwrot ] --+
    |nie                                                |
    v                                                   |
[ Ma dopłacić ] ----------------------------------------+
    |
    v
< Są jeszcze osoby? > --tak--> (wróć do „Weź kolejną osobę”)
    |nie
    v
( Koniec )
```

Rysunek ma dwie zalety. Rozgałęzienia i powroty widać od razu, a w opisie słownym łatwo je przeoczyć. Poza tym pokazuje, gdzie algorytm się kończy, czyli sprawdzalny [[warunek-zakonczenia|warunek zakończenia]].

Konsekwencja: schemat pozwala sprawdzić algorytm na kartce, zanim powstanie [[kod|kod]]. Wrócimy do niego przy podziale problemu na części, a „Wspólna Kasa”, przykład, który będzie nam towarzyszył, dostanie z niego kod dopiero później.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "rozliczenie „Wspólnej Kasy” z trzema osobami",
      "about": "rozliczenie z Wspólnej Kasy, wcześniej zapisane jako algorytm w czterech krokach",
      "target": "lm-8",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "Wrócimy do niego przy podziale problemu na części",
      "about": "powrót do schematu blokowego przy dzieleniu problemu na mniejsze części",
      "target": "11",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "przykład, który będzie nam towarzyszył",
      "about": "Wspólna Kasa jako przykład wracający w kolejnych działach",
      "target": "",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "dostanie z niego kod dopiero później",
      "about": "Wspólna Kasa dostanie kod na podstawie schematu w dalszych działach",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "diagram",
      "detail": "Na rysunku strzałka z „Ma zwrot” schodzi do linii z plusem i łączy się z linią spod „Ma dopłacić”, ale strzałka „Ma dopłacić” wskazuje w lewo/na plus, a dalej biegnie pionowa kreska do „Są jeszcze osoby?”. Czytelnik spoza IT może nie zobaczyć, że obie gałęzie schodzą się przed pytaniem. Warto dodać strzałkę wchodzącą do „Są jeszcze osoby?” z obu gałęzi albo jedno zdanie opisujące, że obie drogi się łączą.",
      "target": "diagram rozliczenia",
      "severity": "sugestia"
    },
    {
      "kind": "konkret",
      "detail": "Pytanie „Wpłaciła więcej niż udział?” nie mówi, co z osobą, która wpłaciła dokładnie tyle, ile wynosi udział (trafia do „Ma dopłacić”). Można dodać krótką uwagę, że wtedy dopłata wynosi 0 zł.",
      "target": "romb decyzyjny",
      "severity": "sugestia"
    }
  ]
}
````
