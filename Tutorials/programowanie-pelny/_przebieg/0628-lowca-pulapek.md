# Krok 0628 · łowca_pułapek

Węzeł: `gotchas` · dział: 6 · pytanie: 34 · próba: —

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

SEKCJA "Pętla nieskończona":
[[petla-nieskonczona|Pętla nieskończona]] to pętla, która nigdy nie dochodzi do końca, bo jej [[warunek-zakonczenia|warunek zakończenia]] nigdy nie zostaje spełniony. Program powtarza wtedy ten sam fragment bez końca, więc nie dociera do dalszych linii i nie oddaje wyniku.

Pętla `for`, którą znasz, kończy się sama, bo zestaw danych się wyczerpuje. Pętla `while` („dopóki”) działa inaczej: powtarza wcięte linie, dopóki warunek daje `True`. Jeśli warunek jest zawsze prawdziwy, każda kolejna [[iteracja|iteracja]] zaczyna się od nowa.

```python
import time
while True:
    print("Liczę wydatki...")
    time.sleep(1)
```

Tu warunek to na stałe `True`, a w ciele nic go nie zmienia. Linia `time.sleep(1)` robi tylko jednosekundową przerwę, żeby napisy nie zalały ekranu. Zdarza się to też przez pomyłkę: warunek zależy od zmiennej, której pętla nigdy nie zmienia.

Problem jest praktyczny. Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków. Tak samo wyglądałaby „Wspólna Kasa”, która czeka na koniec listy, którego nie ma.

Zatrzymasz taki program skrótem Ctrl+C w terminalu. Python przerywa wtedy działanie i wypisuje komunikat `KeyboardInterrupt`, czyli „przerwano z klawiatury”. To nie awaria, tylko Twoja komenda.

Dlatego przy każdej pętli `while` zadaj sobie pytanie: co sprawi, że warunek w końcu stanie się fałszywy?
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
