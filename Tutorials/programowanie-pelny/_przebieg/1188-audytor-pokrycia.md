# Krok 1188 · audytor_pokrycia

Węzeł: `coverage` · dział: 3 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 13. Czym jest kod źródłowy?
  odpowiedź: Kod źródłowy to tekst programu zapisany w języku programowania, czytelny dla człowieka. Jest zwykłym plikiem tekstowym, w którym każda linia to instrukcja zapisana według reguł składni. Komputer nie wykonuje go bezpośrednio, tylko czyta go osobny program. Programista tworzy i poprawia właśnie kod źródłowy.
  sekcje pisarza: sec-03-czym-jest-kod-zrodlowy
- 14. Do czego służy edytor kodu?
  odpowiedź: Edytor kodu służy do pisania i poprawiania kodu źródłowego. Podświetla składnię, numeruje linie, pilnuje wcięć i nawiasów oraz podpowiada nazwy, dzięki czemu łatwiej zauważyć pomyłki. Sam kodu nie uruchamia, a zapisany plik jest zwykłym tekstem, który otworzysz w każdym innym programie.
  sekcje pisarza: sec-03-do-czego-sluzy-edytor
- 15. Co to znaczy uruchomić program?
  odpowiedź: Uruchomić program znaczy polecić komputerowi, by wykonał instrukcje z pliku po kolei, od pierwszej do ostatniej. Robi to inny program, w naszym przypadku Python, któremu podajemy nazwę pliku w terminalu. Samo uruchomienie nie zmienia pliku, więc można je powtarzać po każdej poprawce.
  sekcje pisarza: sec-03-co-znaczy-uruchomic-program
- 16. Czym jest kompilator lub interpreter?
  odpowiedź: Kompilator i interpreter to programy, które zamieniają kod źródłowy na działanie komputera. Kompilator tłumaczy cały program naraz na osobny plik gotowy do uruchomienia. Interpreter czyta kod i wykonuje go na bieżąco, bez osobnego pliku. Python jest używany jako interpreter, więc po zmianie kodu wystarczy zapisać plik i uruchomić go ponownie.
  sekcje pisarza: sec-03-kompilator-i-interpreter
- 17. Co to jest błąd w programie?
  odpowiedź: Błąd w programie to miejsce, w którym program robi coś innego, niż zamierzał autor. Czasem program zatrzymuje się z komunikatem, np. przez literówkę w nazwie polecenia. Czasem działa do końca, ale daje zły wynik, bo zapis instrukcji był nieprawidłowy. Komputer wykonuje to, co napisano, nie to, co miano na myśli.
  sekcje pisarza: sec-03-co-to-jest-blad-w-programie
- 18. Do czego służą komentarze w kodzie?
  odpowiedź: Komentarze to notatki w kodzie przeznaczone dla człowieka: interpreter ich pomija. Wyjaśniają, dlaczego coś jest napisane, oraz pozwalają czasowo wyłączyć instrukcję. Trzeba je aktualizować razem z kodem, bo nieaktualny komentarz wprowadza w błąd.
  sekcje pisarza: sec-03-do-czego-sluza-komentarze

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-19: „Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”” (zapowiedź, że Wspólna Kasa wraca w kolejnych działach)
- ref-24: „przykład, który będzie nam towarzyszył” (Wspólna Kasa wraca w kolejnych działach)
- ref-25: „dostanie z niego kod dopiero później” (kod Wspólnej Kasy pojawi się w dalszych działach)
- ref-30: „przykład, który będzie nam towarzyszył w kolejnych działach” (Wspólna Kasa wraca w kolejnych działach)
- ref-34: „jak to działa, pokażemy przy uruchamianiu programu” (czytanie i wykonywanie pliku z kodem przez osobny program); ma ją spełnić pytanie 15
- ref-35: „nasz przykład, który będzie nam towarzyszył” (Wspólna Kasa jako przykład wracający w kolejnych działach)
- ref-37: „gdy wyjaśnimy, co to znaczy uruchomić program” (uruchamianie programu); ma ją spełnić pytanie 15
- ref-38: „wyjaśnimy w następnej części” (czym jest wykonawca kodu i czym różni się od kompilatora); ma ją spełnić pytanie 16
- ref-41: „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)

SEKCJE DZIAŁU 03 "Kod i jego uruchamianie":
[sec-03-czym-jest-kod-zrodlowy] ## Czym jest kod źródłowy
[[kod-zrodlowy|Kod źródłowy]] to tekst programu zapisany w [[jezyk-programowania|języku programowania]], który czyta i pisze człowiek. To „źródło”, z którego komputer dopiero dostaje coś do wykonania.

Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to [[instrukcja|instrukcja]] zapisana według ścisłych reguł [[skladnia|składni]]. Ten sam [[algorytm|algorytm]], który wcześniej opisywaliśmy słowami i schematem, tu dostaje zapis, którego nie da się zrozumieć na dwa sposoby.

