# Krok 1192 · audytor_pokrycia

Węzeł: `coverage` · dział: 7 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 38. Czym jest funkcja?
  odpowiedź: Funkcja to nazwany fragment kodu, który raz definiujesz słowem def, a potem uruchamiasz, wywołując jego nazwę z nawiasami. Może przyjmować dane i oddawać wynik. Dzięki temu ten sam kod działa w wielu miejscach bez kopiowania.
  sekcje pisarza: sec-07-czym-jest-funkcja
- 39. Po co dzielić program na funkcje?
  odpowiedź: Funkcje dzielą program na nazwane kawałki, z których każdy robi jedną rzecz i istnieje w jednym miejscu. Dzięki temu kod jest czytelniejszy, ta sama logika działa dla różnych danych bez kopiowania, a poprawkę robisz w jednym miejscu. Małe funkcje łatwiej też sprawdzać osobno.
  sekcje pisarza: sec-07-po-co-dzielic-program-na-funkcje
- 40. Czym są argumenty funkcji?
  odpowiedź: Argumenty to wartości, które podajesz w nawiasach przy wywołaniu funkcji, żeby miała na czym pracować. Python przypisuje je parametrom, czyli nazwom z definicji funkcji, według kolejności albo według nazw. Dzięki temu ta sama funkcja liczy dla różnych danych. Zła liczba argumentów kończy się błędem TypeError.
  sekcje pisarza: sec-07-czym-sa-argumenty-funkcji
- 41. Co to znaczy, że funkcja zwraca wynik?
  odpowiedź: Funkcja zwraca wynik, gdy instrukcją return oddaje wartość temu, kto ją wywołał, a wywołanie zamienia się wtedy w tę wartość. Można ją zapisać do zmiennej lub przekazać innej funkcji. Samo wypisanie na ekran to co innego: funkcja bez return oddaje None, czyli nic do dalszej pracy.
  sekcje pisarza: sec-07-zwracanie-wyniku-przez-funkcje
- 42. Dlaczego nazwy zmiennych i funkcji powinny być czytelne?
  odpowiedź: Nazwa to jedyna wskazówka, co robi funkcja albo co trzyma zmienna. Komputer nie dba o nazwy, ale człowiek czyta kod wielokrotnie i musi go rozumieć bez zgadywania. Czytelna nazwa zapobiega też błędom, np. pomyleniu kolejności argumentów.
  sekcje pisarza: sec-07-czytelne-nazwy-zmiennych-i-funkcji
- 43. Czym jest ponowne użycie kodu?
  odpowiedź: Ponowne użycie kodu to korzystanie z tego samego fragmentu wiele razy bez przepisywania go. W Pythonie robisz to przez funkcję: piszesz ją raz i wywołujesz z różnymi danymi. Dzięki temu poprawka w jednym miejscu działa wszędzie, a nowy przypadek to tylko nowe dane.
  sekcje pisarza: sec-07-ponowne-uzycie-kodu

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-28: „takie części zamienimy w osobne” (części staną się funkcjami); ma ją spełnić pytanie 38
- ref-29: „Ich nazwy, np. `suma_wydatkow`, poznasz później” (nazywanie funkcji, np. suma_wydatkow); ma ją spełnić pytanie 42
- ref-41: „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)
- ref-51: „U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika)
- ref-66: „w warsztacie poniżej dopisujesz do swojego skryptu linię” (zapowiedź warsztatu i skryptu, w którym czytelnik wywoła błąd TypeError)
- ref-88: „Oba mechanizmy omówimy osobno w kolejnych sekcjach” (argumenty funkcji (dane wchodzące)); ma ją spełnić pytanie 40
- ref-89: „Oba mechanizmy omówimy osobno w kolejnych sekcjach” (zwracanie wyniku przez return); ma ją spełnić pytanie 41
- ref-93: „Za chwilę dopiszesz `na_osobe` i użyjesz obu” (zapowiedź ćwiczenia praktycznego z funkcją na_osobe)
- ref-96: „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” (własny plik funkcje.py, w którym czytelnik zobaczy błąd)
- ref-100: „przy ponownym użyciu kodu, które omówimy za chwilę” (ponowne użycie kodu); ma ją spełnić pytanie 43
- ref-102: „Usuwamy ją w warsztacie poniżej.” (zapowiedź poprawienia błędnej ostatniej linii w warsztacie)

SEKCJE DZIAŁU 07 "Funkcje i porządek w kodzie":
[sec-07-czym-jest-funkcja] ## Czym jest funkcja
[[funkcja|Funkcja]] to nazwany kawałek kodu, który raz opisujesz, a potem uruchamiasz, kiedy zechcesz, wpisując jego nazwę. Znasz już gotowe funkcje: `print()` i `str()` napisali twórcy Pythona.

