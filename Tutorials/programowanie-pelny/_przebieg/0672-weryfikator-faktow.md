# Krok 0672 · weryfikator_faktów

Węzeł: `review` · dział: 6 · pytanie: 36 · próba: 2

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

NOWA SEKCJA "Odczyt elementu listy":
Po element listy sięgasz przez jego numer w nawiasach kwadratowych: `osoby[0]`. Numer nazywa się [[indeks|indeksem]] i liczenie zaczyna się od zera, więc pierwszy element ma indeks 0, drugi 1, trzeci 2.

Wygląda to dziwnie, ale indeks mówi, o ile miejsc od początku listy się przesunąć. Pierwszy element jest na samym początku, więc przesunięcie wynosi zero. Kolejność zostaje taka, jak w sekcji Czym jest lista danych.

Ujemny indeks liczy od końca: `-1` to ostatni element, `-2` przedostatni. Jest wygodny, gdy nie wiesz, ile elementów ma lista.

```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby[0])
print(osoby[2])
print(osoby[-1])
```

```text
Ania
Celina
Celina
```

Indeks spoza listy kończy się błędem `IndexError`. Przy trzech osobach ostatni jest `osoby[2]`, a `osoby[3]` nie istnieje, więc program się zatrzyma. Największy poprawny indeks to `len(osoby) - 1`.

Odczyt niczego nie zmienia: lista zostaje taka sama, dostajesz tylko kopię wartości.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "dostajesz tylko kopię wartości",
      "detail": "Dokumentacja opisuje indeksowanie (https://docs.python.org/3.13/tutorial/introduction.html), ale w Pythonie odczyt zwraca referencję do tego samego obiektu, nie kopię. Dla liczb i napisów (niezmiennych) różnica jest niewidoczna, a dla zagnieżdżonych list byłaby. Bezpieczniej: „dostajesz wartość tego elementu, lista się nie zmienia”."
    }
  ],
  "sources": [
    {
      "title": "An Informal Introduction to Python (3.13)",
      "url": "https://docs.python.org/3.13/tutorial/introduction.html",
      "supports": "Indeksowanie od zera, indeksy ujemne liczone od końca (-1 ostatni, -2 przedostatni) i IndexError dla indeksu spoza zakresu; przykład kodu daje wskazane wyniki."
    }
  ]
}
````
