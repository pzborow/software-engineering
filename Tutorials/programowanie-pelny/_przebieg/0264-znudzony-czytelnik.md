# Krok 0264 · znudzony_czytelnik

Węzeł: `review` · dział: 3 · pytanie: 17 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Co to jest błąd w programie?".

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
## Kompilator i interpreter
Kompilator i interpreter to programy, które przekładają [[kod-zrodlowy|kod źródłowy]] na działanie komputera, bo procesor sam nie rozumie tekstu z pliku. [[kompilator|Kompilator]] tłumaczy cały kod naraz na osobny, gotowy do uruchomienia plik. [[interpreter|Interpreter]] czyta kod i wykonuje go na bieżąco, instrukcja po instrukcji.

To ten wykonawca, o którym była mowa przy uruchamianiu programu. Gdy wpisujesz `python rozlicz.py`, [[python|Python]] działa jako interpreter: bierze plik i wykonuje go od góry.

| | Kompilator | Interpreter |
|---|---|---|
| Co robi | tłumaczy całość przed startem | wykonuje kod w trakcie czytania |
| Wynik | osobny plik do uruchomienia | brak pliku, od razu efekt |
| Uruchomienie po zmianie | najpierw kompilacja, potem start | zapisz i uruchom |

```text
kompilator:   kod źródłowy --> [kompilator] --> plik programu --> uruchomienie
interpreter:  kod źródłowy --> [interpreter] --> uruchomienie
```

Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania. Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie. W praktyce Python najpierw przekłada plik na pośredni zapis, ale z Twojej strony to jedno polecenie.

NOWA SEKCJA "Co to jest błąd w programie":
[[blad-w-programie|Błąd w programie]] to każde miejsce, w którym program robi coś innego, niż chciał jego autor. Albo zatrzymuje się z komunikatem, albo działa do końca i podaje zły wynik.

Pierwszy rodzaj widać od razu. Python czyta plik od góry i gdy trafi na coś, czego nie rozumie, przerywa pracę i wypisuje komunikat. Tak jest, gdy literówka zmieni `print` w `prnt`: interpreter nie zna takiego słowa. To jeszcze nie katastrofa, bo komunikat wskazuje linię i powód.

Drugi rodzaj jest podstępniejszy, bo nic nie ostrzega. Zobacz, co zrobi program z pozoru poprawny:

```python
# poza kanonem: błąd w dzieleniu
print("Wspólna Kasa")
print(300 / 2)   # 300 zł na troje osób
```

```text
Wspólna Kasa
150.0
```

Python wykonał każdą instrukcję zgodnie z zapisem, tylko że zapis był zły: na troje trzeba dzielić przez 3. Komputer robi dokładnie to, co napisano, a nie to, co miało się na myśli.

Konsekwencja: błąd to normalna część pracy, nie porażka. Komunikat to podpowiedź, a brak komunikatu nie znaczy, że wynik jest dobry. Jak rozróżniać te rodzaje błędów i czytać komunikaty, omówimy osobno, w dziale o poprawianiu programów.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Pierwszy rodzaj błędu (literówka `prnt`) jest opisany, ale nie pokazany. Krótki blok text z komunikatem Pythona (np. NameError: name 'prnt' is not defined, z numerem linii) pokazałby, jak wygląda komunikat wskazujący linię i powód. Wymaga miejsca na drugi blok kodu, więc tylko sugestia.",
      "severity": "sugestia",
      "target": "Pierwszy rodzaj błędu: literówka print/prnt",
      "source": "Pierwszy rodzaj widać od razu"
    },
    {
      "kind": "konkret",
      "detail": "Zdanie 'na troje trzeba dzielić przez 3' pojawia się dopiero po wyniku. Warto dodać oczekiwany wynik (100.0), żeby czytelnik od razu zobaczył różnicę między 150.0 a 100.0. Dodatkowo komentarz w kodzie mówi 'na troje osób', a kod dzieli przez 2, co można zaznaczyć wprost.",
      "severity": "sugestia",
      "target": "Przykład z dzieleniem 300 / 2",
      "source": "print(300 / 2)   # 300 zł na troje osób"
    }
  ]
}
````
