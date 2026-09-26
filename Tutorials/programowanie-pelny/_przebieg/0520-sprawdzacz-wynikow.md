# Krok 0520 · sprawdzacz_wyników

Węzeł: `review` · dział: 5 · pytanie: 29 · próba: 1

## Prompt

````text
Jesteś sprawdzaczem wyników w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.

Dla każdego bloku kodu, który da się uruchomić samodzielnie (ma wszystkie dane, nie zawiera `...`) i coś wypisuje:
1. Czy bezpośrednio pod nim jest blok ```text z wynikiem? Brak: kind="wynik", severity="blokująca",
   detail = dokładny wynik, który trzeba dopisać.
2. Wykonaj kod w myślach krok po kroku (wartości, obliczenia, zaokrąglenia, formatowanie, kolejność linii)
   i porównaj z podanym wynikiem znak w znak. Niezgodność: kind="wynik", severity="blokująca",
   detail = co się nie zgadza i poprawny wynik.
Szkice (z `...`, bez danych) i bloki bez wypisywania pomiń. ok=true, gdy wszystko się zgadza.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

SEKCJA "Instrukcja warunkowa „jeśli… to…”":
[[instrukcja-warunkowa|Instrukcja warunkowa]] to polecenie, które wykonuje wybrany fragment kodu tylko wtedy, gdy warunek jest prawdziwy. W Pythonie zapisujemy ją słowem `if`, czyli „jeśli”.

Warunek to zwykle porównanie z poprzedniej sekcji, bo daje `True` albo `False`. Jeśli wynik to `True`, Python wykonuje zapisane pod spodem linie. Jeśli `False`, pomija je i idzie dalej.

Które linie należą do warunku, pokazuje [[wciecie|wcięcie]]: przesunięcie linii o cztery spacje w prawo. Po warunku stawiamy dwukropek.

```python
kwota = 45.5
if kwota > 40:
    print("Wydatek do sprawdzenia")
if kwota > 100:
    print("Bardzo duży wydatek")
print("Koniec")
```

```text
Wydatek do sprawdzenia
Koniec
```

Pierwszy warunek jest prawdziwy, więc jego linia się wykonała. Drugi jest fałszywy, więc jego wcięta linia została pominięta. Ostatni `print` nie ma wcięcia, więc należy do całego programu i wykonuje się zawsze.

Program przestaje więc biegnąć wszystkimi liniami po kolei: to, co wykona, zależy od danych. Co zrobić, gdy warunek jest fałszywy, pokażemy w następnej sekcji.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
