# Krok 0808 · weryfikator_faktów

Węzeł: `review` · dział: 7 · pytanie: 42 · próba: 1

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
  "needs": [],
  "sources": []
}
````
