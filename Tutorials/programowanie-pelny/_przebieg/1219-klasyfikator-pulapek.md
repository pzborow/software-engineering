# Krok 1219 · klasyfikator_pułapek

Węzeł: `gotchas` · dział: — · pytanie: — · próba: —

## Prompt

````text
Tutorial: Programowanie od podstaw. Przykłady kodu są w: python.
Dla każdej pułapki z listy określ scope względem TEMATU tutorialu, a nie względem języka:
- "temat": pułapka ilustruje zagadnienie, którego dotyczy tutorial (Programowanie od podstaw),
- "poboczna": wynika z narzędzia użytego do pokazania przykładu (język python, biblioteka,
  framework, baza), a nie z tematu.
Gdy tematem jest sam język albo biblioteka, jej zachowania są tematem.
Test pomocniczy, gdy narzędzie NIE jest tematem: czy pułapka wystąpiłaby, gdyby to samo zagadnienie zaimplementować
innym narzędziem? Jeśli nie, bo wynika z mechanizmu tego narzędzia (np. protokołu tworzenia obiektów, cache biblioteki,
sposobu importu), to jest "poboczna", nawet jeśli dotyczy kodu realizującego zagadnienie.
Zwróć items z index i scope dla KAŻDEJ pozycji.

PUŁAPKI:
0. [błąd logiczny (działa do końca, zły wynik)] Brak komunikatu nie oznacza poprawnego wyniku: `print(300 / 2)` działa bez błędu i wypisuje `150.0`, choć dla trojga osób powinno być dzielenie przez 3. Program "bez błędów" może dawać zły wynik, więc trzeba samemu sprawdzić wynik, np. własnym obliczeniem.
1. [zmienna i jej wartość] Zmiana wartości zmienia też typ: Po `kwota = 60` zmienna z liczby dziesiętnej (`45.5`) staje się liczbą całkowitą. Program nie zgłasza błędu, więc dalsze wyniki mogą wyglądać inaczej, niż się spodziewasz (np. `70` zamiast `70.0`).
2. [Nazwy w funkcjach i zasięg (parametr kontra funkcja)] Parametr przesłania funkcję o tej samej nazwie: W `na_osobe(suma, osoby)` nazwa `suma` oznacza liczbę, a nie funkcję `suma`, więc wewnątrz nie da się jej wywołać (błąd: liczba nie jest wywoływalna). Kod działa, bo ciało tego nie robi, ale to mylące. Nadaj parametrowi inną nazwę, np. `kwota_razem`.
3. [dane wejściowe od użytkownika] `input` zawsze zwraca tekst, nawet dla liczb: Wpisane `45.5` trafia do `kwota` jako tekst "45.5", a nie liczba. Dodawanie kwot da błąd albo sklei napisy ("20" + "5" = "205"), a porównania będą działać alfabetycznie. Przed liczeniem trzeba świadomie zamienić tekst na liczbę, np. `float(kwota)`.
4. [plik i tryb otwarcia] Ścieżka względna zależy od folderu uruchomienia: `open("wydatki.txt", ...)` szuka i tworzy plik w bieżącym folderze roboczym, a nie tam, gdzie leży skrypt. Uruchomiony z innego miejsca program zapisze plik gdzie indziej, a tryb `"r"` zgłosi brak pliku, choć plik istnieje. Uruchamiaj program zawsze z tego samego folderu albo podaj pełną ścieżkę.
5. [walidacja danych przed konwersją] Sprawdzenie przepuszcza tekst, którego float nie przyjmie: `isdigit()` uznaje za cyfry także znaki takie jak `²`, więc `sprawdz_kwote("²")` nie zwraca `False`, tylko dochodzi do `float(tekst)` i program kończy się błędem `ValueError`. Reguła sprawdzająca powinna być zgodna z tym, co potem robi konwersja, np. przez próbę `float` w `try/except`.
6. [assert jako test] assert znika przy uruchomieniu z -O: Uruchomienie `python -O` pomija wszystkie instrukcje `assert`, więc nawet błędna funkcja wypisze „Wszystkie testy przeszły”. Testów opartych na `assert` nie uruchamiaj z optymalizacją; do poważniejszych testów używaj narzędzia testowego, np. pytest.
````

## Odpowiedź

````json
{
  "items": [
    {
      "index": 0,
      "scope": "temat"
    },
    {
      "index": 1,
      "scope": "temat"
    },
    {
      "index": 2,
      "scope": "temat"
    },
    {
      "index": 3,
      "scope": "temat"
    },
    {
      "index": 4,
      "scope": "temat"
    },
    {
      "index": 5,
      "scope": "poboczna"
    },
    {
      "index": 6,
      "scope": "poboczna"
    }
  ]
}
````
