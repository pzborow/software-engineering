# Plan tutorialu: Programowanie od podstaw

Perspektywa: **osoba spoza IT** · poziom: **początkujący** · języki kodu: python, text

Rekruter zapytany: „Ile pytań mogłoby opisać wiedzę z zakresu Programowanie od podstaw na poziomie: początkujący, z punktu widzenia: osoba spoza IT? Preferuję mniejsze pytania niż pytania z długim elaboratem. Podaj tylko liczbę.” odpowiedział: **61**.

## Jak zatwierdzić

1. Przeczytaj pytania, moduły i wątki poniżej. Ten plik jest widokiem stanu tutorialu: ręczne zmiany nie są wczytywane.
2. Zmiany zleć słowami; zobaczysz różnicę do zatwierdzenia, a plan powstanie od nowa:

```bash
tutorial-writer edit --output-dir output/programowanie-pelny "zamień pytanie 3 na …; połącz działy 4 i 5"
```

   Zmiana pytań albo modułów wplatanych sprawi, że planista zaprojektuje wątki od nowa (jedno wywołanie na wątek).
3. Uruchom budowę:

```bash
tutorial-writer build --output-dir output/programowanie-pelny --cache
```

## Styl tytułów

Krótkie polecenie do czytelnika w trybie rozkazującym, zaczynające się od czasownika, 2-5 słów, bez znaku zapytania i bez dwukropka, np. 'Rozłóż problem na kroki', 'Poznaj swój pierwszy błąd'. Nie zaczynaj więcej niż dwóch tytułów tym samym czasownikiem; poprawna polszczyzna (przecinki przed 'czym', 'jak').

## Języki kodu

python

## Moduły dodatków

Wplatane w tekst: przykład, warsztat. Dodatki: dygresje, dowcipy, rysunki, wtręty, dykteryjki. Zmiany przez `tutorial-writer edit`.

- wplatane: przykład, warsztat
- włączone: dowcipy, dygresje, dykteryjki, rysunki, wtręty
- intensywność: 1
- dowcipy.widzi: wtręty, dykteryjki
- dygresje.widzi: dykteryjki
- dykteryjki.widzi: wtręty, dygresje
- dykteryjki.narrator: doświadczony Python developer, kilkanaście lat w projektach backendowych i automatyzacji
- dykteryjki.ton: poważny, rzeczowy, bez żartów
- rysunki.widzi: tylko własne
- rysunki.styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
- wtręty.widzi: dowcipy, dykteryjki
- wtręty.bohater: Marta, 34-letnia specjalistka ds. kadr, która w arkuszu kalkulacyjnym radzi sobie świetnie, ale kodu nigdy nie pisała. Co miesiąc rozlicza wspólne wydatki z współlokatorami (czynsz, zakupy, wyjazdy) i chce zastąpić ręczne formuły programem, który policzy podział z napiwkiem i rabatem oraz zapisze wynik do pliku; kłopoty jej sprawiają błędy w składni, niezrozumiałe komunikaty i obawa, że zepsuje coś w komputerze.

## Wersje

Na tych wersjach opierają się przykłady; weryfikator faktów sprawdza wobec nich dokumentację.

- Python 3.13 — Składnia przykładów (zmienne, pętle, funkcje, input, pliki) i komunikaty o błędach pochodzą z Pythona 3.x.

## Pytania

## 01. Czym jest programowanie

1. Czym jest program komputerowy?
2. Czym jest programowanie?
3. Kim jest programista i czym się zajmuje?
4. Czym jest język programowania?
5. Dlaczego komputer potrzebuje precyzyjnych instrukcji?
6. Czym różni się program od aplikacji?

## 02. Algorytmy i myślenie krokowe

7. Czym jest algorytm?
8. Jak przepis kulinarny przypomina algorytm?
9. Dlaczego kolejność kroków w algorytmie ma znaczenie?
10. Czym jest schemat blokowy?
11. Jak podzielić duży problem na mniejsze części?
12. Co to znaczy, że algorytm jest poprawny?

## 03. Kod i jego uruchamianie

13. Czym jest kod źródłowy?
14. Do czego służy edytor kodu?
15. Co to znaczy uruchomić program?
16. Czym jest kompilator lub interpreter?
17. Co to jest błąd w programie?
18. Do czego służą komentarze w kodzie?

## 04. Dane i zmienne

