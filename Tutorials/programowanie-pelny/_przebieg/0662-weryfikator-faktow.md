# Krok 0662 · weryfikator_faktów

Węzeł: `review` · dział: 6 · pytanie: 36 · próba: 1

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

Wygląda to dziwnie, ale trzeba się przyzwyczaić: indeks mówi, o ile miejsc od początku listy się przesunąć. Pierwszy element jest na początku, więc przesunięcie wynosi zero. Kolejność z listy zostaje zachowana, o czym była mowa w sekcji [[sec-06-czym-jest-lista-danych|Czym jest lista danych]].

Ujemny indeks liczy od końca: `-1` to ostatni element, `-2` przedostatni. Wygodne, gdy nie wiesz, ile elementów ma lista.

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

Indeks spoza listy kończy się błędem `IndexError`. Przy trzech osobach ostatni jest `osoby[2]`, a `osoby[3]` nie istnieje, więc program się zatrzyma. Największy poprawny indeks to zawsze `len(osoby) - 1`.

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
      "detail": "W Pythonie odczyt `lista[i]` zwraca odwołanie do tego samego obiektu, nie jego kopię. Dla liczb i napisów (niezmiennych) różnicy nie widać, ale dla elementu-listy zmiana zwróconego obiektu zmieni też listę. Dla poziomu początkującego bezpieczniej: „dostajesz wartość elementu, lista się nie zmienia”. Zob. https://docs.python.org/3.13/reference/datamodel.html",
      "source": "https://docs.python.org/3.13/reference/datamodel.html"
    }
  ],
  "sources": [
    {
      "title": "Python 3.13 tutorial: An Informal Introduction to Python (indeksowanie, indeksy ujemne)",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/introduction.rst",
      "supports": "Indeksy liczone od 0; ujemne liczą od końca (-1 ostatni, -2 przedostatni); potwierdza wynik `osoby[-1]` w przykładzie."
    },
    {
      "title": "Python 3.13 stdtypes: sequence types (range example)",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/library/stdtypes.rst",
      "supports": "Indeksowanie ujemne działa na sekwencjach (r[-1] to ostatni element)."
    }
  ]
}
````
