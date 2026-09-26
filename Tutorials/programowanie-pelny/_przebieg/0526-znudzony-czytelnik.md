# Krok 0526 · znudzony_czytelnik

Węzeł: `review` · dział: 5 · pytanie: 29 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym jest instrukcja warunkowa „jeśli… to…”?".

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
## Porównywanie wartości
Program porównuje wartości [[operator-porownania|operatorami porównania]]. To znaki takie jak `==` czy `>`, które zestawiają dwie wartości i zwracają wynik `True` albo `False`, czyli [[wartosc-logiczna|wartość logiczną]].

| Zapis | Znaczenie |
|---|---|
| `a == b` | równe |
| `a != b` | różne |
| `a < b`, `a > b` | mniejsze, większe |
| `a <= b`, `a >= b` | mniejsze lub równe, większe lub równe |

Uwaga na `==`: pojedynczy znak `=` to [[przypisanie]], czyli zapisanie wartości w zmiennej. Dopiero podwójny pyta „czy są równe?” i niczego nie zmienia.

```python
kwota = 45.5
print(kwota == 45.5)
print(kwota != 45.5)
print(kwota > 50)
print(kwota <= 45.5)
print("Ania" == "ania")
print("45.5" == 45.5)
```

```text
True
False
False
True
False
False
```

Dwa ostatnie wyniki pokazują, że porównanie jest ścisłe. Wielka i mała litera to różne znaki, więc `"Ania"` i `"ania"` się różnią. Tekst `"45.5"` i liczba 45.5 to różne typy, więc też nie są równe, choć wyglądają podobnie.

Sam wynik `True` lub `False` jeszcze nic nie robi. Dopiero instrukcja warunkowa, o której będzie następna sekcja, pozwoli programowi wybrać na jego podstawie, co zrobić dalej.

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
      "kind": "konkret",
      "detail": "Sekcja mówi, że warunek to „zwykle porównanie”, ale nie wspomina, że po `if` można użyć dowolnej wartości logicznej ani co się stanie przy pominięciu dwukropka lub wcięcia. Można dodać jedno zdanie o typowym błędzie (brak dwukropka/wcięcia daje komunikat błędu), żeby początkujący nie wpadł w panikę.",
      "severity": "sugestia",
      "target": "wcięcie i dwukropek"
    }
  ]
}
````
