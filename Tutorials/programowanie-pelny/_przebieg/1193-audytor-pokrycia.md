# Krok 1193 · audytor_pokrycia

Węzeł: `coverage` · dział: 8 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 44. Czym są dane wejściowe programu?
  odpowiedź: Dane wejściowe to informacje, które program dostaje z zewnątrz, zamiast mieć je zapisane w kodzie. Mogą pochodzić od użytkownika, z pliku albo z innego programu. Dzięki nim ten sam kod działa na różnych danych bez edycji. Program nie kontroluje, co dostanie, więc musi je sprawdzać.
  sekcje pisarza: sec-08-dane-wejsciowe-programu
- 45. Czym są dane wyjściowe programu?
  odpowiedź: Dane wyjściowe to wszystko, co program oddaje na zewnątrz po wykonaniu pracy: tekst na ekranie, zapisany plik albo dane dla innego programu. Bez nich wynik obliczeń zostałby w pamięci i zniknął po zakończeniu programu. Najprostszy sposób ich pokazania to `print`.
  sekcje pisarza: sec-08-dane-wyjsciowe-programu
- 46. Jak program może zapytać użytkownika o informację?
  odpowiedź: Program pyta użytkownika funkcją input: wypisuje pytanie, czeka na odpowiedź zakończoną Enterem i oddaje ją jako wartość. Odpowiedź zawsze jest tekstem, więc liczbę trzeba zamienić np. przez float(). Dzięki temu kod jest ten sam, a dane zmieniają się przy każdym uruchomieniu.
  sekcje pisarza: sec-08-pytanie-uzytkownika-o-informacje
- 47. Czym jest plik i jak program może z niego korzystać?
  odpowiedź: Plik to nazwana porcja danych zapisana na dysku, która przetrwa zakończenie programu, w przeciwieństwie do zmiennych. Program otwiera plik funkcją open w wybranym trybie (czytanie, zapis, dopisywanie), czyta albo zapisuje tekst i zamyka go, najlepiej przez blok with. Dzięki temu plik służy zarówno jako źródło danych wejściowych, jak i miejsce zapisu wyników.
  sekcje pisarza: sec-08-czym-jest-plik
- 48. Czym jest interfejs użytkownika?
  odpowiedź: Interfejs użytkownika to całe miejsce spotkania człowieka z programem: to, co program pokazuje, i to, jak przyjmuje polecenia oraz dane. Może być tekstowy (pytania i odpowiedzi w terminalu) albo graficzny (okna, przyciski). Dobry interfejs mówi wprost, czego oczekuje, i pokazuje wynik w zrozumiałej formie.
  sekcje pisarza: sec-08-czym-jest-interfejs-uzytkownika
- 49. Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?
  odpowiedź: Bo użytkownik może wpisać coś nieoczekiwanego: tekst zamiast liczby, wartość ujemną albo nic. Bez sprawdzenia program albo zatrzyma się z błędem, albo po cichu policzy zły wynik. Walidacja przy wejściu chroni resztę kodu i pozwala poprosić o poprawkę zamiast kończyć pracę.
  sekcje pisarza: sec-08-po-co-sprawdzac-dane-uzytkownika

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-13: „pytania do użytkownika” (zapowiedź dobudowania pytań do użytkownika jako oprawy programu); ma ją spełnić pytanie 46
- ref-14: „sprawdzanie danych” (zapowiedź dobudowania sprawdzania danych wpisanych przez użytkownika); ma ją spełnić pytanie 49
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-41: „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)
- ref-51: „U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika)
- ref-66: „w warsztacie poniżej dopisujesz do swojego skryptu linię” (zapowiedź warsztatu i skryptu, w którym czytelnik wywoła błąd TypeError)
- ref-93: „Za chwilę dopiszesz `na_osobe` i użyjesz obu” (zapowiedź ćwiczenia praktycznego z funkcją na_osobe)
- ref-96: „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” (własny plik funkcje.py, w którym czytelnik zobaczy błąd)
- ref-102: „Usuwamy ją w warsztacie poniżej.” (zapowiedź poprawienia błędnej ostatniej linii w warsztacie)
- ref-104: „gdy zajmiemy się pytaniem użytkownika o informację” (input i zapytanie użytkownika); ma ją spełnić pytanie 46
- ref-105: „opowiemy osobno, przy danych wyjściowych” (dane wyjściowe programu); ma ją spełnić pytanie 45
- ref-107: „Do plików wrócimy osobno” (pliki jako miejsce zapisu wyników); ma ją spełnić pytanie 47
- ref-108: „opiszemy przy interfejsie” (interfejs użytkownika, rozmowa z użytkownikiem); ma ją spełnić pytanie 48
- ref-110: „przykładzie, który będzie nam towarzyszył” (program „Wspólna Kasa” wracający w kolejnych sekcjach)
- ref-112: „o czym powiemy przy sprawdzaniu danych użytkownika” (walidacja danych wpisanych przez użytkownika); ma ją spełnić pytanie 49
- ref-115: „człowiek po drugiej stronie potrafi wpisać coś nieoczekiwanego” (sprawdzanie danych wpisanych przez użytkownika); ma ją spełnić pytanie 49

