# Krok 1221 · autor_ściągawki

Węzeł: `cheatsheet` · dział: — · pytanie: — · próba: —

## Prompt

````text
Przygotuj ściągawkę do tutorialu: Programowanie od podstaw.
Czytelnik: osoba spoza IT, poziom: początkujący. Przeczytał tutorial i wraca do ściągawki w pracy.

Wybierz najważniejsze rzeczy, do których się wraca: to, co trzeba pamiętać albo szybko skopiować.
Forma wynika z tematu (komendy, szkielety kodu, reguły decyzji, złożoności, składnia): dobierz ją sam.
- Najwyżej 50 pozycji, w kolejności tutorialu; KAŻDY dział ma mieć co najmniej jedną.
  Pomiń rzeczy trywialne i powtórzenia.
- label: czego szukam, maks. 8 słów (np. "Cofnąć ostatni commit, zachowując zmiany").
- snippet: najwyżej 3 linie SKOPIOWANE z kodu wskazanej sekcji (możesz pomijać linie i wstawić `...`,
  ale nie dopisuj nowych ani nie zmieniaj istniejących); pusty, gdy pozycja to reguła; language: jeden z
  python.
- note: jedno zdanie: kiedy to stosować albo na co uważać.
- section: id sekcji w nawiasach kwadratowych, z której pozycja pochodzi.

