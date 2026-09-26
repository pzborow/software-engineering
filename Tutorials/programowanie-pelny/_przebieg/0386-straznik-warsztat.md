# Krok 0386 · strażnik_warsztat

Węzeł: `review` · dział: 4 · pytanie: 22 · próba: 2

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
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. plik kasa.py (Dopisujemy dzielenie tekstu przez 2, żeby zobaczyć błąd.) zmiana:
 print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
+print(nazwa_wyjazdu / 2)
2. polecenie (Python wykonuje linie po kolei i zatrzymuje się na dzieleniu tekstu.) [CELOWY BŁĄD]:
$ python kasa.py
podany wynik:
Wspólna Kasa
Mazury 45.5 True
Traceback (most recent call last):
  File "/home/ania/wspolna_kasa/kasa.py", line 7, in <module>
    print(nazwa_wyjazdu / 2)
          ~~~~~~~~~~~~~~^~~
TypeError: unsupported operand type(s) for /: 'str' and 'int'

SEKCJA "Liczba a tekst":
Liczba to wartość, na której program liczy. Tekst to ciąg znaków, który program przechowuje, wypisuje, porównuje i skleja. Zapis decyduje o tym, z czym mamy do czynienia: `45.5` bez cudzysłowu to liczba, a `"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5.

| Zapis | Co to jest | Można dzielić? |
|---|---|---|
| `45.5` | liczba | tak |
| `"45.5"` | tekst | nie |
| `"Ania"` | tekst | nie |

W programie ułamek dziesiętny zapisujemy z kropką, nie z przecinkiem, tak jak `kwota = 45.5` w „Wspólnej Kasie”.

```python
kwota = 45.5
imie = "Ania"
print(kwota / 2)
print(imie)
```

```text
22.75
Ania
```

Liczbę można podzielić, tekstu nie. To ta sama myśl co [[imienia nie da się podzielić|imię „Ania” nie do podzielenia przez 2]]. Python zatrzyma się z komunikatem `TypeError`. U siebie zobaczysz to za chwilę we własnym pliku z kodem.

Uwaga na plus: przy liczbach dodaje, a przy tekstach skleja je w jeden. Tym zajmiemy się osobno.

Konsekwencja: kwotę zapisaną w cudzysłowie program potraktuje jak napis, nie jak pieniądze. Nazwę tej cechy danych, czyli typ, omówimy w następnej sekcji.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "detail": "Tekst mówi, że w „Wspólnej Kasie” jest `kwota = 45.5`, a w kasa.py czytelnik ma `kwota_wydatku = 45.5`. Popraw na: „tak jak `kwota_wydatku = 45.5` w „Wspólnej Kasie”” albo napisz, że poniższy przykład używa krótszej nazwy `kwota`.",
      "severity": "blokująca",
      "target": "zdanie o `kwota = 45.5`",
      "source": "kasa.py"
    },
    {
      "kind": "wynik",
      "detail": "W tracebacku jest ścieżka /home/ania/wspolna_kasa/kasa.py. U czytelnika będzie ona inna (jego katalog domowy, na Windows np. C:\\Users\\...\\wspolna_kasa\\kasa.py). Dodaj zdanie, że ścieżka w pierwszej linii `File ...` będzie u niego inna, a liczy się `line 7` i ostatnia linia z TypeError.",
      "severity": "sugestia",
      "target": "krok 2, ścieżka w tracebacku"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Nazwa `TypeError` pojawia się bez wyjaśnienia. Dodaj krótko, że to „błąd typu”: Python informuje, że działanie nie pasuje do rodzaju wartości. Sam typ jest omówiony w następnej sekcji.",
      "severity": "sugestia",
      "target": "TypeError"
    }
  ]
}
````
