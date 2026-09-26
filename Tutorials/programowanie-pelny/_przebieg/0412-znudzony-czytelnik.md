# Krok 0412 · znudzony_czytelnik

Węzeł: `review` · dział: 4 · pytanie: 24 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Co to jest wartość logiczna prawda/fałsz?".

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
## Czym jest typ danych
[[typ-danych|Typ danych]] to rodzaj wartości, który mówi Pythonowi, czym ta wartość jest i jakie działania są na niej dozwolone. Wcześniej pisaliśmy po prostu „rodzaj danych”, teraz mamy na to fachową nazwę.

Typ ma każda wartość, także ta ukryta w zmiennej. Python rozpoznaje go po zapisie: cudzysłów oznacza tekst, cyfry z kropką ułamek, a `True` lub `False` prawdę albo fałsz. Dlatego `"45.5"` to [[cztery znaki zamiast kwoty|tylko cztery znaki: 4, 5, kropka, 5]], a nie pieniądze. Typ sprawdzisz funkcją `type()`.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(type(imie))
print(type(kwota))
print(type(zaplacono))
```

```text
<class 'str'>
<class 'float'>
<class 'bool'>
```

Słowo `class` na razie pomiń, ważna jest nazwa po nim. Oto podstawowe typy Pythona:

| Nazwa w Pythonie | Co to jest | Przykład |
|---|---|---|
| `str` | tekst | `"Ania"` |
| `int` | liczba całkowita | `3` |
| `float` | liczba z ułamkiem | `45.5` |
| `bool` | prawda lub fałsz | `True` |

Typ decyduje o tym, co program może zrobić z wartością. Dlatego [[imienia nie da się podzielić|imienia nie podzielisz przez 2]], a kwotę tak. Typem `bool` zajmiemy się osobno, w kolejnej sekcji.

Konsekwencja: gdy program zachowuje się dziwnie, jedno z pierwszych pytań brzmi „jakiego typu jest ta wartość?”.

NOWA SEKCJA "Wartość logiczna prawda/fałsz":
[[wartosc-logiczna|Wartość logiczna]] to dana, która ma tylko dwie możliwe wartości: prawda albo fałsz. W Pythonie zapisujesz je jako `True` i `False`, a ich typ to `bool`.

Pasuje do każdej odpowiedzi „tak albo nie”: czy wydatek jest zapłacony, czy kwota jest większa od zera. Nie ma nic pomiędzy. W arkuszu to odpowiednik pola wyboru: zaznaczone albo nie.

Zapisuje się je z wielkiej litery i bez cudzysłowu. Ta sama zasada, co przy `"45.5"`: `True` to wartość logiczna, a `"True"` w cudzysłowie to tylko tekst z czterech liter.

```python
zaplacono = True
print(zaplacono)
zaplacono = False
print(zaplacono)
print(type(zaplacono))
```

```text
True
False
<class 'bool'>
```

Zmienną logiczną podmieniasz jak każdą inną: po drugim przypisaniu `True` znika, a jej miejsce zajmuje `False`.

Konsekwencja: taka wartość służy programowi do podejmowania decyzji. Na podstawie `zaplacono` program będzie mógł wybrać, czy przypomnieć o długu. Jak to zapisać, pokażemy przy instrukcji warunkowej.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "skrócenie",
      "detail": "Sekcja w dużej mierze powtarza poprzednią (bool, True/False, cudzysłów vs tekst, ten sam kod z type). Można skrócić akapit o cudzysłowie lub odwołać się do niego jednym zdaniem.",
      "severity": "sugestia",
      "target": "akapit o wielkiej literze i cudzysłowie"
    }
  ]
}
````
