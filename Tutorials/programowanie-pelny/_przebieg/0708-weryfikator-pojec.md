# Krok 0708 · weryfikator_pojęć

Węzeł: `review` · dział: 7 · pytanie: 38 · próba: 1

## Prompt

````text
Jesteś weryfikatorem pojęć. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dziedzina: Programowanie od podstaw.

Przeczytaj sekcję i wskaż pojęcia z dziedziny, które DOSŁOWNIE występują w tekście, czytelnik musi je znać,
żeby zrozumieć sekcję, a które NIE są w glosariuszu, NIE są oznaczone [[id|...]] i NIE są wyjaśnione w tekście.
Nie zgłaszaj pojęć, których w tekście nie ma (to nie jest recenzja kompletności), ani pojęć, które czytelnik zna.
Zgłaszaj najwyżej 3 najważniejsze braki: kind="wyjaśnienie", target=pojęcie dokładnie w brzmieniu z tekstu,
detail=czego czytelnikowi brakuje.

ODWOŁANIA W PRZÓD: jeśli pojęcie jest tematem jednego z późniejszych pytań (lista niżej), tutaj wystarczy
jedno zdanie wyjaśnienia przy pierwszym użyciu. Gdy takie zdanie jest, nie zgłaszaj pojęcia. Gdy go brak,
zgłoś je z detail="wystarczy jedno zdanie; pełne omówienie w pytaniu N".

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

PÓŹNIEJSZE PYTANIA:
- 39. Po co dzielić program na funkcje?
- 40. Czym są argumenty funkcji?
- 41. Co to znaczy, że funkcja zwraca wynik?
- 42. Dlaczego nazwy zmiennych i funkcji powinny być czytelne?
- 43. Czym jest ponowne użycie kodu?
- 44. Czym są dane wejściowe programu?
- 45. Czym są dane wyjściowe programu?
- 46. Jak program może zapytać użytkownika o informację?
- 47. Czym jest plik i jak program może z niego korzystać?
- 48. Czym jest interfejs użytkownika?
- 49. Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?
- 50. Czym różni się błąd składni od błędu logicznego?
- 51. Jak przeczytać komunikat o błędzie?
- 52. Czym jest testowanie programu?
- 53. Czym jest debugowanie?
- 54. Dlaczego warto zapisywać kolejne wersje kodu?
- 55. Jak szukać rozwiązań problemów programistycznych w internecie?
- 56. Jakie są przykłady programów używanych na co dzień?
- 57. Czym różni się strona internetowa od aplikacji mobilnej?
- 58. Jak od pomysłu dojść do działającego programu?
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
- 60. Od czego zacząć samodzielną naukę programowania?
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

GLOSARIUSZ:
- program-komputerowy: program komputerowy
- instrukcja: instrukcja
- programista: programista
- programowanie: programowanie
- jezyk-programowania: język programowania
- kod: kod
- skladnia: składnia
- aplikacja: aplikacja
- algorytm: algorytm
- warunek-zakonczenia: warunek zakończenia
- schemat-blokowy: schemat blokowy
- funkcja: funkcja
- specyfikacja-wyniku: specyfikacja wyniku
- przypadek-brzegowy: przypadek brzegowy
- kod-zrodlowy: kod źródłowy
- edytor-kodu: edytor kodu
- podswietlanie-skladni: podświetlanie składni
- python: Python
- terminal: terminal
- kompilator: kompilator
- interpreter: interpreter
- blad-w-programie: błąd w programie
- print: print
- komentarz: komentarz
- dana: dana
- zmienna: zmienna
- wartosc-zmiennej: wartość zmiennej
- typ-danych: typ danych
- wartosc-logiczna: wartość logiczna
- przypisanie: przypisanie
- operator-arytmetyczny: operator arytmetyczny
- konkatenacja: konkatenacja
- operator-porownania: operator porównania
- instrukcja-warunkowa: instrukcja warunkowa
- wciecie: wcięcie
- operator-logiczny: operator logiczny
- petla: pętla
- iteracja: iteracja
- petla-nieskonczona: pętla nieskończona
- lista-danych: lista danych
- element-listy: element listy
- indeks: indeks
NOWE HASŁA Z TEJ SEKCJI: definicja funkcji, wywołanie funkcji

SEKCJA "Czym jest funkcja":
[[funkcja|Funkcja]] to nazwany kawałek kodu, który raz opisujesz, a potem uruchamiasz, kiedy tylko zechcesz, wpisując jego nazwę. Znasz już takie gotowe kawałki: `print()` i `str()` to funkcje napisane przez twórców Pythona.

Własną funkcję zaczynasz od `def`, nazwy i nawiasów z dwukropkiem. Wcięty blok pod spodem to jej treść. Ten zapis nazywamy [[definicja-funkcji|definicją funkcji]]: tylko opisuje, co funkcja robi, i niczego jeszcze nie wykonuje. Dopiero [[wywolanie-funkcji|wywołanie]], czyli nazwa z nawiasami, uruchamia treść.

Weźmy pętlę, która zbiera sumę wydatków, jak w poprzedniej sekcji. Zamieniamy ją w osobną funkcję:

```python
def suma_wydatkow(wydatki):
    suma = 0
    for wydatek in wydatki:
        suma = suma + wydatek["kwota"]
    return suma

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.50},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 200}]
print(suma_wydatkow(wydatki))
```

```text
320.5
```

Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. Oba mechanizmy omówimy osobno w kolejnych sekcjach; na razie wystarczy, że dane wchodzą, a wynik wychodzi.

Konsekwencja: kod, który wcześniej był kawałkiem długiego skryptu, ma teraz nazwę i można go wywołać w wielu miejscach, bez kopiowania.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "W przykładzie każdy wydatek to zapis w klamrach {\"kto\": ..., \"kwota\": ...}, a kwotę czytamy przez wydatek[\"kwota\"]. Takiej struktury (słownika: pary klucz–wartość) nie ma w glosariuszu ani w tekście. Czytelnik zna tylko listy z indeksami, więc nie zrozumie, czym jest wydatek[\"kwota\"] ani skąd wynik 320.5. Wystarczy jedno zdanie, np. że wydatek to karteczka z podpisanymi polami, a wydatek[\"kwota\"] odczytuje pole „kwota”. Można też uprościć przykład do samych liczb.",
      "severity": "blokująca",
      "target": "wydatek[\"kwota\"]",
      "source": "sekcja Czym jest funkcja"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Słowo „skrypt” nie jest w glosariuszu ani wyjaśnione. Można je zastąpić słowem „program” albo dodać krótkie wyjaśnienie.",
      "severity": "sugestia",
      "target": "skryptu"
    }
  ]
}
````
