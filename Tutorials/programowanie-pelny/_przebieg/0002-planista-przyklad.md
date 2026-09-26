# Krok 0002 · planista_przykład

Węzeł: `plan_canons` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś planistą wątku „Przykład przewodni” dla tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

„Przykład przewodni” to jeden fikcyjny projekt, na którym pokazujemy kolejne zagadnienia: aplikacja, infrastruktura, repozytorium, zbiór danych, klaster, cokolwiek jest naturalne dla TEGO tematu. Rośnie z działu na dział, więc czytelnik widzi, jak każde zagadnienie zmienia ten sam projekt. Kod nie musi działać: liczą się spójne nazwy i deklaracje.

1. Zdecyduj, czy ten wątek pasuje do tutorialu (applicable). Nie pasuje, gdy działy dotyczą rzeczy, których
   nie da się sensownie pokazać w jednym wątku. Wtedy uzasadnij w reason i zostaw resztę pustą.
2. Wymyśl scenariusz sam: znany każdemu, z kilkoma nietrywialnymi wymaganiami, na których widać zagadnienia tematu.
3. elements: obsada startowa, 8-15 elementów w jednostkach właściwych dla dziedziny tematu, nie z innej architektury.
   Przykłady: Terraform: zasób, moduł, zmienna, output; Git: gałąź, commit, tag, remote; RDF/SPARQL: klasa, predykat,
   graf nazwany, zapytanie; Kubernetes: deployment, service, configmap; SQL: tabela, indeks, widok; kod aplikacji: klasa,
   funkcja, moduł. kind nazwij w języku dziedziny.
   signature: deklaracja w jednym z języków kodu tutorialu (python),
   bez szczegółów, maks. 6 linii. file: gdzie element leży (plik, moduł, repozytorium, dataset).
   Nazwy spójne z konwencjami tej dziedziny.
4. steps: dla KAŻDEGO działu jedno zdanie, co przybywa albo zmienia się w wątku. Przyrosty mają prowadzić
   do jednego celu (story), a nie być luźnymi scenkami.

DZIAŁY I PYTANIA:
Dział 01. Czym jest programowanie
  - Czym jest program komputerowy?
  - Czym jest programowanie?
  - Kim jest programista i czym się zajmuje?
  - Czym jest język programowania?
  - Dlaczego komputer potrzebuje precyzyjnych instrukcji?
  - Czym różni się program od aplikacji?
Dział 02. Algorytmy i myślenie krokowe
  - Czym jest algorytm?
  - Jak przepis kulinarny przypomina algorytm?
  - Dlaczego kolejność kroków w algorytmie ma znaczenie?
  - Czym jest schemat blokowy?
  - Jak podzielić duży problem na mniejsze części?
  - Co to znaczy, że algorytm jest poprawny?
Dział 03. Kod i jego uruchamianie
  - Czym jest kod źródłowy?
  - Do czego służy edytor kodu?
  - Co to znaczy uruchomić program?
  - Czym jest kompilator lub interpreter?
  - Co to jest błąd w programie?
  - Do czego służą komentarze w kodzie?
Dział 04. Dane i zmienne
  - Czym jest dana w programie?
  - Czym jest zmienna?
  - Jak można porównać zmienną do pudełka z etykietą?
  - Czym różni się liczba od tekstu w programie?
  - Czym jest typ danych?
  - Co to jest wartość logiczna prawda/fałsz?
  - Do czego służy przypisanie wartości do zmiennej?
Dział 05. Operacje i decyzje
  - Jakie podstawowe działania matematyczne może wykonać program?
  - Jak program łączy ze sobą teksty?
  - Jak program porównuje dwie wartości?
  - Czym jest instrukcja warunkowa „jeśli… to…”?
  - Do czego służy część „w przeciwnym razie”?
  - Do czego służą operatory „i” oraz „lub”?
Dział 06. Powtarzanie i kolekcje
  - Czym jest pętla?
  - Kiedy warto użyć pętli zamiast pisać to samo wiele razy?
  - Czym jest pętla nieskończona i dlaczego jest problemem?
  - Czym jest lista danych?
  - Jak odczytać konkretny element listy?
  - Jak przejść przez wszystkie elementy listy?
