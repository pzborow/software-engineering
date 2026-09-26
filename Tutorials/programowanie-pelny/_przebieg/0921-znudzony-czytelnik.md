# Krok 0921 · znudzony_czytelnik

Węzeł: `review` · dział: 8 · pytanie: 47 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym jest plik i jak program może z niego korzystać?".

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
## Pytanie użytkownika o informację
Program pyta użytkownika funkcją [[input|input]]: wypisuje pytanie, czeka, aż ktoś wpisze odpowiedź i naciśnie Enter, a potem oddaje tę odpowiedź jako wartość. To najprostszy sposób, by [[dane-wejsciowe|dane wejściowe]] przyszły od człowieka.

Tekst w nawiasach to pytanie, które zobaczy użytkownik. Wynik `input` przypisujesz do zmiennej, jak każdą [[wartosc-zwracana|wartość zwracaną]]. Program stoi w miejscu, dopóki odpowiedź nie nadejdzie.

Pokażemy to na przykładzie, który będzie nam towarzyszył: „Wspólnej Kasie”, czyli programie do rozliczania wspólnych wydatków znajomych. Zaczynamy dobudowywać do niego pytania do użytkownika, a pierwsze dotyczy nowego wydatku:

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    kwota = float(kwota)
    ...
```

Pułapka: `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Dla Pythona to wciąż „45.5” w cudzysłowie, czyli tekst, którego nie da się dzielić ani dodawać do liczb (skończyłoby się to błędem [[typeerror|TypeError]]). Dlatego `float()` zamienia tekst na liczbę. Spacja na końcu pytania oddziela je od tego, co wpisze użytkownik.

Konsekwencja: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne. Ale `float("abc")` przerwie program błędem. Jak się przed tym bronić, pokażemy przy sprawdzaniu danych wpisanych przez użytkownika.

NOWA SEKCJA "Czym jest plik":
[[plik|Plik]] to nazwana porcja danych zapisana na dysku, która istnieje także wtedy, gdy program już nie działa. Zmienne żyją tylko podczas pracy programu i znikają wraz z jego zakończeniem, a plik zostaje. Dlatego plik jest miejscem, z którego [[dane-wejsciowe|dane wejściowe]] przychodzą i do którego trafiają [[dane-wyjsciowe|dane wyjściowe]].

Program korzysta z pliku w trzech krokach: otwiera go funkcją `open`, czyta albo zapisuje, a na końcu zamyka. Blok `with` zamyka plik za Ciebie, nawet gdy coś pójdzie źle. Drugi argument `open` to [[tryb-otwarcia-pliku|tryb otwarcia]], czyli informacja, co zamierzasz z plikiem zrobić:

| Tryb | Znaczenie |
|---|---|
| `"r"` | czytanie (plik musi istnieć) |
| `"w"` | zapis od nowa, stara treść przepada |
| `"a"` | dopisywanie na końcu |

Argument `encoding="utf-8"` sprawia, że polskie litery zapiszą się i odczytają poprawnie.

```python
with open("wydatki.txt", "w", encoding="utf-8") as plik:
    plik.write("Ania;120.5\n")
    plik.write("Bartek;45.5\n")

with open("wydatki.txt", "r", encoding="utf-8") as plik:
    tekst = plik.read()
print(tekst, end="")
```

```text
Ania;120.5
Bartek;45.5
```

Uwaga: plik przechowuje wyłącznie tekst, więc kwotę po wczytaniu trzeba znów zamienić przez `float()`, bo `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Pułapką jest tryb `"w"`, który kasuje starą zawartość. Zanim ktoś wpisze do pliku coś błędnego, warto dane sprawdzić, o czym powiemy przy sprawdzaniu danych użytkownika.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "skrócenie",
      "detail": "Ostatni akapit powtarza prawie dosłownie pułapkę z poprzedniej sekcji (input zwraca tekst, nawet gdy ktoś wpisze 45.5), choć tu dane pochodzą z pliku, nie z input. Zdanie o sprawdzaniu danych też nie wnosi nic nowego. Warto zostawić tylko: z pliku wraca tekst, więc trzeba float(), oraz ostrzeżenie o trybie \"w\".",
      "severity": "sugestia",
      "target": "Ostatni akapit (Uwaga)",
      "source": "nowa sekcja"
    },
    {
      "kind": "przykład",
      "detail": "Tryby \"a\" i \"r\" są w tabeli, ale kod pokazuje tylko \"w\" i \"r\". Można w jednej linijce dodać przykład dopisania (\"a\") kolejnego wydatku, np. Celina;30.0, co pokazałoby różnicę wobec \"w\". Pamiętaj o limicie kodu.",
      "severity": "sugestia",
      "target": "Tryb \"a\" (dopisywanie)",
      "source": "nowa sekcja"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Zapis \"\\n\" w kodzie i end=\"\" w print pojawiają się bez objaśnienia. Wystarczy pół zdania: \\n oznacza koniec wiersza, a end=\"\" zapobiega dodatkowej pustej linii.",
      "severity": "sugestia",
      "target": "\\n oraz end=\"\"",
      "source": "nowa sekcja"
    }
  ]
}
````
