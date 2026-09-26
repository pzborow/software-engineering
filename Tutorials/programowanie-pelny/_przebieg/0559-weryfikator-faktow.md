# Krok 0559 · weryfikator_faktów

Węzeł: `review` · dział: 5 · pytanie: 31 · próba: 1

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

NOWA SEKCJA "Operatory „i” oraz „lub”":
[[operator-logiczny|Operatory logiczne]] `and` („i”) oraz `or` („lub”) łączą kilka warunków w jeden. Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: `True` albo `False`.

`and` daje `True` tylko wtedy, gdy prawdziwe są **oba** warunki. `or` daje `True`, gdy prawdziwy jest **którykolwiek** z nich, a `False` dopiero wtedy, gdy oba są fałszywe.

| Lewy warunek | Prawy warunek | `and` | `or` |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

Każdy z połączonych warunków zapisujemy w całości, tak jak w porównywaniu wartości. Wynik można wypisać albo wstawić do `if`:

```python
kwota = 45.5
liczba_osob = 3
print(kwota > 40 and liczba_osob > 5)
print(kwota > 100 or liczba_osob == 3)
if kwota > 100 or liczba_osob > 5:
    print("Duży wydatek")
else:
    print("Zwykły wydatek")
```

```text
False
True
Zwykły wydatek
```

W pierwszej linii drugi warunek zawiódł, więc `and` dało `False`. W drugiej wystarczył prawdziwy drugi warunek, więc `or` dało `True`. W `if` oba są fałszywe, więc zadziałało `else`.

Dla „Wspólnej Kasy” to znaczy, że wydatek można uznać za duży, gdy jest wysoki **lub** dzieli go dużo osób.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: True albo False. / and daje True tylko wtedy... or daje True...",
      "detail": "Dokumentacja Pythona 3.13 (https://docs.python.org/3.13/reference/expressions.html, sekcja Boolean operations) mówi, że and i or nie ograniczają zwracanej wartości do True/False, lecz zwracają ostatnio obliczony operand (np. `s or 'foo'`). Dla warunków będących porównaniami, jak w tej sekcji, wynik jest faktycznie True/False, więc kod i wyniki są poprawne. Można dodać zastrzeżenie, np. „gdy łączymy porównania, wynik to True albo False”, żeby czytelnik nie uogólnił tego później na inne wartości.",
      "source": "https://docs.python.org/3.13/reference/expressions.html"
    }
  ],
  "sources": [
    {
      "title": "Python 3.13 Language Reference: Expressions",
      "url": "https://docs.python.org/3.13/reference/expressions.html",
      "supports": "and/or zwracają ostatnio obliczony operand, a nie zawsze True/False; dla porównań wynik jest bool, więc przykład i jego wyjście (False, True, Zwykły wydatek) są poprawne."
    }
  ]
}
````
