# Krok 0855 · sprawdzacz_wyników

Węzeł: `review` · dział: 8 · pytanie: 44 · próba: 1

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

SEKCJA "Dane wejściowe programu":
[[dane-wejsciowe|Dane wejściowe]] to wszystko, co program dostaje z zewnątrz, żeby mieć na czym pracować: wpisane słowo, liczba, zawartość pliku. Sam z siebie nie wie, kto zapłacił za zakupy ani ile, więc ktoś musi mu to podać.

Źródła są różne, ale idea ta sama: wartość pojawia się w programie, choć nie została zapisana w kodzie.

| Źródło | Przykład we „Wspólnej Kasie” |
|---|---|
| użytkownik | wpisuje imię i kwotę nowego wydatku |
| plik | `wydatki.csv` z listą dotychczasowych wydatków |
| inny program | dane wyeksportowane z aplikacji banku |

Do tej pory kwoty wpisywaliśmy w kodzie, np. `mazury = [45.5, 20, 12.5]`. Wtedy każda zmiana danych wymagała edycji programu. Dane wejściowe rozdzielają obie sprawy: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne.

Tak mogłoby wyglądać pobranie danych od użytkownika (szkic, do którego wrócimy przy pytaniu użytkownika):

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    ...
```

Ważna konsekwencja: program nie kontroluje, co dostanie. Ktoś może wpisać „abc” zamiast kwoty, a plik może być pusty. Dlatego dane wejściowe trzeba traktować ostrożnie i sprawdzać, a o wyniku, który program oddaje na zewnątrz, opowiemy przy [[dane-wejsciowe|danych wyjściowych]].
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "odwołanie",
      "detail": "Odsyłacz [[dane-wejsciowe|danych wyjściowych]] wskazuje na hasło „dane-wejsciowe”, czyli na tę samą sekcję. Tekst mówi o danych wyjściowych, więc czytelnik kliknie i dostanie definicję danych wejściowych. Trzeba zmienić cel na właściwe hasło (np. [[dane-wyjsciowe|danych wyjściowych]]) i sprawdzić, że takie hasło jest w glosariuszu.",
      "severity": "blokująca",
      "target": "[[dane-wejsciowe|danych wyjściowych]]",
      "source": "ostatni akapit"
    }
  ]
}
````