SEKCJE DZIAŁU 08 "Współpraca programu z użytkownikiem":
[sec-08-dane-wejsciowe-programu] ## Dane wejściowe programu
[[dane-wejsciowe|Dane wejściowe]] to wszystko, co program dostaje z zewnątrz, żeby mieć na czym pracować: wpisane słowo, liczba, zawartość pliku. Sam z siebie nie wie, kto zapłacił za zakupy ani ile, więc ktoś musi mu to podać.

Źródła są różne, ale idea ta sama: wartość pojawia się w programie, choć nie została zapisana w kodzie.

| Źródło | Przykład we „Wspólnej Kasie” |
|---|---|
| użytkownik | wpisuje imię i kwotę nowego wydatku |
| plik | `wydatki.csv` z listą dotychczasowych wydatków |
| inny program | dane wyeksportowane z aplikacji banku |

Do tej pory kwoty wpisywaliśmy w kodzie, np. `mazury = [45.5, 20, 12.5]`. Wtedy każda zmiana danych wymagała edycji programu. Dane wejściowe rozdzielają obie sprawy: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne.

Tak mogłoby wyglądać pobranie danych od użytkownika (szkic, do którego wrócimy, gdy zajmiemy się pytaniem użytkownika o informację):

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    ...
```

Ważna konsekwencja: program nie kontroluje, co dostanie. Ktoś może wpisać „abc” zamiast kwoty, a plik może być pusty. Dlatego dane wejściowe trzeba traktować ostrożnie i sprawdzać. O wyniku, który program oddaje na zewnątrz, opowiemy osobno, przy danych wyjściowych.

[sec-08-dane-wyjsciowe-programu] ## Dane wyjściowe programu
[[dane-wyjsciowe|Dane wyjściowe]] to wszystko, co program oddaje na zewnątrz: wynik obliczeń, komunikat, zapisany plik. To druga strona [[dane-wejsciowe|danych wejściowych]]: wejście wpuszcza informacje do programu, wyjście je z niego wypuszcza.

Bez wyjścia program mógłby liczyć, ale nikt by o tym nie wiedział. Wynik zamknięty w zmiennej znika, gdy program się kończy.

Wyjście ma kilka adresatów:

| Dokąd trafia wynik | Przykład we „Wspólnej Kasie” |
|---|---|
| ekran | komunikat „Na osobę wychodzi 26.0” |
| plik | zapisane rozliczenie wyjazdu |
| inny program | dane przekazane do aplikacji banku |

Na razie znasz tylko pierwszą drogę: `print` pokazuje wartość w terminalu. Robiłeś to już w funkcji `wypisz_na_osobe`, o której mówiliśmy przy zwracaniu wyniku (przypomnienie: `print` tylko pokazuje tekst, niczego nie zwraca).

```python
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wypisz_na_osobe(78, 3)
```

```text
26.0
```

Konsekwencja: o tym, co program wypisze, decydujesz Ty. Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. Do plików wrócimy osobno, a wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie.

[sec-08-pytanie-uzytkownika-o-informacje] ## Pytanie użytkownika o informację
Program pyta użytkownika funkcją [[input|input]]: wypisuje pytanie, czeka, aż ktoś wpisze odpowiedź i naciśnie Enter, a potem oddaje tę odpowiedź jako wartość. To najprostszy sposób, by [[dane-wejsciowe|dane wejściowe]] przyszły od człowieka.

Tekst w nawiasach to pytanie, które zobaczy użytkownik. Wynik `input` przypisujesz do zmiennej, jak każdą [[wartosc-zwracana|wartość zwracaną]]. Program stoi w miejscu, dopóki odpowiedź nie nadejdzie.

Pokażemy to na przykładzie, który będzie nam towarzyszył: „Wspólnej Kasie”, czyli programie do rozliczania wspólnych wydatków znajomych. Zaczynamy dobudowywać do niego pytania do użytkownika, a pierwsze dotyczy nowego wydatku:

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    kwota = float(kwota)
    ...
```