Własną funkcję zaczynasz od `def`, nazwy, nawiasów i dwukropka. Wcięty blok pod spodem to jej treść. Ten zapis to [[definicja-funkcji|definicja funkcji]]: tylko opisuje, co funkcja robi, i niczego jeszcze nie wykonuje. Dopiero [[wywolanie-funkcji|wywołanie]], czyli nazwa z nawiasami, uruchamia treść.

Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:

```python
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

print(suma([45.5, 20, 12.5]))
```

```text
78.0
```

Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. Oba mechanizmy omówimy osobno w kolejnych sekcjach; na razie wystarczy, że dane wchodzą, a wynik wychodzi.

Konsekwencja: kod, który był kawałkiem długiego programu, ma teraz nazwę i można go wywołać w wielu miejscach, bez kopiowania.

[sec-07-po-co-dzielic-program-na-funkcje] ## Po co dzielić program na funkcje
Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach.

Zobacz to na „Wspólnej Kasie”. Funkcja `suma` już jest, więc dokładamy drugą, `na_osobe`, i używamy obu dla dwóch wyjazdów:

```python
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
```

```text
Mazury: 26.0
Tatry: 112.5
```

Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz. Gdyby liczenie sumy trzeba było kiedyś zmienić, poprawiasz jedną funkcję, a oba wyniki będą poprawne.

Druga korzyść to czytelność: `na_osobe(suma(mazury), 3)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, do czego wrócimy przy testowaniu programu.

U siebie masz już `funkcje.py` z funkcją `suma`. Za chwilę dopiszesz `na_osobe` i użyjesz obu dla dwóch wyjazdów.

[sec-07-czym-sa-argumenty-funkcji] ## Czym są argumenty funkcji
[[argument-funkcji|Argumenty]] to dane, które przekazujesz funkcji w nawiasach przy wywołaniu, żeby miała na czym pracować. Funkcja bez argumentów robi zawsze to samo, a z argumentami to samo działanie wykonuje na różnych danych.

W definicji funkcji nazwy w nawiasach to [[parametr|parametry]]: puste miejsca, które funkcja wypełnia przy każdym wywołaniu. W `na_osobe(suma, osoby)` są dwa: `suma` i `osoby`. Wartości, które wpisujesz przy wywołaniu, to argumenty. Python przypisuje je parametrom tak samo jak przy przypisaniu: pierwszy argument trafia do pierwszego parametru, drugi do drugiego.

```python
def na_osobe(suma, osoby):
    return suma / osoby

print(na_osobe(300, 4))
print(na_osobe(osoby=4, suma=300))
```

```text
75.0
75.0
```

Pierwsze wywołanie podaje argumenty według kolejności. Drugie podaje je z nazwą, więc kolejność nie gra roli, a zapis mówi wprost, co oznacza każda liczba.

Liczba argumentów musi zgadzać się z liczbą parametrów. Wywołanie `na_osobe(300)` kończy się komunikatem [[typeerror|`TypeError`]]. To nazwa błędu, który Python zgłasza, gdy coś zrobiono w niewłaściwy sposób; tu znaczy: funkcję wywołano bez wartości dla `osoby`. Czytanie takich komunikatów omówimy przy błędach.

Kolejność też ma znaczenie: `na_osobe(4, 300)` da wynik bez błędu, ale zły, bo 4 zł podzielisz na 300 osób. U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`.

[sec-07-zwracanie-wyniku-przez-funkcje] ## Zwracanie wyniku przez funkcję
Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał. Ta oddana wartość to [[wartosc-zwracana|wartość zwracana]]: wywołanie funkcji staje się w kodzie właśnie nią, więc możesz ją zapisać do zmiennej albo przekazać dalej.

Po `return` funkcja od razu kończy pracę. Nic, co stoi pod nim w ciele funkcji, już się nie wykona.

Zwracanie to nie to samo co wypisywanie. `print` tylko pokazuje tekst na ekranie, a program nie dostaje z niego nic do dalszej pracy. Funkcja bez `return` oddaje specjalną wartość [[none|`None`]], czyli „nic”.

```python
def na_osobe(suma, osoby):
    return suma / osoby

def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wynik = na_osobe(300, 4)
nic = wypisz_na_osobe(300, 4)
print(wynik)
print(nic)
```

```text
75.0
75.0
None
```

Pierwsza `75.0` pochodzi z `print` wewnątrz `wypisz_na_osobe`, w chwili wywołania. Druga to `wynik`, czyli wartość zwrócona i zapisana. Zmienna `nic` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła. Nazwy `wynik` i `nic` służą tylko tej ilustracji.

