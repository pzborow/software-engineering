# Krok 0580 · pisarz

Węzeł: `write` · dział: 6 · pytanie: 32 · próba: 1

## Prompt

````text
Jesteś autorem tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Piszesz jedną sekcję działu 06: "Powtarzanie i kolekcje".
PYTANIE 32: Czym jest pętla?

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
W tym dziale wątek rozwija się tak: Pojedyncze zmienne zastępuje lista wydatków i lista osób; pętla for sumuje kwoty i liczy saldo każdego uczestnika, a pętla nieskończona pojawia się jako ostrzeżenie.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
rozlicz.py · plik programu (skrypt główny) · rozlicz.py
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)

osoby · zmienna (lista tekstów) · wspolna_kasa/rozlicz.py
osoby = ["Ania", "Bartek", "Celina"]

imie · zmienna (tekst) · wspolna_kasa/rozlicz.py
imie = "Ania"

kwota · zmienna (liczba) · wspolna_kasa/rozlicz.py
kwota = 45.5

zaplacono · zmienna (prawda/fałsz) · wspolna_kasa/rozlicz.py
zaplacono = True

kwota_stara · zmienna (liczba) · wspolna_kasa/rozlicz.py
kwota_stara = kwota

liczba_osob · zmienna (liczba) · wspolna_kasa/rozlicz.py
liczba_osob = 3
```
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), wydatki (zmienna (lista słowników)), suma_wydatkow (funkcja), udzial_na_osobe (funkcja), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), zapytaj_o_wydatek (funkcja), sprawdz_kwote (funkcja), wypisz_podsumowanie (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

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
W tym dziale: Wydatki trafiają do listy, a pętla for wypisuje je wszystkie, sumuje i wybiera pierwszy oraz ostatni element; czytelnik widzi też, jak wygląda while bez warunku zakończenia i zatrzymuje go Ctrl+C.

Stan u czytelnika przed tą sekcją (wiążący, dokładna treść plików):
```text
--- kasa.py ---
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
nazwa_wyjazdu = "Mazury"
kwota_wydatku = 45.5
czy_oplacone = True
print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
print(type(nazwa_wyjazdu))
print(type(kwota_wydatku))
print(type(czy_oplacone))
czy_oplacone = False
print(czy_oplacone)
liczba_osob = 3
koszt_na_osobe = kwota_wydatku / liczba_osob
print(koszt_na_osobe)
print(kwota_wydatku % liczba_osob)
print("Kwota: " + str(kwota_wydatku) + " zł")
print(f"Wyjazd: {nazwa_wyjazdu}, kwota: {kwota_wydatku} zł")
print(kwota_wydatku > 100)
print(kwota_wydatku >= 45.5)
print(liczba_osob != 3)
print(nazwa_wyjazdu == "mazury")
if kwota_wydatku > 40:
    print("Kwota do sprawdzenia")
if kwota_wydatku > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print(kwota_wydatku > 40 and liczba_osob > 5)
print(kwota_wydatku > 100 or liczba_osob == 3)
if kwota_wydatku > 100 or liczba_osob > 5:
    print("Duża kwota")
else:
    print("Zwykła kwota")