Pułapka: `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Dla Pythona to wciąż „45.5” w cudzysłowie, czyli tekst, którego nie da się dzielić ani dodawać do liczb (skończyłoby się to błędem [[typeerror|TypeError]]). Dlatego `float()` zamienia tekst na liczbę. Spacja na końcu pytania oddziela je od tego, co wpisze użytkownik.

Konsekwencja: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne. Ale `float("abc")` przerwie program błędem. Jak się przed tym bronić, pokażemy przy sprawdzaniu danych wpisanych przez użytkownika.

[sec-08-czym-jest-plik] ## Czym jest plik
[[plik|Plik]] to nazwana porcja danych zapisana na dysku, która istnieje także wtedy, gdy program już nie działa. Zmienne żyją tylko podczas pracy programu i znikają wraz z jego zakończeniem, a plik zostaje. Dlatego plik jest miejscem, z którego [[dane-wejsciowe|dane wejściowe]] przychodzą i do którego trafiają [[dane-wyjsciowe|dane wyjściowe]].

Program korzysta z pliku w trzech krokach: otwiera go funkcją `open`, czyta albo zapisuje, a na końcu zamyka. Blok `with` zamyka plik za Ciebie, nawet gdy coś pójdzie źle. Drugi argument `open` to [[tryb-otwarcia-pliku|tryb otwarcia]], czyli informacja, co zamierzasz z plikiem zrobić:

| Tryb | Znaczenie |
|---|---|
| `"r"` | czytanie (plik musi istnieć) |
| `"w"` | zapis od nowa, stara treść przepada |
| `"a"` | dopisywanie na końcu |

Argument `encoding="utf-8"` sprawia, że polskie litery zapiszą się i odczytają poprawnie.

```python
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")
```

```text
Ania;120.5
Bartek;45.5
```

Uwaga: plik przechowuje wyłącznie tekst, więc kwotę po wczytaniu trzeba znów zamienić przez `float()`, bo `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Pułapką jest tryb `"w"`, który kasuje starą zawartość. Zanim ktoś wpisze do pliku coś błędnego, warto dane sprawdzić, o czym powiemy przy sprawdzaniu danych użytkownika.

[sec-08-czym-jest-interfejs-uzytkownika] ## Czym jest interfejs użytkownika
[[interfejs-uzytkownika|Interfejs użytkownika]] to część programu, przez którą człowiek się z nim komunikuje: to, co program wyświetla, oraz sposób, w jaki przyjmuje od człowieka dane i polecenia. Użytkownik nie widzi kodu, widzi tylko interfejs.

Interfejs bywa różny. W [[interfejs-tekstowy|interfejsie tekstowym]], czyli takim, który działa w [[terminal|terminalu]] na samych napisach, program zadaje pytania, a Ty odpisujesz z klawiatury. W interfejsie graficznym są okna i przyciski. Nasza „Wspólna Kasa” zostaje przy wersji tekstowej, bo wystarczą do niej dwie znane już rzeczy: [[input|input]] do pytań i [[print|print]] do wyników.

