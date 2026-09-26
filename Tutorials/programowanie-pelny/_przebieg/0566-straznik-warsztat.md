# Krok 0566 · strażnik_warsztat

Węzeł: `review` · dział: 5 · pytanie: 31 · próba: 2

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
czy_oplacone = False
print(czy_oplacone)
liczba_osob = 3
koszt_na_osobe = kwota_wydatku / liczba_osob
print(koszt_na_osobe)
print(kwota_wydatku % liczba_osob)
print("Kwota: " + str(kwota_wydatku) + " zł")
print(f"Wyjazd: {nazwa_wyjazdu}, kwota: {kwota_wydatku} zł")
print(kwota_wydatku > 100)
print(kwota_wydatku >= 45.5)
print(liczba_osob != 3)
print(nazwa_wyjazdu == "mazury")
if kwota_wydatku > 40:
    print("Kwota do sprawdzenia")
if kwota_wydatku > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print("Koniec")
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik kasa.py (Dopisujemy warunki z and oraz or przed ostatnim print.) zmiana:
     print("Zwykła kwota")
+print(kwota_wydatku > 40 and liczba_osob > 5)
+print(kwota_wydatku > 100 or liczba_osob == 3)
+if kwota_wydatku > 100 or liczba_osob > 5:
+    print("Duża kwota")
+else:
+    print("Zwykła kwota")
 print("Koniec")
2. polecenie (Uruchamiamy skrypt i sprawdzamy nowe trzy linie wyniku.):
$ python kasa.py
podany wynik:
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>
False
15.166666666666666
2.5
Kwota: 45.5 zł
Wyjazd: Mazury, kwota: 45.5 zł
False
True
False
False
Kwota do sprawdzenia
Zwykła kwota
False
True
Zwykła kwota
Koniec

SEKCJA "Operatory „i” oraz „lub”":
[[operator-logiczny|Operatory logiczne]] `and` („i”) oraz `or` („lub”) łączą kilka warunków w jeden. Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: `True` albo `False`.

`and` daje `True` tylko wtedy, gdy prawdziwe są **oba** warunki. `or` daje `True`, gdy prawdziwy jest **którykolwiek** z nich, a `False` dopiero wtedy, gdy oba są fałszywe.

| Lewy warunek | Prawy warunek | `and` | `or` |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

Każdy z połączonych warunków zapisujemy w całości, tak jak w porównywaniu wartości. Wynik można wypisać albo wstawić do `if`:

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

```text
False
True
Zwykła kwota
```

W pierwszej linii drugi warunek zawiódł, więc `and` dało `False`. W drugiej wystarczył prawdziwy drugi warunek, więc `or` dało `True`. W `if` oba są fałszywe, więc zadziałało `else`.

Dla „Wspólnej Kasy” to znaczy, że kwotę można uznać za dużą, gdy jest wysoka **lub** dzieli ją dużo osób. U siebie w `kasa.py` dopisz te linie w warsztacie poniżej.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "spójność",
      "detail": "Przykład w tekście używa zmiennej `kwota`, a w kasa.py jest `kwota_wydatku`. Można dodać zdanie, że w kasa.py nazwa jest dłuższa (kwota_wydatku), żeby czytelnik nie przepisał `kwota` do pliku.",
      "severity": "sugestia",
      "target": "Przykład w tekście sekcji"
    }
  ]
}
````
