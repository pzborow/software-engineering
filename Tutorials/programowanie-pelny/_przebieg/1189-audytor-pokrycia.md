# Krok 1189 · audytor_pokrycia

Węzeł: `coverage` · dział: 4 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 19. Czym jest dana w programie?
  odpowiedź: Dana to pojedyncza informacja, na której pracuje program, na przykład imię, kwota albo odpowiedź „tak/nie”. Program przyjmuje dane, przetwarza je i wypisuje wynik. Rodzaj danej decyduje o tym, jakie działania mają sens: liczby można dodawać i dzielić, a imion nie.
  sekcje pisarza: sec-04-czym-jest-dana
- 20. Czym jest zmienna?
  odpowiedź: Zmienna to nazwane miejsce w pamięci programu, w którym leży jedna dana. Dzięki nazwie można tę daną odczytać, użyć w obliczeniach albo zastąpić inną. Wartość zmiennej może się zmieniać w trakcie działania programu, a nazwa zostaje ta sama.
  sekcje pisarza: sec-04-czym-jest-zmienna
- 21. Jak można porównać zmienną do pudełka z etykietą?
  odpowiedź: Zmienna przypomina pudełko z etykietą: etykieta to nazwa, a w środku leży jedna wartość. Po nazwie program znajduje pudełko i odczytuje zawartość. Nową wartość można włożyć, wtedy stara znika, a etykieta zostaje. Skopiowanie wartości do drugiego pudełka nie łączy ich na stałe.
  sekcje pisarza: sec-04-zmienna-jako-pudelko-z-etykieta
- 22. Czym różni się liczba od tekstu w programie?
  odpowiedź: Liczba to wartość, na której program wykonuje obliczenia, a tekst to ciąg znaków, który program przechowuje, wypisuje i skleja. O rodzaju decyduje zapis: 45.5 bez cudzysłowu to liczba, a "45.5" w cudzysłowie to tekst. Liczbę można podzielić, a tekstu nie, więc pomylenie ich kończy się błędem albo złym wynikiem.
  sekcje pisarza: sec-04-liczba-a-tekst
- 23. Czym jest typ danych?
  odpowiedź: Typ danych to rodzaj wartości, który określa, czym ona jest i co można z nią zrobić. Podstawowe typy Pythona to tekst (str), liczba całkowita (int), liczba z ułamkiem (float) i prawda/fałsz (bool). Typ wartości sprawdzisz funkcją type().
  sekcje pisarza: sec-04-czym-jest-typ-danych
- 24. Co to jest wartość logiczna prawda/fałsz?
  odpowiedź: Wartość logiczna to dana, która może mieć tylko dwie wartości: prawda (`True`) albo fałsz (`False`). Służy do zapisania odpowiedzi „tak albo nie”, np. czy wydatek został zapłacony. Jej typ w Pythonie nazywa się `bool`.
  sekcje pisarza: sec-04-wartosc-logiczna-prawda-falsz
- 25. Do czego służy przypisanie wartości do zmiennej?
  odpowiedź: Przypisanie zapisuje wartość pod nazwą zmiennej, dzięki czemu program może ją zapamiętać i użyć później. Zapisuje się je znakiem `=`: po lewej nazwa, po prawej wartość. Jeśli zmienna już istniała, jej stara wartość zostaje zastąpiona nową. Przy przypisaniu innej zmiennej kopiowana jest jej aktualna wartość, więc późniejsza zmiana oryginału nie wpływa na kopię.
  sekcje pisarza: sec-04-przypisanie-wartosci-do-zmiennej

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-41: „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)
- ref-44: „Do tego służy zmienna, którą poznasz w następnej sekcji” (zmienna jako miejsce przechowywania danych); ma ją spełnić pytanie 20
- ref-45: „wyjaśnimy przy typach danych” (nazwy rodzajów danych w Pythonie); ma ją spełnić pytanie 23
- ref-47: „Dokładniej opiszemy to przy przypisaniu” (znak = i przypisanie wartości do zmiennej); ma ją spełnić pytanie 25
- ref-51: „U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika)
- ref-53: „omówimy w następnej sekcji” (typ danych); ma ją spełnić pytanie 23
- ref-58: „Typem `bool` zajmiemy się osobno, w kolejnej sekcji” (wartość logiczna prawda/fałsz); ma ją spełnić pytanie 24

SEKCJE DZIAŁU 04 "Dane i zmienne":
[sec-04-czym-jest-dana] ## Czym jest dana
[[dana|Dana]] to każda informacja, na której pracuje program: imię, kwota, data, odpowiedź „tak” lub „nie”. Program bez danych nie miałby czego liczyć ani wypisać.

