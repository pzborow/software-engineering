# Krok 1034 · sprawdzacz_wyników

Węzeł: `review` · dział: 9 · pytanie: 53 · próba: 1

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

SEKCJA "Czym jest debugowanie":
[[debugowanie|Debugowanie]] to szukanie przyczyny błędu i jej usuwanie. Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach.

Metoda jest prosta. Najpierw odtwarzasz błąd na jednych, konkretnych danych. Potem zawężasz miejsce: przed podejrzanym krokiem wypisujesz wartości i porównujesz je z tym, czego oczekujesz. Pierwsze miejsce, w którym wartość jest inna niż powinna, wskazuje przyczynę. Na końcu poprawiasz jedną rzecz i uruchamiasz ponownie.

Weźmy [[blad-logiczny|błąd logiczny]] z wynikiem 39.0 zamiast 26.0. Podejrzewamy dwa dane wejściowe dzielenia, więc je wypisujemy:

```python
def na_osobe(suma, osoby):
    return suma / osoby

suma = 78.0
liczba_osob = 2
print("DEBUG suma:", suma)
print("DEBUG liczba_osob:", liczba_osob)
print(na_osobe(suma, liczba_osob))
```

```text
DEBUG suma: 78.0
DEBUG liczba_osob: 2
39.0
```

Suma się zgadza, a liczba osób nie: mają być trzy. Funkcja jest w porządku, błąd siedzi w danych, które jej podajemy. Bez wypisania szukalibyśmy pewnie w dzieleniu.

Gdy test z poprzedniej sekcji zgłosi błąd, zaczynasz tak samo: odtwarzasz przypadek, który go wywołał, i patrzysz na wartości. Po naprawie usuń linie z `DEBUG`, żeby nie zaśmiecały wyniku.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
