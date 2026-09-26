# Krok 0458 · sprawdzacz_wyników

Węzeł: `review` · dział: 5 · pytanie: 26 · próba: 1

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

SEKCJA "Działania matematyczne w programie":
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
      "detail": "Kolejność działań (mnożenie przed dodawaniem, nawiasy) jest opisana tylko słowami. Krótki przykład, np. print(2 + 3 * 4) daje 14, a print((2 + 3) * 4) daje 20, pomógłby czytelnikowi.",
      "severity": "sugestia",
      "target": "Kolejność działań"
    },
    {
      "kind": "przykład",
      "detail": "Zdanie, że tekstu typu \"Ania\" nie da się podzielić, nie ma przykładu. Można dodać print(\"Ania\" / 2) i pokazać, że kończy się błędem. Przy okazji warto zaznaczyć, że to odwołanie do wcześniejszej sekcji o typach danych.",
      "severity": "sugestia",
      "target": "Konsekwencja: działania tylko na liczbach"
    }
  ]
}
````