Konsekwencja jest praktyczna: tylko zwrócony wynik da się wykorzystać dalej. Dlatego `na_osobe(suma(mazury), 3)` działa: wynik jednej funkcji trafia jako argument do drugiej.

[sec-07-czytelne-nazwy-zmiennych-i-funkcji] ## Czytelne nazwy zmiennych i funkcji
Nazwa to jedyna wskazówka, co kryje się w [[zmienna|zmiennej]] albo [[funkcja|funkcji]]. Komputerowi wszystko jedno, jak ją nazwiesz, ale kod czytasz Ty: dziś, za miesiąc i ktoś inny. Dobra nazwa zastępuje komentarz.

Porównaj dwie wersje tej samej rzeczy:

| Nieczytelnie | Czytelnie |
|---|---|
| `f(a, b)` | `udzial_na_osobe(suma, liczba_osob)` |
| `x = 3` | `liczba_osob = 3` |
| `dane2` | `kwoty_wydatkow` |

Przy `f(300, 4)` trzeba zgadywać, co się dzieje i która liczba jest która. To ryzyko z zamienioną kolejnością, które znasz z argumentów funkcji: zły wynik bez błędu. Nazwa `udzial_na_osobe` mówi to od razu.

Funkcję nazywaj tak, by opisywała, co robi (`suma_wydatkow`), a zmienną tak, by opisywała, co trzyma (`liczba_osob`). Zwykle małe litery, słowa rozdzielone podkreśleniem, bez polskich znaków, tak jak w całym tutorialu.

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

print(udzial_na_osobe(suma_wydatkow([45.5, 20, 12.5]), 3))
```

```text
26.0
```

Ostatnią linię czyta się prawie jak zdanie. Ta czytelność przyda się przy dzieleniu programu na funkcje i przy ponownym użyciu kodu, które omówimy za chwilę.

[sec-07-ponowne-uzycie-kodu] ## Ponowne użycie kodu
Ponowne użycie kodu to wykorzystanie tego samego fragmentu wiele razy zamiast pisania go od nowa. W Pythonie robisz to przez [[funkcja|funkcję]]: [[definicja-funkcji|definicję]] piszesz raz, a potem robisz dowolną liczbę [[wywolanie-funkcji|wywołań]] z innymi danymi.

Zobacz dwa wyjazdy liczone tą samą logiką:

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print(udzial_na_osobe(suma_wydatkow(mazury), 3))
print(udzial_na_osobe(suma_wydatkow(tatry), 4))
```

```text
26.0
112.5
```

Zmieniają się tylko dane: lista wydatków i liczba osób. Logika liczenia leży w jednym miejscu, więc nie kopiujesz pętli dla każdego wyjazdu.

Ma to dwie konsekwencje. Gdy znajdziesz błąd w liczeniu sumy, poprawiasz go raz i naprawiasz wszystkie wyjazdy naraz. A trzeci wyjazd to jedna nowa lista i dwa wywołania, bez nowego kodu.

Właśnie po to funkcje mają parametry: to, co stałe, zostaje w środku, a to, co zmienne, wchodzi z zewnątrz.

