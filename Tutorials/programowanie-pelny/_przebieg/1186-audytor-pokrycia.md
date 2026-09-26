# Krok 1186 · audytor_pokrycia

Węzeł: `coverage` · dział: 1 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 1. Czym jest program komputerowy?
  odpowiedź: Program komputerowy to zapisany z góry ciąg instrukcji, które komputer wykonuje krok po kroku, aby zamienić dane wejściowe na wynik. Komputer robi tylko to, co mu zapisano, i nic ponad to. Raz napisany program można uruchamiać wielokrotnie, dla różnych danych.
  sekcje pisarza: sec-01-czym-jest-program-komputerowy
- 2. Czym jest programowanie?
  odpowiedź: Programowanie to tworzenie programów: zamienianie problemu na dokładny ciąg instrukcji, które komputer potrafi wykonać. Obejmuje zrozumienie problemu, rozbicie go na małe kroki, zapisanie ich w języku zrozumiałym dla komputera oraz sprawdzanie i poprawianie wyniku. Największa część pracy to myślenie o rozwiązaniu, a nie pisanie znaków.
  sekcje pisarza: sec-01-czym-jest-programowanie
- 3. Kim jest programista i czym się zajmuje?
  odpowiedź: Programista to osoba, która zamienia potrzebę opisaną zwykłymi słowami na instrukcje, które wykona komputer. Ustala, co program ma robić, opisuje rozwiązanie krok po kroku, zapisuje je w kodzie, sprawdza i poprawia. Sporo czasu poświęca na myślenie, rozmowy i szukanie błędów, a nie tylko na pisanie.
  sekcje pisarza: sec-01-kim-jest-programista
- 4. Czym jest język programowania?
  odpowiedź: Język programowania to ściśle określony sposób zapisywania instrukcji, który zrozumie i wykona komputer. Ma ustalone słowa i reguły zapisu, więc nie zostawia miejsca na domysły, jak zwykły język. Dzięki temu człowiek pisze polecenia w czytelnej formie, a komputer wykonuje je jednoznacznie.
  sekcje pisarza: sec-01-czym-jest-jezyk-programowania
- 5. Dlaczego komputer potrzebuje precyzyjnych instrukcji?
  odpowiedź: Komputer nie rozumie intencji ani kontekstu, więc wykonuje tylko to, co zapisano, i niczego nie zgaduje. Każdy szczegół, który człowiek dopowiada sobie sam, trzeba dla komputera zapisać wprost. Precyzję zapewnia programista, a błędy w instrukcjach komputer wykona równie sumiennie jak poprawne.
  sekcje pisarza: sec-01-po-co-komputerowi-precyzja
- 6. Czym różni się program od aplikacji?
  odpowiedź: Program to ciąg instrukcji wykonywanych przez komputer, a aplikacja to program przygotowany dla użytkownika: z wygodną obsługą, obsługą błędów i zapisem danych. Każda aplikacja jest programem, ale nie każdy program jest aplikacją. Granica jest płynna, bo chodzi głównie o to, ile oprawy dla użytkownika dobudowano wokół samych instrukcji.
  sekcje pisarza: sec-01-program-a-aplikacja

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-1: „osoba, która zamienia potrzebę na instrukcje” (rola programisty, omówiona później); ma ją spełnić pytanie 3
- ref-2: „przykład, który będzie nam towarzyszył” (zapowiedź, że „Wspólna Kasa” wróci w kolejnych działach)
- ref-3: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się później)
- ref-5: „Tym językiem zajmiemy się osobno” (język programowania); ma ją spełnić pytanie 4
- ref-7: „przykładem, który będzie nam towarzyszył” (Wspólna Kasa jako przykład wracający w kolejnych działach)
- ref-8: „Na razie nie piszemy kodu” (kod pojawi się w dalszych działach)
- ref-9: „języku, którego użyjemy w tym tutorialu” (Python jako język tutorialu)
- ref-10: „Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”” (Python i budowa programu „Wspólna Kasa” omówione później)

