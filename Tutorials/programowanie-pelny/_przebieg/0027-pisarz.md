# Krok 0027 · pisarz

Węzeł: `write` · dział: 1 · pytanie: 3 · próba: 1

## Prompt

````text
Jesteś autorem tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Piszesz jedną sekcję działu 01: "Czym jest programowanie".
PYTANIE 3: Kim jest programista i czym się zajmuje?

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
W tym dziale wątek rozwija się tak: Przedstawiamy problem: rozliczanie wydatków na wyjeździe w arkuszu jest żmudne, więc opisujemy, co miałby robić program „Wspólna Kasa” i kto (programista) go napisze, jeszcze bez kodu.

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
- OBIETNICA DO SPEŁNIENIA W TEJ SEKCJI: „osoba, która zamienia potrzebę na instrukcje” (rola programisty, omówiona później)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykład, który będzie nam towarzyszył” (zapowiedź, że „Wspólna Kasa” wróci w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się później)
- Pole landmarks: 1-3 miejsca TEJ sekcji, do których warto będzie nawiązać (charakterystyczny przykład, błąd, decyzja,
  porównanie, obraz), z krótką nazwą i dokładnym cytatem. Z nich korzystają kolejne sekcje.

Punkty zaczepienia, do których wolno nawiązać (starsze już wyblakły):
- [lm-1] schemat programu (dział 01): „dane na wejściu  -->  program (instrukcje)  -->  wynik na wyjściu”
- [lm-2] czworo znajomych na wyjeździe (dział 01): „Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg.”
- [lm-3] pętla poprawek (dział 01): „Uruchamiasz program, patrzysz na wynik, znajdujesz pomyłkę i poprawiasz.”

Sekcje z tego i poprzedniego działu:
- [sec-01-czym-jest-program-komputerowy] Czym jest program komputerowy (dział 01): Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
- [sec-01-czym-jest-programowanie] Czym jest programowanie (dział 01): Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.

Późniejsze pytania (tylko do pola target, nie do tekstu):
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

Pole answer: samodzielna odpowiedź na pytanie w 2-5 zdaniach, bez kodu (trafi pod pytanie w rozwijanym bloku).
Pole takeaway: jedno zdanie do listy "Co zapamiętać".

Pozostałe pytania tego działu (odpowiesz na nie w kolejnych sekcjach, nie teraz):
- 4. Czym jest język programowania?
- 5. Dlaczego komputer potrzebuje precyzyjnych instrukcji?
- 6. Czym różni się program od aplikacji?

Dotychczasowe działy i sekcje:
Dział 01. Czym jest programowanie
  - Czym jest program komputerowy: Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
  - Czym jest programowanie: Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.

Glosariusz (id: termin):
- program-komputerowy: program komputerowy
- instrukcja: instrukcja
- programista: programista
- programowanie: programowanie
- jezyk-programowania: język programowania

POPRZEDNIA SEKCJA (dla ciągłości, nie powtarzaj jej):
## Czym jest programowanie
[[programowanie|Programowanie]] to tworzenie programów: zamiana problemu na ciąg instrukcji, które komputer wykona bez twojego udziału. Samo pisanie jest tylko jednym z etapów, a największą część pracy zajmuje wymyślenie rozwiązania.

Zwykle wygląda to tak:

```text
problem --> kroki rozwiązania --> zapis dla komputera --> uruchomienie --> poprawki
                   ^                                                         |
                   +---------------------------------------------------------+
```

Wróćmy do czworga znajomych z wyjazdu. Najpierw trzeba dokładnie ustalić, co jest problemem: kto komu ile ma oddać, żeby każdy zapłacił tyle samo. Potem rozbijasz to na kroki, które wykonałbyś na kartce: zsumuj wydatki, podziel przez liczbę osób, porównaj z tym, co kto zapłacił. Dopiero taki opis zapisujesz w [[jezyk-programowania|języku programowania]], czyli w ściśle określonym języku, który komputer potrafi odczytać. Tym językiem zajmiemy się osobno.

Pierwsza wersja rzadko działa idealnie. Uruchamiasz program, patrzysz na wynik, znajdujesz pomyłkę i poprawiasz. Ta pętla poprawek to normalna część pracy, a nie dowód, że coś poszło nie tak.

Zyskujesz na tym jedną rzecz: raz opisane rozwiązanie działa przy każdym kolejnym wyjeździe, dla dowolnych kwot.
````

## Odpowiedź

````json
{
  "title": "Kim jest programista",
  "body": "[[programista|Programista]] to osoba, która zamienia potrzebę na instrukcje: bierze problem opisany zwykłymi słowami i tworzy program, który go rozwiązuje. Pisanie kodu to tylko część tej pracy.\n\nWeźmy czworo znajomych z wyjazdu, którzy męczą się z rozliczaniem wydatków w arkuszu. Ktoś musi ustalić, czego naprawdę potrzebują: czy program ma tylko wyliczyć, kto komu ile oddaje, czy też pamiętać kolejne wyjazdy. Potem opisuje rozwiązanie krok po kroku, zapisuje je w języku programowania, sprawdza na kilku przykładach i poprawia błędy.\n\n```text\npotrzeba --> ustalenie, co program ma robić --> kroki --> kod --> sprawdzanie --> poprawki\n```\n\nProgramista sporo czasu spędza więc na rozmowie, myśleniu, czytaniu cudzego kodu i szukaniu przyczyn błędów. Rzadko zaczyna od pustej strony, często rozwija program, który już istnieje.\n\nNie trzeba być programistą z zawodu, żeby programować. Osoba spoza IT, która napisze mały program do własnych rozliczeń, wykonuje tę samą pracę, tylko na mniejszą skalę.\n\nNa razie nie piszemy kodu. Ten problem z wydatkami będzie jednak przykładem, który będzie nam towarzyszył: program „Wspólna Kasa” zbudujemy razem, a ty przećwiczysz w tej roli.",
  "answer": "Programista to osoba, która zamienia potrzebę na działające instrukcje dla komputera. Ustala, co program ma robić, opisuje rozwiązanie krokami, zapisuje je w języku programowania, sprawdza i poprawia. Kod to tylko jeden z etapów, resztę zajmuje myślenie, rozmowa i szukanie błędów.",
  "takeaway": "Programista zamienia potrzebę na instrukcje: ustala, co program ma robić, opisuje kroki, pisze kod, sprawdza go i poprawia.",
  "references": [
    {
      "direction": "wstecz",
      "phrase": "czworo znajomych z wyjazdu",
      "about": "przykład rozliczenia wydatków",
      "target": "lm-2"
    },
    {
      "direction": "w przód",
      "phrase": "przykładem, który będzie nam towarzyszył",
      "about": "Wspólna Kasa wróci w kolejnych działach"
    },
    {
      "direction": "w przód",
      "phrase": "Na razie nie piszemy kodu.",
      "about": "kod pojawi się później"
    }
  ],
  "landmarks": [
    {
      "label": "schemat pracy programisty",
      "quote": "potrzeba --> ustalenie, co program ma robić --> kroki --> kod --> sprawdzanie --> poprawki"
    }
  ],
  "new_terms": [],
  "canon_changes": [],
  "versions": [],
  "workshop": []
}
````
