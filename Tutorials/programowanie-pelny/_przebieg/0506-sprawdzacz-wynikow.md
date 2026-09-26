# Krok 0506 · sprawdzacz_wyników

Węzeł: `review` · dział: 5 · pytanie: 28 · próba: 1

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

SEKCJA "Porównywanie wartości":
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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
