# Krok 0090 · strażnik_przykład

Węzeł: `review` · dział: 2 · pytanie: 7 · próba: 1

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Zapisujemy rozliczenie jako algorytm krok po kroku i schemat blokowy (zsumuj, podziel, porównaj wpłaty z udziałem), dzieląc problem na części, które później staną się funkcjami.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
(jeszcze nic)
```
Zaplanowane, jeszcze niepokazane: rozlicz.py (plik programu (skrypt główny)), wydatki.csv (plik danych), wydatki (zmienna (lista słowników)), osoby (zmienna (lista tekstów)), suma_wydatkow (funkcja), udzial_na_osobe (funkcja), saldo_osoby (funkcja), wczytaj_wydatki (funkcja), zapytaj_o_wydatek (funkcja), sprawdz_kwote (funkcja), wypisz_podsumowanie (funkcja), test_rozlicz.py (plik testów), wspolna_kasa (repozytorium Git)

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

NOWA SEKCJA "Czym jest algorytm":
[[algorytm|Algorytm]] to skończony ciąg jednoznacznych kroków, który dla podanych danych prowadzi do wyniku. Nie jest jeszcze programem: to sam pomysł na rozwiązanie, który można zapisać zwykłymi słowami, na kartce albo w kodzie.

Dobry algorytm ma trzy cechy. Zaczyna od jasno określonych danych wejściowych, każdy krok jest na tyle dokładny, że nie wymaga domyślania się (tak jak „Resztę groszy dopisz pierwszej osobie” z listy kroków z wcześniejszej sekcji), i po skończonej liczbie kroków się kończy, dając wynik.

Weźmy czworo znajomych na wyjeździe, którzy płacili na zmianę. Rozliczenie da się opisać tak:

```text
dane: lista wydatków (kto, ile) i liczba osób
1. Zsumuj wszystkie wydatki.
2. Podziel sumę przez liczbę osób: to udział jednej osoby.
3. Dla każdej osoby odejmij udział od tego, ile wydała.
4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna.
wynik: saldo każdej osoby
```

Na razie nie piszemy kodu: to celowo zwykły język. Ten sam algorytm można potem zapisać w Pythonie, w arkuszu kalkulacyjnym albo wykonać ręcznie. Właśnie dlatego warto go oddzielać od kodu.

Konsekwencja: zanim napiszesz program, upewnij się, że masz algorytm. Gdy kroki są jasne na papierze, zamiana ich na kod jest już głównie kwestią zapisu.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "spójność",
      "target": "„Resztę groszy dopisz pierwszej osobie” / „lista kroków z wcześniejszej sekcji”",
      "detail": "Tekst odwołuje się do listy kroków z wcześniejszej sekcji i cytuje z niej krok o groszach. Kanon jest pusty (\"jeszcze nic\"), więc czytelnik nie widział żadnej takiej listy. Jedyna lista w sekcji (4 kroki) nie ma kroku o groszach. Popraw: albo usuń odwołanie i weź przykład z listy poniżej, albo dodaj do listy krok o groszach. Przykład jednoznacznego kroku może też brzmieć „Podziel sumę przez liczbę osób”.",
      "severity": "blokująca",
      "source": "kanon",
      "status": "nowa"
    },
    {
      "kind": "spójność",
      "target": "czworo znajomych / dane",
      "detail": "Tekst mówi o czworgu znajomych, ale nie podaje żadnych imion ani kwot. To drobna niespójność z późniejszym kodem (wydatki, osoby). Warto dać krótki konkretny zestaw, np. 4 osoby i kilka wydatków, żeby algorytm dało się prześledzić. Wątek wymaga też schematu blokowego (zsumuj, podziel, porównaj) i podziału na części, które staną się funkcjami (suma_wydatkow, udzial_na_osobe, saldo_osoby). W tej sekcji ich nie ma, więc można je zapowiedzieć.",
      "severity": "sugestia",
      "source": "wątek",
      "status": "nowa"
    }
  ]
}
````
