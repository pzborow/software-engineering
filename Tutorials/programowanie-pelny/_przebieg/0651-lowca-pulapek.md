# Krok 0651 · łowca_pułapek

Węzeł: `gotchas` · dział: 6 · pytanie: 35 · próba: —

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

SEKCJA "Czym jest lista danych":
[[lista-danych|Lista danych]] to jedna zmienna, która przechowuje wiele wartości w ustalonej kolejności. Zamiast trzech zmiennych z imionami masz jedną nazwę, pod którą leży cały zestaw.

Właśnie po takim zestawie chodzi [[petla|pętla]] `for`: wcześniej szła po imionach uczestników, a teraz przyglądamy się samej liście.

Listę zapisujesz w nawiasach kwadratowych, a wartości oddzielasz przecinkami. Każda wartość to [[element-listy|element listy]], czyli jedno miejsce w zestawie. Tekst ma cudzysłów, liczba nie, tak samo jak przy zwykłych zmiennych.

```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby)
print(len(osoby))
```

```text
['Ania', 'Bartek', 'Celina']
3
```

Funkcja `len()` podaje długość listy, czyli liczbę elementów. Python wypisuje listę w nawiasach, a teksty w apostrofach; to tylko sposób wyświetlania.

Kolejność ma znaczenie: „Ania” jest pierwsza i tak zostaje. Lista może być też dłuższa albo pusta (`[]`), a program nie musi z góry znać jej rozmiaru. Dlatego pasuje do „Wspólnej Kasy”: `osoby` to uczestnicy wyjazdu, a `wydatki` to zapłacone rachunki, których przybywa.

Jak sięgnąć po jeden element, omówimy osobno. To, co lista daje pętli, zobaczysz przy przechodzeniu przez wszystkie elementy.
````

## Odpowiedź

````json
{
  "gotchas": []
}
````