print("Koniec")
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
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykład, który będzie nam towarzyszył” (Wspólna Kasa wraca w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „dostanie z niego kod dopiero później” (kod Wspólnej Kasy pojawi się w dalszych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykład, który będzie nam towarzyszył w kolejnych działach” (Wspólna Kasa wraca w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „nasz przykład, który będzie nam towarzyszył” (Wspólna Kasa jako przykład wracający w kolejnych działach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „w warsztacie poniżej dopisujesz do swojego skryptu linię” (zapowiedź warsztatu i skryptu, w którym czytelnik wywoła błąd TypeError)
- Pole landmarks: 1-3 miejsca TEJ sekcji, do których warto będzie nawiązać (charakterystyczny przykład, błąd, decyzja,
  porównanie, obraz), z krótką nazwą i dokładnym cytatem. Z nich korzystają kolejne sekcje.

Punkty zaczepienia, do których wolno nawiązać (starsze już wyblakły):
- [lm-33] nieścisłość ułamka (dział 05): „Końcówka `...336` to drobna nieścisłość: komputer trzyma ułamki w przybliżeniu.”
- [lm-34] zlepione słowa (dział 05): „W drugiej linii zabrakło spacji, więc słowa się zlepiły.”
- [lm-35] tekst nie równa się liczbie (dział 05): „Tekst `"45.5"` i liczba 45.5 to różne typy, więc też nie są równe”
- [lm-36] wcięcie i ostatni print (dział 05): „Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.”
- [lm-37] dwie drogi if/else (dział 05): „Warunek `kwota > 100` jest fałszywy, więc Python pominął pierwszy wcięty blok i wykonał ten pod `else`.”
- [lm-38] kwota duża lub dzielona przez wielu (dział 05): „kwotę można uznać za dużą, gdy jest wysoka **lub** dzieli ją dużo osób”

Sekcje z tego i poprzedniego działu:
- [sec-05-dzialania-matematyczne-w-programie] Działania matematyczne w programie (dział 05): Python zna siedem podstawowych operatorów arytmetycznych (`+ - * / // % **`); na tekście dzielić się nie da, a `+` i `*` znaczą tam sklejanie i powtarzanie.
- [sec-05-laczenie-tekstow] Łączenie tekstów (dział 05): Plus skleja tylko tekst z tekstem, bez dodawania spacji, a liczbę trzeba przed sklejeniem zamienić funkcją str() albo użyć zapisu z f.
- [sec-05-porownywanie-wartosci] Porównywanie wartości (dział 05): Operatory porównania (`==`, `!=`, `<`, `>`, `<=`, `>=`) dają `True` albo `False`, a `==` pyta o równość, w przeciwieństwie do `=`, które przypisuje.
- [sec-05-instrukcja-warunkowa-jesli-to] Instrukcja warunkowa „jeśli… to…” (dział 05): Instrukcja `if` wykonuje wcięte pod nią linie tylko wtedy, gdy warunek daje `True`; w przeciwnym razie Python je pomija.
- [sec-05-czesc-w-przeciwnym-razie] Część „w przeciwnym razie” (dział 05): `else` to droga „w przeciwnym razie”: wykonuje się tylko wtedy, gdy warunek z `if` jest fałszywy, więc program zawsze wybiera dokładnie jedną z dwóch dróg.
- [sec-05-operatory-i-oraz-lub] Operatory „i” oraz „lub” (dział 05): `and` wymaga prawdziwości obu warunków, a `or` wystarczy jeden prawdziwy, żeby całość dała `True`.

Późniejsze pytania (tylko do pola target, nie do tekstu):
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
- 33. Kiedy warto użyć pętli zamiast pisać to samo wiele razy?
- 34. Czym jest pętla nieskończona i dlaczego jest problemem?
- 35. Czym jest lista danych?
- 36. Jak odczytać konkretny element listy?
- 37. Jak przejść przez wszystkie elementy listy?

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
  - Co znaczy uruchomić program: Uruchomienie programu to polecenie, by Python wykonał instrukcje z pliku po kolei, a sam plik pozostaje bez zmian.
  - Kompilator i interpreter: Kompilator tłumaczy cały kod na osobny plik przed startem, a interpreter wykonuje kod na bieżąco, dlatego w Pythonie wystarczy zapisać i uruchomić.
  - Co to jest błąd w programie: Błąd to rozbieżność między zamiarem a działaniem programu: czasem zatrzymuje go komunikat, a czasem zły wynik pojawia się po cichu.
  - Do czego służą komentarze: Komentarz zaczyna się od `#`, jest pomijany przez Pythona i ma wyjaśniać powód, a nie powtarzać kod; po zmianie kodu trzeba go zaktualizować.
Dział 04. Dane i zmienne
  - Czym jest dana: Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.
  - Czym jest zmienna: Zmienna to nazwa, pod którą program przechowuje daną, żeby móc jej użyć wielokrotnie i w razie potrzeby zmienić.
  - Zmienna jako pudełko z etykietą: Zmienna to pudełko z etykietą: nazwa zostaje, w środku jest jedna wartość, którą można podmienić, a kopie są niezależne.
  - Liczba a tekst: Cudzysłów zmienia rodzaj danych: 45.5 to liczba, którą można dzielić, a "45.5" to tekst, którego dzielić się nie da.
  - Czym jest typ danych: Typ danych to rodzaj wartości (str, int, float, bool), który decyduje o tym, jakie działania są na niej możliwe.
  - Wartość logiczna prawda/fałsz: Wartość logiczna (`bool`) to `True` albo `False`, zapisywane z wielkiej litery i bez cudzysłowu, a program używa jej do podejmowania decyzji.
  - Przypisanie wartości do zmiennej: Przypisanie `=` to polecenie zapisania wartości z prawej strony pod nazwą z lewej, a o wartości zmiennej decyduje ostatnie wykonane przypisanie.
Dział 05. Operacje i decyzje
  - Działania matematyczne w programie: Python zna siedem podstawowych operatorów arytmetycznych (`+ - * / // % **`); na tekście dzielić się nie da, a `+` i `*` znaczą tam sklejanie i powtarzanie.
  - Łączenie tekstów: Plus skleja tylko tekst z tekstem, bez dodawania spacji, a liczbę trzeba przed sklejeniem zamienić funkcją str() albo użyć zapisu z f.
  - Porównywanie wartości: Operatory porównania (`==`, `!=`, `<`, `>`, `<=`, `>=`) dają `True` albo `False`, a `==` pyta o równość, w przeciwieństwie do `=`, które przypisuje.
  - Instrukcja warunkowa „jeśli… to…”: Instrukcja `if` wykonuje wcięte pod nią linie tylko wtedy, gdy warunek daje `True`; w przeciwnym razie Python je pomija.
  - Część „w przeciwnym razie”: `else` to droga „w przeciwnym razie”: wykonuje się tylko wtedy, gdy warunek z `if` jest fałszywy, więc program zawsze wybiera dokładnie jedną z dwóch dróg.
  - Operatory „i” oraz „lub”: `and` wymaga prawdziwości obu warunków, a `or` wystarczy jeden prawdziwy, żeby całość dała `True`.

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
- wartosc-logiczna: wartość logiczna
- przypisanie: przypisanie
- operator-arytmetyczny: operator arytmetyczny
- konkatenacja: konkatenacja
- operator-porownania: operator porównania
- instrukcja-warunkowa: instrukcja warunkowa
- wciecie: wcięcie
- operator-logiczny: operator logiczny

POPRZEDNIA SEKCJA (dla ciągłości, nie powtarzaj jej):
## Operatory „i” oraz „lub”
[[operator-logiczny|Operatory logiczne]] `and` („i”) oraz `or` („lub”) łączą kilka warunków w jeden. Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: `True` albo `False`.

`and` daje `True` tylko wtedy, gdy prawdziwe są **oba** warunki. `or` daje `True`, gdy prawdziwy jest **którykolwiek** z nich, a `False` dopiero wtedy, gdy oba są fałszywe.

| Lewy warunek | Prawy warunek | `and` | `or` |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

Każdy z połączonych warunków zapisujemy w całości, tak jak w porównywaniu wartości. Wynik można wypisać albo wstawić do `if`:

```python
kwota = 45.5
liczba_osob = 3
print(kwota > 40 and liczba_osob > 5)
print(kwota > 100 or liczba_osob == 3)
if kwota > 100 or liczba_osob > 5:
    print("Duża kwota")
else:
    print("Zwykła kwota")
```

```text
False
True
Zwykła kwota
```

W pierwszej linii drugi warunek zawiódł, więc `and` dało `False`. W drugiej wystarczył prawdziwy drugi warunek, więc `or` dało `True`. W `if` oba są fałszywe, więc zadziałało `else`.

Dla „Wspólnej Kasy” to znaczy, że kwotę można uznać za dużą, gdy jest wysoka **lub** dzieli ją dużo osób. U siebie w `kasa.py` dopisz te linie w warsztacie poniżej.
````

## Odpowiedź

````json
{
  "title": "Czym jest pętla",
  "body": "[[petla|Pętla]] to instrukcja, która każe programowi wykonać ten sam fragment kodu wielokrotnie. Zamiast pisać tę samą linię trzy razy, zapisujesz ją raz i mówisz, ile razy albo dla czego ją powtórzyć.\n\nJedno powtórzenie fragmentu nazywamy [[iteracja|iteracją]]. Pętla `for` wykonuje po jednej iteracji dla każdego elementu z zestawu danych. Taki zestaw to na razie po prostu lista wartości w nawiasach kwadratowych; jej zapis omówimy osobno.\n\nWcięte linie pod `for` to ciało pętli, tak samo jak przy `if`. Nazwa po słowie `for` to zmienna, która w każdej iteracji dostaje kolejny element:\n\n```python\nosoby = [\"Ania\", \"Bartek\", \"Celina\"]\nfor imie in osoby:\n    print(\"Cześć,\", imie)\nprint(\"Koniec\")\n```\n\n```text\nCześć, Ania\nCześć, Bartek\nCześć, Celina\nKoniec\n```\n\nCiało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. Ostatni `print` nie ma wcięcia, więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.\n\nPętla ma więc początek, powtarzane kroki i koniec, a koniec wynika z [[warunek-zakonczenia|warunku zakończenia]]: w `for` jest nim wyczerpanie elementów. W „Wspólnej Kasie” dzięki temu jeden zapis obsłuży trzy osoby, ale też trzydzieści.",
  "answer": "Pętla to instrukcja, która powtarza ten sam fragment kodu wiele razy. Jedno wykonanie nazywamy iteracją. Pętla `for` powtarza wcięte ciało dla każdego elementu zestawu danych i kończy się, gdy elementy się skończą.",
  "takeaway": "Pętla powtarza wcięty fragment kodu, a `for` robi to raz dla każdego elementu zestawu danych, po czym kończy pracę.",
  "new_terms": [
    {
      "id": "petla",
      "term": "pętla",
      "definition": "Instrukcja, która wykonuje ten sam fragment kodu wielokrotnie, aż zostanie spełniony warunek zakończenia."
    },
    {
      "id": "iteracja",
      "term": "iteracja",
      "definition": "Jedno wykonanie ciała pętli."
    }
  ],
  "references": [
    {
      "direction": "wstecz",
      "phrase": "tak samo jak przy `if`",
      "about": "wcięcie jako oznaczenie ciała bloku",
      "target": "sec-05-instrukcja-warunkowa-jesli-to"
    },
    {
      "direction": "wstecz",
      "phrase": "Ostatni `print` nie ma wcięcia",
      "about": "wcięcie decyduje o przynależności do bloku",
      "target": "lm-36"
    },
    {
      "direction": "w przód",
      "phrase": "jej zapis omówimy osobno",
      "about": "lista danych",
      "target": "35"
    }
  ],
  "landmarks": [
    {
      "label": "pętla po osobach",
      "quote": "Ciało wykonało się trzy razy, bo na liście są trzy osoby."
    }
  ],
  "canon_changes": [
    {
      "action": "dodaj",
      "module": "przykład",
      "element": {
        "name": "imie",
        "kind": "zmienna (tekst)",
        "signature": "for imie in osoby:",
        "file": "wspolna_kasa/rozlicz.py",
        "note": "Zmienna pętli przyjmująca w każdej iteracji kolejną osobę."
      }
    }
  ],
  "workshop": [
    {
      "kind": "plik",
      "path": "kasa.py",
      "lang": "python",
      "note": "Dopisujemy listę kwot i pętlę, która je wypisuje i sumuje",
      "content": "# kasa.py - pierwszy skrypt Wspólnej Kasy\nprint(\"Wspólna Kasa\")\nnazwa_wyjazdu = \"Mazury\"\nkwota_wydatku = 45.5\nczy_oplacone = True\nprint(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)\nprint(type(nazwa_wyjazdu))\nprint(type(kwota_wydatku))\nprint(type(czy_oplacone))\nczy_oplacone = False\nprint(czy_oplacone)\nliczba_osob = 3\nkoszt_na_osobe = kwota_wydatku / liczba_osob\nprint(koszt_na_osobe)\nprint(kwota_wydatku % liczba_osob)\nprint(\"Kwota: \" + str(kwota_wydatku) + \" zł\")\nprint(f\"Wyjazd: {nazwa_wyjazdu}, kwota: {kwota_wydatku} zł\")\nprint(kwota_wydatku > 100)\nprint(kwota_wydatku >= 45.5)\nprint(liczba_osob != 3)\nprint(nazwa_wyjazdu == \"mazury\")\nif kwota_wydatku > 40:\n    print(\"Kwota do sprawdzenia\")\nif kwota_wydatku > 100:\n    print(\"Bardzo duża kwota\")\nelse:\n    print(\"Zwykła kwota\")\nprint(kwota_wydatku > 40 and liczba_osob > 5)\nprint(kwota_wydatku > 100 or liczba_osob == 3)\nif kwota_wydatku > 100 or liczba_osob > 5:\n    print(\"Duża kwota\")\nelse:\n    print(\"Zwykła kwota\")\nkwoty_wydatkow = [45.5, 20, 12.5]\nsuma = 0\nfor kwota in kwoty_wydatkow:\n    print(kwota)\n    suma = suma + kwota\nprint(suma)\nprint(\"Koniec\")\n"
    },
    {
      "kind": "polecenie",
      "command": "python kasa.py",
      "lang": "bash",
      "note": "Uruchamiamy skrypt i sprawdzamy działanie pętli",
      "output": "Wspólna Kasa\nMazury 45.5 True\n<class 'str'>\n<class 'float'>\n<class 'bool'>\nFalse\n15.166666666666666\n0.5\nKwota: 45.5 zł\nWyjazd: Mazury, kwota: 45.5 zł\nFalse\nTrue\nFalse\nFalse\nKwota do sprawdzenia\nZwykła kwota\nFalse\nTrue\nZwykła kwota\n45.5\n20\n12.5\n78.0\nKoniec"
    }
  ]
}
````
