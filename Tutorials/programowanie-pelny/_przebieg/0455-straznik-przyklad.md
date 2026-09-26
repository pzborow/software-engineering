# Krok 0455 · strażnik_przykład

Węzeł: `review` · dział: 5 · pytanie: 26 · próba: 1

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Program liczy udział jednej osoby, skleja tekst podsumowania i decyduje if/else oraz operatorami and/or, czy ktoś jest winien pieniądze, czy ma dostać zwrot.

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

kwota_stara · zmienna (liczba) · wspolna_kasa/rozlicz.py
kwota_stara = kwota
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

NOWA SEKCJA "Działania matematyczne w programie":
Program wykonuje te same działania co kalkulator: dodawanie, odejmowanie, mnożenie i dzielenie, a do tego dzielenie całkowite, resztę z dzielenia i potęgowanie. Zapisujesz je za pomocą [[operator-arytmetyczny|operatorów arytmetycznych]], czyli znaków, które mówią Pythonowi, jakie działanie wykonać na liczbach.

| Działanie | Operator |
|---|---|
| dodawanie | `+` |
| odejmowanie | `-` |
| mnożenie | `*` |
| dzielenie | `/` |
| dzielenie całkowite | `//` |
| reszta z dzielenia | `%` |
| potęgowanie | `**` |

Mnożenie to gwiazdka, a nie „x”. Dzielenie `/` zawsze daje liczbę z częścią ułamkową. Dzielenie całkowite `//` zostawia samą część całkowitą, a `%` pokazuje, ile zostało. Przy dzieleniu kwoty między osoby to bardzo przydatne.

```python
kwota = 100
print(kwota + 20)
print(kwota - 20)
print(kwota * 2)
print(kwota / 3)
print(kwota // 3)
print(kwota % 3)
print(kwota ** 2)
```

```text
120
80
200
33.333333333333336
33
1
10000
```

Zwróć uwagę na wynik `33.333333333333336`. Komputer trzyma ułamki w przybliżeniu, więc na końcu bywa drobna nieścisłość. Kolejność działań jest jak w szkole: mnożenie i dzielenie przed dodawaniem, a nawiasy zmieniają porządek.

Konsekwencja: działania mają sens tylko na liczbach. Tekstu w rodzaju `"Ania"` nie podzielisz, co widzieliśmy przy typach danych.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "fakt",
      "severity": "blokująca",
      "target": "Konsekwencja: działania mają sens tylko na liczbach",
      "detail": "Twierdzenie jest nieprawdziwe w tej ogólności. W Pythonie `+` skleja teksty (`\"Ania\" + \"Bartek\"`), a `*` powtarza tekst (`\"Ania\" * 2`). Ten dział właśnie uczy sklejania tekstu podsumowania, więc czytelnik wyniósłby błędne przekonanie. Popraw np.: „Dzielenia, odejmowania i potęgowania nie da się zastosować do tekstu (`\"Ania\" / 3` to błąd). `+` i `*` działają na tekście inaczej niż na liczbach: sklejają i powtarzają.”",
      "source": "Konsekwencja: działania mają sens tylko na liczbach. Tekstu w rodzaju `\"Ania\"` nie podzielisz"
    },
    {
      "kind": "spójność",
      "severity": "sugestia",
      "target": "kwota",
      "detail": "Kanon deklaruje `kwota = 45.5` (liczba zmiennoprzecinkowa), a przykład nadaje `kwota = 100` (int). Typ „liczba” się zgadza, więc to nie sprzeczność. Zaznacz jednak w tekście, że to nowa wartość, np. „załóżmy, że wydatek wyniósł 100 zł”, i najlepiej wiąż przykład z wątkiem: dzielenie 100 zł na 3 osoby (`osoby` z kanonu)."
    },
    {
      "kind": "spójność",
      "severity": "sugestia",
      "target": "wątek Wspólna Kasa",
      "detail": "Sekcja prawie nie korzysta z wątku. Wspomina tylko dzielenie kwoty między osoby, ale bez kodu. Dodaj krótki przykład, w którym `//` i `%` liczą, ile pełnych złotych przypada na osobę i ile zostaje, np. `kwota // len(osoby)` i `kwota % len(osoby)`. Wszystko na nazwach z kanonu, więc canon_changes nie jest potrzebne."
    }
  ]
}
````
