# Zastosuj wiedzę w praktyce

Znasz już wszystkie klocki, ale wciąż możesz nie wiedzieć, jak użyć ich poza ćwiczeniami. Ten dział pokazuje, gdzie programy spotykasz na co dzień i jak od pomysłu dojść do działającego narzędzia, a Ty dowiesz się, od czego zacząć dalszą naukę i jak zautomatyzować drobne zadania z własnej pracy. Ocenimy Wspólną Kasę, czyli [program](00%20Glosariusz.md#program-komputerowy) do rozliczania wspólnych wydatków, który budowałeś w poprzednich działach, i pomysły na jej rozwój. W warsztacie dopiszesz do niej własną [funkcję](00%20Glosariusz.md#funkcja), np. kto komu ile jest winien, i zapiszesz ją w historii zmian jako kolejny [commit](00%20Glosariusz.md#commit), tak jak w dziale 9. Tak wygląda droga od pomysłu do działającego programu.

```text
pomysł → plan kroków → kod → test → commit
  ↑                      ↑       │
  │                      └───────┘ nie działa – popraw
  └──────── następny pomysł ──────┘
```

**W tym dziale:**

- [Odkryj programy wokół siebie](#odkryj-programy-wokół-siebie)
- [Przeanalizuj stronę i aplikację mobilną](#przeanalizuj-stronę-i-aplikację-mobilną)
- [Dojdź od pomysłu do programu](#dojdź-od-pomysłu-do-programu)
- [Rozwijaj umiejętności poza kodem](#rozwijaj-umiejętności-poza-kodem)
- [Zacznij naukę od małego problemu](#zacznij-naukę-od-małego-problemu)
- [Zautomatyzuj proste zadania](#zautomatyzuj-proste-zadania)

**Warsztat, punkt startowy:** pliki z końca działu 09: `blad_pusta.py`, `debug.py`, `funkcje.py`, `interfejs.py`, `kasa.py`, `nieskonczona.py`, `plik.py`, `pytaj.py`, `test_kasa.py` ([treść](99%20Warsztat.md#po-dziale-09)).

## Odkryj programy wokół siebie

Na co dzień używasz dziesiątek programów, choć rzadko o tym myślisz: komunikatora, mapy, banku w telefonie, arkusza kalkulacyjnego, przeglądarki. Każdy z nich to program albo [aplikacja](00%20Glosariusz.md#aplikacja), czyli program z oprawą dla użytkownika, i działa według tego samego schematu, który znasz z własnych skryptów.

Zawsze są [dane wejściowe](00%20Glosariusz.md#dane-wejściowe), jakieś przetwarzanie i [dane wyjściowe](00%20Glosariusz.md#dane-wyjściowe):

| Program | Wejście | Co robi | Wyjście |
|---|---|---|---|
| Nawigacja | cel podróży, Twoja pozycja | wybiera najkrótszą trasę | trasa na mapie |
| Bank w telefonie | kwota i numer konta | sprawdza saldo, księguje przelew | potwierdzenie |
| Arkusz kalkulacyjny | liczby w komórkach | liczy wzory | sumy i wykresy |
| Wyszukiwarka | wpisane słowa | szuka i układa wyniki | lista stron |
| Alarm w telefonie | ustawiona godzina | porównuje ją z zegarem | dzwonek |

Pod spodem są te same klocki, które już budowałeś: zmienne, decyzje (`if`), pętle po listach, funkcje i pliki. Nawigacja też przegląda listę dróg i wybiera jedną, a bank też sprawdza dane od użytkownika, zanim cokolwiek zaksięguje.

Różni je skala i [interfejs](00%20Glosariusz.md#interfejs-użytkownika): przyciski i mapy zamiast pytań w terminalu. [Program do dzielenia wspólnych wydatków między osoby, który budujesz w warsztacie](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#lm-60) (nazywamy go „Wspólna Kasa”), należy do tej samej rodziny: bierze wydatki, liczy i wypisuje, kto ile zapłacił. Jest po prostu mały. [Czym różni się strona internetowa od aplikacji mobilnej, wyjaśnimy w następnej sekcji](#ref-126).

Konsekwencja: skoro gotowe programy to złożone proste kroki, da się je zrozumieć, a proste zadania z Twojej pracy da się zautomatyzować własnym małym programem.

> **Z przymrużeniem oka:** Alarm w telefonie to wzorowy program: bierze dane wejściowe (godzinę), porównuje je z zegarem i bez wahania oddaje dane wyjściowe, czyli dzwonek. Że wyjściem bywa też Twoja irytacja, to już efekt uboczny.

## Przeanalizuj stronę i aplikację mobilną

<a id="ref-126"></a>Strona internetowa działa w [przeglądarce](00%20Glosariusz.md#przeglądarka) (programie do otwierania stron, np. Chrome czy Firefox) i otwierasz ją przez adres, a aplikacja mobilna to program zainstalowany w telefonie, pobrany ze sklepu. Obie są aplikacjami w sensie oprawy dla użytkownika, ale trafiają do niego inaczej.

Strona leży na cudzym komputerze, czyli [serwerze](00%20Glosariusz.md#serwer) (komputerze w internecie, który przechowuje stronę i odpowiada na zapytania). Przeglądarka pobiera ją za każdym razem, więc nic nie instalujesz, a autor może ją poprawić dla wszystkich naraz. Ta sama strona działa na komputerze, tablecie i telefonie.

Aplikacja mobilna jest zainstalowana na urządzeniu. Ma łatwiejszy dostęp do aparatu, powiadomień czy czujników i często działa bez internetu. Za to wymaga pobrania, aktualizacji i osobnej wersji dla każdego systemu, np. Androida i iOS.

| Cecha | Strona internetowa | Aplikacja mobilna |
|---|---|---|
| Uruchomienie | adres w przeglądarce | ikona na telefonie |
| Instalacja | brak | ze sklepu |
| Aktualizacja | automatyczna, u autora | pobierasz nową wersję |
| Dostęp do aparatu i czujników | ograniczony | szeroki |
| Bez internetu | zwykle nie działa | często działa |

Pod spodem obie robią to samo, co każdy program: [dane wejściowe, przetwarzanie, dane wyjściowe](#odkryj-programy-wokół-siebie). We „Wspólnej Kasie” <a id="lm-68"></a>wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.

Konsekwencja: rachunki możesz kiedyś udostępnić jako stronę, którą znajomi otworzą przez link, albo jako aplikację w telefonie. Na razie masz wersję w terminalu, a jej funkcje liczące przydałyby się w obu wariantach.

> **Z życia wzięte:** Zbudowałem prostą stronę do odnotowywania stanów w magazynie i przez biurowe Wi-Fi działała bez zarzutu. W piwnicznej hali zasięgu prawie nie było, więc strona wczytywała się w połowie albo wcale, a pracownicy zapisywali liczby na kartkach. Okazało się, że to zadanie dla aplikacji, która działa bez internetu i wysyła dane, gdy sieć wróci. Od tamtej pory pytam najpierw, gdzie i w jakich warunkach ktoś będzie z programu korzystać, a dopiero potem wybieram formę.

> **Wtręt:** Marta uznała, że „aplikacją” jest plik `kasa.py` wysłany współlokatorom mailem. Gdy poprawiła w nim liczenie napiwku, wysłała nową wersję, ale jedna osoba dalej uruchamiała starą, zapisaną na pulpicie, i wyszła jej inna kwota niż pozostałym. Gdyby program stał na serwerze jako strona, każdy pobierałby przy otwarciu tę samą, poprawioną wersję.

## Dojdź od pomysłu do programu

Od pomysłu do programu dochodzi się małymi krokami: opisujesz zadanie zwykłymi słowami, piszesz najmniejszy kawałek, który coś robi, sprawdzasz go i dopiero wtedy dokładasz następny. Cały program naraz zwykle nie działa, a szukanie błędu w stu liniach jest męczące.

<a id="lm-69"></a>

```text
pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit
              ↑                                                            |
              └──────────────────── następny kawałek ←─────────────────────┘
```

Weźmy pomysł: „chcę wiedzieć, kto komu ile jest winien”. Opis krokowy to rozbicie zadania na kroki, z których każdy da się zrobić osobno: dla każdej osoby zsumuj to, co zapłaciła, odejmij jej równy udział i wypisz wynik. Z tego wychodzi jedna mała funkcja:

```python
def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...
```

Funkcję sprawdzasz na danych, których wynik znasz z kartki. Dopiero gdy się zgadza, zapisujesz commit (zapisaną wersję kodu z opisem) i myślisz o kolejnym kawałku, np. wczytaniu wydatków z pliku.

Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, [jak w sekcji o zapisywaniu wersji kodu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#zapisuj-wersje-kodu). Dzięki temu nie zgadujesz, gdzie szukać błędu.

**Ilustracja:** _Każdy sprawdzony kawałek to kolejny hak: jak coś pójdzie źle, spadasz tylko do ostatniego._

Tekst alternatywny: Uśmiechnięta wspinaczka w kasku wbija hak w skałę. Pod nią w równych odstępach tkwią wcześniejsze haki połączone liną, a na dole stoi człowiek z termosem i trzyma koniec liny.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Ciepła scena na łagodnej skalnej ścianie w górach. Uśmiechnięta wspinaczka w kasku i uprzęży pnie się w górę i właśnie wbija kolejny hak z liną. Poniżej niej, w równych odstępach, widać rządek już wbitych haków z karabinkami, połączonych jedną liną aż do ziemi. Na dole stoi drugi, zadowolony człowiek z termosem i trzyma koniec liny. Za skałą wschodzące słońce, w oddali łąka i kilka drzew.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/10-dojdź-od-pomysłu-do-programu-1.png`

</details>

> **Z przymrużeniem oka:** Szukanie błędu w stu nowych liniach to szukanie zgubionej skarpetki w całym mieszkaniu. Po jednym małym kroku szukasz jej tylko w szufladzie, do której przed chwilą zaglądałeś.

## Rozwijaj umiejętności poza kodem

Poza samym pisaniem kodu programiście przydaje się przede wszystkim rozumienie problemu, jasne komunikowanie się i umiejętność uczenia się. Kod jest jednym z etapów pracy, a dużo czasu schodzi na to, co dzieje się przed nim i po nim.

| Umiejętność | Do czego służy | Przykład we Wspólnej Kasie |
|---|---|---|
| Rozumienie problemu | ustalenie, co program ma zrobić | „Kto komu ile jest winien?” zamiast „policz sumę” |
| Komunikacja | pytania, opisy zmian | pytanie, czy dzielimy po równo |
| Cierpliwość w szukaniu błędów | spokojne zawężanie przyczyny | sprawdzanie wartości wypisanych przez [print](00%20Glosariusz.md#print) |
| Szukanie informacji | radzenie sobie z nowym | [szukanie po ostatniej linii komunikatu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#lm-67) |
| Dokładność | pilnowanie szczegółów | kwota z kropką, nie z przecinkiem |

Rozumienie problemu oznacza rozmowę z osobą, dla której powstaje program. Zanim napiszesz funkcję, musisz wiedzieć, czy znajomi dzielą rachunek po równo i co ma się stać, gdy ktoś nie płaci. Błędne założenie kosztuje więcej niż literówka.

Komunikacja to także pisanie: czytelne nazwy, komentarze i opisy commitów są wiadomością dla Ciebie za miesiąc i dla innych osób. Do tego dochodzi cierpliwość, bo błąd rzadko ustępuje od razu, oraz nawyk sprawdzania własnej pracy.

Żadna z tych umiejętności nie wymaga wiedzy technicznej, więc część z nich masz już z pracy i życia. Warto je ćwiczyć razem z kodowaniem.

<details>
<summary>Na marginesie: Gumowa kaczuszka jako rozmówca</summary>

Programiści mają metodę o nazwie „debugowanie gumową kaczką”. Polega na tym, że tłumaczysz swój kod linia po linii postawionej na biurku zabawce. Nazwa pochodzi z książki „The Pragmatic Programmer” z 1999 roku, w której opisano programistę noszącego ze sobą taką kaczuszkę. Bardzo często przyczyna błędu wychodzi na jaw już w trakcie mówienia na głos, choć kaczka nie odpowiada ani słowem.

Źródło: [Rubber duck debugging (Wikipedia)](https://en.wikipedia.org/wiki/Rubber_duck_debugging)

</details>

## Zacznij naukę od małego problemu

Zacznij od jednego małego problemu, który naprawdę Cię dotyczy, i jednego języka, np. [Pythona](00%20Glosariusz.md#python). Nie szukaj idealnego kursu ani najlepszego języka: liczy się to, żebyś pisał(a) kod co tydzień i uruchamiał(a) go u siebie.

Praktyczny początek wygląda tak:

<a id="lm-71"></a>

```text
mały problem → opis krokowy → kilka linii kodu → uruchomienie → commit
```

To ta sama [pętla](00%20Glosariusz.md#pętla), którą znasz z [sekcji o budowie programu od pomysłu](#lm-69). Różnica jest tylko w tym, że teraz to Ty wybierasz pomysł. Dobry pierwszy problem jest mały, znany z życia i da się go sprawdzić na kartce: rozliczenie wydatków, lista zakupów, przeliczanie kwot z arkusza.

Nie kopiuj gotowców bez zrozumienia. Lepiej napisać własną, kulawą wersję niż wkleić cudzą. Gdy utkniesz, szukaj tak, jak [w sekcji o rozwiązaniach w internecie: po ostatniej linii komunikatu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#szukaj-rozwiązań-w-sieci).

Kolejne elementy dokładaj po jednym: dane, decyzje, pętle, funkcje, pliki, testy. Ten tutorial jest taką drogą, a [Wspólna Kasa to jej przykład](#lm-68).

Warsztat poniżej to Twój pierwszy samodzielny krok: dopisujesz do Wspólnej Kasy jedną własną funkcję, która wypisuje, kto ile dopłaca albo dostaje, i zapisujesz ją jako commit. [W kolejnej sekcji zobaczysz, jak taki kawałek kodu zaczyna pracować za Ciebie](#ref-134).

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `dlugi.py`.** Dopisujemy własną funkcję rozliczającą, kto ile dopłaca.

```python
# dlugi.py - kto ile dopłaca, a kto dostaje
def wypisz_dlugi(wydatki, osoby):
    razem = 0
    for wydatek in wydatki:
        razem = razem + wydatek["kwota"]
    udzial = razem / len(osoby)
    for imie in osoby:
        zaplacil = 0
        for wydatek in wydatki:
            if wydatek["kto"] == imie:
                zaplacil = zaplacil + wydatek["kwota"]
        saldo = zaplacil - udzial
        if saldo < 0:
            print(f"{imie} dopłaca {-saldo} zł")
        else:
            print(f"{imie} dostaje {saldo} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.0},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.0},
           {"kto": "Celina", "opis": "bilety", "kwota": 15.0}]
osoby = ["Ania", "Bartek", "Celina"]
wypisz_dlugi(wydatki, osoby)
```

**Krok 2. Uruchom.** Uruchamiamy nową funkcję.

```bash
python dlugi.py
```

Wynik:

```text
Ania dostaje 60.0 zł
Bartek dopłaca 15.0 zł
Celina dopłaca 45.0 zł
```

**Krok 3. Uruchom.** Dodajemy plik do zapisu.

```bash
git add dlugi.py
```

**Krok 4. Uruchom.** Zapisujemy wersję jako commit.

```bash
git commit -m "Dodaj funkcję wypisz_dlugi"
```

Wynik:

```text
[main 3f2a9c1] Dodaj funkcję wypisz_dlugi
 1 file changed, 22 insertions(+)
 create mode 100644 dlugi.py
```

> **Wtręt:** Marta postanowiła, że zacznie dopiero wtedy, gdy znajdzie najlepszy język i idealny kurs, więc przez trzy tygodnie porównywała rankingi i zapisywała się na listy mailingowe. Nie uruchomiła w tym czasie ani jednej linii kodu, a rozliczenie wydatków z współlokatorami w kolejnym miesiącu i tak policzyła w arkuszu. Dopiero gdy wkleiła do pliku `kasa.py` trzy własne, kulawe linie z podziałem rachunku, `print` wypisał jej pierwszy wynik. Miał się nijak do rankingów, ale zgadzał się z kartką.

## Zautomatyzuj proste zadania

[Automatyzacja](00%20Glosariusz.md#automatyzacja) to zlecenie komputerowi powtarzalnej czynności, którą wcześniej robiłeś(-aś) ręcznie. Osoba spoza IT zyskuje na niej czas i pewność: komputer nie nudzi się, nie myli przy setnej pozycji i robi to samo za każdym razem.

<a id="ref-134"></a>Mechanizm znasz: to pętla po danych i funkcja. Zamiast przepisywać kwoty do kalkulatora, opisujesz kroki raz, a program wykonuje je dla dowolnej liczby pozycji. [Tak wygląda to we Wspólnej Kasie](#lm-68):

```python
wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.0},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.0},
           {"kto": "Celina", "opis": "bilety", "kwota": 15.0}]
osoby = ["Ania", "Bartek", "Celina"]
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(f"Razem: {suma} zł")
print(f"Na osobę: {suma / len(osoby)} zł")
```

```text
Razem: 180.0 zł
Na osobę: 60.0 zł
```

Jutro lista ma 200 wydatków zamiast trzech, a kod zostaje ten sam. Ten sam mechanizm obsłuży arkusz z fakturami czy listę zamówień w Twojej pracy.

Nie automatyzuj wszystkiego. Opłaca się zadanie, które powtarzasz często, ma jasne reguły i da się sprawdzić na kartce. Zadanie robione raz w roku lub wymagające oceny człowieka zwykle lepiej zostawić sobie.

Konsekwencja jest praktyczna: zaczynasz od małego, nudnego zadania z własnej pracy i piszesz je [tą samą pętlą nauki](#lm-71). Po commicie masz gotowe narzędzie, do którego możesz wracać. W warsztacie zapisujesz w ten sposób swój `dlugi.py`.

> **Warsztat: zrób u siebie**

**Krok 1. Uruchom.** Sprawdzamy, czy Git jest zainstalowany (numer wersji u Ciebie może być inny).

```bash
git --version
```

Wynik:

```text
git version 2.43.0
```

**Krok 2. Uruchom.** Zakładamy repozytorium w katalogu roboczym (ścieżka u Ciebie będzie inna).

```bash
git init -b main
```

Wynik:

```text
Initialized empty Git repository in /home/ty/wspolna_kasa/.git/
```

**Krok 3. Uruchom.** Git podpisuje commity; wpisz własne dane.

```bash
git config user.name "Twoje Imię" && git config user.email "ty@example.com"
```

**Krok 4. Uruchom.** Pierwszy commit: zapisujemy działający dlugi.py (hash u Ciebie będzie inny).

```bash
git add dlugi.py && git commit -m "Dlugi: kto ile doplaca"
```

Wynik:

```text
[main (root-commit) a1b2c3d] Dlugi: kto ile doplaca
 1 file changed, 22 insertions(+)
 create mode 100644 dlugi.py
```

**Krok 5. Zmień plik `dlugi.py`.** Dopisujemy nagłówek przed wywołaniem funkcji.

```diff
 osoby = ["Ania", "Bartek", "Celina"]
+print("=== Rozliczenie ===")
 wypisz_dlugi(wydatki, osoby)
```

<details>
<summary>Cały plik <code>dlugi.py</code> po zmianie</summary>

```python
# dlugi.py - kto ile dopłaca, a kto dostaje
def wypisz_dlugi(wydatki, osoby):
    razem = 0
    for wydatek in wydatki:
        razem = razem + wydatek["kwota"]
    udzial = razem / len(osoby)
    for imie in osoby:
        zaplacil = 0
        for wydatek in wydatki:
            if wydatek["kto"] == imie:
                zaplacil = zaplacil + wydatek["kwota"]
        saldo = zaplacil - udzial
        if saldo < 0:
            print(f"{imie} dopłaca {-saldo} zł")
        else:
            print(f"{imie} dostaje {saldo} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.0},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.0},
           {"kto": "Celina", "opis": "bilety", "kwota": 15.0}]
osoby = ["Ania", "Bartek", "Celina"]
print("=== Rozliczenie ===")
wypisz_dlugi(wydatki, osoby)
```

</details>

**Krok 6. Uruchom.** Uruchamiamy: program liczy rozliczenie sam.

```bash
python dlugi.py
```

Wynik:

```text
=== Rozliczenie ===
Ania dostaje 60.0 zł
Bartek dopłaca 15.0 zł
Celina dopłaca 45.0 zł
```

**Krok 7. Uruchom.** Zapisujemy zmianę jako kolejny commit (hash u Ciebie będzie inny).

```bash
git add dlugi.py && git commit -m "Naglowek rozliczenia"
```

Wynik:

```text
[main e4f5a6b] Naglowek rozliczenia
 1 file changed, 1 insertion(+)
```

## Co zapamiętać

- Programy, których używasz codziennie, to te same proste klocki (dane, decyzje, pętle, funkcje, pliki) w większej skali i z ładniejszym interfejsem.
- Strona otwiera się w przeglądarce bez instalacji, a aplikacja mobilna jest zainstalowana w telefonie i lepiej korzysta z jego możliwości, ale obie działają według schematu wejście, przetwarzanie, wyjście.
- Buduj program małymi kawałkami: opisz, napisz, sprawdź, zapisz commit, dopiero potem dokładaj następny.
- Pisanie kodu to część pracy programisty; równie ważne są rozumienie problemu, komunikacja, cierpliwość i umiejętność uczenia się.
- Naukę zacznij od jednego małego, własnego problemu i jednego języka, a kod pisz i uruchamiaj regularnie, po kawałku.
- Automatyzuj małe, częste zadania o jasnych regułach: raz opisane w pętli i funkcji działają tak samo dla trzech danych i dla tysiąca.

## Pytania sprawdzające

### 56. Jakie są przykłady programów używanych na co dzień?

<details>
<summary>Odpowiedź</summary>

Na co dzień używasz nawigacji, banku w telefonie, arkusza kalkulacyjnego, wyszukiwarki czy budzika. Każdy z nich przyjmuje dane wejściowe, przetwarza je i zwraca wynik. Pod spodem działają te same klocki co w Twoich skryptach: zmienne, decyzje, pętle, funkcje i pliki.

Zobacz: [sekcja „Odkryj programy wokół siebie”](#odkryj-programy-wokół-siebie).

</details>

### 57. Czym różni się strona internetowa od aplikacji mobilnej?

<details>
<summary>Odpowiedź</summary>

Strona internetowa działa w przeglądarce, jest pobierana z serwera przy każdym otwarciu i nie wymaga instalacji. Aplikacja mobilna jest zainstalowana w telefonie, ma szerszy dostęp do aparatu i czujników i często działa bez internetu, ale trzeba ją pobierać i aktualizować. Pod spodem obie robią to samo: przyjmują dane, przetwarzają je i pokazują wynik.

Zobacz: [sekcja „Przeanalizuj stronę i aplikację mobilną”](#przeanalizuj-stronę-i-aplikację-mobilną).

</details>

### 58. Jak od pomysłu dojść do działającego programu?

<details>
<summary>Odpowiedź</summary>

Dochodzi się do niego małymi krokami: opisujesz zadanie zwykłymi słowami, rozbijasz je na kroki i piszesz najmniejszy kawałek kodu. Sprawdzasz go na danych o znanym wyniku, zapisujesz commit i dopiero potem dokładasz następny kawałek. Dzięki temu błąd zawsze leży w ostatniej zmianie.

Zobacz: [sekcja „Dojdź od pomysłu do programu”](#dojdź-od-pomysłu-do-programu).

</details>

### 59. Jakie umiejętności poza kodowaniem przydają się programiście?

<details>
<summary>Odpowiedź</summary>

Programiście oprócz kodowania przydają się: rozumienie problemu i potrzeb użytkownika, komunikacja (rozmowa, opisy zmian, komentarze), cierpliwość w szukaniu błędów, umiejętność szukania informacji i uczenia się oraz dokładność. Większość pracy to ustalanie, co program ma robić, i sprawdzanie, czy robi to dobrze. Wiele z tych umiejętności możesz mieć już z innych zajęć.

Zobacz: [sekcja „Rozwijaj umiejętności poza kodem”](#rozwijaj-umiejętności-poza-kodem).

</details>

### 60. Od czego zacząć samodzielną naukę programowania?

<details>
<summary>Odpowiedź</summary>

Zacznij od jednego małego problemu z własnego życia i jednego języka, np. Pythona. Pisz i uruchamiaj kod regularnie, małymi kawałkami: opis, kilka linii, uruchomienie, commit. Własna, nawet kulawa wersja uczy więcej niż wklejony gotowiec, a kolejne elementy (pętle, funkcje, pliki, testy) dokładasz po jednym.

Zobacz: [sekcja „Zacznij naukę od małego problemu”](#zacznij-naukę-od-małego-problemu).

</details>

### 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

<details>
<summary>Odpowiedź</summary>

Automatyzacja zleca komputerowi powtarzalne, jasno opisane czynności, np. sumowanie kwot czy podział rachunku. Oszczędza czas i eliminuje pomyłki przy dużej liczbie pozycji, bo pętla i funkcja robią to samo dla trzech danych i dla dwustu. Opłaca się zadanie częste, o jasnych regułach, które da się sprawdzić na kartce.

Zobacz: [sekcja „Zautomatyzuj proste zadania”](#zautomatyzuj-proste-zadania).

</details>
