# Krok 0685 · weryfikator_faktów

Węzeł: `review` · dział: 6 · pytanie: 37 · próba: 1

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

Działa to tak: przy pierwszym przebiegu (czyli [[iteracja|iteracji]]) `imie` dostaje pierwszy element, przy drugim drugi, i tak do ostatniego. Kiedy elementy się skończą, pętla sama przestaje, a program idzie dalej, do pierwszej linii bez wcięcia. Nie liczysz indeksów ani nie sprawdzasz długości listy.

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

Elementy przychodzą w kolejności listy, więc „Ania" jest pierwsza, tak jak w sekcji o liście. Dodasz czwartą osobę, a ta sama pętla obsłuży ją bez zmiany kodu.

Nazwa `imie` jest zwykłą zmienną: po pętli zachowuje wartość ostatniego elementu. Wybierz ją tak, by mówiła, co jest na liście, a nie „x".

Pętla może też coś zbierać, np. dodawać kolejne kwoty do sumy. Tak robi Twój `kasa.py`: wypisuje każdą kwotę, sumuje je i dopiero po pętli pokazuje wynik.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "po pętli zachowuje wartość ostatniego elementu",
      "detail": "Dokumentacja (https://docs.python.org/3.13/reference/compound_stmts.html, instrukcja for) potwierdza, że nazwy z pętli nie są usuwane po jej zakończeniu. Dodaje jednak, że dla pustej listy zmienna nie zostanie w ogóle przypisana (późniejsze użycie da NameError). Twierdzenie jest poprawne dla listy z elementami; można dodać zastrzeżenie „jeśli lista nie była pusta”.",
      "source": "docs.python.org",
      "status": "nowa"
    }
  ],
  "sources": [
    {
      "title": "Compound statements: The for statement (Python 3.13)",
      "url": "https://docs.python.org/3.13/reference/compound_stmts.html",
      "supports": "Pętla kończy się po wyczerpaniu elementów, a nazwa zmiennej pętli zachowuje ostatnią wartość po pętli (przy pustej liście nie jest przypisana). Kod przykładowy jest poprawny i daje podany wynik."
    }
  ]
}
````
