# Krok 0348 · strażnik_przykład

Węzeł: `review` · dział: 4 · pytanie: 20 · próba: 2

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Do rozlicz.py trafiają zmienne: imię, opis i kwota pojedynczego wydatku, różnica między tekstem a liczbą oraz wartość logiczna „czy zapłacono”.

Kanon: elementy już pokazane czytelnikowi (nazwy i deklaracje są wiążące):
```text
rozlicz.py · plik programu (skrypt główny) · rozlicz.py
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)

osoby · zmienna (lista tekstów) · wspolna_kasa/rozlicz.py
osoby = ["Ania", "Bartek", "Celina"]
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
- dodaj imie: 
imie = "Ania"
- dodaj kwota: 
kwota = 45.5
- dodaj zaplacono: 
zaplacono = True

NOWA SEKCJA "Czym jest zmienna":
[[zmienna|Zmienna]] to nazwane miejsce w pamięci programu, w którym leży jedna [[dana|dana]]. Dzięki nazwie możesz tę daną wielokrotnie odczytać, użyć w obliczeniach albo zastąpić inną.

Pamiętasz, że dane trzeba gdzieś przechowywać, żeby użyć ich więcej niż raz. Właśnie do tego służy zmienna. Zamiast wpisywać `45.5` w kilku miejscach, nadajesz kwocie nazwę i posługujesz się nią. To trochę jak komórka w arkuszu, którą nazwałeś „kwota”, a potem odwołujesz się do niej po nazwie.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(imie, kwota, zaplacono)
kwota = 60
print(kwota + 10)
```

```text
Ania 45.5 True
70
```

Znak `=` nie oznacza tu „równa się” jak w matematyce. Znaczy: „zapisz to, co po prawej, pod nazwą po lewej”. Dokładniej opiszemy to przy przypisaniu.

Wartość zmiennej może się zmieniać w trakcie działania programu, stąd nazwa: po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce. Nazwa zostaje ta sama. W „Wspólnej Kasie” takie zmienne w `rozlicz.py` opisują pojedynczy wydatek: kto zapłacił, ile i czy już się rozliczył.

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [spójność] kasa.py: Tekst odsyła do pliku `kasa.py`, a w kanonie program to `rozlicz.py` (wspolna_kasa/rozlicz.py). Zmiana nie jest zadeklarowana w canon_changes. Zamień na `rozlicz.py`.
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