Interfejs ma dwie strony: **wejście** (pytania, odpowiedzi) i **wyjście** (wyniki, komunikaty). To dokładnie [[dane-wejsciowe|dane wejściowe]] i [[dane-wyjsciowe|dane wyjściowe]], tylko widziane oczami człowieka. Stąd wniosek z wcześniejszych sekcji: suchy wynik nic nie mówi komuś, kto nie zna kodu, więc trzeba go opisać.

```python
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```

```text
=== Wspólna Kasa ===
Ania: 120.5 zł
Bartek: 45.5 zł
```

Konsekwencja: pytanie w rodzaju „Ile zapłacił? ” i czytelne podsumowanie to nie ozdoby, tylko część działania programu. Interfejs trzeba więc projektować, a człowiek po drugiej stronie potrafi wpisać coś nieoczekiwanego.

[sec-08-po-co-sprawdzac-dane-uzytkownika] ## Po co sprawdzać dane użytkownika
Program powinien sprawdzać dane od użytkownika, bo człowiek potrafi wpisać coś, czego kod się nie spodziewał, a wtedy program albo się zatrzyma, albo policzy coś błędnego.

Ta kontrola to [[walidacja-danych|walidacja]]: sprawdzenie, czy wpisana wartość nadaje się do dalszej pracy, zanim program jej użyje. Pamiętasz, że [[input|input]] zawsze zwraca tekst. Gdy ktoś na pytanie „Ile zapłacił?” wpisze `abc`, samo `float("abc")` przerwie program komunikatem o błędzie. A gdy wpisze `-5`, program nie zgłosi żadnego błędu i po cichu policzy złe saldo.

Dlatego sprawdzamy dane w miejscu, gdzie wchodzą do programu. Pokazuje to funkcja `sprawdz_kwote`, która odpowiada `True` albo `False`:

```python
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

for tekst in ["45.5", "abc", "-5", "0", ""]:
    print(repr(tekst), sprawdz_kwote(tekst))
```

```text
'45.5' True
'abc' False
'-5' False
'0' False
'' False
```

Pierwsza linia sprawdza, czy tekst składa się z cyfr (z najwyżej jedną kropką). Druga dopiero wtedy zamienia go na liczbę i pyta, czy jest dodatnia.

