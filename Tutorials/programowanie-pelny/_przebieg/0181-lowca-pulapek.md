# Krok 0181 · łowca_pułapek

Węzeł: `gotchas` · dział: 2 · pytanie: 12 · próba: —

## Prompt

````text
Jesteś doświadczonym recenzentem kodu. Czytelnik: osoba spoza IT, poziom: początkujący.
Tutorial: Programowanie od podstaw. Dział 02: "Algorytmy i myślenie krokowe".

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
(brak)

SEKCJA "Poprawny algorytm":
[[algorytm|Algorytm]] jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny z tym, czego od niego wymagamy. Nie wystarczy, że zadziałał raz na jednym przykładzie.

Najpierw trzeba więc ustalić, co znaczy „zgodny”. To [[specyfikacja-wyniku|specyfikacja wyniku]]: krótki opis, jaki wynik ma wyjść z jakich danych. Dla rozliczenia może brzmieć tak: suma wszystkich sald wynosi 0 zł, a nikomu nie znika ani nie przybywa grosza. Bez takiego opisu nie ma czego sprawdzać.

Potem sprawdzasz dwie rzeczy: czy algorytm zawsze dochodzi do [[warunek-zakonczenia|warunku zakończenia]] i czy wynik spełnia specyfikację. Ważne są zwłaszcza [[przypadek-brzegowy|przypadki brzegowe]], czyli dane na skraju dozwolonego zakresu: jedna osoba, brak wydatków, kwota, która nie dzieli się równo.

Ten ostatni przypadek łatwo przeoczyć. W kodzie kwoty liczymy w groszach, a znak `//` dzieli i odrzuca resztę: `10000 // 3` daje `3333`, nie `3333,33`.

```python
# poza kanonem: udział w groszach, dzielenie całkowite
def udzial(suma_gr, osoby):
    return suma_gr // osoby

print(udzial(12000, 4) * 4)
print(udzial(10000, 3) * 3)
```

```text
12000
9999
```

Dla 120 zł na czworo wszystko się zgadza. Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza. Dlatego w naszej liście kroków jest zdanie „Resztę groszy dopisz pierwszej osobie.”: bez niego algorytm byłby niepoprawny, choć pierwszy przykład by przeszedł.

Konsekwencja: poprawność sprawdzasz na wielu danych, w tym celowo niewygodnych. Do systematycznego sprawdzania wrócimy przy testowaniu programu.
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
