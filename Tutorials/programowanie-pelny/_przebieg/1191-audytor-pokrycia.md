# Krok 1191 · audytor_pokrycia

Węzeł: `coverage` · dział: 6 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 32. Czym jest pętla?
  odpowiedź: Pętla to instrukcja, która powtarza ten sam fragment kodu wiele razy. Jedno wykonanie nazywamy iteracją. Pętla `for` powtarza wcięte ciało dla każdego elementu zestawu danych i kończy się, gdy elementy się skończą.
  sekcje pisarza: sec-06-czym-jest-petla
- 33. Kiedy warto użyć pętli zamiast pisać to samo wiele razy?
  odpowiedź: Pętli warto użyć, gdy ta sama czynność dotyczy wielu elementów albo gdy liczba powtórzeń zależy od danych. Jeśli kopiujesz linię i zmieniasz w niej tylko jedną wartość, pętla skróci kod i ułatwi jego poprawianie. Zwykłe linie wystarczą, gdy czynność wykonujesz raz albo każdy krok jest inny.
  sekcje pisarza: sec-06-kiedy-siegnac-po-petle
- 34. Czym jest pętla nieskończona i dlaczego jest problemem?
  odpowiedź: Pętla nieskończona to pętla, której warunek zakończenia nigdy się nie spełnia, więc program powtarza ją bez końca. Jest problemem, bo program wygląda na zawieszony, zajmuje procesor i nigdy nie dochodzi do wyniku. Można ją przerwać z terminala skrótem Ctrl+C, ale lepiej od początku zadbać, by warunek kiedyś stał się fałszywy.
  sekcje pisarza: sec-06-petla-nieskonczona
- 35. Czym jest lista danych?
  odpowiedź: Lista danych to jedna zmienna przechowująca wiele wartości w ustalonej kolejności. Zapisujesz ją w nawiasach kwadratowych, oddzielając elementy przecinkami. Może mieć dowolną długość, także zero elementów, a jej rozmiar podaje funkcja len().
  sekcje pisarza: sec-06-czym-jest-lista-danych
- 36. Jak odczytać konkretny element listy?
  odpowiedź: Element listy odczytujesz przez jego numer, czyli indeks, w nawiasach kwadratowych, np. `osoby[0]`. Numeracja zaczyna się od zera, a ujemne indeksy liczą od końca (`-1` to ostatni element). Indeks spoza listy powoduje błąd `IndexError`.
  sekcje pisarza: sec-06-odczyt-elementu-listy
- 37. Jak przejść przez wszystkie elementy listy?
  odpowiedź: Użyj pętli `for`, np. `for imie in osoby:`. Python bierze po kolei każdy element listy, wykonuje dla niego wcięty blok i sam kończy, gdy elementy się skończą. Nie musisz liczyć indeksów ani znać długości listy.
  sekcje pisarza: sec-06-petla-po-elementach-listy

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-41: „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)
- ref-51: „U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika)
- ref-66: „w warsztacie poniżej dopisujesz do swojego skryptu linię” (zapowiedź warsztatu i skryptu, w którym czytelnik wywoła błąd TypeError)
- ref-75: „jej zapis omówimy osobno” (zapis listy danych w nawiasach kwadratowych); ma ją spełnić pytanie 35
- ref-79: „Pętlę, która nigdy się nie kończy, omówimy w następnej kolejności” (pętla nieskończona); ma ją spełnić pytanie 34
- ref-83: „Jak sięgnąć po jeden element, omówimy osobno” (odczyt konkretnego elementu listy); ma ją spełnić pytanie 36
- ref-84: „przy przechodzeniu przez wszystkie elementy” (pętla po wszystkich elementach listy); ma ją spełnić pytanie 37

SEKCJE DZIAŁU 06 "Powtarzanie i kolekcje":
[sec-06-czym-jest-petla] ## Czym jest pętla
[[petla|Pętla]] to instrukcja, która każe programowi wykonać ten sam fragment kodu wielokrotnie. Zamiast pisać tę samą linię trzy razy, zapisujesz ją raz i mówisz, ile razy albo dla czego ją powtórzyć.

