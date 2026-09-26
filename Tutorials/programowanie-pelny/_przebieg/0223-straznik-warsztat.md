# Krok 0223 · strażnik_warsztat

Węzeł: `review` · dział: 3 · pytanie: 15 · próba: 1

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
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. polecenie (Sprawdzamy, że Python jest dostępny):
$ python --version
podany wynik:
Python 3.13.5
2. polecenie (Uruchamiamy pierwszy skrypt):
$ python kasa.py
podany wynik:
Wspólna Kasa
3. plik kasa.py (Celowo psujemy nazwę print) zmiana:
 # kasa.py - pierwszy skrypt Wspólnej Kasy
-print("Wspólna Kasa")
+prnt("Wspólna Kasa")
4. polecenie (Python zatrzymuje się na błędnej linii) [CELOWY BŁĄD]:
$ python kasa.py
podany wynik:
Traceback (most recent call last):
  File "/home/ola/wspolna_kasa/kasa.py", line 2, in <module>
    prnt("Wspólna Kasa")
    ^^^^
NameError: name 'prnt' is not defined. Did you mean: 'print'?
5. plik kasa.py (Przywracamy poprawną nazwę) zmiana:
 # kasa.py - pierwszy skrypt Wspólnej Kasy
-prnt("Wspólna Kasa")
+print("Wspólna Kasa")
6. polecenie (Skrypt znów działa):
$ python kasa.py
podany wynik:
Wspólna Kasa

SEKCJA "Co znaczy uruchomić program":
Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam [[kod-zrodlowy|kod źródłowy]] leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś go nie zacznie realizować.

Plik z kodem jest [[uruchamianie-programu|uruchamiany]] przez inny program, który go czyta i wykonuje linia po linii. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.

Polecenie wpisujemy w [[terminal|terminalu]], czyli oknie, w którym komputer przyjmuje polecenia pisane tekstem i pokazuje odpowiedzi tekstem. Przykład to nasz plik `rozlicz.py`:

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

W terminalu wpisujemy `python rozlicz.py`, a program wypisuje:

```text
Wspólna Kasa
100.0
```

Kolejność wyjścia jest taka sama jak kolejność linii, bo instrukcje wykonują się jedna po drugiej. Wynik `100.0` to 300 zł podzielone na trzy osoby.

Uruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. Tak wygląda cała praca programisty: zapisz, uruchom, przeczytaj wynik.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "detail": "Tekst sekcji mówi o pliku `rozlicz.py` (z `print(300 / 3)` i wynikiem `100.0`), a czytelnik ma w katalogu tylko `kasa.py` z jedną linią `print(\"Wspólna Kasa\")`. Polecenie `python rozlicz.py` zakończy się błędem: can't open file ... No such file or directory. Popraw przykład w tekście na `kasa.py`: blok kodu `# kasa.py - pierwszy skrypt Wspólnej Kasy` + `print(\"Wspólna Kasa\")`, polecenie `python kasa.py`, wynik samo `Wspólna Kasa`. Zdanie o `100.0` i kolejności linii usuń albo przenieś do osobnego przykładu jawnie oznaczonego jako niewykonywany w krokach.",
      "severity": "blokująca",
      "target": "tekst sekcji: przykład rozlicz.py"
    },
    {
      "kind": "spójność",
      "detail": "Tekst sekcji nie wspomina o celowym błędzie z kroków 3–5 (literówka `prnt`, NameError, przywrócenie). Dodaj krótki akapit: Python zatrzymuje się na błędnej linii i podaje numer linii oraz podpowiedź `Did you mean: 'print'?`; po poprawce skrypt działa.",
      "severity": "sugestia",
      "target": "tekst sekcji"
    },
    {
      "kind": "wynik",
      "detail": "Ścieżka w tracebacku `/home/ola/wspolna_kasa/kasa.py` będzie u czytelnika inna (jego katalog domowy i nazwa użytkownika, na Windows np. C:\\Users\\...\\wspolna_kasa\\kasa.py). Dopisz uwagę, że ścieżka w pierwszej linii będzie się różnić, a ważne są numer linii `line 2` i ostatnia linia z NameError.",
      "severity": "sugestia",
      "target": "krok 4"
    }
  ]
}
````
