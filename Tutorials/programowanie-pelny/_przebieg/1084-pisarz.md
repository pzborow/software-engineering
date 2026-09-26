# Krok 1084 · pisarz

Węzeł: `write` · dział: 10 · pytanie: 56 · próba: 1

## Prompt

````text
Jesteś autorem tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Piszesz jedną sekcję działu 10: "Programowanie w praktyce".
PYTANIE 56: Jakie są przykłady programów używanych na co dzień?

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
W tym dziale wątek rozwija się tak: Oceniamy gotowe narzędzie i pomysły na rozwój: wersja webowa lub mobilna, eksport podsumowania, automatyczne wysyłanie e-mailem, oraz plan dalszej nauki i automatyzacji własnych zadań czytelnika.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
rozlicz.py · plik programu (skrypt główny) · rozlicz.py
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)

wydatki · zmienna (lista słowników) · wspolna_kasa/rozlicz.py
wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.50}]

osoby · zmienna (lista tekstów) · wspolna_kasa/rozlicz.py
osoby = ["Ania", "Bartek", "Celina"]

suma_wydatkow · funkcja · funkcje.py
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

udzial_na_osobe · funkcja · funkcje.py
def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

zapytaj_o_wydatek · funkcja · wspolna_kasa/rozlicz.py
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    kwota = float(kwota)
    ...

sprawdz_kwote · funkcja · wspolna_kasa/rozlicz.py
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

wypisz_podsumowanie · funkcja · wspolna_kasa/rozlicz.py
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

test_rozlicz.py · plik testów · test_rozlicz.py
assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0

wspolna_kasa · repozytorium Git · wspolna_kasa
git init -b main

imie · zmienna (tekst) · wspolna_kasa/rozlicz.py
for imie in osoby:

kwota · zmienna (liczba) · wspolna_kasa/rozlicz.py
kwota = 45.5

zaplacono · zmienna (prawda/fałsz) · wspolna_kasa/rozlicz.py
zaplacono = True

kwota_stara · zmienna (liczba) · wspolna_kasa/rozlicz.py
kwota_stara = kwota

liczba_osob · zmienna (liczba) · wspolna_kasa/rozlicz.py
liczba_osob = 3

wydatek · zmienna (słownik) · wspolna_kasa/rozlicz.py
for wydatek in wydatki:

suma · zmienna (liczba) · funkcje.py
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

na_osobe · funkcja · funkcje.py
def na_osobe(suma, osoby):
    return suma / osoby

wypisz_na_osobe · funkcja · funkcje.py
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wydatki.txt · plik danych · wydatki.txt
Ania;120.5
Bartek;45.5
```
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), saldo_osoby (funkcja), wczytaj_wydatki (funkcja)

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
W tym dziale: Czytelnik dopisuje do Wspólnej Kasy jedną własną drobną funkcję, np. wypisanie, kto komu ile jest winien, i zapisuje ją jako kolejny commit, widząc w praktyce automatyzację prostego zadania.

Stan u czytelnika przed tą sekcją (wiążący, dokładna treść plików):
```text
--- blad_pusta.py ---
# blad_pusta.py - Traceback: dzielenie przez zero
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))

--- debug.py ---
# debug.py - szukanie przyczyny złego wyniku przez print
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
liczba_osob = 3
print("Mazury na osobę:", na_osobe(suma(mazury), liczba_osob))

--- funkcje.py ---
# funkcje.py - funkcje Wspólnej Kasy
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print("Mazury:", na_osobe(suma(mazury), 3))
print("Tatry:", na_osobe(suma(tatry), 4))

--- interfejs.py ---
# interfejs.py - Wspólna Kasa pokazuje czytelne podsumowanie
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)

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
kwoty_wydatkow = [45.5, 20, 12.5]
suma = 0
for kwota in kwoty_wydatkow:
    print(kwota)
    suma = suma + kwota
print(suma)
print(kwoty_wydatkow[0])
print(kwoty_wydatkow[-1])
print("Koniec")

--- nieskonczona.py ---
# nieskonczona.py - pętla, która nigdy się nie kończy
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)

--- plik.py ---
# plik.py - Wspólna Kasa zapisuje wydatki do pliku i wczytuje je z powrotem
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")

--- pytaj.py ---
# pytaj.py - Wspólna Kasa pyta o wydatek i sprawdza kwotę
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

kto = input("Kto zapłacił? ")
tekst = input("Ile zapłacił? ")
while not sprawdz_kwote(tekst):
    print("To nie jest poprawna kwota. Wpisz liczbę większą od zera, np. 45.5")
    tekst = input("Ile zapłacił? ")
kwota = float(tekst)
print(f"Zapisano: {kto}, {kwota} zł")

