# Krok 0077 · znudzony_czytelnik

Węzeł: `review` · dział: 1 · pytanie: 6 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym różni się program od aplikacji?".

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
## Po co komputerowi precyzja
Komputer potrzebuje precyzyjnych [[instrukcja|instrukcji]], bo nie rozumie intencji, tylko wykonuje dokładnie to, co zapisano. Człowiek dopowiada sobie brakujące szczegóły, komputer ich nie zna i niczego nie zgaduje.

Wróćmy do czworga znajomych na wyjeździe. Polecenie „podziel rachunek po równo” dla nich jest jasne. Dla komputera brakuje w nim niemal wszystkiego:

| Człowiek rozumie | Komputer musi dostać |
|---|---|
| „rachunek” | które wydatki dodać i skąd je wziąć |
| „po równo” | przez ile osób dzielimy |
| „podziel” | co zrobić, gdy kwota nie dzieli się na równe części |
| (nic) | gdzie i w jakiej formie pokazać wynik |

Prosta lista kroków może wyglądać tak, ale jeszcze nie jest precyzyjna:

```text
1. Dodaj wszystkie wydatki.
2. Podziel sumę przez liczbę osób.
3. Wypisz wynik z dokładnością do grosza.
```

Nie wiadomo tu, skąd wziąć wydatki, ile jest osób ani kto dopłaci grosz, gdy kwota nie dzieli się równo. Precyzyjna wersja rozstrzyga to wprost:

```text
1. Weź kwoty wydatków z listy wpisanej przez użytkownika.
2. Dodaj je do siebie.
3. Podziel sumę przez 4, bo tyle jest osób.
4. Zaokrąglij w dół do pełnych groszy.
5. Resztę groszy dopisz pierwszej osobie.
6. Wypisz wynik na ekranie.
```

Komputer wykona takie kroki tysiące razy bez zmęczenia, ale też bez zdrowego rozsądku. Jeśli podasz złą liczbę osób, pomyli się z pełną pewnością siebie.

Konsekwencja jest praktyczna: precyzja to zadanie programisty. To on ustala, co dokładnie ma się stać, i dlatego w pracy nad programem tyle miejsca zajmuje sprawdzanie i poprawianie.

NOWA SEKCJA "Program a aplikacja":
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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "język",
      "detail": "Słowa „skrypt” i „terminal” pojawiają się bez wyjaśnienia. Osoba spoza IT może nie wiedzieć, czym jest „sam tekst w terminalu”. Wystarczy zastąpić je opisem, np. „krótki program bez okna, który wypisuje wynik jako zwykły tekst”.",
      "severity": "sugestia",
      "target": "skrypt, terminal"
    },
    {
      "kind": "skrócenie",
      "detail": "Akapit o płynnej granicy i ostatnie zdanie „Konsekwencja” powtarzają to, co już wynika z tabeli i przykładu Wspólnej Kasy. Sekcja jest na granicy limitu 250 słów. Można je skrócić do jednego zdania.",
      "severity": "sugestia",
      "target": "akapit „W praktyce granica jest płynna” i końcowa „Konsekwencja”"
    }
  ]
}
````
