# Krok 0204 · strażnik_warsztat

Węzeł: `review` · dział: 3 · pytanie: 14 · próba: 1

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
(brak plików)
```
Ostatnie polecenie zakończyło się celowym błędem: nie.

KROKI TEJ SEKCJI:
1. polecenie (Sprawdzamy, że Python jest zainstalowany):
$ python --version
podany wynik:
Python 3.13.5
2. plik kasa.py (Zapisujemy w edytorze pierwszy plik z komentarzem i jednym print) nowy plik:
# kasa.py - pierwszy plik Wspólnej Kasy
print("Wspólna Kasa")


SEKCJA "Do czego służy edytor":
[[edytor-kodu|Edytor kodu]] to program do pisania i poprawiania [[kod-zrodlowy|kodu źródłowego]], który pomaga czytać kod i zauważać w nim pomyłki. Sam kodu nie uruchamia i nie zmienia jego działania: zmienia tylko to, jak wygodnie się go pisze.

Skoro kod jest [[sec-03-czym-jest-kod-zrodlowy|zwykłym plikiem tekstowym]], można go napisać nawet w Notatniku. Edytor kodu dodaje jednak rzeczy, które przy programowaniu bardzo oszczędzają czas:

| Możliwość | Co daje |
|---|---|
| [[podswietlanie-skladni|podświetlanie składni]] | słowa języka, teksty i liczby mają różne kolory, więc struktura kodu jest widoczna |
| numery linii | komunikat „błąd w linii 3” da się od razu znaleźć |
| wcięcia i nawiasy | edytor wcina linie i domyka cudzysłowy oraz nawiasy |
| podpowiedzi | po wpisaniu kilku liter proponuje dokończenie nazwy |
| zapis w zwykłym tekście | plik da się otworzyć w dowolnym innym programie |

Podświetlanie składni to kolorowanie fragmentów kodu według ich roli. Literówka w nazwie polecenia często od razu zmienia kolor, zanim cokolwiek uruchomisz.

Przykładem będzie VS Code, ale wybór edytora jest sprawą gustu. Zasady pisania kodu są w każdym takie same.

U siebie sprawdzisz teraz Pythona i zapiszesz pierwszy plik. Uruchomimy go w następnej części, gdy wyjaśnimy, co to właściwie znaczy uruchomić program.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wynik",
      "detail": "Numer wersji może się różnić od 3.13.5 (np. 3.13.1 albo 3.13.7). Dopisz, że ważne jest, by zaczynało się od „Python 3.13”, a ostatnia liczba może być inna. Dodaj też, że na macOS/Linux trzeba wpisać python3 --version, jeśli python nie działa.",
      "severity": "sugestia",
      "target": "Krok 1: python --version"
    },
    {
      "kind": "spójność",
      "detail": "Krok nie mówi, gdzie zapisać plik. Dopisz: „Zapisz plik jako kasa.py w katalogu ~/wspolna_kasa (tym samym, w którym masz otwarty terminal)”. W Notatniku warto dodać, żeby wybrać „Wszystkie pliki” i kodowanie UTF-8, żeby nie powstało kasa.py.txt.",
      "severity": "sugestia",
      "target": "Krok 2: kasa.py"
    },
    {
      "kind": "spójność",
      "detail": "Zdanie „Literówka w nazwie polecenia często od razu zmienia kolor” jest niepewne. W VS Code literówka w print (np. prnit) zwykle nie zmienia koloru, bo edytor traktuje ją jak zwykłą nazwę. Zastąp je przykładem, który jest prawdziwy: brakujący cudzysłów zamykający zmienia kolor reszty linii na kolor tekstu.",
      "severity": "sugestia",
      "target": "Akapit o podświetlaniu składni"
    }
  ]
}
````
