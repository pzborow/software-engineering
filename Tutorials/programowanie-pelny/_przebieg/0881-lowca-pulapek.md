# Krok 0881 · łowca_pułapek

Węzeł: `gotchas` · dział: 8 · pytanie: 45 · próba: —

## Prompt

````text
Jesteś doświadczonym recenzentem kodu. Czytelnik: osoba spoza IT, poziom: początkujący.
Tutorial: Programowanie od podstaw. Dział 08: "Współpraca programu z użytkownikiem".

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

SEKCJA "Dane wyjściowe programu":
[[dane-wyjsciowe|Dane wyjściowe]] to wszystko, co program oddaje na zewnątrz: wynik obliczeń, komunikat, zapisany plik. To druga strona [[dane-wejsciowe|danych wejściowych]]: wejście wpuszcza informacje do programu, wyjście je z niego wypuszcza.

Bez wyjścia program mógłby liczyć, ale nikt by o tym nie wiedział. Wynik zamknięty w zmiennej znika, gdy program się kończy.

Wyjście ma kilka adresatów:

| Dokąd trafia wynik | Przykład we „Wspólnej Kasie” |
|---|---|
| ekran | komunikat „Na osobę wychodzi 26.0” |
| plik | zapisane rozliczenie wyjazdu |
| inny program | dane przekazane do aplikacji banku |

Na razie znasz tylko pierwszą drogę: `print` pokazuje wartość w terminalu. Robiłeś to już w funkcji `wypisz_na_osobe`, o której mówiliśmy przy zwracaniu wyniku (przypomnienie: `print` tylko pokazuje tekst, niczego nie zwraca).

```python
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wypisz_na_osobe(78, 3)
```

```text
26.0
```

Konsekwencja: o tym, co program wypisze, decydujesz Ty. Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. Do plików wrócimy osobno, a wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie.
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
