# Krok 0564 · znudzony_czytelnik

Węzeł: `review` · dział: 5 · pytanie: 31 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Do czego służą operatory „i” oraz „lub”?".

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
## Część „w przeciwnym razie”
Część `else`, czyli „w przeciwnym razie”, wykonuje swoje linie wtedy, gdy warunek z `if` jest fałszywy. Dzięki niej program zawsze wybiera jedną z dwóch dróg, a nie tylko „robi coś albo nic”.

Zapisujemy ją pod blokiem `if`, na tym samym poziomie [[wciecie|wcięcia]] co samo `if`, z dwukropkiem po słowie `else`. Sama nie ma warunku: nie pyta o nic, bo obejmuje wszystko, czego `if` nie złapało. Jej własne linie też wcinamy o cztery spacje.

```python
kwota = 45.5
if kwota > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print("Koniec")
```

```text
Zwykła kwota
Koniec
```

Warunek `kwota > 100` jest fałszywy, więc Python pominął pierwszy wcięty blok i wykonał ten pod `else`. Gdyby kwota wynosiła 150, wypisałoby się tylko „Bardzo duża kwota”. Oba bloki nigdy nie wykonają się naraz. Ostatni `print` nie ma wcięcia, więc, jak w poprzedniej sekcji, działa zawsze.

Dla „Wspólnej Kasy” to ważne: program może teraz w każdym przypadku powiedzieć coś sensownego, osobno o dużej i zwykłej kwocie. Sprawdzanie kilku warunków naraz, czyli „i” oraz „lub”, pokażemy w następnej sekcji.

NOWA SEKCJA "Operatory „i” oraz „lub”":
[[operator-logiczny|Operatory logiczne]] `and` („i”) oraz `or` („lub”) łączą kilka warunków w jeden. Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: `True` albo `False`.

`and` daje `True` tylko wtedy, gdy prawdziwe są **oba** warunki. `or` daje `True`, gdy prawdziwy jest **którykolwiek** z nich, a `False` dopiero wtedy, gdy oba są fałszywe.

| Lewy warunek | Prawy warunek | `and` | `or` |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

Każdy z połączonych warunków zapisujemy w całości, tak jak w porównywaniu wartości. Wynik można wypisać albo wstawić do `if`:

```python
kwota = 45.5
liczba_osob = 3
print(kwota > 40 and liczba_osob > 5)
print(kwota > 100 or liczba_osob == 3)
if kwota > 100 or liczba_osob > 5:
    print("Duża kwota")
else:
    print("Zwykła kwota")
```

```text
False
True
Zwykła kwota
```

W pierwszej linii drugi warunek zawiódł, więc `and` dało `False`. W drugiej wystarczył prawdziwy drugi warunek, więc `or` dało `True`. W `if` oba są fałszywe, więc zadziałało `else`.

Dla „Wspólnej Kasy” to znaczy, że kwotę można uznać za dużą, gdy jest wysoka **lub** dzieli ją dużo osób. U siebie w `kasa.py` dopisz te linie w warsztacie poniżej.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Przykład w kodzie ma mało życiowy sens: progi 40 i 5 osób są losowe. Warto jednym zdaniem wskazać, co oznacza każdy warunek w kasie (np. „wysoka kwota lub dużo osób”), albo dać codzienne porównanie („i” = bilet ORAZ dokument).",
      "severity": "sugestia",
      "target": "przykład kodu",
      "source": "kwota > 40 and liczba_osob > 5"
    }
  ]
}
````
