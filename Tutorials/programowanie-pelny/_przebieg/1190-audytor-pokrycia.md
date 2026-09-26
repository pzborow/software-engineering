# Krok 1190 · audytor_pokrycia

Węzeł: `coverage` · dział: 5 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 26. Jakie podstawowe działania matematyczne może wykonać program?
  odpowiedź: Program potrafi dodawać, odejmować, mnożyć i dzielić, a także dzielić całkowicie, liczyć resztę z dzielenia i potęgować. Zapisuje się je operatorami `+`, `-`, `*`, `/`, `//`, `%` i `**`. Kolejność działań jest taka jak w szkole, a nawiasy ją zmieniają. Operatory `+` i `*` działają też na tekście, ale wtedy sklejają i powtarzają.
  sekcje pisarza: sec-05-dzialania-matematyczne-w-programie
- 27. Jak program łączy ze sobą teksty?
  odpowiedź: Program łączy teksty operatorem `+`, który skleja je w jednym napisie dokładnie tak, jak podano, bez dodawania spacji. Sklejać można tylko tekst z tekstem, więc liczbę trzeba najpierw zamienić na tekst funkcją `str()`. Wygodną alternatywą jest zapis z literą `f` przed cudzysłowem i nazwami w nawiasach klamrowych.
  sekcje pisarza: sec-05-laczenie-tekstow
- 28. Jak program porównuje dwie wartości?
  odpowiedź: Program porównuje dwie wartości operatorami takimi jak `==`, `!=`, `<`, `>`, `<=` i `>=`. Każde porównanie daje wynik `True` albo `False`. Podwójny `==` pyta o równość, a pojedynczy `=` zapisuje wartość w zmiennej. Porównanie jest ścisłe: różni się wielkość liter, a tekst `"45.5"` nie jest równy liczbie 45.5.
  sekcje pisarza: sec-05-porownywanie-wartosci
- 29. Czym jest instrukcja warunkowa „jeśli… to…”?
  odpowiedź: Instrukcja warunkowa to polecenie, które wykonuje wskazany fragment kodu tylko wtedy, gdy warunek jest prawdziwy. W Pythonie zapisuje się ją jako `if`, warunek i dwukropek, a należące do niej linie oznacza się wcięciem. Gdy warunek jest fałszywy, Python pomija te linie i wykonuje dalszy kod.
  sekcje pisarza: sec-05-instrukcja-warunkowa-jesli-to
- 30. Do czego służy część „w przeciwnym razie”?
  odpowiedź: Część „w przeciwnym razie” (`else`) wykonuje się wtedy, gdy warunek z `if` jest fałszywy. Dzięki niej program wybiera jedną z dwóch dróg: albo blok pod `if`, albo blok pod `else`. Nigdy oba naraz i nigdy żaden.
  sekcje pisarza: sec-05-czesc-w-przeciwnym-razie
- 31. Do czego służą operatory „i” oraz „lub”?
  odpowiedź: Operator `and` („i”) daje `True` tylko wtedy, gdy oba łączone warunki są prawdziwe. Operator `or` („lub”) daje `True`, gdy prawdziwy jest choć jeden z nich. Dzięki temu program może sprawdzić kilka rzeczy naraz i podjąć jedną decyzję w `if`.
  sekcje pisarza: sec-05-operatory-i-oraz-lub

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-41: „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)
- ref-51: „U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika)
- ref-52: „Tym zajmiemy się osobno.” (łączenie tekstów plusem); ma ją spełnić pytanie 27
- ref-61: „Jak to zapisać, pokażemy przy instrukcji warunkowej” (zapisywanie decyzji na podstawie wartości logicznej); ma ją spełnić pytanie 29
- ref-66: „w warsztacie poniżej dopisujesz do swojego skryptu linię” (zapowiedź warsztatu i skryptu, w którym czytelnik wywoła błąd TypeError)
- ref-69: „instrukcja warunkowa, o której będzie następna sekcja” (instrukcja warunkowa wybierająca działanie na podstawie True/False); ma ją spełnić pytanie 29
- ref-71: „pokażemy w następnej sekcji” (co zrobić, gdy warunek jest fałszywy (else)); ma ją spełnić pytanie 30
- ref-73: „pokażemy w następnej sekcji” (operatory „i” oraz „lub” do sprawdzania kilku warunków naraz); ma ją spełnić pytanie 31

