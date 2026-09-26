# Krok 0003 · planista_warsztat

Węzeł: `plan_canons` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś planistą wątku „Warsztat” dla tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

„Warsztat” to ciąg kroków, które czytelnik wykonuje u siebie od pierwszego do ostatniego działu: zapisuje pliki, uruchamia polecenia i widzi dokładnie te wyniki, które podaje tutorial. W przeciwieństwie do przykładu przewodniego wszystko jest kompletne i wykonywalne; każdy krok startuje ze stanu po poprzednim. Może budować ten sam projekt co przykład przewodni albo osobny, prostszy do uruchomienia. Dział, w którym nie ma nic do zrobienia, nie ma kroków.
Zaplanowany już wątek „Przykład przewodni”: Rozliczenie wspólnych wydatków „Wspólna Kasa”. Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.

1. Zdecyduj, czy ten wątek pasuje do tutorialu (applicable). Nie pasuje, gdy działy dotyczą rzeczy, których
   nie da się sensownie pokazać w jednym wątku. Wtedy uzasadnij w reason i zostaw resztę pustą.
2. Wymyśl scenariusz sam: znany każdemu, z kilkoma nietrywialnymi wymaganiami, na których widać zagadnienia tematu.
   W reason napisz też, czy warsztat buduje to samo co zaplanowany już wątek, czy osobny projekt, i dlaczego.
3. setup: punkt startowy u czytelnika: system i powłoka, narzędzia z wersjami, które musi mieć, katalog roboczy
   (np. „terminal bash, Python 3.12, pusty katalog ~/kalkulator”). Wszystko, czego wymagają kroki, musi tu być
   albo zostać zainstalowane w którymś kroku. Wersje zgodne z tutorialem: Python 3.13.
4. elements: zostaw puste; stan warsztatu to pliki, które powstają w krokach.
5. steps: dla działów, w których czytelnik coś u siebie robi, jedno zdanie: co tworzy, uruchamia albo poprawia.
   Działy bez nic do zrobienia pomiń. Kroki mają tworzyć ciągłą historię do celu (story), bez skoków stanu.

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
  "reason": "Wątek pasuje: działy 03–09 dają się pokazać w jednym rosnącym programie, a działy 01, 02 i 10 są pojęciowe i mają tylko lekkie kroki lub żadne. Warsztat buduje to samo co przykład przewodni („Wspólna Kasa”), bo początkujący spoza IT lepiej uczy się na jednym znanym projekcie niż na kilku rozproszonych. Nie wymaga to dodatkowych narzędzi poza Pythonem, a każdy krok startuje ze stanu po poprzednim. Warsztat jest jednak prostszy niż przykład przewodni: bez bibliotek zewnętrznych, w jednym pliku, potem w dwóch, uruchamiany w terminalu.",
  "title": "Wspólna Kasa krok po kroku",
  "domain": "Czytelnik buduje u siebie w terminalu mały program w Pythonie do rozliczania wspólnych wydatków znajomych na wyjeździe. Program rośnie od pierwszego „Hello” do wersji z plikiem, funkcjami i testami.",
  "setup": "Dowolny system (Windows, macOS lub Linux) z terminalem (PowerShell, bash lub zsh), zainstalowany Python 3.13 (sprawdzenie: python --version, na macOS/Linux ewentualnie python3 --version) oraz prosty edytor kodu, np. VS Code lub Notatnik. Pusty katalog roboczy ~/wspolna_kasa, w którym czytelnik otwiera terminal.",
  "story": "Czytelnik zaczyna od sprawdzenia, że Python działa, i pisze pierwszy skrypt. Potem wprowadza dane o wydatkach, liczy sumy i decyzje, dodaje pętle po liście, wydziela funkcje, wczytuje dane z pliku i od użytkownika. Na końcu program sprawdza dane, ma testy i wersje w git, a czytelnik widzi, jak go rozbudować lub zautomatyzować.",
  "steps": [
    {
      "chapter": 3,
      "goal": "Czytelnik sprawdza python --version, zapisuje w edytorze plik kasa.py z jednym print i komentarzem, uruchamia go poleceniem python kasa.py, po czym celowo psuje nazwę print i ogląda pierwszy błąd."
    },
    {
      "chapter": 4,
      "goal": "W kasa.py pojawiają się zmienne: nazwa wyjazdu (tekst), kwota wydatku (liczba) i czy_oplacone (prawda/fałsz), wypisywane razem z typami przez type()."
    },
    {
      "chapter": 5,
      "goal": "Program liczy koszt na osobę (dzielenie kwoty przez liczbę osób), skleja teksty w zdanie i za pomocą if/else oraz operatorów and/or ocenia, czy wydatek jest duży."
    },
    {
      "chapter": 6,
      "goal": "Wydatki trafiają do listy, a pętla for wypisuje je wszystkie, sumuje i wybiera pierwszy oraz ostatni element; czytelnik widzi też, jak wygląda while bez warunku zakończenia i zatrzymuje go Ctrl+C."
    },
    {
      "chapter": 7,
      "goal": "Kod jest dzielony na funkcje suma(wydatki) i na_osobe(suma, osoby) z argumentami i wartością zwracaną oraz czytelnymi nazwami, a funkcje są używane ponownie dla dwóch różnych wyjazdów."
    },
    {
      "chapter": 8,
      "goal": "Program pyta użytkownika przez input() o imię i kwotę, zapisuje wydatki do pliku wydatki.txt i wczytuje je z powrotem, a błędnie wpisaną kwotę (np. tekst) odrzuca z komunikatem i ponownym pytaniem."
    },
    {
      "chapter": 9,
      "goal": "Czytelnik wywołuje błąd składni i błąd logiczny (np. dzielenie przez złą liczbę), czyta komunikat Traceback, dopisuje kilka testów z assert w test_kasa.py, debuguje przez print i zapisuje wersję w git (git init, git add, git commit)."
    },
    {
      "chapter": 10,
      "goal": "Czytelnik dopisuje do Wspólnej Kasy jedną własną drobną funkcję, np. wypisanie, kto komu ile jest winien, i zapisuje ją jako kolejny commit, widząc w praktyce automatyzację prostego zadania."
    }
  ]
}
````
