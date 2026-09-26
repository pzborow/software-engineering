# Krok 0340 · weryfikator_odwołań

Węzeł: `review` · dział: 4 · pytanie: 20 · próba: 1

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
- wstecz: „dane trzeba gdzieś przechowywać” → sec-04-czym-jest-dana (poprzednia sekcja zapowiedziała zmienną jako miejsce przechowywania danych)
- w przód: „opiszemy to przy przypisaniu” → 25 (znak = i przypisanie wartości)
- w przód: „wyjaśnimy przy typach danych” → 23 (nazwy rodzajów danych)

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

PÓŹNIEJSZE PYTANIA:
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
- [lm-15] kod jako zwykły plik tekstowy (dział 03): „Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów.”
- [lm-16] literówka zmienia kolor (dział 03): „Literówka w nazwie polecenia często od razu zmienia kolor, zanim cokolwiek uruchomisz.”
- [lm-17] przepis w szufladzie (dział 03): „Sam kod źródłowy leży wtedy jak przepis w szufladzie: nic się nie dzieje”
- [lm-18] zapisz, uruchom, przeczytaj (dział 03): „Tak wygląda codzienna praca: zapisz, uruchom, przeczytaj wynik.”
- [lm-19] brak kroku budowania (dział 03): „nie ma osobnego kroku budowania. Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie.”
- [lm-20] dzielenie przez 2 zamiast 3 (dział 03): „Python wykonał każdą instrukcję zgodnie z zapisem, tylko że zapis był zły”
- [lm-21] prnt zamiast print (dział 03): „interpreter nie zna takiego słowa”
- [lm-22] nieaktualny komentarz o dwóch osobach (dział 03): „linia `# udział na dwie osoby` stoi nad dzieleniem przez 3, więc kłamie”
- [lm-23] wyłączona instrukcja (dział 03): „zamiana instrukcji na komentarz „wyłącza” ją bez kasowania”
- [lm-24] imienia nie da się podzielić (dział 04): „Imienia „Ania” nie da się podzielić przez 2, bo to nie ma sensu”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-03-czym-jest-kod-zrodlowy] Czym jest kod źródłowy (dział 03): Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
- [sec-03-do-czego-sluzy-edytor] Do czego służy edytor (dział 03): Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.
- [sec-03-co-znaczy-uruchomic-program] Co znaczy uruchomić program (dział 03): Uruchomienie programu to polecenie, by Python wykonał instrukcje z pliku po kolei, a sam plik pozostaje bez zmian.
- [sec-03-kompilator-i-interpreter] Kompilator i interpreter (dział 03): Kompilator tłumaczy cały kod na osobny plik przed startem, a interpreter wykonuje kod na bieżąco, dlatego w Pythonie wystarczy zapisać i uruchomić.
- [sec-03-co-to-jest-blad-w-programie] Co to jest błąd w programie (dział 03): Błąd to rozbieżność między zamiarem a działaniem programu: czasem zatrzymuje go komunikat, a czasem zły wynik pojawia się po cichu.
- [sec-03-do-czego-sluza-komentarze] Do czego służą komentarze (dział 03): Komentarz zaczyna się od `#`, jest pomijany przez Pythona i ma wyjaśniać powód, a nie powtarzać kod; po zmianie kodu trzeba go zaktualizować.
- [sec-04-czym-jest-dana] Czym jest dana (dział 04): Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.

NOWA SEKCJA "Czym jest zmienna":
[[zmienna|Zmienna]] to nazwane miejsce w pamięci programu, w którym leży jedna [[dana|dana]]. Dzięki nazwie możesz tę daną wielokrotnie odczytać, użyć w obliczeniach albo zastąpić inną.

Pamiętasz, że dane trzeba gdzieś przechowywać, żeby użyć ich więcej niż raz. Właśnie do tego służy zmienna. Zamiast wpisywać `45.5` w kilku miejscach, nadajesz kwocie nazwę i posługujesz się nią. To trochę jak komórka w arkuszu, którą nazwałeś „kwota”, a potem odwołujesz się do niej po nazwie.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(imie, kwota, zaplacono)
kwota = 60
print(kwota + 10)
```

```text
Ania 45.5 True
70
```

Znak `=` nie oznacza tu „równa się” jak w matematyce. Znaczy: „zapisz to, co po prawej, pod nazwą po lewej”. Dokładniej opiszemy to przy przypisaniu.

Wartość zmiennej może się zmieniać w trakcie działania programu, stąd nazwa: po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce. Nazwa zostaje ta sama. W „Wspólnej Kasie” takie zmienne opisują pojedynczy wydatek: kto zapłacił, ile i czy już się rozliczył.

U siebie w `kasa.py` zobaczysz też, jakiego rodzaju daną trzyma każda zmienna. Nazwy tych rodzajów wyjaśnimy przy typach danych.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "dane trzeba gdzieś przechowywać",
      "about": "poprzednia sekcja zapowiedziała zmienną jako miejsce przechowywania danych",
      "target": "sec-04-czym-jest-dana",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "Dokładniej opiszemy to przy przypisaniu",
      "about": "znak = i przypisanie wartości",
      "target": "25",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "Nazwy tych rodzajów wyjaśnimy przy typach danych",
      "about": "nazwy rodzajów danych (typy)",
      "target": "23",
      "quote": ""
    },
    {
      "direction": "poza tutorialem",
      "phrase": "W „Wspólnej Kasie” takie zmienne opisują pojedynczy wydatek",
      "about": "projekt przewodni tutorialu, Wspólna Kasa",
      "target": "",
      "quote": ""
    },
    {
      "direction": "poza tutorialem",
      "phrase": "U siebie w `kasa.py` zobaczysz też",
      "about": "plik kasa.py w projekcie czytelnika",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "konkret",
      "detail": "Zdanie „U siebie w `kasa.py` zobaczysz też, jakiego rodzaju daną trzyma każda zmienna” nie mówi, jak to zobaczyć, a plik `kasa.py` nie został wcześniej przedstawiony w tej sekcji. Dodaj krótki przykład albo usuń zdanie i zostaw samą zapowiedź typów.",
      "target": "kasa.py",
      "severity": "sugestia"
    },
    {
      "kind": "język",
      "detail": "Porównanie „nazwałeś” zakłada rodzaj męski czytelnika. Lepiej: „komórka arkusza, która ma nazwę »kwota«”.",
      "target": "komórka w arkuszu",
      "severity": "sugestia"
    }
  ]
}
````
