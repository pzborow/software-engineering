# Krok 0591 · łowca_pułapek

Węzeł: `gotchas` · dział: 6 · pytanie: 32 · próba: —

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

SEKCJA "Czym jest pętla":
[[petla|Pętla]] to instrukcja, która każe programowi wykonać ten sam fragment kodu wielokrotnie. Zamiast pisać tę samą linię trzy razy, zapisujesz ją raz i mówisz, ile razy albo dla czego ją powtórzyć.

Jedno powtórzenie fragmentu nazywamy [[iteracja|iteracją]]. Pętla `for` wykonuje po jednej iteracji dla każdego elementu z zestawu danych. Taki zestaw to na razie po prostu lista wartości w nawiasach kwadratowych; jej zapis omówimy osobno.

Wcięte linie pod `for` to ciało pętli, tak samo jak przy `if`. Nazwa po słowie `for` to zmienna, która w każdej iteracji dostaje kolejny element:

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print("Cześć,", imie)
print("Koniec")
```

```text
Cześć, Ania
Cześć, Bartek
Cześć, Celina
Koniec
```

Ciało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. Ostatni `print` nie ma wcięcia, więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.

Pętla ma więc początek, powtarzane kroki i koniec, a koniec wynika z [[warunek-zakonczenia|warunku zakończenia]]: w `for` jest nim wyczerpanie elementów. W „Wspólnej Kasie” dzięki temu jeden zapis obsłuży trzy osoby, ale też trzydzieści.
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
