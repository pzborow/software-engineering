# Krok 1194 · audytor_pokrycia

Węzeł: `coverage` · dział: 9 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 50. Czym różni się błąd składni od błędu logicznego?
  odpowiedź: Błąd składni to zapis niezgodny z regułami języka, więc Python zatrzymuje program przed startem i wskazuje linię. Błąd logiczny to poprawny zapis z błędnym pomysłem, więc program działa, ale daje zły wynik i nie ma żadnego komunikatu. Pierwszy znajduje Python, drugi musisz znaleźć sam, porównując wynik z oczekiwanym.
  sekcje pisarza: sec-09-blad-skladni-a-blad-logiczny
- 51. Jak przeczytać komunikat o błędzie?
  odpowiedź: Czytaj komunikat od dołu: ostatnia linia podaje nazwę i opis błędu, a linie nad nią (Traceback) pokazują plik, numer linii i funkcję, w której program się zatrzymał. Najpierw znajdź w śladzie własny plik i numer linii, potem sprawdź, co jest w tej linii.
  sekcje pisarza: sec-09-jak-czytac-komunikat-o-bledzie
- 52. Czym jest testowanie programu?
  odpowiedź: Testowanie programu to systematyczne sprawdzanie go na wielu danych, dla których znasz poprawny wynik. Zapisujesz oczekiwania w kodzie, na przykład przez assert, a komputer porównuje je z tym, co program naprawdę zwraca. Dzięki temu po każdej zmianie szybko widzisz, czy coś przestało działać.
  sekcje pisarza: sec-09-czym-jest-testowanie-programu
- 53. Czym jest debugowanie?
  odpowiedź: Debugowanie to szukanie przyczyny błędu w programie i jej usuwanie. Zamiast zgadywać, sprawdzasz krok po kroku, co program naprawdę robi: w których miejscach wartości są takie, jak myślałeś, a w którym przestają. Najprostsze narzędzie to `print`, który pokazuje wartości w trakcie pracy.
  sekcje pisarza: sec-09-czym-jest-debugowanie
- 54. Dlaczego warto zapisywać kolejne wersje kodu?
  odpowiedź: Zapisujesz wersje, żeby móc wrócić do stanu, który działał, gdy kolejna zmiana coś zepsuje. Historia pokazuje też, kiedy pojawił się błąd, a opisy commitów przypominają, dlaczego kod wygląda tak, a nie inaczej. Robi to program Git: każdy commit to zapisana wersja plików z krótkim opisem.
  sekcje pisarza: sec-09-po-co-zapisywac-wersje-kodu
- 55. Jak szukać rozwiązań problemów programistycznych w internecie?
  odpowiedź: Wpisz w wyszukiwarkę ostatnią linię komunikatu o błędzie razem z nazwą języka, bez ścieżek i własnych nazw. Gdy komunikatu nie ma, opisz problem słowami. Najpierw sprawdzaj dokumentację i dobrze oceniane odpowiedzi z forów, a znaleziony kod przeczytaj i uruchom na małym przykładzie, zanim go użyjesz.
  sekcje pisarza: sec-09-szukanie-rozwiazan-w-internecie

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-32: „Do systematycznego sprawdzania wrócimy przy testowaniu programu” (testowanie programu jako systematyczne sprawdzanie na wielu danych); ma ją spełnić pytanie 52
- ref-41: „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)
- ref-42: „omówimy osobno, w dziale o poprawianiu programów” (rodzaje błędów i czytanie komunikatów); ma ją spełnić pytanie 50
- ref-51: „U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika)
- ref-66: „w warsztacie poniżej dopisujesz do swojego skryptu linię” (zapowiedź warsztatu i skryptu, w którym czytelnik wywoła błąd TypeError)
- ref-91: „do czego wrócimy przy testowaniu programu” (testowanie małych funkcji); ma ją spełnić pytanie 52
- ref-93: „Za chwilę dopiszesz `na_osobe` i użyjesz obu” (zapowiedź ćwiczenia praktycznego z funkcją na_osobe)
- ref-94: „Czytanie takich komunikatów omówimy przy błędach” (czytanie komunikatów o błędach); ma ją spełnić pytanie 51
- ref-96: „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” (własny plik funkcje.py, w którym czytelnik zobaczy błąd)
- ref-102: „Usuwamy ją w warsztacie poniżej.” (zapowiedź poprawienia błędnej ostatniej linii w warsztacie)
- ref-110: „przykładzie, który będzie nam towarzyszył” (program „Wspólna Kasa” wracający w kolejnych sekcjach)
- ref-117: „Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu” (czytanie komunikatów o błędach i debugowanie); ma ją spełnić pytanie 51
- ref-119: „Szukanie przyczyny krok po kroku omówimy przy debugowaniu” (debugowanie: szukanie przyczyny błędu krok po kroku); ma ją spełnić pytanie 53
- ref-121: „szukanie przyczyny omówimy przy debugowaniu” (szukanie przyczyny błędu (debugowanie)); ma ją spełnić pytanie 53
- ref-124: „pokażemy w ćwiczeniu praktycznym” (praktyczne użycie Git na własnym komputerze)

