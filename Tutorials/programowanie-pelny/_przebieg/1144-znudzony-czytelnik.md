# Krok 1144 · znudzony_czytelnik

Węzeł: `review` · dział: 10 · pytanie: 59 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jakie umiejętności poza kodowaniem przydają się programiście?".

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
## Od pomysłu do działającego programu
Od pomysłu do programu dochodzi się małymi krokami: opisujesz zadanie zwykłymi słowami, piszesz najmniejszy kawałek, który coś robi, sprawdzasz go i dopiero wtedy dokładasz następny. Cały program naraz zwykle nie działa, a szukanie błędu w stu liniach jest męczące.

```text
pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit
              ↑                                                            |
              └──────────────────── następny kawałek ←─────────────────────┘
```

Weźmy pomysł: „chcę wiedzieć, kto komu ile jest winien”. Opis krokowy to rozbicie zadania na kroki, z których każdy da się zrobić osobno: dla każdej osoby zsumuj to, co zapłaciła, odejmij jej równy udział i wypisz wynik. Z tego wychodzi jedna mała [[funkcja]]:

```python
def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...
```

Funkcję sprawdzasz na danych, których wynik znasz z kartki. Dopiero gdy się zgadza, zapisujesz [[commit]] (zapisaną wersję kodu z opisem) i myślisz o kolejnym kawałku, np. wczytaniu wydatków z pliku.

Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, jak w sekcji o zapisywaniu wersji kodu. Dzięki temu nie zgadujesz, gdzie szukać błędu.

NOWA SEKCJA "Umiejętności poza kodowaniem":
Poza samym pisaniem kodu programiście przydaje się przede wszystkim rozumienie problemu, jasne komunikowanie się i umiejętność uczenia się. Kod jest jednym z etapów pracy, a dużo czasu schodzi na to, co dzieje się przed nim i po nim.

| Umiejętność | Do czego służy | Przykład we Wspólnej Kasie |
|---|---|---|
| Rozumienie problemu | ustalenie, co program ma zrobić | „Kto komu ile jest winien?” zamiast „policz sumę” |
| Komunikacja | pytania, opisy zmian | pytanie, czy dzielimy po równo |
| Cierpliwość w szukaniu błędów | spokojne zawężanie przyczyny | sprawdzanie wartości wypisanych przez [[print]] |
| Szukanie informacji | radzenie sobie z nowym | szukanie po ostatniej linii komunikatu |
| Dokładność | pilnowanie szczegółów | kwota z kropką, nie z przecinkiem |

Rozumienie problemu oznacza rozmowę z osobą, dla której powstaje program. Zanim napiszesz [[funkcja|funkcję]], musisz wiedzieć, czy znajomi dzielą rachunek po równo i co ma się stać, gdy ktoś nie płaci. Błędne założenie kosztuje więcej niż literówka.

Komunikacja to także pisanie: czytelne nazwy, komentarze i opisy [[commit|commitów]] są wiadomością dla Ciebie za miesiąc i dla innych osób. Do tego dochodzi cierpliwość, bo błąd rzadko ustępuje od razu, oraz nawyk sprawdzania własnej pracy.

Żadna z tych umiejętności nie wymaga wiedzy technicznej, więc część z nich masz już z pracy i życia. Warto je ćwiczyć razem z kodowaniem.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Wiersze „Szukanie informacji” i „Dokładność” są w tabeli szczątkowe i nie wracają w prozie. „Szukanie po ostatniej linii komunikatu” to zagadka dla osoby spoza IT (jaki komunikat? po co ostatnia linia?). Kwota „z kropką, nie z przecinkiem” nie mówi, dlaczego to ma znaczenie. Wystarczy jedno zdanie z przykładem, np. program zgłasza błąd, a jego ostatnia linia nazywa problem i można ją wpisać w wyszukiwarkę.",
      "target": "tabela: Szukanie informacji, Dokładność",
      "severity": "sugestia"
    }
  ]
}
````