U siebie w `funkcje.py` masz te same funkcje (pod krótszymi nazwami `suma` i `na_osobe`). Ostatnia linia wywołuje `na_osobe(300)` z jednym argumentem zamiast dwóch, stąd błąd. Usuwamy ją w warsztacie poniżej.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 38,
      "status": "covered",
      "section_ids": [
        "sec-07-czym-jest-funkcja"
      ],
      "explanation": "Sekcja definiuje funkcję, def, definicję vs wywołanie, dane wejściowe i return oraz wywołanie w wielu miejscach bez kopiowania."
    },
    {
      "question_id": 39,
      "status": "covered",
      "section_ids": [
        "sec-07-po-co-dzielic-program-na-funkcje"
      ],
      "explanation": "Podaje trzy korzyści (jedno miejsce poprawki, czytelność, testowanie) z przykładem dwóch wyjazdów."
    },
    {
      "question_id": 40,
      "status": "covered",
      "section_ids": [
        "sec-07-czym-sa-argumenty-funkcji"
      ],
      "explanation": "Rozróżnia argumenty i parametry, przypisanie po kolejności i po nazwie, TypeError przy złej liczbie oraz ryzyko zamienionej kolejności."
    },
    {
      "question_id": 41,
      "status": "covered",
      "section_ids": [
        "sec-07-zwracanie-wyniku-przez-funkcje"
      ],
      "explanation": "Wyjaśnia return, wywołanie zamieniane na wartość, różnicę względem print i None, z przykładem."
    },
    {
      "question_id": 42,
      "status": "covered",
      "section_ids": [
        "sec-07-czytelne-nazwy-zmiennych-i-funkcji"
      ],
      "explanation": "Uzasadnia, że nazwa to jedyna wskazówka, człowiek czyta kod, a nieczytelne nazwy grożą błędem zamienionej kolejności; podaje zasady i przykład."
    },
    {
      "question_id": 43,
      "status": "covered",
      "section_ids": [
        "sec-07-ponowne-uzycie-kodu"
      ],
      "explanation": "Definiuje ponowne użycie, pokazuje je na funkcji z różnymi danymi i wskazuje konsekwencje: jedna poprawka i nowy przypadek bez nowego kodu."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-16",
      "status": "brak",
      "explanation": "W sekcjach działu 07 nie ma nawiązania do zapowiedzi „Na razie nie piszemy kodu”; kod po prostu się pojawia, ale nie ma to wprost odniesienia."
    },
    {
      "reference_id": "ref-28",
      "status": "spełniona",
      "section_id": "sec-07-czym-jest-funkcja",
      "quote": "Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy",
      "explanation": "Pętla sumująca zostaje zamieniona w funkcję."
    },
    {
      "reference_id": "ref-29",
      "status": "spełniona",
      "section_id": "sec-07-czytelne-nazwy-zmiennych-i-funkcji",
      "quote": "Funkcję nazywaj tak, by opisywała, co robi (`suma_wydatkow`)",
      "explanation": "Nazwa suma_wydatkow jest użyta i omówiona jako przykład nazywania funkcji."
    },
    {
      "reference_id": "ref-41",
      "status": "brak",
      "explanation": "Nie ma zapowiedzianego pokazania komunikatu o błędzie w kasa.py; sekcje mówią o funkcje.py."
    },
    {
      "reference_id": "ref-51",
      "status": "częściowo",
      "section_id": "sec-07-czym-sa-argumenty-funkcji",
      "quote": "U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`.",
      "explanation": "Sekcja opisuje TypeError i zapowiada go, ale samo zobaczenie błędu ma nastąpić w warsztacie, którego nie ma w podanych sekcjach."
    },
    {
      "reference_id": "ref-66",
      "status": "częściowo",
      "section_id": "sec-07-ponowne-uzycie-kodu",
      "quote": "Ostatnia linia wywołuje `na_osobe(300)` z jednym argumentem zamiast dwóch, stąd błąd.",
      "explanation": "Wspomniana jest linia z błędem, ale samego dopisania jej w warsztacie nie ma w sekcjach; dodatkowo mówi się, że już jest w pliku."
    },
    {
      "reference_id": "ref-88",
      "status": "spełniona",
      "section_id": "sec-07-czym-sa-argumenty-funkcji",
      "quote": "Argumenty]] to dane, które przekazujesz funkcji w nawiasach przy wywołaniu",
      "explanation": "Argumenty omówione osobno w własnej sekcji."
    },
    {
      "reference_id": "ref-89",
      "status": "spełniona",
      "section_id": "sec-07-zwracanie-wyniku-przez-funkcje",
      "quote": "Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał.",
      "explanation": "Return omówiony osobno w własnej sekcji."
    },
    {
      "reference_id": "ref-93",
      "status": "częściowo",
      "section_id": "sec-07-po-co-dzielic-program-na-funkcje",
      "quote": "Za chwilę dopiszesz `na_osobe` i użyjesz obu dla dwóch wyjazdów.",
      "explanation": "Zapowiedź powtórzona, ale samo ćwiczenie (warsztat) nie jest w podanych sekcjach; sekcja podaje tylko kod do przeczytania."
    },
    {
      "reference_id": "ref-96",
      "status": "częściowo",
      "section_id": "sec-07-czym-sa-argumenty-funkcji",
      "quote": "U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`.",
      "explanation": "Sekcja opisuje błąd, ale nie pokazuje jego wyniku; zobaczenie go zależy od warsztatu spoza sekcji."
    },
    {
      "reference_id": "ref-100",
      "status": "spełniona",
      "section_id": "sec-07-ponowne-uzycie-kodu",
      "quote": "Ponowne użycie kodu to wykorzystanie tego samego fragmentu wiele razy zamiast pisania go od nowa.",
      "explanation": "Ponowne użycie kodu omówione we własnej sekcji."
    },
    {
      "reference_id": "ref-102",
      "status": "częściowo",
      "section_id": "sec-07-ponowne-uzycie-kodu",
      "quote": "Usuwamy ją w warsztacie poniżej.",
      "explanation": "Zapowiedź jest powtórzona, ale samego warsztatu z poprawką nie ma w podanych sekcjach."
    }
  ]
}
````
