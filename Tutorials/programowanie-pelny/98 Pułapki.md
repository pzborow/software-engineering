# Pułapki

Nieoczywiste zachowania kodu z przykładów, które prowadzą do błędów w produkcji albo w testach. Łowca pułapek sprawdza tylko sekcje z kodem i nie wypisuje niczego na siłę.

Sekcje z kodem: 43 · sprawdzone: 43 · pułapki tematu: 5 · poboczne: 2

## Pułapki tematu

Ilustrują zagadnienia, których dotyczy tutorial. Te same uwagi są w ramkach pod sekcjami.

### 03. Napisz i uruchom kod

- **błąd logiczny (działa do końca, zły wynik):** **Brak komunikatu nie oznacza poprawnego wyniku.** `print(300 / 2)` działa bez błędu i wypisuje `150.0`, choć dla trojga osób powinno być dzielenie przez 3. Program "bez błędów" może dawać zły wynik, więc trzeba samemu sprawdzić wynik, np. własnym obliczeniem.
  Dotyczy: `print(300 / 2) # 300 zł na troje osób` · [sekcja „Rozpoznaj błąd w programie”](03%20Napisz%20i%20uruchom%20kod.md#rozpoznaj-błąd-w-programie)

### 04. Zapamiętaj dane w zmiennych

- **zmienna i jej wartość:** **Zmiana wartości zmienia też typ.** Po `kwota = 60` zmienna z liczby dziesiętnej (`45.5`) staje się liczbą całkowitą. Program nie zgłasza błędu, więc dalsze wyniki mogą wyglądać inaczej, niż się spodziewasz (np. `70` zamiast `70.0`).
  Dotyczy: `kwota = 60` · [sekcja „Nazwij swoją pierwszą zmienną”](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#nazwij-swoją-pierwszą-zmienną)

### 07. Uporządkuj kod funkcjami

- **Nazwy w funkcjach i zasięg (parametr kontra funkcja):** **Parametr przesłania funkcję o tej samej nazwie.** W `na_osobe(suma, osoby)` nazwa `suma` oznacza liczbę, a nie funkcję `suma`, więc wewnątrz nie da się jej wywołać (błąd: liczba nie jest wywoływalna). Kod działa, bo ciało tego nie robi, ale to mylące. Nadaj parametrowi inną nazwę, np. `kwota_razem`.
  Dotyczy: `def na_osobe(suma, osoby):` · [sekcja „Podziel program na funkcje”](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#podziel-program-na-funkcje)

### 08. Porozmawiaj z użytkownikiem

- **dane wejściowe od użytkownika:** **`input` zawsze zwraca tekst, nawet dla liczb.** Wpisane `45.5` trafia do `kwota` jako tekst "45.5", a nie liczba. Dodawanie kwot da błąd albo sklei napisy ("20" + "5" = "205"), a porównania będą działać alfabetycznie. Przed liczeniem trzeba świadomie zamienić tekst na liczbę, np. `float(kwota)`.
  Dotyczy: `kwota = input("Ile zapłacił? ")` · [sekcja „Przyjmij dane z zewnątrz”](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#przyjmij-dane-z-zewnątrz)

- **plik i tryb otwarcia:** **Ścieżka względna zależy od folderu uruchomienia.** `open("wydatki.txt", ...)` szuka i tworzy plik w bieżącym folderze roboczym, a nie tam, gdzie leży skrypt. Uruchomiony z innego miejsca program zapisze plik gdzie indziej, a tryb `"r"` zgłosi brak pliku, choć plik istnieje. Uruchamiaj program zawsze z tego samego folderu albo podaj pełną ścieżkę.
  Dotyczy: `open("wydatki.txt", "r", encoding="utf-8")` · [sekcja „Zapisz dane w pliku”](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapisz-dane-w-pliku)

## Pułapki poboczne (Python i narzędzia przykładów)

Wynikają z narzędzi użytych do pokazania przykładów, a nie z tematu. Nie ma ich w tekście, żeby nie rozpraszały czytania.

### 08. Porozmawiaj z użytkownikiem

- **walidacja danych przed konwersją:** **Sprawdzenie przepuszcza tekst, którego float nie przyjmie.** `isdigit()` uznaje za cyfry także znaki takie jak `²`, więc `sprawdz_kwote("²")` nie zwraca `False`, tylko dochodzi do `float(tekst)` i program kończy się błędem `ValueError`. Reguła sprawdzająca powinna być zgodna z tym, co potem robi konwersja, np. przez próbę `float` w `try/except`.
  Dotyczy: `if not tekst.replace(".", "", 1).isdigit():` · [sekcja „Weryfikuj wpisane dane”](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#weryfikuj-wpisane-dane)

### 09. Oswój błędy w kodzie

- **assert jako test:** **assert znika przy uruchomieniu z -O.** Uruchomienie `python -O` pomija wszystkie instrukcje `assert`, więc nawet błędna funkcja wypisze „Wszystkie testy przeszły”. Testów opartych na `assert` nie uruchamiaj z optymalizacją; do poważniejszych testów używaj narzędzia testowego, np. pytest.
  Dotyczy: `assert na_osobe(78, 3) == 26` · [sekcja „Przetestuj swój program”](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#przetestuj-swój-program)
