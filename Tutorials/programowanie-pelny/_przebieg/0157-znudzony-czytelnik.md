# Krok 0157 · znudzony_czytelnik

Węzeł: `review` · dział: 2 · pytanie: 11 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak podzielić duży problem na mniejsze części?".

Zgłoś potrzeby (najwyżej 3, zero też jest dobrą odpowiedzią), wybierając kind:
- "przykład": teza jest abstrakcyjna i brakuje krótkiego kodu lub scenariusza,
- "konkret": ogólniki zamiast decyzji, liczby, nazwy klasy albo porównania,
- "skrócenie": powtórzenia, lanie wody, przykład dłuższy niż potrzeba,
- "diagram": przepływ łatwiej zrozumieć z rysunku tekstowego,
- "tempo": za dużo nowych pojęć naraz albo sekcja nie wnosi nic nowego względem poprzedniej.
Sekcja ma limit 250 słów prozy i jeden, najwyżej dwa krótkie bloki kodu.
Nie proś o coś, co się w tym nie zmieści, i nie żądaj jednocześnie dodania i skrócenia.
Kod może być tylko w językach: python, text.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

POPRZEDNIA SEKCJA:
## Czym jest schemat blokowy
[[schemat-blokowy|Schemat blokowy]] to rysunek [[algorytm|algorytmu]]: każdy krok jest w ramce, a strzałki pokazują, w jakiej kolejności je wykonać. Działa jak mapa, po której palcem przejdziesz od początku do końca.

Używa kilku umownych kształtów. Owal oznacza początek albo koniec, prostokąt to zwykły krok, a romb to pytanie, po którym droga rozwidla się na „tak” i „nie”. Krok wykonujesz, gdy dojdziesz do niego strzałką, a nie dlatego, że stoi niżej na kartce.

Oto rozliczenie „Wspólnej Kasy” z trzema osobami, narysowane znakami tekstowymi:

```text
( Start )
    v
[ Zsumuj wydatki, podziel przez liczbę osób = udział ]
    v
[ Weź kolejną osobę ]
    v
< Wpłaciła więcej niż udział? > --tak--> [ Ma zwrot ] --+
    |nie                                                |
    v                                                   |
[ Ma dopłacić ] ----------------------------------------+
    v
< Są jeszcze osoby? > --tak--> (wróć do „Weź kolejną osobę”)
    |nie
    v
( Koniec )
```

Rysunek ma dwie zalety. Rozgałęzienia i powroty widać od razu, a w opisie słownym łatwo je przeoczyć. Poza tym pokazuje, gdzie algorytm się kończy, czyli sprawdzalny [[warunek-zakonczenia|warunek zakończenia]].

Konsekwencja: schemat pozwala sprawdzić algorytm na kartce, zanim powstanie [[kod|kod]]. Wrócimy do niego przy podziale problemu na części, a „Wspólna Kasa”, przykład, który będzie nam towarzyszył, dostanie z niego kod dopiero później.

NOWA SEKCJA "Podział problemu na części":
Duży problem dzielisz tak, by każda część miała własne dane wejściowe, jedno zadanie i wynik, który da się sprawdzić osobno. Zaczynasz od całego zadania, a potem pytasz: z jakich mniejszych kroków się składa?

Weźmy „rozlicz wyjazd”. To za dużo naraz, więc rozbijamy to na trzy części. Wracamy tu do [[schemat-blokowy|schematu blokowego]] z poprzedniej sekcji: kroki w jego ramkach to gotowe kandydatki na części.

```text
Rozlicz wyjazd
  |-- 1. Zsumuj wydatki          (wydatki -> suma)
  |-- 2. Policz udział osoby     (suma, liczba osób -> udział)
  `-- 3. Porównaj wpłatę z udziałem
                                 (wpłata, udział -> saldo)
```

Każda część ma jasne wejście i wynik. Część 3 potrzebuje wyniku części 2, a ta wyniku części 1, więc kolejność wynika z tych zależności, tak jak w sekcji o kolejności kroków.

Jeśli część nadal jest zbyt duża, dziel ją dalej, aż każdą da się opisać jednym zdaniem. Dobra część daje się też przetestować samodzielnie: znasz jej dane i wiesz, jaki wynik ma wyjść.

Konsekwencja: w programie takie części zamienimy w osobne [[funkcja|funkcje]], czyli nazwane fragmenty kodu do wielokrotnego użycia. Ich nazwy, np. `suma_wydatkow`, poznasz później, gdy zaczniemy pisać „Wspólną Kasę”, przykład, który będzie nam towarzyszył w kolejnych działach.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Zdanie „znasz jej dane i wiesz, jaki wynik ma wyjść” jest ogólnikiem. Wystarczy jedna liczbowa próba, np. wydatki 30, 50 i 20 zł dają sumę 100 zł, a przy 4 osobach udział wynosi 25 zł. Wtedy czytelnik zobaczy, co znaczy „sprawdzić osobno”.",
      "severity": "sugestia",
      "target": "Dobra część daje się przetestować samodzielnie"
    },
    {
      "kind": "skrócenie",
      "detail": "Zdanie o „Wspólnej Kasie”, przykładzie na kolejne działy, powtarza końcówkę poprzedniej sekcji. Można je usunąć, a zwolnione miejsce przeznaczyć na liczbowy przykład.",
      "severity": "sugestia",
      "target": "Ostatni akapit („Konsekwencja”)"
    }
  ]
}
````
