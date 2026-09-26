# Krok 0137 · pisarz

Węzeł: `write` · dział: 2 · pytanie: 10 · próba: 1

## Prompt

````text
Jesteś autorem tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Piszesz jedną sekcję działu 02: "Algorytmy i myślenie krokowe".
PYTANIE 10: Czym jest schemat blokowy?

ZASADY TEMPA I FORMY (wzorzec: zwięzły tutorial techniczny):
- Sekcja odpowiada na jedno pytanie. Zacznij od sedna odpowiedzi w 1-2 zdaniach, potem mechanizm, na końcu konsekwencja.
- Krótkie akapity po 2-4 zdania. Proza sekcji: 80-250 słów. Nie pisz wstępów typu "W tej sekcji omówimy".
- Najwyżej jeden blok kodu (wyjątkowo dwa), maks. 15 linii. Kod pokazuje jedną rzecz: pomiń importy i boilerplate, resztę zastąp `...`.
- Kod, który da się uruchomić samodzielnie i coś wypisuje, pokaż razem z wynikiem: bezpośrednio pod nim blok ```text
  z dokładnym wyjściem programu (dokładnie tym, co wypisze, znak w znak). Szkicom z `...` wyniku nie podawaj.
- Bloki kodu wyłącznie w językach: python, text. Żadnych innych języków programowania.
- Porównując 2+ opcje, użyj małej tabeli. Przepływ pokaż diagramem ```text ze strzałkami.
- Nie powtarzaj tego, co już zostało powiedziane w poprzednich sekcjach; możesz się do tego odwołać nazwą sekcji, nigdy numerem.
- Pojęcia z dziedziny oznaczaj przy pierwszym użyciu w sekcji jako [[id|tekst]], np. [[driven-port|port wyjściowy]].
  Używaj id z glosariusza. Nowe pojęcie dodaj do new_terms (id kebab-case ASCII, definicja 1-2 zdania)
  i wyjaśnij je jednym zdaniem w tekście przy pierwszym użyciu. Najwyżej 3 nowe pojęcia na sekcję.
  Pojęcie, które jest tematem późniejszego pytania, możesz użyć, ale wyjaśnij je jednym zdaniem przy pierwszym użyciu.
  Przy poprawianiu wersji zachowaj w new_terms wszystkie nowe pojęcia, które nadal oznaczasz w tekście.
- Nie pisz nagłówka sekcji w body; tytuł podaj w polu title. W body możesz użyć ### dla podpunktów, rzadko.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Zapisujemy rozliczenie jako algorytm krok po kroku i schemat blokowy (zsumuj, podziel, porównaj wpłaty z udziałem), dzieląc problem na części, które później staną się funkcjami.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
(jeszcze nic)
```
Zaplanowane, jeszcze niepokazane: rozlicz.py (plik programu (skrypt główny)), wydatki.csv (plik danych), wydatki (zmienna (lista słowników)), osoby (zmienna (lista tekstów)), suma_wydatkow (funkcja), udzial_na_osobe (funkcja), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), zapytaj_o_wydatek (funkcja), sprawdz_kwote (funkcja), wypisz_podsumowanie (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

Zasady wątku:
- Kod w sekcji używa elementów kanonu z dokładnie tymi nazwami i deklaracjami.
- Każdy nowy element i każdą zmianę deklaracji zadeklaruj w canon_changes z module="przykład" (dodaj/zmień + reason).
  Zaplanowany element przy pierwszym użyciu deklaruj jako "dodaj" z pełną deklaracją.
- Temat pytania ma pierwszeństwo przed wątkiem. Kontrprzykład ("źle: ...") albo porównanie spoza wątku
  oznacz pierwszą linią bloku: komentarz „poza kanonem”.

WARSZTAT (wątek wplatany „warsztat”, pole workshop): Wspólna Kasa krok po kroku
Czytelnik buduje u siebie w terminalu mały program w Pythonie do rozliczania wspólnych wydatków znajomych na wyjeździe. Program rośnie od pierwszego „Hello” do wersji z plikiem, funkcjami i testami.
Cel całości: Czytelnik zaczyna od sprawdzenia, że Python działa, i pisze pierwszy skrypt. Potem wprowadza dane o wydatkach, liczy sumy i decyzje, dodaje pętle po liście, wydziela funkcje, wczytuje dane z pliku i od użytkownika. Na końcu program sprawdza dane, ma testy i wersje w git, a czytelnik widzi, jak go rozbudować lub zautomatyzować.
Punkt startowy u czytelnika: Dowolny system (Windows, macOS lub Linux) z terminalem (PowerShell, bash lub zsh), zainstalowany Python 3.13 (sprawdzenie: python --version, na macOS/Linux ewentualnie python3 --version) oraz prosty edytor kodu, np. VS Code lub Notatnik. Pusty katalog roboczy ~/wspolna_kasa, w którym czytelnik otwiera terminal.
W tym dziale: (brak planu kroków; dodaj krok tylko, gdy sekcja naprawdę coś u czytelnika zmienia)

Stan u czytelnika przed tą sekcją (wiążący, dokładna treść plików):
```text
(brak plików)
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

