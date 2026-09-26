# Krok 0089 · znudzony_czytelnik

Węzeł: `review` · dział: 2 · pytanie: 7 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym jest algorytm?".

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
## Program a aplikacja
Program to ciąg instrukcji, które komputer wykonuje. [[aplikacja|Aplikacja]] to program (albo zestaw programów) przygotowany tak, by zwykły użytkownik mógł z niego wygodnie korzystać: z oknem, przyciskami, zapisem danych i instrukcją obsługi. Każda aplikacja jest więc programem, ale nie każdy program jest aplikacją.

Różnica dotyczy głównie tego, dla kogo coś powstało. Program może być krótkim skryptem napisanym dla siebie, który robi jedną rzecz i nie ma żadnej oprawy. Aplikacja musi jeszcze radzić sobie z pomyłkami użytkownika, zapamiętywać jego dane i być zrozumiała bez znajomości kodu.

| | Program | Aplikacja |
|---|---|---|
| Dla kogo | często dla autora | dla wielu użytkowników |
| Wygląd | może być sam tekst w terminalu | okna, przyciski, menu |
| Obsługa błędów | minimalna | przewidziane komunikaty i pomoc |
| Przykład | kilka linii liczących rachunek | arkusz kalkulacyjny, aplikacja bankowa |

W praktyce granica jest płynna, a w mowie potocznej oba słowa często zamienia się miejscami. Ważne, by rozumieć, że wokół samych instrukcji można dobudować wiele warstw wygody.

„Wspólna Kasa”, przykład, który będzie nam towarzyszył, zacznie jako mały program: wczyta wydatki i wypisze, kto komu ile jest winien. Nie będzie miała okna ani przycisków. Dopiero dobudowana oprawa (pytania do użytkownika, sprawdzanie danych) przybliży ją do aplikacji.

Konsekwencja: zaczynamy od programu, bo to on jest rdzeniem. Oprawę dodaje się później, gdy rdzeń działa.

NOWA SEKCJA "Czym jest algorytm":
[[algorytm|Algorytm]] to skończony ciąg jednoznacznych kroków, który dla podanych danych prowadzi do wyniku. Nie jest jeszcze programem: to sam pomysł na rozwiązanie, który można zapisać zwykłymi słowami, na kartce albo w kodzie.

Dobry algorytm ma trzy cechy. Zaczyna od jasno określonych danych wejściowych, każdy krok jest na tyle dokładny, że nie wymaga domyślania się (tak jak „Resztę groszy dopisz pierwszej osobie” z listy kroków z wcześniejszej sekcji), i po skończonej liczbie kroków się kończy, dając wynik.

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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Algorytm jest podany tylko ogólnie. Dwie–trzy linie z liczbami by go uruchomiły, np. wydatki 100, 60, 40, 0 zł, suma 200, udział 50 zł, salda +50, +10, −10, −50. Wtedy czytelnik zobaczy, że kroki naprawdę dają wynik. Wystarczy zastąpić część zdania o „ręcznym wykonaniu”, więc limit słów zostaje.",
      "target": "blok text z krokami rozliczenia",
      "severity": "sugestia"
    }
  ]
}
````