SEKCJE DZIAŁU 05 "Operacje i decyzje":
[sec-05-dzialania-matematyczne-w-programie] ## Działania matematyczne w programie
Program wykonuje te same działania co kalkulator: dodawanie, odejmowanie, mnożenie i dzielenie, a do tego dzielenie całkowite, resztę z dzielenia i potęgowanie. Zapisujesz je za pomocą [[operator-arytmetyczny|operatorów arytmetycznych]], czyli znaków, które mówią Pythonowi, jakie działanie wykonać na liczbach.

| Działanie | Operator |
|---|---|
| dodawanie | `+` |
| odejmowanie | `-` |
| mnożenie | `*` |
| dzielenie | `/` |
| dzielenie całkowite | `//` |
| reszta z dzielenia | `%` |
| potęgowanie | `**` |

Mnożenie to gwiazdka, a nie „x”. Dzielenie `/` zawsze daje liczbę z częścią ułamkową, `//` zostawia samą część całkowitą, a `%` pokazuje, ile zostało. Kolejność działań jest jak w szkole: mnożenie i dzielenie przed dodawaniem, a nawiasy zmieniają porządek.

```python
kwota = 100
print(kwota / 3)
print(kwota // 3)
print(kwota % 3)
```

```text
33.333333333333336
33
1
```

Końcówka `...336` to drobna nieścisłość: komputer trzyma ułamki w przybliżeniu.

Odejmowanie, dzielenie, `//`, `%` i `**` mają sens tylko na liczbach. Skoro `nazwa_wyjazdu` jest tekstem, `nazwa_wyjazdu / 2` kończy się błędem `TypeError`. Wyjątkiem są `+` i `*`, które na tekście działają inaczej: sklejają i powtarzają.

```python
print("Ania" + "Bartek")
print("Ha" * 3)
```

```text
AniaBartek
HaHaHa
```

[sec-05-laczenie-tekstow] ## Łączenie tekstów
Program łączy teksty operatorem `+`, który skleja je w jeden, dokładnie w takiej kolejności i z takimi znakami, jakie mu podasz. Ta operacja nazywa się [[konkatenacja|sklejaniem tekstów]] (konkatenacją). Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono.

Python niczego nie dopowiada. Nie doda spacji ani przecinka, więc odstępy musisz wstawić sam, jako część tekstu w cudzysłowie:

```python
imie = "Ania"
kwota = 45.5
print(imie + " zapłaciła " + str(kwota) + " zł")
print(imie + "zapłaciła")
```

```text
Ania zapłaciła 45.5 zł
Aniazapłaciła
```

W drugiej linii zabrakło spacji, więc słowa się zlepiły.

Sklejać można tylko tekst z tekstem. Zapis `"Kwota: " + kwota` zatrzyma program błędem `TypeError`, bo liczby 45.5 nie da się dokleić do napisu. Zamienia ją na tekst funkcja `str()`: `str(kwota)` daje `"45.5"`. Nie zmienia to samej zmiennej `kwota`, która dalej jest liczbą.

Wygodniejszy bywa zapis z literą `f` przed cudzysłowem: `f"{imie} zapłaciła {kwota} zł"`. Nazwy w nawiasach klamrowych Python podmienia na wartości, także liczbowe.

Ten błąd możesz wywołać od razu: w warsztacie poniżej dopisujesz do swojego skryptu linię, która skleja tekst z liczbą.

[sec-05-porownywanie-wartosci] ## Porównywanie wartości
Program porównuje wartości [[operator-porownania|operatorami porównania]]. To znaki takie jak `==` czy `>`, które zestawiają dwie wartości i zwracają wynik `True` albo `False`, czyli [[wartosc-logiczna|wartość logiczną]].

| Zapis | Znaczenie |
|---|---|
| `a == b` | równe |
| `a != b` | różne |
| `a < b`, `a > b` | mniejsze, większe |
| `a <= b`, `a >= b` | mniejsze lub równe, większe lub równe |

Uwaga na `==`: pojedynczy znak `=` to [[przypisanie]], czyli zapisanie wartości w zmiennej. Dopiero podwójny pyta „czy są równe?” i niczego nie zmienia.

```python
kwota = 45.5
print(kwota == 45.5)
print(kwota != 45.5)
print(kwota > 50)
print(kwota <= 45.5)
print("Ania" == "ania")
print("45.5" == 45.5)
```

```text
True
False
False
True
False
False
```

Dwa ostatnie wyniki pokazują, że porównanie jest ścisłe. Wielka i mała litera to różne znaki, więc `"Ania"` i `"ania"` się różnią. Tekst `"45.5"` i liczba 45.5 to różne typy, więc też nie są równe, choć wyglądają podobnie.