Kod źródłowy zapisujemy w pliku o rozszerzeniu zależnym od języka. Pliki Pythona kończą się na `.py`. Taki plik będzie miał nasz przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Zaczyna się od pliku `rozlicz.py`:

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

```text
Wspólna Kasa
100.0
```

Plik sam niczego nie robi. Dopiero osobny program czyta go i wykonuje linia po linii, a jak to działa, pokażemy przy uruchamianiu programu.

Konsekwencja: kod źródłowy możesz otworzyć, przeczytać i poprawić w każdym edytorze tekstu. Dlatego to on jest tym, co programista naprawdę tworzy i zmienia.

[sec-03-do-czego-sluzy-edytor] ## Do czego służy edytor
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

[sec-03-co-znaczy-uruchomic-program] ## Co znaczy uruchomić program
Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam [[kod-zrodlowy|kod źródłowy]] leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś nie zacznie go realizować.

Plik z kodem czyta i wykonuje linia po linii inny program. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.

Polecenie wpisujemy w [[terminal|terminalu]], czyli oknie, w którym komputer przyjmuje polecenia pisane tekstem i odpowiada tekstem. U siebie masz już plik `kasa.py`:

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
```

W terminalu, w katalogu z plikiem, wpisujemy `python kasa.py`, a program wypisuje:

```text
Wspólna Kasa
```

Linia z `#` to komentarz, który Python pomija, więc wykonuje się tylko `print`. Gdyby linii było więcej, wykonywałyby się jedna po drugiej, w kolejności zapisu.

Uruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. Tak wygląda codzienna praca: zapisz, uruchom, przeczytaj wynik.

[sec-03-kompilator-i-interpreter] ## Kompilator i interpreter
Kompilator i interpreter to programy, które przekładają [[kod-zrodlowy|kod źródłowy]] na działanie komputera, bo procesor sam nie rozumie tekstu z pliku. [[kompilator|Kompilator]] tłumaczy cały kod naraz na osobny, gotowy do uruchomienia plik. [[interpreter|Interpreter]] czyta kod i wykonuje go na bieżąco, instrukcja po instrukcji.

To ten wykonawca, o którym była mowa przy uruchamianiu programu. Gdy wpisujesz `python rozlicz.py`, [[python|Python]] działa jako interpreter: bierze plik i wykonuje go od góry.

| | Kompilator | Interpreter |
|---|---|---|
| Co robi | tłumaczy całość przed startem | wykonuje kod w trakcie czytania |
| Wynik | osobny plik do uruchomienia | brak pliku, od razu efekt |
| Uruchomienie po zmianie | najpierw kompilacja, potem start | zapisz i uruchom |

```text
kompilator:   kod źródłowy --> [kompilator] --> plik programu --> uruchomienie
interpreter:  kod źródłowy --> [interpreter] --> uruchomienie
```

Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania. Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie. W praktyce Python najpierw przekłada plik na pośredni zapis, ale z Twojej strony to jedno polecenie.

[sec-03-co-to-jest-blad-w-programie] ## Co to jest błąd w programie
[[blad-w-programie|Błąd w programie]] to każde miejsce, w którym program robi coś innego, niż chciał jego autor. Albo zatrzymuje się z komunikatem, albo działa do końca i podaje zły wynik.

Pierwszy rodzaj widać od razu. Python czyta plik od góry i gdy trafi na coś, czego nie rozumie, przerywa pracę i wypisuje komunikat. Tak jest, gdy literówka zmieni [[print|print]] (polecenie, które każe programowi wypisać tekst lub liczbę na ekranie) w `prnt`: interpreter nie zna takiego słowa. To jeszcze nie katastrofa, bo komunikat wskazuje linię i powód. U siebie zobaczysz to za chwilę w `kasa.py`.

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

Konsekwencja: błąd to normalna część pracy, nie porażka. Komunikat to podpowiedź, a brak komunikatu nie znaczy, że wynik jest dobry. Jak rozróżniać te rodzaje błędów i czytać komunikaty, omówimy osobno, w dziale o poprawianiu programów.

[sec-03-do-czego-sluza-komentarze] ## Do czego służą komentarze
[[komentarz|Komentarz]] to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi.

W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. [[interpreter|Interpreter]] pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją.

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

