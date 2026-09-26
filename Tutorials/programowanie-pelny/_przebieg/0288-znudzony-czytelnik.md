# Krok 0288 · znudzony_czytelnik

Węzeł: `review` · dział: 3 · pytanie: 18 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Do czego służą komentarze w kodzie?".

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
## Co to jest błąd w programie
[[blad-w-programie|Błąd w programie]] to każde miejsce, w którym program robi coś innego, niż chciał jego autor. Albo zatrzymuje się z komunikatem, albo działa do końca i podaje zły wynik.

Pierwszy rodzaj widać od razu. Python czyta plik od góry i gdy trafi na coś, czego nie rozumie, przerywa pracę i wypisuje komunikat. Tak jest, gdy literówka zmieni [[print|print]] (polecenie, które każe programowi wypisać tekst lub liczbę na ekranie) w `prnt`: interpreter nie zna takiego słowa. To jeszcze nie katastrofa, bo komunikat wskazuje linię i powód. U siebie zobaczysz to za chwilę w `kasa.py`.

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

NOWA SEKCJA "Do czego służą komentarze":
[[komentarz|Komentarz]] to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi.

W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. [[interpreter|Interpreter]] pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją.

```python
# rozlicz.py - rozliczenie wspólnych wydatków
print("Wspólna Kasa")
print(300 / 3)  # 300 zł na troje osób: udział jednej osoby
# print(300 / 2)  <- ta linia jest wyłączona
```

```text
Wspólna Kasa
100.0
```

Ostatnia linia pokazuje drugie zastosowanie: zamiana instrukcji na komentarz „wyłącza” ją bez kasowania. Przyda się to, gdy będziesz coś sprawdzać.

Komentarz ma sens, gdy podaje powód lub kontekst („300 zł na troje osób”). Powtarzanie tego, co widać w kodzie, tylko go zaśmieca. Pamiętaj też, że komentarz może się zestarzeć: jeśli zmienisz kod, a opis zostawisz, wprowadzi czytelnika w błąd. U siebie masz już taki komentarz w pierwszej linii `kasa.py`. Za chwilę go poprawisz i sprawdzisz, że nie wpływa na wynik.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
