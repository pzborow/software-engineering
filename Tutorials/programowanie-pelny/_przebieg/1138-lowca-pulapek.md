# Krok 1138 · łowca_pułapek

Węzeł: `gotchas` · dział: 10 · pytanie: 58 · próba: —

## Prompt

````text
Jesteś doświadczonym recenzentem kodu. Czytelnik: osoba spoza IT, poziom: początkujący.
Tutorial: Programowanie od podstaw. Dział 10: "Programowanie w praktyce".

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
- `input` zawsze zwraca tekst, nawet dla liczb
- Ścieżka względna zależy od folderu uruchomienia
- Sprawdzenie przepuszcza tekst, którego float nie przyjmie
- assert znika przy uruchomieniu z -O

SEKCJA "Od pomysłu do działającego programu":
Od pomysłu do programu dochodzi się małymi krokami: opisujesz zadanie zwykłymi słowami, piszesz najmniejszy kawałek, który coś robi, sprawdzasz go i dopiero wtedy dokładasz następny. Cały program naraz zwykle nie działa, a szukanie błędu w stu liniach jest męczące.

```text
pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit
              ↑                                                            |
              └──────────────────── następny kawałek ←─────────────────────┘
```

Weźmy pomysł: „chcę wiedzieć, kto komu ile jest winien”. Opis krokowy to rozbicie zadania na kroki, z których każdy da się zrobić osobno: dla każdej osoby zsumuj to, co zapłaciła, odejmij jej równy udział i wypisz wynik. Z tego wychodzi jedna mała [[funkcja]]:

```python
def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...
```

Funkcję sprawdzasz na danych, których wynik znasz z kartki. Dopiero gdy się zgadza, zapisujesz [[commit]] (zapisaną wersję kodu z opisem) i myślisz o kolejnym kawałku, np. wczytaniu wydatków z pliku.

Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, jak w sekcji o zapisywaniu wersji kodu. Dzięki temu nie zgadujesz, gdzie szukać błędu.
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