Dział 07. Funkcje i porządek w kodzie
  - Czym jest funkcja?
  - Po co dzielić program na funkcje?
  - Czym są argumenty funkcji?
  - Co to znaczy, że funkcja zwraca wynik?
  - Dlaczego nazwy zmiennych i funkcji powinny być czytelne?
  - Czym jest ponowne użycie kodu?
Dział 08. Współpraca programu z użytkownikiem
  - Czym są dane wejściowe programu?
  - Czym są dane wyjściowe programu?
  - Jak program może zapytać użytkownika o informację?
  - Czym jest plik i jak program może z niego korzystać?
  - Czym jest interfejs użytkownika?
  - Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?
Dział 09. Błędy i dobre praktyki
  - Czym różni się błąd składni od błędu logicznego?
  - Jak przeczytać komunikat o błędzie?
  - Czym jest testowanie programu?
  - Czym jest debugowanie?
  - Dlaczego warto zapisywać kolejne wersje kodu?
  - Jak szukać rozwiązań problemów programistycznych w internecie?
Dział 10. Programowanie w praktyce
  - Jakie są przykłady programów używanych na co dzień?
  - Czym różni się strona internetowa od aplikacji mobilnej?
  - Jak od pomysłu dojść do działającego programu?
  - Jakie umiejętności poza kodowaniem przydają się programiście?
  - Od czego zacząć samodzielną naukę programowania?
  - Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?
````

## Odpowiedź

