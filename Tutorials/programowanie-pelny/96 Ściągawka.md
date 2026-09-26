# Ściągawka: Programowanie od podstaw

Najważniejsze rzeczy z tutorialu na jednej stronie. Każda pozycja prowadzi do sekcji, która ją wyjaśnia.

## 01. Wejdź w świat programowania

**Wypisać tekst na ekran**: print pokazuje tekst w cudzysłowie; komputer wykonuje dokładnie to, co zapisano. → [Poznaj język programowania](01%20Wejd%C5%BA%20w%20%C5%9Bwiat%20programowania.md#poznaj-język-programowania)

```python
print("Cześć, Wspólna Kasa!")
```

## 02. Myśl krok po kroku

**Definicja poprawnego algorytmu**: Musi kończyć pracę i dawać zgodny ze specyfikacją wynik dla każdych dozwolonych danych, także brzegowych. → [Sprawdź poprawność algorytmu](02%20My%C5%9Bl%20krok%20po%20kroku.md#sprawdź-poprawność-algorytmu)

**Dzielenie całkowite dla groszy**: Sprawdź przypadki brzegowe: przy dzieleniu 10000 na 3 osoby suma udziałów nie musi się zgadzać. → [Sprawdź poprawność algorytmu](02%20My%C5%9Bl%20krok%20po%20kroku.md#sprawdź-poprawność-algorytmu)

```python
def udzial(suma_gr, osoby):
    return suma_gr // osoby
```

**Kolejność kroków w algorytmie**: Krok potrzebujący wyniku innego kroku musi stać po nim; komputer nie poprawi kolejności za Ciebie. → [Pilnuj kolejności kroków](02%20My%C5%9Bl%20krok%20po%20kroku.md#pilnuj-kolejności-kroków)

## 03. Napisz i uruchom kod

**Uruchomić skrypt Pythona**: Kod to zwykły plik tekstowy; edytor go tylko pisze, a uruchamia go Python. → [Poznaj kod źródłowy](03%20Napisz%20i%20uruchom%20kod.md#poznaj-kod-źródłowy)

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

**Komentarz i wyłączanie linii**: Komentarz wyjaśnia powód, nie powtarza kodu; po zmianie kodu zaktualizuj go. → [Opisuj kod komentarzami](03%20Napisz%20i%20uruchom%20kod.md#opisuj-kod-komentarzami)

```python
# udział na dwie osoby
print(300 / 3)  # 300 zł na troje osób
# print(300 / 2)  <- ta linia jest wyłączona
```

**Błąd bez komunikatu (zły wynik)**: Program może działać i po cichu liczyć źle, np. dzielić przez 2 zamiast przez 3 — sprawdzaj wyniki. → [Rozpoznaj błąd w programie](03%20Napisz%20i%20uruchom%20kod.md#rozpoznaj-błąd-w-programie)

```python
print(300 / 2)   # 300 zł na troje osób
```

## 04. Zapamiętaj dane w zmiennych

**Zmienne: tworzenie i podmiana**: Nazwa zostaje, wartość można podmienić; liczy się ostatnie przypisanie. → [Nazwij swoją pierwszą zmienną](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#nazwij-swoją-pierwszą-zmienną)

```python
imie = "Ania"
kwota = 45.5
kwota = 60
```

**Kopia zmiennej jest niezależna**: Zmiana kwoty po przypisaniu nie rusza kwota_stara. → [Przypisz wartość zmiennej](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#przypisz-wartość-zmiennej)

```python
kwota_stara = kwota
kwota = 60
print(kwota_stara)
```

**Liczba czy tekst: cudzysłów**: 45.5 to liczba, którą można dzielić; "45.5" to tekst. → [Rozróżnij liczbę i tekst](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#rozróżnij-liczbę-i-tekst)

```python
kwota = 45.5
print(kwota / 2)
```

**Sprawdzić typ danych**: Typy: str, int, float, bool; typ decyduje, co można z wartością zrobić. → [Sprawdź typ danych](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#sprawdź-typ-danych)

```python
print(type(imie))
print(type(kwota))
```

**Wartości logiczne True i False**: Pisz z wielkiej litery i bez cudzysłowu. → [Użyj prawdy i fałszu](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#użyj-prawdy-i-fałszu)

```python
zaplacono = True
zaplacono = False
```

## 05. Podejmuj decyzje w programie

**Operatory arytmetyczne: / // %**: / dzieli dokładnie, // daje część całkowitą, % resztę; dostępne też + - * **. → [Wykonuj działania matematyczne](05%20Podejmuj%20decyzje%20w%20programie.md#wykonuj-działania-matematyczne)

```python
print(kwota / 3)
print(kwota // 3)
print(kwota % 3)
```

**Sklejanie i powtarzanie tekstu**: Na tekście + skleja, * powtarza; dzielić tekstu się nie da. → [Wykonuj działania matematyczne](05%20Podejmuj%20decyzje%20w%20programie.md#wykonuj-działania-matematyczne)

```python
print("Ania" + "Bartek")
print("Ha" * 3)
```

**Skleić tekst z liczbą**: Liczbę zamień przez str(); plus nie dodaje spacji, więc wstaw je sam. → [Połącz kilka tekstów](05%20Podejmuj%20decyzje%20w%20programie.md#połącz-kilka-tekstów)

```python
print(imie + " zapłaciła " + str(kwota) + " zł")
```

**Porównania: == a =**: == pyta o równość, = przypisuje; "45.5" nie równa się 45.5, a wielkość liter ma znaczenie. → [Porównaj dwie wartości](05%20Podejmuj%20decyzje%20w%20programie.md#porównaj-dwie-wartości)

```python
print(kwota == 45.5)
print("Ania" == "ania")
print("45.5" == 45.5)
```

**Jeśli… to… (if)**: Wcięte linie wykonują się tylko, gdy warunek jest True; koniec wcięcia to koniec bloku. → [Zapisz warunek z if](05%20Podejmuj%20decyzje%20w%20programie.md#zapisz-warunek-z-if)

```python
if kwota > 40:
    print("Kwota do sprawdzenia")
```

**Dwie drogi: if i else**: Wykona się dokładnie jedna z dwóch dróg. → [Dodaj drugą drogę](05%20Podejmuj%20decyzje%20w%20programie.md#dodaj-drugą-drogę)

```python
if kwota > 100:
    print("Bardzo duża kwota")
else:
```

**Łączenie warunków: and, or**: and wymaga obu warunków prawdziwych, or wystarczy jednego. → [Łącz warunki spójnikami](05%20Podejmuj%20decyzje%20w%20programie.md#łącz-warunki-spójnikami)

```python
print(kwota > 40 and liczba_osob > 5)
print(kwota > 100 or liczba_osob == 3)
```

## 06. Powtarzaj i zbieraj dane

**Pętla for po liście**: Blok wykona się raz dla każdego elementu i sam się zakończy; użyj, gdy kopiujesz linię zmieniając jedną wartość. → [Powtórz kod pętlą](06%20Powtarzaj%20i%20zbieraj%20dane.md#powtórz-kod-pętlą)

```python
for imie in osoby:
    print("Cześć,", imie)
print("Koniec")
```

**Pętla nieskończona: zatrzymanie**: Ctrl+C przerywa program; przy każdym while pytaj, co w końcu zmieni warunek na fałsz. → [Unikaj pętli nieskończonej](06%20Powtarzaj%20i%20zbieraj%20dane.md#unikaj-pętli-nieskończonej)

```python
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

**Lista i jej długość**: Elementy w nawiasach kwadratowych rozdzielone przecinkami; len liczy elementy. → [Zbierz dane w liście](06%20Powtarzaj%20i%20zbieraj%20dane.md#zbierz-dane-w-liście)

```python
osoby = ["Ania", "Bartek", "Celina"]
print(len(osoby))
```

**Element listy po indeksie**: Liczenie zaczyna się od 0, a -1 to ostatni element. → [Wybierz element z listy](06%20Powtarzaj%20i%20zbieraj%20dane.md#wybierz-element-z-listy)

```python
print(osoby[0])
print(osoby[-1])
```

**Zsumować wartości w pętli**: Zacznij od zera i dodawaj każdy element do sumy. → [Przejdź przez całą listę](06%20Powtarzaj%20i%20zbieraj%20dane.md#przejdź-przez-całą-listę)

```python
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
```

## 07. Uporządkuj kod funkcjami

**Zdefiniować i wywołać funkcję**: def definiuje raz, a wywołanie z nawiasami uruchamia; ciało funkcji jest wcięte. → [Zdefiniuj i wywołaj funkcję](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#zdefiniuj-i-wywołaj-funkcję)

```python
def suma(wydatki):
    ...
print(suma([45.5, 20, 12.5]))
```

**Funkcje składane w jednym wyrażeniu**: Jedna logika w jednym miejscu: poprawka w funkcji naprawia wszystkie użycia. → [Podziel program na funkcje](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#podziel-program-na-funkcje)

```python
print("Mazury:", na_osobe(suma(mazury), 3))
print("Tatry:", na_osobe(suma(tatry), 4))
```

**Argumenty według kolejności lub nazwy**: Liczba argumentów musi pasować do definicji funkcji. → [Przekaż funkcji argumenty](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#przekaż-funkcji-argumenty)

```python
print(na_osobe(300, 4))
print(na_osobe(osoby=4, suma=300))
```

**return a print**: return oddaje wartość i kończy funkcję; print tylko pokazuje, a funkcja bez return daje None. → [Odbierz wynik z funkcji](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#odbierz-wynik-z-funkcji)

```python
wynik = na_osobe(300, 4)
nic = wypisz_na_osobe(300, 4)
print(nic)
```

**Jak nazywać funkcje i zmienne**: Funkcję nazwij od tego, co robi, zmienną od tego, co trzyma; kod czyta się częściej, niż pisze. → [Nadawaj czytelne nazwy](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#nadawaj-czytelne-nazwy)

```python
def suma_wydatkow(wydatki):
    ...
def udzial_na_osobe(suma, liczba_osob):
```

**Użyć funkcji z różnymi danymi**: Napisz raz, wywołuj wielokrotnie z innymi danymi. → [Wykorzystaj kod ponownie](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#wykorzystaj-kod-ponownie)

```python
print(udzial_na_osobe(suma_wydatkow(mazury), 3))
print(udzial_na_osobe(suma_wydatkow(tatry), 4))
```

## 08. Porozmawiaj z użytkownikiem

**Zapytać użytkownika o dane**: input wypisuje pytanie i zwraca odpowiedź zawsze jako tekst. → [Zapytaj użytkownika o dane](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapytaj-użytkownika-o-dane)

```python
kto = input("Kto zapłacił? ")
kwota = input("Ile zapłacił? ")
kwota = float(kwota)
```

**Wynik opisany dla człowieka**: Dane wyjściowe opisuj tak, by zrozumiał je ktoś, kto nie zna kodu. → [Pokaż wynik programu](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#pokaż-wynik-programu)

```python
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)
```

**Zapisać i odczytać plik**: Użyj with; tryby: "w" zapis (nadpisuje), "r" czytanie, "a" dopisywanie; z pliku dostajesz tekst. → [Zapisz dane w pliku](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapisz-dane-w-pliku)

```python
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    tekst = plik.read()
```

**Czytelne podsumowanie z f-stringiem**: Interfejs ma być jasny dla osoby spoza kodu: nagłówek i opisane linie. → [Zaprojektuj jasny interfejs](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zaprojektuj-jasny-interfejs)

```python
print("=== Wspólna Kasa ===")
for wydatek in wydatki:
    print(f"{wydatek['kto']}: {wydatek['kwota']} zł")
```

**Sprawdzić, czy wpisano poprawną kwotę**: Waliduj wpis od razu; przy złym daj komunikat i drugą szansę. → [Weryfikuj wpisane dane](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#weryfikuj-wpisane-dane)

```python
if not tekst.replace(".", "", 1).isdigit():
    return False
return float(tekst) > 0
```

## 09. Oswój błędy w kodzie

**Błąd składni a logiczny**: Składni zatrzymuje program przed startem (tu brak dwukropka po if); logiczny daje po cichu zły wynik. → [Rozróżnij dwa rodzaje błędów](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#rozróżnij-dwa-rodzaje-błędów)

```python
if suma > 10
    print("dużo")
```

**Czytać komunikat o błędzie**: Czytaj od dołu: ostatnia linia mówi, co się stało, wyżej jest plik i numer linii. → [Czytaj komunikat o błędzie](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#czytaj-komunikat-o-błędzie)

**Test przez assert**: Zapisz znany poprawny wynik i uruchamiaj po każdej zmianie kodu. → [Przetestuj swój program](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#przetestuj-swój-program)

```python
assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0
print("Wszystkie testy przeszły")
```

**Debugowanie printami**: Wypisuj wartości, aż znajdziesz pierwszy krok, w którym rzeczywistość rozjeżdża się z oczekiwaniem. → [Wytrop błąd krok po kroku](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#wytrop-błąd-krok-po-kroku)

```python
print("DEBUG suma:", suma)
print("DEBUG liczba_osob:", liczba_osob)
```

**Kiedy zrobić commit**: Commit zapisuje działającą wersję z opisem, do której zawsze możesz wrócić. → [Zapisuj wersje kodu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#zapisuj-wersje-kodu)

**Jak szukać rozwiązania błędu**: Szukaj po ostatniej linii komunikatu i nazwie języka; nie wklejaj kodu, którego nie rozumiesz. → [Szukaj rozwiązań w sieci](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#szukaj-rozwiązań-w-sieci)

## 10. Zastosuj wiedzę w praktyce

**Schemat każdego programu**: Strona i aplikacja mobilna działają tak samo: wejście, przetwarzanie, wyjście. → [Przeanalizuj stronę i aplikację mobilną](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md#przeanalizuj-stronę-i-aplikację-mobilną)

**Budować program małymi kawałkami**: Opisz, napisz, sprawdź, zrób commit, dopiero potem następny kawałek. → [Dojdź od pomysłu do programu](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md#dojdź-od-pomysłu-do-programu)

```python
def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...
```

**Od czego zacząć naukę**: Jeden mały własny problem, jeden język, kod pisany i uruchamiany regularnie. → [Zacznij naukę od małego problemu](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md#zacznij-naukę-od-małego-problemu)

**Zautomatyzować proste rozliczenie**: Pętla plus podział przez len(osoby) działa tak samo dla trzech danych i dla tysiąca. → [Zautomatyzuj proste zadania](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md#zautomatyzuj-proste-zadania)

```python
print(f"Razem: {suma} zł")
print(f"Na osobę: {suma / len(osoby)} zł")
```