TUTORIAL:
## Dział 01. Czym jest programowanie
[sec-01-czym-jest-program-komputerowy] Czym jest program komputerowy: Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
[sec-01-czym-jest-programowanie] Czym jest programowanie: Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.
[sec-01-kim-jest-programista] Kim jest programista: Programista zamienia potrzebę na działający program, a pisanie kodu to tylko jeden z etapów tej pracy.
[sec-01-czym-jest-jezyk-programowania] Czym jest język programowania: Język programowania to ścisły zestaw słów i reguł zapisu, dzięki któremu człowiek wyraża instrukcje tak, by komputer wykonał je jednoznacznie.
```python
print("Cześć, Wspólna Kasa!")
```
[sec-01-po-co-komputerowi-precyzja] Po co komputerowi precyzja: Komputer wykonuje dokładnie to, co zapisano, więc każdy szczegół, który człowiek by sobie dopowiedział, trzeba podać wprost.
[sec-01-program-a-aplikacja] Program a aplikacja: Aplikacja to program z oprawą dla użytkownika, więc każda aplikacja jest programem, ale nie odwrotnie.
## Dział 02. Algorytmy i myślenie krokowe
[sec-02-czym-jest-algorytm] Czym jest algorytm: Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
[sec-02-przepis-jako-algorytm] Przepis jako algorytm: Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
[sec-02-kolejnosc-krokow-algorytmu] Kolejność kroków algorytmu: Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.
[sec-02-czym-jest-schemat-blokowy] Czym jest schemat blokowy: Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, dzięki czemu rozgałęzienia, powroty i koniec widać, zanim powstanie kod.
[sec-02-podzial-problemu-na-czesci] Podział problemu na części: Dziel problem na części z jasnym wejściem i wynikiem, aż każdą da się opisać jednym zdaniem i sprawdzić osobno.
[sec-02-poprawny-algorytm] Poprawny algorytm: Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, także w przypadkach brzegowych.
```python
# poza kanonem: udział w groszach, dzielenie całkowite
def udzial(suma_gr, osoby):
    return suma_gr // osoby

print(udzial(12000, 4) * 4)
print(udzial(10000, 3) * 3)
```
## Dział 03. Kod i jego uruchamianie
[sec-03-czym-jest-kod-zrodlowy] Czym jest kod źródłowy: Kod źródłowy to zwykły plik tekstowy z instrukcjami w języku programowania, który człowiek pisze i czyta, a komputer wykonuje dopiero za pośrednictwem innego programu.
```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```
[sec-03-do-czego-sluzy-edytor] Do czego służy edytor: Edytor kodu to wygodne narzędzie do pisania zwykłego pliku tekstowego z kodem: koloruje, numeruje i podpowiada, ale niczego nie uruchamia.
[sec-03-co-znaczy-uruchomic-program] Co znaczy uruchomić program: Uruchomienie programu to polecenie, by Python wykonał instrukcje z pliku po kolei, a sam plik pozostaje bez zmian.
```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
```
[sec-03-kompilator-i-interpreter] Kompilator i interpreter: Kompilator tłumaczy cały kod na osobny plik przed startem, a interpreter wykonuje kod na bieżąco, dlatego w Pythonie wystarczy zapisać i uruchomić.
[sec-03-co-to-jest-blad-w-programie] Co to jest błąd w programie: Błąd to rozbieżność między zamiarem a działaniem programu: czasem zatrzymuje go komunikat, a czasem zły wynik pojawia się po cichu.
```python
# poza kanonem: błąd w dzieleniu
print("Wspólna Kasa")
print(300 / 2)   # 300 zł na troje osób
```
[sec-03-do-czego-sluza-komentarze] Do czego służą komentarze: Komentarz zaczyna się od `#`, jest pomijany przez Pythona i ma wyjaśniać powód, a nie powtarzać kod; po zmianie kodu trzeba go zaktualizować.
```python
# rozlicz.py - rozliczenie wspólnych wydatków
print("Wspólna Kasa")
# udział na dwie osoby
print(300 / 3)  # 300 zł na troje osób
# print(300 / 2)  <- ta linia jest wyłączona
```
## Dział 04. Dane i zmienne
[sec-04-czym-jest-dana] Czym jest dana: Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.
```python
# poza kanonem
print("Ania")       # tekst: imię
print(45.5)         # liczba: kwota
print(True)         # prawda albo fałsz: czy zapłacono
print(45.5 + 10)    # z liczbą można liczyć
```
[sec-04-czym-jest-zmienna] Czym jest zmienna: Zmienna to nazwa, pod którą program przechowuje daną, żeby móc jej użyć wielokrotnie i w razie potrzeby zmienić.
```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(imie, kwota, zaplacono)
kwota = 60
print(kwota + 10)
```
[sec-04-zmienna-jako-pudelko-z-etykieta] Zmienna jako pudełko z etykietą: Zmienna to pudełko z etykietą: nazwa zostaje, w środku jest jedna wartość, którą można podmienić, a kopie są niezależne.
```python
# poza kanonem
kwota_stara = 45.5
kwota = kwota_stara
kwota = 60
print(kwota_stara, kwota)
```
[sec-04-liczba-a-tekst] Liczba a tekst: Cudzysłów zmienia rodzaj danych: 45.5 to liczba, którą można dzielić, a "45.5" to tekst, którego dzielić się nie da.
```python
kwota = 45.5
imie = "Ania"
print(kwota / 2)
print(imie)
```
[sec-04-czym-jest-typ-danych] Czym jest typ danych: Typ danych to rodzaj wartości (str, int, float, bool), który decyduje o tym, jakie działania są na niej możliwe.
```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(type(imie))
print(type(kwota))
print(type(zaplacono))
```
[sec-04-wartosc-logiczna-prawda-falsz] Wartość logiczna prawda/fałsz: Wartość logiczna (`bool`) to `True` albo `False`, zapisywane z wielkiej litery i bez cudzysłowu, a program używa jej do podejmowania decyzji.
```python
zaplacono = True
print(zaplacono)
zaplacono = False
print(zaplacono)
print(type(zaplacono))
```
[sec-04-przypisanie-wartosci-do-zmiennej] Przypisanie wartości do zmiennej: Przypisanie `=` to polecenie zapisania wartości z prawej strony pod nazwą z lewej, a o wartości zmiennej decyduje ostatnie wykonane przypisanie.
```python
kwota = 45.5
kwota_stara = kwota
kwota = 60
print(kwota)
print(kwota_stara)
```
## Dział 05. Operacje i decyzje
[sec-05-dzialania-matematyczne-w-programie] Działania matematyczne w programie: Python zna siedem podstawowych operatorów arytmetycznych (`+ - * / // % **`); na tekście dzielić się nie da, a `+` i `*` znaczą tam sklejanie i powtarzanie.
```python
kwota = 100
print(kwota / 3)
print(kwota // 3)
print(kwota % 3)
```
```python
print("Ania" + "Bartek")
print("Ha" * 3)
```
[sec-05-laczenie-tekstow] Łączenie tekstów: Plus skleja tylko tekst z tekstem, bez dodawania spacji, a liczbę trzeba przed sklejeniem zamienić funkcją str() albo użyć zapisu z f.
```python
imie = "Ania"
kwota = 45.5
print(imie + " zapłaciła " + str(kwota) + " zł")
print(imie + "zapłaciła")
```
[sec-05-porownywanie-wartosci] Porównywanie wartości: Operatory porównania (`==`, `!=`, `<`, `>`, `<=`, `>=`) dają `True` albo `False`, a `==` pyta o równość, w przeciwieństwie do `=`, które przypisuje.
```python
kwota = 45.5
print(kwota == 45.5)
print(kwota != 45.5)
print(kwota > 50)
print(kwota <= 45.5)
print("Ania" == "ania")
print("45.5" == 45.5)
```
[sec-05-instrukcja-warunkowa-jesli-to] Instrukcja warunkowa „jeśli… to…”: Instrukcja `if` wykonuje wcięte pod nią linie tylko wtedy, gdy warunek daje `True`; w przeciwnym razie Python je pomija.
```python
kwota = 45.5
if kwota > 40:
    print("Kwota do sprawdzenia")
if kwota > 100:
    print("Bardzo duża kwota")
print("Koniec")
```
[sec-05-czesc-w-przeciwnym-razie] Część „w przeciwnym razie”: `else` to droga „w przeciwnym razie”: wykonuje się tylko wtedy, gdy warunek z `if` jest fałszywy, więc program zawsze wybiera dokładnie jedną z dwóch dróg.
```python
kwota = 45.5
if kwota > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print("Koniec")
```
[sec-05-operatory-i-oraz-lub] Operatory „i” oraz „lub”: `and` wymaga prawdziwości obu warunków, a `or` wystarczy jeden prawdziwy, żeby całość dała `True`.
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
## Dział 06. Powtarzanie i kolekcje
[sec-06-czym-jest-petla] Czym jest pętla: Pętla powtarza wcięty fragment kodu, a `for` robi to raz dla każdego elementu zestawu danych, po czym kończy pracę.
```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print("Cześć,", imie)
print("Koniec")
```
[sec-06-kiedy-siegnac-po-petle] Kiedy sięgnąć po pętlę: Gdy kopiujesz linię i zmieniasz w niej tylko jedną wartość, użyj pętli: jeden zapis obsłuży dowolną liczbę elementów.
```python
osoby = ["Ania", "Bartek", "Celina"]
liczba_osob = 3
for imie in osoby:
    print(imie, "płaci", 300 / liczba_osob)
```
[sec-06-petla-nieskonczona] Pętla nieskończona: Pętla nieskończona nigdy nie osiąga warunku zakończenia, więc program się „zawiesza”; zatrzymasz go Ctrl+C, a przy każdym `while` pytaj, co w końcu zmieni warunek na fałsz.
```python
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```
[sec-06-czym-jest-lista-danych] Czym jest lista danych: Lista to jedna zmienna z wieloma wartościami w ustalonej kolejności, zapisana w nawiasach kwadratowych, z elementami rozdzielonymi przecinkami.
```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby)
print(len(osoby))
```
[sec-06-odczyt-elementu-listy] Odczyt elementu listy: Element listy pobierasz indeksem w nawiasach kwadratowych, licząc od zera, a `-1` oznacza ostatni element.
```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby[0])
print(osoby[2])
print(osoby[-1])
```
[sec-06-petla-po-elementach-listy] Pętla po elementach listy: Pętla `for element in lista:` wykonuje blok raz dla każdego elementu, w kolejności listy, i sama kończy pracę po ostatnim.
```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print(imie)
print("Koniec")
```
```python
wydatki = ...
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(suma)
```
## Dział 07. Funkcje i porządek w kodzie
[sec-07-czym-jest-funkcja] Czym jest funkcja: Funkcję definiujesz raz przez def, a uruchamiasz każdym wywołaniem jej nazwy z nawiasami.
```python
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

print(suma([45.5, 20, 12.5]))
```
[sec-07-po-co-dzielic-program-na-funkcje] Po co dzielić program na funkcje: Funkcje dają kodowi nazwy i jedno miejsce na każdą logikę, więc program jest czytelniejszy, a poprawki robisz raz.
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
[sec-07-czym-sa-argumenty-funkcji] Czym są argumenty funkcji: Argumenty to wartości podane przy wywołaniu, które trafiają do parametrów funkcji według kolejności lub nazwy, a ich liczba musi pasować do definicji.
```python
def na_osobe(suma, osoby):
    return suma / osoby

print(na_osobe(300, 4))
print(na_osobe(osoby=4, suma=300))
```
[sec-07-zwracanie-wyniku-przez-funkcje] Zwracanie wyniku przez funkcję: Return oddaje wartość wywołującemu, po czym kończy funkcję, a print tylko pokazuje tekst i niczego nie zwraca (funkcja bez return daje None).
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
[sec-07-czytelne-nazwy-zmiennych-i-funkcji] Czytelne nazwy zmiennych i funkcji: Nazywaj funkcję według tego, co robi, a zmienną według tego, co trzyma, bo kod czyta się częściej, niż pisze.
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
[sec-07-ponowne-uzycie-kodu] Ponowne użycie kodu: Funkcję piszesz raz, a wywołujesz z różnymi danymi, więc poprawka w jednym miejscu naprawia wszystkie użycia.
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
## Dział 08. Współpraca programu z użytkownikiem
[sec-08-dane-wejsciowe-programu] Dane wejściowe programu: Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.
```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    ...
```
[sec-08-dane-wyjsciowe-programu] Dane wyjściowe programu: Dane wyjściowe to wynik, który program oddaje na zewnątrz (ekran, plik, inny program), a dobre wyjście jest opisane tak, by zrozumiał je człowiek.
```python
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wypisz_na_osobe(78, 3)
```
[sec-08-pytanie-uzytkownika-o-informacje] Pytanie użytkownika o informację: Funkcja input wypisuje pytanie i zwraca odpowiedź użytkownika zawsze jako tekst, więc liczbę trzeba zamienić przez float().
```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    kwota = float(kwota)
    ...
```
[sec-08-czym-jest-plik] Czym jest plik: Plik przechowuje dane na dysku po zakończeniu programu, a program otwiera go przez open (najlepiej z with) w trybie czytania, zapisu lub dopisywania i pamięta, że dostaje z niego tekst.
```python
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")
```
[sec-08-czym-jest-interfejs-uzytkownika] Czym jest interfejs użytkownika: Interfejs użytkownika to wszystko, przez co człowiek rozmawia z programem: pytania, które program zadaje, i wyniki, które pokazuje, więc powinny być jasne dla kogoś, kto nie zna kodu.
```python
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```
[sec-08-po-co-sprawdzac-dane-uzytkownika] Po co sprawdzać dane użytkownika: Sprawdzaj dane od użytkownika zaraz po wpisaniu, bo człowiek może wpisać coś nieoczekiwanego, a zły wpis powinien dostać komunikat i drugą szansę.
```python
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

for tekst in ["45.5", "abc", "-5", "0", ""]:
    print(repr(tekst), sprawdz_kwote(tekst))
```
## Dział 09. Błędy i dobre praktyki
[sec-09-blad-skladni-a-blad-logiczny] Błąd składni a błąd logiczny: Błąd składni zatrzymuje program przed startem z komunikatem, a błąd logiczny daje po cichu zły wynik, który musisz wychwycić sam.
```python
print("start")
suma = 45.5 + 20
if suma > 10
    print("dużo")
```
```python
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)
```
[sec-09-jak-czytac-komunikat-o-bledzie] Jak czytać komunikat o błędzie: Komunikat czytaj od dołu: ostatnia linia mówi, co się stało, a ślad nad nią wskazuje plik i numer linii, gdzie to szukać.
```python
# blad_pusta.py - Traceback: dzielenie przez zero
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))
```
[sec-09-czym-jest-testowanie-programu] Czym jest testowanie programu: Test to zapisane oczekiwanie: znasz poprawny wynik z góry, a komputer sprawdza go za Ciebie po każdej zmianie kodu.
```python
def na_osobe(suma, osoby):
    return suma / osoby

assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0
assert na_osobe(100, 4) == 25
print("Wszystkie testy przeszły")
```
[sec-09-czym-jest-debugowanie] Czym jest debugowanie: Debugowanie to zawężanie miejsca błędu przez sprawdzanie, co program faktycznie robi, np. wartości wypisane przez print, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.
```python
def na_osobe(suma, osoby):
    return suma / osoby

suma = 78.0
liczba_osob = 2
print("DEBUG suma:", suma)
print("DEBUG liczba_osob:", liczba_osob)
print(na_osobe(suma, liczba_osob))
```
[sec-09-po-co-zapisywac-wersje-kodu] Po co zapisywać wersje kodu: Commit zapisuje działającą wersję kodu z opisem, dzięki czemu zawsze możesz do niej wrócić i sprawdzić, kiedy coś się zepsuło.
[sec-09-szukanie-rozwiazan-w-internecie] Szukanie rozwiązań w internecie: Szukaj po ostatniej linii komunikatu i nazwie języka, oceniaj źródła i nigdy nie wklejaj skopiowanego kodu bez zrozumienia.
## Dział 10. Programowanie w praktyce
[sec-10-programy-uzywane-na-co-dzien] Programy używane na co dzień: Programy, których używasz codziennie, to te same proste klocki (dane, decyzje, pętle, funkcje, pliki) w większej skali i z ładniejszym interfejsem.
[sec-10-strona-internetowa-a-aplikacja-mobilna] Strona internetowa a aplikacja mobilna: Strona otwiera się w przeglądarce bez instalacji, a aplikacja mobilna jest zainstalowana w telefonie i lepiej korzysta z jego możliwości, ale obie działają według schematu wejście, przetwarzanie, wyjście.
[sec-10-od-pomyslu-do-dzialajacego-programu] Od pomysłu do działającego programu: Buduj program małymi kawałkami: opisz, napisz, sprawdź, zapisz commit, dopiero potem dokładaj następny.
```python
def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...
```
[sec-10-umiejetnosci-poza-kodowaniem] Umiejętności poza kodowaniem: Pisanie kodu to część pracy programisty; równie ważne są rozumienie problemu, komunikacja, cierpliwość i umiejętność uczenia się.
[sec-10-od-czego-zaczac-nauke] Od czego zacząć naukę: Naukę zacznij od jednego małego, własnego problemu i jednego języka, a kod pisz i uruchamiaj regularnie, po kawałku.
[sec-10-automatyzacja-prostych-zadan] Automatyzacja prostych zadań: Automatyzuj małe, częste zadania o jasnych regułach: raz opisane w pętli i funkcji działają tak samo dla trzech danych i dla tysiąca.
```python
wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.0},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.0},
           {"kto": "Celina", "opis": "bilety", "kwota": 15.0}]
osoby = ["Ania", "Bartek", "Celina"]
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(f"Razem: {suma} zł")
print(f"Na osobę: {suma / len(osoby)} zł")
```
````

