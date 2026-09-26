# Krok 0737 · sprawdzacz_wyników

Węzeł: `review` · dział: 7 · pytanie: 39 · próba: 1

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

SEKCJA "Po co dzielić program na funkcje":
Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach.

Zobacz to na „Wspólnej Kasie”. Sumę wydatków wydzieliliśmy już do funkcji, a teraz dokładamy drugą, która z niej korzysta:

```python
def suma_wydatkow(wydatki):
    suma = 0
    for wydatek in wydatki:
        suma = suma + wydatek["kwota"]
    return suma

def udzial_na_osobe(wydatki, liczba_osob):
    return suma_wydatkow(wydatki) / liczba_osob

mazury = [{"kto": "Ania", "kwota": 120.5}, {"kto": "Bartek", "kwota": 79.5}]
tatry = [{"kto": "Celina", "kwota": 450}]
print(udzial_na_osobe(mazury, 2))
print(udzial_na_osobe(tatry, 3))
```

```text
100.0
150.0
```

Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz. Gdyby liczenie sumy trzeba było kiedyś zmienić, poprawiasz jedną funkcję, a oba wyniki będą poprawne.

Druga korzyść to czytelność: `udzial_na_osobe(mazury, 2)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, do czego wrócimy przy testowaniu programu.

U siebie masz już `funkcje.py` z jedną funkcją. Za chwilę dopiszesz drugą i użyjesz obu dla dwóch wyjazdów.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