Jedno powtórzenie fragmentu nazywamy [[iteracja|iteracją]]. Pętla `for` wykonuje po jednej iteracji dla każdego elementu z zestawu danych. Taki zestaw to na razie po prostu lista wartości w nawiasach kwadratowych; jej zapis omówimy osobno.

Wcięte linie pod `for` to ciało pętli, tak samo jak przy `if`. Nazwa po słowie `for` to zmienna, która w każdej iteracji dostaje kolejny element:

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print("Cześć,", imie)
print("Koniec")
```

```text
Cześć, Ania
Cześć, Bartek
Cześć, Celina
Koniec
```

Ciało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. Ostatni `print` nie ma wcięcia, więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.

Pętla ma więc początek, powtarzane kroki i koniec, a koniec wynika z [[warunek-zakonczenia|warunku zakończenia]]: w `for` jest nim wyczerpanie elementów. W „Wspólnej Kasie” dzięki temu jeden zapis obsłuży trzy osoby, ale też trzydzieści.

[sec-06-kiedy-siegnac-po-petle] ## Kiedy sięgnąć po pętlę
Pętli warto użyć, gdy ta sama czynność dotyczy wielu elementów albo liczba powtórzeń zależy od danych. Jeśli kopiujesz linię i zmieniasz w niej tylko jedną wartość, to znak, że potrzebna jest [[petla|pętla]].

Powtarzanie ręczne ma dwie wady. Poprawkę trzeba wprowadzić w wielu miejscach, a przy każdej łatwo o pomyłkę. Poza tym taki kod nie dopasuje się do danych: napisany na trzy osoby nie obsłuży czwartej.

```python
osoby = ["Ania", "Bartek", "Celina"]
liczba_osob = 3
for imie in osoby:
    print(imie, "płaci", 300 / liczba_osob)
```

```text
Ania płaci 100.0
Bartek płaci 100.0
Celina płaci 100.0
```

Zmienia się tylko `imie`, więc reszta linii jest zapisana jeden raz. Poprawka wzoru to jedna zmiana zamiast trzech.

| Sytuacja | Rozwiązanie |
|---|---|
| Ta sama czynność dla każdego elementu zestawu | pętla |
| Liczba powtórzeń zależy od danych | pętla |
| Dwie różne czynności, każda raz | zwykłe linie |
| Pojedyncza czynność, która się nie powtarza | zwykła linia |

Pętla `for` ma z góry znany koniec. Pętlę, która nigdy się nie kończy, omówimy w następnej kolejności.

[sec-06-petla-nieskonczona] ## Pętla nieskończona
[[petla-nieskonczona|Pętla nieskończona]] to pętla, która nigdy nie dochodzi do końca, bo jej [[warunek-zakonczenia|warunek zakończenia]] nigdy nie zostaje spełniony. Program powtarza wtedy ten sam fragment bez końca, więc nie dociera do dalszych linii i nie oddaje wyniku.

Pętla `for`, którą znasz, kończy się sama, bo zestaw danych się wyczerpuje. Pętla `while` („dopóki”) działa inaczej: powtarza wcięte linie, dopóki warunek daje `True`. Jeśli warunek jest zawsze prawdziwy, każda kolejna [[iteracja|iteracja]] zaczyna się od nowa.

```python
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

Tu warunek to na stałe `True`, a w ciele nic go nie zmienia. Linia `time.sleep(1)` robi tylko jednosekundową przerwę, żeby napisy nie zalały ekranu. Zdarza się to też przez pomyłkę: warunek zależy od zmiennej, której pętla nigdy nie zmienia.

Problem jest praktyczny. Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków. Tak samo wyglądałaby „Wspólna Kasa”, która czeka na koniec listy, którego nie ma.

Zatrzymasz taki program skrótem Ctrl+C w terminalu. Python przerywa wtedy działanie i wypisuje komunikat `KeyboardInterrupt`, czyli „przerwano z klawiatury”. To nie awaria, tylko Twoja komenda.

