# Krok 0290 · strażnik_warsztat

Węzeł: `review` · dział: 3 · pytanie: 18 · próba: 1

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
prnt("Wspólna Kasa")
```
Ostatnie polecenie zakończyło się celowym błędem: tak.

KROKI TEJ SEKCJI:
1. plik kasa.py (Naprawiamy literówkę i dopisujemy komentarz.) zmiana:
 # kasa.py - pierwszy skrypt Wspólnej Kasy
-prnt("Wspólna Kasa")
+# Poprawka: literówka prnt zamieniona na print
+print("Wspólna Kasa")
2. polecenie (Uruchamiamy ponownie: komentarze nie wpływają na wynik.):
$ python kasa.py
podany wynik:
Wspólna Kasa

SEKCJA "Do czego służą komentarze":
[[komentarz|Komentarz]] to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi.

W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. [[interpreter|Interpreter]] pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją.

```python
# rozlicz.py - rozliczenie wspólnych wydatków
print("Wspólna Kasa")
print(300 / 3)  # 300 zł na troje osób: udział jednej osoby
# print(300 / 2)  <- ta linia jest wyłączona
```

```text
Wspólna Kasa
100.0
```

Ostatnia linia pokazuje drugie zastosowanie: zamiana instrukcji na komentarz „wyłącza” ją bez kasowania. Przyda się to, gdy będziesz coś sprawdzać.

Komentarz ma sens, gdy podaje powód lub kontekst („300 zł na troje osób”). Powtarzanie tego, co widać w kodzie, tylko go zaśmieca. Pamiętaj też, że komentarz może się zestarzeć: jeśli zmienisz kod, a opis zostawisz, wprowadzi czytelnika w błąd. U siebie masz już taki komentarz w pierwszej linii `kasa.py`. Za chwilę go poprawisz i sprawdzisz, że nie wpływa na wynik.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "spójność",
      "detail": "Ostatni akapit mówi, że pierwsza linia kasa.py to komentarz, który czytelnik „za chwilę poprawi”. Krok 1 nie zmienia tej linii (`# kasa.py - pierwszy skrypt Wspólnej Kasy` zostaje bez zmian). Dopisuje nową linię `# Poprawka: literówka prnt zamieniona na print` i zamienia `prnt` na `print`. Ten pierwszy komentarz też nie jest przestarzały. Zamień ostatnie dwa zdania na: „U siebie masz już taki komentarz w pierwszej linii `kasa.py`. Za chwilę dopiszesz pod nim drugi, o poprawce, i sprawdzisz, że żaden z nich nie wpływa na wynik.” Możesz też usunąć zdanie o „starzeniu się” komentarza z odniesienia do pliku.",
      "target": "ostatni akapit sekcji vs krok 1",
      "severity": "sugestia",
      "status": "nowa"
    }
  ]
}
````
