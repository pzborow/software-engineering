# Krok 0625 · weryfikator_faktów

Węzeł: `review` · dział: 6 · pytanie: 34 · próba: 2

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

NOWA SEKCJA "Pętla nieskończona":
[[petla-nieskonczona|Pętla nieskończona]] to pętla, która nigdy nie dochodzi do końca, bo jej [[warunek-zakonczenia|warunek zakończenia]] nigdy nie zostaje spełniony. Program powtarza wtedy ten sam fragment bez końca, więc nie dociera do dalszych linii i nie oddaje wyniku.

Pętla `for`, którą znasz, kończy się sama, bo zestaw danych się wyczerpuje. Pętla `while` („dopóki”) działa inaczej: powtarza wcięte linie, dopóki warunek daje `True`. Jeśli warunek jest zawsze prawdziwy, każda kolejna [[iteracja|iteracja]] zaczyna się od nowa.

```python
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

Tu warunek to na stałe `True`, a w ciele nic go nie zmienia. Linia `time.sleep(1)` robi tylko jednosekundową przerwę, żeby napisy nie zalały ekranu. Zdarza się to też przez pomyłkę: warunek zależy od zmiennej, której pętla nigdy nie zmienia.

Problem jest praktyczny. Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków. Tak samo wyglądałaby „Wspólna Kasa”, która czeka na koniec listy, którego nie ma.

Zatrzymasz taki program skrótem Ctrl+C w terminalu. Python przerywa wtedy działanie i wypisuje komunikat `KeyboardInterrupt`, czyli „przerwano z klawiatury”. To nie awaria, tylko Twoja komenda.

Dlatego przy każdej pętli `while` zadaj sobie pytanie: co sprawi, że warunek w końcu stanie się fałszywy?
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków.",
      "detail": "Dokumentacja time.sleep (https://docs.python.org/3.13/library/time.html) mówi, że sleep zawiesza wykonanie wątku na podany czas. Pętla z przykładu, z time.sleep(1), prawie nie obciąża procesora. Twierdzenie o zajmowaniu procesora jest prawdziwe dla pętli bez sleep. Można dopisać „pętla bez przerwy zajmuje procesor” albo „program bez sleep zajmuje procesor”. Przykład ze sleep nie wygląda też na zawieszony, bo wypisuje napisy. To tylko nieścisłość, kod działa zgodnie z opisem.",
      "source": "https://docs.python.org/3.13/library/time.html"
    }
  ],
  "sources": [
    {
      "title": "Compound statements (while)",
      "url": "https://docs.python.org/3.13/reference/compound_stmts.html",
      "supports": "Pętla while powtarza ciało, dopóki warunek jest prawdziwy. Kod `while True:` jest poprawny."
    },
    {
      "title": "Built-in Exceptions (KeyboardInterrupt)",
      "url": "https://docs.python.org/3.13/library/exceptions.html",
      "supports": "KeyboardInterrupt jest zgłaszany, gdy użytkownik naciśnie klawisz przerwania, zwykle Control-C."
    },
    {
      "title": "time — Time access and conversions",
      "url": "https://docs.python.org/3.13/library/time.html",
      "supports": "time.sleep(1) zawiesza wykonanie na 1 sekundę. Wywołanie w tym przykładzie jest poprawne."
    }
  ]
}
````
