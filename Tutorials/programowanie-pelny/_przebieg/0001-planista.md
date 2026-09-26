# Krok 0001 · planista

Węzeł: `plan_decisions` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś planistą tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

1. code_languages: języki bloków kodu, których potrzebuje ten tutorial: języki, w których TEMAT się wyraża
   (np. zapytania, konfiguracja, manifesty) oraz języki, w których pisze czytelnik z tej perspektywy
   (wskazówka z profilu: python).
   Podaj identyfikatory jak po ``` (np. hcl, sparql, turtle, yaml, sql, tsx, bash), zwykle 2-4, bez "text".
2. versions: najwyżej 5 wersji, od których zależy POPRAWNOŚĆ kodu i twierdzeń tutorialu: składnia, API, flagi,
   zachowanie (np. "Terraform 1.9", "Kubernetes 1.30", "SPARQL 1.1"). Nie wymieniaj narzędzi pobocznych
   (lintery, skanery, CI). Wybierz aktualne, stabilne wersje. Pusta lista, gdy temat od wersji nie zależy (np. algorytmy).

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
  "code_languages": [
    "python",
    "bash"
  ],
  "versions": [
    {
      "name": "Python",
      "version": "3.13",
      "why": "Składnia przykładów (zmienne, pętle, funkcje, input, pliki) i komunikaty o błędach pochodzą z Pythona 3.x."
    }
  ]
}
````
