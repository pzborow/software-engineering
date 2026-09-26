# Krok 1017 · strażnik_przykład

Węzeł: `review` · dział: 9 · pytanie: 52 · próba: 1

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Naprawiamy błąd logiczny (np. dzielenie przez zero przy pustej liście), czytamy komunikaty błędów, dodajemy test_rozlicz.py, debugujemy i zapisujemy wersje w repozytorium Git.

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

sprawdz_kwote · funkcja · wspolna_kasa/rozlicz.py
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

wypisz_podsumowanie · funkcja · wspolna_kasa/rozlicz.py
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

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

wydatki.txt · plik danych · wydatki.txt
Ania;120.5
Bartek;45.5
```
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

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
- dodaj test_rozlicz.py: 
assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0

NOWA SEKCJA "Czym jest testowanie programu":
[[testowanie|Testowanie]] to systematyczne sprawdzanie programu na wielu danych, dla których z góry znasz poprawny wynik. Zamiast raz spojrzeć na ekran i uznać, że „wygląda dobrze”, zapisujesz oczekiwania i pozwalasz komputerowi je porównać.

Najprostszy test to jedno sprawdzenie małej funkcji. W Pythonie służy do tego [[assert|assert]]: instrukcja, która nic nie robi, gdy warunek jest prawdziwy, a zatrzymuje program błędem `AssertionError`, gdy jest fałszywy.

```python
def na_osobe(suma, osoby):
    return suma / osoby

assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0
assert na_osobe(100, 4) == 25
print("Wszystkie testy przeszły")
```

```text
Wszystkie testy przeszły
```

Cisza po `assert` znaczy „zgadza się”. Gdyby ktoś zmienił dzielenie tak, że wynik byłby zły, jak przy błędzie z niewłaściwym dzielnikiem, pierwszy test zatrzymałby program i wskazał linię, w której oczekiwanie przestało być prawdą.

Dobre testy obejmują zwykłe dane i przypadki brzegowe, np. pustą listę wydatków. Kosztują chwilę, a po każdej zmianie kodu uruchamiasz je jednym poleceniem i wiesz, czy niczego nie zepsułeś.

Test nie dowodzi, że błędów nie ma, tylko że w sprawdzonych przypadkach ich nie ma. Gdy test się wywali, szukanie przyczyny omówimy przy debugowaniu.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "spójność",
      "target": "test_rozlicz.py",
      "detail": "Autor zadeklarował dodanie test_rozlicz.py z dwoma asercjami (78/3 i 0/4). Blok w sekcji ma trzy asercje (dodatkowo na_osobe(100, 4) == 25) oraz print i nie mówi, że to zawartość test_rozlicz.py. Wpisz nazwę pliku w komentarzu na początku bloku i zrównaj zawartość z deklaracją albo zaktualizuj deklarację. Dopisz też, że definicja na_osobe jest tu tylko skrótem (w rzeczywistości byłby import z funkcje.py).",
      "severity": "sugestia",
      "source": "canon_changes"
    },
    {
      "kind": "spójność",
      "target": "pusta lista wydatków",
      "detail": "Tekst wymienia „pustą listę wydatków” jako przypadek brzegowy, ale test na_osobe(0, 4) == 0 sprawdza sumę równą 0, a nie pustą listę. Przypadek z wątku, czyli dzielenie przez zero (osoby = 0), nie jest pokazany. Zmień przykład na suma_wydatkow([]) == 0 albo opisz na_osobe(0, 4) jako „sumę zero”.",
      "severity": "sugestia",
      "source": "tekst sekcji"
    }
  ]
}
````
