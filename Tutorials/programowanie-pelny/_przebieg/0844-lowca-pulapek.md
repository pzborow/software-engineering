# Krok 0844 · łowca_pułapek

Węzeł: `gotchas` · dział: 7 · pytanie: 43 · próba: —

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

SEKCJA "Ponowne użycie kodu":
Ponowne użycie kodu to wykorzystanie tego samego fragmentu wiele razy zamiast pisania go od nowa. W Pythonie robisz to przez [[funkcja|funkcję]]: [[definicja-funkcji|definicję]] piszesz raz, a potem robisz dowolną liczbę [[wywolanie-funkcji|wywołań]] z innymi danymi.

Zobacz dwa wyjazdy liczone tą samą logiką:

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print(udzial_na_osobe(suma_wydatkow(mazury), 3))
print(udzial_na_osobe(suma_wydatkow(tatry), 4))
```

```text
26.0
112.5
```

Zmieniają się tylko dane: lista wydatków i liczba osób. Logika liczenia leży w jednym miejscu, więc nie kopiujesz pętli dla każdego wyjazdu.

Ma to dwie konsekwencje. Gdy znajdziesz błąd w liczeniu sumy, poprawiasz go raz i naprawiasz wszystkie wyjazdy naraz. A trzeci wyjazd to jedna nowa lista i dwa wywołania, bez nowego kodu.

Właśnie po to funkcje mają parametry: to, co stałe, zostaje w środku, a to, co zmienne, wchodzi z zewnątrz.

U siebie w `funkcje.py` masz te same funkcje (pod krótszymi nazwami `suma` i `na_osobe`). Ostatnia linia wywołuje `na_osobe(300)` z jednym argumentem zamiast dwóch, stąd błąd. Usuwamy ją w warsztacie poniżej.
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
