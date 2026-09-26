# Napisz i uruchom kod

Do tej pory układałeś algorytmy na papierze i w głowie, a teraz zapiszesz pierwszy prawdziwy kod i sprawdzisz, że komputer go wykona. Po tym dziale będziesz wiedzieć, czym jest [kod źródłowy](00%20Glosariusz.md#kod-źródłowy), do czego służy edytor, jak uruchomić program i co robi [interpreter](00%20Glosariusz.md#interpreter). Nauczysz się też rozpoznawać błąd i opisywać kod komentarzami. Zaczniemy plik kasa.py dla „Wspólnej Kasy” i celowo go zepsujemy, żeby zobaczyć pierwszy komunikat o błędzie.

```text
algorytm (dział 02) → kod w pliku → interpreter → wynik lub błąd
```

**W tym dziale:**

- [Poznaj kod źródłowy](#poznaj-kod-źródłowy)
- [Pisz kod w edytorze](#pisz-kod-w-edytorze)
- [Uruchom swój program](#uruchom-swój-program)
- [Odróżnij kompilator od interpretera](#odróżnij-kompilator-od-interpretera)
- [Rozpoznaj błąd w programie](#rozpoznaj-błąd-w-programie)
- [Opisuj kod komentarzami](#opisuj-kod-komentarzami)

**Warsztat, punkt startowy:** Dowolny system (Windows, macOS lub Linux) z terminalem (PowerShell, bash lub zsh), zainstalowany Python 3.13 (sprawdzenie: python --version, na macOS/Linux ewentualnie python3 --version) oraz prosty edytor kodu, np. VS Code lub Notatnik. Pusty katalog roboczy ~/wspolna_kasa, w którym czytelnik otwiera terminal. [Cały warsztat](99%20Warsztat.md).

## Poznaj kod źródłowy

Kod źródłowy to tekst programu zapisany w [języku programowania](00%20Glosariusz.md#język-programowania), który czyta i pisze człowiek. To „źródło”, z którego komputer dopiero dostaje coś do wykonania.

<a id="lm-15"></a>Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to [instrukcja](00%20Glosariusz.md#instrukcja) zapisana według ścisłych reguł [składni](00%20Glosariusz.md#składnia). [Ten sam algorytm, który wcześniej opisywaliśmy słowami i schematem](02%20My%C5%9Bl%20krok%20po%20kroku.md#lm-8), tu dostaje zapis, którego nie da się zrozumieć na dwa sposoby.

Kod źródłowy zapisujemy w pliku o rozszerzeniu zależnym od języka. Pliki [Pythona](00%20Glosariusz.md#python) kończą się na `.py`. <a id="ref-19"></a>Taki plik będzie miał [nasz przykład, który będzie nam towarzyszył](#ref-35): „Wspólna Kasa”. <a id="ref-16"></a><a id="ref-24"></a>Zaczyna się od pliku `rozlicz.py`:

<a id="ref-25"></a>

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

```text
Wspólna Kasa
100.0
```

Plik sam niczego nie robi. Dopiero osobny program czyta go i wykonuje linia po linii, a [jak to działa, pokażemy przy uruchamianiu programu](#ref-38).

Konsekwencja: kod źródłowy możesz otworzyć, przeczytać i poprawić w każdym edytorze tekstu. Dlatego to on jest tym, co programista naprawdę tworzy i zmienia.

> **Z życia wzięte:** Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na ekranie wyglądała identycznie jak poprawna. Edytor dokumentów zamienił proste cudzysłowy na typograficzne, a interpreter tych znaków nie uznaje za cudzysłowy. Od tamtej pory kod źródłowy piszę i przesyłam wyłącznie jako zwykły tekst, w edytorze przeznaczonym do kodu.

## Pisz kod w edytorze

[Edytor kodu](00%20Glosariusz.md#edytor-kodu) to program do pisania i poprawiania kodu źródłowego, który pomaga czytać kod i zauważać w nim pomyłki. Sam kodu nie uruchamia i nie zmienia jego działania: zmienia tylko to, jak wygodnie się go pisze.

[Skoro kod jest zwykłym plikiem tekstowym](#lm-15), można go napisać nawet w Notatniku. Edytor kodu dodaje jednak rzeczy, które przy programowaniu bardzo oszczędzają czas:

| Możliwość | Co daje |
|---|---|
| [podświetlanie składni](00%20Glosariusz.md#podświetlanie-składni) | słowa języka, teksty i liczby mają różne kolory, więc struktura kodu jest widoczna |
| numery linii | komunikat „błąd w linii 3” da się od razu znaleźć |
| wcięcia i nawiasy | edytor wcina linie i domyka cudzysłowy oraz nawiasy |
| podpowiedzi | po wpisaniu kilku liter proponuje dokończenie nazwy |
| zapis w zwykłym tekście | plik da się otworzyć w dowolnym innym programie |

Podświetlanie składni to kolorowanie fragmentów kodu według ich roli. Literówka w nazwie polecenia często od razu zmienia kolor, zanim cokolwiek uruchomisz.

Przykładem będzie VS Code, ale wybór edytora jest sprawą gustu. Zasady pisania kodu są w każdym takie same.

U siebie sprawdzisz teraz, czy działa Python (jeden z języków programowania, którego użyjemy w tym kursie), i zapiszesz pierwszy plik. Uruchomimy go w następnej części, gdy wyjaśnimy, co to znaczy uruchomić program.

> **Warsztat: zrób u siebie**

**Krok 1. Uruchom.** Sprawdzamy, czy Python działa.

```bash
python --version
```

Wynik:

```text
Python 3.13.0
```

**Krok 2. Utwórz plik `kasa.py`.** Zapisujemy w edytorze pierwszy plik z komentarzem i jednym print.

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
```

> **Z przymrużeniem oka:** Komunikat „błąd w linii 3” bez numerów linii to jak list z adresem „mieszkam na ulicy, po lewej”. Edytor kodu daje każdej linii numer, żeby listonosz nie musiał pukać do wszystkich drzwi.

**Ilustracja:** _Edytor nie uruchamia kodu, ale świetnie pokazuje, gdzie coś wygląda podejrzanie._

Tekst alternatywny: Uśmiechnięta osoba przy laptopie, a obok mały pomocnik z kolorowymi zakreślaczami koloruje fragmenty kodu na ekranie i ogląda przez lupę jeden podejrzany fragment zaznaczony na koralowo.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Ciepła scena przy biurku: uśmiechnięta osoba siedzi przed laptopem, na którego ekranie widać kilka linii abstrakcyjnego kodu jako kolorowe paski i kropki, bez czytelnych liter. Obok na krześle siedzi mały, przyjazny pomocnik o okrągłych kształtach i trzyma w rączkach zakreślacze w miętowym, musztardowym i koralowym kolorze. Zakreśla fragmenty na ekranie różnymi kolorami, a jeden podejrzany fragment podświetla koralem i przygląda mu się przez lupę. Osoba z ciekawością pochyla się w stronę ekranu.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/03-pisz-kod-w-edytorze-1.png`

</details>

## Uruchom swój program

<a id="ref-37"></a>Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam kod źródłowy leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś nie zacznie go realizować.

<a id="ref-34"></a>Plik z kodem czyta i wykonuje linia po linii inny program. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.

Polecenie wpisujemy w [terminalu](00%20Glosariusz.md#terminal), czyli oknie, w którym komputer przyjmuje polecenia pisane tekstem i odpowiada tekstem. U siebie masz już plik `kasa.py`:

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
```

W terminalu, w katalogu z plikiem, wpisujemy `python kasa.py`, a program wypisuje:

```text
Wspólna Kasa
```

Linia z `#` to [komentarz](00%20Glosariusz.md#komentarz), który Python pomija, więc wykonuje się tylko `print`. Gdyby linii było więcej, wykonywałyby się jedna po drugiej, w kolejności zapisu.

Uruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. <a id="lm-18"></a>Tak wygląda codzienna praca: zapisz, uruchom, przeczytaj wynik.

> **Warsztat: zrób u siebie**

**Krok 1. Uruchom.** Uruchamiamy pierwszy skrypt.

```bash
python kasa.py
```

Wynik:

```text
Wspólna Kasa
```

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-napisz-i-uruchom-kod)_

> **Wtręt:** Marta wpisała w `kasa.py` cały podział wydatków, zapisała plik i patrzyła w ekran, czekając na wynik. Nic się nie działo, więc uznała, że komputer jest wolny, a potem, że coś zepsuła. Dopiero gdy wpisała w terminalu `python kasa.py`, pojawił się wynik: sam zapis pliku to tylko położenie przepisu w szufladzie, a gotować ktoś musi zacząć.

<details>
<summary>Na marginesie: Skąd Python wziął swoją nazwę</summary>

Polecenie `python`, którego używamy do uruchamiania plików, ma nazwę nie od węża, lecz od brytyjskiego programu komediowego. Twórca języka, Guido van Rossum, czytał w czasie pracy nad nim scenariusze „Monty Python's Flying Circus” i chciał nazwy krótkiej, unikalnej i lekko tajemniczej. Stąd w dokumentacji języka i przykładach często pojawiają się żarty z tego programu.

Źródło: [Python FAQ: Why is it called Python?](https://docs.python.org/3/faq/general.html#why-is-it-called-python)

</details>

## Odróżnij kompilator od interpretera

[Kompilator](00%20Glosariusz.md#kompilator) i interpreter to programy, które przekładają kod źródłowy na działanie komputera, bo procesor sam nie rozumie tekstu z pliku. Kompilator tłumaczy cały kod naraz na osobny, gotowy do uruchomienia plik. Interpreter czyta kod i wykonuje go na bieżąco, instrukcja po instrukcji.

<a id="ref-38"></a>[To ten wykonawca, o którym była mowa przy uruchamianiu programu](#uruchom-swój-program). Gdy wpisujesz `python rozlicz.py`, Python działa jako interpreter: bierze plik i wykonuje go od góry.

| | Kompilator | Interpreter |
|---|---|---|
| Co robi | tłumaczy całość przed startem | wykonuje kod w trakcie czytania |
| Wynik | osobny plik do uruchomienia | brak pliku, od razu efekt |
| Uruchomienie po zmianie | najpierw kompilacja, potem start | zapisz i uruchom |

```text
kompilator:   kod źródłowy --> [kompilator] --> plik programu --> uruchomienie
interpreter:  kod źródłowy --> [interpreter] --> uruchomienie
```

<a id="ref-30"></a>Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania. [Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie](#lm-18). W praktyce Python najpierw przekłada plik na pośredni zapis, ale z Twojej strony to jedno polecenie.

> **Z przymrużeniem oka:** Kompilator to tłumacz, który zabiera całą książkę i oddaje ją przetłumaczoną dopiero na końcu. Interpreter to tłumacz symultaniczny: mówi na bieżąco, więc o błędzie w ostatnim rozdziale dowiesz się dopiero, gdy do niego dojdzie.

## Rozpoznaj błąd w programie

[Błąd w programie](00%20Glosariusz.md#błąd-w-programie) to każde miejsce, w którym program robi coś innego, niż chciał jego autor. Albo zatrzymuje się z komunikatem, albo działa do końca i podaje zły wynik.

Pierwszy rodzaj widać od razu. Python czyta plik od góry i gdy trafi na coś, czego nie rozumie, przerywa pracę i wypisuje komunikat. Tak jest, gdy literówka zmieni [print](00%20Glosariusz.md#print) (polecenie, które każe programowi wypisać tekst lub liczbę na ekranie) w `prnt`: <a id="lm-21"></a>interpreter nie zna takiego słowa. To jeszcze nie katastrofa, bo komunikat wskazuje linię i powód.

Drugi rodzaj jest podstępniejszy, bo nic nie ostrzega. Zobacz, co zrobi program z pozoru poprawny:

```python
# poza kanonem: błąd w dzieleniu
print("Wspólna Kasa")
print(300 / 2)   # 300 zł na troje osób
```

```text
Wspólna Kasa
150.0
```

Python wykonał każdą instrukcję zgodnie z zapisem, tylko że zapis był zły: na troje trzeba dzielić przez 3. Komputer robi dokładnie to, co napisano, a nie to, co miało się na myśli.

Konsekwencja: błąd to normalna część pracy, nie porażka. Komunikat to podpowiedź, a brak komunikatu nie znaczy, że wynik jest dobry. Jak rozróżniać te rodzaje błędów i czytać komunikaty, [omówimy osobno, w dziale o poprawianiu programów](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#ref-42).

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Celowo psujemy nazwę print, wpisując prnt.

```diff
 # kasa.py - pierwszy skrypt Wspólnej Kasy
-print("Wspólna Kasa")
+prnt("Wspólna Kasa")
```

<details>
<summary>Cały plik <code>kasa.py</code> po zmianie</summary>

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
prnt("Wspólna Kasa")
```

</details>

**Krok 2. Uruchom.** Uruchamiamy i oglądamy pierwszy błąd.

```bash
python kasa.py
```

Zobaczysz błąd (celowy, poprawimy go):

```text
Traceback (most recent call last):
  File "/home/ala/wspolna_kasa/kasa.py", line 2, in <module>
    prnt("Wspólna Kasa")
    ^^^^
NameError: name 'prnt' is not defined. Did you mean: 'print'?
```

_Wersje: Python 3.13_

> **Wtręt:** Marta zamiast `print` wpisała `prnt`, uruchomiła plik i zobaczyła czerwony komunikat o nieznanej nazwie. Cofnęła ręce z klawiatury jak spod gorącego piekarnika, przekonana, że zepsuła komputer. Dopiero po chwili zauważyła, że komunikat podaje numer linii i to samo słowo, które przed chwilą napisała z błędem. Komputer był cały, tylko grzecznie poprosił o poprawkę.

> **Pułapka: Brak komunikatu nie oznacza poprawnego wyniku.** `print(300 / 2)` działa bez błędu i wypisuje `150.0`, choć dla trojga osób powinno być dzielenie przez 3. Program "bez błędów" może dawać zły wynik, więc trzeba samemu sprawdzić wynik, np. własnym obliczeniem.

## Opisuj kod komentarzami

Komentarz to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi.

W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. Interpreter pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją.

<a id="ref-35"></a>

```python
# rozlicz.py - rozliczenie wspólnych wydatków
print("Wspólna Kasa")
# udział na dwie osoby
print(300 / 3)  # 300 zł na troje osób
# print(300 / 2)  <- ta linia jest wyłączona
```

```text
Wspólna Kasa
100.0
```

Ostatnia linia pokazuje drugie zastosowanie: zamiana instrukcji na komentarz „wyłącza” ją bez kasowania. Przyda się to, gdy będziesz coś sprawdzać.

Komentarz ma sens, gdy podaje powód lub kontekst („300 zł na troje osób”). Powtarzanie tego, co widać w kodzie, tylko go zaśmieca.

Komentarz może się też zestarzeć. W przykładzie wyżej linia `# udział na dwie osoby` stoi nad dzieleniem przez 3, więc kłamie, a Python tego nie zauważy, bo jej nie czyta. Zmieniając kod, poprawiaj też komentarz.

[U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej](#lm-21). Komentarz nie przeszkadza w znalezieniu błędu: popraw literówkę i uruchom plik ponownie.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Poprawiamy literówkę prnt na print; komentarz zostaje.

```diff
 # kasa.py - pierwszy skrypt Wspólnej Kasy
-prnt("Wspólna Kasa")
+print("Wspólna Kasa")
```

<details>
<summary>Cały plik <code>kasa.py</code> po zmianie</summary>

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
```

</details>

**Krok 2. Uruchom.** Uruchamiamy poprawiony skrypt.

```bash
python kasa.py
```

Wynik:

```text
Wspólna Kasa
```

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-napisz-i-uruchom-kod)_

> **Z życia wzięte:** W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygodni ufałem komentarzowi i szukałem błędu w danych, choć dane były w porządku. Od tamtej pory zmieniając kod, w tym samym momencie sprawdzam komentarz przy nim. Jeśli komentarz tylko powtarza kod, wolę go usunąć, bo nie ma czego zestarzeć.

## Co zapamiętać

- Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
- Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.
- Uruchomienie programu to polecenie, by Python wykonał instrukcje z pliku po kolei, a sam plik pozostaje bez zmian.
- Kompilator tłumaczy cały kod na osobny plik przed startem, a interpreter wykonuje kod na bieżąco, dlatego w Pythonie wystarczy zapisać i uruchomić.
- Błąd to rozbieżność między zamiarem a działaniem programu: czasem zatrzymuje go komunikat, a czasem zły wynik pojawia się po cichu.
- Komentarz zaczyna się od `#`, jest pomijany przez Pythona i ma wyjaśniać powód, a nie powtarzać kod; po zmianie kodu trzeba go zaktualizować.

## Pytania sprawdzające

### 13. Czym jest kod źródłowy?

<details>
<summary>Odpowiedź</summary>

Kod źródłowy to tekst programu zapisany w języku programowania, czytelny dla człowieka. Jest zwykłym plikiem tekstowym, w którym każda linia to instrukcja zapisana według reguł składni. Komputer nie wykonuje go bezpośrednio, tylko czyta go osobny program. Programista tworzy i poprawia właśnie kod źródłowy.

Zobacz: [sekcja „Poznaj kod źródłowy”](#poznaj-kod-źródłowy).

</details>

### 14. Do czego służy edytor kodu?

<details>
<summary>Odpowiedź</summary>

Edytor kodu służy do pisania i poprawiania kodu źródłowego. Podświetla składnię, numeruje linie, pilnuje wcięć i nawiasów oraz podpowiada nazwy, dzięki czemu łatwiej zauważyć pomyłki. Sam kodu nie uruchamia, a zapisany plik jest zwykłym tekstem, który otworzysz w każdym innym programie.

Zobacz: [sekcja „Pisz kod w edytorze”](#pisz-kod-w-edytorze).

</details>

### 15. Co to znaczy uruchomić program?

<details>
<summary>Odpowiedź</summary>

Uruchomić program znaczy polecić komputerowi, by wykonał instrukcje z pliku po kolei, od pierwszej do ostatniej. Robi to inny program, w naszym przypadku Python, któremu podajemy nazwę pliku w terminalu. Samo uruchomienie nie zmienia pliku, więc można je powtarzać po każdej poprawce.

Zobacz: [sekcja „Uruchom swój program”](#uruchom-swój-program).

</details>

### 16. Czym jest kompilator lub interpreter?

<details>
<summary>Odpowiedź</summary>

Kompilator i interpreter to programy, które zamieniają kod źródłowy na działanie komputera. Kompilator tłumaczy cały program naraz na osobny plik gotowy do uruchomienia. Interpreter czyta kod i wykonuje go na bieżąco, bez osobnego pliku. Python jest używany jako interpreter, więc po zmianie kodu wystarczy zapisać plik i uruchomić go ponownie.

Zobacz: [sekcja „Odróżnij kompilator od interpretera”](#odróżnij-kompilator-od-interpretera).

</details>

### 17. Co to jest błąd w programie?

<details>
<summary>Odpowiedź</summary>

Błąd w programie to miejsce, w którym program robi coś innego, niż zamierzał autor. Czasem program zatrzymuje się z komunikatem, np. przez literówkę w nazwie polecenia. Czasem działa do końca, ale daje zły wynik, bo zapis instrukcji był nieprawidłowy. Komputer wykonuje to, co napisano, nie to, co miano na myśli.

Zobacz: [sekcja „Rozpoznaj błąd w programie”](#rozpoznaj-błąd-w-programie).

</details>

### 18. Do czego służą komentarze w kodzie?

<details>
<summary>Odpowiedź</summary>

Komentarze to notatki w kodzie przeznaczone dla człowieka: interpreter ich pomija. Wyjaśniają, dlaczego coś jest napisane, oraz pozwalają czasowo wyłączyć instrukcję. Trzeba je aktualizować razem z kodem, bo nieaktualny komentarz wprowadza w błąd.

Zobacz: [sekcja „Opisuj kod komentarzami”](#opisuj-kod-komentarzami).

</details>