SEKCJE DZIAŁU 09 "Błędy i dobre praktyki":
[sec-09-blad-skladni-a-blad-logiczny] ## Błąd składni a błąd logiczny
Błąd składni łamie zasady zapisu, więc Python zatrzymuje się, zanim cokolwiek wykona. Błąd logiczny ma zapis poprawny, ale robi coś innego, niż zamierzałeś, więc program działa i po cichu podaje zły wynik.

[[blad-skladni|Błąd składni]] to naruszenie [[skladnia|składni]], czyli reguł zapisu: brakujący dwukropek, niedomknięty cudzysłów, źle wcięta linia. Python czyta cały plik przed startem, więc nie wykona nawet linii sprzed błędu:

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

Słowo „start” się nie pojawiło, a komunikat wskazuje linię i miejsce.

[[blad-logiczny|Błąd logiczny]] to pomyłka w pomyśle: zły wzór, dzielnik albo warunek. Python jej nie zauważy, bo każda instrukcja jest poprawna. Trzy osoby dzielą wydatki 45.5, 20 i 12.5 zł:

```python
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)
```

```text
Na osobę: 39.0
```

Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.

Konsekwencja: błędy składni są uciążliwe, ale łatwe, bo wskaże je Python. Za błędy logiczne odpowiadasz Ty, więc wynik porównuj z rachunkiem na kartce. Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu.

[sec-09-jak-czytac-komunikat-o-bledzie] ## Jak czytać komunikat o błędzie
Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak, a linie nad nią pokazują, gdzie to się stało. Komunikat nie jest wyrokiem, tylko wskazówką.

Gdy program zatrzyma się w trakcie pracy, Python wypisuje [[traceback|Traceback]], czyli ślad wywołań: listę miejsc w kodzie, przez które przeszło wykonanie aż do błędu. Wszystko razem to [[komunikat-o-bledzie|komunikat o błędzie]], czyli tekst, w którym Python opisuje, co go zatrzymało i w którym miejscu. Dzielimy przez zero:

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

Inaczej niż przy błędzie składni ze „Startem”, który się nie pojawił, tu „Start” się wypisał, bo program ruszył i padł dopiero w środku.

Konsekwencja: nie bój się czerwonego tekstu. Przeczytaj ostatnią linię, znajdź w śladzie własny plik i numer linii, a zwykle już wiesz, gdzie szukać. Szukanie przyczyny krok po kroku omówimy przy debugowaniu.

[sec-09-czym-jest-testowanie-programu] ## Czym jest testowanie programu
[[testowanie|Testowanie]] to systematyczne sprawdzanie programu na wielu danych, dla których z góry znasz poprawny wynik. Zamiast raz spojrzeć na ekran i uznać, że „wygląda dobrze”, zapisujesz oczekiwania i pozwalasz komputerowi je porównać.

Najprostszy test to jedno sprawdzenie małej funkcji. W Pythonie służy do tego [[assert|assert]]: instrukcja, która nic nie robi, gdy warunek jest prawdziwy, a zatrzymuje program błędem `AssertionError`, gdy jest fałszywy.

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

Cisza po `assert` znaczy „zgadza się”. Gdyby ktoś zmienił dzielenie tak, że wynik byłby zły, jak przy błędzie z niewłaściwym dzielnikiem, pierwszy test zatrzymałby program i wskazał linię, w której oczekiwanie przestało być prawdą.

Dobre testy obejmują zwykłe dane i przypadki brzegowe, np. pustą listę wydatków. Kosztują chwilę, a po każdej zmianie kodu uruchamiasz je jednym poleceniem i wiesz, czy niczego nie zepsułeś.

Test nie dowodzi, że błędów nie ma, tylko że w sprawdzonych przypadkach ich nie ma. Gdy test się wywali, szukanie przyczyny omówimy przy debugowaniu.

[sec-09-czym-jest-debugowanie] ## Czym jest debugowanie
[[debugowanie|Debugowanie]] to szukanie przyczyny błędu i jej usuwanie. Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach.

