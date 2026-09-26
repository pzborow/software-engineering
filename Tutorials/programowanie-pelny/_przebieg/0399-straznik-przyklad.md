# Krok 0399 · strażnik_przykład

Węzeł: `review` · dział: 4 · pytanie: 23 · próba: 1

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Do rozlicz.py trafiają zmienne: imię, opis i kwota pojedynczego wydatku, różnica między tekstem a liczbą oraz wartość logiczna „czy zapłacono”.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
rozlicz.py · plik programu (skrypt główny) · rozlicz.py
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)

osoby · zmienna (lista tekstów) · wspolna_kasa/rozlicz.py
osoby = ["Ania", "Bartek", "Celina"]

imie · zmienna (tekst) · wspolna_kasa/rozlicz.py
imie = "Ania"

kwota · zmienna (liczba) · wspolna_kasa/rozlicz.py
kwota = 45.5

zaplacono · zmienna (prawda/fałsz) · wspolna_kasa/rozlicz.py
zaplacono = True
```
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), wydatki (zmienna (lista słowników)), suma_wydatkow (funkcja), udzial_na_osobe (funkcja), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), zapytaj_o_wydatek (funkcja), sprawdz_kwote (funkcja), wypisz_podsumowanie (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

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

NOWA SEKCJA "Czym jest typ danych":
[[typ-danych|Typ danych]] to rodzaj wartości, który mówi Pythonowi, czym ta wartość jest i jakie działania są na niej dozwolone. Wcześniej pisaliśmy po prostu „rodzaj danych”, teraz mamy na to fachową nazwę.

Typ ma każda wartość, także ta ukryta w zmiennej. Python rozpoznaje go po zapisie: cudzysłów oznacza tekst, cyfry z kropką ułamek, a `True` lub `False` prawdę albo fałsz. Dlatego `"45.5"` to [[cztery znaki zamiast kwoty|tylko cztery znaki: 4, 5, kropka, 5]], a nie pieniądze. Typ sprawdzisz funkcją `type()`.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(type(imie))
print(type(kwota))
print(type(zaplacono))
```

```text
<class 'str'>
<class 'float'>
<class 'bool'>
```

Słowo `class` na razie pomiń, ważna jest nazwa po nim. Oto podstawowe typy Pythona:

| Nazwa w Pythonie | Co to jest | Przykład |
|---|---|---|
| `str` | tekst | `"Ania"` |
| `int` | liczba całkowita | `3` |
| `float` | liczba z ułamkiem | `45.5` |
| `bool` | prawda lub fałsz | `True` |

Typ decyduje o tym, co program może zrobić z wartością. Dlatego [[imienia nie da się podzielić|imienia nie podzielisz przez 2]], a kwotę tak. Typem `bool` zajmiemy się osobno, w kolejnej sekcji.

Konsekwencja: gdy program zachowuje się dziwnie, jedno z pierwszych pytań brzmi „jakiego typu jest ta wartość?”.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Teza, że typ decyduje o dozwolonych działaniach (imienia nie podzielisz przez 2, kwotę tak), jest podana tylko słowami. Warto dodać krótki blok, np. `print(kwota / 2)` i `print(imie / 2)` z komunikatem TypeError, oznaczony pierwszą linią „# poza kanonem” dla błędnej linii. Tekst jest zrozumiały bez tego, więc to tylko sugestia.",
      "severity": "sugestia",
      "target": "Typ decyduje o tym, co program może zrobić z wartością"
    }
  ]
}
````
