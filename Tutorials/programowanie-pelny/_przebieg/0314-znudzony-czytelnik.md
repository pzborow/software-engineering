# Krok 0314 · znudzony_czytelnik

Węzeł: `review` · dział: 4 · pytanie: 19 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym jest dana w programie?".

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
## Do czego służą komentarze
[[komentarz|Komentarz]] to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi.

W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. [[interpreter|Interpreter]] pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją.

```python
# rozlicz.py - rozliczenie wspólnych wydatków
print("Wspólna Kasa")
# udział na dwie osoby
print(300 / 3)  # 300 zł na troje osób
# print(300 / 2)  <- ta linia jest wyłączona
```

```text
Wspólna Kasa
100.0
```

Ostatnia linia pokazuje drugie zastosowanie: zamiana instrukcji na komentarz „wyłącza” ją bez kasowania. Przyda się to, gdy będziesz coś sprawdzać.

Komentarz ma sens, gdy podaje powód lub kontekst („300 zł na troje osób”). Powtarzanie tego, co widać w kodzie, tylko go zaśmieca.

Komentarz może się też zestarzeć. W przykładzie wyżej linia `# udział na dwie osoby` stoi nad dzieleniem przez 3, więc kłamie, a Python tego nie zauważy, bo jej nie czyta. Zmieniając kod, poprawiaj też komentarz.

U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej. Komentarz nie przeszkadza w znalezieniu błędu: popraw literówkę i uruchom plik ponownie.

NOWA SEKCJA "Czym jest dana":
[[dana|Dana]] to każda informacja, na której pracuje program: imię, kwota, data, odpowiedź „tak” lub „nie”. Program bez danych nie miałby czego liczyć ani wypisać.

W arkuszu kalkulacyjnym danymi są wartości w komórkach: nazwisko w jednej, kwota w drugiej. W programie jest podobnie, tylko że dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz.

```python
print("Ania")   # tekst: imię
print(45.5)     # liczba: kwota wydatku
print(True)     # prawda albo fałsz: czy zapłacono
```

```text
Ania
45.5
True
```

Każda z tych trzech wartości to jedna dana, ale każda jest innego rodzaju. Tekst w cudzysłowie służy do pokazywania i porównywania napisów. Liczbę można dodawać i dzielić. Prawda lub fałsz odpowiada na pytanie tak/nie. Rodzaj danej decyduje o tym, co program może z nią zrobić: kwoty da się dodać, imion nie.

Dane trzeba też gdzieś przechowywać, żeby użyć ich więcej niż raz. Do tego służy zmienna, którą poznasz w następnej sekcji. Rodzaje danych omówimy osobno, gdy przejdziemy do typów.

U siebie w `kasa.py` dopiszesz za chwilę te trzy rodzaje danych dla wyjazdu i sprawdzisz, jak Python je nazywa.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Zdanie „dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz” jest ogólnikowe. Wystarczy jedno konkretne wskazanie, np. „wpisane z klawiatury lub wczytane z pliku”. Można też usunąć „albo dostajesz z zewnątrz”, skoro w tutorialu nie ma o tym przykładu. Zdanie „imion nie da się dodać” jest też uproszczone, bo napisy można łączyć, ale dla początkującego to zrozumiałe.",
      "severity": "sugestia",
      "target": "dostajesz z zewnątrz"
    }
  ]
}
````