19. Czym jest dana w programie?
20. Czym jest zmienna?
21. Jak można porównać zmienną do pudełka z etykietą?
22. Czym różni się liczba od tekstu w programie?
23. Czym jest typ danych?
24. Co to jest wartość logiczna prawda/fałsz?
25. Do czego służy przypisanie wartości do zmiennej?

## 05. Operacje i decyzje

26. Jakie podstawowe działania matematyczne może wykonać program?
27. Jak program łączy ze sobą teksty?
28. Jak program porównuje dwie wartości?
29. Czym jest instrukcja warunkowa „jeśli… to…”?
30. Do czego służy część „w przeciwnym razie”?
31. Do czego służą operatory „i” oraz „lub”?

## 06. Powtarzanie i kolekcje

32. Czym jest pętla?
33. Kiedy warto użyć pętli zamiast pisać to samo wiele razy?
34. Czym jest pętla nieskończona i dlaczego jest problemem?
35. Czym jest lista danych?
36. Jak odczytać konkretny element listy?
37. Jak przejść przez wszystkie elementy listy?

## 07. Funkcje i porządek w kodzie

38. Czym jest funkcja?
39. Po co dzielić program na funkcje?
40. Czym są argumenty funkcji?
41. Co to znaczy, że funkcja zwraca wynik?
42. Dlaczego nazwy zmiennych i funkcji powinny być czytelne?
43. Czym jest ponowne użycie kodu?

## 08. Współpraca programu z użytkownikiem

44. Czym są dane wejściowe programu?
45. Czym są dane wyjściowe programu?
46. Jak program może zapytać użytkownika o informację?
47. Czym jest plik i jak program może z niego korzystać?
48. Czym jest interfejs użytkownika?
49. Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?

## 09. Błędy i dobre praktyki

50. Czym różni się błąd składni od błędu logicznego?
51. Jak przeczytać komunikat o błędzie?
52. Czym jest testowanie programu?
53. Czym jest debugowanie?
54. Dlaczego warto zapisywać kolejne wersje kodu?
55. Jak szukać rozwiązań problemów programistycznych w internecie?

## 10. Programowanie w praktyce

56. Jakie są przykłady programów używanych na co dzień?
57. Czym różni się strona internetowa od aplikacji mobilnej?
58. Jak od pomysłu dojść do działającego programu?
59. Jakie umiejętności poza kodowaniem przydają się programiście?
60. Od czego zacząć samodzielną naukę programowania?
61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

## Przykład przewodni: Rozliczenie wspólnych wydatków „Wspólna Kasa”

Mały program w Pythonie do rozliczania wspólnych wydatków współlokatorów lub znajomych na wyjeździe: kto ile wydał, kto komu ile jest winien. Pokazuje dane, decyzje, pętle, funkcje, pliki i testy na czymś znanym z życia.

**Dokąd zmierza:** Zaczynamy od rozliczenia wydatków na kartce i opisu krokowego, potem zamieniamy je w kod: zmienne z kwotami, decyzje, pętle po liście wydatków, funkcje. Następnie program czyta wydatki z pliku CSV i pyta użytkownika, na końcu dostaje testy, wersje w Git i pomysły na automatyzację, np. wysyłanie podsumowania.

_Planista: Wszystkie działy da się pokazać na jednym małym programie w Pythonie, który rośnie od opisu krokowego do w pełni działającego narzędzia z plikiem, testami i wersjami._

