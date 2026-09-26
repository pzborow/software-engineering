# Krok 0316 · strażnik_warsztat

Węzeł: `review` · dział: 4 · pytanie: 19 · próba: 1

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
1. plik kasa.py (Dopisujemy trzy dane i wypisujemy je razem z rodzajem.) zmiana:
 print("Wspólna Kasa")
+nazwa_wyjazdu = "Mazury"
+kwota_wydatku = 45.5
+czy_oplacone = True
+print(nazwa_wyjazdu, type(nazwa_wyjazdu))
+print(kwota_wydatku, type(kwota_wydatku))
+print(czy_oplacone, type(czy_oplacone))
2. polecenie (Uruchamiamy skrypt i czytamy rodzaje danych.):
$ python kasa.py
podany wynik:
Wspólna Kasa
Mazury <class 'str'>
45.5 <class 'float'>
True <class 'bool'>

SEKCJA "Czym jest dana":
[[dana|Dana]] to każda informacja, na której pracuje program: imię, kwota, data, odpowiedź „tak” lub „nie”. Program bez danych nie miałby czego liczyć ani wypisać.

W arkuszu kalkulacyjnym danymi są wartości w komórkach: nazwisko w jednej, kwota w drugiej. W programie jest podobnie, tylko że dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz.

```python
print("Ania")   # tekst: imię
print(45.5)     # liczba: kwota wydatku
print(True)     # prawda albo fałsz: czy zapłacono
```

```text
Ania
45.5
True
```

Każda z tych trzech wartości to jedna dana, ale każda jest innego rodzaju. Tekst w cudzysłowie służy do pokazywania i porównywania napisów. Liczbę można dodawać i dzielić. Prawda lub fałsz odpowiada na pytanie tak/nie. Rodzaj danej decyduje o tym, co program może z nią zrobić: kwoty da się dodać, imion nie.

Dane trzeba też gdzieś przechowywać, żeby użyć ich więcej niż raz. Do tego służy zmienna, którą poznasz w następnej sekcji. Rodzaje danych omówimy osobno, gdy przejdziemy do typów.

U siebie w `kasa.py` dopiszesz za chwilę te trzy rodzaje danych dla wyjazdu i sprawdzisz, jak Python je nazywa.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "severity": "sugestia",
      "target": "krok 1 (zmienne i type())",
      "detail": "Krok 1 używa zmiennych (nazwa_wyjazdu = \"Mazury\") i funkcji type(), a tekst tylko zapowiada zmienną w następnej sekcji. Dodaj jedno zdanie, np.: „W kodzie użyjemy nazw, pod którymi Python zapamięta dane (o zmiennych więcej w następnej sekcji), oraz type(), które pokazuje rodzaj danej.”",
      "source": "Sekcja „Czym jest dana”"
    },
    {
      "kind": "odwołanie",
      "severity": "sugestia",
      "target": "wynik kroku 2 (str, float, bool)",
      "detail": "Wynik zawiera nazwy str, float i bool, a tekst ich nie objaśnia. Dodaj zdanie, np.: „str to tekst, float to liczba z przecinkiem, bool to prawda/fałsz.”",
      "source": "Sekcja „Czym jest dana”"
    }
  ]
}
````
