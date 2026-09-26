# Krok 0798 · łowca_pułapek

Węzeł: `gotchas` · dział: 7 · pytanie: 41 · próba: —

## Prompt

````text
Jesteś doświadczonym recenzentem kodu. Czytelnik: osoba spoza IT, poziom: początkujący.
Tutorial: Programowanie od podstaw. Dział 07: "Funkcje i porządek w kodzie".

Wypisz pułapki (gotchas) dotyczące DOKŁADNIE kodu z poniższej sekcji i TEMATU tutorialu: Programowanie od podstaw.

Pułapka to zaskakujące zachowanie albo konsekwencja samego zagadnienia z tematu (wzorca, mechanizmu,
reguły architektonicznej) w pokazanym kodzie: coś, co doświadczony programista przeoczy NAWET wtedy,
gdy zastosował zagadnienie zgodnie z opisem, i co prowadzi do błędu w produkcji albo w testach.
Zadaj sobie pytanie: czy ta pułapka zniknęłaby, gdyby usunąć z kodu omawiane zagadnienie? Jeśli nie,
to nie jest pułapka tego tematu.

NIE zgłaszaj (nawet jeśli to prawda):
- problemów niezwiązanych z tematem: zaokrąglanie kwot i walut, specyfika bazy danych, sterownika, ORM,
  frameworka webowego, typowania, formatowania tekstu, wydajności pojedynczego wywołania,
- braków uproszczonego szkicu: obsługa błędów, walidacja, logowanie, cache, zamykanie zasobów, `...` zamiast ciała,
- ogólnych rad ("pamiętaj o testach", "nazwij sensownie"),
- tego samego zjawiska co pułapka już wypisana, nawet pod inną nazwą.

Zasady:
- Nie na siłę. Pusta lista to oczekiwany wynik dla większości sekcji. Drugą pułapkę dodaj tylko wtedy,
  gdy jest równie ważna jak pierwsza.
- Każdej nadaj scope względem TEMATU tutorialu (Programowanie od podstaw), a nie względem języka:
  "temat", jeśli pułapka ilustruje zagadnienie, którego dotyczy tutorial; "poboczna", jeśli wynika z narzędzia
  użytego do pokazania przykładu (język python, biblioteka, framework, baza), a nie z tematu.
  Gdy tematem jest sam język albo biblioteka, jej zachowania są tematem, nie pułapką poboczną.
  Test pomocniczy, gdy narzędzie NIE jest tematem: czy pułapka wystąpiłaby, gdyby to samo zagadnienie zaimplementować
  innym narzędziem? Jeśli nie, bo wynika z mechanizmu tego narzędzia (np. protokołu tworzenia obiektów, cache biblioteki,
  sposobu importu), to jest "poboczna", nawet jeśli dotyczy kodu realizującego zagadnienie.
- Opisuj tylko kod, który jest w sekcji, a nie jego hipotetyczne rozszerzenia ("gdy ktoś doda..."); używaj nazw
  z tego kodu. Nazwy z kodu (klasy, metody, flagi) pisz w backtickach, np. `__init__`.
- Najwyżej 2. Każda musi wskazywać konkretny fragment tego kodu (trigger)
  i zagadnienie z tematu, którego dotyczy (concept). Jeśli nie umiesz go nazwać, nie zgłaszaj pułapki.
- Nie powtarzaj pułapek już wypisanych w tutorialu:
- Brak komunikatu nie oznacza poprawnego wyniku
- Zmiana wartości zmienia też typ
- Parametr przesłania funkcję o tej samej nazwie

SEKCJA "Zwracanie wyniku przez funkcję":
Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał. Ta oddana wartość to [[wartosc-zwracana|wartość zwracana]]: wywołanie funkcji staje się w kodzie właśnie nią, więc możesz ją zapisać do zmiennej albo przekazać dalej.

Po `return` funkcja od razu kończy pracę. Nic, co stoi pod nim w ciele funkcji, już się nie wykona.

Zwracanie to nie to samo co wypisywanie. `print` tylko pokazuje tekst na ekranie, a program nie dostaje z niego nic do dalszej pracy. Funkcja bez `return` oddaje specjalną wartość [[none|`None`]], czyli „nic”.

```python
def na_osobe(suma, osoby):
    return suma / osoby

def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wynik = na_osobe(300, 4)
nic = wypisz_na_osobe(300, 4)
print(wynik)
print(nic)
```

```text
75.0
75.0
None
```

Pierwsza `75.0` pochodzi z `print` wewnątrz `wypisz_na_osobe`, w chwili wywołania. Druga to `wynik`, czyli wartość zwrócona i zapisana. Zmienna `nic` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła. Nazwy `wynik` i `nic` służą tylko tej ilustracji.

Konsekwencja jest praktyczna: tylko zwrócony wynik da się wykorzystać dalej. Dlatego `na_osobe(suma(mazury), 3)` działa: wynik jednej funkcji trafia jako argument do drugiej.
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
