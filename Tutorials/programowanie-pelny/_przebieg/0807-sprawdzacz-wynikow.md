# Krok 0807 · sprawdzacz_wyników

Węzeł: `review` · dział: 7 · pytanie: 42 · próba: 1

## Prompt

````text
Jesteś sprawdzaczem wyników w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.

Dla każdego bloku kodu, który da się uruchomić samodzielnie (ma wszystkie dane, nie zawiera `...`) i coś wypisuje:
1. Czy bezpośrednio pod nim jest blok ```text z wynikiem? Brak: kind="wynik", severity="blokująca",
   detail = dokładny wynik, który trzeba dopisać.
2. Wykonaj kod w myślach krok po kroku (wartości, obliczenia, zaokrąglenia, formatowanie, kolejność linii)
   i porównaj z podanym wynikiem znak w znak. Niezgodność: kind="wynik", severity="blokująca",
   detail = co się nie zgadza i poprawny wynik.
Szkice (z `...`, bez danych) i bloki bez wypisywania pomiń. ok=true, gdy wszystko się zgadza.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

SEKCJA "Czytelne nazwy zmiennych i funkcji":
Nazwa to jedyna wskazówka, co kryje się w [[zmienna|zmiennej]] albo [[funkcja|funkcji]]. Komputerowi wszystko jedno, jak ją nazwiesz, ale kod czytasz Ty: dziś, za miesiąc i ktoś inny. Dobra nazwa zastępuje komentarz.

Porównaj dwie wersje tej samej rzeczy:

| Nieczytelnie | Czytelnie |
|---|---|
| `f(a, b)` | `udzial_na_osobe(suma, liczba_osob)` |
| `x = 3` | `liczba_osob = 3` |
| `dane2` | `kwoty_wydatkow` |

Przy `f(300, 4)` trzeba zgadywać, co się dzieje i która liczba jest która. To ryzyko z zamienioną kolejnością, które znasz z [[sec-07-czym-sa-argumenty-funkcji|argumentów funkcji]]: zły wynik bez błędu. Nazwa `udzial_na_osobe` mówi to od razu.

Funkcję nazywaj tak, by opisywała, co robi (`suma_wydatkow`), a zmienną tak, by opisywała, co trzyma (`liczba_osob`). Zwykle małe litery, słowa rozdzielone podkreśleniem, bez polskich znaków, tak jak w całym tutorialu.

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

print(udzial_na_osobe(suma_wydatkow([45.5, 20, 12.5]), 3))
```

```text
26.0
```

Ostatnią linię czyta się prawie jak zdanie. Ta czytelność przyda się przy [[sec-07-po-co-dzielic-program-na-funkcje|dzieleniu programu na funkcje]] i przy ponownym użyciu kodu, które omówimy za chwilę.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
