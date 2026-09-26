# Krok 0786 · weryfikator_faktów

Węzeł: `review` · dział: 7 · pytanie: 41 · próba: 1

## Prompt

````text
Jesteś weryfikatorem faktów tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Wersje obowiązujące w tutorialu: Python 3.13. Wersje zadeklarowane w sekcji: (brak).

Sprawdź w DOKUMENTACJI konkretne, sprawdzalne twierdzenia nowej sekcji: komendy i ich flagi, nazwy argumentów,
pól i zasobów, wartości domyślne, składnię oraz zachowanie zależne od wersji.
- Najpierw Context7: resolve-library-id, potem query-docs. Gdy czegoś nie ma w Context7, użyj WebFetch
  na oficjalnej stronie dokumentacji. Najwyżej 4 zapytania łącznie: wybierz twierdzenia najbardziej narażone na błąd.
- Nie oceniaj stylu, dydaktyki ani ogólnych idei. Kod jest szkicem: `...` i pominięte fragmenty nie są błędem.
- Każdą niezgodność z dokumentacją zgłoś jako kind="fakt", target=fragment sekcji, detail=co mówi dokumentacja
  (z adresem strony) i jak poprawić. "blokująca", gdy czytelnik wykonując kod dostałby błąd albo inne zachowanie;
  "sugestia", gdy to nieścisłość bez takich skutków.
- sources: tylko strony, które faktycznie przeczytałeś, i które twierdzenie sekcji potwierdzają albo obalają.
- ok=true, gdy nie ma blokujących niezgodności.

NOWA SEKCJA "Zwracanie wyniku przez funkcję":
Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał. Wywołanie funkcji staje się wtedy w kodzie tą wartością, więc możesz ją zapisać do zmiennej albo przekazać dalej.

Po `return` funkcja od razu kończy pracę. Nic, co stoi pod nim w ciele funkcji, już się nie wykona.

Zwracanie to nie to samo co wypisywanie. `print` tylko pokazuje tekst na ekranie, a program nie dostaje z niego nic do dalszej pracy. Funkcja bez `return` oddaje specjalną wartość `None`, czyli „nic”.

```python
def na_osobe(suma, osoby):
    return suma / osoby

def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

a = na_osobe(300, 4)
b = wypisz_na_osobe(300, 4)
print(a)
print(b)
```

```text
75.0
75.0
None
```

Pierwsza `75.0` pochodzi z `print` wewnątrz `wypisz_na_osobe`, w chwili wywołania. Druga to `a`, czyli wynik zwrócony i zapisany. Zmienna `b` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła.

Konsekwencja jest praktyczna: tylko zwrócony wynik da się wykorzystać dalej. Dlatego `na_osobe(suma(mazury), 3)` działa: wynik jednej funkcji trafia jako argument do drugiej.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": [
    {
      "title": "Python 3.13 tutorial, kontrola przepływu (funkcje bez return zwracają None)",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/controlflow.rst",
      "supports": "Funkcja bez jawnego return zwraca None, a print(funkcja()) wypisuje None."
    },
    {
      "title": "Python 3.13 reference, simple statements (return)",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/reference/simple_stmts.rst",
      "supports": "Instrukcja return opuszcza funkcję i oddaje wartość wyrażenia. Bez wyrażenia oddaje None."
    }
  ]
}
````