Zasady warsztatu:
- W polu workshop podaj kroki, które czytelnik wykonuje u siebie po przeczytaniu tej sekcji, w kolejności:
  kind="plik": path, lang, content = PEŁNA nowa treść pliku (cały plik; to, co się zmieniło, pokaże czytelnikowi kod);
  kind="polecenie": command, lang powłoki, output = dokładnie to, co czytelnik zobaczy; fails=true dla celowego błędu.
- Kroki są kompletne i wykonywalne dosłownie: bez `...`, bez „uzupełnij sam”, z prawdziwymi wynikami.
- Kontynuuj stan powyżej: istniejące pliki zmieniaj tylko tam, gdzie dotyczy tego sekcja; resztę przepisz bez zmian.
- Celowy błąd (np. literówka, zła wartość) pokaż jako polecenie z fails=true i prawdziwym komunikatem, a poprawkę
  najpóźniej w ostatniej sekcji działu.
- Sekcja, w której nie ma nic do zrobienia, ma puste workshop. Nie na siłę.
- Tekst sekcji może odwoływać się do warsztatu („u siebie masz już plik…”). Przykłady w tekście mogą być inne niż warsztat.

WERSJE OBOWIĄZUJĄCE W TUTORIALU: Python 3.13
- Kod i twierdzenia muszą być zgodne z tymi wersjami.
- Pole versions: wpisz te wersje, od których naprawdę zależy kod albo twierdzenie tej sekcji (np. flaga, argument,
  składnia albo zachowanie, które zmieniło się między wersjami). Gdy sekcja od wersji nie zależy, zostaw puste.
- Inną wersję niż obowiązująca wpisz tylko świadomie, z uzasadnieniem w why.

ODWOŁANIA (pole references):
- Nawiązanie („jak widzieliśmy”, „ten błąd z napiwkiem”) wolno zrobić do punktu zaczepienia z listy (target = lm-N),
  do sekcji z tego lub poprzedniego działu (target = id w nawiasach) albo do hasła glosariusza (target "glosariusz:<id>").
  Starsze rzeczy wyjaśnij na miejscu jednym zdaniem. Zwykłe użycie pojęcia nie jest nawiązaniem, nie deklaruj go.
- Obietnica („opiszemy to później”, „wrócimy do tego przy pętlach”) zapowiada temat, który tutorial naprawdę omówi dalej.
  Jeśli wiesz, które późniejsze pytanie go omówi, podaj jego numer w target; inaczej zostaw target puste.
  W tekście pisz naturalnie, o temacie: nigdy nie wspominaj numerów ani „pytań” z listy, czytelnik ich nie zna.
  „Temat na osobny kurs” oznacz direction="poza tutorialem".
