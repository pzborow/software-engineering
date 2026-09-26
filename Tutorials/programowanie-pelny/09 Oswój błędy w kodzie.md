# Oswój błędy w kodzie

Każdy program prędzej czy później się myli, a do tej pory wiedziałeś tylko, że coś poszło nie tak. Ten dział uczy, jak spokojnie znaleźć przyczynę: przeczytać komunikat błędu, sprawdzić program testami, prześledzić go krok po kroku i zapisać poprawioną wersję, żeby nic nie przepadło. Wracamy do funkcji z działu 7 i danych od użytkownika z działu 8, bo w nich najłatwiej o pomyłkę. Na przykładzie „Wspólnej Kasy" naprawimy błąd psujący rozliczenie, a w warsztacie sami go wywołamy, zbadamy i zapiszemy poprawkę w Git.

```text
uruchomienie → komunikat lub zły wynik
   → szukanie przyczyny (debugowanie)
   → poprawka
   → test
        ├─ test nie przechodzi → wracamy do szukania przyczyny
        └─ test przechodzi → zapis wersji (Git)
```

**W tym dziale:**

- [Rozróżnij dwa rodzaje błędów](#rozróżnij-dwa-rodzaje-błędów)
- [Czytaj komunikat o błędzie](#czytaj-komunikat-o-błędzie)
- [Przetestuj swój program](#przetestuj-swój-program)
- [Wytrop błąd krok po kroku](#wytrop-błąd-krok-po-kroku)
- [Zapisuj wersje kodu](#zapisuj-wersje-kodu)
- [Szukaj rozwiązań w sieci](#szukaj-rozwiązań-w-sieci)

**Warsztat, punkt startowy:** pliki z końca działu 08: `funkcje.py`, `interfejs.py`, `kasa.py`, `nieskonczona.py`, `plik.py`, `pytaj.py` ([treść](99%20Warsztat.md#po-dziale-08)).

## Rozróżnij dwa rodzaje błędów

<a id="ref-42"></a>Błąd [składni](00%20Glosariusz.md#składnia) łamie zasady zapisu, więc Python zatrzymuje się, zanim cokolwiek wykona. [Błąd logiczny](00%20Glosariusz.md#błąd-logiczny) ma zapis poprawny, ale robi coś innego, niż zamierzałeś, więc program działa i po cichu podaje zły wynik.

[Błąd składni](00%20Glosariusz.md#błąd-składni) to naruszenie składni, czyli reguł zapisu: brakujący dwukropek, niedomknięty cudzysłów, źle wcięta linia. Python czyta cały plik przed startem, więc nie wykona nawet linii sprzed błędu:

```python
print("start")
suma = 45.5 + 20
if suma > 10
    print("dużo")
```

```text
  File "blad.py", line 3
    if suma > 10
                ^
SyntaxError: expected ':'
```

<a id="lm-61"></a>Słowo „start” się nie pojawiło, a komunikat wskazuje linię i miejsce.

Błąd logiczny to pomyłka w pomyśle: zły wzór, dzielnik albo warunek. Python jej nie zauważy, bo każda instrukcja jest poprawna. Trzy osoby dzielą wydatki 45.5, 20 i 12.5 zł:

```python
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)
```

```text
Na osobę: 39.0
```

<a id="lm-60"></a>Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.

Konsekwencja: błędy składni są uciążliwe, ale łatwe, bo wskaże je Python. Za błędy logiczne odpowiadasz Ty, więc wynik porównuj z rachunkiem na kartce. [Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu](#ref-119).

_Wersje: Python 3.13 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#09-oswój-błędy-w-kodzie)_

> **Wtręt:** Marta uruchomiła program, nie zobaczyła żadnego czerwonego komunikatu i uznała, że skoro Python milczy, to wszystko się zgadza. Wysłała współlokatorom wynik `39.0` zł na osobę, choć dzielnik w programie wynosił `2`, a osób było troje. Dopiero jedna z koleżanek policzyła to na kartce i wyszło `26.0`. Marta zrozumiała, że brak komunikatu znaczy tylko tyle, że zapis jest poprawny, a nie że wynik jest dobry.

> **Z życia wzięte:** Napisałem skrypt liczący średni czas realizacji zamówień, ale dzieliłem sumę czasów przez liczbę wszystkich zamówień, a sumowałem tylko zrealizowane. Skrypt działał bez żadnego błędu, a raport miał sensowne liczby, więc przez kilka tygodni nikt go nie kwestionował. Rozbieżność wyszła, gdy porównałem wynik z ręcznym rachunkiem na dziesięciu rekordach. Od tamtej pory każdy nowy wzór sprawdzam na małej próbce policzonej ręcznie, bo błąd logiczny nie zgłosi się sam.

## Czytaj komunikat o błędzie

<a id="ref-94"></a><a id="lm-62"></a>Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak, a linie nad nią pokazują, gdzie to się stało. Komunikat nie jest wyrokiem, tylko wskazówką.

Gdy program zatrzyma się w trakcie pracy, Python wypisuje [Traceback](00%20Glosariusz.md#traceback), czyli ślad wywołań: listę miejsc w kodzie, przez które przeszło wykonanie aż do błędu. Wszystko razem to [komunikat o błędzie](00%20Glosariusz.md#komunikat-o-błędzie), czyli tekst, w którym Python opisuje, co go zatrzymało i w którym miejscu. Dzielimy przez zero:

```python
# blad_pusta.py - Traceback: dzielenie przez zero
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))
```

```text
Start
Traceback (most recent call last):
  File "/home/ania/wspolna_kasa/blad_pusta.py", line 6, in <module>
    print(na_osobe(0, 0))
          ~~~~~~~~^^^^^^
  File "/home/ania/wspolna_kasa/blad_pusta.py", line 3, in na_osobe
    return suma / osoby
           ~~~~~^~~~~~~
ZeroDivisionError: division by zero
```

(Ścieżka u Ciebie będzie inna, bo zależy od miejsca pliku.)

Ostatnia linia ma dwie części: nazwę błędu (`ZeroDivisionError`, dzielenie przez zero) i opis (`division by zero`). Wyżej stoją pary „plik, linia, funkcja” i przepisana linia kodu. Ostatnia para jest miejscem, w którym Python się potknął, a wyższe pokazują, kto tę funkcję wywołał. Znaki `^` i `~` wskazują fragment linii.

[Inaczej niż przy błędzie składni ze „Startem”, który się nie pojawił](#lm-61), tu „Start” się wypisał, bo program ruszył i padł dopiero w środku.

Konsekwencja: nie bój się czerwonego tekstu. <a id="ref-117"></a>Przeczytaj ostatnią linię, znajdź w śladzie własny plik i numer linii, a zwykle już wiesz, gdzie szukać. [Szukanie przyczyny krok po kroku omówimy przy debugowaniu](#ref-119).

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `blad_pusta.py`.** Zapisujemy skrypt, który celowo dzieli przez zero.

```python
# blad_pusta.py - Traceback: dzielenie przez zero
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))
```

**Krok 2. Uruchom.** Czytamy komunikat od dołu; ścieżka u Ciebie będzie inna.

```bash
python blad_pusta.py
```

Zobaczysz błąd (celowy, poprawimy go):

```text
Start
Traceback (most recent call last):
  File "/home/ania/wspolna_kasa/blad_pusta.py", line 6, in <module>
    print(na_osobe(0, 0))
          ~~~~~~~~^^^^^^
  File "/home/ania/wspolna_kasa/blad_pusta.py", line 3, in na_osobe
    return suma / osoby
           ~~~~~^~~~~~~
ZeroDivisionError: division by zero
```

_Wersje: Python 3.13 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#09-oswój-błędy-w-kodzie)_

> **Z przymrużeniem oka:** Traceback to łańcuszek „to nie ja, to on”: każda funkcja z góry przyznaje tylko, że wywołała następną. Dopiero ostatnia, ta z `ZeroDivisionError`, mówi uczciwie: „to ja się potknęłam”.

## Przetestuj swój program

[Testowanie](00%20Glosariusz.md#testowanie) to <a id="ref-32"></a>systematyczne sprawdzanie programu na wielu danych, dla których z góry znasz poprawny wynik. Zamiast raz spojrzeć na ekran i uznać, że „wygląda dobrze”, zapisujesz oczekiwania i pozwalasz komputerowi je porównać.

<a id="ref-91"></a>Najprostszy test to jedno sprawdzenie małej funkcji. W Pythonie służy do tego [assert](00%20Glosariusz.md#assert): instrukcja, która nic nie robi, gdy warunek jest prawdziwy, a zatrzymuje program błędem `AssertionError`, gdy jest fałszywy.

```python
def na_osobe(suma, osoby):
    return suma / osoby

assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0
assert na_osobe(100, 4) == 25
print("Wszystkie testy przeszły")
```

```text
Wszystkie testy przeszły
```

Cisza po `assert` znaczy „zgadza się”. Gdyby ktoś zmienił dzielenie tak, że wynik byłby zły, [jak przy błędzie z niewłaściwym dzielnikiem](#lm-60), pierwszy test zatrzymałby program i wskazał linię, w której oczekiwanie przestało być prawdą.

Dobre testy obejmują zwykłe dane i przypadki brzegowe, np. pustą listę wydatków. Kosztują chwilę, a po każdej zmianie kodu uruchamiasz je jednym poleceniem i wiesz, czy niczego nie zepsułeś.

Test nie dowodzi, że błędów nie ma, tylko że w sprawdzonych przypadkach ich nie ma. Gdy test się wywali, szukanie przyczyny omówimy przy debugowaniu.

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `test_kasa.py`.** Tworzymy plik z czterema testami funkcji z funkcje.py.

```python
# test_kasa.py - testy funkcji Wspólnej Kasy
from funkcje import suma, na_osobe

assert suma([45.5, 20, 12.5]) == 78.0
assert suma([]) == 0
assert na_osobe(78.0, 3) == 26.0
assert na_osobe(0, 4) == 0
print("Wszystkie testy przeszły")
```

**Krok 2. Uruchom.** Dwie pierwsze linie to wypisy z funkcje.py, wykonane przy imporcie.

```bash
python test_kasa.py
```

Wynik:

```text
Mazury: 26.0
Tatry: 112.5
Wszystkie testy przeszły
```

**Ilustracja:** _Most, który przeszedł cztery próby, wciąż czeka na piątą._

Tekst alternatywny: Uśmiechnięta osoba przy klockowym mostku sprawdza go po kolei samochodzikiem, ciężarówką, misiem i wózkiem; największa zabawka czeka na swoją kolej.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Jasny pokój z dywanem. Uśmiechnięta osoba klęczy przy małym drewnianym mostku zbudowanym z klocków nad niebieskim kocem udającym rzekę. Po mostku jedzie kolejno rząd zabawek: malutki samochodzik, drewniana ciężarówka, pluszowy miś i pusty wózek. Obok stoi mały zielony ptaszek-kartka w kształcie znaczka z symbolem odhaczenia (bez liter) i kilka odhaczonych kartek leży w rzędzie. Jedna zabawka, największa, czeka jeszcze na końcu kolejki i osoba patrzy na nią z ciekawością.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/09-przetestuj-swój-program-1.png`

</details>

> **Wtręt:** Marta dopisała jeden `assert na_osobe(78, 3) == 26`, zobaczyła „Wszystkie testy przeszły” i uznała sprawę za zamkniętą. W następnym miesiącu wyjazd rozliczała sama, wpisała `na_osobe(120, 0)` i dostała czerwony `ZeroDivisionError`. Jeden test sprawdził jedną sytuację, a przypadek brzegowy czekał cierpliwie na swoją kolej.

## Wytrop błąd krok po kroku

<a id="ref-121"></a>[Debugowanie](00%20Glosariusz.md#debugowanie) to szukanie przyczyny błędu i jej usuwanie. <a id="ref-119"></a>Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach.

Metoda jest prosta. Najpierw odtwarzasz błąd na jednych, konkretnych danych. Potem zawężasz miejsce: przed podejrzanym krokiem wypisujesz wartości i porównujesz je z tym, czego oczekujesz. Pierwsze miejsce, w którym wartość jest inna niż powinna, wskazuje przyczynę. Na końcu poprawiasz jedną rzecz i uruchamiasz ponownie.

Weźmy [błąd logiczny z wynikiem 39.0 zamiast 26.0](#lm-60). Podejrzewamy dwa dane wejściowe dzielenia, więc je wypisujemy:

```python
def na_osobe(suma, osoby):
    return suma / osoby

suma = 78.0
liczba_osob = 2
print("DEBUG suma:", suma)
print("DEBUG liczba_osob:", liczba_osob)
print(na_osobe(suma, liczba_osob))
```

```text
DEBUG suma: 78.0
DEBUG liczba_osob: 2
39.0
```

Suma się zgadza, a liczba osób nie: mają być trzy. Funkcja jest w porządku, błąd siedzi w danych, które jej podajemy. Bez wypisania szukalibyśmy pewnie w dzieleniu.

Gdy [test z poprzedniej sekcji](#przetestuj-swój-program) zgłosi błąd, zaczynasz tak samo: odtwarzasz przypadek, który go wywołał, i patrzysz na wartości. Po naprawie usuń linie z `DEBUG`, żeby nie zaśmiecały wyniku.

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `debug.py`.** Program z błędnymi danymi i liniami DEBUG.

```python
# debug.py - szukanie przyczyny złego wyniku przez print
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

mazury = [45.5, 20, 12.5]
liczba_osob = 2
print("DEBUG suma:", suma(mazury))
print("DEBUG liczba_osob:", liczba_osob)
print("Mazury na osobę:", na_osobe(suma(mazury), liczba_osob))
```

**Krok 2. Uruchom.** Wynik jest zły, ale wypisane wartości pokazują, że winna jest liczba osób.

```bash
python debug.py
```

Wynik:

```text
DEBUG suma: 78.0
DEBUG liczba_osob: 2
Mazury na osobę: 39.0
```

**Krok 3. Zmień plik `debug.py`.** Poprawiamy liczbę osób i usuwamy linie DEBUG.

```diff
 mazury = [45.5, 20, 12.5]
-liczba_osob = 2
-print("DEBUG suma:", suma(mazury))
-print("DEBUG liczba_osob:", liczba_osob)
+liczba_osob = 3
 print("Mazury na osobę:", na_osobe(suma(mazury), liczba_osob))
```

<details>
<summary>Cały plik <code>debug.py</code> po zmianie</summary>

```python
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
```

</details>

**Krok 4. Uruchom.**

```bash
python debug.py
```

Wynik:

```text
Mazury na osobę: 26.0
```

## Zapisuj wersje kodu

Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast szukać własnych zmian z pamięci.

Robi to [Git](00%20Glosariusz.md#git), program do zapisywania historii plików. Zapis jednej wersji to [commit](00%20Glosariusz.md#commit): zdjęcie wybranych plików z danej chwili, z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię, to [repozytorium](00%20Glosariusz.md#repozytorium). <a id="ref-110"></a>W przykładowym programie do dzielenia wydatków, „Wspólnej Kasie”, będzie nim folder `wspolna_kasa`, w którym leżą pliki programu.

Wersje przydają się w trzech sytuacjach:

- Dopisujesz do „Wspólnej Kasy” nową funkcję, testy przestają przechodzić, a Ty wracasz do wczorajszego commita zamiast szukać własnych zmian.
- Historia pokazuje, kiedy pojawił się błąd, co przy szukaniu przyczyny oszczędza sporo czasu.
- Każdy commit ma opis, więc po miesiącu wiesz, dlaczego kod wygląda tak, a nie inaczej.

Dobry moment na commit to chwila, gdy testy przechodzą. Wiele małych commitów jest lepsze niż jeden wielki.

Sam zapis wygląda tak:

```text
git init -b main
git add funkcje.py test_rozlicz.py
git commit -m "Funkcje i testy Wspolnej Kasy"
```

`init` zakłada repozytorium w bieżącym folderze, `add` wybiera pliki do zapisu, a `commit` zapisuje wersję. Git trzeba mieć zainstalowanym (sprawdzisz to poleceniem `git --version`, a instalator jest na stronie git-scm.com).

> **Warsztat: zrób u siebie**

**Krok 1. Uruchom.** Sprawdzamy, czy Git jest zainstalowany; jeśli nie, pobierz go ze strony git-scm.com.

```bash
git --version
```

Wynik:

```text
git version 2.43.0
```

**Krok 2. Uruchom.** Jednorazowo podpisujemy swoje commity imieniem.

```bash
git config --global user.name "Twoje Imie"
```

**Krok 3. Uruchom.** Jednorazowo podajemy adres e-mail do commitów.

```bash
git config --global user.email "ty@example.com"
```

**Krok 4. Uruchom.** Zakładamy repozytorium w folderze wspolna_kasa.

```bash
git init -b main
```

Wynik:

```text
Initialized empty Git repository in /home/ania/wspolna_kasa/.git/
```

**Krok 5. Uruchom.** Wybieramy pliki, które trafią do wersji.

```bash
git add funkcje.py test_kasa.py
```

**Krok 6. Uruchom.** Zapisujemy pierwszą wersję z opisem.

```bash
git commit -m "Funkcje Wspolnej Kasy i testy"
```

Wynik:

```text
[main (root-commit) 3f2a9c1] Funkcje Wspolnej Kasy i testy
 2 files changed, 22 insertions(+)
 create mode 100644 funkcje.py
 create mode 100644 test_kasa.py
```

_Wersje: Git 2.x · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#09-oswój-błędy-w-kodzie)_

## Szukaj rozwiązań w sieci

Wpisz w wyszukiwarkę to, co widzisz: ostatnią linię komunikatu o błędzie i nazwę języka. Prawie każdy błąd ktoś już miał i ktoś już opisał, jak go naprawić.

Ostatnia linia Tracebacku to ta, którą, [jak w sekcji o czytaniu komunikatów, czytasz od dołu](#lm-62). <a id="lm-67"></a>Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych, bo nikt inny ich nie ma.

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

## Co zapamiętać

- Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.
- Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.
- Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.
- Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.
- Commit zapisuje działającą wersję kodu z opisem, dzięki czemu zawsze możesz do niej wrócić i sprawdzić, kiedy coś się zepsuło.
- Szukaj po ostatniej linii komunikatu i nazwie języka, oceniaj źródła i nigdy nie wklejaj skopiowanego kodu bez zrozumienia.

## Pytania sprawdzające

### 50. Czym różni się błąd składni od błędu logicznego?

<details>
<summary>Odpowiedź</summary>

Błąd składni to zapis niezgodny z regułami języka, więc Python zatrzymuje program przed startem i wskazuje linię. Błąd logiczny to poprawny zapis z błędnym pomysłem, więc program działa, ale daje zły wynik i nie ma żadnego komunikatu. Pierwszy znajduje Python, drugi musisz znaleźć sam, porównując wynik z oczekiwanym.

Zobacz: [sekcja „Rozróżnij dwa rodzaje błędów”](#rozróżnij-dwa-rodzaje-błędów).

</details>

### 51. Jak przeczytać komunikat o błędzie?

<details>
<summary>Odpowiedź</summary>

Czytaj komunikat od dołu: ostatnia linia podaje nazwę i opis błędu, a linie nad nią (Traceback) pokazują plik, numer linii i funkcję, w której program się zatrzymał. Najpierw znajdź w śladzie własny plik i numer linii, potem sprawdź, co jest w tej linii.

Zobacz: [sekcja „Czytaj komunikat o błędzie”](#czytaj-komunikat-o-błędzie).

</details>

### 52. Czym jest testowanie programu?

<details>
<summary>Odpowiedź</summary>

Testowanie programu to systematyczne sprawdzanie go na wielu danych, dla których znasz poprawny wynik. Zapisujesz oczekiwania w kodzie, na przykład przez assert, a komputer porównuje je z tym, co program naprawdę zwraca. Dzięki temu po każdej zmianie szybko widzisz, czy coś przestało działać.

Zobacz: [sekcja „Przetestuj swój program”](#przetestuj-swój-program).

</details>

### 53. Czym jest debugowanie?

<details>
<summary>Odpowiedź</summary>

Debugowanie to szukanie przyczyny błędu w programie i jej usuwanie. Zamiast zgadywać, sprawdzasz krok po kroku, co program naprawdę robi: w których miejscach wartości są takie, jak myślałeś, a w którym przestają. Najprostsze narzędzie to `print`, który pokazuje wartości w trakcie pracy.

Zobacz: [sekcja „Wytrop błąd krok po kroku”](#wytrop-błąd-krok-po-kroku).

</details>

### 54. Dlaczego warto zapisywać kolejne wersje kodu?

<details>
<summary>Odpowiedź</summary>

Zapisujesz wersje, żeby móc wrócić do stanu, który działał, gdy kolejna zmiana coś zepsuje. Historia pokazuje też, kiedy pojawił się błąd, a opisy commitów przypominają, dlaczego kod wygląda tak, a nie inaczej. Robi to program Git: każdy commit to zapisana wersja plików z krótkim opisem.

Zobacz: [sekcja „Zapisuj wersje kodu”](#zapisuj-wersje-kodu).

</details>

### 55. Jak szukać rozwiązań problemów programistycznych w internecie?

<details>
<summary>Odpowiedź</summary>

Wpisz w wyszukiwarkę ostatnią linię komunikatu o błędzie razem z nazwą języka, bez ścieżek i własnych nazw. Gdy komunikatu nie ma, opisz problem słowami. Najpierw sprawdzaj dokumentację i dobrze oceniane odpowiedzi z forów, a znaleziony kod przeczytaj i uruchom na małym przykładzie, zanim go użyjesz.

Zobacz: [sekcja „Szukaj rozwiązań w sieci”](#szukaj-rozwiązań-w-sieci).

</details>
