# Krok 0935 · znudzony_czytelnik

Węzeł: `review` · dział: 8 · pytanie: 48 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym jest interfejs użytkownika?".

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
## Czym jest plik
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

NOWA SEKCJA "Czym jest interfejs użytkownika":
[[interfejs-uzytkownika|Interfejs użytkownika]] to część programu, przez którą człowiek się z nim komunikuje: to, co program wyświetla, oraz sposób, w jaki przyjmuje od człowieka dane i polecenia. Użytkownik nie widzi kodu, widzi tylko interfejs.

Interfejs bywa różny. W [[interfejs-tekstowy|interfejsie tekstowym]], czyli takim, który działa w [[terminal|terminalu]] na samych napisach, program zadaje pytania, a Ty odpisujesz z klawiatury. W interfejsie graficznym są okna i przyciski. Nasza „Wspólna Kasa” zostaje przy wersji tekstowej, bo wystarczą do niej dwie znane już rzeczy: [[input|input]] do pytań i [[print|print]] do wyników.

Interfejs ma dwie strony: **wejście** (pytania, odpowiedzi) i **wyjście** (wyniki, komunikaty). To dokładnie [[dane-wejsciowe|dane wejściowe]] i [[dane-wyjsciowe|dane wyjściowe]], tylko widziane oczami człowieka. Stąd wniosek z wcześniejszych sekcji: suchy wynik nic nie mówi komuś, kto nie zna kodu, więc trzeba go opisać.

```python
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```

```text
=== Wspólna Kasa ===
Ania: 120.5 zł
Bartek: 45.5 zł
```

Konsekwencja: pytanie w rodzaju „Ile zapłacił? ” i czytelne podsumowanie to nie ozdoby, tylko część działania programu. Interfejs trzeba więc projektować, a człowiek po drugiej stronie potrafi wpisać coś nieoczekiwanego.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Kod pokazuje tylko wyjście (print). Strona wejściowa, czyli pytanie i odpowiedź człowieka, jest tylko opisana. Wystarczyłby krótki blok text z rozmową, np. „Kto płacił? Ania / Ile zapłacił? 120.5”, zamiast jednego z opisów.",
      "severity": "sugestia",
      "target": "wejście interfejsu (input)",
      "source": "akapit o dwóch stronach interfejsu"
    }
  ]
}
````