| Dział | Co przybywa |
|---|---|
| 01. Czym jest programowanie | Przedstawiamy problem: rozliczanie wydatków na wyjeździe w arkuszu jest żmudne, więc opisujemy, co miałby robić program „Wspólna Kasa” i kto (programista) go napisze, jeszcze bez kodu. |
| 02. Algorytmy i myślenie krokowe | Zapisujemy rozliczenie jako algorytm krok po kroku i schemat blokowy (zsumuj, podziel, porównaj wpłaty z udziałem), dzieląc problem na części, które później staną się funkcjami. |
| 03. Kod i jego uruchamianie | Powstaje pierwszy plik rozlicz.py w edytorze VS Code z komentarzami; uruchamiamy go interpreterem Pythona i widzimy pierwszy celowy błąd. |
| 04. Dane i zmienne | Do rozlicz.py trafiają zmienne: imię, opis i kwota pojedynczego wydatku, różnica między tekstem a liczbą oraz wartość logiczna „czy zapłacono”. |
| 05. Operacje i decyzje | Program liczy udział jednej osoby, skleja tekst podsumowania i decyduje if/else oraz operatorami and/or, czy ktoś jest winien pieniądze, czy ma dostać zwrot. |
| 06. Powtarzanie i kolekcje | Pojedyncze zmienne zastępuje lista wydatków i lista osób; pętla for sumuje kwoty i liczy saldo każdego uczestnika, a pętla nieskończona pojawia się jako ostrzeżenie. |
| 07. Funkcje i porządek w kodzie | Kod dzieli się na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby z czytelnymi nazwami, argumentami i zwracanymi wynikami, gotowe do ponownego użycia. |
| 08. Współpraca programu z użytkownikiem | Program wczytuje wydatki z pliku wydatki.csv, pyta użytkownika o nowy wydatek przez zapytaj_o_wydatek, waliduje kwotę w sprawdz_kwote i drukuje wynik jako prosty interfejs tekstowy. |
| 09. Błędy i dobre praktyki | Naprawiamy błąd logiczny (np. dzielenie przez zero przy pustej liście), czytamy komunikaty błędów, dodajemy test_rozlicz.py, debugujemy i zapisujemy wersje w repozytorium Git. |
| 10. Programowanie w praktyce | Oceniamy gotowe narzędzie i pomysły na rozwój: wersja webowa lub mobilna, eksport podsumowania, automatyczne wysyłanie e-mailem, oraz plan dalszej nauki i automatyzacji własnych zadań czytelnika. |

### Obsada

| Element | Rodzaj | Plik | Rola |
|---|---|---|---|
| `rozlicz.py` | plik programu (skrypt główny) | `wspolna_kasa/rozlicz.py` | Punkt wejścia: uruchamiany poleceniem python rozlicz.py. |
| `wydatki.csv` | plik danych | `wspolna_kasa/wydatki.csv` | Lista wydatków wczytywana przez program. |
| `wydatki` | zmienna (lista słowników) | `wspolna_kasa/rozlicz.py` | Kolekcja wszystkich wydatków w pamięci programu. |
| `osoby` | zmienna (lista tekstów) | `wspolna_kasa/rozlicz.py` | Uczestnicy, między których dzielimy koszty. |
| `suma_wydatkow` | funkcja | `wspolna_kasa/rozlicz.py` | Dodaje kwoty wszystkich wydatków (pętla). |
| `udzial_na_osobe` | funkcja | `wspolna_kasa/rozlicz.py` | Dzieli sumę po równo; zwraca wynik. |
| `saldo_osoby` | funkcja | `wspolna_kasa/rozlicz.py` | Wpłacone minus udział; dodatnie oznacza, że ktoś ma dostać zwrot. |
| `wczytaj_wydatki` | funkcja | `wspolna_kasa/rozlicz.py` | Czyta plik CSV i buduje listę wydatków. |
| `zapytaj_o_wydatek` | funkcja | `wspolna_kasa/rozlicz.py` | Pyta użytkownika o osobę, opis i kwotę oraz sprawdza dane. |
| `sprawdz_kwote` | funkcja | `wspolna_kasa/rozlicz.py` | Walidacja: odrzuca tekst niebędący liczbą i kwoty ujemne. |
| `wypisz_podsumowanie` | funkcja | `wspolna_kasa/rozlicz.py` | Drukuje, kto komu ile jest winien. |
| `test_rozlicz.py` | plik testów | `wspolna_kasa/test_rozlicz.py` | Sprawdza automatycznie poprawność funkcji. |
| `wspolna_kasa` | repozytorium Git | `wspolna_kasa/.git` | Historia wersji kodu; wprowadzone w dziale 09. |

<details>
<summary>Deklaracje</summary>

```text
# rozlicz.py
if __name__ == "__main__":
    glowna()

# kto,opis,kwota
Ania,zakupy,120.50
Bartek,paliwo,200.00

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.50}]

osoby = ["Ania", "Bartek", "Celina"]

def suma_wydatkow(wydatki: list) -> float:

def udzial_na_osobe(suma: float, liczba_osob: int) -> float:

def saldo_osoby(imie: str, wydatki: list, udzial: float) -> float:

def wczytaj_wydatki(sciezka: str) -> list:

def zapytaj_o_wydatek() -> dict:

def sprawdz_kwote(tekst: str) -> float:

def wypisz_podsumowanie(salda: dict) -> None:

def test_udzial_na_osobe():
    assert udzial_na_osobe(300.0, 3) == 100.0

git init
git add .
git commit -m "Pierwsza wersja rozliczenia"
```