Konsekwencja: zły wpis nie kończy programu, tylko dostaje komunikat i kolejną szansę. Program, który sprawdza dane, jest odporny na pomyłki, a Ty masz pewność, że reszta kodu dostaje wartości, na które jest przygotowana.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 44,
      "status": "covered",
      "section_ids": [
        "sec-08-dane-wejsciowe-programu"
      ],
      "explanation": "Definicja, źródła (użytkownik, plik, inny program), rozdzielenie kodu od danych i konieczność sprawdzania są wyjaśnione."
    },
    {
      "question_id": 45,
      "status": "covered",
      "section_ids": [
        "sec-08-dane-wyjsciowe-programu"
      ],
      "explanation": "Definicja, adresaci wyjścia, uzasadnienie (wynik w zmiennej znika) i print jako najprostsza droga."
    },
    {
      "question_id": 46,
      "status": "covered",
      "section_ids": [
        "sec-08-pytanie-uzytkownika-o-informacje"
      ],
      "explanation": "Opisano działanie input, Enter, zwracanie wartości, pułapkę tekstu i konwersję float()."
    },
    {
      "question_id": 47,
      "status": "covered",
      "section_ids": [
        "sec-08-czym-jest-plik"
      ],
      "explanation": "Plik vs zmienne, open, tryby, with, zapis i odczyt, plik jako wejście i wyjście, pułapka trybu w."
    },
    {
      "question_id": 48,
      "status": "covered",
      "section_ids": [
        "sec-08-czym-jest-interfejs-uzytkownika"
      ],
      "explanation": "Definicja, tekstowy vs graficzny, wejście i wyjście, przykład z podsumowaniem oraz uzasadnienie wyboru tekstowego."
    },
    {
      "question_id": 49,
      "status": "covered",
      "section_ids": [
        "sec-08-po-co-sprawdzac-dane-uzytkownika"
      ],
      "explanation": "Wyjaśnia, że zły wpis zatrzymuje program lub daje cichy błąd (abc, -5), pokazuje przykład walidacji i korzyść dla reszty kodu."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-13",
      "status": "spełniona",
      "section_id": "sec-08-pytanie-uzytkownika-o-informacje",
      "quote": "Zaczynamy dobudowywać do niego pytania do użytkownika, a pierwsze dotyczy nowego wydatku",
      "explanation": ""
    },
    {
      "reference_id": "ref-14",
      "status": "spełniona",
      "section_id": "sec-08-po-co-sprawdzac-dane-uzytkownika",
      "quote": "Ta kontrola to walidacja: sprawdzenie, czy wpisana wartość nadaje się do dalszej pracy",
      "explanation": ""
    },
    {
      "reference_id": "ref-16",
      "status": "brak",
      "explanation": "W tym dziale kod już się pojawia, ale sekcje nie odnoszą się do tej zapowiedzi jako jej spełnienia; nic wprost jej nie domyka."
    },
    {
      "reference_id": "ref-41",
      "status": "brak",
      "explanation": "Żadna sekcja nie pokazuje komunikatu o błędzie w pliku kasa.py."
    },
    {
      "reference_id": "ref-51",
      "status": "brak",
      "explanation": "Brak warsztatu z wywołaniem TypeError u czytelnika w tym dziale."
    },
    {
      "reference_id": "ref-66",
      "status": "brak",
      "explanation": "Brak warsztatu, w którym czytelnik dopisuje linię wywołującą TypeError."
    },
    {
      "reference_id": "ref-93",
      "status": "brak",
      "explanation": "Funkcja na_osobe nie jest tu dopisywana ani używana w ćwiczeniu."
    },
    {
      "reference_id": "ref-96",
      "status": "brak",
      "explanation": "Brak pliku funkcje.py i błędu TypeError w tym dziale."
    },
    {
      "reference_id": "ref-102",
      "status": "brak",
      "explanation": "Brak warsztatu usuwającego błędną ostatnią linię."
    },
    {
      "reference_id": "ref-104",
      "status": "spełniona",
      "section_id": "sec-08-pytanie-uzytkownika-o-informacje",
      "quote": "Program pyta użytkownika funkcją input: wypisuje pytanie, czeka, aż ktoś wpisze odpowiedź",
      "explanation": ""
    },
    {
      "reference_id": "ref-105",
      "status": "spełniona",
      "section_id": "sec-08-dane-wyjsciowe-programu",
      "quote": "Dane wyjściowe to wszystko, co program oddaje na zewnątrz",
      "explanation": ""
    },
    {
      "reference_id": "ref-107",
      "status": "spełniona",
      "section_id": "sec-08-czym-jest-plik",
      "quote": "Plik to nazwana porcja danych zapisana na dysku, która istnieje także wtedy",
      "explanation": ""
    },
    {
      "reference_id": "ref-108",
      "status": "spełniona",
      "section_id": "sec-08-czym-jest-interfejs-uzytkownika",
      "quote": "Interfejs użytkownika to część programu, przez którą człowiek się z nim komunikuje",
      "explanation": ""
    },
    {
      "reference_id": "ref-110",
      "status": "spełniona",
      "section_id": "sec-08-pytanie-uzytkownika-o-informacje",
      "quote": "Pokażemy to na przykładzie, który będzie nam towarzyszył: „Wspólnej Kasie”",
      "explanation": ""
    },
    {
      "reference_id": "ref-112",
      "status": "spełniona",
      "section_id": "sec-08-po-co-sprawdzac-dane-uzytkownika",
      "quote": "Program powinien sprawdzać dane od użytkownika, bo człowiek potrafi wpisać coś, czego kod się nie spodziewał",
      "explanation": ""
    },
    {
      "reference_id": "ref-115",
      "status": "spełniona",
      "section_id": "sec-08-po-co-sprawdzac-dane-uzytkownika",
      "quote": "Gdy ktoś na pytanie „Ile zapłacił?” wpisze `abc`, samo `float(\"abc\")` przerwie program",
      "explanation": ""
    }
  ]
}
````