Metoda jest prosta. Najpierw odtwarzasz błąd na jednych, konkretnych danych. Potem zawężasz miejsce: przed podejrzanym krokiem wypisujesz wartości i porównujesz je z tym, czego oczekujesz. Pierwsze miejsce, w którym wartość jest inna niż powinna, wskazuje przyczynę. Na końcu poprawiasz jedną rzecz i uruchamiasz ponownie.

Weźmy [[blad-logiczny|błąd logiczny]] z wynikiem 39.0 zamiast 26.0. Podejrzewamy dwa dane wejściowe dzielenia, więc je wypisujemy:

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

Gdy test z poprzedniej sekcji zgłosi błąd, zaczynasz tak samo: odtwarzasz przypadek, który go wywołał, i patrzysz na wartości. Po naprawie usuń linie z `DEBUG`, żeby nie zaśmiecały wyniku.

[sec-09-po-co-zapisywac-wersje-kodu] ## Po co zapisywać wersje kodu
Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast szukać własnych zmian z pamięci.

Robi to [[git|Git]], program do zapisywania historii plików. Zapis jednej wersji to [[commit|commit]]: zdjęcie wybranych plików z danej chwili, z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię, to [[repozytorium|repozytorium]]. W przykładowym programie do dzielenia wydatków, „Wspólnej Kasie”, będzie nim folder `wspolna_kasa`, w którym leżą pliki programu.

Wersje przydają się w trzech sytuacjach:

- Dopisujesz do „Wspólnej Kasy” nową funkcję, [[sec-09-czym-jest-testowanie-programu|testy]] przestają przechodzić, a Ty wracasz do wczorajszego commita zamiast szukać własnych zmian.
- Historia pokazuje, kiedy pojawił się błąd, co przy szukaniu przyczyny oszczędza sporo czasu.
- Każdy commit ma opis, więc po miesiącu wiesz, dlaczego kod wygląda tak, a nie inaczej.

Dobry moment na commit to chwila, gdy testy przechodzą. Wiele małych commitów jest lepsze niż jeden wielki.

Sam zapis wygląda tak:

```text
git init -b main
git add funkcje.py test_rozlicz.py
git commit -m "Funkcje i testy Wspolnej Kasy"
```

`init` zakłada repozytorium w bieżącym folderze, `add` wybiera pliki do zapisu, a `commit` zapisuje wersję. Git trzeba mieć zainstalowanym (sprawdzisz to poleceniem `git --version`, a instalator jest na stronie git-scm.com). Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym.