SEKCJE DZIAŁU 01 "Czym jest programowanie":
[sec-01-czym-jest-program-komputerowy] ## Czym jest program komputerowy
[[program-komputerowy|Program komputerowy]] to zapisany z góry ciąg poleceń, które komputer wykonuje krok po kroku, żeby zamienić dane na wynik. Komputer sam nic nie wie ani nie zgaduje: robi dokładnie to, co mu zapisano.

Pojedyncze polecenie to [[instrukcja|instrukcja]], czyli jeden mały, jednoznaczny krok, np. „dodaj dwie liczby” albo „wypisz tekst na ekranie”. Program to wiele takich instrukcji ułożonych w określonej kolejności. Kalkulator, przeglądarka i gra działają tak samo, tylko mają instrukcji bardzo dużo.

Prosty schemat każdego programu wygląda tak:

```text
dane na wejściu  -->  program (instrukcje)  -->  wynik na wyjściu
```

Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

Program „Wspólna Kasa” zrobi to za ciebie. Na wejściu dostanie listę wydatków (kto zapłacił i ile), a na wyjściu poda rozliczenie. Napisze go [[programista|programista]], czyli osoba, która zamienia potrzebę na instrukcje zrozumiałe dla komputera. Na razie nie piszemy kodu; ważne, że raz zapisane instrukcje można uruchamiać bez końca.

[sec-01-czym-jest-programowanie] ## Czym jest programowanie
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

[sec-01-kim-jest-programista] ## Kim jest programista
[[programista|Programista]] to osoba, która zamienia potrzebę na instrukcje: bierze problem opisany zwykłymi słowami i tworzy program, który go rozwiązuje. Pisanie [[kod|kodu]], czyli zapisanych w języku programowania instrukcji programu, to tylko część tej pracy.

Weźmy czworo znajomych z wyjazdu, którzy męczą się z rozliczaniem wydatków w arkuszu. Ktoś musi ustalić, czego naprawdę potrzebują: czy program ma tylko wyliczyć, kto komu ile oddaje, czy też pamiętać kolejne wyjazdy. Potem opisuje rozwiązanie krok po kroku, zapisuje je w języku programowania, sprawdza na kilku przykładach i poprawia błędy.

```text
potrzeba --> ustalenie, co program ma robić --> kroki --> kod --> sprawdzanie --> poprawki
```

Programista sporo czasu spędza więc na rozmowie, myśleniu, czytaniu cudzego kodu i szukaniu przyczyn błędów. Rzadko zaczyna od pustej strony, często rozwija program, który już istnieje.

Nie trzeba być programistą z zawodu, żeby programować. Osoba spoza IT, która napisze mały program do własnych rozliczeń, wykonuje tę samą pracę, tylko na mniejszą skalę.

Na razie nie piszemy kodu. Ten problem z wydatkami będzie jednak przykładem, który będzie nam towarzyszył: program „Wspólna Kasa” zbudujemy razem, a ty przećwiczysz w tej roli.

[sec-01-czym-jest-jezyk-programowania] ## Czym jest język programowania
[[jezyk-programowania|Język programowania]] to ściśle określony sposób zapisywania [[instrukcja|instrukcji]], który potrafi zrozumieć komputer. Ma własne słowa i reguły zapisu, ale jest o wiele prostszy i bardziej rygorystyczny niż język polski.

Komputer nie wyciąga wniosków z kontekstu. Zdanie „podziel rachunek po równo” człowiek zrozumie od razu, komputer nie. Język programowania wymusza zapis, który ma jedno znaczenie. Zbiór jego reguł nazywamy [[skladnia|składnią]]: mówi ona, jak wolno układać słowa i znaki, żeby powstało poprawne polecenie.

Oto jedna instrukcja w Pythonie, języku, którego użyjemy w tym tutorialu:

