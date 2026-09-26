# Krok 0469 · weryfikator_faktów

Węzeł: `review` · dział: 5 · pytanie: 26 · próba: 2

## Prompt

````text
Jesteś weryfikatorem faktów tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Wersje obowiązujące w tutorialu: Python 3.13. Wersje zadeklarowane w sekcji: Python 3.13.

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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "`//` zostawia samą część całkowitą",
      "detail": "Dokumentacja (https://docs.python.org/3.13/reference/expressions.html) opisuje `//` jako dzielenie z zaokrągleniem w dół (floor), a nie odcięcie części ułamkowej. Dla liczb dodatnich wynik jest ten sam, ale `-7 // 2` daje `-4`, nie `-3`. Dla początkującego opis jest wystarczający, więc można go zostawić. Jeśli chcesz go uściślić, napisz „zaokrągla w dół do liczby całkowitej”."
    },
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "`/` zawsze daje liczbę z częścią ułamkową",
      "detail": "Dokumentacja (https://docs.python.org/3.13/reference/expressions.html) mówi, że dzielenie liczb całkowitych daje float. Nie musi to jednak być liczba z niezerową częścią ułamkową: `10 / 2` daje `5.0`. Dokładniejsze sformułowanie: „zawsze daje liczbę zapisaną z ułamkiem (np. `5.0`)”."
    }
  ],
  "sources": [
    {
      "title": "Python 3.13: Expressions (arytmetyka, priorytety operatorów)",
      "url": "https://docs.python.org/3.13/reference/expressions.html",
      "supports": "Potwierdza operatory + - * / // % **, wynik float z `/`, dzielenie z zaokrągleniem w dół dla `//`, resztę dla `%`, kolejność działań, sklejanie (`+`) i powtarzanie (`*`) tekstu oraz to, że pozostałe działania wymagają liczb (TypeError)."
    },
    {
      "title": "Python 3.13 Tutorial: Floating-Point Arithmetic",
      "url": "https://docs.python.org/3.13/tutorial/floatingpoint.html",
      "supports": "Potwierdza, że ułamki są trzymane jako przybliżenia binarne, co tłumaczy końcówkę `...336` w wyniku `100 / 3`."
    }
  ]
}
````
