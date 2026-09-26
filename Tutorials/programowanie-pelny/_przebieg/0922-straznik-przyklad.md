# Krok 0922 · strażnik_przykład

Węzeł: `review` · dział: 8 · pytanie: 47 · próba: 2

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Program wczytuje wydatki z pliku wydatki.csv, pyta użytkownika o nowy wydatek przez zapytaj_o_wydatek, waliduje kwotę w sprawdz_kwote i drukuje wynik jako prosty interfejs tekstowy.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
rozlicz.py · plik programu (skrypt główny) · rozlicz.py
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)

wydatki · zmienna (lista słowników) · wspolna_kasa/rozlicz.py
wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.50}]

osoby · zmienna (lista tekstów) · wspolna_kasa/rozlicz.py
osoby = ["Ania", "Bartek", "Celina"]

suma_wydatkow · funkcja · funkcje.py
def suma_wydatkow(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

udzial_na_osobe · funkcja · funkcje.py
def udzial_na_osobe(suma, liczba_osob):
    return suma / liczba_osob

zapytaj_o_wydatek · funkcja · wspolna_kasa/rozlicz.py
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    kwota = float(kwota)
    ...

imie · zmienna (tekst) · wspolna_kasa/rozlicz.py
for imie in osoby:

kwota · zmienna (liczba) · wspolna_kasa/rozlicz.py
kwota = 45.5

zaplacono · zmienna (prawda/fałsz) · wspolna_kasa/rozlicz.py
zaplacono = True

kwota_stara · zmienna (liczba) · wspolna_kasa/rozlicz.py
kwota_stara = kwota

liczba_osob · zmienna (liczba) · wspolna_kasa/rozlicz.py
liczba_osob = 3

wydatek · zmienna (słownik) · wspolna_kasa/rozlicz.py
for wydatek in wydatki:

suma · zmienna (liczba) · funkcje.py
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

na_osobe · funkcja · funkcje.py
def na_osobe(suma, osoby):
    return suma / osoby

wypisz_na_osobe · funkcja · funkcje.py
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)
```
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), sprawdz_kwote (funkcja), wypisz_podsumowanie (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

Zasady wątku:
- Kod w sekcji używa elementów kanonu z dokładnie tymi nazwami i deklaracjami.
- Każdy nowy element i każdą zmianę deklaracji zadeklaruj w canon_changes z module="przykład" (dodaj/zmień + reason).
  Zaplanowany element przy pierwszym użyciu deklaruj jako "dodaj" z pełną deklaracją.
- Temat pytania ma pierwszeństwo przed wątkiem. Kontrprzykład ("źle: ...") albo porównanie spoza wątku
  oznacz pierwszą linią bloku: komentarz „poza kanonem”.

Sprawdź kod w nowej sekcji (pomiń bloki text i bloki oznaczone „poza kanonem”):
- czy nazwy i deklaracje zgadzają się z kanonem albo ze zmianami zadeklarowanymi przez autora,
- czy zachowanie nie przeczy kanonowi (np. inny typ wyniku, inne argumenty, inna nazwa zasobu lub gałęzi),
- czy sekcja trzyma się wątku, zamiast wprowadzać obcą dziedzinę bez oznaczenia.
Kod jest szkicem: `...` zamiast ciała, pominięte importy, konstruktory i argumenty NIE są problemem, o ile czytelnik
rozumie z tekstu, co się dzieje. Nie żądaj implementacji.
Każdy problem zgłoś jako kind="spójność", target=nazwa elementu, detail=co się nie zgadza i jak to poprawić.
Niezadeklarowana sprzeczność z kanonem jest blokująca; drobne różnice (np. nazwa parametru) to sugestia.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

ZMIANY ZADEKLAROWANE PRZEZ AUTORA:
- dodaj wydatki.txt: 
Ania;120.5
Bartek;45.5

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
      "kind": "spójność",
      "target": "wydatki.txt",
      "detail": "Wątek zakłada plik danych wydatki.csv, który program wczytuje w tym dziale. Sekcja i zadeklarowana zmiana wprowadzają wydatki.txt z separatorem ';' i bez pola opis (kanon: kto, opis, kwota). Zmiana jest zadeklarowana, więc to nie sprzeczność, ale czytelnik może się pogubić, gdy później pojawi się wydatki.csv. Rozważ użycie od razu wydatki.csv, np. 'Ania,zakupy,120.5', albo dodaj jedno zdanie, że .txt służy tu tylko do ćwiczenia, a docelowy plik to wydatki.csv.",
      "severity": "sugestia",
      "source": "kanon: wydatki.csv (zaplanowany)",
      "status": "nowa"
    }
  ]
}
````
