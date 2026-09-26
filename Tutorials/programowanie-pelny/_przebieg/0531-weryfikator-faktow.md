# Krok 0531 · weryfikator_faktów

Węzeł: `review` · dział: 5 · pytanie: 29 · próba: 2

## Prompt

````text
Jesteś weryfikatorem faktów tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Wersje obowiązujące w tutorialu: Python 3.13. Wersje zadeklarowane w sekcji: Python 3.13.

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

NOWA SEKCJA "Instrukcja warunkowa „jeśli… to…”":
[[instrukcja-warunkowa|Instrukcja warunkowa]] to polecenie, które wykonuje wybrany fragment kodu tylko wtedy, gdy warunek jest prawdziwy. W Pythonie zapisujemy ją słowem `if`, czyli „jeśli”.

Warunek to zwykle porównanie z poprzedniej sekcji, bo daje `True` albo `False`. Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej.

Które linie należą do warunku, pokazuje [[wciecie|wcięcie]]: przesunięcie linii o cztery spacje w prawo. Po warunku stawiamy dwukropek.

```python
kwota = 45.5
if kwota > 40:
    print("Kwota do sprawdzenia")
if kwota > 100:
    print("Bardzo duża kwota")
print("Koniec")
```

```text
Kwota do sprawdzenia
Koniec
```

Pierwszy warunek jest prawdziwy, więc jego linia się wykonała. Drugi jest fałszywy, więc jego wcięta linia została pominięta. Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.

Program przestaje więc biegnąć wszystkimi liniami po kolei: to, co wykona, zależy od danych. Co zrobić, gdy warunek jest fałszywy, pokażemy w następnej sekcji.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Wcięcie: „przesunięcie linii o cztery spacje w prawo”",
      "detail": "Dokumentacja Pythona (https://docs.python.org/3.13/reference/compound_stmts.html) nie wymaga czterech spacji. Wymaga spójnego wcięcia w całym bloku, a cztery spacje to konwencja z PEP 8. Kod z sekcji działa poprawnie. Warto napisać np. „zwykle o cztery spacje (przyjęta konwencja); ważne, by w bloku było tak samo”."
    }
  ],
  "sources": [
    {
      "title": "Compound statements — Python 3.13 documentation",
      "url": "https://docs.python.org/3.13/reference/compound_stmts.html",
      "supports": "Składnia `if warunek:` z dwukropkiem i blokiem wciętych linii (suite); dokumentacja wymaga spójnego wcięcia, a nie dokładnie czterech spacji."
    }
  ]
}
````
