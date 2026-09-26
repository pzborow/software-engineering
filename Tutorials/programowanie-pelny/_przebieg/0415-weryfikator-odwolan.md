# Krok 0415 · weryfikator_odwołań

Węzeł: `review` · dział: 4 · pytanie: 24 · próba: 1

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
- wstecz: „Ta sama zasada, co przy `"45.5"`” → lm-27 (cudzysłów zmienia liczbę w tekst)
- w przód: „Jak to zapisać, pokażemy przy instrukcji warunkowej” → 29 (decyzje na podstawie wartości logicznej)

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
- wartosc-zmiennej: wartość zmiennej
- typ-danych: typ danych

PÓŹNIEJSZE PYTANIA:
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
- [lm-26] pudełko i kopia (dział 04): „Zmiana `kwota` nie ruszyła `kwota_stara`, bo do drugiego pudełka trafiła kopia wartości.”
- [lm-27] cztery znaki zamiast kwoty (dział 04): „`"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5”
- [lm-28] type() pokazuje typ (dział 04): „Typ sprawdzisz funkcją `type()`.”
- [lm-29] tabela typów Pythona (dział 04): „Oto podstawowe typy Pythona:”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-03-czym-jest-kod-zrodlowy] Czym jest kod źródłowy (dział 03): Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
- [sec-03-do-czego-sluzy-edytor] Do czego służy edytor (dział 03): Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.
- [sec-03-co-znaczy-uruchomic-program] Co znaczy uruchomić program (dział 03): Uruchomienie programu to polecenie, by Python wykonał instrukcje z pliku po kolei, a sam plik pozostaje bez zmian.
- [sec-03-kompilator-i-interpreter] Kompilator i interpreter (dział 03): Kompilator tłumaczy cały kod na osobny plik przed startem, a interpreter wykonuje kod na bieżąco, dlatego w Pythonie wystarczy zapisać i uruchomić.
- [sec-03-co-to-jest-blad-w-programie] Co to jest błąd w programie (dział 03): Błąd to rozbieżność między zamiarem a działaniem programu: czasem zatrzymuje go komunikat, a czasem zły wynik pojawia się po cichu.
- [sec-03-do-czego-sluza-komentarze] Do czego służą komentarze (dział 03): Komentarz zaczyna się od `#`, jest pomijany przez Pythona i ma wyjaśniać powód, a nie powtarzać kod; po zmianie kodu trzeba go zaktualizować.
- [sec-04-czym-jest-dana] Czym jest dana (dział 04): Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.
- [sec-04-czym-jest-zmienna] Czym jest zmienna (dział 04): Zmienna to nazwa, pod którą program przechowuje daną, żeby móc jej użyć wielokrotnie i w razie potrzeby zmienić.
- [sec-04-zmienna-jako-pudelko-z-etykieta] Zmienna jako pudełko z etykietą (dział 04): Zmienna to pudełko z etykietą: nazwa zostaje, w środku jest jedna wartość, którą można podmienić, a kopie są niezależne.
- [sec-04-liczba-a-tekst] Liczba a tekst (dział 04): Cudzysłów zmienia rodzaj danych: 45.5 to liczba, którą można dzielić, a "45.5" to tekst, którego dzielić się nie da.
- [sec-04-czym-jest-typ-danych] Czym jest typ danych (dział 04): Typ danych to rodzaj wartości (str, int, float, bool), który decyduje o tym, jakie działania są na niej możliwe.

NOWA SEKCJA "Wartość logiczna prawda/fałsz":
[[wartosc-logiczna|Wartość logiczna]] to dana, która ma tylko dwie możliwe wartości: prawda albo fałsz. W Pythonie zapisujesz je jako `True` i `False`, a ich typ to `bool`.

Pasuje do każdej odpowiedzi „tak albo nie”: czy wydatek jest zapłacony, czy kwota jest większa od zera. Nie ma nic pomiędzy. W arkuszu to odpowiednik pola wyboru: zaznaczone albo nie.

Zapisuje się je z wielkiej litery i bez cudzysłowu. Ta sama zasada, co przy `"45.5"`: `True` to wartość logiczna, a `"True"` w cudzysłowie to tylko tekst z czterech liter.

```python
zaplacono = True
print(zaplacono)
zaplacono = False
print(zaplacono)
print(type(zaplacono))
```

```text
True
False
<class 'bool'>
```

Zmienną logiczną podmieniasz jak każdą inną: po drugim przypisaniu `True` znika, a jej miejsce zajmuje `False`.

Konsekwencja: taka wartość służy programowi do podejmowania decyzji. Na podstawie `zaplacono` program będzie mógł wybrać, czy przypomnieć o długu. Jak to zapisać, pokażemy przy instrukcji warunkowej.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "Ta sama zasada, co przy `\"45.5\"`",
      "about": "cudzysłów zmienia wartość w tekst",
      "target": "lm-27",
      "quote": ""
    },
    {
      "direction": "wstecz",
      "phrase": "Zmienną logiczną podmieniasz jak każdą inną: po drugim przypisaniu `True` znika",
      "about": "podmiana wartości zmiennej, tak jak przy zmianie kwoty",
      "target": "lm-25",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "Jak to zapisać, pokażemy przy instrukcji warunkowej",
      "about": "zapisywanie decyzji na podstawie wartości logicznej",
      "target": "29",
      "quote": ""
    }
  ]
}
````