Sam wynik `True` lub `False` jeszcze nic nie robi. Dopiero instrukcja warunkowa, o której będzie następna sekcja, pozwoli programowi wybrać na jego podstawie, co zrobić dalej.

[sec-05-instrukcja-warunkowa-jesli-to] ## Instrukcja warunkowa „jeśli… to…”
[[instrukcja-warunkowa|Instrukcja warunkowa]] to polecenie, które wykonuje wybrany fragment kodu tylko wtedy, gdy warunek jest prawdziwy. W Pythonie zapisujemy ją słowem `if`, czyli „jeśli”.

Warunek to zwykle porównanie z poprzedniej sekcji, bo daje `True` albo `False`. Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej.

Które linie należą do warunku, pokazuje [[wciecie|wcięcie]]: przesunięcie linii o cztery spacje w prawo. Po warunku stawiamy dwukropek.

```python
kwota = 45.5
if kwota > 40:
    print("Kwota do sprawdzenia")
if kwota > 100:
    print("Bardzo duża kwota")
print("Koniec")
```

```text
Kwota do sprawdzenia
Koniec
```

Pierwszy warunek jest prawdziwy, więc jego linia się wykonała. Drugi jest fałszywy, więc jego wcięta linia została pominięta. Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.

Program przestaje więc biegnąć wszystkimi liniami po kolei: to, co wykona, zależy od danych. Co zrobić, gdy warunek jest fałszywy, pokażemy w następnej sekcji.

[sec-05-czesc-w-przeciwnym-razie] ## Część „w przeciwnym razie”
Część `else`, czyli „w przeciwnym razie”, wykonuje swoje linie wtedy, gdy warunek z `if` jest fałszywy. Dzięki niej program zawsze wybiera jedną z dwóch dróg, a nie tylko „robi coś albo nic”.

Zapisujemy ją pod blokiem `if`, na tym samym poziomie [[wciecie|wcięcia]] co samo `if`, z dwukropkiem po słowie `else`. Sama nie ma warunku: nie pyta o nic, bo obejmuje wszystko, czego `if` nie złapało. Jej własne linie też wcinamy o cztery spacje.

```python
kwota = 45.5
if kwota > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print("Koniec")
```

```text
Zwykła kwota
Koniec
```

Warunek `kwota > 100` jest fałszywy, więc Python pominął pierwszy wcięty blok i wykonał ten pod `else`. Gdyby kwota wynosiła 150, wypisałoby się tylko „Bardzo duża kwota”. Oba bloki nigdy nie wykonają się naraz. Ostatni `print` nie ma wcięcia, więc, jak w poprzedniej sekcji, działa zawsze.

Dla „Wspólnej Kasy” to ważne: program może teraz w każdym przypadku powiedzieć coś sensownego, osobno o dużej i zwykłej kwocie. Sprawdzanie kilku warunków naraz, czyli „i” oraz „lub”, pokażemy w następnej sekcji.

[sec-05-operatory-i-oraz-lub] ## Operatory „i” oraz „lub”
[[operator-logiczny|Operatory logiczne]] `and` („i”) oraz `or` („lub”) łączą kilka warunków w jeden. Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: `True` albo `False`.

`and` daje `True` tylko wtedy, gdy prawdziwe są **oba** warunki. `or` daje `True`, gdy prawdziwy jest **którykolwiek** z nich, a `False` dopiero wtedy, gdy oba są fałszywe.

| Lewy warunek | Prawy warunek | `and` | `or` |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

Każdy z połączonych warunków zapisujemy w całości, tak jak w porównywaniu wartości. Wynik można wypisać albo wstawić do `if`:

```python
kwota = 45.5
liczba_osob = 3
print(kwota > 40 and liczba_osob > 5)
print(kwota > 100 or liczba_osob == 3)
if kwota > 100 or liczba_osob > 5:
    print("Duża kwota")
else:
    print("Zwykła kwota")
```

```text
False
True
Zwykła kwota
```

W pierwszej linii drugi warunek zawiódł, więc `and` dało `False`. W drugiej wystarczył prawdziwy drugi warunek, więc `or` dało `True`. W `if` oba są fałszywe, więc zadziałało `else`.

