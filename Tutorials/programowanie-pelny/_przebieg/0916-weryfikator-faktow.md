# Krok 0916 · weryfikator_faktów

Węzeł: `review` · dział: 8 · pytanie: 47 · próba: 1

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

NOWA SEKCJA "Czym jest plik":
[[plik|Plik]] to nazwana porcja danych zapisana na dysku, która istnieje także wtedy, gdy program już nie działa. Program może plik odczytać albo zapisać, więc plik jest miejscem, z którego [[dane-wejsciowe|dane wejściowe]] przychodzą i do którego trafiają [[dane-wyjsciowe|dane wyjściowe]]. To odpowiedź na problem zmiennych: te znikają razem z zakończeniem programu, a plik zostaje.

Program korzysta z pliku w trzech krokach: otwiera go funkcją `open`, czyta albo zapisuje, a na końcu zamyka. Blok `with` zamyka plik za Ciebie, nawet gdy coś pójdzie źle. Drugi argument `open` to [[tryb-otwarcia-pliku|tryb otwarcia]], czyli informacja, co zamierzasz z plikiem zrobić:

| Tryb | Znaczenie |
|---|---|
| `"r"` | czytanie (plik musi istnieć) |
| `"w"` | zapis od nowa, stara treść przepada |
| `"a"` | dopisywanie na końcu |

Argument `encoding="utf-8"` sprawia, że polskie litery zapiszą się i odczytają poprawnie.

```python
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")
```

```text
Ania;120.5
Bartek;45.5
```

Uwaga: plik przechowuje wyłącznie tekst, więc kwotę po wczytaniu trzeba znów zamienić przez `float()`, tak jak przy odpowiedzi z `input`. Pułapką jest tryb `"w"`, który kasuje starą zawartość. Zanim ktoś wpisze do pliku coś błędnego, warto dane sprawdzić, o czym powiemy przy sprawdzaniu danych użytkownika.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Uwaga: plik przechowuje wyłącznie tekst, więc kwotę po wczytaniu trzeba znów zamienić przez `float()`",
      "detail": "Dokumentacja open() (https://docs.python.org/3.13/library/functions.html#open) opisuje też tryb binarny ('b'), więc plik nie przechowuje wyłącznie tekstu. Tekstowy tryb (domyślny) zwraca str, więc wniosek o float() jest poprawny. Wystarczy zawęzić: „plik otwarty w trybie tekstowym daje tekst”.",
      "source": "https://docs.python.org/3.13/library/functions.html#open"
    },
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Tabela trybów: \"w\" i \"a\"",
      "detail": "Dokumentacja podaje, że \"w\" obcina plik, a \"a\" dopisuje na końcu. Oba tryby tworzą plik, gdy go nie ma, a tabela tego nie mówi. Nie blokuje to kodu, w którym \"w\" tworzy wydatki.txt. Można dodać „plik zostanie utworzony, jeśli go nie ma”.",
      "source": "https://docs.python.org/3.13/library/functions.html#open"
    }
  ],
  "sources": [
    {
      "title": "Built-in Functions: open() (Python 3.13)",
      "url": "https://docs.python.org/3.13/library/functions.html#open",
      "supports": "Tryby 'r' (plik musi istnieć, inaczej FileNotFoundError), 'w' (obcina plik), 'a' (dopisuje na końcu), parametr encoding oraz platformowo zależne kodowanie domyślne. Kod przykładu jest poprawny."
    }
  ]
}
````