Dlatego przy każdej pętli `while` zadaj sobie pytanie: co sprawi, że warunek w końcu stanie się fałszywy?

[sec-06-czym-jest-lista-danych] ## Czym jest lista danych
[[lista-danych|Lista danych]] to jedna zmienna, która przechowuje wiele wartości w ustalonej kolejności. Zamiast trzech zmiennych z imionami masz jedną nazwę, pod którą leży cały zestaw.

Właśnie po takim zestawie chodzi [[petla|pętla]] `for`: wcześniej szła po imionach uczestników, a teraz przyglądamy się samej liście.

Listę zapisujesz w nawiasach kwadratowych, a wartości oddzielasz przecinkami. Każda wartość to [[element-listy|element listy]], czyli jedno miejsce w zestawie. Tekst ma cudzysłów, liczba nie, tak samo jak przy zwykłych zmiennych.

```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby)
print(len(osoby))
```

```text
['Ania', 'Bartek', 'Celina']
3
```

Funkcja `len()` podaje długość listy, czyli liczbę elementów. Python wypisuje listę w nawiasach, a teksty w apostrofach; to tylko sposób wyświetlania.

Kolejność ma znaczenie: „Ania” jest pierwsza i tak zostaje. Lista może być też dłuższa albo pusta (`[]`), a program nie musi z góry znać jej rozmiaru. Dlatego pasuje do „Wspólnej Kasy”: `osoby` to uczestnicy wyjazdu, a `wydatki` to zapłacone rachunki, których przybywa.

Jak sięgnąć po jeden element, omówimy osobno. To, co lista daje pętli, zobaczysz przy przechodzeniu przez wszystkie elementy.

[sec-06-odczyt-elementu-listy] ## Odczyt elementu listy
Po element listy sięgasz przez jego numer w nawiasach kwadratowych: `osoby[0]`. Numer nazywa się [[indeks|indeksem]] i liczenie zaczyna się od zera, więc pierwszy element ma indeks 0, drugi 1, trzeci 2.

Wygląda to dziwnie, ale indeks mówi, o ile miejsc od początku listy się przesunąć. Pierwszy element jest na samym początku, więc przesunięcie wynosi zero. Kolejność zostaje taka, jak w sekcji Czym jest lista danych.

Ujemny indeks liczy od końca: `-1` to ostatni element, `-2` przedostatni. Jest wygodny, gdy nie wiesz, ile elementów ma lista.

```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby[0])
print(osoby[2])
print(osoby[-1])
```

```text
Ania
Celina
Celina
```

Indeks spoza listy kończy się błędem `IndexError`. Przy trzech osobach ostatni jest `osoby[2]`, a `osoby[3]` nie istnieje, więc program się zatrzyma. Największy poprawny indeks to `len(osoby) - 1`.

Odczyt niczego nie zmienia: lista zostaje taka sama, dostajesz tylko kopię wartości.

[sec-06-petla-po-elementach-listy] ## Pętla po elementach listy
Przez wszystkie elementy [[lista-danych|listy]] przechodzisz [[petla|pętlą]] `for`: `for imie in osoby:` bierze po kolei każdy [[element-listy|element]] i wykonuje dla niego wcięty blok.