</details>

## Warsztat: Wspólna Kasa krok po kroku

Czytelnik buduje u siebie w terminalu mały program w Pythonie do rozliczania wspólnych wydatków znajomych na wyjeździe. Program rośnie od pierwszego „Hello” do wersji z plikiem, funkcjami i testami.

**Dokąd zmierza:** Czytelnik zaczyna od sprawdzenia, że Python działa, i pisze pierwszy skrypt. Potem wprowadza dane o wydatkach, liczy sumy i decyzje, dodaje pętle po liście, wydziela funkcje, wczytuje dane z pliku i od użytkownika. Na końcu program sprawdza dane, ma testy i wersje w git, a czytelnik widzi, jak go rozbudować lub zautomatyzować.

**Punkt startowy:** Dowolny system (Windows, macOS lub Linux) z terminalem (PowerShell, bash lub zsh), zainstalowany Python 3.13 (sprawdzenie: python --version, na macOS/Linux ewentualnie python3 --version) oraz prosty edytor kodu, np. VS Code lub Notatnik. Pusty katalog roboczy ~/wspolna_kasa, w którym czytelnik otwiera terminal.

_Planista: Wątek pasuje: działy 03–09 dają się pokazać w jednym rosnącym programie, a działy 01, 02 i 10 są pojęciowe i mają tylko lekkie kroki lub żadne. Warsztat buduje to samo co przykład przewodni („Wspólna Kasa”), bo początkujący spoza IT lepiej uczy się na jednym znanym projekcie niż na kilku rozproszonych. Nie wymaga to dodatkowych narzędzi poza Pythonem, a każdy krok startuje ze stanu po poprzednim. Warsztat jest jednak prostszy niż przykład przewodni: bez bibliotek zewnętrznych, w jednym pliku, potem w dwóch, uruchamiany w terminalu._

| Dział | Co przybywa |
|---|---|
| 03. Kod i jego uruchamianie | Czytelnik sprawdza python --version, zapisuje w edytorze plik kasa.py z jednym print i komentarzem, uruchamia go poleceniem python kasa.py, po czym celowo psuje nazwę print i ogląda pierwszy błąd. |
| 04. Dane i zmienne | W kasa.py pojawiają się zmienne: nazwa wyjazdu (tekst), kwota wydatku (liczba) i czy_oplacone (prawda/fałsz), wypisywane razem z typami przez type(). |
| 05. Operacje i decyzje | Program liczy koszt na osobę (dzielenie kwoty przez liczbę osób), skleja teksty w zdanie i za pomocą if/else oraz operatorów and/or ocenia, czy wydatek jest duży. |
| 06. Powtarzanie i kolekcje | Wydatki trafiają do listy, a pętla for wypisuje je wszystkie, sumuje i wybiera pierwszy oraz ostatni element; czytelnik widzi też, jak wygląda while bez warunku zakończenia i zatrzymuje go Ctrl+C. |
| 07. Funkcje i porządek w kodzie | Kod jest dzielony na funkcje suma(wydatki) i na_osobe(suma, osoby) z argumentami i wartością zwracaną oraz czytelnymi nazwami, a funkcje są używane ponownie dla dwóch różnych wyjazdów. |
| 08. Współpraca programu z użytkownikiem | Program pyta użytkownika przez input() o imię i kwotę, zapisuje wydatki do pliku wydatki.txt i wczytuje je z powrotem, a błędnie wpisaną kwotę (np. tekst) odrzuca z komunikatem i ponownym pytaniem. |
| 09. Błędy i dobre praktyki | Czytelnik wywołuje błąd składni i błąd logiczny (np. dzielenie przez złą liczbę), czyta komunikat Traceback, dopisuje kilka testów z assert w test_kasa.py, debuguje przez print i zapisuje wersję w git (git init, git add, git commit). |
| 10. Programowanie w praktyce | Czytelnik dopisuje do Wspólnej Kasy jedną własną drobną funkcję, np. wypisanie, kto komu ile jest winien, i zapisuje ją jako kolejny commit, widząc w praktyce automatyzację prostego zadania. |
