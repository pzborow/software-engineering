# Krok 0289 · strażnik_przykład

Węzeł: `review` · dział: 3 · pytanie: 18 · próba: 1

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Powstaje pierwszy plik rozlicz.py w edytorze VS Code z komentarzami; uruchamiamy go interpreterem Pythona i widzimy pierwszy celowy błąd.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
rozlicz.py · plik programu (skrypt główny) · rozlicz.py
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```
Zaplanowane, jeszcze niepokazane: wydatki.csv (plik danych), wydatki (zmienna (lista słowników)), osoby (zmienna (lista tekstów)), suma_wydatkow (funkcja), udzial_na_osobe (funkcja), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), zapytaj_o_wydatek (funkcja), sprawdz_kwote (funkcja), wypisz_podsumowanie (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

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
- zmień rozlicz.py: Dodajemy komentarze do pierwszego pliku programu.
# rozlicz.py - rozliczenie wspólnych wydatków
print("Wspólna Kasa")
print(300 / 3)  # 300 zł na troje osób: udział jednej osoby

NOWA SEKCJA "Do czego służą komentarze":
[[komentarz|Komentarz]] to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi.

W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. [[interpreter|Interpreter]] pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją.

```python
# rozlicz.py - rozliczenie wspólnych wydatków
print("Wspólna Kasa")
print(300 / 3)  # 300 zł na troje osób: udział jednej osoby
# print(300 / 2)  <- ta linia jest wyłączona
```

```text
Wspólna Kasa
100.0
```

Ostatnia linia pokazuje drugie zastosowanie: zamiana instrukcji na komentarz „wyłącza” ją bez kasowania. Przyda się to, gdy będziesz coś sprawdzać.

Komentarz ma sens, gdy podaje powód lub kontekst („300 zł na troje osób”). Powtarzanie tego, co widać w kodzie, tylko go zaśmieca. Pamiętaj też, że komentarz może się zestarzeć: jeśli zmienisz kod, a opis zostawisz, wprowadzi czytelnika w błąd. U siebie masz już taki komentarz w pierwszej linii `kasa.py`. Za chwilę go poprawisz i sprawdzisz, że nie wpływa na wynik.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "target": "kasa.py",
      "detail": "Ostatni akapit odwołuje się do pliku `kasa.py` z komentarzem w pierwszej linii. W kanonie jest tylko `rozlicz.py`, a jego pierwsza linia (`# rozlicz.py - rozliczenie wspólnych wydatków`) jest aktualna, nie przestarzała. Zamień na `rozlicz.py` i dopasuj resztę zdania. Można np. zapowiedzieć, że czytelnik zmieni komentarz w `rozlicz.py`, uruchomi plik i sprawdzi, że wynik się nie zmienił.",
      "severity": "blokująca",
      "source": "akapit ostatni",
      "status": "nowa"
    },
    {
      "kind": "spójność",
      "target": "rozlicz.py",
      "detail": "Blok kodu ma czwartą linię `# print(300 / 2)  <- ta linia jest wyłączona`, której nie ma w zadeklarowanej zmianie `rozlicz.py`. Dodaj ją do deklaracji zmiany albo oznacz ten fragment jako demonstrację poza kanonem, żeby plik czytelnika nie rozjechał się z kanonem.",
      "severity": "sugestia",
      "source": "blok python",
      "status": "nowa"
    }
  ]
}
````
