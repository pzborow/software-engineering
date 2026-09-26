# Krok 1053 · strażnik_przykład

Węzeł: `review` · dział: 9 · pytanie: 54 · próba: 2

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
- dodaj wspolna_kasa: Pierwsze użycie zaplanowanego elementu.
git init -b main

NOWA SEKCJA "Po co zapisywać wersje kodu":
Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast szukać własnych zmian z pamięci.

Robi to [[git|Git]], program do zapisywania historii plików. Zapis jednej wersji to [[commit|commit]]: zdjęcie wybranych plików z danej chwili, z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię, to [[repozytorium|repozytorium]]. W przykładowym programie do dzielenia wydatków, „Wspólnej Kasie”, będzie nim folder `wspolna_kasa`, w którym leżą pliki programu.

Wersje przydają się w trzech sytuacjach:

- Dopisujesz do „Wspólnej Kasy” nową funkcję, [[sec-09-czym-jest-testowanie-programu|testy]] przestają przechodzić, a Ty wracasz do wczorajszego commita zamiast szukać własnych zmian.
- Historia pokazuje, kiedy pojawił się błąd, co przy szukaniu przyczyny oszczędza sporo czasu.
- Każdy commit ma opis, więc po miesiącu wiesz, dlaczego kod wygląda tak, a nie inaczej.

Dobry moment na commit to chwila, gdy testy przechodzą. Wiele małych commitów jest lepsze niż jeden wielki.

Sam zapis wygląda tak:

```text
git init -b main
git add funkcje.py test_rozlicz.py
git commit -m "Funkcje i testy Wspolnej Kasy"
```

`init` zakłada repozytorium w bieżącym folderze, `add` wybiera pliki do zapisu, a `commit` zapisuje wersję. Git trzeba mieć zainstalowanym (sprawdzisz to poleceniem `git --version`, a instalator jest na stronie git-scm.com). Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym.

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [spójność] test_rozlicz.py: W poleceniu `git add funkcje.py test_kasa.py` pojawia się plik `test_kasa.py`, a w kanonie plik testów nazywa się `test_rozlicz.py`. Nie ma deklaracji zmiany nazwy. Zamień na `git add funkcje.py test_rozlicz.py`, a komunikat commita dostosuj do tego, co faktycznie w nim jest.
- [spójność] wspolna_kasa: Tekst mówi, że repozytorium „będzie to `wspolna_kasa`”, ale `git init -b main` bez argumentu zakłada repozytorium w bieżącym katalogu i nie tworzy katalogu o tej nazwie. Dodaj `git init -b main wspolna_kasa` albo `mkdir wspolna_kasa && cd wspolna_kasa` przed `init`. W kanonie `wspolna_kasa/` jest też katalogiem z `rozlicz.py`, więc warto wyjaśnić, że to ten sam katalog.
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "spójność",
      "target": "wspolna_kasa",
      "detail": "Tekst nadal nie mówi, że polecenie `git init -b main` trzeba uruchomić w folderze `wspolna_kasa`. Samo `init` zakłada repozytorium w bieżącym folderze i nie tworzy folderu o tej nazwie. Dodaj jedno zdanie, np. „Uruchom polecenia w folderze `wspolna_kasa`”, albo linię `cd wspolna_kasa` przed `git init`.",
      "severity": "sugestia",
      "status": "niespełniona",
      "source": "uwaga 2 z poprzedniej recenzji"
    }
  ]
}
````
