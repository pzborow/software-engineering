# Krok 0690 · znudzony_czytelnik

Węzeł: `review` · dział: 6 · pytanie: 37 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak przejść przez wszystkie elementy listy?".

Zgłoś potrzeby (najwyżej 3, zero też jest dobrą odpowiedzią), wybierając kind:
- "przykład": teza jest abstrakcyjna i brakuje krótkiego kodu lub scenariusza,
- "konkret": ogólniki zamiast decyzji, liczby, nazwy klasy albo porównania,
- "skrócenie": powtórzenia, lanie wody, przykład dłuższy niż potrzeba,
- "diagram": przepływ łatwiej zrozumieć z rysunku tekstowego,
- "tempo": za dużo nowych pojęć naraz albo sekcja nie wnosi nic nowego względem poprzedniej.
Sekcja ma limit 250 słów prozy i jeden, najwyżej dwa krótkie bloki kodu.
Nie proś o coś, co się w tym nie zmieści, i nie żądaj jednocześnie dodania i skrócenia.
Kod może być tylko w językach: python, text.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

POPRZEDNIA SEKCJA:
## Odczyt elementu listy
Po element listy sięgasz przez jego numer w nawiasach kwadratowych: `osoby[0]`. Numer nazywa się [[indeks|indeksem]] i liczenie zaczyna się od zera, więc pierwszy element ma indeks 0, drugi 1, trzeci 2.

Wygląda to dziwnie, ale indeks mówi, o ile miejsc od początku listy się przesunąć. Pierwszy element jest na samym początku, więc przesunięcie wynosi zero. Kolejność zostaje taka, jak w sekcji Czym jest lista danych.

Ujemny indeks liczy od końca: `-1` to ostatni element, `-2` przedostatni. Jest wygodny, gdy nie wiesz, ile elementów ma lista.

```python
osoby = ["Ania", "Bartek", "Celina"]
print(osoby[0])
print(osoby[2])
print(osoby[-1])
```

```text
Ania
Celina
Celina
```

Indeks spoza listy kończy się błędem `IndexError`. Przy trzech osobach ostatni jest `osoby[2]`, a `osoby[3]` nie istnieje, więc program się zatrzyma. Największy poprawny indeks to `len(osoby) - 1`.

Odczyt niczego nie zmienia: lista zostaje taka sama, dostajesz tylko kopię wartości.

NOWA SEKCJA "Pętla po elementach listy":
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
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Drugi blok zaczyna się od `wydatki = ...`, więc czytelnik nie widzi, jak wyglądają dane, i nie może sprawdzić wyniku. Dajcie 2–3 konkretne wydatki, np. `{\"nazwa\": \"chleb\", \"kwota\": 5}`, i pokażcie wynik w bloku text. Wtedy zapis `wydatek[\"kwota\"]` będzie zrozumiały bez zgadywania.",
      "severity": "sugestia",
      "target": "blok kodu z sumą wydatków"
    }
  ]
}
````
