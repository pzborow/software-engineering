# Krok 0861 · znudzony_czytelnik

Węzeł: `review` · dział: 8 · pytanie: 44 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym są dane wejściowe programu?".

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
## Ponowne użycie kodu
Ponowne użycie kodu to wykorzystanie tego samego fragmentu wiele razy zamiast pisania go od nowa. W Pythonie robisz to przez [[funkcja|funkcję]]: [[definicja-funkcji|definicję]] piszesz raz, a potem robisz dowolną liczbę [[wywolanie-funkcji|wywołań]] z innymi danymi.

Zobacz dwa wyjazdy liczone tą samą logiką:

```python
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

mazury = [45.5, 20, 12.5]
tatry = [300, 150]
print(udzial_na_osobe(suma_wydatkow(mazury), 3))
print(udzial_na_osobe(suma_wydatkow(tatry), 4))
```

```text
26.0
112.5
```

Zmieniają się tylko dane: lista wydatków i liczba osób. Logika liczenia leży w jednym miejscu, więc nie kopiujesz pętli dla każdego wyjazdu.

Ma to dwie konsekwencje. Gdy znajdziesz błąd w liczeniu sumy, poprawiasz go raz i naprawiasz wszystkie wyjazdy naraz. A trzeci wyjazd to jedna nowa lista i dwa wywołania, bez nowego kodu.

Właśnie po to funkcje mają parametry: to, co stałe, zostaje w środku, a to, co zmienne, wchodzi z zewnątrz.

U siebie w `funkcje.py` masz te same funkcje (pod krótszymi nazwami `suma` i `na_osobe`). Ostatnia linia wywołuje `na_osobe(300)` z jednym argumentem zamiast dwóch, stąd błąd. Usuwamy ją w warsztacie poniżej.

NOWA SEKCJA "Dane wejściowe programu":
[[dane-wejsciowe|Dane wejściowe]] to wszystko, co program dostaje z zewnątrz, żeby mieć na czym pracować: wpisane słowo, liczba, zawartość pliku. Sam z siebie nie wie, kto zapłacił za zakupy ani ile, więc ktoś musi mu to podać.

Źródła są różne, ale idea ta sama: wartość pojawia się w programie, choć nie została zapisana w kodzie.

| Źródło | Przykład we „Wspólnej Kasie” |
|---|---|
| użytkownik | wpisuje imię i kwotę nowego wydatku |
| plik | `wydatki.csv` z listą dotychczasowych wydatków |
| inny program | dane wyeksportowane z aplikacji banku |

Do tej pory kwoty wpisywaliśmy w kodzie, np. `mazury = [45.5, 20, 12.5]`. Wtedy każda zmiana danych wymagała edycji programu. Dane wejściowe rozdzielają obie sprawy: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne.

Tak mogłoby wyglądać pobranie danych od użytkownika (szkic, do którego wrócimy, gdy zajmiemy się pytaniem użytkownika o informację):

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    ...
```

Ważna konsekwencja: program nie kontroluje, co dostanie. Ktoś może wpisać „abc” zamiast kwoty, a plik może być pusty. Dlatego dane wejściowe trzeba traktować ostrożnie i sprawdzać. O wyniku, który program oddaje na zewnątrz, opowiemy osobno, przy danych wyjściowych.

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [odwołanie] [[dane-wejsciowe|danych wyjściowych]]: Fraza „danych wyjściowych” ma ten sam identyfikator hasła co dane wejściowe: [[dane-wejsciowe|danych wyjściowych]]. Kliknięcie prowadzi do złego hasła i miesza dwa przeciwne pojęcia. Trzeba podać osobny identyfikator (np. dane-wyjsciowe) z własnym hasłem w glosariuszu albo usunąć link i zostawić samą zapowiedź.
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
