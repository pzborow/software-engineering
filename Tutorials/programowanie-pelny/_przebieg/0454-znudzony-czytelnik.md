# Krok 0454 · znudzony_czytelnik

Węzeł: `review` · dział: 5 · pytanie: 26 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jakie podstawowe działania matematyczne może wykonać program?".

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
## Przypisanie wartości do zmiennej
[[przypisanie|Przypisanie]] to instrukcja, która zapisuje wartość pod nazwą zmiennej. Dzięki niej program zapamiętuje daną i może do niej wrócić w dalszej części kodu.

Zapisujesz je znakiem `=`. Po lewej stoi nazwa, po prawej wartość: `kwota = 45.5`. To nie jest równanie ze szkoły, tylko polecenie: „weź to, co po prawej, i połóż pod nazwą po lewej”. Jeśli zmienna jeszcze nie istniała, Python ją tworzy. Jeśli istniała, podmienia jej wartość, tak jak przy pudełku z etykietą.

Przypisanie działa od prawej do lewej i tylko w chwili wykonania. Gdy po prawej stronie stoi inna zmienna, Python kopiuje jej aktualną wartość. Późniejsza zmiana oryginału nie rusza kopii.

```python
kwota = 45.5
kwota_stara = kwota
kwota = 60
print(kwota)
print(kwota_stara)
```

```text
60
45.5
```

Linia `kwota_stara = kwota` skopiowała 45.5 w chwili wykonania. Dopiero potem `kwota = 60` zmieniła tylko `kwota`.

Konsekwencja: kolejność linii ma znaczenie. Program czyta kod od góry, więc wartość zmiennej zależy od tego, które przypisanie wykonało się ostatnie.

NOWA SEKCJA "Działania matematyczne w programie":
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

Mnożenie to gwiazdka, a nie „x”. Dzielenie `/` zawsze daje liczbę z częścią ułamkową. Dzielenie całkowite `//` zostawia samą część całkowitą, a `%` pokazuje, ile zostało. Przy dzieleniu kwoty między osoby to bardzo przydatne.

```python
kwota = 100
print(kwota + 20)
print(kwota - 20)
print(kwota * 2)
print(kwota / 3)
print(kwota // 3)
print(kwota % 3)
print(kwota ** 2)
```

```text
120
80
200
33.333333333333336
33
1
10000
```

Zwróć uwagę na wynik `33.333333333333336`. Komputer trzyma ułamki w przybliżeniu, więc na końcu bywa drobna nieścisłość. Kolejność działań jest jak w szkole: mnożenie i dzielenie przed dodawaniem, a nawiasy zmieniają porządek.

Konsekwencja: działania mają sens tylko na liczbach. Tekstu w rodzaju `"Ania"` nie podzielisz, co widzieliśmy przy typach danych.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Zdanie o dzieleniu kwoty między osoby jest ogólne, a wyniki 33 i 1 nie są z nim połączone. Wystarczy jedno zdanie: 100 zł na 3 osoby to po 33 zł (`//`) i 1 zł zostaje (`%`).",
      "severity": "sugestia",
      "target": "`//` i `%` – „bardzo przydatne”",
      "source": "",
      "status": "nowa"
    },
    {
      "kind": "przykład",
      "detail": "Kolejność działań jest tylko stwierdzona. Krótki przykład, np. `2 + 3 * 4` daje 14, a `(2 + 3) * 4` daje 20, pokazałby to od razu. Wystarczy jedna linia w bloku kodu.",
      "severity": "sugestia",
      "target": "kolejność działań i nawiasy",
      "source": "",
      "status": "nowa"
    }
  ]
}
````
