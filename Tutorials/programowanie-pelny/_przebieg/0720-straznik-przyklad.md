# Krok 0720 · strażnik_przykład

Węzeł: `review` · dział: 7 · pytanie: 38 · próba: 2

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
(brak)

NOWA SEKCJA "Czym jest funkcja":
[[funkcja|Funkcja]] to nazwany kawałek kodu, który raz opisujesz, a potem uruchamiasz, kiedy zechcesz, wpisując jego nazwę. Znasz już gotowe funkcje: `print()` i `str()` napisali twórcy Pythona.

Własną funkcję zaczynasz od `def`, nazwy, nawiasów i dwukropka. Wcięty blok pod spodem to jej treść. Ten zapis to [[definicja-funkcji|definicja funkcji]]: tylko opisuje, co funkcja robi, i niczego jeszcze nie wykonuje. Dopiero [[wywolanie-funkcji|wywołanie]], czyli nazwa z nawiasami, uruchamia treść.

Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:

```python
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

print(suma([45.5, 20, 12.5]))
```

```text
78.0
```

Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. Oba mechanizmy omówimy osobno w kolejnych sekcjach; na razie wystarczy, że dane wchodzą, a wynik wychodzi.

Konsekwencja: kod, który był kawałkiem długiego programu, ma teraz nazwę i można go wywołać w wielu miejscach, bez kopiowania.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "target": "suma (funkcja)",
      "detail": "Kanon ma już `suma` jako zmienną (liczbę: `suma = 0` w pętli po `wydatki`). Funkcja `def suma(wydatki)` nadaje tę samą nazwę innemu bytowi, a czytelnik ma w programie obie rzeczy. Plan wątku przewiduje funkcję `suma_wydatkow`. Zmień na `def suma_wydatkow(wydatki):` i zadeklaruj ją w canon_changes (module=\"przykład\", dodaj, np. `suma_wydatkow(wydatki)` · funkcja · wspolna_kasa/rozlicz.py, zwraca liczbę).",
      "severity": "blokująca",
      "source": "kanon: suma; plan: suma_wydatkow"
    },
    {
      "kind": "spójność",
      "target": "wydatki",
      "detail": "W kanonie `wydatki` to lista słowników (`{\"kto\", \"opis\", \"kwota\"}`), a pętla używa `wydatek[\"kwota\"]`. Tu `wydatki` to lista samych liczb (`[45.5, 20, 12.5]`), a pętla ma `for kwota in wydatki`. To inny typ argumentu pod tą samą nazwą, a `kwota` w kanonie jest zmienną liczbową, nie zmienną pętli. Popraw ciało na `for wydatek in wydatki: suma = suma + wydatek[\"kwota\"]`, a wywołanie na liście słowników, np. `[{\"kto\": \"Ania\", \"opis\": \"zakupy\", \"kwota\": 45.5}, ...]`. Wynik 78.0 zostaje.",
      "severity": "blokująca",
      "source": "kanon: wydatki, wydatek, suma"
    },
    {
      "kind": "spójność",
      "target": "razem",
      "detail": "Nowa zmienna `razem` dubluje kanoniczną `suma` z pętli, na którą tekst się powołuje („taką jak w sekcji o pętli”). Użyj `suma` wewnątrz funkcji (nie koliduje, jeśli funkcja nazywa się `suma_wydatkow`), żeby czytelnik widział ten sam kod przeniesiony do funkcji.",
      "severity": "sugestia",
      "source": "kanon: suma"
    }
  ]
}
````