[sec-09-szukanie-rozwiazan-w-internecie] ## Szukanie rozwiązań w internecie
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
  "items": [
    {
      "question_id": 50,
      "status": "covered",
      "section_ids": [
        "sec-09-blad-skladni-a-blad-logiczny"
      ],
      "explanation": "Sekcja definiuje oba błędy, pokazuje przykłady z komunikatem i bez, oraz wskazuje, kto znajduje każdy z nich."
    },
    {
      "question_id": 51,
      "status": "covered",
      "section_ids": [
        "sec-09-jak-czytac-komunikat-o-bledzie"
      ],
      "explanation": "Wyjaśnia czytanie od dołu, nazwę i opis błędu, pary plik-linia-funkcja oraz szukanie własnego pliku i numeru linii, z przykładem."
    },
    {
      "question_id": 52,
      "status": "covered",
      "section_ids": [
        "sec-09-czym-jest-testowanie-programu"
      ],
      "explanation": "Definiuje testowanie, pokazuje assert z przykładem, przypadki brzegowe i ograniczenie testów."
    },
    {
      "question_id": 53,
      "status": "covered",
      "section_ids": [
        "sec-09-czym-jest-debugowanie"
      ],
      "explanation": "Definiuje debugowanie, opisuje metodę krok po kroku i pokazuje użycie print na przykładzie z wynikiem 39.0."
    },
    {
      "question_id": 54,
      "status": "covered",
      "section_ids": [
        "sec-09-po-co-zapisywac-wersje-kodu"
      ],
      "explanation": "Podaje powody (powrót do działającego stanu, historia błędu, opisy commitów), wyjaśnia Git i commit z przykładem poleceń."
    },
    {
      "question_id": 55,
      "status": "covered",
      "section_ids": [
        "sec-09-szukanie-rozwiazan-w-internecie"
      ],
      "explanation": "Opisuje wpisywanie ostatniej linii komunikatu bez ścieżek, opis słowami, ocenę źródeł oraz ostrożne uruchamianie znalezionego kodu."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-16",
      "status": "brak",
      "explanation": "Sekcje działu 09 nie zawierają zapowiedzi ani wyjaśnienia dotyczącego tego, że kod pojawi się w dalszych działach; ta obietnica dotyczy wcześniejszego działu."
    },
    {
      "reference_id": "ref-32",
      "status": "spełniona",
      "section_id": "sec-09-czym-jest-testowanie-programu",
      "quote": "systematyczne sprawdzanie programu na wielu danych, dla których z góry znasz poprawny wynik",
      "explanation": "Sekcja definiuje testowanie dokładnie tak, jak obiecano."
    },
    {
      "reference_id": "ref-41",
      "status": "brak",
      "explanation": "Żadna sekcja działu 09 nie pokazuje komunikatu o błędzie w pliku kasa.py."
    },
    {
      "reference_id": "ref-42",
      "status": "spełniona",
      "section_id": "sec-09-blad-skladni-a-blad-logiczny",
      "quote": "Błąd składni łamie zasady zapisu, więc Python zatrzymuje się, zanim cokolwiek wykona.",
      "explanation": "Rodzaje błędów omówione w osobnej sekcji działu."
    },
    {
      "reference_id": "ref-51",
      "status": "brak",
      "explanation": "Dział 09 nie pokazuje TypeError we własnym pliku czytelnika; TypeError pojawia się tylko jako przykład zapytania do wyszukiwarki."
    },
    {
      "reference_id": "ref-66",
      "status": "brak",
      "explanation": "W dziale 09 nie ma warsztatu, w którym czytelnik dopisuje linię wywołującą TypeError."
    },
    {
      "reference_id": "ref-91",
      "status": "spełniona",
      "section_id": "sec-09-czym-jest-testowanie-programu",
      "quote": "Najprostszy test to jedno sprawdzenie małej funkcji.",
      "explanation": "Testowanie małych funkcji jest pokazane na na_osobe z assert."
    },
    {
      "reference_id": "ref-93",
      "status": "brak",
      "explanation": "Dział 09 zawiera na_osobe w przykładach, ale nie ćwiczenie, w którym czytelnik ją dopisuje i używa obu funkcji."
    },
    {
      "reference_id": "ref-94",
      "status": "spełniona",
      "section_id": "sec-09-jak-czytac-komunikat-o-bledzie",
      "quote": "Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak",
      "explanation": "Sekcja omawia czytanie komunikatów o błędach."
    },
    {
      "reference_id": "ref-96",
      "status": "brak",
      "explanation": "Dział 09 nie pokazuje TypeError w pliku funkcje.py czytelnika."
    },
    {
      "reference_id": "ref-102",
      "status": "brak",
      "explanation": "Żadna sekcja działu 09 nie zawiera warsztatu poprawiającego błędną ostatnią linię."
    },
    {
      "reference_id": "ref-110",
      "status": "spełniona",
      "section_id": "sec-09-po-co-zapisywac-wersje-kodu",
      "quote": "W przykładowym programie do dzielenia wydatków, „Wspólnej Kasie”",
      "explanation": "Program Wspólna Kasa wraca w sekcji o wersjach kodu."
    },
    {
      "reference_id": "ref-117",
      "status": "spełniona",
      "section_id": "sec-09-jak-czytac-komunikat-o-bledzie",
      "quote": "Przeczytaj ostatnią linię, znajdź w śladzie własny plik i numer linii",
      "explanation": "Czytanie komunikatów omówione w sekcji, a debugowanie w sec-09-czym-jest-debugowanie."
    },
    {
      "reference_id": "ref-119",
      "status": "spełniona",
      "section_id": "sec-09-czym-jest-debugowanie",
      "quote": "Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach.",
      "explanation": "Sekcja omawia szukanie przyczyny krok po kroku."
    },
    {
      "reference_id": "ref-121",
      "status": "spełniona",
      "section_id": "sec-09-czym-jest-debugowanie",
      "quote": "Debugowanie to szukanie przyczyny błędu i jej usuwanie.",
      "explanation": "Szukanie przyczyny omówione w sekcji o debugowaniu."
    },
    {
      "reference_id": "ref-124",
      "status": "częściowo",
      "section_id": "sec-09-po-co-zapisywac-wersje-kodu",
      "quote": "Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym.",
      "explanation": "Sekcja pokazuje polecenia i ponawia zapowiedź, ale samo ćwiczenie praktyczne nie jest w podanych sekcjach."
    }
  ]
}
````
