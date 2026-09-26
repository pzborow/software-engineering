# Krok 0697 · łowca_pułapek

Węzeł: `gotchas` · dział: 6 · pytanie: 37 · próba: —

## Prompt

````text
Jesteś doświadczonym recenzentem kodu. Czytelnik: osoba spoza IT, poziom: początkujący.
Tutorial: Programowanie od podstaw. Dział 06: "Powtarzanie i kolekcje".

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

SEKCJA "Pętla po elementach listy":
Przez wszystkie elementy [[lista-danych|listy]] przechodzisz [[petla|pętlą]] `for`: `for imie in osoby:` bierze po kolei każdy [[element-listy|element]] i wykonuje dla niego wcięty blok.

Przy pierwszym przebiegu (czyli [[iteracja|iteracji]]) `imie` dostaje pierwszy element, przy drugim drugi, i tak do ostatniego. Gdy elementy się skończą, pętla sama przestaje, a program idzie dalej, do pierwszej linii bez wcięcia. Nie liczysz indeksów ani nie sprawdzasz długości listy.

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print(imie)
print("Koniec")
```

```text
Ania
Bartek
Celina
Koniec
```

Elementy przychodzą w kolejności listy, więc „Ania” jest pierwsza. Dodasz czwartą osobę, a ta sama pętla obsłuży ją bez zmian.

Pętla może też coś zbierać. Przy liście `wydatki` dodaje kwotę każdego wydatku do sumy; zapis `wydatek["kwota"]` bierze z jednego wydatku pole `kwota`:

```python
wydatki = ...
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(suma)
```

Suma zaczyna od zera, rośnie w każdej iteracji, a wynik pokazujesz dopiero po pętli, już bez wcięcia.
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
