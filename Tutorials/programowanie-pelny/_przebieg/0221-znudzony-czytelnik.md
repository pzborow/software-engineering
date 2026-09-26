# Krok 0221 · znudzony_czytelnik

Węzeł: `review` · dział: 3 · pytanie: 15 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Co to znaczy uruchomić program?".

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
## Do czego służy edytor
[[edytor-kodu|Edytor kodu]] to program do pisania i poprawiania [[kod-zrodlowy|kodu źródłowego]], który pomaga czytać kod i zauważać w nim pomyłki. Sam kodu nie uruchamia i nie zmienia jego działania: zmienia tylko to, jak wygodnie się go pisze.

Skoro kod jest zwykłym plikiem tekstowym, można go napisać nawet w Notatniku. Edytor kodu dodaje jednak rzeczy, które przy programowaniu bardzo oszczędzają czas:

| Możliwość | Co daje |
|---|---|
| [[podswietlanie-skladni|podświetlanie składni]] | słowa języka, teksty i liczby mają różne kolory, więc struktura kodu jest widoczna |
| numery linii | komunikat „błąd w linii 3” da się od razu znaleźć |
| wcięcia i nawiasy | edytor wcina linie i domyka cudzysłowy oraz nawiasy |
| podpowiedzi | po wpisaniu kilku liter proponuje dokończenie nazwy |
| zapis w zwykłym tekście | plik da się otworzyć w dowolnym innym programie |

Podświetlanie składni to kolorowanie fragmentów kodu według ich roli. Literówka w nazwie polecenia często od razu zmienia kolor, zanim cokolwiek uruchomisz.

Przykładem będzie VS Code, ale wybór edytora jest sprawą gustu. Zasady pisania kodu są w każdym takie same.

U siebie sprawdzisz teraz, czy działa [[python|Python]] (jeden z języków programowania, którego użyjemy w tym kursie), i zapiszesz pierwszy plik. Uruchomimy go w następnej części, gdy wyjaśnimy, co to znaczy uruchomić program.

NOWA SEKCJA "Co znaczy uruchomić program":
Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam [[kod-zrodlowy|kod źródłowy]] leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś go nie zacznie realizować.

Plik z kodem jest [[uruchamianie-programu|uruchamiany]] przez inny program, który go czyta i wykonuje linia po linii. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.

Polecenie wpisujemy w [[terminal|terminalu]], czyli oknie, w którym komputer przyjmuje polecenia pisane tekstem i pokazuje odpowiedzi tekstem. Przykład to nasz plik `rozlicz.py`:

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

W terminalu wpisujemy `python rozlicz.py`, a program wypisuje:

```text
Wspólna Kasa
100.0
```

Kolejność wyjścia jest taka sama jak kolejność linii, bo instrukcje wykonują się jedna po drugiej. Wynik `100.0` to 300 zł podzielone na trzy osoby.

Uruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. Tak wygląda cała praca programisty: zapisz, uruchom, przeczytaj wynik.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Nie jest jasne, gdzie wpisać polecenie ani czy terminal trzeba otworzyć w folderze z plikiem. Początkujący może dostać błąd „nie znaleziono pliku”. Wystarczy jedno zdanie, np. że terminal otwieramy w folderze z rozlicz.py.",
      "target": "terminal / python rozlicz.py",
      "severity": "sugestia",
      "source": "",
      "status": "nowa"
    }
  ]
}
````
