# Krok 0414 · strażnik_warsztat

Węzeł: `review` · dział: 4 · pytanie: 24 · próba: 1

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
print(type(nazwa_wyjazdu))
print(type(kwota_wydatku))
print(type(czy_oplacone))
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik kasa.py (Podmieniamy wartość logiczną na False i wypisujemy ją.) zmiana:
 print(type(czy_oplacone))
+czy_oplacone = False
+print(czy_oplacone)
2. polecenie ():
$ python kasa.py
podany wynik:
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>
False

SEKCJA "Wartość logiczna prawda/fałsz":
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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
