# Krok 0106 · znudzony_czytelnik

Węzeł: `review` · dział: 2 · pytanie: 8 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak przepis kulinarny przypomina algorytm?".

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
## Czym jest algorytm
[[algorytm|Algorytm]] to skończony ciąg jednoznacznych kroków, który dla podanych danych prowadzi do wyniku. Nie jest jeszcze programem: to sam pomysł na rozwiązanie, który można zapisać zwykłymi słowami, na kartce albo w kodzie.

Dobry algorytm ma trzy cechy. Zaczyna od jasno określonych danych wejściowych. Każdy krok jest na tyle dokładny, że nie wymaga domyślania się: „Podziel sumę przez liczbę osób” jest jednoznaczne, a „rozlicz się jakoś sprawiedliwie” nie. Wreszcie po skończonej liczbie kroków algorytm się kończy i daje wynik.

Weźmy czworo znajomych na wyjeździe, którzy płacili na zmianę. Rozliczenie da się opisać tak:

```text
dane: lista wydatków (kto, ile) i liczba osób
1. Zsumuj wszystkie wydatki.
2. Podziel sumę przez liczbę osób: to udział jednej osoby.
3. Dla każdej osoby odejmij udział od tego, ile wydała.
4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna.
wynik: saldo każdej osoby
```

Na razie nie piszemy kodu: to celowo zwykły język. Ten sam algorytm można potem zapisać w Pythonie, w arkuszu kalkulacyjnym albo wykonać ręcznie. Właśnie dlatego warto go oddzielać od kodu.

Konsekwencja: zanim napiszesz program, upewnij się, że masz algorytm. Gdy kroki są jasne na papierze, zamiana ich na kod jest już głównie kwestią zapisu.

NOWA SEKCJA "Przepis jako algorytm":
Przepis kulinarny to [[algorytm|algorytm]] zapisany dla kucharza: ma dane wejściowe (składniki), uporządkowane kroki i wynik (gotowe danie). Różnica polega na tym, że człowiek wybaczy przepisowi niedokładność, a komputer nie.

Zestawmy oba zapisy:

| Przepis | Algorytm |
|---|---|
| składniki i ich ilości | dane wejściowe |
| kolejne kroki: „pokrój”, „wymieszaj” | jednoznaczne instrukcje |
| „piecz, aż się zrumieni” | warunek zakończenia |
| gotowe ciasto | wynik |

Przepis pokazuje też, gdzie kuchnia jest luźniejsza. „Dodaj szczyptę soli” czy „smaż chwilę” kucharz zinterpretuje po swojemu. W algorytmie musi stać coś takiego jak „Podziel sumę przez liczbę osób”, bez pola na domysły.

Ten sam przepis mogą wykonać różne osoby w różnych kuchniach i wyjdzie to samo danie. Tak samo algorytm da się wykonać w Pythonie, w arkuszu albo na kartce.

Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”. Jej przepis to [[lm-8|cztery kroki rozliczenia, które już znasz]]: składniki to wydatki i liczba osób, a „danie” to saldo każdego.

Konsekwencja: pisząc algorytm, wyobraź sobie przepis dla kogoś, kto nigdy nie gotował. Jeśli taka osoba wykona go bez pytań, kroki są dość dokładne.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "konkret",
      "severity": "blokująca",
      "target": "tabela, wiersz „piecz, aż się zrumieni”",
      "detail": "Tabela podaje „piecz, aż się zrumieni” jako wzorcowy warunek zakończenia. Tymczasem „zrumieni się” jest tak samo niejednoznaczne jak „smaż chwilę”, które tekst niżej krytykuje. Czytelnik może uznać, że takie zdanie nadaje się do algorytmu. Trzeba dać wersję mierzalną, np. „piecz 40 minut w 180°C” albo „piecz, aż temperatura w środku wyniesie 95°C”. Warto też jednym zdaniem wyjaśnić, że warunek zakończenia to sprawdzalny test „czy już koniec?”.",
      "source": "",
      "status": "nowa"
    },
    {
      "kind": "tempo",
      "severity": "sugestia",
      "target": "akapity o wykonaniu w Pythonie/arkuszu i o „Wspólnej Kasie”",
      "detail": "Akapit „ten sam przepis w różnych kuchniach” powtarza to, co poprzednia sekcja już powiedziała o Pythonie, arkuszu i kartce. Akapit o „Wspólnej Kasie” też niewiele dodaje, bo cztery kroki rozliczenia były już podane. Można je skrócić do jednego zdania albo usunąć i zwolnić miejsce na mierzalny przykład kroku przepisu.",
      "source": "",
      "status": "nowa"
    }
  ]
}
````