```python
print("Cześć, Wspólna Kasa!")
```

```text
Cześć, Wspólna Kasa!
```

Słowo `print` znaczy „wypisz”, a tekst w cudzysłowie to to, co ma się pojawić na ekranie. Gdybyś pominął jeden cudzysłów, komputer odmówiłby wykonania polecenia, bo zapis łamie reguły.

Języków jest bardzo wiele, a każdy ma inną składnię i inne zastosowania. Różnią się zapisem, ale robią to samo: pozwalają opisać kroki, które komputer wykona. Kto pozna zasady jednego, łatwiej nauczy się następnych.

Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”.

[sec-01-po-co-komputerowi-precyzja] ## Po co komputerowi precyzja
Komputer potrzebuje precyzyjnych [[instrukcja|instrukcji]], bo nie rozumie intencji, tylko wykonuje dokładnie to, co zapisano. Człowiek dopowiada sobie brakujące szczegóły, komputer ich nie zna i niczego nie zgaduje.

Wróćmy do czworga znajomych na wyjeździe. Polecenie „podziel rachunek po równo” dla nich jest jasne. Dla komputera brakuje w nim niemal wszystkiego:

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

[sec-01-program-a-aplikacja] ## Program a aplikacja
Program to ciąg instrukcji, które komputer wykonuje. [[aplikacja|Aplikacja]] to program (albo zestaw programów) przygotowany tak, by zwykły użytkownik mógł z niego wygodnie korzystać: z oknem, przyciskami, zapisem danych i instrukcją obsługi. Każda aplikacja jest więc programem, ale nie każdy program jest aplikacją.

Różnica dotyczy głównie tego, dla kogo coś powstało. Program może być krótkim skryptem napisanym dla siebie, który robi jedną rzecz i nie ma żadnej oprawy. Aplikacja musi jeszcze radzić sobie z pomyłkami użytkownika, zapamiętywać jego dane i być zrozumiała bez znajomości kodu.

| | Program | Aplikacja |
|---|---|---|
| Dla kogo | często dla autora | dla wielu użytkowników |
| Wygląd | może być sam tekst w terminalu | okna, przyciski, menu |
| Obsługa błędów | minimalna | przewidziane komunikaty i pomoc |
| Przykład | kilka linii liczących rachunek | arkusz kalkulacyjny, aplikacja bankowa |

W praktyce granica jest płynna, a w mowie potocznej oba słowa często zamienia się miejscami. Ważne, by rozumieć, że wokół samych instrukcji można dobudować wiele warstw wygody.

„Wspólna Kasa”, przykład, który będzie nam towarzyszył, zacznie jako mały program: wczyta wydatki i wypisze, kto komu ile jest winien. Nie będzie miała okna ani przycisków. Dopiero dobudowana oprawa (pytania do użytkownika, sprawdzanie danych) przybliży ją do aplikacji.