--- test_kasa.py ---
# test_kasa.py - testy funkcji Wspólnej Kasy
from funkcje import suma, na_osobe

assert suma([45.5, 20, 12.5]) == 78.0
assert suma([]) == 0
assert na_osobe(78.0, 3) == 26.0
assert na_osobe(0, 4) == 0
print("Wszystkie testy przeszły")
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
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Za chwilę dopiszesz `na_osobe` i użyjesz obu” (zapowiedź ćwiczenia praktycznego z funkcją na_osobe)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” (własny plik funkcje.py, w którym czytelnik zobaczy błąd)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „Usuwamy ją w warsztacie poniżej.” (zapowiedź poprawienia błędnej ostatniej linii w warsztacie)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „przykładzie, który będzie nam towarzyszył” (program „Wspólna Kasa” wracający w kolejnych sekcjach)
- otwarta obietnica (spełnij, jeśli ta sekcja jest naturalnym miejscem): „pokażemy w ćwiczeniu praktycznym” (praktyczne użycie Git na własnym komputerze)
- Pole landmarks: 1-3 miejsca TEJ sekcji, do których warto będzie nawiązać (charakterystyczny przykład, błąd, decyzja,
  porównanie, obraz), z krótką nazwą i dokładnym cytatem. Z nich korzystają kolejne sekcje.

Punkty zaczepienia, do których wolno nawiązać (starsze już wyblakły):
- [lm-60] zły dzielnik: 39.0 zamiast 26.0 (dział 09): „Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.”
- [lm-61] start nie wypisany (dział 09): „Słowo „start” się nie pojawiło, a komunikat wskazuje linię i miejsce.”
- [lm-62] czytaj od dołu (dział 09): „Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak”
- [lm-63] start się wypisał (dział 09): „tu „Start” się wypisał, bo program ruszył i padł dopiero w środku”
- [lm-64] cisza po assert (dział 09): „Cisza po `assert` znaczy „zgadza się”.”
- [lm-65] print pokazuje złą liczbę osób (dział 09): „Suma się zgadza, a liczba osób nie: mają być trzy.”
- [lm-66] cofnięcie do wczorajszego commita (dział 09): „wracasz do wczorajszego commita zamiast szukać własnych zmian”
- [lm-67] kopiuj ostatnią linię bez ścieżek (dział 09): „Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych”

Sekcje z tego i poprzedniego działu:
- [sec-09-blad-skladni-a-blad-logiczny] Błąd składni a błąd logiczny (dział 09): Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.
- [sec-09-jak-czytac-komunikat-o-bledzie] Jak czytać komunikat o błędzie (dział 09): Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.
- [sec-09-czym-jest-testowanie-programu] Czym jest testowanie programu (dział 09): Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.
- [sec-09-czym-jest-debugowanie] Czym jest debugowanie (dział 09): Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.
- [sec-09-po-co-zapisywac-wersje-kodu] Po co zapisywać wersje kodu (dział 09): Commit zapisuje działającą wersję kodu z opisem, dzięki czemu zawsze możesz do niej wrócić i sprawdzić, kiedy coś się zepsuło.
- [sec-09-szukanie-rozwiazan-w-internecie] Szukanie rozwiązań w internecie (dział 09): Szukaj po ostatniej linii komunikatu i nazwie języka, oceniaj źródła i nigdy nie wklejaj skopiowanego kodu bez zrozumienia.

Późniejsze pytania (tylko do pola target, nie do tekstu):
- 57. Czym różni się strona internetowa od aplikacji mobilnej?
- 58. Jak od pomysłu dojść do działającego programu?
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
- 60. Od czego zacząć samodzielną naukę programowania?
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

Pole answer: samodzielna odpowiedź na pytanie w 2-5 zdaniach, bez kodu (trafi pod pytanie w rozwijanym bloku).
Pole takeaway: jedno zdanie do listy "Co zapamiętać".

Pozostałe pytania tego działu (odpowiesz na nie w kolejnych sekcjach, nie teraz):
- 57. Czym różni się strona internetowa od aplikacji mobilnej?
- 58. Jak od pomysłu dojść do działającego programu?
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
- 60. Od czego zacząć samodzielną naukę programowania?
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

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
Dział 06. Powtarzanie i kolekcje
  - Czym jest pętla: Pętla powtarza wcięty fragment kodu, a `for` robi to raz dla każdego elementu zestawu danych, po czym kończy pracę.
  - Kiedy sięgnąć po pętlę: Gdy kopiujesz linię i zmieniasz w niej tylko jedną wartość, użyj pętli: jeden zapis obsłuży dowolną liczbę elementów.
  - Pętla nieskończona: Pętla nieskończona nigdy nie osiąga warunku zakończenia, więc program się „zawiesza”; zatrzymasz go Ctrl+C, a przy każdym `while` pytaj, co w końcu zmieni warunek na fałsz.
  - Czym jest lista danych: Lista to jedna zmienna z wieloma wartościami w ustalonej kolejności, zapisana w nawiasach kwadratowych, z elementami rozdzielonymi przecinkami.
  - Odczyt elementu listy: Element listy pobierasz indeksem w nawiasach kwadratowych, licząc od zera, a `-1` oznacza ostatni element.
  - Pętla po elementach listy: Pętla `for element in lista:` wykonuje blok raz dla każdego elementu, w kolejności listy, i sama kończy pracę po ostatnim.
