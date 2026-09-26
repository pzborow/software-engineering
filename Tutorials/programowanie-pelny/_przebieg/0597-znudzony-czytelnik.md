# Krok 0597 · znudzony_czytelnik

Węzeł: `review` · dział: 6 · pytanie: 33 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Kiedy warto użyć pętli zamiast pisać to samo wiele razy?".

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
## Czym jest pętla
[[petla|Pętla]] to instrukcja, która każe programowi wykonać ten sam fragment kodu wielokrotnie. Zamiast pisać tę samą linię trzy razy, zapisujesz ją raz i mówisz, ile razy albo dla czego ją powtórzyć.

Jedno powtórzenie fragmentu nazywamy [[iteracja|iteracją]]. Pętla `for` wykonuje po jednej iteracji dla każdego elementu z zestawu danych. Taki zestaw to na razie po prostu lista wartości w nawiasach kwadratowych; jej zapis omówimy osobno.

Wcięte linie pod `for` to ciało pętli, tak samo jak przy `if`. Nazwa po słowie `for` to zmienna, która w każdej iteracji dostaje kolejny element:

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print("Cześć,", imie)
print("Koniec")
```

```text
Cześć, Ania
Cześć, Bartek
Cześć, Celina
Koniec
```

Ciało wykonało się trzy razy, bo na liście są trzy osoby. Za każdym razem `imie` miało inną wartość. Ostatni `print` nie ma wcięcia, więc pętla nie obejmuje go i wykonuje się raz, po jej zakończeniu.

Pętla ma więc początek, powtarzane kroki i koniec, a koniec wynika z [[warunek-zakonczenia|warunku zakończenia]]: w `for` jest nim wyczerpanie elementów. W „Wspólnej Kasie” dzięki temu jeden zapis obsłuży trzy osoby, ale też trzydzieści.

NOWA SEKCJA "Kiedy sięgnąć po pętlę":
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
      "kind": "spójność",
      "detail": "Tekst twierdzi, że pętla dopasowuje się do danych i obsłuży czwartą osobę. W przykładzie liczba_osob = 3 jest wpisana ręcznie, więc po dodaniu czwartej osoby wynik byłby błędny (300/3). Warto to zauważyć w jednym zdaniu, np. że tę liczbę też trzeba by zmienić, a jak liczyć elementy listy, pokażemy później. Albo dać przykład, w którym liczba osób nie jest potrzebna.",
      "severity": "sugestia",
      "target": "przykład z liczba_osob = 3"
    },
    {
      "kind": "przykład",
      "detail": "Zdanie o poprawce wzoru w jednym miejscu zamiast trzech odwołuje się do wersji bez pętli, której czytelnik nie widzi. Wystarczą trzy linie print z powtórzonym wzorem, żeby zobaczyć, co pętla oszczędza.",
      "severity": "sugestia",
      "target": "Poprawka wzoru to jedna zmiana zamiast trzech"
    }
  ]
}
````
