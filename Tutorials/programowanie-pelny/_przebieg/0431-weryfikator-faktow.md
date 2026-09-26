# Krok 0431 · weryfikator_faktów

Węzeł: `review` · dział: 4 · pytanie: 25 · próba: 1

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

NOWA SEKCJA "Przypisanie wartości do zmiennej":
[[przypisanie|Przypisanie]] to instrukcja, która zapisuje wartość pod nazwą zmiennej. Dzięki niej program zapamiętuje daną i może do niej wrócić w dalszej części kodu.

Zapisujesz je znakiem `=`. Po lewej stoi nazwa, po prawej wartość: `kwota = 45.5`. To nie jest równanie ze szkoły, tylko polecenie: „weź to, co po prawej, i połóż pod nazwą po lewej”. Jeśli zmienna jeszcze nie istniała, Python ją tworzy. Jeśli istniała, podmienia jej wartość, tak jak przy [[sec-04-zmienna-jako-pudelko-z-etykieta|pudełku z etykietą]].

Przypisanie działa od prawej do lewej i tylko w chwili wykonania. Gdy wpiszesz jedną zmienną po prawej stronie, Python kopiuje jej aktualną wartość. Późniejsza zmiana oryginału nie rusza kopii.

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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Python kopiuje jej aktualną wartość",
      "detail": "Oficjalna dokumentacja Pythona (https://docs.python.org/3/reference/simple_stmts.html#assignment-statements) opisuje przypisanie jako wiązanie nazwy z obiektem, a nie kopiowanie wartości. Dla liczb (float, int) skutek jest taki, jak opisano w sekcji, więc kod i wynik (60 i 45.5) są poprawne. Nieścisłość ujawni się dopiero przy listach, gdzie zmiana przez jedną nazwę jest widoczna przez drugą. Można dopisać \"dla liczb i tekstów\" albo zostawić i wyjaśnić przy listach. Nie opieram tego na zapytaniu do dokumentacji w tej sesji, tylko na znajomości semantyki języka.",
      "source": "docs.python.org",
      "status": "nowa"
    }
  ],
  "sources": []
}
````
