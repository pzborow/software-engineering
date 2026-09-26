# Krok 0489 · strażnik_przykład

Węzeł: `review` · dział: 5 · pytanie: 27 · próba: 2

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

NOWA SEKCJA "Łączenie tekstów":
Program łączy teksty operatorem `+`, który skleja je w jeden, dokładnie w takiej kolejności i z takimi znakami, jakie mu podasz. Ta operacja nazywa się [[konkatenacja|sklejaniem tekstów]] (konkatenacją). Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono.

Python niczego nie dopowiada. Nie doda spacji ani przecinka, więc odstępy musisz wstawić sam, jako część tekstu w cudzysłowie:

```python
imie = "Ania"
kwota = 45.5
print(imie + " zapłaciła " + str(kwota) + " zł")
print(imie + "zapłaciła")
```

```text
Ania zapłaciła 45.5 zł
Aniazapłaciła
```

W drugiej linii zabrakło spacji, więc słowa się zlepiły.

Sklejać można tylko tekst z tekstem. Zapis `"Kwota: " + kwota` zatrzyma program błędem `TypeError`, bo liczby 45.5 nie da się dokleić do napisu. Zamienia ją na tekst funkcja `str()`: `str(kwota)` daje `"45.5"`. Nie zmienia to samej zmiennej `kwota`, która dalej jest liczbą.

Wygodniejszy bywa zapis z literą `f` przed cudzysłowem: `f"{imie} zapłaciła {kwota} zł"`. Nazwy w nawiasach klamrowych Python podmienia na wartości, także liczbowe.

Ten błąd możesz wywołać od razu: w warsztacie poniżej dopisujesz do swojego skryptu linię, która skleja tekst z liczbą.

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [spójność] kasa.py: Tekst odsyła do pliku `kasa.py`, a w kanonie plik programu (skrypt główny) nazywa się `rozlicz.py` (w katalogu wspolna_kasa). Nie ma zadeklarowanej zmiany nazwy. Popraw na `rozlicz.py`.
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
