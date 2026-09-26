# Krok 0541 · strażnik_przykład

Węzeł: `review` · dział: 5 · pytanie: 30 · próba: 1

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

NOWA SEKCJA "Część „w przeciwnym razie”":
Część `else`, czyli „w przeciwnym razie”, wykonuje swoje linie wtedy, gdy warunek z `if` jest fałszywy. Dzięki niej program zawsze wybiera jedną z dwóch dróg, a nie tylko „robi coś albo nic”.

Zapisujemy ją pod blokiem `if`, na tym samym poziomie [[wciecie|wcięcia]] co samo `if`, z dwukropkiem po słowie `else`. Sama nie ma warunku: nie pyta o nic, bo obejmuje wszystko, czego `if` nie złapało. Jej własne linie też wcinamy o cztery spacje.

```python
kwota = 45.5
if kwota > 100:
    print("Bardzo duża kwota")
else:
    print("Zwykła kwota")
print("Koniec")
```

```text
Zwykła kwota
Koniec
```

Warunek `kwota > 100` jest fałszywy, więc Python pominął pierwszy wcięty blok i wykonał ten pod `else`. Gdyby kwota wynosiła 150, wypisałoby się tylko „Bardzo duża kwota”. Oba bloki nigdy nie wykonają się naraz. Ostatni `print` nie ma wcięcia, więc, jak w poprzedniej sekcji, działa zawsze.

Dla „Wspólnej Kasy” to ważne: program może teraz w każdym przypadku powiedzieć coś sensownego, osobno o dużej i zwykłej kwocie. Sprawdzanie kilku warunków naraz, czyli „i” oraz „lub”, pokażemy w następnej sekcji.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "spójność",
      "target": "kwota",
      "detail": "Kod używa `kwota = 45.5` zgodnie z kanonem, bez konfliktów. Drobna sugestia: dział dotyczy ustalenia, czy ktoś jest winien pieniądze, czy ma dostać zwrot. Przykład z „dużą/zwykłą kwotą” jest tylko luźno związany z wątkiem. Można w przyszłości pokazać `else` na rozróżnieniu „winien” / „dostaje zwrot”, np. na zmiennej salda.",
      "severity": "sugestia",
      "source": "kod przykładu",
      "status": "nowa"
    }
  ]
}
````
