# Wejdź w świat programowania

[Programowanie](00%20Glosariusz.md#programowanie) od podstaw to kurs dla osób, które codziennie korzystają z komputera, ale nigdy nie zastanawiały się, skąd bierze się to, co robi on na ekranie. Rozwiązuje prosty problem: bez zrozumienia, jak powstają programy, komputer pozostaje tajemniczą skrzynką, której można tylko ufać albo się bać. Zaczniemy od najważniejszego pytania, czyli czym właściwie jest programowanie i dlaczego wymaga tak dużej dokładności. Po tym dziale będziesz umieć własnymi słowami wyjaśnić, czym jest [program](00%20Glosariusz.md#program-komputerowy), czym zajmuje się [programista](00%20Glosariusz.md#programista) i dlaczego komputer działa tylko według precyzyjnych [instrukcji](00%20Glosariusz.md#instrukcja).

**W tym dziale:**

- [Zrozum, czym jest program](#zrozum-czym-jest-program)
- [Odkryj sens programowania](#odkryj-sens-programowania)
- [Przyjrzyj się pracy programisty](#przyjrzyj-się-pracy-programisty)
- [Poznaj język programowania](#poznaj-język-programowania)
- [Podawaj komputerowi każdy szczegół](#podawaj-komputerowi-każdy-szczegół)
- [Odróżnij program od aplikacji](#odróżnij-program-od-aplikacji)

## Zrozum, czym jest program

Program komputerowy to zapisany z góry ciąg poleceń, które komputer wykonuje krok po kroku, żeby zamienić dane na wynik. Komputer sam nic nie wie ani nie zgaduje: robi dokładnie to, co mu zapisano.

Pojedyncze polecenie to instrukcja, czyli jeden mały, jednoznaczny krok, np. „dodaj dwie liczby” albo „wypisz tekst na ekranie”. Program to wiele takich instrukcji ułożonych w określonej kolejności. Kalkulator, przeglądarka i gra działają tak samo, tylko mają instrukcji bardzo dużo.

Prosty schemat każdego programu wygląda tak:

```text
dane na wejściu  -->  program (instrukcje)  -->  wynik na wyjściu
```

Weźmy [przykład, który będzie nam towarzyszył](#lm-2): „Wspólna Kasa”. <a id="lm-2"></a>Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

Program „Wspólna Kasa” zrobi to za ciebie. Na wejściu dostanie listę wydatków (kto zapłacił i ile), a na wyjściu poda rozliczenie. Napisze go programista, czyli [osoba, która zamienia potrzebę na instrukcje](#ref-1) zrozumiałe dla komputera. [Na razie nie piszemy kodu](#ref-3); ważne, że raz zapisane instrukcje można uruchamiać bez końca.

> **Wtręt:** Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo, czy według tego, kto ile zjadł. Dopiero gdy zamieniła to na jednoznaczne kroki (zsumuj wydatki, podziel przez liczbę osób, odejmij to, co kto już zapłacił), dostała wynik.

<details>
<summary>Na marginesie: Pierwszy program powstał przed komputerami</summary>

W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Bernoulliego, uznawany przez wielu za pierwszy opublikowany program komputerowy. Maszyna nigdy nie została zbudowana, więc ten program nie mógł być wtedy uruchomiony.

Źródło: [Ada Lovelace – Wikipedia](https://en.wikipedia.org/wiki/Ada_Lovelace)

</details>

## Odkryj sens programowania

Programowanie to tworzenie programów: zamiana problemu na ciąg instrukcji, które komputer wykona bez twojego udziału. Samo pisanie jest tylko jednym z etapów, a największą część pracy zajmuje wymyślenie rozwiązania.

Zwykle wygląda to tak:

```text
problem --> kroki rozwiązania --> zapis dla komputera --> uruchomienie --> poprawki
                   ^                                                         |
                   +---------------------------------------------------------+
```

Wróćmy do czworga znajomych z wyjazdu. Najpierw trzeba dokładnie ustalić, co jest problemem: kto komu ile ma oddać, żeby każdy zapłacił tyle samo. Potem rozbijasz to na kroki, które wykonałbyś na kartce: zsumuj wydatki, podziel przez liczbę osób, porównaj z tym, co kto zapłacił. Dopiero taki opis zapisujesz w [języku programowania](00%20Glosariusz.md#język-programowania), czyli w ściśle określonym języku, który komputer potrafi odczytać. [Tym językiem zajmiemy się osobno](#ref-5).

Pierwsza wersja rzadko działa idealnie. Uruchamiasz program, patrzysz na wynik, znajdujesz pomyłkę i poprawiasz. Ta pętla poprawek to normalna część pracy, a nie dowód, że coś poszło nie tak.

Zyskujesz na tym jedną rzecz: raz opisane rozwiązanie działa przy każdym kolejnym wyjeździe, dla dowolnych kwot.

**Ilustracja:** _Zanim komputer dostanie instrukcję, ktoś musi ją wymyślić, sprawdzić i poprawić._

Tekst alternatywny: Kobieta przy stole rysuje ołówkiem na kartce schemat ze strzałkami tworzącymi pętlę; obok zmięte kartki i paragony, a cierpliwy mały robot czeka na jej instrukcje.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Przy drewnianym stole siedzi uśmiechnięta kobieta z ołówkiem i gumką. Przed nią kartka z ręcznie narysowanymi kółkami połączonymi strzałkami, które tworzą zamkniętą pętlę. Obok leży kilka zmiętych kartek i paragony z wyjazdu. Na stole stoi mały, przyjazny, okrągły robot z ekranem zamiast twarzy i cierpliwie czeka z założonymi rękami. W tle przez okno widać trzech znajomych z plecakami machających na pożegnanie.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/01-odkryj-sens-programowania-1.png`

</details>

## Przyjrzyj się pracy programisty

Programista to <a id="ref-1"></a>osoba, która zamienia potrzebę na instrukcje: bierze problem opisany zwykłymi słowami i tworzy program, który go rozwiązuje. Pisanie [kodu](00%20Glosariusz.md#kod), czyli zapisanych w języku programowania instrukcji programu, to tylko część tej pracy.

[Weźmy czworo znajomych z wyjazdu](#lm-2), którzy męczą się z rozliczaniem wydatków w arkuszu. Ktoś musi ustalić, czego naprawdę potrzebują: czy program ma tylko wyliczyć, kto komu ile oddaje, czy też pamiętać kolejne wyjazdy. Potem opisuje rozwiązanie krok po kroku, zapisuje je w języku programowania, sprawdza na kilku przykładach i poprawia błędy.

```text
potrzeba --> ustalenie, co program ma robić --> kroki --> kod --> sprawdzanie --> poprawki
```

Programista sporo czasu spędza więc na rozmowie, myśleniu, czytaniu cudzego kodu i szukaniu przyczyn błędów. Rzadko zaczyna od pustej strony, często rozwija program, który już istnieje.

Nie trzeba być programistą z zawodu, żeby programować. Osoba spoza IT, która napisze mały program do własnych rozliczeń, wykonuje tę samą pracę, tylko na mniejszą skalę.

<a id="ref-3"></a>[Na razie nie piszemy kodu](03%20Napisz%20i%20uruchom%20kod.md#ref-35). Ten problem z wydatkami będzie jednak przykładem, który będzie nam towarzyszył: <a id="ref-2"></a>program „Wspólna Kasa” zbudujemy razem, a ty przećwiczysz w tej roli.

## Poznaj język programowania

Język programowania to <a id="ref-5"></a>ściśle określony sposób zapisywania instrukcji, który potrafi zrozumieć komputer. Ma własne słowa i reguły zapisu, ale jest o wiele prostszy i bardziej rygorystyczny niż język polski.

Komputer nie wyciąga wniosków z kontekstu. Zdanie „podziel rachunek po równo” człowiek zrozumie od razu, komputer nie. Język programowania wymusza zapis, który ma jedno znaczenie. Zbiór jego reguł nazywamy [składnią](00%20Glosariusz.md#składnia): mówi ona, jak wolno układać słowa i znaki, żeby powstało poprawne polecenie.

Oto jedna instrukcja w Pythonie, [języku, którego użyjemy w tym tutorialu](03%20Napisz%20i%20uruchom%20kod.md#ref-16):

```python
print("Cześć, Wspólna Kasa!")
```

```text
Cześć, Wspólna Kasa!
```

Słowo `print` znaczy „wypisz”, a tekst w cudzysłowie to to, co ma się pojawić na ekranie. Gdybyś pominął jeden cudzysłów, komputer odmówiłby wykonania polecenia, bo zapis łamie reguły.

Języków jest bardzo wiele, a każdy ma inną składnię i inne zastosowania. Różnią się zapisem, ale robią to samo: pozwalają opisać kroki, które komputer wykona. Kto pozna zasady jednego, łatwiej nauczy się następnych.

[Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#ref-28).

_Wersje: Python 3.13 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#01-wejdź-w-świat-programowania)_

> **Z przymrużeniem oka:** W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyka, w której literówka kończy rozmowę.

## Podawaj komputerowi każdy szczegół

Komputer potrzebuje precyzyjnych instrukcji, bo nie rozumie intencji, tylko wykonuje dokładnie to, co zapisano. Człowiek dopowiada sobie brakujące szczegóły, komputer ich nie zna i niczego nie zgaduje.

[Wróćmy do czworga znajomych na wyjeździe](#lm-2). Polecenie „podziel rachunek po równo” dla nich jest jasne. Dla komputera brakuje w nim niemal wszystkiego:

| Człowiek rozumie | Komputer musi dostać |
|---|---|
| „rachunek” | które wydatki dodać i skąd je wziąć |
| „po równo” | przez ile osób dzielimy |
| „podziel” | co zrobić, gdy kwota nie dzieli się na równe części |
| (nic) | gdzie i w jakiej formie pokazać wynik |

Prosta lista kroków może wyglądać tak, ale jeszcze nie jest precyzyjna:

```text
1. Dodaj wszystkie wydatki.
2. Podziel sumę przez liczbę osób.
3. Wypisz wynik z dokładnością do grosza.
```

Nie wiadomo tu, skąd wziąć wydatki, ile jest osób ani kto dopłaci grosz, gdy kwota nie dzieli się równo. Precyzyjna wersja rozstrzyga to wprost:

<a id="lm-6"></a>

```text
1. Weź kwoty wydatków z listy wpisanej przez użytkownika.
2. Dodaj je do siebie.
3. Podziel sumę przez 4, bo tyle jest osób.
4. Zaokrąglij w dół do pełnych groszy.
5. Resztę groszy dopisz pierwszej osobie.
6. Wypisz wynik na ekranie.
```

Komputer wykona takie kroki tysiące razy bez zmęczenia, ale też bez zdrowego rozsądku. Jeśli podasz złą liczbę osób, pomyli się z pełną pewnością siebie.

Konsekwencja jest praktyczna: precyzja to zadanie programisty. To on ustala, co dokładnie ma się stać, i dlatego w pracy nad programem tyle miejsca zajmuje sprawdzanie i poprawianie.

> **Wtręt:** Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił sumę na trzy z całkowitym spokojem, a każdy współlokator dostał rachunek wyższy, niż powinien. Błąd wyszedł na jaw dopiero wtedy, gdy ktoś zapytał, dlaczego za zakupy ma zapłacić tyle.

## Odróżnij program od aplikacji

Program to ciąg instrukcji, które komputer wykonuje. [Aplikacja](00%20Glosariusz.md#aplikacja) to program (albo zestaw programów) przygotowany tak, by zwykły użytkownik mógł z niego wygodnie korzystać: z oknem, przyciskami, zapisem danych i instrukcją obsługi. Każda aplikacja jest więc programem, ale nie każdy program jest aplikacją.

Różnica dotyczy głównie tego, dla kogo coś powstało. Program może być krótkim skryptem napisanym dla siebie, który robi jedną rzecz i nie ma żadnej oprawy. Aplikacja musi jeszcze radzić sobie z pomyłkami użytkownika, zapamiętywać jego dane i być zrozumiała bez znajomości kodu.

| | Program | Aplikacja |
|---|---|---|
| Dla kogo | często dla autora | dla wielu użytkowników |
| Wygląd | może być sam tekst w terminalu | okna, przyciski, menu |
| Obsługa błędów | minimalna | przewidziane komunikaty i pomoc |
| Przykład | kilka linii liczących rachunek | arkusz kalkulacyjny, aplikacja bankowa |

W praktyce granica jest płynna, a w mowie potocznej oba słowa często zamienia się miejscami. Ważne, by rozumieć, że wokół samych instrukcji można dobudować wiele warstw wygody.

<a id="ref-7"></a>[„Wspólna Kasa”, przykład, który będzie nam towarzyszył](#lm-2), <a id="lm-7"></a>zacznie jako mały program: wczyta wydatki i wypisze, kto komu ile jest winien. Nie będzie miała okna ani przycisków. Dopiero dobudowana oprawa ([pytania do użytkownika](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#ref-13), [sprawdzanie danych](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#ref-14)) przybliży ją do aplikacji.

Konsekwencja: zaczynamy od programu, bo to on jest rdzeniem. Oprawę dodaje się później, gdy rdzeń działa.

## Co zapamiętać

- Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
- Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.
- Programista zamienia potrzebę na działający program, a pisanie kodu to tylko jeden z etapów tej pracy.
- Język programowania to ścisły zestaw słów i reguł zapisu, dzięki któremu człowiek wyraża instrukcje tak, by komputer wykonał je jednoznacznie.
- Komputer wykonuje dokładnie to, co zapisano, więc każdy szczegół, który człowiek by sobie dopowiedział, trzeba podać wprost.
- Aplikacja to program z oprawą dla użytkownika, więc każda aplikacja jest programem, ale nie odwrotnie.

## Pytania sprawdzające

### 1. Czym jest program komputerowy?

<details>
<summary>Odpowiedź</summary>

Program komputerowy to zapisany z góry ciąg instrukcji, które komputer wykonuje krok po kroku, aby zamienić dane wejściowe na wynik. Komputer robi tylko to, co mu zapisano, i nic ponad to. Raz napisany program można uruchamiać wielokrotnie, dla różnych danych.

Zobacz: [sekcja „Zrozum, czym jest program”](#zrozum-czym-jest-program).

</details>

### 2. Czym jest programowanie?

<details>
<summary>Odpowiedź</summary>

Programowanie to tworzenie programów: zamienianie problemu na dokładny ciąg instrukcji, które komputer potrafi wykonać. Obejmuje zrozumienie problemu, rozbicie go na małe kroki, zapisanie ich w języku zrozumiałym dla komputera oraz sprawdzanie i poprawianie wyniku. Największa część pracy to myślenie o rozwiązaniu, a nie pisanie znaków.

Zobacz: [sekcja „Odkryj sens programowania”](#odkryj-sens-programowania).

</details>

### 3. Kim jest programista i czym się zajmuje?

<details>
<summary>Odpowiedź</summary>

Programista to osoba, która zamienia potrzebę opisaną zwykłymi słowami na instrukcje, które wykona komputer. Ustala, co program ma robić, opisuje rozwiązanie krok po kroku, zapisuje je w kodzie, sprawdza i poprawia. Sporo czasu poświęca na myślenie, rozmowy i szukanie błędów, a nie tylko na pisanie.

Zobacz: [sekcja „Przyjrzyj się pracy programisty”](#przyjrzyj-się-pracy-programisty).

</details>

### 4. Czym jest język programowania?

<details>
<summary>Odpowiedź</summary>

Język programowania to ściśle określony sposób zapisywania instrukcji, który zrozumie i wykona komputer. Ma ustalone słowa i reguły zapisu, więc nie zostawia miejsca na domysły, jak zwykły język. Dzięki temu człowiek pisze polecenia w czytelnej formie, a komputer wykonuje je jednoznacznie.

Zobacz: [sekcja „Poznaj język programowania”](#poznaj-język-programowania).

</details>

### 5. Dlaczego komputer potrzebuje precyzyjnych instrukcji?

<details>
<summary>Odpowiedź</summary>

Komputer nie rozumie intencji ani kontekstu, więc wykonuje tylko to, co zapisano, i niczego nie zgaduje. Każdy szczegół, który człowiek dopowiada sobie sam, trzeba dla komputera zapisać wprost. Precyzję zapewnia programista, a błędy w instrukcjach komputer wykona równie sumiennie jak poprawne.

Zobacz: [sekcja „Podawaj komputerowi każdy szczegół”](#podawaj-komputerowi-każdy-szczegół).

</details>

### 6. Czym różni się program od aplikacji?

<details>
<summary>Odpowiedź</summary>

Program to ciąg instrukcji wykonywanych przez komputer, a aplikacja to program przygotowany dla użytkownika: z wygodną obsługą, obsługą błędów i zapisem danych. Każda aplikacja jest programem, ale nie każdy program jest aplikacją. Granica jest płynna, bo chodzi głównie o to, ile oprawy dla użytkownika dobudowano wokół samych instrukcji.

Zobacz: [sekcja „Odróżnij program od aplikacji”](#odróżnij-program-od-aplikacji).

</details>
