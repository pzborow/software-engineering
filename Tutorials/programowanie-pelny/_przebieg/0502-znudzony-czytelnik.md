# Krok 0502 · znudzony_czytelnik

Węzeł: `review` · dział: 5 · pytanie: 28 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak program porównuje dwie wartości?".

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
## Łączenie tekstów
Program łączy teksty operatorem `+`, który skleja je w jeden, dokładnie w takiej kolejności i z takimi znakami, jakie mu podasz. Ta operacja nazywa się [[konkatenacja|sklejaniem tekstów]] (konkatenacją). Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono.

Python niczego nie dopowiada. Nie doda spacji ani przecinka, więc odstępy musisz wstawić sam, jako część tekstu w cudzysłowie:

```python
imie = "Ania"
kwota = 45.5
print(imie + " zapłaciła " + str(kwota) + " zł")
print(imie + "zapłaciła")
```

```text
Ania zapłaciła 45.5 zł
Aniazapłaciła
```

W drugiej linii zabrakło spacji, więc słowa się zlepiły.

Sklejać można tylko tekst z tekstem. Zapis `"Kwota: " + kwota` zatrzyma program błędem `TypeError`, bo liczby 45.5 nie da się dokleić do napisu. Zamienia ją na tekst funkcja `str()`: `str(kwota)` daje `"45.5"`. Nie zmienia to samej zmiennej `kwota`, która dalej jest liczbą.

Wygodniejszy bywa zapis z literą `f` przed cudzysłowem: `f"{imie} zapłaciła {kwota} zł"`. Nazwy w nawiasach klamrowych Python podmienia na wartości, także liczbowe.

Ten błąd możesz wywołać od razu: w warsztacie poniżej dopisujesz do swojego skryptu linię, która skleja tekst z liczbą.

NOWA SEKCJA "Porównywanie wartości":
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
  "needs": [
    {
      "kind": "przykład",
      "detail": "Tekst zapowiada, że wynik jest wartością, ale nie pokazuje, że można ją zapisać w zmiennej, np. `czy_drogo = kwota > 50`. Jedna linia kodu pomogłaby zrozumieć, że True/False to zwykła wartość, a nie tylko wydruk.",
      "severity": "sugestia",
      "target": "wartość logiczna",
      "source": "Sam wynik `True` lub `False` jeszcze nic nie robi."
    }
  ]
}
````
