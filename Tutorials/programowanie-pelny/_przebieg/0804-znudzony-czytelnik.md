# Krok 0804 · znudzony_czytelnik

Węzeł: `review` · dział: 7 · pytanie: 42 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Dlaczego nazwy zmiennych i funkcji powinny być czytelne?".

Zgłoś potrzeby (najwyżej 3, zero też jest dobrą odpowiedzią), wybierając kind:
- "przykład": teza jest abstrakcyjna i brakuje krótkiego kodu lub scenariusza,
- "konkret": ogólniki zamiast decyzji, liczby, nazwy klasy albo porównania,
- "skrócenie": powtórzenia, lanie wody, przykład dłuższy niż potrzeba,
- "diagram": przepływ łatwiej zrozumieć z rysunku tekstowego,
- "tempo": za dużo nowych pojęć naraz albo sekcja nie wnosi nic nowego względem poprzedniej.
Sekcja ma limit 250 słów prozy i jeden, najwyżej dwa krótkie bloki kodu.
Nie proś o coś, co się w tym nie zmieści, i nie żądaj jednocześnie dodania i skrócenia.
Kod może być tylko w językach: python, text.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

POPRZEDNIA SEKCJA:
## Zwracanie wyniku przez funkcję
Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał. Ta oddana wartość to [[wartosc-zwracana|wartość zwracana]]: wywołanie funkcji staje się w kodzie właśnie nią, więc możesz ją zapisać do zmiennej albo przekazać dalej.

Po `return` funkcja od razu kończy pracę. Nic, co stoi pod nim w ciele funkcji, już się nie wykona.

Zwracanie to nie to samo co wypisywanie. `print` tylko pokazuje tekst na ekranie, a program nie dostaje z niego nic do dalszej pracy. Funkcja bez `return` oddaje specjalną wartość [[none|`None`]], czyli „nic”.

```python
def na_osobe(suma, osoby):
    return suma / osoby

def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wynik = na_osobe(300, 4)
nic = wypisz_na_osobe(300, 4)
print(wynik)
print(nic)
```

```text
75.0
75.0
None
```

Pierwsza `75.0` pochodzi z `print` wewnątrz `wypisz_na_osobe`, w chwili wywołania. Druga to `wynik`, czyli wartość zwrócona i zapisana. Zmienna `nic` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła. Nazwy `wynik` i `nic` służą tylko tej ilustracji.

Konsekwencja jest praktyczna: tylko zwrócony wynik da się wykorzystać dalej. Dlatego `na_osobe(suma(mazury), 3)` działa: wynik jednej funkcji trafia jako argument do drugiej.

NOWA SEKCJA "Czytelne nazwy zmiennych i funkcji":
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
