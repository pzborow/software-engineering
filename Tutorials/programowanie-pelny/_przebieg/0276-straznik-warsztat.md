# Krok 0276 · strażnik_warsztat

Węzeł: `review` · dział: 3 · pytanie: 17 · próba: 2

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
1. plik kasa.py (Celowo psujemy nazwę print, wpisując prnt.) zmiana:
 # kasa.py - pierwszy skrypt Wspólnej Kasy
-print("Wspólna Kasa")
+prnt("Wspólna Kasa")
2. polecenie (Uruchamiamy i oglądamy pierwszy błąd.) [CELOWY BŁĄD]:
$ python kasa.py
podany wynik:
Traceback (most recent call last):
  File "/home/ala/wspolna_kasa/kasa.py", line 2, in <module>
    prnt("Wspólna Kasa")
    ^^^^
NameError: name 'prnt' is not defined. Did you mean: 'print'?

SEKCJA "Co to jest błąd w programie":
[[blad-w-programie|Błąd w programie]] to każde miejsce, w którym program robi coś innego, niż chciał jego autor. Albo zatrzymuje się z komunikatem, albo działa do końca i podaje zły wynik.

Pierwszy rodzaj widać od razu. Python czyta plik od góry i gdy trafi na coś, czego nie rozumie, przerywa pracę i wypisuje komunikat. Tak jest, gdy literówka zmieni [[print|print]] (polecenie, które każe programowi wypisać tekst lub liczbę na ekranie) w `prnt`: interpreter nie zna takiego słowa. To jeszcze nie katastrofa, bo komunikat wskazuje linię i powód. U siebie zobaczysz to za chwilę w `kasa.py`.

Drugi rodzaj jest podstępniejszy, bo nic nie ostrzega. Zobacz, co zrobi program z pozoru poprawny:

```python
# poza kanonem: błąd w dzieleniu
print("Wspólna Kasa")
print(300 / 2)   # 300 zł na troje osób
```

```text
Wspólna Kasa
150.0
```

Python wykonał każdą instrukcję zgodnie z zapisem, tylko że zapis był zły: na troje trzeba dzielić przez 3. Komputer robi dokładnie to, co napisano, a nie to, co miało się na myśli.

Konsekwencja: błąd to normalna część pracy, nie porażka. Komunikat to podpowiedź, a brak komunikatu nie znaczy, że wynik jest dobry. Jak rozróżniać te rodzaje błędów i czytać komunikaty, omówimy osobno, w dziale o poprawianiu programów.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wynik",
      "detail": "Ścieżka w tracebacku (/home/ala/wspolna_kasa/kasa.py) będzie u czytelnika inna (jego katalog domowy, na Windows np. C:\\Users\\...\\wspolna_kasa\\kasa.py). Dodaj jedno zdanie, że ścieżka w pierwszej linii File będzie u niego inna i to normalne; ważne są numer linii i ostatnia linia komunikatu. Reszta wyniku (NameError, karety pod prnt, podpowiedź Did you mean: 'print'?) jest zgodna z Pythonem 3.13.",
      "severity": "sugestia",
      "target": "krok 2"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Zdanie „gdy trafi na coś, czego nie rozumie” jest nieścisłe: `prnt(...)` jest poprawnie zapisane, Python dowiaduje się o braku nazwy dopiero przy wykonaniu tej linii. Lepiej: „gdy trafi na coś, z czym nie umie się zmierzyć (np. nazwę, której nie zna)”.",
      "severity": "sugestia",
      "target": "akapit „Pierwszy rodzaj”"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Słowo „interpreter” pojawia się bez wyjaśnienia. Zamień na „Python” albo dodaj krótką definicję (program, który czyta i wykonuje kod).",
      "severity": "sugestia",
      "target": "interpreter"
    }
  ]
}
````
