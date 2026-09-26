# Krok 0224 · weryfikator_odwołań

Węzeł: `review` · dział: 3 · pytanie: 15 · próba: 1

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
- wstecz: „Sam kod źródłowy” → lm-15 (kod jako zwykły plik tekstowy)
- w przód: „wyjaśnimy w następnej części” → 16 (interpreter i kompilator)

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

PÓŹNIEJSZE PYTANIA:
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
- [lm-8] algorytm rozliczenia w czterech krokach (dział 02): „Podziel sumę przez liczbę osób: to udział jednej osoby.”
- [lm-9] przepis dla kogoś, kto nie gotował (dział 02): „wyobraź sobie przepis dla kogoś, kto nigdy nie gotował”
- [lm-10] mierzalny warunek pieczenia (dział 02): „„Piecz 40 minut” albo „piecz, aż termometr pokaże 95°C w środku” da się zmierzyć.”
- [lm-11] odejmowanie przed policzeniem udziału (dział 02): „Źle:     udział jeszcze nieznany (0 zł) --> Ala: 60 - 0 = +60 zł”
- [lm-12] schemat rozliczenia z rombem (dział 02): „< Wpłaciła więcej niż udział? > --tak--> [ Ma zwrot ] --+”
- [lm-13] drzewo podziału rozliczenia (dział 02): „Rozlicz wyjazd”
- [lm-14] brakujący grosz (dział 02): „Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza.”
- [lm-15] kod jako zwykły plik tekstowy (dział 03): „Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów.”
- [lm-16] literówka zmienia kolor (dział 03): „Literówka w nazwie polecenia często od razu zmienia kolor, zanim cokolwiek uruchomisz.”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-02-czym-jest-algorytm] Czym jest algorytm (dział 02): Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
- [sec-02-przepis-jako-algorytm] Przepis jako algorytm (dział 02): Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
- [sec-02-kolejnosc-krokow-algorytmu] Kolejność kroków algorytmu (dział 02): Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.
- [sec-02-czym-jest-schemat-blokowy] Czym jest schemat blokowy (dział 02): Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, dzięki czemu rozgałęzienia, powroty i koniec widać, zanim powstanie kod.
- [sec-02-podzial-problemu-na-czesci] Podział problemu na części (dział 02): Dziel problem na części z jasnym wejściem i wynikiem, aż każdą da się opisać jednym zdaniem i sprawdzić osobno.
- [sec-02-poprawny-algorytm] Poprawny algorytm (dział 02): Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, także w przypadkach brzegowych.
- [sec-03-czym-jest-kod-zrodlowy] Czym jest kod źródłowy (dział 03): Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
- [sec-03-do-czego-sluzy-edytor] Do czego służy edytor (dział 03): Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.

NOWA SEKCJA "Co znaczy uruchomić program":
Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam [[kod-zrodlowy|kod źródłowy]] leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś go nie zacznie realizować.

Plik z kodem jest [[uruchamianie-programu|uruchamiany]] przez inny program, który go czyta i wykonuje linia po linii. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.

Polecenie wpisujemy w [[terminal|terminalu]], czyli oknie, w którym komputer przyjmuje polecenia pisane tekstem i pokazuje odpowiedzi tekstem. Przykład to nasz plik `rozlicz.py`:

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

W terminalu wpisujemy `python rozlicz.py`, a program wypisuje:

```text
Wspólna Kasa
100.0
```

Kolejność wyjścia jest taka sama jak kolejność linii, bo instrukcje wykonują się jedna po drugiej. Wynik `100.0` to 300 zł podzielone na trzy osoby.

Uruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. Tak wygląda cała praca programisty: zapisz, uruchom, przeczytaj wynik.
````

## Odpowiedź

````json
{
  "ok": false,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "Sam kod źródłowy leży wtedy jak przepis w szufladzie",
      "about": "kod źródłowy jako plik z instrukcjami",
      "target": "lm-15"
    },
    {
      "direction": "w przód",
      "phrase": "wyjaśnimy w następnej części",
      "about": "czym jest wykonawca programu i czym różni się od kompilatora",
      "target": "16"
    }
  ],
  "needs": [
    {
      "kind": "odwołanie",
      "severity": "blokująca",
      "target": "[[uruchamianie-programu|uruchamiany]]",
      "detail": "Link wskazuje hasło „uruchamianie-programu”, którego nie ma w glosariuszu. Usuń znacznik linku (pojęcie i tak jest zdefiniowane w pierwszym zdaniu sekcji) albo dodaj hasło do glosariusza.",
      "source": "Plik z kodem jest [[uruchamianie-programu|uruchamiany]]"
    },
    {
      "kind": "odwołanie",
      "severity": "sugestia",
      "target": "lm-15",
      "detail": "Deklarowane nawiązanie „Sam kod źródłowy” to zwykłe użycie pojęcia, a zdanie nie odnosi się do miejsca, gdzie mowa o pliku tekstowym. Można je zostawić lub dopisać „jak wiesz, zwykły plik tekstowy”.",
      "source": "Sam kod źródłowy leży wtedy jak przepis w szufladzie"
    },
    {
      "kind": "konkret",
      "severity": "sugestia",
      "target": "terminal",
      "detail": "„Terminal” jest zdefiniowany w tekście, ale nie ma go w glosariuszu; warto dodać hasło, bo pojęcie wróci w kolejnych sekcjach.",
      "source": "Polecenie wpisujemy w [[terminal|terminalu]]"
    },
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Tak wygląda cała praca programisty",
      "detail": "Przesada: praca programisty to też projektowanie, testowanie, szukanie błędów. Zmień na „Tak wygląda podstawowy rytm pracy”.",
      "source": "Tak wygląda cała praca programisty: zapisz, uruchom, przeczytaj wynik."
    }
  ]
}
````
