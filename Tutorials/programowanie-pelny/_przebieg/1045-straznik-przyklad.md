# Krok 1045 · strażnik_przykład

Węzeł: `review` · dział: 9 · pytanie: 54 · próba: 1

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

test_rozlicz.py · plik testów · test_rozlicz.py
assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0

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
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), wspolna_kasa (repozytorium Git)

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
- dodaj wspolna_kasa: 
git init -b main
git add funkcje.py test_kasa.py
git commit -m "Funkcje Wspolnej Kasy i testy"

NOWA SEKCJA "Po co zapisywać wersje kodu":
Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast pamiętać, co dokładnie zmieniłeś.

Robi to [[git|Git]], program do zapisywania historii plików. Zapis jednej wersji to [[commit|commit]]: migawka wybranych plików z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię projektu, to [[repozytorium|repozytorium]]. Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.

Wersje przydają się w trzech sytuacjach:

- Po nieudanej zmianie wracasz do ostatniej działającej wersji.
- Historia pokazuje, kiedy pojawił się błąd, co przy szukaniu przyczyny oszczędza sporo czasu.
- Możesz śmiało eksperymentować, bo stara wersja i tak jest bezpieczna.

Dobry moment na commit to chwila, gdy testy przechodzą. Opis pisz tak, żeby po miesiącu dało się z niego coś zrozumieć. Wiele małych commitów jest lepsze niż jeden wielki.

Sam zapis wygląda tak:

```text
git init -b main
git add funkcje.py test_kasa.py
git commit -m "Funkcje Wspolnej Kasy i testy"
```

`init` zakłada repozytorium, `add` wybiera pliki do zapisu, a `commit` zapisuje wersję. Wybór plików przez `add` sprawia, że do historii trafia tylko to, co chcesz. Wykonasz to u siebie w warsztacie.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "target": "test_rozlicz.py",
      "detail": "W poleceniu `git add funkcje.py test_kasa.py` pojawia się plik `test_kasa.py`, a w kanonie plik testów nazywa się `test_rozlicz.py`. Nie ma deklaracji zmiany nazwy. Zamień na `git add funkcje.py test_rozlicz.py`, a komunikat commita dostosuj do tego, co faktycznie w nim jest.",
      "severity": "blokująca",
      "source": "kod: git add",
      "status": "nowa"
    },
    {
      "kind": "spójność",
      "target": "wspolna_kasa",
      "detail": "Tekst mówi, że repozytorium „będzie to `wspolna_kasa`”, ale `git init -b main` bez argumentu zakłada repozytorium w bieżącym katalogu i nie tworzy katalogu o tej nazwie. Dodaj `git init -b main wspolna_kasa` albo `mkdir wspolna_kasa && cd wspolna_kasa` przed `init`. W kanonie `wspolna_kasa/` jest też katalogiem z `rozlicz.py`, więc warto wyjaśnić, że to ten sam katalog.",
      "severity": "blokująca",
      "source": "kod: git init",
      "status": "nowa"
    },
    {
      "kind": "spójność",
      "target": "funkcje.py",
      "detail": "W kanonie `funkcje.py` i `test_rozlicz.py` leżą w katalogu głównym, a `rozlicz.py` w `wspolna_kasa/`. Polecenie `git add` nie obejmuje `rozlicz.py`, więc główny plik programu nie trafia do historii. Ujednolić układ plików względem repozytorium albo dodać `rozlicz.py` do `add` i napisać jedno zdanie, gdzie leżą pliki.",
      "severity": "sugestia",
      "source": "kod: git add",
      "status": "nowa"
    }
  ]
}
````
