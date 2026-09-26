# Krok 0565 · strażnik_przykład

Węzeł: `review` · dział: 5 · pytanie: 31 · próba: 2

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
- dodaj liczba_osob: 
liczba_osob = 3

NOWA SEKCJA "Operatory „i” oraz „lub”":
[[operator-logiczny|Operatory logiczne]] `and` („i”) oraz `or` („lub”) łączą kilka warunków w jeden. Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: `True` albo `False`.

`and` daje `True` tylko wtedy, gdy prawdziwe są **oba** warunki. `or` daje `True`, gdy prawdziwy jest **którykolwiek** z nich, a `False` dopiero wtedy, gdy oba są fałszywe.

| Lewy warunek | Prawy warunek | `and` | `or` |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

Każdy z połączonych warunków zapisujemy w całości, tak jak w porównywaniu wartości. Wynik można wypisać albo wstawić do `if`:

```python
kwota = 45.5
liczba_osob = 3
print(kwota > 40 and liczba_osob > 5)
print(kwota > 100 or liczba_osob == 3)
if kwota > 100 or liczba_osob > 5:
    print("Duża kwota")
else:
    print("Zwykła kwota")
```

```text
False
True
Zwykła kwota
```

W pierwszej linii drugi warunek zawiódł, więc `and` dało `False`. W drugiej wystarczył prawdziwy drugi warunek, więc `or` dało `True`. W `if` oba są fałszywe, więc zadziałało `else`.

Dla „Wspólnej Kasy” to znaczy, że kwotę można uznać za dużą, gdy jest wysoka **lub** dzieli ją dużo osób. U siebie w `kasa.py` dopisz te linie w warsztacie poniżej.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "target": "kasa.py",
      "detail": "Tekst każe dopisać kod w `kasa.py`, a w kanonie plik programu to `rozlicz.py` (wspolna_kasa/rozlicz.py). Nazwa pliku nie została zadeklarowana jako zmiana. Zamień `kasa.py` na `rozlicz.py`.",
      "severity": "blokująca",
      "source": "Dla „Wspólnej Kasy” ... U siebie w `kasa.py` dopisz te linie",
      "status": "nowa"
    }
  ]
}
````
