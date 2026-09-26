# Krok 0363 · weryfikator_odwołań

Węzeł: `review` · dział: 4 · pytanie: 21 · próba: 1

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
- wstecz: „zmiany kwoty z poprzedniej sekcji” → lm-25 (po kwota = 60 stara kwota znika)

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
- zmienna: zmienna

PÓŹNIEJSZE PYTANIA:
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
- [lm-25] zmiana kwoty (dział 04): „po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-03-czym-jest-kod-zrodlowy] Czym jest kod źródłowy (dział 03): Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
- [sec-03-do-czego-sluzy-edytor] Do czego służy edytor (dział 03): Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.
- [sec-03-co-znaczy-uruchomic-program] Co znaczy uruchomić program (dział 03): Uruchomienie programu to polecenie, by Python wykonał instrukcje z pliku po kolei, a sam plik pozostaje bez zmian.
- [sec-03-kompilator-i-interpreter] Kompilator i interpreter (dział 03): Kompilator tłumaczy cały kod na osobny plik przed startem, a interpreter wykonuje kod na bieżąco, dlatego w Pythonie wystarczy zapisać i uruchomić.
- [sec-03-co-to-jest-blad-w-programie] Co to jest błąd w programie (dział 03): Błąd to rozbieżność między zamiarem a działaniem programu: czasem zatrzymuje go komunikat, a czasem zły wynik pojawia się po cichu.
- [sec-03-do-czego-sluza-komentarze] Do czego służą komentarze (dział 03): Komentarz zaczyna się od `#`, jest pomijany przez Pythona i ma wyjaśniać powód, a nie powtarzać kod; po zmianie kodu trzeba go zaktualizować.
- [sec-04-czym-jest-dana] Czym jest dana (dział 04): Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.
- [sec-04-czym-jest-zmienna] Czym jest zmienna (dział 04): Zmienna to nazwa, pod którą program przechowuje daną, żeby móc jej użyć wielokrotnie i w razie potrzeby zmienić.

NOWA SEKCJA "Zmienna jako pudełko z etykietą":
[[zmienna|Zmienną]] można porównać do pudełka z etykietą: etykieta to nazwa, a w środku leży jedna [[dana|dana]], czyli [[wartosc-zmiennej|wartość zmiennej]] (to, co aktualnie jest w pudełku). Program szuka pudełka po etykiecie i zagląda do środka.

```text
etykieta: kwota      etykieta: imie
┌──────────┐         ┌──────────┐
│   45.5   │         │  "Ania"  │
└──────────┘         └──────────┘
```

Porównanie tłumaczy trzy rzeczy. Pudełko mieści jedną wartość naraz, więc nowa wartość wypiera starą, jak w przypadku zmiany kwoty z poprzedniej sekcji. Etykieta zostaje, zmienia się tylko zawartość. Wreszcie każde pudełko żyje własnym życiem: kopia wartości do drugiego pudełka nie łączy ich na stałe.

```python
# poza kanonem
kwota_stara = 45.5
kwota = kwota_stara
kwota = 60
print(kwota_stara, kwota)
```

```text
45.5 60
```

Zmiana `kwota` nie ruszyła `kwota_stara`, bo do drugiego pudełka trafiła kopia wartości.

Obraz jest uproszczony: pod spodem Python działa nieco inaczej, ale na tym etapie to nie ma znaczenia. Ważna konsekwencja: etykieta ma być czytelna. W „Wspólnej Kasie” pudełko `kwota` jest zrozumiałe, a `x` zmusza do zgadywania, co w środku.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "zmiany kwoty z poprzedniej sekcji",
      "about": "nowa wartość zmiennej wypiera starą (kwota = 60)",
      "target": "lm-25",
      "quote": ""
    },
    {
      "direction": "poza tutorialem",
      "phrase": "W „Wspólnej Kasie” pudełko `kwota`",
      "about": "przykład przewodni „Wspólna Kasa”, nieobecny na listach punktów i sekcji",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "odwołanie",
      "severity": "sugestia",
      "target": "„Wspólnej Kasie”",
      "detail": "Nazwa „Wspólna Kasa” nie ma punktu zaczepienia w tym ani poprzednim dziale. Jeśli to program przewodni, dodaj pół zdania przypominającego, czym jest (np. „w programie do rozliczania wspólnych wydatków”). Czytelnik spoza IT może nie kojarzyć nazwy."
    }
  ]
}
````
