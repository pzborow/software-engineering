# Krok 0682 · strażnik_przykład

Węzeł: `review` · dział: 6 · pytanie: 37 · próba: 1

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Pojedyncze zmienne zastępuje lista wydatków i lista osób; pętla for sumuje kwoty i liczy saldo każdego uczestnika, a pętla nieskończona pojawia się jako ostrzeżenie.

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

NOWA SEKCJA "Pętla po elementach listy":
Przez wszystkie elementy [[lista-danych|listy]] przechodzisz [[petla|pętlą]] `for`: `for imie in osoby:` bierze po kolei każdy [[element-listy|element]] i wykonuje dla niego wcięty blok.

Działa to tak: przy pierwszym przebiegu (czyli [[iteracja|iteracji]]) `imie` dostaje pierwszy element, przy drugim drugi, i tak do ostatniego. Kiedy elementy się skończą, pętla sama przestaje, a program idzie dalej, do pierwszej linii bez wcięcia. Nie liczysz indeksów ani nie sprawdzasz długości listy.

```python
osoby = ["Ania", "Bartek", "Celina"]
for imie in osoby:
    print(imie)
print("Koniec")
```

```text
Ania
Bartek
Celina
Koniec
```

Elementy przychodzą w kolejności listy, więc „Ania" jest pierwsza, tak jak w sekcji o liście. Dodasz czwartą osobę, a ta sama pętla obsłuży ją bez zmiany kodu.

Nazwa `imie` jest zwykłą zmienną: po pętli zachowuje wartość ostatniego elementu. Wybierz ją tak, by mówiła, co jest na liście, a nie „x".

Pętla może też coś zbierać, np. dodawać kolejne kwoty do sumy. Tak robi Twój `kasa.py`: wypisuje każdą kwotę, sumuje je i dopiero po pętli pokazuje wynik.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "target": "kasa.py",
      "detail": "Tekst mówi o pliku „Twój `kasa.py`”, a w kanonie skrypt główny nazywa się `rozlicz.py` (repozytorium wspolna_kasa). Nazwa pliku jest niezgodna z kanonem i niezadeklarowana. Zamień na `rozlicz.py`. Dodatkowo nic w kanonie nie pokazuje, by rozlicz.py wypisywał każdą kwotę i sumował – lepiej opisać to na liście `wydatki` (np. `for wydatek in wydatki: suma += wydatek[\"kwota\"]`).",
      "severity": "blokująca",
      "source": "Pętla po elementach listy, ostatni akapit"
    },
    {
      "kind": "przykład",
      "target": "pętla zbierająca sumę",
      "detail": "Sekcja zapowiada w ostatnim akapicie pętlę sumującą kwoty, ale nie pokazuje jej kodu. To główny motyw działu (pętla for sumuje kwoty z listy wydatków), a przykład w sekcji używa tylko `print(imie)`. Dodaj krótki blok z `wydatki` i sumowaniem kwot albo usuń zapowiedź.",
      "severity": "sugestia",
      "source": "ostatni akapit",
      "status": "nowa"
    }
  ]
}
````
