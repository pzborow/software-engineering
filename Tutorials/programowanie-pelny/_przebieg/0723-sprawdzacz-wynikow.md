# Krok 0723 · sprawdzacz_wyników

Węzeł: `review` · dział: 7 · pytanie: 38 · próba: 2

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

SEKCJA "Czym jest funkcja":
[[funkcja|Funkcja]] to nazwany kawałek kodu, który raz opisujesz, a potem uruchamiasz, kiedy zechcesz, wpisując jego nazwę. Znasz już gotowe funkcje: `print()` i `str()` napisali twórcy Pythona.

Własną funkcję zaczynasz od `def`, nazwy, nawiasów i dwukropka. Wcięty blok pod spodem to jej treść. Ten zapis to [[definicja-funkcji|definicja funkcji]]: tylko opisuje, co funkcja robi, i niczego jeszcze nie wykonuje. Dopiero [[wywolanie-funkcji|wywołanie]], czyli nazwa z nawiasami, uruchamia treść.

Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:

```python
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

print(suma([45.5, 20, 12.5]))
```

```text
78.0
```

Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. Oba mechanizmy omówimy osobno w kolejnych sekcjach; na razie wystarczy, że dane wchodzą, a wynik wychodzi.

Konsekwencja: kod, który był kawałkiem długiego programu, ma teraz nazwę i można go wywołać w wielu miejscach, bez kopiowania.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
