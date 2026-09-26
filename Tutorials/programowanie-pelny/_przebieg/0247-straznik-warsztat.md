# Krok 0247 · strażnik_warsztat

Węzeł: `review` · dział: 3 · pytanie: 16 · próba: 1

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
1. polecenie (Sprawdzamy, który interpreter Pythona masz zainstalowany (numer poprawki może się różnić).):
$ python --version
podany wynik:
Python 3.13.1

SEKCJA "Kompilator i interpreter":
Kompilator i interpreter to programy, które przekładają [[kod-zrodlowy|kod źródłowy]] na działanie komputera, bo procesor sam nie rozumie tekstu z pliku. [[kompilator|Kompilator]] tłumaczy cały kod naraz na osobny, gotowy do uruchomienia plik. [[interpreter|Interpreter]] czyta kod i wykonuje go na bieżąco, instrukcja po instrukcji.

To ten wykonawca, o którym była mowa przy uruchamianiu programu. Gdy wpisujesz `python kasa.py`, [[python|Python]] działa jako interpreter: bierze plik i wykonuje go od góry.

| | Kompilator | Interpreter |
|---|---|---|
| Co robi | tłumaczy całość przed startem | wykonuje kod w trakcie czytania |
| Wynik | osobny plik do uruchomienia | brak pliku, od razu efekt |
| Uruchomienie po zmianie | najpierw kompilacja, potem start | zapisz i uruchom |

```text
kompilator:   kod źródłowy --> [kompilator] --> plik programu --> uruchomienie
interpreter:  kod źródłowy --> [interpreter] --> uruchomienie
```

Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania. Zmieniasz `kasa.py`, zapisujesz i uruchamiasz ponownie. W praktyce Python najpierw przekłada plik na pośredni zapis, ale z Twojej strony to jedno polecenie.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "odwołanie",
      "detail": "Krok `python --version` nie jest omówiony w tekście sekcji. Dodaj zdanie, np. „Wynik `Python 3.13.1` potwierdza, że masz zainstalowany interpreter Pythona (numer po drugiej kropce może być inny).”. Bez niego czytelnik nie wie, po co wykonał to polecenie.",
      "severity": "sugestia",
      "target": "krok 1 / tekst sekcji",
      "source": "weryfikacja kroków"
    }
  ]
}
````