````json
{
  "applicable": true,
  "reason": "Wszystkie działy da się pokazać na jednym małym programie w Pythonie, który rośnie od opisu krokowego do w pełni działającego narzędzia z plikiem, testami i wersjami.",
  "title": "Rozliczenie wspólnych wydatków „Wspólna Kasa”",
  "domain": "Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.",
  "setup": "Dowolny system (Windows, macOS lub Linux), Python 3.12 zainstalowany z python.org, edytor kodu Visual Studio Code, terminal (wiersz poleceń) otwarty w pustym folderze roboczym wspolna_kasa. Git 2.40 pojawia się dopiero w dziale 09.",
  "story": "Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.",
  "elements": [
    {
      "name": "rozlicz.py",
      "kind": "plik programu (skrypt główny)",
      "signature": "# rozlicz.py\nif __name__ == \"__main__\":\n    glowna()",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Punkt wejścia: uruchamiany poleceniem python rozlicz.py."
    },
    {
      "name": "wydatki.csv",
      "kind": "plik danych",
      "signature": "# kto,opis,kwota\nAnia,zakupy,120.50\nBartek,paliwo,200.00",
      "file": "wspolna_kasa/wydatki.csv",
      "note": "Lista wydatków wczytywana przez program."
    },
    {
      "name": "wydatki",
      "kind": "zmienna (lista słowników)",
      "signature": "wydatki = [{\"kto\": \"Ania\", \"opis\": \"zakupy\", \"kwota\": 120.50}]",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Kolekcja wszystkich wydatków w pamięci programu."
    },
    {
      "name": "osoby",
      "kind": "zmienna (lista tekstów)",
      "signature": "osoby = [\"Ania\", \"Bartek\", \"Celina\"]",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Uczestnicy, między których dzielimy koszty."
    },
    {
      "name": "suma_wydatkow",
      "kind": "funkcja",
      "signature": "def suma_wydatkow(wydatki: list) -> float:",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Dodaje kwoty wszystkich wydatków (pętla)."
    },
    {
      "name": "udzial_na_osobe",
      "kind": "funkcja",
      "signature": "def udzial_na_osobe(suma: float, liczba_osob: int) -> float:",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Dzieli sumę po równo; zwraca wynik."
    },
    {
      "name": "saldo_osoby",
      "kind": "funkcja",
      "signature": "def saldo_osoby(imie: str, wydatki: list, udzial: float) -> float:",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Wpłacone minus udział; dodatnie oznacza, że ktoś ma dostać zwrot."
    },
    {
      "name": "wczytaj_wydatki",
      "kind": "funkcja",
      "signature": "def wczytaj_wydatki(sciezka: str) -> list:",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Czyta plik CSV i buduje listę wydatków."
    },
    {
      "name": "zapytaj_o_wydatek",
      "kind": "funkcja",
      "signature": "def zapytaj_o_wydatek() -> dict:",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Pyta użytkownika o osobę, opis i kwotę oraz sprawdza dane."
    },
    {
      "name": "sprawdz_kwote",
      "kind": "funkcja",
      "signature": "def sprawdz_kwote(tekst: str) -> float:",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Walidacja: odrzuca tekst niebędący liczbą i kwoty ujemne."
    },
    {
      "name": "wypisz_podsumowanie",
      "kind": "funkcja",
      "signature": "def wypisz_podsumowanie(salda: dict) -> None:",
      "file": "wspolna_kasa/rozlicz.py",
      "note": "Drukuje, kto komu ile jest winien."
    },
    {
      "name": "test_rozlicz.py",
      "kind": "plik testów",
      "signature": "def test_udzial_na_osobe():\n    assert udzial_na_osobe(300.0, 3) == 100.0",
      "file": "wspolna_kasa/test_rozlicz.py",
      "note": "Sprawdza automatycznie poprawność funkcji."
    },
    {
      "name": "wspolna_kasa",
      "kind": "repozytorium Git",
      "signature": "git init\ngit add .\ngit commit -m \"Pierwsza wersja rozliczenia\"",
      "file": "wspolna_kasa/.git",
      "note": "Historia wersji kodu; wprowadzone w dziale 09."
    }
  ],
  "steps": [
    {
      "chapter": 1,
      "goal": "Przedstawiamy problem: rozliczanie wydatków na wyjeździe w arkuszu jest żmudne, więc opisujemy, co miałby robić program „Wspólna Kasa” i kto (programista) go napisze, jeszcze bez kodu."
    },
    {
      "chapter": 2,
      "goal": "Zapisujemy rozliczenie jako algorytm krok po kroku i schemat blokowy (zsumuj, podziel, porównaj wpłaty z udziałem), dzieląc problem na części, które później staną się funkcjami."
    },
    {
      "chapter": 3,
      "goal": "Powstaje pierwszy plik rozlicz.py w edytorze VS Code z komentarzami; uruchamiamy go interpreterem Pythona i widzimy pierwszy celowy błąd."
    },
    {
      "chapter": 4,
      "goal": "Do rozlicz.py trafiają zmienne: imię, opis i kwota pojedynczego wydatku, różnica między tekstem a liczbą oraz wartość logiczna „czy zapłacono”."
    },
    {
      "chapter": 5,
      "goal": "Program liczy udział jednej osoby, skleja tekst podsumowania i decyduje if/else oraz operatorami and/or, czy ktoś jest winien pieniądze, czy ma dostać zwrot."
    },
    {
      "chapter": 6,
      "goal": "Pojedyncze zmienne zastępuje lista wydatków i lista osób; pętla for sumuje kwoty i liczy saldo każdego uczestnika, a pętla nieskończona pojawia się jako ostrzeżenie."
    },
    {
      "chapter": 7,
      "goal": "Kod dzieli się na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby z czytelnymi nazwami, argumentami i zwracanymi wynikami, gotowe do ponownego użycia."
    },
    {
      "chapter": 8,
      "goal": "Program wczytuje wydatki z pliku wydatki.csv, pyta użytkownika o nowy wydatek przez zapytaj_o_wydatek, waliduje kwotę w sprawdz_kwote i drukuje wynik jako prosty interfejs tekstowy."
    },
    {
      "chapter": 9,
      "goal": "Naprawiamy błąd logiczny (np. dzielenie przez zero przy pustej liście), czytamy komunikaty błędów, dodajemy test_rozlicz.py, debugujemy i zapisujemy wersje w repozytorium Git."
    },
    {
      "chapter": 10,
      "goal": "Oceniamy gotowe narzędzie i pomysły na rozwój: wersja webowa lub mobilna, eksport podsumowania, automatyczne wysyłanie e-mailem, oraz plan dalszej nauki i automatyzacji własnych zadań czytelnika."
    }
  ]
}
````
