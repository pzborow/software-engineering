# Krok 0600 · sprawdzacz_wyników

Węzeł: `review` · dział: 6 · pytanie: 33 · próba: 1

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

SEKCJA "Kiedy sięgnąć po pętlę":
Pętli warto użyć, gdy ta sama czynność dotyczy wielu elementów albo liczba powtórzeń zależy od danych. Jeśli kopiujesz linię i zmieniasz w niej tylko jedną wartość, to znak, że potrzebna jest [[petla|pętla]].

Powtarzanie ręczne ma dwie wady. Poprawkę trzeba wprowadzić w wielu miejscach, a przy każdej łatwo o pomyłkę. Poza tym taki kod nie dopasuje się do danych: napisany na trzy osoby nie obsłuży czwartej.

```python
osoby = ["Ania", "Bartek", "Celina"]
liczba_osob = 3
for imie in osoby:
    print(imie, "płaci", 300 / liczba_osob)
```

```text
Ania płaci 100.0
Bartek płaci 100.0
Celina płaci 100.0
```

Zmienia się tylko `imie`, więc reszta linii jest zapisana jeden raz. Poprawka wzoru to jedna zmiana zamiast trzech.

| Sytuacja | Rozwiązanie |
|---|---|
| Ta sama czynność dla każdego elementu zestawu | pętla |
| Liczba powtórzeń zależy od danych | pętla |
| Dwie różne czynności, każda raz | zwykłe linie |
| Pojedyncza czynność, która się nie powtarza | zwykła linia |

Pętla `for` ma z góry znany koniec. Pętlę, która nigdy się nie kończy, omówimy w następnej kolejności.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Sygnał 'kopiujesz linię i zmieniasz jedną wartość' nie ma pokazanego kodu. Warto dać wersję ręczną (trzy razy print z inną nazwą) przed pętlą, żeby czytelnik zobaczył kontrast.",
      "severity": "sugestia",
      "target": "Powtarzanie ręczne / przykład z pętlą"
    }
  ]
}
````
