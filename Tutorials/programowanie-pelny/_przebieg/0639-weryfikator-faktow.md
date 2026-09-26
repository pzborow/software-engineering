# Krok 0639 · weryfikator_faktów

Węzeł: `review` · dział: 6 · pytanie: 35 · próba: 1

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

NOWA SEKCJA "Czym jest lista danych":
[[lista-danych|Lista danych]] to jedna zmienna, która przechowuje wiele wartości w ustalonej kolejności. Zamiast trzech zmiennych z imionami masz jedną nazwę, pod którą leży cały zestaw.

To właśnie po takim zestawie chodzi [[sec-06-czym-jest-petla|pętla]] `for`. Do tej pory w kasa.py miałeś jedną listę kwot; teraz przyjrzymy się jej samej.

Listę zapisujesz w nawiasach kwadratowych, a wartości oddzielasz przecinkami. Każda wartość to [[element-listy|element listy]], czyli jedno miejsce w zestawie. Tekst ma cudzysłów, liczba nie, tak samo jak przy zwykłych zmiennych.

```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby)
print(len(osoby))
```

```text
['Ania', 'Bartek', 'Celina']
3
```

Funkcja `len()` podaje długość listy, czyli liczbę elementów. Python wypisuje listę w nawiasach, a teksty w apostrofach; to tylko sposób wyświetlania.

Kolejność ma znaczenie: „Ania” jest pierwsza i tak zostaje. Lista może być też dłuższa albo pusta (`[]`), a program nie musi z góry znać jej rozmiaru. Dlatego pasuje do „Wspólnej Kasy”: `osoby` to uczestnicy wyjazdu, a `wydatki` to wszystkie zapłacone rachunki, których przybywa.

Jak sięgnąć po jeden element, omówimy osobno. To, co lista daje pętli, zobaczysz przy przechodzeniu przez wszystkie elementy.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": [
    {
      "title": "Python 3.13 tutorial: An Informal Introduction (introduction.rst, CPython v3.13.9)",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/introduction.rst",
      "supports": "len() zwraca liczbę elementów listy; napisy w interpreterze i w wypisanej liście są pokazywane w apostrofach (repr), a listę zapisuje się w nawiasach kwadratowych z przecinkami."
    }
  ]
}
````
