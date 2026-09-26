# Krok 0389 · weryfikator_faktów

Węzeł: `review` · dział: 4 · pytanie: 22 · próba: 2

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

NOWA SEKCJA "Liczba a tekst":
Liczba to wartość, na której program liczy. Tekst to ciąg znaków, który program przechowuje, wypisuje, porównuje i skleja. Zapis decyduje o tym, z czym mamy do czynienia: `45.5` bez cudzysłowu to liczba, a `"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5.

| Zapis | Co to jest | Można dzielić? |
|---|---|---|
| `45.5` | liczba | tak |
| `"45.5"` | tekst | nie |
| `"Ania"` | tekst | nie |

W programie ułamek dziesiętny zapisujemy z kropką, nie z przecinkiem, tak jak `kwota = 45.5` w „Wspólnej Kasie”.

```python
kwota = 45.5
imie = "Ania"
print(kwota / 2)
print(imie)
```

```text
22.75
Ania
```

Liczbę można podzielić, tekstu nie. To ta sama myśl co [[imienia nie da się podzielić|imię „Ania” nie do podzielenia przez 2]]. Python zatrzyma się z komunikatem `TypeError`. U siebie zobaczysz to za chwilę we własnym pliku z kodem.

Uwaga na plus: przy liczbach dodaje, a przy tekstach skleja je w jeden. Tym zajmiemy się osobno.

Konsekwencja: kwotę zapisaną w cudzysłowie program potraktuje jak napis, nie jak pieniądze. Nazwę tej cechy danych, czyli typ, omówimy w następnej sekcji.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [],
  "sources": [
    {
      "title": "CPython 3.13 tokenizer tests: float literals",
      "url": "https://github.com/python/cpython/blob/v3.13.9/Lib/test/tokenizedata/tokenize_tests.txt",
      "supports": "Ułamek dziesiętny zapisuje się z kropką (np. `x = 3.14`), więc `kwota = 45.5` jest poprawnym literałem float."
    }
  ]
}
````
