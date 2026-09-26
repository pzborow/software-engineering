# Krok 0738 · weryfikator_faktów

Węzeł: `review` · dział: 7 · pytanie: 39 · próba: 1

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

NOWA SEKCJA "Po co dzielić program na funkcje":
Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach.

Zobacz to na „Wspólnej Kasie”. Sumę wydatków wydzieliliśmy już do funkcji, a teraz dokładamy drugą, która z niej korzysta:

```python
def suma_wydatkow(wydatki):
    suma = 0
    for wydatek in wydatki:
        suma = suma + wydatek["kwota"]
    return suma

def udzial_na_osobe(wydatki, liczba_osob):
    return suma_wydatkow(wydatki) / liczba_osob

mazury = [{"kto": "Ania", "kwota": 120.5}, {"kto": "Bartek", "kwota": 79.5}]
tatry = [{"kto": "Celina", "kwota": 450}]
print(udzial_na_osobe(mazury, 2))
print(udzial_na_osobe(tatry, 3))
```

```text
100.0
150.0
```

Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz. Gdyby liczenie sumy trzeba było kiedyś zmienić, poprawiasz jedną funkcję, a oba wyniki będą poprawne.

Druga korzyść to czytelność: `udzial_na_osobe(mazury, 2)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, do czego wrócimy przy testowaniu programu.

U siebie masz już `funkcje.py` z jedną funkcją. Za chwilę dopiszesz drugą i użyjesz obu dla dwóch wyjazdów.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": []
}
````
