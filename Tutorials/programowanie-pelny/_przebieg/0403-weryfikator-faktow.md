# Krok 0403 · weryfikator_faktów

Węzeł: `review` · dział: 4 · pytanie: 23 · próba: 1

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

NOWA SEKCJA "Czym jest typ danych":
[[typ-danych|Typ danych]] to rodzaj wartości, który mówi Pythonowi, czym ta wartość jest i jakie działania są na niej dozwolone. Wcześniej pisaliśmy po prostu „rodzaj danych”, teraz mamy na to fachową nazwę.

Typ ma każda wartość, także ta ukryta w zmiennej. Python rozpoznaje go po zapisie: cudzysłów oznacza tekst, cyfry z kropką ułamek, a `True` lub `False` prawdę albo fałsz. Dlatego `"45.5"` to [[cztery znaki zamiast kwoty|tylko cztery znaki: 4, 5, kropka, 5]], a nie pieniądze. Typ sprawdzisz funkcją `type()`.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(type(imie))
print(type(kwota))
print(type(zaplacono))
```

```text
<class 'str'>
<class 'float'>
<class 'bool'>
```

Słowo `class` na razie pomiń, ważna jest nazwa po nim. Oto podstawowe typy Pythona:

| Nazwa w Pythonie | Co to jest | Przykład |
|---|---|---|
| `str` | tekst | `"Ania"` |
| `int` | liczba całkowita | `3` |
| `float` | liczba z ułamkiem | `45.5` |
| `bool` | prawda lub fałsz | `True` |

Typ decyduje o tym, co program może zrobić z wartością. Dlatego [[imienia nie da się podzielić|imienia nie podzielisz przez 2]], a kwotę tak. Typem `bool` zajmiemy się osobno, w kolejnej sekcji.

Konsekwencja: gdy program zachowuje się dziwnie, jedno z pierwszych pytań brzmi „jakiego typu jest ta wartość?”.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": [
    {
      "title": "Python 3.13 typing docs (przykład z type(a) dla int)",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/library/typing.rst",
      "supports": "type() zwraca typ wartości (type(3) to int); nazwy int oraz typ obiektu zgadzają się z tabelą sekcji."
    },
    {
      "title": "Python 3.13 built-in functions (type())",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/library/functions.rst",
      "supports": "type(obiekt) jest wbudowaną funkcją zwracającą typ obiektu; w Pythonie 3 typy wbudowane są klasami, więc wynik ma postać <class 'str'>."
    }
  ]
}
````
