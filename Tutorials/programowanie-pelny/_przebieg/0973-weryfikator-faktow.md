# Krok 0973 · weryfikator_faktów

Węzeł: `review` · dział: 9 · pytanie: 50 · próba: 1

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

[[blad-skladni|Błąd składni]] to naruszenie [[skladnia|składni]] języka, czyli reguł zapisu: brakujący dwukropek po `if`, niedomknięty cudzysłów, źle wcięta linia. Python czyta cały plik przed startem i takiego zapisu nie rozumie, więc nie wykona nawet linii przed błędem. Komunikat wskazuje linię i miejsce.

[[blad-logiczny|Błąd logiczny]] to pomyłka w pomyśle: zły wzór, zły dzielnik, zły warunek. Python nie ma jak jej zauważyć, bo każda instrukcja jest poprawna. Widzisz go tylko wtedy, gdy porównasz wynik z tym, czego się spodziewałeś.

| | Błąd składni | Błąd logiczny |
|---|---|---|
| Kiedy wychodzi | przed startem programu | w trakcie i po nim |
| Komunikat | jest, ze wskazaną linią | brak |
| Kto go znajduje | Python | Ty |

Trzy osoby dzielą wydatki 45.5, 20 i 12.5 zł:

```python
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)
```

```text
Na osobę: 39.0
```

Program nie zgłasza żadnego problemu, a wynik jest zły: powinno być 26.0, bo osoby są trzy. Podobnie działał zły wpis `-5` z poprzedniej sekcji: brak komunikatu, zły wynik. Konsekwencja: błędy składni są uciążliwe, ale łatwe, bo Python je wskaże. Za błędy logiczne odpowiadasz Ty, dlatego wynik zawsze sprawdzaj z rachunkiem na kartce. Jak czytać komunikaty i szukać takich błędów, omówimy osobno, w dalszych sekcjach tego działu.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": []
}
````
