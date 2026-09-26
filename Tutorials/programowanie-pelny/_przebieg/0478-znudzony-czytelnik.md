# Krok 0478 · znudzony_czytelnik

Węzeł: `review` · dział: 5 · pytanie: 27 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak program łączy ze sobą teksty?".

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
## Działania matematyczne w programie
Program wykonuje te same działania co kalkulator: dodawanie, odejmowanie, mnożenie i dzielenie, a do tego dzielenie całkowite, resztę z dzielenia i potęgowanie. Zapisujesz je za pomocą [[operator-arytmetyczny|operatorów arytmetycznych]], czyli znaków, które mówią Pythonowi, jakie działanie wykonać na liczbach.

| Działanie | Operator |
|---|---|
| dodawanie | `+` |
| odejmowanie | `-` |
| mnożenie | `*` |
| dzielenie | `/` |
| dzielenie całkowite | `//` |
| reszta z dzielenia | `%` |
| potęgowanie | `**` |

Mnożenie to gwiazdka, a nie „x”. Dzielenie `/` zawsze daje liczbę z częścią ułamkową, `//` zostawia samą część całkowitą, a `%` pokazuje, ile zostało. Kolejność działań jest jak w szkole: mnożenie i dzielenie przed dodawaniem, a nawiasy zmieniają porządek.

```python
kwota = 100
print(kwota / 3)
print(kwota // 3)
print(kwota % 3)
```

```text
33.333333333333336
33
1
```

Końcówka `...336` to drobna nieścisłość: komputer trzyma ułamki w przybliżeniu.

Odejmowanie, dzielenie, `//`, `%` i `**` mają sens tylko na liczbach. Skoro `nazwa_wyjazdu` jest tekstem, `nazwa_wyjazdu / 2` kończy się błędem `TypeError`. Wyjątkiem są `+` i `*`, które na tekście działają inaczej: sklejają i powtarzają.

```python
print("Ania" + "Bartek")
print("Ha" * 3)
```

```text
AniaBartek
HaHaHa
```

NOWA SEKCJA "Łączenie tekstów":
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

U siebie zobaczysz ten błąd za chwilę w `kasa.py`.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "skrócenie",
      "detail": "Zdanie „Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono” nic nie wnosi. Poprzednia sekcja nie zawiera takiej obietnicy, więc zdanie może zmylić czytelnika. Warto je usunąć.",
      "severity": "sugestia",
      "target": "zdanie o obietnicy z poprzedniej sekcji",
      "source": "nowa sekcja, pierwszy akapit"
    }
  ]
}
````
