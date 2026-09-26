# Krok 1021 · weryfikator_faktów

Węzeł: `review` · dział: 9 · pytanie: 52 · próba: 1

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

NOWA SEKCJA "Czym jest testowanie programu":
[[testowanie|Testowanie]] to systematyczne sprawdzanie programu na wielu danych, dla których z góry znasz poprawny wynik. Zamiast raz spojrzeć na ekran i uznać, że „wygląda dobrze”, zapisujesz oczekiwania i pozwalasz komputerowi je porównać.

Najprostszy test to jedno sprawdzenie małej funkcji. W Pythonie służy do tego [[assert|assert]]: instrukcja, która nic nie robi, gdy warunek jest prawdziwy, a zatrzymuje program błędem `AssertionError`, gdy jest fałszywy.

```python
def na_osobe(suma, osoby):
    return suma / osoby

assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0
assert na_osobe(100, 4) == 25
print("Wszystkie testy przeszły")
```

```text
Wszystkie testy przeszły
```

Cisza po `assert` znaczy „zgadza się”. Gdyby ktoś zmienił dzielenie tak, że wynik byłby zły, jak przy błędzie z niewłaściwym dzielnikiem, pierwszy test zatrzymałby program i wskazał linię, w której oczekiwanie przestało być prawdą.

Dobre testy obejmują zwykłe dane i przypadki brzegowe, np. pustą listę wydatków. Kosztują chwilę, a po każdej zmianie kodu uruchamiasz je jednym poleceniem i wiesz, czy niczego nie zepsułeś.

Test nie dowodzi, że błędów nie ma, tylko że w sprawdzonych przypadkach ich nie ma. Gdy test się wywali, szukanie przyczyny omówimy przy debugowaniu.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": []
}
````
