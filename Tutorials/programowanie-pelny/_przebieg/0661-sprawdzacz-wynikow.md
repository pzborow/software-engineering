# Krok 0661 · sprawdzacz_wyników

Węzeł: `review` · dział: 6 · pytanie: 36 · próba: 1

## Prompt

````text
Jesteś sprawdzaczem wyników w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.

Dla każdego bloku kodu, który da się uruchomić samodzielnie (ma wszystkie dane, nie zawiera `...`) i coś wypisuje:
1. Czy bezpośrednio pod nim jest blok ```text z wynikiem? Brak: kind="wynik", severity="blokująca",
   detail = dokładny wynik, który trzeba dopisać.
2. Wykonaj kod w myślach krok po kroku (wartości, obliczenia, zaokrąglenia, formatowanie, kolejność linii)
   i porównaj z podanym wynikiem znak w znak. Niezgodność: kind="wynik", severity="blokująca",
   detail = co się nie zgadza i poprawny wynik.
Szkice (z `...`, bez danych) i bloki bez wypisywania pomiń. ok=true, gdy wszystko się zgadza.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

SEKCJA "Odczyt elementu listy":
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
  "needs": [
    {
      "kind": "przykład",
      "detail": "Błąd IndexError opisany tylko słowami. Można dodać krótki blok z osoby[3] i wynikiem błędu (Traceback... IndexError: list index out of range), żeby czytelnik zobaczył, jak on wygląda.",
      "severity": "sugestia",
      "target": "IndexError"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Funkcja len() pojawia się bez wyjaśnienia. Warto dodać jedno zdanie, że len(osoby) daje liczbę elementów (tu 3), albo odesłać do sekcji, w której len() jest omówione.",
      "severity": "sugestia",
      "target": "len(osoby) - 1"
    }
  ]
}
````