U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej. Komentarz nie przeszkadza w znalezieniu błędu: popraw literówkę i uruchom plik ponownie.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 13,
      "status": "covered",
      "section_ids": [
        "sec-03-czym-jest-kod-zrodlowy"
      ],
      "explanation": "Sekcja definiuje kod źródłowy jako tekst w języku programowania, zwykły plik tekstowy z instrukcjami wg składni, wykonywany przez osobny program; to on jest tym, co programista tworzy."
    },
    {
      "question_id": 14,
      "status": "covered",
      "section_ids": [
        "sec-03-do-czego-sluzy-edytor"
      ],
      "explanation": "Wyjaśnia rolę edytora (pisanie, poprawianie), listuje podświetlanie, numery linii, wcięcia, podpowiedzi i zaznacza, że sam kodu nie uruchamia, a plik to zwykły tekst."
    },
    {
      "question_id": 15,
      "status": "covered",
      "section_ids": [
        "sec-03-co-znaczy-uruchomic-program"
      ],
      "explanation": "Definiuje uruchomienie jako wykonywanie instrukcji od pierwszej do ostatniej przez inny program (Python) po podaniu nazwy pliku w terminalu, z przykładem i informacją, że plik się nie zmienia."
    },
    {
      "question_id": 16,
      "status": "covered",
      "section_ids": [
        "sec-03-kompilator-i-interpreter"
      ],
      "explanation": "Porównuje kompilator i interpreter (definicje, tabela, schemat), wskazuje Pythona jako interpreter i konsekwencję: zapisz i uruchom bez osobnego budowania."
    },
    {
      "question_id": 17,
      "status": "covered",
      "section_ids": [
        "sec-03-co-to-jest-blad-w-programie"
      ],
      "explanation": "Definiuje błąd i pokazuje dwa rodzaje: zatrzymanie z komunikatem (literówka prnt) oraz zły wynik bez ostrzeżenia (300 / 2), z zasadą, że komputer robi to, co napisano."
    },
    {
      "question_id": 18,
      "status": "covered",
      "section_ids": [
        "sec-03-do-czego-sluza-komentarze"
      ],
      "explanation": "Wyjaśnia, że komentarz jest dla człowieka, pomijany przez interpreter, służy do podania powodu i do wyłączania instrukcji, oraz że trzeba go aktualizować, z przykładem nieaktualnego komentarza."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-16",
      "status": "brak",
      "explanation": "Dział nie zawiera zapowiedzi, że kod pojawi się w dalszych działach; sam już pokazuje kod."
    },
    {
      "reference_id": "ref-19",
      "status": "spełniona",
      "section_id": "sec-03-czym-jest-kod-zrodlowy",
      "quote": "Taki plik będzie miał nasz przykład, który będzie nam towarzyszył: „Wspólna Kasa”",
      "explanation": "Wspólna Kasa jest użyta jako przykład z kodem rozlicz.py."
    },
    {
      "reference_id": "ref-24",
      "status": "spełniona",
      "section_id": "sec-03-czym-jest-kod-zrodlowy",
      "quote": "Zaczyna się od pliku `rozlicz.py`",
      "explanation": "Wspólna Kasa pojawia się w dziale z kodem i jest kontynuowana w kolejnych sekcjach."
    },
    {
      "reference_id": "ref-25",
      "status": "spełniona",
      "section_id": "sec-03-czym-jest-kod-zrodlowy",
      "quote": "print(\"Wspólna Kasa\")\nprint(300 / 3)",
      "explanation": "Kod Wspólnej Kasy (rozlicz.py, kasa.py) pojawia się w tym dziale."
    },
    {
      "reference_id": "ref-30",
      "status": "spełniona",
      "section_id": "sec-03-kompilator-i-interpreter",
      "quote": "Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania.",
      "explanation": "Wspólna Kasa wraca jako przykład w tym dziale."
    },
    {
      "reference_id": "ref-34",
      "status": "spełniona",
      "section_id": "sec-03-co-znaczy-uruchomic-program",
      "quote": "Plik z kodem czyta i wykonuje linia po linii inny program.",
      "explanation": "Sekcja pokazuje, jak osobny program (Python) czyta i wykonuje plik."
    },
    {
      "reference_id": "ref-35",
      "status": "spełniona",
      "section_id": "sec-03-do-czego-sluza-komentarze",
      "quote": "# rozlicz.py - rozliczenie wspólnych wydatków",
      "explanation": "Wspólna Kasa wraca jako przykład w komentarzach i pozostałych sekcjach działu."
    },
    {
      "reference_id": "ref-37",
      "status": "spełniona",
      "section_id": "sec-03-co-znaczy-uruchomic-program",
      "quote": "Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku",
      "explanation": "Sekcja wyjaśnia, co znaczy uruchomić program."
    },
    {
      "reference_id": "ref-38",
      "status": "spełniona",
      "section_id": "sec-03-kompilator-i-interpreter",
      "quote": "To ten wykonawca, o którym była mowa przy uruchamianiu programu.",
      "explanation": "Sekcja wyjaśnia wykonawcę i różnicę między kompilatorem a interpreterem."
    },
    {
      "reference_id": "ref-41",
      "status": "częściowo",
      "section_id": "sec-03-do-czego-sluza-komentarze",
      "quote": "U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej.",
      "explanation": "Sekcja zakłada literówkę prnt w kasa.py, ale sekcja o uruchamianiu podaje kasa.py z poprawnym print; czytelnik nie zobaczy komunikatu o błędzie, a sam komunikat nigdzie nie jest pokazany."
    }
  ]
}
````
