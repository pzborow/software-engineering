# Krok 0189 · znudzony_czytelnik

Węzeł: `review` · dział: 3 · pytanie: 13 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym jest kod źródłowy?".

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
## Poprawny algorytm
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

NOWA SEKCJA "Czym jest kod źródłowy":
[[kod-zrodlowy|Kod źródłowy]] to tekst programu zapisany w [[jezyk-programowania|języku programowania]], który czyta i pisze człowiek. To „źródło”, z którego komputer dopiero dostaje coś do wykonania.

Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to [[instrukcja|instrukcja]] zapisana według ścisłych reguł [[skladnia|składni]]. Ten sam [[algorytm|algorytm]], który wcześniej opisywaliśmy słowami i schematem, tu dostaje zapis, którego nie da się zrozumieć na dwa sposoby.

Kod źródłowy zapisujemy w pliku o rozszerzeniu zależnym od języka. Pliki Pythona kończą się na `.py`. Taki plik będzie miał nasz przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Zaczyna się od pliku `rozlicz.py`:

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

```text
Wspólna Kasa
100.0
```

Plik sam niczego nie robi. Dopiero osobny program czyta go i wykonuje linia po linii, a jak to działa, pokażemy przy uruchamianiu programu.

Konsekwencja: kod źródłowy możesz otworzyć, przeczytać i poprawić w każdym edytorze tekstu. Dlatego to on jest tym, co programista naprawdę tworzy i zmienia.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "Kod używa print i dzielenia `/`, ale nie mówi, że print wyświetla tekst na ekranie. Warto dodać jedno zdanie pod wynikiem. Można też wyjaśnić, dlaczego wychodzi `100.0`, a nie `100`. Poprzednia sekcja użyła `//`, więc czytelnik może się zdziwić.",
      "severity": "sugestia",
      "target": "blok kodu rozlicz.py",
      "source": "nowa sekcja"
    },
    {
      "kind": "skrócenie",
      "detail": "Zdanie „Taki plik będzie miał nasz przykład, który będzie nam towarzyszył” jest niezgrabne i powtarza „będzie”. Lepiej: „Tak nazwiemy plik naszego przykładu „Wspólna Kasa”.”",
      "severity": "sugestia",
      "target": "akapit o rozszerzeniu .py",
      "source": "nowa sekcja"
    }
  ]
}
````