Dział 07. Funkcje i porządek w kodzie
  - Czym jest funkcja: Funkcję definiujesz raz przez def, a uruchamiasz każdym wywołaniem jej nazwy z nawiasami.
  - Po co dzielić program na funkcje: Funkcje dają kodowi nazwy i jedno miejsce na każdą logikę, więc program jest czytelniejszy, a poprawki robisz raz.
  - Czym są argumenty funkcji: Argumenty to wartości podane przy wywołaniu, które trafiają do parametrów funkcji według kolejności lub nazwy, a ich liczba musi pasować do definicji.
  - Zwracanie wyniku przez funkcję: Return oddaje wartość wywołującemu, po czym kończy funkcję, a print tylko pokazuje tekst i niczego nie zwraca (funkcja bez return daje None).
  - Czytelne nazwy zmiennych i funkcji: Nazywaj funkcję według tego, co robi, a zmienną według tego, co trzyma, bo kod czyta się częściej, niż pisze.
  - Ponowne użycie kodu: Funkcję piszesz raz, a wywołujesz z różnymi danymi, więc poprawka w jednym miejscu naprawia wszystkie użycia.
Dział 08. Współpraca programu z użytkownikiem
  - Dane wejściowe programu: Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.
  - Dane wyjściowe programu: Dane wyjściowe to wynik, który program oddaje na zewnątrz (ekran, plik, inny program), a dobre wyjście jest opisane tak, by zrozumiał je człowiek.
  - Pytanie użytkownika o informację: Funkcja input wypisuje pytanie i zwraca odpowiedź użytkownika zawsze jako tekst, więc liczbę trzeba zamienić przez float().
  - Czym jest plik: Plik przechowuje dane na dysku po zakończeniu programu, a program otwiera go przez open (najlepiej z with) w trybie czytania, zapisu lub dopisywania i pamięta, że dostaje z niego tekst.
  - Czym jest interfejs użytkownika: Interfejs użytkownika to wszystko, przez co człowiek rozmawia z programem: pytania, które program zadaje, i wyniki, które pokazuje, więc powinny być jasne dla kogoś, kto nie zna kodu.
  - Po co sprawdzać dane użytkownika: Sprawdzaj dane od użytkownika zaraz po wpisaniu, bo człowiek może wpisać coś nieoczekiwanego, a zły wpis powinien dostać komunikat i drugą szansę.
Dział 09. Błędy i dobre praktyki
  - Błąd składni a błąd logiczny: Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.
  - Jak czytać komunikat o błędzie: Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.
  - Czym jest testowanie programu: Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.
  - Czym jest debugowanie: Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.
  - Po co zapisywać wersje kodu: Commit zapisuje działającą wersję kodu z opisem, dzięki czemu zawsze możesz do niej wrócić i sprawdzić, kiedy coś się zepsuło.
  - Szukanie rozwiązań w internecie: Szukaj po ostatniej linii komunikatu i nazwie języka, oceniaj źródła i nigdy nie wklejaj skopiowanego kodu bez zrozumienia.

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
- petla: pętla
- iteracja: iteracja
- petla-nieskonczona: pętla nieskończona
- lista-danych: lista danych
- element-listy: element listy
- indeks: indeks
- definicja-funkcji: definicja funkcji
- wywolanie-funkcji: wywołanie funkcji
- argument-funkcji: argument funkcji
- parametr: parametr
- typeerror: TypeError
- none: None
- wartosc-zwracana: wartość zwracana
- dane-wejsciowe: dane wejściowe
- dane-wyjsciowe: dane wyjściowe
- input: input
- plik: plik
- tryb-otwarcia-pliku: tryb otwarcia pliku
- interfejs-uzytkownika: interfejs użytkownika
- interfejs-tekstowy: interfejs tekstowy
- walidacja-danych: walidacja danych
- blad-skladni: błąd składni
- blad-logiczny: błąd logiczny
- traceback: Traceback
- komunikat-o-bledzie: komunikat o błędzie
- testowanie: testowanie
- assert: assert
- debugowanie: debugowanie
- git: Git
- commit: commit
- repozytorium: repozytorium