W arkuszu kalkulacyjnym danymi są wartości w komórkach: nazwisko w jednej, kwota w drugiej. W programie jest podobnie, tylko że dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz.

```python
# poza kanonem
print("Ania")       # tekst: imię
print(45.5)         # liczba: kwota
print(True)         # prawda albo fałsz: czy zapłacono
print(45.5 + 10)    # z liczbą można liczyć
```

```text
Ania
45.5
True
55.5
```

Każda z tych trzech wartości to jedna dana, ale każda jest innego rodzaju. Rodzaj danej decyduje o tym, co program może z nią zrobić. Do liczby 45.5 da się dodać 10 albo ją podzielić. Imienia „Ania” nie da się podzielić przez 2, bo to nie ma sensu; można je co najwyżej wypisać, porównać z innym albo połączyć z innym tekstem. Prawda lub fałsz odpowiada na pytanie tak/nie.

Dane trzeba też gdzieś przechowywać, żeby użyć ich więcej niż raz. Do tego służy zmienna, którą poznasz w następnej sekcji. To, jak Python nazywa poszczególne rodzaje danych, wyjaśnimy przy typach danych.

[sec-04-czym-jest-zmienna] ## Czym jest zmienna
[[zmienna|Zmienna]] to nazwane miejsce w pamięci programu, w którym leży jedna [[dana|dana]]. Dzięki nazwie możesz tę daną wielokrotnie odczytać, użyć w obliczeniach albo zastąpić inną.

Pamiętasz, że dane trzeba gdzieś przechowywać, żeby użyć ich więcej niż raz. Właśnie do tego służy zmienna. Zamiast wpisywać `45.5` w kilku miejscach, nadajesz kwocie nazwę i posługujesz się nią. To trochę jak komórka w arkuszu, którą nazwałeś „kwota”, a potem odwołujesz się do niej po nazwie.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(imie, kwota, zaplacono)
kwota = 60
print(kwota + 10)
```

```text
Ania 45.5 True
70
```

Znak `=` nie oznacza tu „równa się” jak w matematyce. Znaczy: „zapisz to, co po prawej, pod nazwą po lewej”. Dokładniej opiszemy to przy przypisaniu.

Wartość zmiennej może się zmieniać w trakcie działania programu, stąd nazwa: po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce. Nazwa zostaje ta sama. W „Wspólnej Kasie” takie zmienne w `rozlicz.py` opisują pojedynczy wydatek: kto zapłacił, ile i czy już się rozliczył.

[sec-04-zmienna-jako-pudelko-z-etykieta] ## Zmienna jako pudełko z etykietą
[[zmienna|Zmienną]] można porównać do pudełka z etykietą: etykieta to nazwa, a w środku leży jedna [[dana|dana]], czyli [[wartosc-zmiennej|wartość zmiennej]] (to, co aktualnie jest w pudełku). Program szuka pudełka po etykiecie i zagląda do środka.

```text
etykieta: kwota      etykieta: imie
┌──────────┐         ┌──────────┐
│   45.5   │         │  "Ania"  │
└──────────┘         └──────────┘
```

Porównanie tłumaczy trzy rzeczy. Pudełko mieści jedną wartość naraz, więc nowa wartość wypiera starą, jak w przypadku zmiany kwoty z poprzedniej sekcji. Etykieta zostaje, zmienia się tylko zawartość. Wreszcie każde pudełko żyje własnym życiem: kopia wartości do drugiego pudełka nie łączy ich na stałe.

```python
# poza kanonem
kwota_stara = 45.5
kwota = kwota_stara
kwota = 60
print(kwota_stara, kwota)
```

```text
45.5 60
```

Zmiana `kwota` nie ruszyła `kwota_stara`, bo do drugiego pudełka trafiła kopia wartości.

Obraz jest uproszczony: pod spodem Python działa nieco inaczej, ale na tym etapie to nie ma znaczenia. Ważna konsekwencja: etykieta ma być czytelna. W „Wspólnej Kasie” pudełko `kwota` jest zrozumiałe, a `x` zmusza do zgadywania, co w środku.

[sec-04-liczba-a-tekst] ## Liczba a tekst
Liczba to wartość, na której program liczy. Tekst to ciąg znaków, który program przechowuje, wypisuje, porównuje i skleja. Zapis decyduje o tym, z czym mamy do czynienia: `45.5` bez cudzysłowu to liczba, a `"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5.

| Zapis | Co to jest | Można dzielić? |
|---|---|---|
| `45.5` | liczba | tak |
| `"45.5"` | tekst | nie |
| `"Ania"` | tekst | nie |

