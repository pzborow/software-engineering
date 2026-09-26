# Krok 0714 · weryfikator_faktów

Węzeł: `review` · dział: 7 · pytanie: 38 · próba: 1

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

NOWA SEKCJA "Czym jest funkcja":
[[funkcja|Funkcja]] to nazwany kawałek kodu, który raz opisujesz, a potem uruchamiasz, kiedy tylko zechcesz, wpisując jego nazwę. Znasz już takie gotowe kawałki: `print()` i `str()` to funkcje napisane przez twórców Pythona.

Własną funkcję zaczynasz od `def`, nazwy i nawiasów z dwukropkiem. Wcięty blok pod spodem to jej treść. Ten zapis nazywamy [[definicja-funkcji|definicją funkcji]]: tylko opisuje, co funkcja robi, i niczego jeszcze nie wykonuje. Dopiero [[wywolanie-funkcji|wywołanie]], czyli nazwa z nawiasami, uruchamia treść.

Weźmy pętlę, która zbiera sumę wydatków, jak w poprzedniej sekcji. Zamieniamy ją w osobną funkcję:

```python
def suma_wydatkow(wydatki):
    suma = 0
    for wydatek in wydatki:
        suma = suma + wydatek["kwota"]
    return suma

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.50},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 200}]
print(suma_wydatkow(wydatki))
```

```text
320.5
```

Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. Oba mechanizmy omówimy osobno w kolejnych sekcjach; na razie wystarczy, że dane wchodzą, a wynik wychodzi.

Konsekwencja: kod, który wcześniej był kawałkiem długiego skryptu, ma teraz nazwę i można go wywołać w wielu miejscach, bez kopiowania.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "`print()` i `str()` to funkcje napisane przez twórców Pythona",
      "detail": "Dokumentacja Pythona 3.13 (https://docs.python.org/3.13/library/functions.html) opisuje `print` jako funkcję wbudowaną, ale `str` jako klasę (`class str(object='')`). Dla początkującego różnica jest nieistotna, a `str()` wywołuje się tak samo jak funkcję. Można zostawić albo zamienić przykład na `print()` i `len()` (`len` to funkcja wbudowana), albo napisać „gotowe kawałki, np. `print()` i `len()`”.",
      "source": "https://docs.python.org/3.13/library/functions.html"
    }
  ],
  "sources": [
    {
      "title": "Built-in Functions — Python 3.13 documentation",
      "url": "https://docs.python.org/3.13/library/functions.html",
      "supports": "`print` jest funkcją wbudowaną, a `str` klasą wbudowaną, więc określenie „str() to funkcja” jest nieścisłe, ale nie powoduje błędu w kodzie."
    }
  ]
}
````
