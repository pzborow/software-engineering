# Krok 1170 · weryfikator_faktów

Węzeł: `review` · dział: 10 · pytanie: 61 · próba: 1

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

NOWA SEKCJA "Automatyzacja prostych zadań":
[[automatyzacja|Automatyzacja]] to zlecenie komputerowi powtarzalnej czynności, którą wcześniej robiłeś(-aś) ręcznie. Osoba spoza IT zyskuje na niej czas i pewność: komputer nie nudzi się, nie myli przy setnej pozycji i robi to samo za każdym razem.

Mechanizm znasz: to [[petla|pętla]] i [[funkcja|funkcja]] na Twoich danych. Zamiast przepisywać kwoty do kalkulatora, opisujesz kroki raz, a program wykonuje je dla dowolnej liczby pozycji:

```python
faktury = [1000, 250, 50]
razem = 0
for kwota in faktury:
    razem = razem + kwota
vat = round(razem * 0.23, 2)
print(f"Netto: {razem} zł")
print(f"VAT 23%: {vat} zł")
print(f"Brutto: {razem + vat} zł")
```

```text
Netto: 1300 zł
VAT 23%: 299.0 zł
Brutto: 1599.0 zł
```

Jutro lista ma 200 faktur zamiast trzech, a kod zostaje ten sam. Podobnie działa Twój `dlugi.py`: raz opisany podział rachunku liczy się sam.

Nie automatyzuj wszystkiego. Opłaca się zadanie, które powtarzasz często, ma jasne reguły i da się sprawdzić na kartce. Zadanie robione raz w roku lub wymagające oceny człowieka zwykle lepiej zostawić sobie.

Konsekwencja jest praktyczna: zaczynasz od małego, nudnego zadania z własnej pracy i piszesz je tą samą pętlą nauki. Po commicie masz gotowe narzędzie, do którego możesz wracać.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": []
}
````
