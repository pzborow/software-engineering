# Krok 0218 · pisarz

Węzeł: `write` · dział: 3 · pytanie: 15 · próba: 1

## Prompt

````text
Jesteś autorem tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Piszesz jedną sekcję działu 03: "Kod i jego uruchamianie".
PYTANIE 15: Co to znaczy uruchomić program?

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
W tym dziale wątek rozwija się tak: Powstaje pierwszy plik rozlicz.py w edytorze VS Code z komentarzami; uruchamiamy go interpreterem Pythona i widzimy pierwszy celowy błąd.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
rozlicz.py · plik programu (skrypt główny) · rozlicz.py
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), wydatki (zmienna (lista słowników)), osoby (zmienna (lista tekstów)), suma_wydatkow (funkcja), udzial_na_osobe (funkcja), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), zapytaj_o_wydatek (funkcja), sprawdz_kwote (funkcja), wypisz_podsumowanie (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

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
W tym dziale: Czytelnik sprawdza python --version, zapisuje w edytorze plik kasa.py z jednym print i komentarzem, uruchamia go poleceniem python kasa.py, po czym celowo psuje nazwę print i ogląda pierwszy błąd.

Stan u czytelnika przed tą sekcją (wiążący, dokładna treść plików):
```text
--- kasa.py ---
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
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
- OBIETNICA DO SPEŁNIENIA W TEJ SEKCJI: „jak to działa, pokażemy przy uruchamianiu programu” (czytanie i wykonywanie pliku z kodem przez osobny program)
- OBIETNICA DO SPEŁNIENIA W TEJ SEKCJI: „gdy wyjaśnimy, co to znaczy uruchomić program” (uruchamianie programu)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykład, który będzie nam towarzyszył” (zapowiedź, że „Wspólna Kasa” wróci w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się później)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykładem, który będzie nam towarzyszył” (Wspólna Kasa jako przykład wracający w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Na razie nie piszemy kodu” (kod pojawi się w dalszych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „języku, którego użyjemy w tym tutorialu” (Python jako język tutorialu)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”” (Python i budowa programu „Wspólna Kasa” omówione później)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”” (zapowiedź, że Wspólna Kasa wraca w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykład, który będzie nam towarzyszył” (Wspólna Kasa wraca w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „dostanie z niego kod dopiero później” (kod Wspólnej Kasy pojawi się w dalszych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykład, który będzie nam towarzyszył w kolejnych działach” (Wspólna Kasa wraca w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „nasz przykład, który będzie nam towarzyszył” (Wspólna Kasa jako przykład wracający w kolejnych działach)
- Pole landmarks: 1-3 miejsca TEJ sekcji, do których warto będzie nawiązać (charakterystyczny przykład, błąd, decyzja,
  porównanie, obraz), z krótką nazwą i dokładnym cytatem. Z nich korzystają kolejne sekcje.

Punkty zaczepienia, do których wolno nawiązać (starsze już wyblakły):
- [lm-8] algorytm rozliczenia w czterech krokach (dział 02): „Podziel sumę przez liczbę osób: to udział jednej osoby.”
- [lm-9] przepis dla kogoś, kto nie gotował (dział 02): „wyobraź sobie przepis dla kogoś, kto nigdy nie gotował”
- [lm-10] mierzalny warunek pieczenia (dział 02): „„Piecz 40 minut” albo „piecz, aż termometr pokaże 95°C w środku” da się zmierzyć.”
- [lm-11] odejmowanie przed policzeniem udziału (dział 02): „Źle:     udział jeszcze nieznany (0 zł) --> Ala: 60 - 0 = +60 zł”
- [lm-12] schemat rozliczenia z rombem (dział 02): „< Wpłaciła więcej niż udział? > --tak--> [ Ma zwrot ] --+”
- [lm-13] drzewo podziału rozliczenia (dział 02): „Rozlicz wyjazd”
- [lm-14] brakujący grosz (dział 02): „Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza.”
- [lm-15] kod jako zwykły plik tekstowy (dział 03): „Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów.”
- [lm-16] literówka zmienia kolor (dział 03): „Literówka w nazwie polecenia często od razu zmienia kolor, zanim cokolwiek uruchomisz.”

Sekcje z tego i poprzedniego działu:
- [sec-02-czym-jest-algorytm] Czym jest algorytm (dział 02): Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
- [sec-02-przepis-jako-algorytm] Przepis jako algorytm (dział 02): Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
- [sec-02-kolejnosc-krokow-algorytmu] Kolejność kroków algorytmu (dział 02): Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.
- [sec-02-czym-jest-schemat-blokowy] Czym jest schemat blokowy (dział 02): Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, dzięki czemu rozgałęzienia, powroty i koniec widać, zanim powstanie kod.
- [sec-02-podzial-problemu-na-czesci] Podział problemu na części (dział 02): Dziel problem na części z jasnym wejściem i wynikiem, aż każdą da się opisać jednym zdaniem i sprawdzić osobno.
- [sec-02-poprawny-algorytm] Poprawny algorytm (dział 02): Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, także w przypadkach brzegowych.
- [sec-03-czym-jest-kod-zrodlowy] Czym jest kod źródłowy (dział 03): Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
- [sec-03-do-czego-sluzy-edytor] Do czego służy edytor (dział 03): Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.

Późniejsze pytania (tylko do pola target, nie do tekstu):
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
- 16. Czym jest kompilator lub interpreter?
- 17. Co to jest błąd w programie?
- 18. Do czego służą komentarze w kodzie?

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
  - Czym jest schemat blokowy: Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, dzięki czemu rozgałęzienia, powroty i koniec widać, zanim powstanie kod.
  - Podział problemu na części: Dziel problem na części z jasnym wejściem i wynikiem, aż każdą da się opisać jednym zdaniem i sprawdzić osobno.
  - Poprawny algorytm: Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, także w przypadkach brzegowych.
Dział 03. Kod i jego uruchamianie
  - Czym jest kod źródłowy: Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
  - Do czego służy edytor: Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.

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
- schemat-blokowy: schemat blokowy
- funkcja: funkcja
- specyfikacja-wyniku: specyfikacja wyniku
- przypadek-brzegowy: przypadek brzegowy
- kod-zrodlowy: kod źródłowy
- edytor-kodu: edytor kodu
- podswietlanie-skladni: podświetlanie składni
- python: Python

POPRZEDNIA SEKCJA (dla ciągłości, nie powtarzaj jej):
## Do czego służy edytor
[[edytor-kodu|Edytor kodu]] to program do pisania i poprawiania [[kod-zrodlowy|kodu źródłowego]], który pomaga czytać kod i zauważać w nim pomyłki. Sam kodu nie uruchamia i nie zmienia jego działania: zmienia tylko to, jak wygodnie się go pisze.

Skoro kod jest zwykłym plikiem tekstowym, można go napisać nawet w Notatniku. Edytor kodu dodaje jednak rzeczy, które przy programowaniu bardzo oszczędzają czas:

| Możliwość | Co daje |
|---|---|
| [[podswietlanie-skladni|podświetlanie składni]] | słowa języka, teksty i liczby mają różne kolory, więc struktura kodu jest widoczna |
| numery linii | komunikat „błąd w linii 3” da się od razu znaleźć |
| wcięcia i nawiasy | edytor wcina linie i domyka cudzysłowy oraz nawiasy |
| podpowiedzi | po wpisaniu kilku liter proponuje dokończenie nazwy |
| zapis w zwykłym tekście | plik da się otworzyć w dowolnym innym programie |

Podświetlanie składni to kolorowanie fragmentów kodu według ich roli. Literówka w nazwie polecenia często od razu zmienia kolor, zanim cokolwiek uruchomisz.

Przykładem będzie VS Code, ale wybór edytora jest sprawą gustu. Zasady pisania kodu są w każdym takie same.

U siebie sprawdzisz teraz, czy działa [[python|Python]] (jeden z języków programowania, którego użyjemy w tym kursie), i zapiszesz pierwszy plik. Uruchomimy go w następnej części, gdy wyjaśnimy, co to znaczy uruchomić program.
````

## Odpowiedź

````json
{
  "title": "Co znaczy uruchomić program",
  "body": "Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam [[kod-zrodlowy|kod źródłowy]] leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś go nie zacznie realizować.\n\nPlik z kodem jest [[uruchamianie-programu|uruchamiany]] przez inny program, który go czyta i wykonuje linia po linii. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.\n\nPolecenie wpisujemy w [[terminal|terminalu]], czyli oknie, w którym komputer przyjmuje polecenia pisane tekstem i pokazuje odpowiedzi tekstem. Przykład to nasz plik `rozlicz.py`:\n\n```python\n# rozlicz.py\nprint(\"Wspólna Kasa\")\nprint(300 / 3)\n```\n\nW terminalu wpisujemy `python rozlicz.py`, a program wypisuje:\n\n```text\nWspólna Kasa\n100.0\n```\n\nKolejność wyjścia jest taka sama jak kolejność linii, bo instrukcje wykonują się jedna po drugiej. Wynik `100.0` to 300 zł podzielone na trzy osoby.\n\nUruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. Tak wygląda cała praca programisty: zapisz, uruchom, przeczytaj wynik.",
  "answer": "Uruchomić program znaczy polecić komputerowi, żeby wykonał instrukcje zapisane w pliku z kodem, jedna po drugiej. Plik sam niczego nie robi, dopiero inny program (w Pythonie: sam Python) go czyta i wykonuje. Uruchomienie nie zmienia pliku, więc można je powtarzać po każdej poprawce.",
  "takeaway": "Uruchomienie programu to wykonanie instrukcji z pliku przez inny program, w kolejności zapisu, bez zmieniania samego pliku.",
  "new_terms": [
    {
      "id": "uruchamianie-programu",
      "term": "uruchamianie programu",
      "definition": "Polecenie komputerowi, by zaczął wykonywać instrukcje z pliku z kodem, od pierwszej do ostatniej."
    },
    {
      "id": "terminal",
      "term": "terminal",
      "definition": "Okno, w którym komputerowi wpisuje się polecenia tekstem i odczytuje jego odpowiedzi tekstem."
    }
  ],
  "references": [
    {
      "direction": "wstecz",
      "phrase": "Sam kod źródłowy",
      "about": "kod jako zwykły plik tekstowy",
      "target": "lm-15"
    },
    {
      "direction": "w przód",
      "phrase": "wyjaśnimy w następnej części",
      "about": "interpreter i kompilator",
      "target": "16"
    }
  ],
  "landmarks": [
    {
      "label": "przepis w szufladzie",
      "quote": "Sam kod źródłowy leży wtedy jak przepis w szufladzie: nic się nie dzieje"
    },
    {
      "label": "zapisz, uruchom, przeczytaj",
      "quote": "zapisz, uruchom, przeczytaj wynik"
    }
  ],
  "versions": [
    {
      "name": "Python",
      "version": "3.13",
      "why": "Komunikat błędu w warsztacie (wskazanie miejsca i podpowiedź „Did you mean”) pochodzi z tej wersji."
    }
  ],
  "workshop": [
    {
      "kind": "polecenie",
      "command": "python --version",
      "lang": "bash",
      "output": "Python 3.13.5",
      "note": "Sprawdzamy, że Python jest dostępny"
    },
    {
      "kind": "polecenie",
      "command": "python kasa.py",
      "lang": "bash",
      "output": "Wspólna Kasa",
      "note": "Uruchamiamy pierwszy skrypt"
    },
    {
      "kind": "plik",
      "path": "kasa.py",
      "lang": "python",
      "content": "# kasa.py - pierwszy skrypt Wspólnej Kasy\nprnt(\"Wspólna Kasa\")\n",
      "note": "Celowo psujemy nazwę print"
    },
    {
      "kind": "polecenie",
      "command": "python kasa.py",
      "lang": "bash",
      "fails": true,
      "output": "Traceback (most recent call last):\n  File \"/home/ola/wspolna_kasa/kasa.py\", line 2, in <module>\n    prnt(\"Wspólna Kasa\")\n    ^^^^\nNameError: name 'prnt' is not defined. Did you mean: 'print'?",
      "note": "Python zatrzymuje się na błędnej linii"
    },
    {
      "kind": "plik",
      "path": "kasa.py",
      "lang": "python",
      "content": "# kasa.py - pierwszy skrypt Wspólnej Kasy\nprint(\"Wspólna Kasa\")\n",
      "note": "Przywracamy poprawną nazwę"
    },
    {
      "kind": "polecenie",
      "command": "python kasa.py",
      "lang": "bash",
      "output": "Wspólna Kasa",
      "note": "Skrypt znów działa"
    }
  ]
}
````