- phrase: dokładny fragment zdania z sekcji (bez [[...]]), 2-8 słów, który stanie się linkiem.
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykład, który będzie nam towarzyszył” (zapowiedź, że „Wspólna Kasa” wróci w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się później)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykładem, który będzie nam towarzyszył” (Wspólna Kasa jako przykład wracający w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Na razie nie piszemy kodu” (kod pojawi się w dalszych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „języku, którego użyjemy w tym tutorialu” (Python jako język tutorialu)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”” (Python i budowa programu „Wspólna Kasa” omówione później)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”” (zapowiedź, że Wspólna Kasa wraca w kolejnych działach)
- Pole landmarks: 1-3 miejsca TEJ sekcji, do których warto będzie nawiązać (charakterystyczny przykład, błąd, decyzja,
  porównanie, obraz), z krótką nazwą i dokładnym cytatem. Z nich korzystają kolejne sekcje.

Punkty zaczepienia, do których wolno nawiązać (starsze już wyblakły):
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

Sekcje z tego i poprzedniego działu:
- [sec-01-czym-jest-program-komputerowy] Czym jest program komputerowy (dział 01): Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
- [sec-01-czym-jest-programowanie] Czym jest programowanie (dział 01): Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.
- [sec-01-kim-jest-programista] Kim jest programista (dział 01): Programista zamienia potrzebę na działający program, a pisanie kodu to tylko jeden z etapów tej pracy.
- [sec-01-czym-jest-jezyk-programowania] Czym jest język programowania (dział 01): Język programowania to ścisły zestaw słów i reguł zapisu, dzięki któremu człowiek wyraża instrukcje tak, by komputer wykonał je jednoznacznie.
- [sec-01-po-co-komputerowi-precyzja] Po co komputerowi precyzja (dział 01): Komputer wykonuje dokładnie to, co zapisano, więc każdy szczegół, który człowiek by sobie dopowiedział, trzeba podać wprost.
- [sec-01-program-a-aplikacja] Program a aplikacja (dział 01): Aplikacja to program z oprawą dla użytkownika, więc każda aplikacja jest programem, ale nie odwrotnie.
- [sec-02-czym-jest-algorytm] Czym jest algorytm (dział 02): Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
- [sec-02-przepis-jako-algorytm] Przepis jako algorytm (dział 02): Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
- [sec-02-kolejnosc-krokow-algorytmu] Kolejność kroków algorytmu (dział 02): Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.

Późniejsze pytania (tylko do pola target, nie do tekstu):
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

Pole answer: samodzielna odpowiedź na pytanie w 2-5 zdaniach, bez kodu (trafi pod pytanie w rozwijanym bloku).
Pole takeaway: jedno zdanie do listy "Co zapamiętać".

Pozostałe pytania tego działu (odpowiesz na nie w kolejnych sekcjach, nie teraz):
- 11. Jak podzielić duży problem na mniejsze części?
- 12. Co to znaczy, że algorytm jest poprawny?

Dotychczasowe działy i sekcje:
Dział 01. Czym jest programowanie
  - Czym jest program komputerowy: Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
  - Czym jest programowanie: Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.
  - Kim jest programista: Programista zamienia potrzebę na działający program, a pisanie kodu to tylko jeden z etapów tej pracy.
  - Czym jest język programowania: Język programowania to ścisły zestaw słów i reguł zapisu, dzięki któremu człowiek wyraża instrukcje tak, by komputer wykonał je jednoznacznie.
  - Po co komputerowi precyzja: Komputer wykonuje dokładnie to, co zapisano, więc każdy szczegół, który człowiek by sobie dopowiedział, trzeba podać wprost.
  - Program a aplikacja: Aplikacja to program z oprawą dla użytkownika, więc każda aplikacja jest programem, ale nie odwrotnie.
Dział 02. Algorytmy i myślenie krokowe
  - Czym jest algorytm: Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
  - Przepis jako algorytm: Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
  - Kolejność kroków algorytmu: Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.

Glosariusz (id: termin):
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

POPRZEDNIA SEKCJA (dla ciągłości, nie powtarzaj jej):
## Kolejność kroków algorytmu
Kolejność ma znaczenie, bo prawie każdy krok korzysta z wyniku poprzedniego. Zamiana miejsc sprawia, że krok dostaje dane, których jeszcze nie ma, i [[algorytm|algorytm]] daje zły wynik albo wcale nie działa.

Weźmy cztery kroki rozliczenia we „Wspólnej Kasie”. Ala wydała 60 zł, Bartek 40 zł, Czarek 20 zł. Najpierw sumujemy: 120 zł. Potem dzielimy przez trzy osoby: udział wynosi 40 zł. Na końcu odejmujemy udział od wpłaty każdego.

Teraz zamieńmy kroki: odejmujemy udział, zanim go policzyliśmy.

```text
# poza kanonem
Dobrze:  suma 120 zł --> udział 40 zł --> Ala: 60 - 40 = +20 zł
Źle:     udział jeszcze nieznany (0 zł) --> Ala: 60 - 0 = +60 zł
```

Krok „odejmij udział” nie miał czego odjąć. Zależność między krokami to właśnie taka sytuacja: jeden krok potrzebuje wyniku innego, więc musi stać po nim.

Nie każda para kroków jest tak związana. Policzenie osób i zsumowanie wydatków są niezależne, więc możesz zrobić je w dowolnej kolejności. Oba muszą jednak być gotowe przed dzieleniem.

Konsekwencja: pisząc algorytm, przy każdym kroku zapytaj, skąd bierze dane. Jeśli z wyniku innego kroku, ten krok stoi za nim. Komputer wykona kroki dokładnie w zapisanej kolejności i niczego sam nie przestawi.
````

## Odpowiedź

````json
{
  "title": "Czym jest schemat blokowy",
  "body": "[[schemat-blokowy|Schemat blokowy]] to rysunek [[algorytm|algorytmu]]: każdy krok jest w ramce, a strzałki pokazują, w jakiej kolejności je wykonać. Działa jak mapa, po której palcem przejdziesz od początku do końca.\n\nUżywa kilku umownych kształtów. Owal oznacza początek albo koniec, prostokąt to zwykły krok, a romb to pytanie, po którym droga rozwidla się na „tak” i „nie”. Krok wykonujesz, gdy dojdziesz do niego strzałką, a nie dlatego, że stoi niżej na kartce.\n\nOto rozliczenie „Wspólnej Kasy” z trzema osobami, narysowane znakami tekstowymi:\n\n```text\n( Start )\n    |\n    v\n[ Zsumuj wydatki ]\n    |\n    v\n[ Podziel sumę przez liczbę osób = udział ]\n    |\n    v\n[ Weź kolejną osobę ]\n    |\n    v\n< Wpłaciła więcej niż udział? > --tak--> [ Ma zwrot ] --+\n    |nie                                                |\n    v                                                   |\n[ Ma dopłacić ] ----------------------------------------+\n    |\n    v\n< Są jeszcze osoby? > --tak--> (wróć do „Weź kolejną osobę”)\n    |nie\n    v\n( Koniec )\n```\n\nRysunek ma dwie zalety. Rozgałęzienia i powroty widać od razu, a w opisie słownym łatwo je przeoczyć. Poza tym pokazuje, gdzie algorytm się kończy, czyli sprawdzalny [[warunek-zakonczenia|warunek zakończenia]].\n\nKonsekwencja: schemat pozwala sprawdzić algorytm na kartce, zanim powstanie [[kod|kod]]. Wrócimy do niego przy podziale problemu na części, a „Wspólna Kasa”, przykład, który będzie nam towarzyszył, dostanie z niego kod dopiero później.",
  "answer": "Schemat blokowy to rysunek algorytmu: kroki są w ramkach, a strzałki pokazują kolejność wykonania. Prostokąt oznacza krok, romb pytanie z rozgałęzieniem „tak” lub „nie”, a owal początek albo koniec. Dzięki temu widać rozgałęzienia, powroty i miejsce zakończenia, jeszcze zanim powstanie kod.",
  "takeaway": "Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, z rombami dla decyzji, więc kolejność, rozgałęzienia i koniec widać na jednym rysunku.",
  "new_terms": [
    {
      "id": "schemat-blokowy",
      "term": "schemat blokowy",
      "definition": "Rysunek algorytmu złożony z ramek (kroków, decyzji, początku i końca) połączonych strzałkami pokazującymi kolejność wykonania."
    }
  ],
  "references": [
    {
      "direction": "w przód",
      "phrase": "Wrócimy do niego przy podziale problemu na części",
      "about": "podział problemu na mniejsze części",
      "target": "11"
    },
    {
      "direction": "w przód",
      "phrase": "przykład, który będzie nam towarzyszył",
      "about": "Wspólna Kasa wraca w kolejnych działach",
      "target": ""
    },
    {
      "direction": "w przód",
      "phrase": "dostanie z niego kod dopiero później",
      "about": "kod pojawi się w dalszych działach",
      "target": ""
    }
  ],
  "landmarks": [
    {
      "label": "schemat rozliczenia z rombami",
      "quote": "< Wpłaciła więcej niż udział? > --tak--> [ Ma zwrot ] --+"
    },
    {
      "label": "mapa po kroku",
      "quote": "Działa jak mapa, po której palcem przejdziesz od początku do końca."
    }
  ]
}
````
