# Krok 0997 · weryfikator_faktów

Węzeł: `review` · dział: 9 · pytanie: 51 · próba: 1

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

NOWA SEKCJA "Jak czytać komunikat o błędzie":
Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak, a linie nad nią pokazują, gdzie to się stało. Komunikat nie jest wyrokiem, tylko wskazówką.

Gdy program zatrzyma się w trakcie pracy, Python wypisuje [[traceback|Traceback]], czyli ślad wywołań: listę miejsc w kodzie, przez które przeszło wykonanie aż do błędu. Wszystko razem to [[komunikat-o-bledzie|komunikat o błędzie]], czyli tekst, w którym Python opisuje, co go zatrzymało i w którym miejscu. Dzielimy przez zero:

```python
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))
```

```text
Start
Traceback (most recent call last):
  File "/home/ania/wspolna_kasa/blad_pusta.py", line 6, in <module>
    print(na_osobe(0, 0))
          ~~~~~~~~^^^^^^
  File "/home/ania/wspolna_kasa/blad_pusta.py", line 2, in na_osobe
    return suma / osoby
           ~~~~~^~~~~~~
ZeroDivisionError: division by zero
```

(Numery linii i ścieżka u Ciebie będą inne, bo zależą od pliku.)

Ostatnia linia ma dwie części: nazwę błędu (`ZeroDivisionError`, dzielenie przez zero) i opis (`division by zero`). Wyżej stoją pary „plik, linia, funkcja” i przepisana linia kodu. Ostatnia para jest miejscem, w którym Python się potknął, a wyższe pokazują, kto tę funkcję wywołał. Znaki `^` i `~` wskazują fragment linii.

Inaczej niż przy błędzie składni ze „Startem”, który się nie pojawił, tu „Start” się wypisał, bo program ruszył i padł dopiero w środku.

Konsekwencja: nie bój się czerwonego tekstu. Przeczytaj ostatnią linię, znajdź w śladzie własny plik i numer linii, a zwykle już wiesz, gdzie szukać. Szukanie przyczyny krok po kroku omówimy przy debugowaniu.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Znaki `^` i `~` wskazują fragment linii",
      "detail": "Dokumentacja (https://docs.python.org/3.13/tutorial/errors.html) pokazuje ten sam mechanizm, np. `~^~` pod `(1/0)`. Twoje znaczniki `~~~~~~~~^^^^^^` i `~~~~~^~~~~~~` są zgodne z zasadą działania Pythona 3.13. Dokładne rozmieszczenie zależy od wyrażenia, więc warto dopisać, że 'u Ciebie znaki mogą wyglądać nieco inaczej'. To nie błąd.",
      "source": "https://docs.python.org/3.13/tutorial/errors.html"
    },
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "opis `division by zero`",
      "detail": "Dokumentacja pokazuje `ZeroDivisionError: division by zero` dla dzielenia `/` (tutorial errors). Strona wyjątków nie podaje dokładnego tekstu, ale przykład w tutorialu go potwierdza. Sekcja jest zgodna.",
      "source": "https://docs.python.org/3.13/tutorial/errors.html"
    }
  ],
  "sources": [
    {
      "title": "Errors and Exceptions — Python 3.13",
      "url": "https://docs.python.org/3.13/tutorial/errors.html",
      "supports": "Format tracebacku (nagłówek, File/line/in, przepisana linia, znaczniki ~ i ^), ostatnia linia z nazwą i opisem, `ZeroDivisionError: division by zero`."
    },
    {
      "title": "Built-in Exceptions — Python 3.13",
      "url": "https://docs.python.org/3.13/library/exceptions.html",
      "supports": "ZeroDivisionError występuje przy dzieleniu przez zero; dokładny tekst komunikatu nie jest tam podany."
    }
  ]
}
````
