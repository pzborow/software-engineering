# Krok 0782 · strażnik_przykład

Węzeł: `review` · dział: 7 · pytanie: 41 · próba: 1

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Kod dzieli się na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby z czytelnymi nazwami, argumentami i zwracanymi wynikami, gotowe do ponownego użycia.

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
```
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), suma_wydatkow (funkcja), udzial_na_osobe (funkcja), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), zapytaj_o_wydatek (funkcja), sprawdz_kwote (funkcja), wypisz_podsumowanie (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

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
(brak)

NOWA SEKCJA "Zwracanie wyniku przez funkcję":
Funkcja zwraca wynik, gdy instrukcją `return` oddaje wartość temu, kto ją wywołał. Wywołanie funkcji staje się wtedy w kodzie tą wartością, więc możesz ją zapisać do zmiennej albo przekazać dalej.

Po `return` funkcja od razu kończy pracę. Nic, co stoi pod nim w ciele funkcji, już się nie wykona.

Zwracanie to nie to samo co wypisywanie. `print` tylko pokazuje tekst na ekranie, a program nie dostaje z niego nic do dalszej pracy. Funkcja bez `return` oddaje specjalną wartość `None`, czyli „nic”.

```python
def na_osobe(suma, osoby):
    return suma / osoby

def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

a = na_osobe(300, 4)
b = wypisz_na_osobe(300, 4)
print(a)
print(b)
```

```text
75.0
75.0
None
```

Pierwsza `75.0` pochodzi z `print` wewnątrz `wypisz_na_osobe`, w chwili wywołania. Druga to `a`, czyli wynik zwrócony i zapisany. Zmienna `b` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła.

Konsekwencja jest praktyczna: tylko zwrócony wynik da się wykorzystać dalej. Dlatego `na_osobe(suma(mazury), 3)` działa: wynik jednej funkcji trafia jako argument do drugiej.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "target": "wypisz_na_osobe",
      "detail": "Nowa funkcja pojawia się w kodzie bez deklaracji w canon_changes (module=\"przykład\", „dodaj”, pełna deklaracja: funkcja, plik, argumenty suma i osoby, brak return). Zadeklaruj ją albo zrób z niej kontrprzykład i oznacz pierwszą linią bloku „# poza kanonem”. Zmienne a i b są tu tylko przykładem, ale też warto je nazwać jako lokalne dla ilustracji.",
      "severity": "blokująca",
      "source": "kod",
      "status": "nowa"
    },
    {
      "kind": "spójność",
      "target": "mazury",
      "detail": "W ostatnim zdaniu `suma(mazury)` używa nazwy spoza kanonu, niezdefiniowanej i sugerującej obcą dziedzinę (wyjazd). Zastąp ją kanonicznym `wydatki` albo listą kwot, tak by pasowało do `suma(wydatki)` z kanonu. Lepiej pokazać to też w kodzie, nie tylko w prozie.",
      "severity": "sugestia",
      "source": "tekst",
      "status": "nowa"
    },
    {
      "kind": "spójność",
      "target": "na_osobe",
      "detail": "Przykład używa 300 i 4, a wątek ma 300 / 3 i liczba_osob = 3. Rozważ `na_osobe(300, 3)` (wynik 100.0) lub przekazanie `liczba_osob`, by trzymać się Wspólnej Kasy. Dział zapowiada też suma_wydatkow i udzial_na_osobe; można zaznaczyć, że to kolejny krok.",
      "severity": "sugestia",
      "source": "kod",
      "status": "nowa"
    }
  ]
}
````