POPRZEDNIA SEKCJA (dla ciągłości, nie powtarzaj jej):
## Szukanie rozwiązań w internecie
Wpisz w wyszukiwarkę to, co widzisz: ostatnią linię [[komunikat-o-bledzie|komunikatu o błędzie]] i nazwę języka. Prawie każdy błąd ktoś już miał i ktoś już opisał, jak go naprawić.

Ostatnia linia [[traceback|Tracebacku]] to ta, którą, jak w sekcji o czytaniu komunikatów, czytasz od dołu. Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych, bo nikt inny ich nie ma.

```text
python TypeError: unsupported operand type(s) for /: 'str' and 'int'
```

Gdy nie ma komunikatu, a wynik jest zły, opisz problem słowami: co robisz i co się dzieje, np. „python input zwraca tekst zamiast liczby”.

Wyniki oceniaj po kolei:

| Źródło | Jak je traktować |
|---|---|
| dokumentacja Pythona, czyli oficjalny opis języka i jego funkcji (docs.python.org) | najbardziej wiarygodna, ale sucha |
| pytania i odpowiedzi na forach, np. Stack Overflow | szukaj odpowiedzi z dużą liczbą głosów i sprawdź datę |
| poradniki i filmy | dobre na start, ale bywają przestarzałe |

Skopiowanego kodu nie wklejaj w ciemno. Przeczytaj, zrozum, co robi, i uruchom na małym przykładzie. Jeśli po kilku próbach nadal nic, zadaj własne pytanie: wklej pełny komunikat i najmniejszy kod, który błąd wywołuje.

Umiejętność szukania to zwykła część pracy programisty, nie oznaka słabości.
````

## Odpowiedź

````json
{
  "title": "Programy używane na co dzień",
  "body": "Na co dzień używasz dziesiątek programów, choć rzadko o tym myślisz: komunikatora, mapy, banku w telefonie, arkusza kalkulacyjnego, przeglądarki. Każdy z nich to [[program-komputerowy|program]] albo [[aplikacja|aplikacja]], czyli program z oprawą dla użytkownika, i działa według tego samego schematu, który znasz z własnych skryptów.\n\nZawsze są [[dane-wejsciowe|dane wejściowe]], jakieś przetwarzanie i [[dane-wyjsciowe|dane wyjściowe]]:\n\n| Program | Wejście | Co robi | Wyjście |\n|---|---|---|---|\n| Nawigacja | cel podróży, Twoja pozycja | wybiera najkrótszą trasę | trasa na mapie |\n| Bank w telefonie | kwota i numer konta | sprawdza saldo, księguje przelew | potwierdzenie |\n| Arkusz kalkulacyjny | liczby w komórkach | liczy wzory | sumy i wykresy |\n| Wyszukiwarka | wpisane słowa | szuka i układa wyniki | lista stron |\n| Alarm w telefonie | ustawiona godzina | porównuje ją z zegarem | dzwonek |\n\nPod spodem są te same klocki, które już budowałeś: zmienne, decyzje (`if`), pętle po listach, funkcje i pliki. Nawigacja też przegląda listę dróg i wybiera jedną, a bank też sprawdza dane od użytkownika, zanim cokolwiek zaksięguje.\n\nRóżni je skala i [[interfejs-uzytkownika|interfejs]]: przyciski i mapy zamiast pytań w terminalu. Twoja „Wspólna Kasa” należy do tej samej rodziny: bierze wydatki, liczy i wypisuje, kto ile zapłacił. Jest po prostu mała. Czym różni się strona internetowa od aplikacji mobilnej, wyjaśnimy w następnej sekcji.\n\nKonsekwencja: skoro gotowe programy to złożone proste kroki, da się je zrozumieć, a proste zadania z Twojej pracy da się zautomatyzować własnym małym programem.",
  "answer": "Do programów na co dzień należą nawigacja, aplikacja bankowa, arkusz kalkulacyjny, wyszukiwarka czy alarm w telefonie. Każdy bierze dane wejściowe, przetwarza je (decyzje, pętle, funkcje) i oddaje wynik. Różnią się skalą i wyglądem, a nie zasadą działania, dlatego „Wspólna Kasa” jest ich małym krewnym.",
  "takeaway": "Programy z codziennego życia, od nawigacji po bank, działają jak Twoja Wspólna Kasa: biorą dane, przetwarzają je prostymi krokami i pokazują wynik.",
  "references": [
    {
      "direction": "w przód",
      "phrase": "Czym różni się strona internetowa od aplikacji mobilnej",
      "about": "różnica między stroną a aplikacją mobilną",
      "target": "57"
    }
  ],
  "landmarks": [
    {
      "label": "wspólna rodzina programów",
      "quote": "Twoja „Wspólna Kasa” należy do tej samej rodziny: bierze wydatki, liczy i wypisuje"
    }
  ]
}
````
