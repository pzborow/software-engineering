# Krok 0657 · znudzony_czytelnik

Węzeł: `review` · dział: 6 · pytanie: 36 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak odczytać konkretny element listy?".

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
## Czym jest lista danych
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

NOWA SEKCJA "Odczyt elementu listy":
Po element listy sięgasz przez jego numer w nawiasach kwadratowych: `osoby[0]`. Numer nazywa się [[indeks|indeksem]] i liczenie zaczyna się od zera, więc pierwszy element ma indeks 0, drugi 1, trzeci 2.

Wygląda to dziwnie, ale trzeba się przyzwyczaić: indeks mówi, o ile miejsc od początku listy się przesunąć. Pierwszy element jest na początku, więc przesunięcie wynosi zero. Kolejność z listy zostaje zachowana, o czym była mowa w sekcji [[sec-06-czym-jest-lista-danych|Czym jest lista danych]].

Ujemny indeks liczy od końca: `-1` to ostatni element, `-2` przedostatni. Wygodne, gdy nie wiesz, ile elementów ma lista.

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

Indeks spoza listy kończy się błędem `IndexError`. Przy trzech osobach ostatni jest `osoby[2]`, a `osoby[3]` nie istnieje, więc program się zatrzyma. Największy poprawny indeks to zawsze `len(osoby) - 1`.

Odczyt niczego nie zmienia: lista zostaje taka sama, dostajesz tylko kopię wartości.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