W programie ułamek dziesiętny zapisujemy z kropką, nie z przecinkiem, tak jak `kwota = 45.5` w „Wspólnej Kasie”.

```python
kwota = 45.5
imie = "Ania"
print(kwota / 2)
print(imie)
```

```text
22.75
Ania
```

Liczbę można podzielić, tekstu nie. To ta sama myśl co [[imienia nie da się podzielić|imię „Ania” nie do podzielenia przez 2]]. Python zatrzyma się z komunikatem `TypeError`. U siebie zobaczysz to za chwilę we własnym pliku z kodem.

Uwaga na plus: przy liczbach dodaje, a przy tekstach skleja je w jeden. Tym zajmiemy się osobno.

Konsekwencja: kwotę zapisaną w cudzysłowie program potraktuje jak napis, nie jak pieniądze. Nazwę tej cechy danych, czyli typ, omówimy w następnej sekcji.

[sec-04-czym-jest-typ-danych] ## Czym jest typ danych
[[typ-danych|Typ danych]] to rodzaj wartości, który mówi Pythonowi, czym ta wartość jest i jakie działania są na niej dozwolone. Wcześniej pisaliśmy po prostu „rodzaj danych”, teraz mamy na to fachową nazwę.

Typ ma każda wartość, także ta ukryta w zmiennej. Python rozpoznaje go po zapisie: cudzysłów oznacza tekst, cyfry z kropką ułamek, a `True` lub `False` prawdę albo fałsz. Dlatego `"45.5"` to [[cztery znaki zamiast kwoty|tylko cztery znaki: 4, 5, kropka, 5]], a nie pieniądze. Typ sprawdzisz funkcją `type()`.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(type(imie))
print(type(kwota))
print(type(zaplacono))
```

```text
<class 'str'>
<class 'float'>
<class 'bool'>
```

Słowo `class` na razie pomiń, ważna jest nazwa po nim. Oto podstawowe typy Pythona:

| Nazwa w Pythonie | Co to jest | Przykład |
|---|---|---|
| `str` | tekst | `"Ania"` |
| `int` | liczba całkowita | `3` |
| `float` | liczba z ułamkiem | `45.5` |
| `bool` | prawda lub fałsz | `True` |

Typ decyduje o tym, co program może zrobić z wartością. Dlatego [[imienia nie da się podzielić|imienia nie podzielisz przez 2]], a kwotę tak. Typem `bool` zajmiemy się osobno, w kolejnej sekcji.

Konsekwencja: gdy program zachowuje się dziwnie, jedno z pierwszych pytań brzmi „jakiego typu jest ta wartość?”.

[sec-04-wartosc-logiczna-prawda-falsz] ## Wartość logiczna prawda/fałsz
[[wartosc-logiczna|Wartość logiczna]] to dana, która ma tylko dwie możliwe wartości: prawda albo fałsz. W Pythonie zapisujesz je jako `True` i `False`, a ich typ to `bool`.

Pasuje do każdej odpowiedzi „tak albo nie”: czy wydatek jest zapłacony, czy kwota jest większa od zera. Nie ma nic pomiędzy. W arkuszu to odpowiednik pola wyboru: zaznaczone albo nie.

Zapisuje się je z wielkiej litery i bez cudzysłowu. Ta sama zasada, co przy `"45.5"`: `True` to wartość logiczna, a `"True"` w cudzysłowie to tylko tekst z czterech liter.

```python
zaplacono = True
print(zaplacono)
zaplacono = False
print(zaplacono)
print(type(zaplacono))
```

```text
True
False
<class 'bool'>
```

Zmienną logiczną podmieniasz jak każdą inną: po drugim przypisaniu `True` znika, a jej miejsce zajmuje `False`.

Konsekwencja: taka wartość służy programowi do podejmowania decyzji. Na podstawie `zaplacono` program będzie mógł wybrać, czy przypomnieć o długu. Jak to zapisać, pokażemy przy instrukcji warunkowej.

[sec-04-przypisanie-wartosci-do-zmiennej] ## Przypisanie wartości do zmiennej
[[przypisanie|Przypisanie]] to instrukcja, która zapisuje wartość pod nazwą zmiennej. Dzięki niej program zapamiętuje daną i może do niej wrócić w dalszej części kodu.

Zapisujesz je znakiem `=`. Po lewej stoi nazwa, po prawej wartość: `kwota = 45.5`. To nie jest równanie ze szkoły, tylko polecenie: „weź to, co po prawej, i połóż pod nazwą po lewej”. Jeśli zmienna jeszcze nie istniała, Python ją tworzy. Jeśli istniała, podmienia jej wartość, tak jak przy pudełku z etykietą.

Przypisanie działa od prawej do lewej i tylko w chwili wykonania. Gdy po prawej stronie stoi inna zmienna, Python kopiuje jej aktualną wartość. Późniejsza zmiana oryginału nie rusza kopii.

```python
kwota = 45.5
kwota_stara = kwota
kwota = 60
print(kwota)
print(kwota_stara)
```

```text
60
45.5
```

Linia `kwota_stara = kwota` skopiowała 45.5 w chwili wykonania. Dopiero potem `kwota = 60` zmieniła tylko `kwota`.

Konsekwencja: kolejność linii ma znaczenie. Program czyta kod od góry, więc wartość zmiennej zależy od tego, które przypisanie wykonało się ostatnie.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 19,
      "status": "covered",
      "section_ids": [
        "sec-04-czym-jest-dana"
      ],
      "explanation": "Definicja, przykłady (imię, kwota, tak/nie), analogia do arkusza oraz wyjaśnienie, że rodzaj danej decyduje o dozwolonych działaniach."
    },
    {
      "question_id": 20,
      "status": "covered",
      "section_ids": [
        "sec-04-czym-jest-zmienna"
      ],
      "explanation": "Zmienna jako nazwane miejsce na jedną daną, z przykładem odczytu, użycia w obliczeniach i zmiany wartości przy stałej nazwie."
    },
    {
      "question_id": 21,
      "status": "covered",
      "section_ids": [
        "sec-04-zmienna-jako-pudelko-z-etykieta"
      ],
      "explanation": "Etykieta, zawartość, podmiana wartości i niezależność kopii są wyjaśnione, z diagramem i przykładem."
    },
    {
      "question_id": 22,
      "status": "covered",
      "section_ids": [
        "sec-04-liczba-a-tekst"
      ],
      "explanation": "Różnica pokazana przez zapis (cudzysłów), tabelę i przykład; wyjaśniono, że liczbę można dzielić, a tekstu nie, oraz wspomniano TypeError."
    },
    {
      "question_id": 23,
      "status": "covered",
      "section_ids": [
        "sec-04-czym-jest-typ-danych"
      ],
      "explanation": "Definicja typu, tabela str/int/float/bool i użycie type() z przykładem wyniku."
    },
    {
      "question_id": 24,
      "status": "covered",
      "section_ids": [
        "sec-04-wartosc-logiczna-prawda-falsz"
      ],
      "explanation": "Dwie wartości True/False, zastosowanie tak/nie, typ bool, różnica względem tekstu \"True\" i przykład."
    },
    {
      "question_id": 25,
      "status": "covered",
      "section_ids": [
        "sec-04-przypisanie-wartosci-do-zmiennej"
      ],
      "explanation": "Cel przypisania, znak =, podmiana istniejącej wartości i kopiowanie wartości innej zmiennej z przykładem."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-16",
      "status": "brak",
      "explanation": "Ta zapowiedź dotyczy dalszych działów; w dziale 04 kod już jest i nie ma jej co spełniać, ale nie ma też odniesienia do niej."
    },
    {
      "reference_id": "ref-41",
      "status": "brak",
      "explanation": "Żadna sekcja nie pokazuje komunikatu o błędzie w pliku kasa.py."
    },
    {
      "reference_id": "ref-44",
      "status": "spełniona",
      "section_id": "sec-04-czym-jest-zmienna",
      "quote": "nazwane miejsce w pamięci programu, w którym leży jedna dana"
    },
    {
      "reference_id": "ref-45",
      "status": "spełniona",
      "section_id": "sec-04-czym-jest-typ-danych",
      "quote": "Oto podstawowe typy Pythona"
    },
    {
      "reference_id": "ref-47",
      "status": "spełniona",
      "section_id": "sec-04-przypisanie-wartosci-do-zmiennej",
      "quote": "Zapisujesz je znakiem `=`. Po lewej stoi nazwa, po prawej wartość"
    },
    {
      "reference_id": "ref-51",
      "status": "brak",
      "explanation": "Sekcja liczba-a-tekst powtarza obietnicę „za chwilę”, ale nigdzie nie pokazano TypeError w pliku czytelnika; sama obietnica została tylko przesunięta."
    },
    {
      "reference_id": "ref-53",
      "status": "spełniona",
      "section_id": "sec-04-czym-jest-typ-danych",
      "quote": "Typ danych to rodzaj wartości, który mówi Pythonowi, czym ta wartość jest"
    },
    {
      "reference_id": "ref-58",
      "status": "spełniona",
      "section_id": "sec-04-wartosc-logiczna-prawda-falsz",
      "quote": "ma tylko dwie możliwe wartości: prawda albo fałsz"
    }
  ]
}
````