## Odpowiedź

````json
{
  "items": [
    {
      "label": "Wypisać tekst na ekran",
      "note": "print pokazuje tekst w cudzysłowie; komputer wykonuje dokładnie to, co zapisano.",
      "section": "sec-01-czym-jest-jezyk-programowania",
      "snippet": "print(\"Cześć, Wspólna Kasa!\")",
      "language": "python"
    },
    {
      "label": "Definicja poprawnego algorytmu",
      "note": "Musi kończyć pracę i dawać zgodny ze specyfikacją wynik dla każdych dozwolonych danych, także brzegowych.",
      "section": "sec-02-poprawny-algorytm",
      "snippet": "",
      "language": ""
    },
    {
      "label": "Dzielenie całkowite dla groszy",
      "note": "Sprawdź przypadki brzegowe: przy dzieleniu 10000 na 3 osoby suma udziałów nie musi się zgadzać.",
      "section": "sec-02-poprawny-algorytm",
      "snippet": "def udzial(suma_gr, osoby):\n    return suma_gr // osoby",
      "language": "python"
    },
    {
      "label": "Kolejność kroków w algorytmie",
      "note": "Krok potrzebujący wyniku innego kroku musi stać po nim; komputer nie poprawi kolejności za Ciebie.",
      "section": "sec-02-kolejnosc-krokow-algorytmu",
      "snippet": "",
      "language": ""
    },
    {
      "label": "Uruchomić skrypt Pythona",
      "note": "Kod to zwykły plik tekstowy; edytor go tylko pisze, a uruchamia go Python.",
      "section": "sec-03-czym-jest-kod-zrodlowy",
      "snippet": "# rozlicz.py\nprint(\"Wspólna Kasa\")\nprint(300 / 3)",
      "language": "python"
    },
    {
      "label": "Komentarz i wyłączanie linii",
      "note": "Komentarz wyjaśnia powód, nie powtarza kodu; po zmianie kodu zaktualizuj go.",
      "section": "sec-03-do-czego-sluza-komentarze",
      "snippet": "# udział na dwie osoby\nprint(300 / 3)  # 300 zł na troje osób\n# print(300 / 2)  <- ta linia jest wyłączona",
      "language": "python"
    },
    {
      "label": "Błąd bez komunikatu (zły wynik)",
      "note": "Program może działać i po cichu liczyć źle, np. dzielić przez 2 zamiast przez 3 — sprawdzaj wyniki.",
      "section": "sec-03-co-to-jest-blad-w-programie",
      "snippet": "print(300 / 2)   # 300 zł na troje osób",
      "language": "python"
    },
    {
      "label": "Zmienne: tworzenie i podmiana",
      "note": "Nazwa zostaje, wartość można podmienić; liczy się ostatnie przypisanie.",
      "section": "sec-04-czym-jest-zmienna",
      "snippet": "imie = \"Ania\"\nkwota = 45.5\nkwota = 60",
      "language": "python"
    },
    {
      "label": "Kopia zmiennej jest niezależna",
      "note": "Zmiana kwoty po przypisaniu nie rusza kwota_stara.",
      "section": "sec-04-przypisanie-wartosci-do-zmiennej",
      "snippet": "kwota_stara = kwota\nkwota = 60\nprint(kwota_stara)",
      "language": "python"
    },
    {
      "label": "Liczba czy tekst: cudzysłów",
      "note": "45.5 to liczba, którą można dzielić; \"45.5\" to tekst.",
      "section": "sec-04-liczba-a-tekst",
      "snippet": "kwota = 45.5\nprint(kwota / 2)",
      "language": "python"
    },
    {
      "label": "Sprawdzić typ danych",
      "note": "Typy: str, int, float, bool; typ decyduje, co można z wartością zrobić.",
      "section": "sec-04-czym-jest-typ-danych",
      "snippet": "print(type(imie))\nprint(type(kwota))",
      "language": "python"
    },
    {
      "label": "Wartości logiczne True i False",
      "note": "Pisz z wielkiej litery i bez cudzysłowu.",
      "section": "sec-04-wartosc-logiczna-prawda-falsz",
      "snippet": "zaplacono = True\nzaplacono = False",
      "language": "python"
    },
    {
      "label": "Operatory arytmetyczne: / // %",
      "note": "/ dzieli dokładnie, // daje część całkowitą, % resztę; dostępne też + - * **.",
      "section": "sec-05-dzialania-matematyczne-w-programie",
      "snippet": "print(kwota / 3)\nprint(kwota // 3)\nprint(kwota % 3)",
      "language": "python"
    },
    {
      "label": "Sklejanie i powtarzanie tekstu",
      "note": "Na tekście + skleja, * powtarza; dzielić tekstu się nie da.",
      "section": "sec-05-dzialania-matematyczne-w-programie",
      "snippet": "print(\"Ania\" + \"Bartek\")\nprint(\"Ha\" * 3)",
      "language": "python"
    },
    {
      "label": "Skleić tekst z liczbą",
      "note": "Liczbę zamień przez str(); plus nie dodaje spacji, więc wstaw je sam.",
      "section": "sec-05-laczenie-tekstow",
      "snippet": "print(imie + \" zapłaciła \" + str(kwota) + \" zł\")",
      "language": "python"
    },
    {
      "label": "Porównania: == a =",
      "note": "== pyta o równość, = przypisuje; \"45.5\" nie równa się 45.5, a wielkość liter ma znaczenie.",
      "section": "sec-05-porownywanie-wartosci",
      "snippet": "print(kwota == 45.5)\nprint(\"Ania\" == \"ania\")\nprint(\"45.5\" == 45.5)",
      "language": "python"
    },
    {
      "label": "Jeśli… to… (if)",
      "note": "Wcięte linie wykonują się tylko, gdy warunek jest True; koniec wcięcia to koniec bloku.",
      "section": "sec-05-instrukcja-warunkowa-jesli-to",
      "snippet": "if kwota > 40:\n    print(\"Kwota do sprawdzenia\")",
      "language": "python"
    },
    {
      "label": "Dwie drogi: if i else",
      "note": "Wykona się dokładnie jedna z dwóch dróg.",
      "section": "sec-05-czesc-w-przeciwnym-razie",
      "snippet": "if kwota > 100:\n    print(\"Bardzo duża kwota\")\nelse:\n    print(\"Zwykła kwota\")",
      "language": "python"
    },
    {
      "label": "Łączenie warunków: and, or",
      "note": "and wymaga obu warunków prawdziwych, or wystarczy jednego.",
      "section": "sec-05-operatory-i-oraz-lub",
      "snippet": "print(kwota > 40 and liczba_osob > 5)\nprint(kwota > 100 or liczba_osob == 3)",
      "language": "python"
    },
    {
      "label": "Pętla for po liście",
      "note": "Blok wykona się raz dla każdego elementu i sam się zakończy; użyj, gdy kopiujesz linię zmieniając jedną wartość.",
      "section": "sec-06-czym-jest-petla",
      "snippet": "for imie in osoby:\n    print(\"Cześć,\", imie)\nprint(\"Koniec\")",
      "language": "python"
    },
    {
      "label": "Pętla nieskończona: zatrzymanie",
      "note": "Ctrl+C przerywa program; przy każdym while pytaj, co w końcu zmieni warunek na fałsz.",
      "section": "sec-06-petla-nieskonczona",
      "snippet": "while True:\n    print(\"Liczę wydatki...\")\n    time.sleep(1)",
      "language": "python"
    },
    {
      "label": "Lista i jej długość",
      "note": "Elementy w nawiasach kwadratowych rozdzielone przecinkami; len liczy elementy.",
      "section": "sec-06-czym-jest-lista-danych",
      "snippet": "osoby = [\"Ania\", \"Bartek\", \"Celina\"]\nprint(len(osoby))",
      "language": "python"
    },
    {
      "label": "Element listy po indeksie",
      "note": "Liczenie zaczyna się od 0, a -1 to ostatni element.",
      "section": "sec-06-odczyt-elementu-listy",
      "snippet": "print(osoby[0])\nprint(osoby[-1])",
      "language": "python"
    },
    {
      "label": "Zsumować wartości w pętli",
      "note": "Zacznij od zera i dodawaj każdy element do sumy.",
      "section": "sec-06-petla-po-elementach-listy",
      "snippet": "suma = 0\nfor wydatek in wydatki:\n    suma = suma + wydatek[\"kwota\"]",
      "language": "python"
    },
    {
      "label": "Zdefiniować i wywołać funkcję",
      "note": "def definiuje raz, a wywołanie z nawiasami uruchamia; ciało funkcji jest wcięte.",
      "section": "sec-07-czym-jest-funkcja",
      "snippet": "def suma(wydatki):\n    ...\nprint(suma([45.5, 20, 12.5]))",
      "language": "python"
    },
    {
      "label": "Funkcje składane w jednym wyrażeniu",
      "note": "Jedna logika w jednym miejscu: poprawka w funkcji naprawia wszystkie użycia.",
      "section": "sec-07-po-co-dzielic-program-na-funkcje",
      "snippet": "print(\"Mazury:\", na_osobe(suma(mazury), 3))\nprint(\"Tatry:\", na_osobe(suma(tatry), 4))",
      "language": "python"
    },
    {
      "label": "Argumenty według kolejności lub nazwy",
      "note": "Liczba argumentów musi pasować do definicji funkcji.",
      "section": "sec-07-czym-sa-argumenty-funkcji",
      "snippet": "print(na_osobe(300, 4))\nprint(na_osobe(osoby=4, suma=300))",
      "language": "python"
    },
    {
      "label": "return a print",
      "note": "return oddaje wartość i kończy funkcję; print tylko pokazuje, a funkcja bez return daje None.",
      "section": "sec-07-zwracanie-wyniku-przez-funkcje",
      "snippet": "wynik = na_osobe(300, 4)\nnic = wypisz_na_osobe(300, 4)\nprint(nic)",
      "language": "python"
    },
    {
      "label": "Jak nazywać funkcje i zmienne",
      "note": "Funkcję nazwij od tego, co robi, zmienną od tego, co trzyma; kod czyta się częściej, niż pisze.",
      "section": "sec-07-czytelne-nazwy-zmiennych-i-funkcji",
      "snippet": "def suma_wydatkow(wydatki):\n    ...\ndef udzial_na_osobe(suma, liczba_osob):",
      "language": "python"
    },
    {
      "label": "Użyć funkcji z różnymi danymi",
      "note": "Napisz raz, wywołuj wielokrotnie z innymi danymi.",
      "section": "sec-07-ponowne-uzycie-kodu",
      "snippet": "print(udzial_na_osobe(suma_wydatkow(mazury), 3))\nprint(udzial_na_osobe(suma_wydatkow(tatry), 4))",
      "language": "python"
    },
    {
      "label": "Zapytać użytkownika o dane",
      "note": "input wypisuje pytanie i zwraca odpowiedź zawsze jako tekst.",
      "section": "sec-08-pytanie-uzytkownika-o-informacje",
      "snippet": "kto = input(\"Kto zapłacił? \")\nkwota = input(\"Ile zapłacił? \")\nkwota = float(kwota)",
      "language": "python"
    },
    {
      "label": "Wynik opisany dla człowieka",
      "note": "Dane wyjściowe opisuj tak, by zrozumiał je ktoś, kto nie zna kodu.",
      "section": "sec-08-dane-wyjsciowe-programu",
      "snippet": "def wypisz_na_osobe(suma, osoby):\n    print(suma / osoby)",
      "language": "python"
    },
    {
      "label": "Zapisać i odczytać plik",
      "note": "Użyj with; tryby: \"w\" zapis (nadpisuje), \"r\" czytanie, \"a\" dopisywanie; z pliku dostajesz tekst.",
      "section": "sec-08-czym-jest-plik",
      "snippet": "with open(\"wydatki.txt\", \"w\", encoding=\"utf-8\") as plik:\n    plik.write(\"Ania;120.5\\n\")\n    tekst = plik.read()",
      "language": "python"
    },
    {
      "label": "Czytelne podsumowanie z f-stringiem",
      "note": "Interfejs ma być jasny dla osoby spoza kodu: nagłówek i opisane linie.",
      "section": "sec-08-czym-jest-interfejs-uzytkownika",
      "snippet": "print(\"=== Wspólna Kasa ===\")\nfor wydatek in wydatki:\n    print(f\"{wydatek['kto']}: {wydatek['kwota']} zł\")",
      "language": "python"
    },
    {
      "label": "Sprawdzić, czy wpisano poprawną kwotę",
      "note": "Waliduj wpis od razu; przy złym daj komunikat i drugą szansę.",
      "section": "sec-08-po-co-sprawdzac-dane-uzytkownika",
      "snippet": "if not tekst.replace(\".\", \"\", 1).isdigit():\n    return False\nreturn float(tekst) > 0",
      "language": "python"
    },
    {
      "label": "Błąd składni a logiczny",
      "note": "Składni zatrzymuje program przed startem (tu brak dwukropka po if); logiczny daje po cichu zły wynik.",
      "section": "sec-09-blad-skladni-a-blad-logiczny",
      "snippet": "if suma > 10\n    print(\"dużo\")",
      "language": "python"
    },
    {
      "label": "Czytać komunikat o błędzie",
      "note": "Czytaj od dołu: ostatnia linia mówi, co się stało, wyżej jest plik i numer linii.",
      "section": "sec-09-jak-czytac-komunikat-o-bledzie",
      "snippet": "",
      "language": ""
    },
    {
      "label": "Test przez assert",
      "note": "Zapisz znany poprawny wynik i uruchamiaj po każdej zmianie kodu.",
      "section": "sec-09-czym-jest-testowanie-programu",
      "snippet": "assert na_osobe(78, 3) == 26\nassert na_osobe(0, 4) == 0\nprint(\"Wszystkie testy przeszły\")",
      "language": "python"
    },
    {
      "label": "Debugowanie printami",
      "note": "Wypisuj wartości, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem.",
      "section": "sec-09-czym-jest-debugowanie",
      "snippet": "print(\"DEBUG suma:\", suma)\nprint(\"DEBUG liczba_osob:\", liczba_osob)",
      "language": "python"
    },
    {
      "label": "Kiedy zrobić commit",
      "note": "Commit zapisuje działającą wersję z opisem, do której zawsze możesz wrócić.",
      "section": "sec-09-po-co-zapisywac-wersje-kodu",
      "snippet": "",
      "language": ""
    },
    {
      "label": "Jak szukać rozwiązania błędu",
      "note": "Szukaj po ostatniej linii komunikatu i nazwie języka; nie wklejaj kodu, którego nie rozumiesz.",
      "section": "sec-09-szukanie-rozwiazan-w-internecie",
      "snippet": "",
      "language": ""
    },
    {
      "label": "Schemat każdego programu",
      "note": "Strona i aplikacja mobilna działają tak samo: wejście, przetwarzanie, wyjście.",
      "section": "sec-10-strona-internetowa-a-aplikacja-mobilna",
      "snippet": "",
      "language": ""
    },
    {
      "label": "Budować program małymi kawałkami",
      "note": "Opisz, napisz, sprawdź, zrób commit, dopiero potem następny kawałek.",
      "section": "sec-10-od-pomyslu-do-dzialajacego-programu",
      "snippet": "def saldo_osoby(wydatki, kto, liczba_osob):\n    # ile zapłacił kto minus jego równy udział\n    ...",
      "language": "python"
    },
    {
      "label": "Od czego zacząć naukę",
      "note": "Jeden mały własny problem, jeden język, kod pisany i uruchamiany regularnie.",
      "section": "sec-10-od-czego-zaczac-nauke",
      "snippet": "",
      "language": ""
    },
    {
      "label": "Zautomatyzować proste rozliczenie",
      "note": "Pętla plus podział przez len(osoby) działa tak samo dla trzech danych i dla tysiąca.",
      "section": "sec-10-automatyzacja-prostych-zadan",
      "snippet": "print(f\"Razem: {suma} zł\")\nprint(f\"Na osobę: {suma / len(osoby)} zł\")",
      "language": "python"
    }
  ]
}
````
