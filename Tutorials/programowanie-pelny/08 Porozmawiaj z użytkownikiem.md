# Porozmawiaj z użytkownikiem

Dotąd Twoje programy liczyły na danych wpisanych na sztywno w kodzie, a prawdziwy program musi umieć rozmawiać z człowiekiem. W tym dziale nauczysz się przyjmować dane od użytkownika, pokazywać mu wyniki, zapisywać je w pliku i wczytywać z powrotem oraz odrzucać błędnie wpisane wartości. Wykorzystasz przy tym zmienne, decyzje, pętle i funkcje z poprzednich działów. W przykładzie „Wspólna Kasa” program wczyta wydatki z pliku, zapyta o nowy wydatek i sprawdzi kwotę, a w warsztacie zbudujesz to krok po kroku, łącznie z ponownym pytaniem po wpisaniu tekstu zamiast liczby.

```text
użytkownik --wpisuje--> [ program ] --pokazuje--> użytkownik
                        ^    |
                    wczytuje zapisuje
                        |    v
                        [ plik ]
```

**W tym dziale:**

- [Przyjmij dane z zewnątrz](#przyjmij-dane-z-zewnątrz)
- [Pokaż wynik programu](#pokaż-wynik-programu)
- [Zapytaj użytkownika o dane](#zapytaj-użytkownika-o-dane)
- [Zapisz dane w pliku](#zapisz-dane-w-pliku)
- [Zaprojektuj jasny interfejs](#zaprojektuj-jasny-interfejs)
- [Weryfikuj wpisane dane](#weryfikuj-wpisane-dane)

**Warsztat, punkt startowy:** pliki z końca działu 07: `funkcje.py`, `kasa.py`, `nieskonczona.py` ([treść](99%20Warsztat.md#po-dziale-07)).

## Przyjmij dane z zewnątrz

[Dane wejściowe](00%20Glosariusz.md#dane-wejściowe) to wszystko, co program dostaje z zewnątrz, żeby mieć na czym pracować: wpisane słowo, liczba, zawartość pliku. Sam z siebie nie wie, kto zapłacił za zakupy ani ile, więc ktoś musi mu to podać.

Źródła są różne, ale idea ta sama: wartość pojawia się w programie, choć nie została zapisana w kodzie.

| Źródło | Przykład we „Wspólnej Kasie” |
|---|---|
| użytkownik | wpisuje imię i kwotę nowego wydatku |
| [plik](00%20Glosariusz.md#plik) | `wydatki.csv` z listą dotychczasowych wydatków |
| inny program | dane wyeksportowane z aplikacji banku |

[Do tej pory kwoty wpisywaliśmy w kodzie](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#lm-51), np. `mazury = [45.5, 20, 12.5]`. Wtedy każda zmiana danych wymagała edycji programu. Dane wejściowe rozdzielają obie sprawy: <a id="lm-52"></a>kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne.

Tak mogłoby wyglądać pobranie danych od użytkownika (szkic, do którego wrócimy, [gdy zajmiemy się pytaniem użytkownika o informację](#ref-104)):

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    ...
```

Ważna konsekwencja: program nie kontroluje, co dostanie. Ktoś może wpisać „abc” zamiast kwoty, a plik może być pusty. Dlatego dane wejściowe trzeba traktować ostrożnie i sprawdzać. O wyniku, który program oddaje na zewnątrz, [opowiemy osobno, przy danych wyjściowych](#ref-105).

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#08-porozmawiaj-z-użytkownikiem)_

> **Pułapka: `input` zawsze zwraca tekst, nawet dla liczb.** Wpisane `45.5` trafia do `kwota` jako tekst "45.5", a nie liczba. Dodawanie kwot da błąd albo sklei napisy ("20" + "5" = "205"), a porównania będą działać alfabetycznie. Przed liczeniem trzeba świadomie zamienić tekst na liczbę, np. `float(kwota)`.

## Pokaż wynik programu

<a id="ref-105"></a>[Dane wyjściowe](00%20Glosariusz.md#dane-wyjściowe) to wszystko, co program oddaje na zewnątrz: wynik obliczeń, komunikat, zapisany plik. To druga strona danych wejściowych: wejście wpuszcza informacje do programu, wyjście je z niego wypuszcza.

Bez wyjścia program mógłby liczyć, ale nikt by o tym nie wiedział. Wynik zamknięty w zmiennej znika, gdy program się kończy.

Wyjście ma kilka adresatów:

| Dokąd trafia wynik | Przykład we „Wspólnej Kasie” |
|---|---|
| ekran | komunikat „Na osobę wychodzi 26.0” |
| plik | zapisane rozliczenie wyjazdu |
| inny program | dane przekazane do aplikacji banku |

Na razie znasz tylko pierwszą drogę: `print` pokazuje wartość w [terminalu](00%20Glosariusz.md#terminal). Robiłeś to już w funkcji `wypisz_na_osobe`, [o której mówiliśmy przy zwracaniu wyniku](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#lm-49) (przypomnienie: `print` tylko pokazuje tekst, niczego nie zwraca).

```python
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wypisz_na_osobe(78, 3)
```

```text
26.0
```

Konsekwencja: o tym, co program wypisze, decydujesz Ty. <a id="lm-53"></a>Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. [Do plików wrócimy osobno](#ref-107), a wygląd całej rozmowy z użytkownikiem [opiszemy przy interfejsie](#ref-108).

> **Z przymrużeniem oka:** Program, który wszystko policzył, ale niczego nie wypisał, przypomina drzewo przewracające się w lesie: nikt tego nie słyszał, więc trudno dowieść, że w ogóle coś się stało. `print` to świadek.

## Zapytaj użytkownika o dane

<a id="ref-104"></a>Program pyta użytkownika funkcją [input](00%20Glosariusz.md#input): wypisuje pytanie, czeka, aż ktoś wpisze odpowiedź i naciśnie Enter, a potem oddaje tę odpowiedź jako wartość. To najprostszy sposób, by dane wejściowe przyszły od człowieka.

Tekst w nawiasach to pytanie, które zobaczy użytkownik. Wynik `input` przypisujesz do zmiennej, jak każdą [wartość zwracaną](00%20Glosariusz.md#wartość-zwracana). Program stoi w miejscu, dopóki odpowiedź nie nadejdzie.

Pokażemy to na [przykładzie, który będzie nam towarzyszył](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#ref-110): „Wspólnej Kasie”, czyli programie do rozliczania wspólnych wydatków znajomych. <a id="ref-13"></a>Zaczynamy dobudowywać do niego pytania do użytkownika, a pierwsze dotyczy nowego wydatku:

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    kwota = float(kwota)
    ...
```

<a id="lm-54"></a>Pułapka: `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Dla Pythona to wciąż „45.5” w cudzysłowie, czyli tekst, którego nie da się dzielić ani dodawać do liczb (skończyłoby się to błędem [TypeError](00%20Glosariusz.md#typeerror)). Dlatego `float()` zamienia tekst na liczbę. Spacja na końcu pytania oddziela je od tego, co wpisze użytkownik.

Konsekwencja: [kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne](#lm-52). Ale `float("abc")` przerwie program błędem. Jak się przed tym bronić, pokażemy przy sprawdzaniu danych wpisanych przez użytkownika.

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `pytaj.py`.** Nowy skrypt z dwoma pytaniami do użytkownika.

```python
# pytaj.py - Wspólna Kasa pyta o wydatek
kto = input("Kto zapłacił? ")
kwota = float(input("Ile zapłacił? "))
print(f"Zapisano: {kto}, {kwota} zł")
```

**Krok 2. Uruchom.** Uruchamiamy i wpisujemy Ania oraz 45.5.

```bash
python pytaj.py
```

Wynik:

```text
Kto zapłacił? Ania
Ile zapłacił? 45.5
Zapisano: Ania, 45.5 zł
```

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#08-porozmawiaj-z-użytkownikiem)_

> **Z życia wzięte:** W małym skrypcie do zestawień pytałem operatora o dwie liczby przez `input` i dodawałem je do siebie. Przy wartościach 10 i 5 wynik brzmiał 105, bo obie odpowiedzi były tekstem, więc plus je skleił. Nie było żadnego błędu, więc raport z takimi sumami trafił dalej i ktoś zauważył problem dopiero przy sprawdzaniu. Od tamtej pory każdą odpowiedź z `input` od razu zamieniam na właściwy typ, w tej samej linii lub zaraz po niej.

## Zapisz dane w pliku

<a id="ref-107"></a>Plik to nazwana porcja danych zapisana na dysku, która istnieje także wtedy, gdy program już nie działa. Zmienne żyją tylko podczas pracy programu i znikają wraz z jego zakończeniem, a plik zostaje. Dlatego plik jest miejscem, z którego dane wejściowe przychodzą i do którego trafiają dane wyjściowe.

Program korzysta z pliku w trzech krokach: otwiera go funkcją `open`, czyta albo zapisuje, a na końcu zamyka. Blok `with` zamyka plik za Ciebie, nawet gdy coś pójdzie źle. Drugi argument `open` to [tryb otwarcia](00%20Glosariusz.md#tryb-otwarcia-pliku), czyli informacja, co zamierzasz z plikiem zrobić:

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

Uwaga: plik przechowuje wyłącznie tekst, więc kwotę po wczytaniu trzeba znów zamienić przez `float()`, bo `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Pułapką jest tryb `"w"`, który kasuje starą zawartość. Zanim ktoś wpisze do pliku coś błędnego, warto dane sprawdzić, [o czym powiemy przy sprawdzaniu danych użytkownika](#ref-112).

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `plik.py`.** Zapisujemy dwa wydatki i czytamy je z pliku.

```python
# plik.py - Wspólna Kasa zapisuje wydatki do pliku i wczytuje je z powrotem
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")
```

**Krok 2. Uruchom.** Uruchamiamy skrypt; obok skryptu pojawi się plik wydatki.txt.

```bash
python plik.py
```

Wynik:

```text
Ania;120.5
Bartek;45.5
```

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#08-porozmawiaj-z-użytkownikiem)_

> **Wtręt:** Marta miała w `wydatki.txt` rozliczenie z trzech miesięcy. Żeby dodać jeszcze jeden zakup, otworzyła plik w trybie `"w"`, bo tak robiła w poprzednim przykładzie, i zapisała jedną linię. Po chwili w pliku była tylko ta jedna linia, a trzy miesiące zniknęły. Tryb `"w"` zaczyna od pustej kartki, więc do dopisywania na końcu potrzebny był `"a"`.

**Ilustracja:** _Zmienne jak napisy na tablicy: po skończonej pracy znikają. Plik jak zeszyt: leży dalej._

Tekst alternatywny: Woźny w klasie ściera gąbką napisy z tablicy, a na pobliskiej ławce spokojnie leży zamknięty zeszyt.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Jasna klasa po lekcjach. Uśmiechnięty woźny w granatowym fartuchu ściera gąbką kredowe napisy z dużej zielonej tablicy, na której widać tylko abstrakcyjne bazgroły i cyfry bez czytelnego tekstu. Na ławce tuż obok leży zamknięty gruby zeszyt z musztardowo-żółtą okładką i zakładką w kolorze koralowym, nietknięty. Przez okno wpada ciepłe popołudniowe światło.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/08-zapisz-dane-w-pliku-1.png`

</details>

> **Pułapka: Ścieżka względna zależy od folderu uruchomienia.** `open("wydatki.txt", ...)` szuka i tworzy plik w bieżącym folderze roboczym, a nie tam, gdzie leży skrypt. Uruchomiony z innego miejsca program zapisze plik gdzie indziej, a tryb `"r"` zgłosi brak pliku, choć plik istnieje. Uruchamiaj program zawsze z tego samego folderu albo podaj pełną ścieżkę.

## Zaprojektuj jasny interfejs

<a id="ref-108"></a>[Interfejs użytkownika](00%20Glosariusz.md#interfejs-użytkownika) to część programu, przez którą człowiek się z nim komunikuje: to, co program wyświetla, oraz sposób, w jaki przyjmuje od człowieka dane i polecenia. Użytkownik nie widzi kodu, widzi tylko interfejs.

Interfejs bywa różny. W [interfejsie tekstowym](00%20Glosariusz.md#interfejs-tekstowy), czyli takim, który działa w terminalu na samych napisach, program zadaje pytania, a Ty odpisujesz z klawiatury. W interfejsie graficznym są okna i przyciski. Nasza „Wspólna Kasa” zostaje przy wersji tekstowej, bo wystarczą do niej dwie znane już rzeczy: input do pytań i [print](00%20Glosariusz.md#print) do wyników.

Interfejs ma dwie strony: **wejście** (pytania, odpowiedzi) i **wyjście** (wyniki, komunikaty). To dokładnie dane wejściowe i dane wyjściowe, tylko widziane oczami człowieka. Stąd wniosek z wcześniejszych sekcji: [suchy wynik nic nie mówi komuś, kto nie zna kodu](#lm-53), więc trzeba go opisać.

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

Konsekwencja: pytanie w rodzaju „Ile zapłacił? ” i czytelne podsumowanie to nie ozdoby, tylko część działania programu. Interfejs trzeba więc projektować, a [człowiek po drugiej stronie potrafi wpisać coś nieoczekiwanego](#ref-115).

> **Warsztat: zrób u siebie**

**Krok 1. Utwórz plik `interfejs.py`.** Nowy plik z opisanym wyjściem programu.

```python
# interfejs.py - Wspólna Kasa pokazuje czytelne podsumowanie
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```

**Krok 2. Uruchom.** Uruchamiamy i oglądamy interfejs.

```bash
python interfejs.py
```

Wynik:

```text
=== Wspólna Kasa ===
Ania: 120.5 zł
Bartek: 45.5 zł
```

<details>
<summary>Na marginesie: Mysz i okna na pokazie z 1968 roku</summary>

9 grudnia 1968 roku Douglas Engelbart pokazał w San Francisco system, w którym po raz pierwszy publicznie użyto myszy do sterowania komputerem. Na jednym ekranie były też okna z tekstem i połączenia między dokumentami. Pokaz nazwano później „matką wszystkich demonstracji”. Przez kolejne dekady interfejs, który dziś wydaje się oczywisty, był dopiero wymyślany.

Źródło: [The Mother of All Demos – Wikipedia](https://en.wikipedia.org/wiki/The_Mother_of_All_Demos)

</details>

> **Z przymrużeniem oka:** Interfejs to lada w sklepie: klient nie widzi magazynu ani zaplecza, widzi tylko ladę i sprzedawcę. Jeśli lada jest zawalona kartonami, nikt nie zapyta, jak świetnie posegregowany jest magazyn.

## Weryfikuj wpisane dane

<a id="ref-112"></a>Program powinien sprawdzać dane od użytkownika, bo człowiek potrafi wpisać coś, czego kod się nie spodziewał, a wtedy program albo się zatrzyma, albo policzy coś błędnego.

<a id="ref-115"></a><a id="ref-14"></a>Ta kontrola to [walidacja](00%20Glosariusz.md#walidacja-danych): sprawdzenie, czy wpisana wartość nadaje się do dalszej pracy, zanim program jej użyje. Pamiętasz, że input [zawsze zwraca tekst](#lm-54). Gdy ktoś na pytanie „Ile zapłacił?” wpisze `abc`, samo `float("abc")` przerwie program komunikatem o błędzie. A gdy wpisze `-5`, program nie zgłosi żadnego błędu i po cichu policzy złe saldo.

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

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `pytaj.py`.** Dodajemy sprawdzanie kwoty i ponowne pytanie przy błędnym wpisie.

```diff
-# pytaj.py - Wspólna Kasa pyta o wydatek
+# pytaj.py - Wspólna Kasa pyta o wydatek i sprawdza kwotę
+def sprawdz_kwote(tekst):
+    if not tekst.replace(".", "", 1).isdigit():
+        return False
+    return float(tekst) > 0
+
 kto = input("Kto zapłacił? ")
-kwota = float(input("Ile zapłacił? "))
+tekst = input("Ile zapłacił? ")
+while not sprawdz_kwote(tekst):
+    print("To nie jest poprawna kwota. Wpisz liczbę większą od zera, np. 45.5")
+    tekst = input("Ile zapłacił? ")
+kwota = float(tekst)
 print(f"Zapisano: {kto}, {kwota} zł")
```

<details>
<summary>Cały plik <code>pytaj.py</code> po zmianie</summary>

```python
# pytaj.py - Wspólna Kasa pyta o wydatek i sprawdza kwotę
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

kto = input("Kto zapłacił? ")
tekst = input("Ile zapłacił? ")
while not sprawdz_kwote(tekst):
    print("To nie jest poprawna kwota. Wpisz liczbę większą od zera, np. 45.5")
    tekst = input("Ile zapłacił? ")
kwota = float(tekst)
print(f"Zapisano: {kto}, {kwota} zł")
```

</details>

**Krok 2. Uruchom.** Wpisz kolejno: Ania, abc, -5, 45.5 i zobacz, jak program odrzuca złe kwoty.

```bash
python pytaj.py
```

Wynik:

```text
Kto zapłacił? Ania
Ile zapłacił? abc
To nie jest poprawna kwota. Wpisz liczbę większą od zera, np. 45.5
Ile zapłacił? -5
To nie jest poprawna kwota. Wpisz liczbę większą od zera, np. 45.5
Ile zapłacił? 45.5
Zapisano: Ania, 45.5 zł
```

## Co zapamiętać

- Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.
- Dane wyjściowe to wynik, który program oddaje na zewnątrz (ekran, plik, inny program), a dobre wyjście jest opisane tak, by zrozumiał je człowiek.
- Funkcja input wypisuje pytanie i zwraca odpowiedź użytkownika zawsze jako tekst, więc liczbę trzeba zamienić przez float().
- Plik przechowuje dane na dysku po zakończeniu programu, a program otwiera go przez open (najlepiej z with) w trybie czytania, zapisu lub dopisywania i pamięta, że dostaje z niego tekst.
- Interfejs użytkownika to wszystko, przez co człowiek rozmawia z programem: pytania, które program zadaje, i wyniki, które pokazuje, więc powinny być jasne dla kogoś, kto nie zna kodu.
- Sprawdzaj dane od użytkownika zaraz po wpisaniu, bo człowiek może wpisać coś nieoczekiwanego, a zły wpis powinien dostać komunikat i drugą szansę.

## Pytania sprawdzające

### 44. Czym są dane wejściowe programu?

<details>
<summary>Odpowiedź</summary>

Dane wejściowe to informacje, które program dostaje z zewnątrz, zamiast mieć je zapisane w kodzie. Mogą pochodzić od użytkownika, z pliku albo z innego programu. Dzięki nim ten sam kod działa na różnych danych bez edycji. Program nie kontroluje, co dostanie, więc musi je sprawdzać.

Zobacz: [sekcja „Przyjmij dane z zewnątrz”](#przyjmij-dane-z-zewnątrz).

</details>

### 45. Czym są dane wyjściowe programu?

<details>
<summary>Odpowiedź</summary>

Dane wyjściowe to wszystko, co program oddaje na zewnątrz po wykonaniu pracy: tekst na ekranie, zapisany plik albo dane dla innego programu. Bez nich wynik obliczeń zostałby w pamięci i zniknął po zakończeniu programu. Najprostszy sposób ich pokazania to `print`.

Zobacz: [sekcja „Pokaż wynik programu”](#pokaż-wynik-programu).

</details>

### 46. Jak program może zapytać użytkownika o informację?

<details>
<summary>Odpowiedź</summary>

Program pyta użytkownika funkcją input: wypisuje pytanie, czeka na odpowiedź zakończoną Enterem i oddaje ją jako wartość. Odpowiedź zawsze jest tekstem, więc liczbę trzeba zamienić np. przez float(). Dzięki temu kod jest ten sam, a dane zmieniają się przy każdym uruchomieniu.

Zobacz: [sekcja „Zapytaj użytkownika o dane”](#zapytaj-użytkownika-o-dane).

</details>

### 47. Czym jest plik i jak program może z niego korzystać?

<details>
<summary>Odpowiedź</summary>

Plik to nazwana porcja danych zapisana na dysku, która przetrwa zakończenie programu, w przeciwieństwie do zmiennych. Program otwiera plik funkcją open w wybranym trybie (czytanie, zapis, dopisywanie), czyta albo zapisuje tekst i zamyka go, najlepiej przez blok with. Dzięki temu plik służy zarówno jako źródło danych wejściowych, jak i miejsce zapisu wyników.

Zobacz: [sekcja „Zapisz dane w pliku”](#zapisz-dane-w-pliku).

</details>

### 48. Czym jest interfejs użytkownika?

<details>
<summary>Odpowiedź</summary>

Interfejs użytkownika to całe miejsce spotkania człowieka z programem: to, co program pokazuje, i to, jak przyjmuje polecenia oraz dane. Może być tekstowy (pytania i odpowiedzi w terminalu) albo graficzny (okna, przyciski). Dobry interfejs mówi wprost, czego oczekuje, i pokazuje wynik w zrozumiałej formie.

Zobacz: [sekcja „Zaprojektuj jasny interfejs”](#zaprojektuj-jasny-interfejs).

</details>

### 49. Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?

<details>
<summary>Odpowiedź</summary>

Bo użytkownik może wpisać coś nieoczekiwanego: tekst zamiast liczby, wartość ujemną albo nic. Bez sprawdzenia program albo zatrzyma się z błędem, albo po cichu policzy zły wynik. Walidacja przy wejściu chroni resztę kodu i pozwala poprosić o poprawkę zamiast kończyć pracę.

Zobacz: [sekcja „Weryfikuj wpisane dane”](#weryfikuj-wpisane-dane).

</details>
