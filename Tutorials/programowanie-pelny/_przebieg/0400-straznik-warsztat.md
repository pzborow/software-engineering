# Krok 0400 · strażnik_warsztat

Węzeł: `review` · dział: 4 · pytanie: 23 · próba: 1

## Prompt

````text
Jesteś weryfikatorem warsztatu „Wspólna Kasa krok po kroku” w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.
Czytelnik wykonuje kroki u siebie dosłownie. Punkt startowy: Dowolny system (Windows, macOS lub Linux) z terminalem (PowerShell, bash lub zsh), zainstalowany Python 3.13 (sprawdzenie: python --version, na macOS/Linux ewentualnie python3 --version) oraz prosty edytor kodu, np. VS Code lub Notatnik. Pusty katalog roboczy ~/wspolna_kasa, w którym czytelnik otwiera terminal..

Wykonaj kroki w myślach na stanie poniżej i sprawdź:
1. Czy każde polecenie da się wykonać w tym stanie (pliki istnieją, narzędzia są w punkcie startowym albo zainstalowane wcześniej).
2. Czy podany wynik zgadza się znak w znak z tym, co naprawdę wypisze polecenie (wartości, zaokrąglenia, formatowanie,
   kolejność). Przy celowym błędzie: czy komunikat jest prawdziwy dla tego narzędzia i wersji.
3. Czy zmiany w plikach dotyczą tego, o czym mówi sekcja, bez przypadkowych zmian w innych miejscach.
4. Czy tekst sekcji zgadza się z krokami (nazwy plików, wartości, wyniki).
Każdy problem zgłoś jako kind="wynik" (zły albo brakujący wynik) lub "spójność" (reszta), target=krok albo plik,
detail=co się nie zgadza i DOKŁADNIE jak poprawić (poprawny wynik, poprawna linia). Błąd wykonania jest blokujący.
Nie żądaj usunięcia kroków: warsztat poprawiamy, nie odrzucamy.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

STAN U CZYTELNIKA PRZED SEKCJĄ:
```text
--- kasa.py ---
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
nazwa_wyjazdu = "Mazury"
kwota_wydatku = 45.5
czy_oplacone = True
print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
print(nazwa_wyjazdu / 2)
```
Ostatnie polecenie zakończyło się celowym błędem: tak.

KROKI TEJ SEKCJI:
1. plik kasa.py (Zamiast dzielenia tekstu przez 2 sprawdzamy typy zmiennych.) zmiana:
 print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
-print(nazwa_wyjazdu / 2)
+print(type(nazwa_wyjazdu))
+print(type(kwota_wydatku))
+print(type(czy_oplacone))
2. polecenie (Uruchamiamy poprawiony skrypt.):
$ python kasa.py
podany wynik:
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>

SEKCJA "Czym jest typ danych":
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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Teza „typ decyduje o tym, co program może zrobić z wartością” ma tylko zdanie o dzieleniu imienia przez 2. Dobrze byłoby dodać krótki kod, np. print(kwota / 2) z wynikiem 22.75 oraz odwołanie do wcześniejszego błędu przy nazwa_wyjazdu / 2. Nic tu nie jest błędne, to tylko sugestia.",
      "severity": "sugestia",
      "target": "zdanie „Typ decyduje o tym…”"
    }
  ]
}
````
