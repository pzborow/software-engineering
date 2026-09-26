# Krok 0734 · strażnik_przykład

Węzeł: `review` · dział: 7 · pytanie: 39 · próba: 1

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

suma · zmienna (liczba) · wspolna_kasa/rozlicz.py
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
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
- dodaj suma_wydatkow: 
def suma_wydatkow(wydatki):
    suma = 0
    for wydatek in wydatki:
        suma = suma + wydatek["kwota"]
    return suma
- dodaj udzial_na_osobe: 
def udzial_na_osobe(wydatki, liczba_osob):
    return suma_wydatkow(wydatki) / liczba_osob

NOWA SEKCJA "Po co dzielić program na funkcje":
Dzielisz program na funkcje, żeby każdy jego kawałek miał nazwę, robił jedną rzecz i istniał w jednym miejscu. Dzięki temu program czytasz jak listę zadań, a poprawkę robisz raz, nie w pięciu kopiach.

Zobacz to na „Wspólnej Kasie”. Sumę wydatków wydzieliliśmy już do funkcji, a teraz dokładamy drugą, która z niej korzysta:

```python
def suma_wydatkow(wydatki):
    suma = 0
    for wydatek in wydatki:
        suma = suma + wydatek["kwota"]
    return suma

def udzial_na_osobe(wydatki, liczba_osob):
    return suma_wydatkow(wydatki) / liczba_osob

mazury = [{"kto": "Ania", "kwota": 120.5}, {"kto": "Bartek", "kwota": 79.5}]
tatry = [{"kto": "Celina", "kwota": 450}]
print(udzial_na_osobe(mazury, 2))
print(udzial_na_osobe(tatry, 3))
```

```text
100.0
150.0
```

Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz. Gdyby liczenie sumy trzeba było kiedyś zmienić, poprawiasz jedną funkcję, a oba wyniki będą poprawne.

Druga korzyść to czytelność: `udzial_na_osobe(mazury, 2)` mówi, co się dzieje, bez zaglądania w pętlę. Trzecia to sprawdzanie: małą funkcję z jasnym wejściem i wynikiem łatwo przetestować osobno, do czego wrócimy przy testowaniu programu.

U siebie masz już `funkcje.py` z jedną funkcją. Za chwilę dopiszesz drugą i użyjesz obu dla dwóch wyjazdów.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "target": "funkcje.py",
      "detail": "Ostatni akapit mówi o pliku `funkcje.py`, którego nie ma w kanonie ani wśród zmian autora. Program „Wspólnej Kasy” jest w `wspolna_kasa/rozlicz.py`. Zmień na `rozlicz.py` albo zadeklaruj nowy plik z powodem. Zdanie „masz już … z jedną funkcją” też nie pasuje do kanonu, bo w `rozlicz.py` jest na razie tylko pętla z `suma`. Lepiej napisać, że sumę z pętli zamieniasz teraz w funkcję.",
      "severity": "blokująca",
      "source": "kanon: rozlicz.py",
      "status": "nowa"
    },
    {
      "kind": "spójność",
      "target": "suma_wydatkow",
      "detail": "Tekst mówi „Sumę wydatków wydzieliliśmy już do funkcji”, a `suma_wydatkow` jest w tej sekcji dodawana po raz pierwszy (kanon pokazuje tylko pętlę z `suma`). Przeformułuj, np. „Pętlę z `suma` zapisujemy jako funkcję `suma_wydatkow`”.",
      "severity": "sugestia",
      "source": "",
      "status": "nowa"
    },
    {
      "kind": "spójność",
      "target": "mazury, tatry",
      "detail": "Zmienne `mazury` i `tatry` to nowe nazwy poza kanonem i nie zostały zadeklarowane. Zadeklaruj je jako „dodaj” albo zaznacz, że to dane przykładowe tylko do tej sekcji. Kanoniczna lista to `wydatki`, więc można też użyć jej dla jednego wyjazdu. Wpisy nie mają klucza `opis` z kanonu (`{\"kto\", \"opis\", \"kwota\"}`), co jest tylko drobną różnicą.",
      "severity": "sugestia",
      "source": "",
      "status": "nowa"
    }
  ]
}
````
