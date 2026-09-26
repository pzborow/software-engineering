# Krok 0174 · znudzony_czytelnik

Węzeł: `review` · dział: 2 · pytanie: 12 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Co to znaczy, że algorytm jest poprawny?".

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
## Podział problemu na części
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

NOWA SEKCJA "Poprawny algorytm":
[[algorytm|Algorytm]] jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny z tym, czego od niego wymagamy. Nie wystarczy, że zadziałał raz na jednym przykładzie.

Najpierw trzeba więc ustalić, co znaczy „zgodny”. To [[specyfikacja-wyniku|specyfikacja wyniku]]: krótki opis, jaki wynik ma wyjść z jakich danych. Dla rozliczenia może brzmieć tak: suma wszystkich sald wynosi 0 zł, a nikomu nie znika ani nie przybywa grosza. Bez takiego opisu nie ma czego sprawdzać.

Potem sprawdzasz dwie rzeczy: czy algorytm zawsze dochodzi do [[warunek-zakonczenia|warunku zakończenia]] i czy wynik spełnia specyfikację. Ważne są zwłaszcza [[przypadek-brzegowy|przypadki brzegowe]], czyli dane na skraju dozwolonego zakresu: jedna osoba, brak wydatków, kwota, która nie dzieli się równo.

Ten ostatni przypadek łatwo przeoczyć. W kodzie kwoty liczymy w groszach, a znak `//` dzieli i odrzuca resztę: `10000 // 3` daje `3333`, nie `3333,33`.

```python
# poza kanonem: udział w groszach, dzielenie całkowite
def udzial(suma_gr, osoby):
    return suma_gr // osoby

print(udzial(12000, 4) * 4)
print(udzial(10000, 3) * 3)
```

```text
12000
9999
```

Dla 120 zł na czworo wszystko się zgadza. Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza. Dlatego w naszej liście kroków jest zdanie „Resztę groszy dopisz pierwszej osobie.”: bez niego algorytm byłby niepoprawny, choć pierwszy przykład by przeszedł.

Konsekwencja: poprawność sprawdzasz na wielu danych, w tym celowo niewygodnych. Do systematycznego sprawdzania wrócimy przy testowaniu programu.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
