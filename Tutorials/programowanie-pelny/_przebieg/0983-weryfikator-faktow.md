# Krok 0983 · weryfikator_faktów

Węzeł: `review` · dział: 9 · pytanie: 50 · próba: 2

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

NOWA SEKCJA "Błąd składni a błąd logiczny":
Błąd składni łamie zasady zapisu, więc Python zatrzymuje się, zanim cokolwiek wykona. Błąd logiczny ma zapis poprawny, ale robi coś innego, niż zamierzałeś, więc program działa i po cichu podaje zły wynik.

[[blad-skladni|Błąd składni]] to naruszenie [[skladnia|składni]], czyli reguł zapisu: brakujący dwukropek, niedomknięty cudzysłów, źle wcięta linia. Python czyta cały plik przed startem, więc nie wykona nawet linii sprzed błędu:

```python
print("start")
suma = 45.5 + 20
if suma > 10
    print("dużo")
```

```text
  File "blad.py", line 3
    if suma > 10
                ^
SyntaxError: expected ':'
```

Słowo „start” się nie pojawiło, a komunikat wskazuje linię i miejsce.

[[blad-logiczny|Błąd logiczny]] to pomyłka w pomyśle: zły wzór, dzielnik albo warunek. Python jej nie zauważy, bo każda instrukcja jest poprawna. Trzy osoby dzielą wydatki 45.5, 20 i 12.5 zł:

```python
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)
```

```text
Na osobę: 39.0
```

Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.

Konsekwencja: błędy składni są uciążliwe, ale łatwe, bo wskaże je Python. Za błędy logiczne odpowiadasz Ty, więc wynik porównuj z rachunkiem na kartce. Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "Komunikat SyntaxError: expected ':' i pozycja karetki",
      "detail": "Dokumentacja (https://docs.python.org/3.13/tutorial/errors.html) pokazuje format: plik i linia, powtórzona linia kodu, strzałki, typ i komunikat; sama nie podaje dokładnego tekstu 'expected ':''. Ten komunikat dla brakującego dwukropka po if jest w Pythonie 3.10+ zgodny z 3.13, ale karetka bywa dokładnie pod miejscem błędu (tu za '10'), a plik w prawdziwym uruchomieniu pokaże pełną ścieżkę. Szkic jest akceptowalny; można dodać zastrzeżenie, że wygląd komunikatu może się nieco różnić."
    }
  ],
  "sources": [
    {
      "title": "Errors and Exceptions — Python 3.13",
      "url": "https://docs.python.org/3.13/tutorial/errors.html",
      "supports": "Format komunikatu SyntaxError (plik, linia, karetka, typ i komunikat) oraz to, że błędy składni wykrywane są przy parsowaniu, przed wykonaniem; potwierdza też, że błąd bywa wskazany za miejscem do poprawy."
    }
  ]
}
````