Dla „Wspólnej Kasy” to znaczy, że kwotę można uznać za dużą, gdy jest wysoka **lub** dzieli ją dużo osób. U siebie w `kasa.py` dopisz te linie w warsztacie poniżej.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 26,
      "status": "covered",
      "section_ids": [
        "sec-05-dzialania-matematyczne-w-programie"
      ],
      "explanation": "Sekcja wymienia wszystkie operatory z tabelą, przykładem, kolejnością działań i nawiasami oraz zachowaniem + i * na tekście."
    },
    {
      "question_id": 27,
      "status": "covered",
      "section_ids": [
        "sec-05-laczenie-tekstow"
      ],
      "explanation": "Wyjaśnia sklejanie plusem bez dodawania spacji, konieczność str() dla liczb oraz alternatywę z f-stringiem."
    },
    {
      "question_id": 28,
      "status": "covered",
      "section_ids": [
        "sec-05-porownywanie-wartosci"
      ],
      "explanation": "Podaje operatory, wyniki True/False, różnicę == i =, oraz ścisłość porównania z przykładami."
    },
    {
      "question_id": 29,
      "status": "covered",
      "section_ids": [
        "sec-05-instrukcja-warunkowa-jesli-to"
      ],
      "explanation": "Definiuje if, składnię z dwukropkiem i wcięciem oraz pokazuje pomijanie bloku przy fałszu."
    },
    {
      "question_id": 30,
      "status": "covered",
      "section_ids": [
        "sec-05-czesc-w-przeciwnym-razie"
      ],
      "explanation": "Wyjaśnia else, jego wcięcie, brak warunku i to, że wykonuje się dokładnie jeden z bloków."
    },
    {
      "question_id": 31,
      "status": "covered",
      "section_ids": [
        "sec-05-operatory-i-oraz-lub"
      ],
      "explanation": "Opisuje and i or z tabelą prawdy, przykładami i użyciem w if."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-16",
      "status": "brak",
      "explanation": "W sekcjach działu 05 nie ma odniesienia do tej zapowiedzi; kod pojawia się, ale nic jej nie domyka."
    },
    {
      "reference_id": "ref-41",
      "status": "brak",
      "explanation": "Żadna sekcja nie pokazuje komunikatu o błędzie w kasa.py; TypeError jest tylko wspomniany słownie, bez wyniku."
    },
    {
      "reference_id": "ref-51",
      "status": "częściowo",
      "section_id": "sec-05-laczenie-tekstow",
      "quote": "Zapis `\"Kwota: \" + kwota` zatrzyma program błędem `TypeError`",
      "explanation": "Błąd jest opisany, ale nie pokazano go w pliku czytelnika; wykonanie odsyła do warsztatu, którego tu nie ma."
    },
    {
      "reference_id": "ref-52",
      "status": "spełniona",
      "section_id": "sec-05-laczenie-tekstow",
      "quote": "Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono.",
      "explanation": "Sekcja o łączeniu tekstów realizuje obietnicę."
    },
    {
      "reference_id": "ref-61",
      "status": "spełniona",
      "section_id": "sec-05-instrukcja-warunkowa-jesli-to",
      "quote": "Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie.",
      "explanation": "Pokazano zapis decyzji na podstawie wartości logicznej przez if."
    },
    {
      "reference_id": "ref-66",
      "status": "częściowo",
      "section_id": "sec-05-laczenie-tekstow",
      "quote": "w warsztacie poniżej dopisujesz do swojego skryptu linię, która skleja tekst z liczbą",
      "explanation": "Sekcja powtarza zapowiedź, ale samego warsztatu z błędem TypeError w materiale nie ma."
    },
    {
      "reference_id": "ref-69",
      "status": "spełniona",
      "section_id": "sec-05-instrukcja-warunkowa-jesli-to",
      "quote": "wykonuje wybrany fragment kodu tylko wtedy, gdy warunek jest prawdziwy",
      "explanation": "Instrukcja warunkowa wybiera działanie na podstawie True/False."
    },
    {
      "reference_id": "ref-71",
      "status": "spełniona",
      "section_id": "sec-05-czesc-w-przeciwnym-razie",
      "quote": "wykonuje swoje linie wtedy, gdy warunek z `if` jest fałszywy",
      "explanation": "Sekcja pokazuje else jako reakcję na fałszywy warunek."
    },
    {
      "reference_id": "ref-73",
      "status": "spełniona",
      "section_id": "sec-05-operatory-i-oraz-lub",
      "quote": "łączą kilka warunków w jeden. Dzięki nim program sprawdza kilka rzeczy naraz",
      "explanation": "Sekcja omawia and i or do sprawdzania kilku warunków naraz."
    }
  ]
}
````
