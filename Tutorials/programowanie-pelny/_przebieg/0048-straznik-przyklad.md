# Krok 0048 · strażnik_przykład

Węzeł: `review` · dział: 1 · pytanie: 4 · próba: 1

## Prompt

````text
Jesteś strażnikiem wątku „Przykład przewodni” w tutorialu: Programowanie od podstaw.

PRZYKŁAD PRZEWODNI (wątek wplatany „przykład”): Rozliczenie wspólnych wydatków „Wspólna Kasa”
Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.
Cel całości: Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.
W tym dziale wątek rozwija się tak: Przedstawiamy problem: rozliczanie wydatków na wyjeździe w arkuszu jest żmudne, więc opisujemy, co miałby robić program „Wspólna Kasa” i kto (programista) go napisze, jeszcze bez kodu.

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

NOWA SEKCJA "Czym jest język programowania":
[[jezyk-programowania|Język programowania]] to ściśle określony sposób zapisywania [[instrukcja|instrukcji]], który potrafi zrozumieć komputer. Ma własne słowa i reguły zapisu, ale jest o wiele prostszy i bardziej rygorystyczny niż język polski.

Komputer nie wyciąga wniosków z kontekstu. Zdanie „podziel rachunek po równo” człowiek zrozumie od razu, komputer nie. Język programowania wymusza zapis, który ma jedno znaczenie. Zbiór jego reguł nazywamy [[skladnia|składnią]]: mówi ona, jak wolno układać słowa i znaki, żeby powstało poprawne polecenie.

Oto jedna instrukcja w Pythonie, języku, którego użyjemy w tym tutorialu:

```python
print("Cześć, Wspólna Kasa!")
```

```text
Cześć, Wspólna Kasa!
```

Słowo `print` znaczy „wypisz”, a tekst w cudzysłowie to to, co ma się pojawić na ekranie. Gdybyś pominął jeden cudzysłów, komputer odmówiłby wykonania polecenia, bo zapis łamie reguły.

Języków jest bardzo wiele, a każdy ma inną składnię i inne zastosowania. Różnią się zapisem, ale robią to samo: pozwalają opisać kroki, które komputer wykona. Kto pozna zasady jednego, łatwiej nauczy się następnych.

Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "spójność",
      "target": "print(\"Cześć, Wspólna Kasa!\")",
      "detail": "Jednolinijkowy przykład z print jest ilustracją składni, a nie elementem kanonu; nie koliduje z żadną nazwą ani deklaracją. Wątek „Wspólna Kasa” pojawia się tylko w tekście powitania. Opcjonalnie można zapowiedzieć, że docelowy program rozliczy wydatki, ale nie jest to konieczne.",
      "severity": "sugestia",
      "source": "kod w sekcji",
      "status": "nowa"
    }
  ]
}
````
