# Przykład przewodni: Rozliczenie wspólnych wydatków „Wspólna Kasa”

Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.

**Dokąd zmierza:** Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.

## Plan przyrostów

| Dział | Co przybywa |
|---|---|
| [01. Wejdź w świat programowania](01%20Wejd%C5%BA%20w%20%C5%9Bwiat%20programowania.md) | Przedstawiamy problem: rozliczanie wydatków na wyjeździe w arkuszu jest żmudne, więc opisujemy, co miałby robić program „Wspólna Kasa” i kto (programista) go napisze, jeszcze bez kodu. |
| [02. Myśl krok po kroku](02%20My%C5%9Bl%20krok%20po%20kroku.md) | Zapisujemy rozliczenie jako algorytm krok po kroku i schemat blokowy (zsumuj, podziel, porównaj wpłaty z udziałem), dzieląc problem na części, które później staną się funkcjami. |
| [03. Napisz i uruchom kod](03%20Napisz%20i%20uruchom%20kod.md) | Powstaje pierwszy plik rozlicz.py w edytorze VS Code z komentarzami; uruchamiamy go interpreterem Pythona i widzimy pierwszy celowy błąd. |
| [04. Zapamiętaj dane w zmiennych](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md) | Do rozlicz.py trafiają zmienne: imię, opis i kwota pojedynczego wydatku, różnica między tekstem a liczbą oraz wartość logiczna „czy zapłacono”. |
| [05. Podejmuj decyzje w programie](05%20Podejmuj%20decyzje%20w%20programie.md) | Program liczy udział jednej osoby, skleja tekst podsumowania i decyduje if/else oraz operatorami and/or, czy ktoś jest winien pieniądze, czy ma dostać zwrot. |
| [06. Powtarzaj i zbieraj dane](06%20Powtarzaj%20i%20zbieraj%20dane.md) | Pojedyncze zmienne zastępuje lista wydatków i lista osób; pętla for sumuje kwoty i liczy saldo każdego uczestnika, a pętla nieskończona pojawia się jako ostrzeżenie. |
| [07. Uporządkuj kod funkcjami](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md) | Kod dzieli się na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby z czytelnymi nazwami, argumentami i zwracanymi wynikami, gotowe do ponownego użycia. |
| [08. Porozmawiaj z użytkownikiem](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md) | Program wczytuje wydatki z pliku wydatki.csv, pyta użytkownika o nowy wydatek przez zapytaj_o_wydatek, waliduje kwotę w sprawdz_kwote i drukuje wynik jako prosty interfejs tekstowy. |
| [09. Oswój błędy w kodzie](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md) | Naprawiamy błąd logiczny (np. dzielenie przez zero przy pustej liście), czytamy komunikaty błędów, dodajemy test_rozlicz.py, debugujemy i zapisujemy wersje w repozytorium Git. |
| [10. Zastosuj wiedzę w praktyce](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md) | Oceniamy gotowe narzędzie i pomysły na rozwój: wersja webowa lub mobilna, eksport podsumowania, automatyczne wysyłanie e-mailem, oraz plan dalszej nauki i automatyzacji własnych zadań czytelnika. |

## Stan kodu po ostatnim dziale

Szkic, nie działający kod: nazwy i sygnatury, których trzymają się przykłady w tekście.

### `dlugi.py`

```python
def wypisz_dlugi(wydatki, osoby):
    # dla każdej osoby: ile dopłaca albo dostaje
    ...
```

- **wypisz_dlugi** (funkcja): Własna funkcja czytelnika, która wypisuje saldo każdej osoby. Wprowadzony: [10 › Zacznij naukę od małego problemu](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md#zacznij-naukę-od-małego-problemu).

### `funkcje.py`

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...

def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def na_osobe(suma, osoby):
    return suma / osoby

def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)
```

- **suma_wydatkow** (funkcja): Sumuje listę kwot; czytelniejsza nazwa dla funkcji suma. Wprowadzony: [07 › Nadawaj czytelne nazwy](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#nadawaj-czytelne-nazwy).
- **udzial_na_osobe** (funkcja): Dzieli sumę przez liczbę osób; czytelniejsza nazwa dla na_osobe. Wprowadzony: [07 › Nadawaj czytelne nazwy](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#nadawaj-czytelne-nazwy).
- **saldo_osoby** (funkcja): Liczy, ile ktoś zapłacił ponad swój udział albo poniżej niego. Wprowadzony: [10 › Dojdź od pomysłu do programu](10%20Zastosuj%20wiedz%C4%99%20w%20praktyce.md#dojdź-od-pomysłu-do-programu).
- **suma** (zmienna (liczba)): Suma kwot zbierana w pętli. Wprowadzony: [06 › Przejdź przez całą listę](06%20Powtarzaj%20i%20zbieraj%20dane.md#przejdź-przez-całą-listę).
  - zmiana w [07 › Podziel program na funkcje](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#podziel-program-na-funkcje): bez uzasadnienia
- **na_osobe** (funkcja): Dzieli sumę przez liczbę osób. Wprowadzony: [07 › Podziel program na funkcje](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#podziel-program-na-funkcje).
- **wypisz_na_osobe** (funkcja): Wypisuje wynik zamiast go zwracać, więc daje None; służy do pokazania różnicy między print a return. Wprowadzony: [07 › Odbierz wynik z funkcji](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#odbierz-wynik-z-funkcji).

### `rozlicz.py`

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

- **rozlicz.py** (plik programu (skrypt główny)): Pierwszy plik kodu źródłowego Wspólnej Kasy. Wprowadzony: [03 › Poznaj kod źródłowy](03%20Napisz%20i%20uruchom%20kod.md#poznaj-kod-źródłowy).

### `test_rozlicz.py`

```python
assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0
```

- **test_rozlicz.py** (plik testów): Testy funkcji na_osobe przez assert. Wprowadzony: [09 › Przetestuj swój program](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#przetestuj-swój-program).

### `wspolna_kasa`

```python
git init -b main
```

- **wspolna_kasa** (repozytorium Git): Repozytorium w folderze projektu, w którym zapisujemy wersje Wspólnej Kasy. Wprowadzony: [09 › Zapisuj wersje kodu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#zapisuj-wersje-kodu).

### `wspolna_kasa/rozlicz.py`

```python
wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.50}]

