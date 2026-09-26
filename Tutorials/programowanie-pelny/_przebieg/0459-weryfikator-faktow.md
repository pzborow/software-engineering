# Krok 0459 · weryfikator_faktów

Węzeł: `review` · dział: 5 · pytanie: 26 · próba: 1

## Prompt

````text
Jesteś weryfikatorem faktów tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Wersje obowiązujące w tutorialu: Python 3.13. Wersje zadeklarowane w sekcji: (brak).

Sprawdź w DOKUMENTACJI konkretne, sprawdzalne twierdzenia nowej sekcji: komendy i ich flagi, nazwy argumentów,
pól i zasobów, wartości domyślne, składnię oraz zachowanie zależne od wersji.
- Najpierw Context7: resolve-library-id, potem query-docs. Gdy czegoś nie ma w Context7, użyj WebFetch
  na oficjalnej stronie dokumentacji. Najwyżej 4 zapytania łącznie: wybierz twierdzenia najbardziej narażone na błąd.
- Nie oceniaj stylu, dydaktyki ani ogólnych idei. Kod jest szkicem: `...` i pominięte fragmenty nie są błędem.
- Każdą niezgodność z dokumentacją zgłoś jako kind="fakt", target=fragment sekcji, detail=co mówi dokumentacja
  (z adresem strony) i jak poprawić. "blokująca", gdy czytelnik wykonując kod dostałby błąd albo inne zachowanie;
  "sugestia", gdy to nieścisłość bez takich skutków.
- sources: tylko strony, które faktycznie przeczytałeś, i które twierdzenie sekcji potwierdzają albo obalają.
- ok=true, gdy nie ma blokujących niezgodności.

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
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Dzielenie `/` zawsze daje liczbę z częścią ułamkową.",
      "detail": "Dokumentacja: dzielenie liczb całkowitych daje float (np. 10 / 2 to 5.0). Wynik jest więc zawsze typu float, ale nie zawsze ma niezerową część ułamkową. Lepiej: „Dzielenie / zawsze daje liczbę zmiennoprzecinkową, np. 6 / 3 to 2.0”. Źródło: https://docs.python.org/3.13/reference/expressions.html",
      "source": "https://docs.python.org/3.13/reference/expressions.html"
    },
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "`//` zostawia samą część całkowitą",
      "detail": "Dokumentacja: `//` to dzielenie z zaokrągleniem w dół (floor), np. -10 // 3 daje -4, a nie -3. Dla liczb dodatnich w przykładzie opis jest poprawny. Jeśli kiedyś pojawią się liczby ujemne, mów „zaokrągla w dół”. Źródło: https://docs.python.org/3.13/reference/expressions.html",
      "source": "https://docs.python.org/3.13/reference/expressions.html"
    }
  ],
  "sources": [
    {
      "title": "Python 3.13 Language Reference: Expressions",
      "url": "https://docs.python.org/3.13/reference/expressions.html",
      "supports": "Wszystkie operatory z tabeli istnieją. `/` na liczbach całkowitych daje float. `//` zaokrągla w dół i daje int dla int. `%` daje resztę spójną z `//`. `**` z nieujemnym wykładnikiem daje int (100 ** 2 = 10000). Priorytet: `**`, potem `*` `/` `//` `%`, potem `+` `-`. Wyniki z bloku text (120, 80, 200, 33, 1, 10000) są zgodne, a 33.333333333333336 to standardowy wynik float dla 100 / 3."
    }
  ]
}
````
