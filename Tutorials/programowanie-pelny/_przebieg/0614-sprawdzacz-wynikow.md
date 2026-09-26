# Krok 0614 · sprawdzacz_wyników

Węzeł: `review` · dział: 6 · pytanie: 34 · próba: 1

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

SEKCJA "Pętla nieskończona":
[[petla-nieskonczona|Pętla nieskończona]] to pętla, która nigdy nie dochodzi do końca, bo jej [[warunek-zakonczenia|warunek zakończenia]] nigdy nie zostaje spełniony. Program powtarza wtedy ten sam fragment bez końca, więc nie dociera do dalszych linii i nie oddaje wyniku.

Pętla `for`, którą znasz, kończy się sama, bo zestaw danych się wyczerpuje. Pętla `while` („dopóki”) działa inaczej: powtarza wcięte linie, dopóki warunek daje `True`. Jeśli warunek jest zawsze prawdziwy, każda kolejna [[iteracja|iteracja]] zaczyna się od nowa.

```python
while True:
    print("Liczę wydatki...")
    ...
```

Tu warunek to na stałe `True`, a w ciele nic go nie zmienia. Zdarza się to też przez pomyłkę: warunek zależy od zmiennej, której pętla nigdy nie zmienia.

Problem jest praktyczny. Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków. Tak samo wyglądałaby „Wspólna Kasa”, która czeka na koniec listy, którego nie ma.

Zatrzymasz taki program skrótem Ctrl+C w terminalu. Python przerywa wtedy działanie i wypisuje komunikat `KeyboardInterrupt`, czyli „przerwano z klawiatury”. To nie awaria, tylko Twoja komenda.

Dlatego przy każdej pętli `while` zadaj sobie pytanie: co sprawi, że warunek w końcu stanie się fałszywy?
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