Przy pierwszym przebiegu (czyli [[iteracja|iteracji]]) `imie` dostaje pierwszy element, przy drugim drugi, i tak do ostatniego. Gdy elementy się skończą, pętla sama przestaje, a program idzie dalej, do pierwszej linii bez wcięcia. Nie liczysz indeksów ani nie sprawdzasz długości listy.

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print(imie)
print("Koniec")
```

```text
Ania
Bartek
Celina
Koniec
```

Elementy przychodzą w kolejności listy, więc „Ania” jest pierwsza. Dodasz czwartą osobę, a ta sama pętla obsłuży ją bez zmian.

Pętla może też coś zbierać. Przy liście `wydatki` dodaje kwotę każdego wydatku do sumy; zapis `wydatek["kwota"]` bierze z jednego wydatku pole `kwota`:

```python
wydatki = ...
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(suma)
```

Suma zaczyna od zera, rośnie w każdej iteracji, a wynik pokazujesz dopiero po pętli, już bez wcięcia.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 32,
      "status": "covered",
      "section_ids": [
        "sec-06-czym-jest-petla"
      ],
      "explanation": "Definicja pętli, iteracji, ciała i zakończenia pętli for wraz z przykładem i wyjaśnieniem wcięcia."
    },
    {
      "question_id": 33,
      "status": "covered",
      "section_ids": [
        "sec-06-kiedy-siegnac-po-petle"
      ],
      "explanation": "Podane kryteria, wady ręcznego powtarzania, przykład oraz tabela wskazująca, kiedy wystarczą zwykłe linie."
    },
    {
      "question_id": 34,
      "status": "covered",
      "section_ids": [
        "sec-06-petla-nieskonczona"
      ],
      "explanation": "Definicja, przykład while True, przyczyny, skutki (zawieszenie, procesor), przerwanie Ctrl+C i pytanie kontrolne o warunek."
    },
    {
      "question_id": 35,
      "status": "covered",
      "section_ids": [
        "sec-06-czym-jest-lista-danych"
      ],
      "explanation": "Wyjaśnia listę jako jedną zmienną z wieloma wartościami w kolejności, zapis w nawiasach, pustą listę i len()."
    },
    {
      "question_id": 36,
      "status": "covered",
      "section_ids": [
        "sec-06-odczyt-elementu-listy"
      ],
      "explanation": "Indeks od zera, ujemne indeksy, przykład oraz IndexError z uzasadnieniem i największym poprawnym indeksem."
    },
    {
      "question_id": 37,
      "status": "covered",
      "section_ids": [
        "sec-06-petla-po-elementach-listy"
      ],
      "explanation": "Pętla for po liście, kolejność, samoczynne zakończenie, brak potrzeby indeksów, przykład i zbieranie sumy."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-16",
      "status": "brak",
      "explanation": "Ta zapowiedź nie jest tu rozliczana; dział zawiera już kod, ale sekcje nie odnoszą się do niej."
    },
    {
      "reference_id": "ref-41",
      "status": "brak",
      "explanation": "Żadna sekcja działu nie prowadzi czytelnika do kasa.py z komunikatem o błędzie."
    },
    {
      "reference_id": "ref-51",
      "status": "brak",
      "explanation": "Brak TypeError w działe 06; obietnica niespełniona."
    },
    {
      "reference_id": "ref-66",
      "status": "brak",
      "explanation": "Brak warsztatu z dopisaniem linii wywołującej TypeError w tym dziale."
    },
    {
      "reference_id": "ref-75",
      "status": "spełniona",
      "section_id": "sec-06-czym-jest-lista-danych",
      "quote": "Listę zapisujesz w nawiasach kwadratowych, a wartości oddzielasz przecinkami.",
      "explanation": "Zapis listy omówiony."
    },
    {
      "reference_id": "ref-79",
      "status": "spełniona",
      "section_id": "sec-06-petla-nieskonczona",
      "quote": "Pętla nieskończona to pętla, która nigdy nie dochodzi do końca",
      "explanation": "Pętla nieskończona omówiona."
    },
    {
      "reference_id": "ref-83",
      "status": "spełniona",
      "section_id": "sec-06-odczyt-elementu-listy",
      "quote": "Po element listy sięgasz przez jego numer w nawiasach kwadratowych",
      "explanation": "Odczyt elementu omówiony."
    },
    {
      "reference_id": "ref-84",
      "status": "spełniona",
      "section_id": "sec-06-petla-po-elementach-listy",
      "quote": "Przez wszystkie elementy listy przechodzisz pętlą for",
      "explanation": "Przechodzenie przez wszystkie elementy omówione."
    }
  ]
}
````
