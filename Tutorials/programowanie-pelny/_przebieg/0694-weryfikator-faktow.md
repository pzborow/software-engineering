# Krok 0694 · weryfikator_faktów

Węzeł: `review` · dział: 6 · pytanie: 37 · próba: 2

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

NOWA SEKCJA "Pętla po elementach listy":
Przez wszystkie elementy [[lista-danych|listy]] przechodzisz [[petla|pętlą]] `for`: `for imie in osoby:` bierze po kolei każdy [[element-listy|element]] i wykonuje dla niego wcięty blok.

Przy pierwszym przebiegu (czyli [[iteracja|iteracji]]) `imie` dostaje pierwszy element, przy drugim drugi, i tak do ostatniego. Gdy elementy się skończą, pętla sama przestaje, a program idzie dalej, do pierwszej linii bez wcięcia. Nie liczysz indeksów ani nie sprawdzasz długości listy.

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print(imie)
print("Koniec")
```

```text
Ania
Bartek
Celina
Koniec
```

Elementy przychodzą w kolejności listy, więc „Ania” jest pierwsza. Dodasz czwartą osobę, a ta sama pętla obsłuży ją bez zmian.

Pętla może też coś zbierać. Przy liście `wydatki` dodaje kwotę każdego wydatku do sumy; zapis `wydatek["kwota"]` bierze z jednego wydatku pole `kwota`:

```python
wydatki = ...
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(suma)
```

Suma zaczyna od zera, rośnie w każdej iteracji, a wynik pokazujesz dopiero po pętli, już bez wcięcia.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": [
    {
      "title": "Python 3.13 tutorial: More Control Flow Tools (for statements)",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/controlflow.rst",
      "supports": "Pętla `for` iteruje po elementach sekwencji (np. listy) w kolejności ich występowania, a przykład `for w in words:` odpowiada składni `for imie in osoby:`."
    },
    {
      "title": "Python 3.13 language reference: Compound statements (for)",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/reference/compound_stmts.rst",
      "supports": "Zmienna pętli jest przy każdej iteracji nadpisywana kolejnym elementem, więc `imie` dostaje po kolei każdy element."
    }
  ]
}
````