osoby = ["Ania", "Bartek", "Celina"]

def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    kwota = float(kwota)
    ...

def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

for imie in osoby:

kwota = 45.5

zaplacono = True

kwota_stara = kwota

liczba_osob = 3

for wydatek in wydatki:
```

- **wydatki** (zmienna (lista słowników)): Kolekcja wszystkich wydatków w pamięci programu. Wprowadzony: [06 › Unikaj pętli nieskończonej](06%20Powtarzaj%20i%20zbieraj%20dane.md#unikaj-pętli-nieskończonej).
- **osoby** (zmienna (lista tekstów)): Uczestnicy, między których dzielimy koszty. Wprowadzony: [03 › Opisuj kod komentarzami](03%20Napisz%20i%20uruchom%20kod.md#opisuj-kod-komentarzami).
- **zapytaj_o_wydatek** (funkcja): Szkic pobrania danych wejściowych od użytkownika. Wprowadzony: [08 › Przyjmij dane z zewnątrz](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#przyjmij-dane-z-zewnątrz).
  - zmiana w [08 › Zapytaj użytkownika o dane](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapytaj-użytkownika-o-dane): Dopisujemy zamianę odpowiedzi na liczbę, bo input zwraca tekst.
- **sprawdz_kwote** (funkcja): Waliduje wpisaną kwotę: liczba większa od zera. Wprowadzony: [08 › Weryfikuj wpisane dane](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#weryfikuj-wpisane-dane).
- **wypisz_podsumowanie** (funkcja): Wypisuje czytelne podsumowanie wydatków jako część interfejsu tekstowego. Wprowadzony: [08 › Zaprojektuj jasny interfejs](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zaprojektuj-jasny-interfejs).
- **imie** (zmienna (tekst)): Kto zapłacił za pojedynczy wydatek. Wprowadzony: [04 › Nazwij swoją pierwszą zmienną](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#nazwij-swoją-pierwszą-zmienną).
  - zmiana w [06 › Powtórz kod pętlą](06%20Powtarzaj%20i%20zbieraj%20dane.md#powtórz-kod-pętlą): bez uzasadnienia
- **kwota** (zmienna (liczba)): Kwota pojedynczego wydatku. Wprowadzony: [04 › Nazwij swoją pierwszą zmienną](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#nazwij-swoją-pierwszą-zmienną).
- **zaplacono** (zmienna (prawda/fałsz)): Czy wydatek został już rozliczony. Wprowadzony: [04 › Nazwij swoją pierwszą zmienną](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#nazwij-swoją-pierwszą-zmienną).
- **kwota_stara** (zmienna (liczba)): Kopia wartości kwoty, niezależna od późniejszej zmiany kwota. Wprowadzony: [04 › Przypisz wartość zmiennej](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#przypisz-wartość-zmiennej).
- **liczba_osob** (zmienna (liczba)): Liczba osób dzielących kwotę, używana w warunkach z and/or. Wprowadzony: [05 › Łącz warunki spójnikami](05%20Podejmuj%20decyzje%20w%20programie.md#łącz-warunki-spójnikami).
- **wydatek** (zmienna (słownik)): Zmienna pętli: jeden wydatek z listy wydatki. Wprowadzony: [06 › Przejdź przez całą listę](06%20Powtarzaj%20i%20zbieraj%20dane.md#przejdź-przez-całą-listę).

### `wydatki.txt`

```python
Ania;120.5
Bartek;45.5
```

- **wydatki.txt** (plik danych): Tekstowy plik z wydatkami, zapisywany i wczytywany przez program. Wprowadzony: [08 › Zapisz dane w pliku](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapisz-dane-w-pliku).

## Zaplanowane, jeszcze niepokazane

- **wydatki.csv** (plik danych): Lista wydatków wczytywana przez program.
- **wczytaj_wydatki** (funkcja): Czyta plik CSV i buduje listę wydatków.
