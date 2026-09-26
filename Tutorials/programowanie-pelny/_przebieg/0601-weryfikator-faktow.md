# Krok 0601 · weryfikator_faktów

Węzeł: `review` · dział: 6 · pytanie: 33 · próba: 1

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

NOWA SEKCJA "Kiedy sięgnąć po pętlę":
Pętli warto użyć, gdy ta sama czynność dotyczy wielu elementów albo liczba powtórzeń zależy od danych. Jeśli kopiujesz linię i zmieniasz w niej tylko jedną wartość, to znak, że potrzebna jest [[petla|pętla]].

Powtarzanie ręczne ma dwie wady. Poprawkę trzeba wprowadzić w wielu miejscach, a przy każdej łatwo o pomyłkę. Poza tym taki kod nie dopasuje się do danych: napisany na trzy osoby nie obsłuży czwartej.

```python
osoby = ["Ania", "Bartek", "Celina"]
liczba_osob = 3
for imie in osoby:
    print(imie, "płaci", 300 / liczba_osob)
```

```text
Ania płaci 100.0
Bartek płaci 100.0
Celina płaci 100.0
```

Zmienia się tylko `imie`, więc reszta linii jest zapisana jeden raz. Poprawka wzoru to jedna zmiana zamiast trzech.

| Sytuacja | Rozwiązanie |
|---|---|
| Ta sama czynność dla każdego elementu zestawu | pętla |
| Liczba powtórzeń zależy od danych | pętla |
| Dwie różne czynności, każda raz | zwykłe linie |
| Pojedyncza czynność, która się nie powtarza | zwykła linia |

Pętla `for` ma z góry znany koniec. Pętlę, która nigdy się nie kończy, omówimy w następnej kolejności.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Pętla `for` ma z góry znany koniec.",
      "detail": "Dla list i zakresów (range) to prawda, ale dokumentacja Pythona (https://docs.python.org/3/reference/compound_stmts.html#the-for-statement) mówi, że `for` iteruje po dowolnym iterowalnym obiekcie, a taki obiekt może nie mieć końca (np. itertools.count()). Dla początkującego zdanie jest bezpieczne; dokładniej: „`for` przechodzi po elementach zestawu, więc kończy się razem z nim”.",
      "source": "",
      "status": "nowa"
    }
  ],
  "sources": []
}
````