Konsekwencja: zaczynamy od programu, bo to on jest rdzeniem. Oprawę dodaje się później, gdy rdzeń działa.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 1,
      "status": "covered",
      "section_ids": [
        "sec-01-czym-jest-program-komputerowy"
      ],
      "explanation": "Sekcja definiuje program jako z góry zapisany ciąg poleceń, pokazuje schemat wejście-program-wyjście, mówi że komputer robi tylko to, co zapisano, i że program można uruchamiać wielokrotnie."
    },
    {
      "question_id": 2,
      "status": "covered",
      "section_ids": [
        "sec-01-czym-jest-programowanie"
      ],
      "explanation": "Definicja, etapy (problem, kroki, zapis, uruchomienie, poprawki), pętla poprawek i stwierdzenie, że najwięcej pracy to wymyślenie rozwiązania."
    },
    {
      "question_id": 3,
      "status": "covered",
      "section_ids": [
        "sec-01-kim-jest-programista"
      ],
      "explanation": "Opisuje rolę programisty, jego czynności (ustalenie potrzeb, kroki, kod, sprawdzanie) oraz że sporo czasu zajmuje rozmowa, myślenie i szukanie błędów."
    },
    {
      "question_id": 4,
      "status": "covered",
      "section_ids": [
        "sec-01-czym-jest-jezyk-programowania"
      ],
      "explanation": "Definicja, słowa i reguły (składnia), jednoznaczność wobec języka naturalnego, przykład w Pythonie i wyjaśnienie, że błąd składni uniemożliwia wykonanie."
    },
    {
      "question_id": 5,
      "status": "covered",
      "section_ids": [
        "sec-01-po-co-komputerowi-precyzja"
      ],
      "explanation": "Wyjaśnia, że komputer nie rozumie intencji, pokazuje tabelę brakujących szczegółów, wersję nieprecyzyjną i precyzyjną oraz że precyzja to zadanie programisty, a błędy są wykonywane pewnie."
    },
    {
      "question_id": 6,
      "status": "covered",
      "section_ids": [
        "sec-01-program-a-aplikacja"
      ],
      "explanation": "Definiuje oba pojęcia, wskazuje różnicę (dla kogo, oprawa, obsługa błędów), tabelę, zależność 'każda aplikacja jest programem' i płynną granicę."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-1",
      "status": "spełniona",
      "section_id": "sec-01-kim-jest-programista",
      "quote": "osoba, która zamienia potrzebę na instrukcje: bierze problem opisany zwykłymi słowami",
      "explanation": "Rola programisty omówiona w pełni."
    },
    {
      "reference_id": "ref-2",
      "status": "spełniona",
      "section_id": "sec-01-kim-jest-programista",
      "quote": "program „Wspólna Kasa” zbudujemy razem, a ty przećwiczysz w tej roli",
      "explanation": "Zapowiedź, że Wspólna Kasa wróci; dodatkowo sec-01-program-a-aplikacja opisuje jej początkową postać."
    },
    {
      "reference_id": "ref-3",
      "status": "spełniona",
      "section_id": "sec-01-kim-jest-programista",
      "quote": "Na razie nie piszemy kodu.",
      "explanation": "Zapowiedź kodu później; w dziale jest tylko jedna instrukcja print jako ilustracja, a pisanie zapowiedziano na dalsze działy."
    },
    {
      "reference_id": "ref-5",
      "status": "spełniona",
      "section_id": "sec-01-czym-jest-jezyk-programowania",
      "quote": "ściśle określony sposób zapisywania instrukcji, który potrafi zrozumieć komputer",
      "explanation": "Pytanie 4 wyjaśnia język programowania."
    },
    {
      "reference_id": "ref-7",
      "status": "spełniona",
      "section_id": "sec-01-program-a-aplikacja",
      "quote": "„Wspólna Kasa”, przykład, który będzie nam towarzyszył, zacznie jako mały program",
      "explanation": "Przykład jest rozwijany i zapowiedziany na kolejne działy."
    },
    {
      "reference_id": "ref-8",
      "status": "spełniona",
      "section_id": "sec-01-kim-jest-programista",
      "quote": "Na razie nie piszemy kodu.",
      "explanation": "Zapowiedź, że kod pojawi się później, wraz ze zbudowaniem programu razem."
    },
    {
      "reference_id": "ref-9",
      "status": "spełniona",
      "section_id": "sec-01-czym-jest-jezyk-programowania",
      "quote": "Oto jedna instrukcja w Pythonie, języku, którego użyjemy w tym tutorialu",
      "explanation": "Python wskazany jako język tutorialu, z przykładem."
    },
    {
      "reference_id": "ref-10",
      "status": "spełniona",
      "section_id": "sec-01-czym-jest-jezyk-programowania",
      "quote": "Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”.",
      "explanation": "Wprost zapowiada późniejsze omówienie Pythona przy budowie programu."
    }
  ]
}
````
