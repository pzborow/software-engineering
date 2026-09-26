# Raport przebiegu

Dziedzina: **Programowanie od podstaw** · perspektywa: **osoba spoza IT** · języki kodu: python, text

## Podsumowanie agentów

| Agent | Wywołań | Czas [s] | Koszt [$] | Z cache |
|---|---|---|---|---|
| planista | 1 | 3 | 0.025 | 0 |
| planista_przykład | 1 | 27 | 0.057 | 0 |
| planista_warsztat | 1 | 18 | 0.035 | 0 |
| autor_wstępu | 15 | 81 | 0.441 | 0 |
| recenzent_wstępu | 15 | 136 | 0.319 | 0 |
| weryfikator_żargonu | 1 | 2 | 0.009 | 0 |
| pisarz | 102 | 2248 | 9.637 | 0 |
| kontrola_deterministyczna | 102 | 0 | 0.000 | 0 |
| weryfikator_pojęć | 102 | 625 | 2.359 | 0 |
| znudzony_czytelnik | 102 | 735 | 2.166 | 0 |
| strażnik_przykład | 102 | 729 | 2.500 | 0 |
| weryfikator_odwołań | 102 | 1186 | 3.926 | 0 |
| decyzja | 109 | 0 | 0.000 | 0 |
| akceptacja | 61 | 0 | 0.000 | 0 |
| autor_dodatków | 61 | 751 | 4.002 | 0 |
| weryfikator_dodatków | 61 | 555 | 4.355 | 0 |
| sprawdzacz_wyników | 71 | 384 | 1.095 | 0 |
| weryfikator_faktów | 73 | 810 | 3.838 | 0 |
| łowca_pułapek | 43 | 133 | 0.658 | 0 |
| strażnik_warsztat | 60 | 652 | 1.746 | 0 |
| audytor_pokrycia | 10 | 140 | 0.556 | 0 |
| audytor_obietnic | 16 | 64 | 0.303 | 0 |
| redaktor_zdania | 7 | 20 | 0.086 | 0 |
| klasyfikator_pułapek | 1 | 3 | 0.022 | 0 |
| redaktor_tytułów | 1 | 42 | 0.115 | 0 |
| autor_ściągawki | 1 | 41 | 0.120 | 0 |
| **razem** | 1221 | 9386 | 38.369 | 0 |

## Zgłoszone potrzeby

| Rodzaj | Źródło | Waga | Status | Ile razy |
|---|---|---|---|---|
| odwołanie | weryfikator_odwołań | sugestia | nowa | 99 |
| spójność | strażnik_przykład | sugestia | nowa | 69 |
| spójność | strażnik_warsztat | sugestia | nowa | 50 |
| wyjaśnienie | weryfikator_pojęć | sugestia | nowa | 49 |
| odwołanie | weryfikator_odwołań | blokująca | nowa | 35 |
| konkret | znudzony_czytelnik | sugestia | nowa | 29 |
| wynik | sprawdzacz_wyników | sugestia | nowa | 29 |
| przykład | znudzony_czytelnik | sugestia | nowa | 27 |
| fakt | weryfikator_faktów | sugestia | nowa | 27 |
| spójność | strażnik_przykład | blokująca | nowa | 23 |
| skrócenie | znudzony_czytelnik | sugestia | nowa | 16 |
| spójność | strażnik_warsztat | blokująca | nowa | 12 |
| diagram | recenzent_wstępu | blokująca | nowa | 12 |
| tempo | znudzony_czytelnik | sugestia | nowa | 10 |
| wyjaśnienie | kontrola_glosariusza | blokująca | nowa | 10 |
| wyjaśnienie | weryfikator_pojęć | blokująca | nowa | 9 |
| odwołanie | kontrola_odwołań | blokująca | nowa | 9 |
| diagram | recenzent_wstępu | sugestia | nowa | 7 |
| wynik | strażnik_warsztat | sugestia | nowa | 7 |
| wynik | strażnik_warsztat | blokująca | nowa | 6 |
| wyjaśnienie | znudzony_czytelnik | sugestia | nowa | 5 |
| wyjaśnienie | recenzent_wstępu | sugestia | nowa | 5 |
| spójność | kontrola_przykład | blokująca | nowa | 5 |
| odwołanie | weryfikator_odwołań | blokująca | niespełniona | 4 |
| wynik | sprawdzacz_wyników | blokująca | nowa | 4 |
| konkret | recenzent_wstępu | sugestia | nowa | 4 |
| diagram | recenzent_wstępu | blokująca | niespełniona | 4 |
| tempo | recenzent_wstępu | sugestia | nowa | 3 |
| język | recenzent_wstępu | sugestia | nowa | 3 |
| spójność | znudzony_czytelnik | sugestia | nowa | 3 |
| spójność | strażnik_przykład | blokująca | niespełniona | 3 |
| konkret | znudzony_czytelnik | blokująca | nowa | 2 |
| fakt | znudzony_czytelnik | sugestia | nowa | 2 |
| spójność | kontrola_warsztat | sugestia | nowa | 2 |
| fakt | znudzony_czytelnik | blokująca | nowa | 2 |
| wynik | strażnik_warsztat | blokująca | niespełniona | 2 |
| spójność | recenzent_wstępu | blokująca | nowa | 2 |
| przykład | znudzony_czytelnik | blokująca | nowa | 2 |
| odwołanie | znudzony_czytelnik | sugestia | nowa | 2 |
| wyjaśnienie | recenzent_wstępu | blokująca | nowa | 2 |
| odwołanie | recenzent_wstępu | blokująca | nowa | 2 |
| tempo | kontrola_długości | blokująca | nowa | 2 |
| język | znudzony_czytelnik | sugestia | nowa | 1 |
| wyjaśnienie | kontrola_glosariusza | blokująca | niespełniona | 1 |
| skrócenie | kontrola_kodu | blokująca | nowa | 1 |
| spójność | recenzent_wstępu | sugestia | nowa | 1 |
| spójność | strażnik_warsztat | blokująca | niespełniona | 1 |
| diagram | znudzony_czytelnik | sugestia | nowa | 1 |
| spójność | kontrola_warsztat | blokująca | nowa | 1 |
| spójność | kontrola_warsztat | blokująca | niespełniona | 1 |
| odwołanie | znudzony_czytelnik | blokująca | nowa | 1 |
| pokrycie | recenzent_wstępu | sugestia | nowa | 1 |

## Oś czasu

### 0001 · planista

- Wynik: Języki: python, text. Wersje: Python 3.13.
- [prompt i odpowiedź](_przebieg/0001-planista.md) · 3.3 s · $0.0247

### 0002 · planista_przykład

- Wynik: „Rozliczenie wspólnych wydatków „Wspólna Kasa””: 13 elementów obsady, 10 kroków. 01: Przedstawiamy problem: rozliczanie wydatków na wyjeździe w arkuszu jest żmudne, więc opisujemy, co miałby robić program „Wspólna Kasa” i kto (programista) go napisze, jeszcze bez kodu. · 02: Zapisujemy rozliczenie jako algorytm krok po kroku i schemat blokowy (zsumuj, podziel, porównaj wpłaty z udziałem), dzieląc problem na części, które później staną się funkcjami. · 03: Powstaje pierwszy plik rozlicz.py w edytorze VS Code z komentarzami; uruchamiamy go interpreterem Pythona i widzimy pierwszy celowy błąd. · 04: Do rozlicz.py trafiają zmienne: imię, opis i kwota pojedynczego wydatku, różnica między tekstem a liczbą oraz wartość logiczna „czy zapłacono”. · 05: Program liczy udział jednej osoby, skleja tekst podsumowania i decyduje if/else oraz operatorami and/or, czy ktoś jest winien pieniądze, czy ma dostać zwrot. · 06: Pojedyncze zmienne zastępuje lista wydatków i lista osób; pętla for sumuje kwoty i liczy saldo każdego uczestnika, a pętla nieskończona pojawia się jako ostrzeżenie. · 07: Kod dzieli się na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby z czytelnymi nazwami, argumentami i zwracanymi wynikami, gotowe do ponownego użycia. · 08: Program wczytuje wydatki z pliku wydatki.csv, pyta użytkownika o nowy wydatek przez zapytaj_o_wydatek, waliduje kwotę w sprawdz_kwote i drukuje wynik jako prosty interfejs tekstowy. · 09: Naprawiamy błąd logiczny (np. dzielenie przez zero przy pustej liście), czytamy komunikaty błędów, dodajemy test_rozlicz.py, debugujemy i zapisujemy wersje w repozytorium Git. · 10: Oceniamy gotowe narzędzie i pomysły na rozwój: wersja webowa lub mobilna, eksport podsumowania, automatyczne wysyłanie e-mailem, oraz plan dalszej nauki i automatyzacji własnych zadań czytelnika.
- [prompt i odpowiedź](_przebieg/0002-planista-przyklad.md) · 27.1 s · $0.0574

### 0003 · planista_warsztat

- Wynik: „Wspólna Kasa krok po kroku”: 0 elementów obsady, 8 kroków, start: Dowolny system (Windows, macOS lub Linux) z terminalem (PowerShell, bash lub zsh), zainstalowany Python 3.13 (sprawdzenie: python --version, na macOS/Linux ewentualnie python3 --version) oraz prosty edytor kodu, np. VS Code lub Notatnik. Pusty katalog roboczy ~/wspolna_kasa, w którym czytelnik otwiera terminal.. 03: Czytelnik sprawdza python --version, zapisuje w edytorze plik kasa.py z jednym print i komentarzem, uruchamia go poleceniem python kasa.py, po czym celowo psuje nazwę print i ogląda pierwszy błąd. · 04: W kasa.py pojawiają się zmienne: nazwa wyjazdu (tekst), kwota wydatku (liczba) i czy_oplacone (prawda/fałsz), wypisywane razem z typami przez type(). · 05: Program liczy koszt na osobę (dzielenie kwoty przez liczbę osób), skleja teksty w zdanie i za pomocą if/else oraz operatorów and/or ocenia, czy wydatek jest duży. · 06: Wydatki trafiają do listy, a pętla for wypisuje je wszystkie, sumuje i wybiera pierwszy oraz ostatni element; czytelnik widzi też, jak wygląda while bez warunku zakończenia i zatrzymuje go Ctrl+C. · 07: Kod jest dzielony na funkcje suma(wydatki) i na_osobe(suma, osoby) z argumentami i wartością zwracaną oraz czytelnymi nazwami, a funkcje są używane ponownie dla dwóch różnych wyjazdów. · 08: Program pyta użytkownika przez input() o imię i kwotę, zapisuje wydatki do pliku wydatki.txt i wczytuje je z powrotem, a błędnie wpisaną kwotę (np. tekst) odrzuca z komunikatem i ponownym pytaniem. · 09: Czytelnik wywołuje błąd składni i błąd logiczny (np. dzielenie przez złą liczbę), czyta komunikat Traceback, dopisuje kilka testów z assert w test_kasa.py, debuguje przez print i zapisuje wersję w git (git init, git add, git commit). · 10: Czytelnik dopisuje do Wspólnej Kasy jedną własną drobną funkcję, np. wypisanie, kto komu ile jest winien, i zapisuje ją jako kolejny commit, widząc w praktyce automatyzację prostego zadania.
- [prompt i odpowiedź](_przebieg/0003-planista-warsztat.md) · 17.5 s · $0.0346

### 0004 · autor_wstępu · dział 01 · próba 1

- Kolejka TODO (61): 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 …
- Wynik: Wstęp: 83 słów
- [prompt i odpowiedź](_przebieg/0004-autor-wstepu.md) · 4.7 s · $0.0118

### 0005 · recenzent_wstępu · dział 01 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `tempo` (sugestia) **Rozwiązuje prosty problem: bez zrozumienia... ufać albo się bać**: Można złagodzić metaforę „tajemniczej skrzynki” i dodać, że kurs prowadzi krok po kroku od zera. To tylko drobne ulepszenie, wstęp jest zrozumiały i mieści się w limitach. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0005-recenzent-wstepu.md) · 3.7 s · $0.0148

### 0006 · weryfikator_żargonu · dział 01 · próba 1

- Wynik: Pierwszy akapit bez żargonu.
- [prompt i odpowiedź](_przebieg/0006-weryfikator-zargonu.md) · 2.3 s · $0.0089

### 0007 · pisarz · dział 01 · pytanie 1 · próba 1

- Kolejka TODO (60): 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13 …
- Wynik: „Czym jest program komputerowy”: 173 słów prozy, ```text 1 linii; nowe hasła: program komputerowy, instrukcja, programista
- [prompt i odpowiedź](_przebieg/0007-pisarz.md) · 16.3 s · $0.0494

### 0008 · kontrola_deterministyczna · dział 01 · pytanie 1 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0009 · weryfikator_pojęć · dział 01 · pytanie 1 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **kodu**: wystarczy jedno zdanie; pełne omówienie w pytaniu 13. Np. że kod to zapisane instrukcje programu, czyli tekst, który pisze programista. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0009-weryfikator-pojec.md) · 6.2 s · $0.0247

### 0010 · znudzony_czytelnik · dział 01 · pytanie 1 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **akapit o „Wspólnej Kasie”**: Wejście i wyjście „Wspólnej Kasy” opisano ogólnie („lista wydatków”, „rozliczenie”). Jedna linijka z liczbami (np. Ania zapłaciła 120 zł za paliwo, a wynik: Bartek oddaje Ani 30 zł) zilustrowałaby schemat wejście → program → wyjście. Zmieściłoby się w limicie po skróceniu jednego zdania. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0010-znudzony-czytelnik.md) · 7.0 s · $0.0181

### 0011 · strażnik_przykład · dział 01 · pytanie 1 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0011-straznik-przyklad.md) · 2.4 s · $0.0149

### 0012 · weryfikator_odwołań · dział 01 · pytanie 1 · próba 1

- Wynik: Brak uwag. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0012-weryfikator-odwolan.md) · 7.0 s · $0.0270

### 0013 · decyzja · dział 01 · pytanie 1 · próba 1

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 0014 · akceptacja · dział 01 · pytanie 1

- Wynik: Sekcja [sec-01-czym-jest-program-komputerowy] dopisana do działu 01; hasła w glosariuszu: program komputerowy, instrukcja, programista; odwołania: w przód „osoba, która zamienia potrzebę na instrukcje”, w przód „przykład, który będzie nam towarzyszył”, w przód „Na razie nie piszemy kodu”; punkty zaczepienia: schemat programu, czworo znajomych na wyjeździe; w TODO zostało 60.
- 0.0 s

### 0015 · autor_dodatków · dział 01 · pytanie 1

- Wynik: „Czym jest program komputerowy”: wtręty: Marta prosi komputer o „sprawiedliwy” podział, dygresje: Pierwszy program powstał przed komputerami
- [prompt i odpowiedź](_przebieg/0015-autor-dodatkow.md) · 11.2 s · $0.0280

### 0016 · weryfikator_dodatków · dział 01 · pytanie 1

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0016-weryfikator-dodatkow.md) · 13.7 s · $0.0927

### 0017 · pisarz · dział 01 · pytanie 2 · próba 1

- Kolejka TODO (59): 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14 …
- Wynik: „Czym jest programowanie”: 143 słów prozy, ```text 3 linii; nowe hasła: programowanie, język programowania
- [prompt i odpowiedź](_przebieg/0017-pisarz.md) · 18.9 s · $0.0573

### 0018 · kontrola_deterministyczna · dział 01 · pytanie 2 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0019 · weryfikator_pojęć · dział 01 · pytanie 2 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0019-weryfikator-pojec.md) · 2.6 s · $0.0202

### 0020 · znudzony_czytelnik · dział 01 · pytanie 2 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **Akapit o rozbijaniu problemu na kroki**: Kroki „zsumuj, podziel, porównaj” są podane bez liczb. Wystarczy jedno zdanie z danymi, np. wydatki 100, 60, 0 i 40 zł dają razem 200 zł, czyli po 50 zł na osobę, więc ostatnia osoba dopłaca 50 zł. Wtedy widać, że to „rozbicie na kroki” naprawdę rozwiązuje problem. Zmieści się w limicie słów, jeśli skrócisz zdanie o pętli poprawek. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0020-znudzony-czytelnik.md) · 7.6 s · $0.0210

### 0021 · strażnik_przykład · dział 01 · pytanie 2 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Wróćmy do czworga znajomych**: Zdanie „Wróćmy do czworga znajomych z wyjazdu” zakłada, że przykład był już przedstawiony, a kanon jest pusty. Czworo znajomych nie pojawia się wcześniej. Lepiej napisać „Weźmy czworo znajomych po wspólnym wyjeździe” i krótko wprowadzić „Wspólną Kasę”. Sekcja nie dotyka kodu ani nazw z kanonu, więc nic mu nie przeczy. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0021-straznik-przyklad.md) · 6.5 s · $0.0214

### 0022 · weryfikator_odwołań · dział 01 · pytanie 2 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **kroki rozwiązania**: Można dodać krótki przykład liczbowy do kroków rozliczenia (np. 4 osoby, wydatki 200 zł, 100 zł, 0 zł, 100 zł: średnio 100 zł, więc ktoś dopłaca), by teza o rozbijaniu problemu na kroki była bardziej konkretna. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **ostatni akapit**: Zdanie „Zyskujesz na tym jedną rzecz” jest nieco sztuczne; można je przeformułować, np. „Zaleta jest taka:”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0022-weryfikator-odwolan.md) · 6.3 s · $0.0267

### 0023 · decyzja · dział 01 · pytanie 2 · próba 1

- Wynik: Sekcja przyjęta; 4 sugestii trafia do raportu.
- 0.0 s

### 0024 · akceptacja · dział 01 · pytanie 2

- Wynik: Sekcja [sec-01-czym-jest-programowanie] dopisana do działu 01; hasła w glosariuszu: programowanie, język programowania; odwołania: wstecz „Wróćmy do czworga znajomych z wyjazdu”, w przód „Tym językiem zajmiemy się osobno”; punkty zaczepienia: pętla poprawek; w TODO zostało 59.
- 0.0 s

### 0025 · autor_dodatków · dział 01 · pytanie 2

- Wynik: „Czym jest programowanie”: dowcipy: Najwięcej myślenia dla kogoś, kto nie myśli, rysunki: Pętla poprawek przy stole
- [prompt i odpowiedź](_przebieg/0025-autor-dodatkow.md) · 13.3 s · $0.0321

### 0026 · weryfikator_dodatków · dział 01 · pytanie 2

- Wynik: odrzucone: 1; Najwięcej myślenia dla kogoś, kto nie myśli: Powtarza motyw wcześniejszego wpisu o Marcie (komputer nie domyśla się, trzeba mu wszystko powiedzieć wprost), a „jedyna praca” to nieprawdziwe uogólnienie.
- [prompt i odpowiedź](_przebieg/0026-weryfikator-dodatkow.md) · 8.8 s · $0.0230

### 0027 · pisarz · dział 01 · pytanie 3 · próba 1

- Kolejka TODO (58): 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 …
- Wynik: „Kim jest programista”: 156 słów prozy, ```text 1 linii
- [prompt i odpowiedź](_przebieg/0027-pisarz.md) · 20.3 s · $0.0752

### 0028 · kontrola_deterministyczna · dział 01 · pytanie 3 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0029 · weryfikator_pojęć · dział 01 · pytanie 3 · próba 1

- Wynik: 1 blokujących, 0 sugestii. (eskalowano 1 powtarzających się braków do blokujących)
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **kod**: wystarczy jedno zdanie; pełne omówienie w pytaniu 13. Słowo „kod” pada już w drugim zdaniu („Pisanie kodu”), a nie ma go w glosariuszu ani nie jest wyjaśnione. Czytelnik może się domyślić z kontekstu (zapis w języku programowania), więc to tylko sugestia: np. „kod to zapisane w języku programowania instrukcje programu”. [Eskalacja: zgłaszane już w sekcji „Czym jest program komputerowy”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0029-weryfikator-pojec.md) · 8.9 s · $0.0269

### 0030 · znudzony_czytelnik · dział 01 · pytanie 3 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `tempo` (sugestia) **akapit z wyjazdem i diagram**: Poprzednia sekcja pokazała prawie ten sam przepływ (potrzeba, kroki, kod, uruchomienie, poprawki) na tym samym przykładzie z czworgiem znajomych. Nowego jest tu tylko ustalanie, czego ktoś naprawdę potrzebuje. Diagram można wyciąć albo zastąpić jednym zdaniem o tym, czym rola różni się od samego procesu. _← znudzony_czytelnik_
  - `konkret` (sugestia) **Programista sporo czasu spędza na rozmowie, myśleniu, czytaniu cudzego kodu**: To lista ogólników. Jedno małe porównanie albo liczba by pomogły, na przykład: pisanie to ułamek dnia, a reszta to ustalanie i szukanie błędów. Można też dodać jedno pytanie, które programista zadałby znajomym. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0030-znudzony-czytelnik.md) · 8.9 s · $0.0222

### 0031 · strażnik_przykład · dział 01 · pytanie 3 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Wspólna Kasa**: Sekcja nie zawiera kodu, więc nie ma sprzeczności z kanonem. Wątek jest zgodny z celem działu: przedstawia problem rozliczania wydatków i program „Wspólna Kasa”, bez kodu. Opcjonalnie można dodać, że dane wejściowe to lista wydatków (kto zapłacił, ile, za co), co przygotuje późniejsze `wydatki`. To tylko sugestia. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0031-straznik-przyklad.md) · 4.3 s · $0.0192

### 0032 · weryfikator_odwołań · dział 01 · pytanie 3 · próba 1

- Wynik: Brak uwag. (odwołania: 5)
- [prompt i odpowiedź](_przebieg/0032-weryfikator-odwolan.md) · 8.8 s · $0.0314

### 0033 · decyzja · dział 01 · pytanie 3 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **kod**: wystarczy jedno zdanie; pełne omówienie w pytaniu 13. Słowo „kod” pada już w drugim zdaniu („Pisanie kodu”), a nie ma go w glosariuszu ani nie jest wyjaśnione. Czytelnik może się domyślić z kontekstu (zapis w języku programowania), więc to tylko sugestia: np. „kod to zapisane w języku programowania instrukcje programu”. [Eskalacja: zgłaszane już w sekcji „Czym jest program komputerowy”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 3 sugestii trafia do raportu.
- 0.0 s

### 0034 · pisarz · dział 01 · pytanie 3 · próba 2

- Kolejka TODO (58): 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 …
- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **kod**: wystarczy jedno zdanie; pełne omówienie w pytaniu 13. Słowo „kod” pada już w drugim zdaniu („Pisanie kodu”), a nie ma go w glosariuszu ani nie jest wyjaśnione. Czytelnik może się domyślić z kontekstu (zapis w języku programowania), więc to tylko sugestia: np. „kod to zapisane w języku programowania instrukcje programu”. [Eskalacja: zgłaszane już w sekcji „Czym jest program komputerowy”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: „Kim jest programista”: 163 słów prozy, ```text 1 linii; nowe hasła: kod
- [prompt i odpowiedź](_przebieg/0034-pisarz.md) · 9.6 s · $0.0562

### 0035 · kontrola_deterministyczna · dział 01 · pytanie 3 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0036 · weryfikator_pojęć · dział 01 · pytanie 3 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **kod**: wystarczy jedno zdanie; pełne omówienie w pytaniu 13. Słowo „kod” pada już w drugim zdaniu („Pisanie kodu”), a nie ma go w glosariuszu ani nie jest wyjaśnione. Czytelnik może się domyślić z kontekstu (zapis w języku programowania), więc to tylko sugestia: np. „kod to zapisane w języku programowania instrukcje programu”. [Eskalacja: zgłaszane już w sekcji „Czym jest program komputerowy”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0036-weryfikator-pojec.md) · 2.7 s · $0.0222

### 0037 · znudzony_czytelnik · dział 01 · pytanie 3 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `tempo` (sugestia) **akapit z wyjazdem i diagram**: Poprzednia sekcja już pokazała ten sam przykład (czworo znajomych) i niemal ten sam diagram: potrzeba, kroki, kod, uruchomienie, poprawki. Tu nowa jest tylko rola człowieka: rozmowa o potrzebach, czytanie cudzego kodu, szukanie błędów. Warto skrócić powtórkę etapów. Diagram można wyrzucić albo zastąpić jednym konkretnym zdaniem o tym, co programista robi w typowy dzień. Np. ustala ze znajomymi, czy kwoty mają być w złotych i groszach, i sprawdza, czy program dobrze liczy dla 3 osób i kwoty 100 zł. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0037-znudzony-czytelnik.md) · 7.7 s · $0.0209

### 0038 · strażnik_przykład · dział 01 · pytanie 3 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0038-straznik-przyklad.md) · 2.7 s · $0.0173

### 0039 · weryfikator_odwołań · dział 01 · pytanie 3 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0039-weryfikator-odwolan.md) · 10.0 s · $0.0324

### 0040 · decyzja · dział 01 · pytanie 3 · próba 2

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 0041 · akceptacja · dział 01 · pytanie 3

- Wynik: Sekcja [sec-01-kim-jest-programista] dopisana do działu 01; hasła w glosariuszu: kod; odwołania: wstecz „Weźmy czworo znajomych z wyjazdu”, w przód „przykładem, który będzie nam towarzyszył”, w przód „Na razie nie piszemy kodu”; punkty zaczepienia: ścieżka od potrzeby do poprawek; w TODO zostało 58.
- 0.0 s

### 0042 · autor_dodatków · dział 01 · pytanie 3

- Wynik: „Kim jest programista”: dykteryjki: Zanim napisałem pierwszą linijkę
- [prompt i odpowiedź](_przebieg/0042-autor-dodatkow.md) · 12.1 s · $0.0313

### 0043 · weryfikator_dodatków · dział 01 · pytanie 3

- Wynik: odrzucone: 1; Zanim napisałem pierwszą linijkę: Powtarza motyw wcześniejszego wpisu o Marcie (nieprecyzyjne zamówienie, które trzeba doprecyzować, zanim powstanie program) oraz jest zmyśloną osobistą anegdotą narratora, której nie da się potwierdzić.
- [prompt i odpowiedź](_przebieg/0043-weryfikator-dodatkow.md) · 5.5 s · $0.0207

### 0044 · pisarz · dział 01 · pytanie 4 · próba 1

- Kolejka TODO (57): 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 …
- Wynik: „Czym jest język programowania”: 153 słów prozy, ```python 1 linii, ```text 1 linii; nowe hasła: składnia
- [prompt i odpowiedź](_przebieg/0044-pisarz.md) · 17.4 s · $0.0572

### 0045 · kontrola_deterministyczna · dział 01 · pytanie 4 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0046 · weryfikator_pojęć · dział 01 · pytanie 4 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0046-weryfikator-pojec.md) · 3.0 s · $0.0202

### 0047 · znudzony_czytelnik · dział 01 · pytanie 4 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0047-znudzony-czytelnik.md) · 6.0 s · $0.0190

### 0048 · strażnik_przykład · dział 01 · pytanie 4 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **print("Cześć, Wspólna Kasa!")**: Jednolinijkowy przykład z print jest ilustracją składni, a nie elementem kanonu; nie koliduje z żadną nazwą ani deklaracją. Wątek „Wspólna Kasa” pojawia się tylko w tekście powitania. Opcjonalnie można zapowiedzieć, że docelowy program rozliczy wydatki, ale nie jest to konieczne. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0048-straznik-przyklad.md) · 4.8 s · $0.0193

### 0049 · weryfikator_odwołań · dział 01 · pytanie 4 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **Wspólna Kasa**: „Wspólna Kasa” pojawia się bez wyjaśnienia (w przykładzie i w ostatnim zdaniu). Warto jednym zdaniem przypomnieć, że to program do rozliczania wydatków znajomych z wyjazdu, żeby czytelnik wiedział, co to jest. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0049-weryfikator-odwolan.md) · 12.6 s · $0.0348

### 0050 · sprawdzacz_wyników · dział 01 · pytanie 4 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0050-sprawdzacz-wynikow.md) · 4.0 s · $0.0138

### 0051 · weryfikator_faktów · dział 01 · pytanie 4 · próba 1

- Wynik: Brak uwag. (źródła: 2)
- [prompt i odpowiedź](_przebieg/0051-weryfikator-faktow.md) · 13.9 s · $0.0678

### 0052 · decyzja · dział 01 · pytanie 4 · próba 1

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 0053 · akceptacja · dział 01 · pytanie 4

- Wynik: Sekcja [sec-01-czym-jest-jezyk-programowania] dopisana do działu 01; hasła w glosariuszu: składnia; odwołania: w przód „języku, którego użyjemy w tym tutorialu”, w przód „Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy””; punkty zaczepienia: pierwsza instrukcja w Pythonie; w TODO zostało 57.
- 0.0 s

### 0054 · łowca_pułapek · dział 01 · pytanie 4

- Wynik: „Czym jest język programowania”: brak pułapek
- [prompt i odpowiedź](_przebieg/0054-lowca-pulapek.md) · 2.2 s · $0.0127

### 0055 · autor_dodatków · dział 01 · pytanie 4

- Wynik: „Czym jest język programowania”: dowcipy: Gramatyka bez taryfy ulgowej
- [prompt i odpowiedź](_przebieg/0055-autor-dodatkow.md) · 12.3 s · $0.0316

### 0056 · weryfikator_dodatków · dział 01 · pytanie 4

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0056-weryfikator-dodatkow.md) · 6.1 s · $0.0201

### 0057 · pisarz · dział 01 · pytanie 5 · próba 1

- Kolejka TODO (56): 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17 …
- Wynik: „Po co komputerowi precyzja”: 170 słów prozy, ```text 3 linii
- [prompt i odpowiedź](_przebieg/0057-pisarz.md) · 17.4 s · $0.0585

### 0058 · kontrola_deterministyczna · dział 01 · pytanie 5 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0059 · weryfikator_pojęć · dział 01 · pytanie 5 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0059-weryfikator-pojec.md) · 3.4 s · $0.0212

### 0060 · znudzony_czytelnik · dział 01 · pytanie 5 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **Każdy krok ma jedno znaczenie i nie zostawia miejsca na domysły**: Sekcja opisuje kroki słowami, ale nie pokazuje, co się dzieje, gdy komputer dostanie niedokładną instrukcję. Krótki przykład z liczbami (np. 100 zł na 3 osoby = 33,333… i pytanie, ile wypisać) uczyniłby tezę o „braku domysłów” namacalną. Można zastąpić zdanie o „złej liczbie osób”. _← znudzony_czytelnik_
  - `tempo` (sugestia) **Ostatni akapit**: Sekcja w dużej mierze powtarza tezę z poprzedniej („komputer nie wyciąga wniosków z kontekstu”, „podziel rachunek po równo”). Nowością jest tabela i lista kroków, ale ostatni akapit o pracy programisty i sprawdzaniu wprowadza nowy wątek bez rozwinięcia. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0060-znudzony-czytelnik.md) · 5.9 s · $0.0202

### 0061 · strażnik_przykład · dział 01 · pytanie 5 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0061-straznik-przyklad.md) · 4.4 s · $0.0193

### 0062 · weryfikator_odwołań · dział 01 · pytanie 5 · próba 1

- Wynik: 1 blokujących, 2 sugestii. (odwołania: 2)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **Każdy krok ma jedno znaczenie i nie zostawia miejsca na domysły**: Twierdzenie jest nieprawdziwe wobec własnej tabeli. Trzy kroki nadal nie mówią, skąd wziąć wydatki, ile jest osób ani co zrobić z resztą, gdy kwota nie dzieli się równo (samo „do grosza” nie rozstrzyga, kto dopłaca ten grosz). Czytelnik może wynieść przekonanie, że taka lista już jest precyzyjna. Popraw: albo rozbuduj kroki (np. „Weź kwoty wydatków z listy wpisanej przez użytkownika”, „Liczba osób to 4”, „Zaokrąglij do pełnych groszy, resztę dopisz pierwszej osobie”), albo napisz wprost, że to wersja jeszcze nieprecyzyjna i pokaż, czego w niej brakuje. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **wiersz tabeli „(nic)”**: Lewa komórka „(nic)” jest niejasna. Lepiej wpisać np. „wynik po prostu widać” albo „człowiek sam powie wynik”, żeby kontrast był zrozumiały. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **„zła liczba osób”**: Dodaj liczbowy przykład błędu, np. wpisano 5 zamiast 4, więc każdy dostaje 20% zamiast 25% rachunku i program bez wahania pokazuje zły wynik. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0062-weryfikator-odwolan.md) · 17.6 s · $0.0404

### 0063 · decyzja · dział 01 · pytanie 5 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Każdy krok ma jedno znaczenie i nie zostawia miejsca na domysły**: Twierdzenie jest nieprawdziwe wobec własnej tabeli. Trzy kroki nadal nie mówią, skąd wziąć wydatki, ile jest osób ani co zrobić z resztą, gdy kwota nie dzieli się równo (samo „do grosza” nie rozstrzyga, kto dopłaca ten grosz). Czytelnik może wynieść przekonanie, że taka lista już jest precyzyjna. Popraw: albo rozbuduj kroki (np. „Weź kwoty wydatków z listy wpisanej przez użytkownika”, „Liczba osób to 4”, „Zaokrąglij do pełnych groszy, resztę dopisz pierwszej osobie”), albo napisz wprost, że to wersja jeszcze nieprecyzyjna i pokaż, czego w niej brakuje. _← weryfikator_odwołań_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 4 sugestii trafia do raportu.
- 0.0 s

### 0064 · pisarz · dział 01 · pytanie 5 · próba 2

- Kolejka TODO (56): 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17 …
- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Każdy krok ma jedno znaczenie i nie zostawia miejsca na domysły**: Twierdzenie jest nieprawdziwe wobec własnej tabeli. Trzy kroki nadal nie mówią, skąd wziąć wydatki, ile jest osób ani co zrobić z resztą, gdy kwota nie dzieli się równo (samo „do grosza” nie rozstrzyga, kto dopłaca ten grosz). Czytelnik może wynieść przekonanie, że taka lista już jest precyzyjna. Popraw: albo rozbuduj kroki (np. „Weź kwoty wydatków z listy wpisanej przez użytkownika”, „Liczba osób to 4”, „Zaokrąglij do pełnych groszy, resztę dopisz pierwszej osobie”), albo napisz wprost, że to wersja jeszcze nieprecyzyjna i pokaż, czego w niej brakuje. _← weryfikator_odwołań_
- Wynik: „Po co komputerowi precyzja”: 189 słów prozy, ```text 3 linii, ```text 6 linii
- [prompt i odpowiedź](_przebieg/0064-pisarz.md) · 10.5 s · $0.0597

### 0065 · kontrola_deterministyczna · dział 01 · pytanie 5 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0066 · weryfikator_pojęć · dział 01 · pytanie 5 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0066-weryfikator-pojec.md) · 4.6 s · $0.0230

### 0067 · znudzony_czytelnik · dział 01 · pytanie 5 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0067-znudzony-czytelnik.md) · 5.8 s · $0.0206

### 0068 · strażnik_przykład · dział 01 · pytanie 5 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **krok 1 listy precyzyjnej**: Krok 1 precyzyjnej listy mówi o „liście wpisanej przez użytkownika”. W planie wątku dane najpierw trafiają do pliku wydatki.csv, a dopiero potem program pyta użytkownika. Rozważ neutralne sformułowanie, np. „z listy wydatków”. Nie jest to sprzeczność, bo blok jest typu text i nie wprowadza żadnych nazw z kanonu. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0068-straznik-przyklad.md) · 7.8 s · $0.0236

### 0069 · weryfikator_odwołań · dział 01 · pytanie 5 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Każdy krok ma jedno znaczenie i nie zostawia miejsca na domysły**: Twierdzenie jest nieprawdziwe wobec własnej tabeli. Trzy kroki nadal nie mówią, skąd wziąć wydatki, ile jest osób ani co zrobić z resztą, gdy kwota nie dzieli się równo (samo „do grosza” nie rozstrzyga, kto dopłaca ten grosz). Czytelnik może wynieść przekonanie, że taka lista już jest precyzyjna. Popraw: albo rozbuduj kroki (np. „Weź kwoty wydatków z listy wpisanej przez użytkownika”, „Liczba osób to 4”, „Zaokrąglij do pełnych groszy, resztę dopisz pierwszej osobie”), albo napisz wprost, że to wersja jeszcze nieprecyzyjna i pokaż, czego w niej brakuje. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- [prompt i odpowiedź](_przebieg/0069-weryfikator-odwolan.md) · 6.5 s · $0.0328

### 0070 · decyzja · dział 01 · pytanie 5 · próba 2

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 0071 · akceptacja · dział 01 · pytanie 5

- Wynik: Sekcja [sec-01-po-co-komputerowi-precyzja] dopisana do działu 01; odwołania: wstecz „Wróćmy do czworga znajomych na wyjeździe”; punkty zaczepienia: lista precyzyjnych kroków; w TODO zostało 56.
- 0.0 s

### 0072 · autor_dodatków · dział 01 · pytanie 5

- Wynik: „Po co komputerowi precyzja”: dykteryjki: Brakujące grosze w rozliczeniu, wtręty: Marta wpisuje złą liczbę osób
- [prompt i odpowiedź](_przebieg/0072-autor-dodatkow.md) · 11.8 s · $0.0330

### 0073 · weryfikator_dodatków · dział 01 · pytanie 5

- Wynik: odrzucone: 1; Brakujące grosze w rozliczeniu: Wymyślona anegdota w pierwszej osobie, która powtarza temat wcześniejszego wpisu o dzieleniu kosztów i duplikuje wątek reszty groszy z samej sekcji; do tego „zaokrąglone do grosza” nie tłumaczy, czemu suma wyszła mniejsza (to działa tylko przy zaokrąglaniu w dół).
- [prompt i odpowiedź](_przebieg/0073-weryfikator-dodatkow.md) · 9.7 s · $0.0284

### 0074 · pisarz · dział 01 · pytanie 6 · próba 1

- Kolejka TODO (55): 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18 …
- Wynik: „Program a aplikacja”: 222 słów prozy, bez kodu; nowe hasła: aplikacja
- [prompt i odpowiedź](_przebieg/0074-pisarz.md) · 12.7 s · $0.0562

### 0075 · kontrola_deterministyczna · dział 01 · pytanie 6 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0076 · weryfikator_pojęć · dział 01 · pytanie 6 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **terminalu**: Czytelnik spoza IT nie wie, czym jest terminal. Wystarczy pół zdania, np. że to okno, w którym wpisuje się polecenia i widzi się tylko tekst, bez przycisków. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **skryptem**: Słowo „skrypt” nie ma hasła w glosariuszu. Kontekst podpowiada, że to mały program, ale warto dodać krótkie wyjaśnienie, np. „skrypt to bardzo krótki program do jednego zadania”. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0076-weryfikator-pojec.md) · 8.1 s · $0.0262

### 0077 · znudzony_czytelnik · dział 01 · pytanie 6 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `język` (sugestia) **skrypt, terminal**: Słowa „skrypt” i „terminal” pojawiają się bez wyjaśnienia. Osoba spoza IT może nie wiedzieć, czym jest „sam tekst w terminalu”. Wystarczy zastąpić je opisem, np. „krótki program bez okna, który wypisuje wynik jako zwykły tekst”. _← znudzony_czytelnik_
  - `skrócenie` (sugestia) **akapit „W praktyce granica jest płynna” i końcowa „Konsekwencja”**: Akapit o płynnej granicy i ostatnie zdanie „Konsekwencja” powtarzają to, co już wynika z tabeli i przykładu Wspólnej Kasy. Sekcja jest na granicy limitu 250 słów. Można je skrócić do jednego zdania. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0077-znudzony-czytelnik.md) · 10.4 s · $0.0254

### 0078 · strażnik_przykład · dział 01 · pytanie 6 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0078-straznik-przyklad.md) · 4.8 s · $0.0202

### 0079 · weryfikator_odwołań · dział 01 · pytanie 6 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 3)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **terminal**: Słowo „terminal” pojawia się w tabeli bez wyjaśnienia, a czytelnik spoza IT może go nie znać. Wystarczy krótkie dopowiedzenie, np. „okno, w którym widać tylko tekst”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0079-weryfikator-odwolan.md) · 12.1 s · $0.0366

### 0080 · decyzja · dział 01 · pytanie 6 · próba 1

- Wynik: Sekcja przyjęta; 5 sugestii trafia do raportu.
- 0.0 s

### 0081 · akceptacja · dział 01 · pytanie 6

- Wynik: Sekcja [sec-01-program-a-aplikacja] dopisana do działu 01; hasła w glosariuszu: aplikacja; odwołania: wstecz „„Wspólna Kasa”, przykład, który będzie nam towarzyszył”, w przód „pytania do użytkownika”, w przód „sprawdzanie danych”; punkty zaczepienia: Wspólna Kasa jako mały program; w TODO zostało 55.
- 0.0 s

### 0082 · autor_dodatków · dział 01 · pytanie 6

- Wynik: „Program a aplikacja”: dykteryjki: Skrypt, który wyszedł poza biurko autora
- [prompt i odpowiedź](_przebieg/0082-autor-dodatkow.md) · 9.1 s · $0.0320

### 0083 · weryfikator_dodatków · dział 01 · pytanie 6

- Wynik: odrzucone: 1; Skrypt, który wyszedł poza biurko autora: Puenta „kod się nie zmienił, tylko odbiorca” przeczy opowieści, w której autor dopisał sprawdzanie formatu i czytelne komunikaty, więc kod jednak się zmienił.
- [prompt i odpowiedź](_przebieg/0083-weryfikator-dodatkow.md) · 7.1 s · $0.0253

### 0084 · autor_wstępu · dział 02 · próba 1

- Kolejka TODO (55): 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18 …
- Wynik: Wstęp: 79 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0084-autor-wstepu.md) · 5.1 s · $0.0155

### 0085 · recenzent_wstępu · dział 02 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `język` (sugestia) **a te później staną się funkcjami**: Czytelnik spoza IT nie zna słowa „funkcje”, a wstęp go nie wyjaśnia. Lepiej napisać np. „a te później zamienimy w osobne fragmenty programu”. Można też po prostu skończyć na „podzielimy na części”. _← recenzent_wstępu_
  - `diagram` (sugestia) **strzałki w diagramie**: Strzałki nie mają opisu, a wygląda to na jednokierunkowy proces, w którym poprawność sprawdza się dopiero na końcu. Dodaj strzałkę powrotną od „sprawdzenia poprawności” do „kroków” z etykietą, np. „jeśli wynik zły – popraw kroki”. Wtedy nie powstanie błędne wrażenie, że wystarczy przejść listę raz. Możesz też dopisać pod diagramem jedno zdanie, że strzałka oznacza „następny etap pracy”. _← recenzent_wstępu_
  - `diagram` (sugestia) **„algorytm (kroki)”**: Nawias jest niejasny: czy „kroki” to inna nazwa algorytmu, czy jego część? W diagramie nie widać też kolejności kroków, choć wstęp ją obiecuje. Zapisz np. „algorytm (kroki w kolejności)”. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0085-recenzent-wstepu.md) · 12.8 s · $0.0231

### 0086 · pisarz · dział 02 · pytanie 7 · próba 1

- Kolejka TODO (54): 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19 …
- Wynik: „Czym jest algorytm”: 144 słów prozy, ```text 6 linii; nowe hasła: algorytm
- [prompt i odpowiedź](_przebieg/0086-pisarz.md) · 18.5 s · $0.0643

### 0087 · kontrola_deterministyczna · dział 02 · pytanie 7 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0088 · weryfikator_pojęć · dział 02 · pytanie 7 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **danych wejściowych**: wystarczy jedno zdanie; pełne omówienie w pytaniu 44. Przy pierwszym użyciu warto dodać, że dane wejściowe to informacje, które algorytm dostaje na start (tu: wydatki i liczba osób). _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **Pythonie**: Nazwa Pythona pojawia się bez wyjaśnienia. Wystarczy dopisać „(jeden z języków programowania)”. Czytelnik i tak zrozumie sens zdania. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0088-weryfikator-pojec.md) · 8.2 s · $0.0258

### 0089 · znudzony_czytelnik · dział 02 · pytanie 7 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **blok text z krokami rozliczenia**: Algorytm jest podany tylko ogólnie. Dwie–trzy linie z liczbami by go uruchomiły, np. wydatki 100, 60, 40, 0 zł, suma 200, udział 50 zł, salda +50, +10, −10, −50. Wtedy czytelnik zobaczy, że kroki naprawdę dają wynik. Wystarczy zastąpić część zdania o „ręcznym wykonaniu”, więc limit słów zostaje. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0089-znudzony-czytelnik.md) · 8.9 s · $0.0227

### 0090 · strażnik_przykład · dział 02 · pytanie 7 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **„Resztę groszy dopisz pierwszej osobie” / „lista kroków z wcześniejszej sekcji”**: Tekst odwołuje się do listy kroków z wcześniejszej sekcji i cytuje z niej krok o groszach. Kanon jest pusty ("jeszcze nic"), więc czytelnik nie widział żadnej takiej listy. Jedyna lista w sekcji (4 kroki) nie ma kroku o groszach. Popraw: albo usuń odwołanie i weź przykład z listy poniżej, albo dodaj do listy krok o groszach. Przykład jednoznacznego kroku może też brzmieć „Podziel sumę przez liczbę osób”. _← strażnik_przykład_
  - `spójność` (sugestia) **czworo znajomych / dane**: Tekst mówi o czworgu znajomych, ale nie podaje żadnych imion ani kwot. To drobna niespójność z późniejszym kodem (wydatki, osoby). Warto dać krótki konkretny zestaw, np. 4 osoby i kilka wydatków, żeby algorytm dało się prześledzić. Wątek wymaga też schematu blokowego (zsumuj, podziel, porównaj) i podziału na części, które staną się funkcjami (suma_wydatkow, udzial_na_osobe, saldo_osoby). W tej sekcji ich nie ma, więc można je zapowiedzieć. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0090-straznik-przyklad.md) · 12.4 s · $0.0274

### 0091 · weryfikator_odwołań · dział 02 · pytanie 7 · próba 1

- Wynik: Brak uwag. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0091-weryfikator-odwolan.md) · 9.3 s · $0.0346

### 0092 · decyzja · dział 02 · pytanie 7 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **„Resztę groszy dopisz pierwszej osobie” / „lista kroków z wcześniejszej sekcji”**: Tekst odwołuje się do listy kroków z wcześniejszej sekcji i cytuje z niej krok o groszach. Kanon jest pusty ("jeszcze nic"), więc czytelnik nie widział żadnej takiej listy. Jedyna lista w sekcji (4 kroki) nie ma kroku o groszach. Popraw: albo usuń odwołanie i weź przykład z listy poniżej, albo dodaj do listy krok o groszach. Przykład jednoznacznego kroku może też brzmieć „Podziel sumę przez liczbę osób”. _← strażnik_przykład_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 4 sugestii trafia do raportu.
- 0.0 s

### 0093 · pisarz · dział 02 · pytanie 7 · próba 2

- Kolejka TODO (54): 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19 …
- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **„Resztę groszy dopisz pierwszej osobie” / „lista kroków z wcześniejszej sekcji”**: Tekst odwołuje się do listy kroków z wcześniejszej sekcji i cytuje z niej krok o groszach. Kanon jest pusty ("jeszcze nic"), więc czytelnik nie widział żadnej takiej listy. Jedyna lista w sekcji (4 kroki) nie ma kroku o groszach. Popraw: albo usuń odwołanie i weź przykład z listy poniżej, albo dodaj do listy krok o groszach. Przykład jednoznacznego kroku może też brzmieć „Podziel sumę przez liczbę osób”. _← strażnik_przykład_
- Wynik: „Czym jest algorytm”: 146 słów prozy, ```text 6 linii; nowe hasła: algorytm
- [prompt i odpowiedź](_przebieg/0093-pisarz.md) · 12.4 s · $0.0648

### 0094 · kontrola_deterministyczna · dział 02 · pytanie 7 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0095 · weryfikator_pojęć · dział 02 · pytanie 7 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **danych wejściowych**: wystarczy jedno zdanie; pełne omówienie w pytaniu 44. Np. dane wejściowe to informacje, które podajemy na początku, a algorytm na ich podstawie liczy wynik (w przykładzie: wydatki i liczba osób). _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0095-weryfikator-pojec.md) · 6.9 s · $0.0251

### 0096 · znudzony_czytelnik · dział 02 · pytanie 7 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **blok tekstowy z algorytmem rozliczenia**: Algorytm rozliczenia jest podany bez liczb, więc trudno sprawdzić, czy kroki działają. Wystarczy jedna linia z danymi, np. wydatki 100, 60, 0, 40 zł: suma 200, udział 50, salda +50, +10, −50, −10. Można to zrobić kosztem zdania „Na razie nie piszemy kodu…”, żeby zmieścić się w limicie słów. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0096-znudzony-czytelnik.md) · 7.3 s · $0.0216

### 0097 · strażnik_przykład · dział 02 · pytanie 7 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **„Resztę groszy dopisz pierwszej osobie” / „lista kroków z wcześniejszej sekcji”**: Tekst odwołuje się do listy kroków z wcześniejszej sekcji i cytuje z niej krok o groszach. Kanon jest pusty ("jeszcze nic"), więc czytelnik nie widział żadnej takiej listy. Jedyna lista w sekcji (4 kroki) nie ma kroku o groszach. Popraw: albo usuń odwołanie i weź przykład z listy poniżej, albo dodaj do listy krok o groszach. Przykład jednoznacznego kroku może też brzmieć „Podziel sumę przez liczbę osób”. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0097-straznik-przyklad.md) · 2.5 s · $0.0196

### 0098 · weryfikator_odwołań · dział 02 · pytanie 7 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/0098-weryfikator-odwolan.md) · 8.6 s · $0.0326

### 0099 · decyzja · dział 02 · pytanie 7 · próba 2

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 0100 · akceptacja · dział 02 · pytanie 7

- Wynik: Sekcja [sec-02-czym-jest-algorytm] dopisana do działu 02; hasła w glosariuszu: algorytm; odwołania: wstecz „czworo znajomych na wyjeździe, którzy płacili na zmianę”, w przód „Na razie nie piszemy kodu”; punkty zaczepienia: algorytm rozliczenia w czterech krokach; w TODO zostało 54.
- 0.0 s

### 0101 · autor_dodatków · dział 02 · pytanie 7

- Wynik: „Czym jest algorytm”: dygresje: Skąd wzięło się słowo „algorytm”
- [prompt i odpowiedź](_przebieg/0101-autor-dodatkow.md) · 13.4 s · $0.0369

### 0102 · weryfikator_dodatków · dział 02 · pytanie 7

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0102-weryfikator-dodatkow.md) · 12.8 s · $0.0981

### 0103 · pisarz · dział 02 · pytanie 8 · próba 1

- Kolejka TODO (53): 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20 …
- Wynik: „Przepis jako algorytm”: 183 słów prozy, bez kodu
- [prompt i odpowiedź](_przebieg/0103-pisarz.md) · 21.5 s · $0.0815

### 0104 · kontrola_deterministyczna · dział 02 · pytanie 8 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **lm-8**: Oznaczenie [[lm-8]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 0105 · weryfikator_pojęć · dział 02 · pytanie 8 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **warunek zakończenia**: Termin pojawia się tylko w tabeli, jako odpowiednik „piecz, aż się zrumieni”. Wystarczy jedno zdanie, że to sprawdzenie, czy można przestać powtarzać czynność (pełne omówienie przy pętlach, pytania 32 i 34). _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **Pythonie**: Czytelnik spoza IT nie wie, czym jest Python. Wystarczy dopisać „(jeden z języków programowania)”. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0105-weryfikator-pojec.md) · 7.6 s · $0.0257

### 0106 · znudzony_czytelnik · dział 02 · pytanie 8 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `konkret` (blokująca) **tabela, wiersz „piecz, aż się zrumieni”**: Tabela podaje „piecz, aż się zrumieni” jako wzorcowy warunek zakończenia. Tymczasem „zrumieni się” jest tak samo niejednoznaczne jak „smaż chwilę”, które tekst niżej krytykuje. Czytelnik może uznać, że takie zdanie nadaje się do algorytmu. Trzeba dać wersję mierzalną, np. „piecz 40 minut w 180°C” albo „piecz, aż temperatura w środku wyniesie 95°C”. Warto też jednym zdaniem wyjaśnić, że warunek zakończenia to sprawdzalny test „czy już koniec?”. _← znudzony_czytelnik_
  - `tempo` (sugestia) **akapity o wykonaniu w Pythonie/arkuszu i o „Wspólnej Kasie”**: Akapit „ten sam przepis w różnych kuchniach” powtarza to, co poprzednia sekcja już powiedziała o Pythonie, arkuszu i kartce. Akapit o „Wspólnej Kasie” też niewiele dodaje, bo cztery kroki rozliczenia były już podane. Można je skrócić do jednego zdania albo usunąć i zwolnić miejsce na mierzalny przykład kroku przepisu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0106-znudzony-czytelnik.md) · 11.7 s · $0.0262

### 0107 · strażnik_przykład · dział 02 · pytanie 8 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **„cztery kroki rozliczenia, które już znasz”**: Zapowiedziany w wątku algorytm to trzy kroki: zsumuj, podziel, porównaj wpłaty z udziałem. Tu jest mowa o czterech krokach, które czytelnik „już zna”. Kanon jest pusty, więc nic jeszcze ich nie pokazało. Popraw: albo zgodnie z wątkiem napisz o trzech krokach (zsumuj, podziel, porównaj) i zapowiedz, że zaraz je rozpiszesz, albo wymień cztery kroki wprost, jeśli poprzedni dział rzeczywiście je podał. Sprawdź też, czy odwołanie lm-8 prowadzi do takiego działu. _← strażnik_przykład_
  - `spójność` (sugestia) **„danie” to saldo każdego**: Wynik zgadza się z wątkiem, bo saldo osoby jest wynikiem rozliczenia i później stanie się funkcją saldo_osoby. Sekcja nie zawiera kodu, więc nie ma sprzeczności z kanonem. Nazwy funkcji nie są potrzebne w tej sekcji. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0107-straznik-przyklad.md) · 10.2 s · $0.0255

### 0108 · weryfikator_odwołań · dział 02 · pytanie 8 · próba 1

- Wynik: 0 blokujących, 3 sugestii. (odwołania: 3)
- Nowe potrzeby (3):
  - `odwołanie` (sugestia) **warunek zakończenia**: W tabeli „piecz, aż się zrumieni” to „warunek zakończenia”, ale pojęcie nie ma hasła w glosariuszu ani wyjaśnienia w tekście. Dodaj jedno zdanie, np. że to sprawdzenie, kiedy przestać powtarzać krok. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **tabela, wiersz „piecz, aż się zrumieni”**: „Piecz, aż się zrumieni” jest podane jako przykład kroku luźnego i zarazem jako odpowiednik warunku zakończenia w algorytmie. Czytelnik może się pogubić, bo „zrumieni się” jest niejednoznaczne. Zamień na dokładny warunek, np. „piecz 40 minut w 180 °C”, albo powiedz, że w algorytmie warunek musi być sprawdzalny. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **saldo każdego**: Słowo „saldo” w zdaniu o „daniu” Wspólnej Kasy nie jest wyjaśnione w tej sekcji ani w glosariuszu. Dodaj krótkie objaśnienie, np. ile ktoś jest winien albo ile mu się należy. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0108-weryfikator-odwolan.md) · 17.3 s · $0.0440

### 0109 · decyzja · dział 02 · pytanie 8 · próba 1

- Potrzeby w kolejce przed krokiem (2):
  - `wyjaśnienie` (blokująca) **lm-8**: Oznaczenie [[lm-8]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `konkret` (blokująca) **tabela, wiersz „piecz, aż się zrumieni”**: Tabela podaje „piecz, aż się zrumieni” jako wzorcowy warunek zakończenia. Tymczasem „zrumieni się” jest tak samo niejednoznaczne jak „smaż chwilę”, które tekst niżej krytykuje. Czytelnik może uznać, że takie zdanie nadaje się do algorytmu. Trzeba dać wersję mierzalną, np. „piecz 40 minut w 180°C” albo „piecz, aż temperatura w środku wyniesie 95°C”. Warto też jednym zdaniem wyjaśnić, że warunek zakończenia to sprawdzalny test „czy już koniec?”. _← znudzony_czytelnik_
- Wynik: Do poprawy: 2 blokujących potrzeb wraca do pisarza; 8 sugestii trafia do raportu.
- 0.0 s

### 0110 · pisarz · dział 02 · pytanie 8 · próba 2

- Kolejka TODO (53): 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20 …
- Potrzeby w kolejce przed krokiem (2):
  - `wyjaśnienie` (blokująca) **lm-8**: Oznaczenie [[lm-8]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `konkret` (blokująca) **tabela, wiersz „piecz, aż się zrumieni”**: Tabela podaje „piecz, aż się zrumieni” jako wzorcowy warunek zakończenia. Tymczasem „zrumieni się” jest tak samo niejednoznaczne jak „smaż chwilę”, które tekst niżej krytykuje. Czytelnik może uznać, że takie zdanie nadaje się do algorytmu. Trzeba dać wersję mierzalną, np. „piecz 40 minut w 180°C” albo „piecz, aż temperatura w środku wyniesie 95°C”. Warto też jednym zdaniem wyjaśnić, że warunek zakończenia to sprawdzalny test „czy już koniec?”. _← znudzony_czytelnik_
- Wynik: „Przepis jako algorytm”: 215 słów prozy, bez kodu; nowe hasła: warunek zakończenia
- [prompt i odpowiedź](_przebieg/0110-pisarz.md) · 11.2 s · $0.0653

### 0111 · kontrola_deterministyczna · dział 02 · pytanie 8 · próba 2

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca, niespełniona) **lm-8**: Oznaczenie [[lm-8]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 0112 · weryfikator_pojęć · dział 02 · pytanie 8 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **Pythonie**: Python pada bez wyjaśnienia. Wystarczy pół zdania, np. „Python – jeden z języków programowania”. Bez tego czytelnik może się zatrzymać, ale sens zdania (algorytm da się wykonać w różnych miejscach) jest zrozumiały dzięki „w arkuszu albo na kartce”. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0112-weryfikator-pojec.md) · 7.3 s · $0.0258

### 0113 · znudzony_czytelnik · dział 02 · pytanie 8 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `konkret` (blokująca) **tabela, wiersz „piecz, aż się zrumieni”**: Tabela podaje „piecz, aż się zrumieni” jako wzorcowy warunek zakończenia. Tymczasem „zrumieni się” jest tak samo niejednoznaczne jak „smaż chwilę”, które tekst niżej krytykuje. Czytelnik może uznać, że takie zdanie nadaje się do algorytmu. Trzeba dać wersję mierzalną, np. „piecz 40 minut w 180°C” albo „piecz, aż temperatura w środku wyniesie 95°C”. Warto też jednym zdaniem wyjaśnić, że warunek zakończenia to sprawdzalny test „czy już koniec?”. _← znudzony_czytelnik_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0113-znudzony-czytelnik.md) · 3.2 s · $0.0203

### 0114 · strażnik_przykład · dział 02 · pytanie 8 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **cztery kroki rozliczenia, które już znasz**: Kanon jest pusty, więc czytelnik nie widział jeszcze kroków rozliczenia „Wspólnej Kasy”. Opis wątku wymienia trzy kroki (zsumuj, podziel, porównaj wpłaty z udziałem), a tekst mówi o czterech. Popraw na „kroki, które zaraz zapiszemy” albo wypisz je w tekście i zgodnie z wątkiem ustal ich liczbę. Odwołanie [[lm-8]] może zostać, jeśli wcześniejszy materiał faktycznie je podał. _← strażnik_przykład_
  - `spójność` (sugestia) **Wspólna Kasa**: Przykład przewodni pojawia się tylko w jednym zdaniu, a reszta sekcji opiera się na przepisie kulinarnym. Wątek jest zachowany, bo nie ma obcej dziedziny ani kodu. Warto jednak dopisać jedną linię kroku rozliczenia, np. „Podziel sumę wydatków przez liczbę osób”, bo tym zdaniem sekcja sama ilustruje swoją tezę. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0114-straznik-przyklad.md) · 10.7 s · $0.0269

### 0115 · weryfikator_odwołań · dział 02 · pytanie 8 · próba 2

- Wynik: 1 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 3)
- Nowe potrzeby (2):
  - `odwołanie` (blokująca) **[[warunek-zakonczenia|warunek zakończenia]]**: Znacznik odsyła do hasła glosariusza „warunek-zakonczenia”, którego nie ma na liście haseł. Pojęcie jest zdefiniowane w tekście („sprawdzalny test »czy już koniec?«”), więc usuń znacznik linku i zostaw zwykły tekst „warunek zakończenia” (albo dodaj hasło do glosariusza). _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **ostatnie zdanie**: „kroki są dość dokładne” osłabia sedno sekcji, że w algorytmie nie ma miejsca na domysły. Lepiej: „kroki są wystarczająco dokładne”, albo „nie zostaje nic do dopowiedzenia”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0115-weryfikator-odwolan.md) · 15.4 s · $0.0422

### 0116 · decyzja · dział 02 · pytanie 8 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `wyjaśnienie` (blokująca, niespełniona) **lm-8**: Oznaczenie [[lm-8]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `odwołanie` (blokująca) **[[warunek-zakonczenia|warunek zakończenia]]**: Znacznik odsyła do hasła glosariusza „warunek-zakonczenia”, którego nie ma na liście haseł. Pojęcie jest zdefiniowane w tekście („sprawdzalny test »czy już koniec?«”), więc usuń znacznik linku i zostaw zwykły tekst „warunek zakończenia” (albo dodaj hasło do glosariusza). _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 2 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0117 · akceptacja · dział 02 · pytanie 8

- Wynik: Sekcja [sec-02-przepis-jako-algorytm] dopisana do działu 02; hasła w glosariuszu: warunek zakończenia; odwołania: wstecz „cztery kroki rozliczenia, które już znasz”, wstecz „Podziel sumę przez liczbę osób”, w przód „Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa””; punkty zaczepienia: przepis dla kogoś, kto nie gotował, mierzalny warunek pieczenia; w TODO zostało 53.
- 0.0 s

### 0118 · autor_dodatków · dział 02 · pytanie 8

- Wynik: „Przepis jako algorytm”: wtręty: Marta zapisuje warunek „aż będzie ładnie”, rysunki: Przepis dla kogoś, kto nigdy nie gotował
- [prompt i odpowiedź](_przebieg/0118-autor-dodatkow.md) · 15.6 s · $0.0398

### 0119 · weryfikator_dodatków · dział 02 · pytanie 8

- Wynik: odrzucone: 1; Marta zapisuje warunek „aż będzie ładnie”: Powtarza motyw wcześniejszego wpisu (Marta używa nieprecyzyjnego słowa, którego komputer nie potrafi zinterpretować, jak „sprawiedliwie”) i tylko odtwarza przykład „piecz, aż się zrumieni” z samej sekcji.
- [prompt i odpowiedź](_przebieg/0119-weryfikator-dodatkow.md) · 9.1 s · $0.0297

### 0120 · pisarz · dział 02 · pytanie 9 · próba 1

- Kolejka TODO (52): 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21 …
- Wynik: „Kolejność kroków algorytmu”: 160 słów prozy, ```text 2 linii; nowe hasła: zależność między krokami
- [prompt i odpowiedź](_przebieg/0120-pisarz.md) · 18.8 s · $0.0668

### 0121 · kontrola_deterministyczna · dział 02 · pytanie 9 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **lm-8**: Oznaczenie [[lm-8]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 0122 · weryfikator_pojęć · dział 02 · pytanie 9 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0122-weryfikator-pojec.md) · 2.6 s · $0.0170

### 0123 · znudzony_czytelnik · dział 02 · pytanie 9 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0123-znudzony-czytelnik.md) · 4.3 s · $0.0187

### 0124 · strażnik_przykład · dział 02 · pytanie 9 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0124-straznik-przyklad.md) · 4.1 s · $0.0190

### 0125 · weryfikator_odwołań · dział 02 · pytanie 9 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 1)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **cztery kroki rozliczenia**: Tekst nazywa „cztery kroki rozliczenia”, a w przykładzie wymienia tylko trzy (sumowanie, dzielenie, odejmowanie); policzenie osób pojawia się dopiero w dalszym akapicie. Warto od razu wymienić cztery kroki, np. dodać „policzmy osoby”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0125-weryfikator-odwolan.md) · 12.4 s · $0.0383

### 0126 · decyzja · dział 02 · pytanie 9 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **lm-8**: Oznaczenie [[lm-8]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 1 sugestii trafia do raportu.
- 0.0 s

### 0127 · pisarz · dział 02 · pytanie 9 · próba 2

- Kolejka TODO (52): 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21 …
- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **lm-8**: Oznaczenie [[lm-8]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- Wynik: „Kolejność kroków algorytmu”: 160 słów prozy, ```text 3 linii
- [prompt i odpowiedź](_przebieg/0127-pisarz.md) · 19.5 s · $0.0906

### 0128 · kontrola_deterministyczna · dział 02 · pytanie 9 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0129 · weryfikator_pojęć · dział 02 · pytanie 9 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0129-weryfikator-pojec.md) · 2.6 s · $0.0202

### 0130 · znudzony_czytelnik · dział 02 · pytanie 9 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0130-znudzony-czytelnik.md) · 5.0 s · $0.0193

### 0131 · strażnik_przykład · dział 02 · pytanie 9 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0131-straznik-przyklad.md) · 4.3 s · $0.0194

### 0132 · weryfikator_odwołań · dział 02 · pytanie 9 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **Weźmy cztery kroki rozliczenia**: Tekst zapowiada „cztery kroki rozliczenia”, ale w akapicie wymienia trzy (sumowanie, dzielenie, odejmowanie). Czwarty krok (policzenie osób) pojawia się dopiero niżej. Wymień wszystkie cztery od razu albo napisz, że tu pokazujemy trzy z nich. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0132-weryfikator-odwolan.md) · 11.6 s · $0.0372

### 0133 · decyzja · dział 02 · pytanie 9 · próba 2

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 0134 · akceptacja · dział 02 · pytanie 9

- Wynik: Sekcja [sec-02-kolejnosc-krokow-algorytmu] dopisana do działu 02; odwołania: wstecz „cztery kroki rozliczenia”, wstecz „we „Wspólnej Kasie””; punkty zaczepienia: odejmowanie przed policzeniem udziału; w TODO zostało 52.
- 0.0 s

### 0135 · autor_dodatków · dział 02 · pytanie 9

- Wynik: „Kolejność kroków algorytmu”: wtręty: Marta odejmuje udział, zanim go policzy, dykteryjki: Archiwizacja przed wygenerowaniem raportu
- [prompt i odpowiedź](_przebieg/0135-autor-dodatkow.md) · 12.9 s · $0.0369

### 0136 · weryfikator_dodatków · dział 02 · pytanie 9

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0136-weryfikator-dodatkow.md) · 10.1 s · $0.0301

### 0137 · pisarz · dział 02 · pytanie 10 · próba 1

- Kolejka TODO (51): 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22 …
- Wynik: „Czym jest schemat blokowy”: 140 słów prozy, ```text 22 linii; nowe hasła: schemat blokowy
- [prompt i odpowiedź](_przebieg/0137-pisarz.md) · 14.0 s · $0.0634

### 0138 · kontrola_deterministyczna · dział 02 · pytanie 10 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `skrócenie` (blokująca) **blok kodu 1**: Blok ma 22 linii, limit to 15. Pokaż tylko linie ilustrujące tezę, resztę zastąp `...`. _← kontrola_kodu_
- 0.0 s

### 0139 · weryfikator_pojęć · dział 02 · pytanie 10 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0139-weryfikator-pojec.md) · 3.5 s · $0.0216

### 0140 · znudzony_czytelnik · dział 02 · pytanie 10 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0140-znudzony-czytelnik.md) · 5.7 s · $0.0201

### 0141 · strażnik_przykład · dział 02 · pytanie 10 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0141-straznik-przyklad.md) · 4.6 s · $0.0198

### 0142 · weryfikator_odwołań · dział 02 · pytanie 10 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 4)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **diagram rozliczenia**: Na rysunku strzałka z „Ma zwrot” schodzi do linii z plusem i łączy się z linią spod „Ma dopłacić”, ale strzałka „Ma dopłacić” wskazuje w lewo/na plus, a dalej biegnie pionowa kreska do „Są jeszcze osoby?”. Czytelnik spoza IT może nie zobaczyć, że obie gałęzie schodzą się przed pytaniem. Warto dodać strzałkę wchodzącą do „Są jeszcze osoby?” z obu gałęzi albo jedno zdanie opisujące, że obie drogi się łączą. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **romb decyzyjny**: Pytanie „Wpłaciła więcej niż udział?” nie mówi, co z osobą, która wpłaciła dokładnie tyle, ile wynosi udział (trafia do „Ma dopłacić”). Można dodać krótką uwagę, że wtedy dopłata wynosi 0 zł. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0142-weryfikator-odwolan.md) · 17.3 s · $0.0463

### 0143 · decyzja · dział 02 · pytanie 10 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `skrócenie` (blokująca) **blok kodu 1**: Blok ma 22 linii, limit to 15. Pokaż tylko linie ilustrujące tezę, resztę zastąp `...`. _← kontrola_kodu_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 2 sugestii trafia do raportu.
- 0.0 s

### 0144 · pisarz · dział 02 · pytanie 10 · próba 2

- Kolejka TODO (51): 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22 …
- Potrzeby w kolejce przed krokiem (1):
  - `skrócenie` (blokująca) **blok kodu 1**: Blok ma 22 linii, limit to 15. Pokaż tylko linie ilustrujące tezę, resztę zastąp `...`. _← kontrola_kodu_
- Wynik: „Czym jest schemat blokowy”: 140 słów prozy, ```text 15 linii; nowe hasła: schemat blokowy
- [prompt i odpowiedź](_przebieg/0144-pisarz.md) · 25.1 s · $0.0834

### 0145 · kontrola_deterministyczna · dział 02 · pytanie 10 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0146 · weryfikator_pojęć · dział 02 · pytanie 10 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0146-weryfikator-pojec.md) · 3.8 s · $0.0215

### 0147 · znudzony_czytelnik · dział 02 · pytanie 10 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `fakt` (sugestia) **romb w diagramie**: Romb „Wpłaciła więcej niż udział?” przy odpowiedzi „nie” kieruje do „Ma dopłacić”. Osoba, która wpłaciła dokładnie swój udział, nie ma nic do dopłacenia. Wystarczy drobna zmiana, np. „Wpłaciła co najmniej tyle, ile udział?” albo krok „Ma dopłacić (lub 0 zł)”. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0147-znudzony-czytelnik.md) · 9.4 s · $0.0234

### 0148 · strażnik_przykład · dział 02 · pytanie 10 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0148-straznik-przyklad.md) · 3.4 s · $0.0188

### 0149 · weryfikator_odwołań · dział 02 · pytanie 10 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 4)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **warunek zakończenia**: Zdanie „pokazuje, gdzie algorytm się kończy, czyli sprawdzalny warunek zakończenia” myli owal „Koniec” z warunkiem. Warunkiem jest romb „Są jeszcze osoby?”. Lepiej napisać, że romb sprawdza, czy wolno zakończyć. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **diagram**: Romb „Wpłaciła więcej niż udział?” przy równej wpłacie kieruje na „Ma dopłacić”, co jest nieścisłe. Można zmienić pytanie na „Wpłaciła mniej niż udział?” albo dodać uwagę o równej kwocie. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0149-weryfikator-odwolan.md) · 14.1 s · $0.0437

### 0150 · decyzja · dział 02 · pytanie 10 · próba 2

- Wynik: Sekcja przyjęta; 3 sugestii trafia do raportu.
- 0.0 s

### 0151 · akceptacja · dział 02 · pytanie 10

- Wynik: Sekcja [sec-02-czym-jest-schemat-blokowy] dopisana do działu 02; hasła w glosariuszu: schemat blokowy; odwołania: wstecz „rozliczenie „Wspólnej Kasy” z trzema osobami”, w przód „Wrócimy do niego przy podziale problemu na części”, w przód „przykład, który będzie nam towarzyszył”, w przód „dostanie z niego kod dopiero później”; punkty zaczepienia: schemat rozliczenia z rombem; w TODO zostało 51.
- 0.0 s

### 0152 · autor_dodatków · dział 02 · pytanie 10

- Wynik: „Czym jest schemat blokowy”: dowcipy: Rondo bez zjazdu
- [prompt i odpowiedź](_przebieg/0152-autor-dodatkow.md) · 7.9 s · $0.0366

### 0153 · weryfikator_dodatków · dział 02 · pytanie 10

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0153-weryfikator-dodatkow.md) · 4.6 s · $0.0276

### 0154 · pisarz · dział 02 · pytanie 11 · próba 1

- Kolejka TODO (50): 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23 …
- Wynik: „Podział problemu na części”: 161 słów prozy, ```text 5 linii; nowe hasła: funkcja
- [prompt i odpowiedź](_przebieg/0154-pisarz.md) · 12.9 s · $0.0645

### 0155 · kontrola_deterministyczna · dział 02 · pytanie 11 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0156 · weryfikator_pojęć · dział 02 · pytanie 11 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **dane wejściowe**: wystarczy jedno zdanie; pełne omówienie w pytaniu 44. Przy pierwszym użyciu warto dodać, że dane wejściowe to informacje, które część dostaje na start (np. wydatki). Diagram częściowo to pokazuje, więc tekst jest zrozumiały. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0156-weryfikator-pojec.md) · 6.9 s · $0.0253

### 0157 · znudzony_czytelnik · dział 02 · pytanie 11 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `konkret` (sugestia) **Dobra część daje się przetestować samodzielnie**: Zdanie „znasz jej dane i wiesz, jaki wynik ma wyjść” jest ogólnikiem. Wystarczy jedna liczbowa próba, np. wydatki 30, 50 i 20 zł dają sumę 100 zł, a przy 4 osobach udział wynosi 25 zł. Wtedy czytelnik zobaczy, co znaczy „sprawdzić osobno”. _← znudzony_czytelnik_
  - `skrócenie` (sugestia) **Ostatni akapit („Konsekwencja”)**: Zdanie o „Wspólnej Kasie”, przykładzie na kolejne działy, powtarza końcówkę poprzedniej sekcji. Można je usunąć, a zwolnione miejsce przeznaczyć na liczbowy przykład. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0157-znudzony-czytelnik.md) · 8.6 s · $0.0233

### 0158 · strażnik_przykład · dział 02 · pytanie 11 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0158-straznik-przyklad.md) · 4.1 s · $0.0191

### 0159 · weryfikator_odwołań · dział 02 · pytanie 11 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 5)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **saldo**: Słowo „saldo” pojawia się na diagramie bez wyjaśnienia. Dodaj krótko, że to różnica między wpłatą a udziałem (ile osoba ma dostać lub dopłacić). _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **przetestować samodzielnie**: Zdanie, że część da się przetestować samodzielnie, warto poprzeć liczbami, np. wydatki 60, 40 i 20 zł dają sumę 120 zł. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0159-weryfikator-odwolan.md) · 13.2 s · $0.0434

### 0160 · decyzja · dział 02 · pytanie 11 · próba 1

- Wynik: Sekcja przyjęta; 5 sugestii trafia do raportu.
- 0.0 s

### 0161 · akceptacja · dział 02 · pytanie 11

- Wynik: Sekcja [sec-02-podzial-problemu-na-czesci] dopisana do działu 02; hasła w glosariuszu: funkcja; odwołania: wstecz „schematu blokowego z poprzedniej sekcji”, wstecz „tak jak w sekcji o kolejności kroków”, w przód „takie części zamienimy w osobne”, w przód „Ich nazwy, np. `suma_wydatkow`, poznasz później”, w przód „przykład, który będzie nam towarzyszył w kolejnych działach”; punkty zaczepienia: drzewo podziału rozliczenia; w TODO zostało 50.
- 0.0 s

### 0162 · autor_dodatków · dział 02 · pytanie 11

- Wynik: „Podział problemu na części”: wtręty: Marta zleca całe rozliczenie jednym zdaniem, dykteryjki: Funkcja, która robiła wszystko naraz
- [prompt i odpowiedź](_przebieg/0162-autor-dodatkow.md) · 10.4 s · $0.0391

### 0163 · weryfikator_dodatków · dział 02 · pytanie 11

- Wynik: odrzucone: 1; Funkcja, która robiła wszystko naraz: Powtarza temat i puentę dodatku 0 (monolit rozbity na trzy części, dzięki czemu znaleziono błąd w jednej z nich) i tylko streszcza sekcję, a do tego zawiera błąd językowy „w wczytywaniu”.
- [prompt i odpowiedź](_przebieg/0163-weryfikator-dodatkow.md) · 10.3 s · $0.0404

### 0164 · pisarz · dział 02 · pytanie 12 · próba 1

- Kolejka TODO (49): 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24 …
- Wynik: „Poprawny algorytm”: 172 słów prozy, ```text 6 linii, ```text 2 linii; nowe hasła: specyfikacja wyniku, przypadek brzegowy
- [prompt i odpowiedź](_przebieg/0164-pisarz.md) · 32.1 s · $0.1170

### 0165 · kontrola_deterministyczna · dział 02 · pytanie 12 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0166 · weryfikator_pojęć · dział 02 · pytanie 12 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (blokująca) **dzielenie całkowite**: Wystarczy jedno zdanie; pełne omówienie w pytaniu 26. Czytelnik nie wie, że znak // dzieli i odrzuca resztę (10000 // 3 daje 3333, nie 3333,33). Bez tego nie zrozumie, dlaczego wychodzi 9999, a to sedno przykładu. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **print**: Wystarczy jedno zdanie; pełne omówienie w pytaniu 45. Czytelnik nie wie, że print wyświetla wartość na ekranie i że dwie liczby pod kodem to jego wyniki. Warto też jednym zdaniem powiedzieć, że def i return tworzą funkcję i zwracają wynik (pytania 38 i 41). _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0166-weryfikator-pojec.md) · 10.3 s · $0.0287

### 0167 · znudzony_czytelnik · dział 02 · pytanie 12 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **blok kodu z udzial(), dzielenie całkowite `//`**: Kod używa `//`, `def`, `return` i `print`, a tekst nie mówi, co robią. Wystarczy jedno zdanie, np.: `//` odrzuca resztę, więc 10000 // 3 daje 3333, a nie 3333,33. Bez tego wynik 9999 trzeba zgadywać. Uwaga: nie dodawaj tego bez skrócenia czegoś innego, bo limit słów jest ciasny. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0167-znudzony-czytelnik.md) · 8.5 s · $0.0223

### 0168 · strażnik_przykład · dział 02 · pytanie 12 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **lista kroków algorytmu rozliczenia**: Tekst powołuje się na „naszą listę kroków” ze zdaniem „Resztę groszy dopisz pierwszej osobie.”, ale kanon jest pusty, więc nie ma potwierdzenia, że taka lista i takie zdanie już się pojawiły. Upewnij się, że wcześniejsza sekcja tego działu zawiera dokładnie ten krok. Jeśli nie, dopisz go tutaj albo zmień zdanie na „do listy kroków dopiszemy”. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0168-straznik-przyklad.md) · 8.9 s · $0.0244

### 0169 · weryfikator_odwołań · dział 02 · pytanie 12 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **udzial(suma_gr, osoby) i „//”**: W kodzie użyto „//” bez objaśnienia. Komentarz mówi „dzielenie całkowite”, ale czytelnik spoza IT może nie wiedzieć, że to dzielenie z odrzuceniem reszty. Warto dodać jedno zdanie po kodzie, np. że 10000 // 3 daje 3333, a reszta 1 gr przepada. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **komentarz w kodzie**: Komentarz „# poza kanonem” jest żargonem autora i czytelnik go nie zrozumie. Lepiej go usunąć albo zamienić na zwykłe zdanie, np. „kod tylko do obejrzenia, nie trzeba go rozumieć”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0169-weryfikator-odwolan.md) · 13.0 s · $0.0428

### 0170 · decyzja · dział 02 · pytanie 12 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **dzielenie całkowite**: Wystarczy jedno zdanie; pełne omówienie w pytaniu 26. Czytelnik nie wie, że znak // dzieli i odrzuca resztę (10000 // 3 daje 3333, nie 3333,33). Bez tego nie zrozumie, dlaczego wychodzi 9999, a to sedno przykładu. _← weryfikator_pojęć_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 5 sugestii trafia do raportu.
- 0.0 s

### 0171 · pisarz · dział 02 · pytanie 12 · próba 2

- Kolejka TODO (49): 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24 …
- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **dzielenie całkowite**: Wystarczy jedno zdanie; pełne omówienie w pytaniu 26. Czytelnik nie wie, że znak // dzieli i odrzuca resztę (10000 // 3 daje 3333, nie 3333,33). Bez tego nie zrozumie, dlaczego wychodzi 9999, a to sedno przykładu. _← weryfikator_pojęć_
- Wynik: „Poprawny algorytm”: 192 słów prozy, ```python 6 linii, ```text 2 linii; nowe hasła: specyfikacja wyniku, przypadek brzegowy
- [prompt i odpowiedź](_przebieg/0171-pisarz.md) · 14.9 s · $0.0753

### 0172 · kontrola_deterministyczna · dział 02 · pytanie 12 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0173 · weryfikator_pojęć · dział 02 · pytanie 12 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **dzielenie całkowite**: Wystarczy jedno zdanie; pełne omówienie w pytaniu 26. Czytelnik nie wie, że znak // dzieli i odrzuca resztę (10000 // 3 daje 3333, nie 3333,33). Bez tego nie zrozumie, dlaczego wychodzi 9999, a to sedno przykładu. _← weryfikator_pojęć_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0173-weryfikator-pojec.md) · 2.9 s · $0.0225

### 0174 · znudzony_czytelnik · dział 02 · pytanie 12 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0174-znudzony-czytelnik.md) · 5.2 s · $0.0198

### 0175 · strażnik_przykład · dział 02 · pytanie 12 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **lista kroków / kwoty w groszach**: Tekst powołuje się na „naszą listę kroków” ze zdaniem „Resztę groszy dopisz pierwszej osobie.” oraz na to, że „w kodzie kwoty liczymy w groszach”. Kanon jest pusty, więc nie wiadomo, czy wcześniejsze sekcje to pokazały. Upewnij się, że lista kroków z tym zdaniem i konwencja groszy pojawiły się wcześniej w dziale. Jeśli nie, dopisz to zdanie w tej sekcji albo przenieś je do sekcji z listą kroków. Kod jest oznaczony „poza kanonem”, więc nazwa `udzial` (zamiast planowanego `udzial_na_osobe`) nie jest problemem. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0175-straznik-przyklad.md) · 9.9 s · $0.0258

### 0176 · weryfikator_odwołań · dział 02 · pytanie 12 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **komentarz w bloku kodu**: Komentarz w kodzie „# poza kanonem” to wewnętrzna uwaga autora, niezrozumiała dla czytelnika. Zastąp go np. „# udział w groszach, dzielenie całkowite” bez słowa o kanonie. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **def udzial(...)**: Kod używa `def` i `return`, których czytelnik może jeszcze nie znać. Wystarczy jedno zdanie, że to mała funkcja zwracająca udział jednej osoby. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0176-weryfikator-odwolan.md) · 13.1 s · $0.0422

### 0177 · sprawdzacz_wyników · dział 02 · pytanie 12 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0177-sprawdzacz-wynikow.md) · 4.0 s · $0.0146

### 0178 · weryfikator_faktów · dział 02 · pytanie 12 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0178-weryfikator-faktow.md) · 4.6 s · $0.0284

### 0179 · decyzja · dział 02 · pytanie 12 · próba 2

- Wynik: Sekcja przyjęta; 3 sugestii trafia do raportu.
- 0.0 s

### 0180 · akceptacja · dział 02 · pytanie 12

- Wynik: Sekcja [sec-02-poprawny-algorytm] dopisana do działu 02; hasła w glosariuszu: specyfikacja wyniku, przypadek brzegowy; odwołania: wstecz „w naszej liście kroków jest zdanie „Resztę groszy dopisz pierwszej osobie.””, w przód „Do systematycznego sprawdzania wrócimy przy testowaniu programu”; punkty zaczepienia: brakujący grosz; w TODO zostało 49.
- 0.0 s

### 0181 · łowca_pułapek · dział 02 · pytanie 12

- Wynik: „Poprawny algorytm”: brak pułapek
- [prompt i odpowiedź](_przebieg/0181-lowca-pulapek.md) · 2.2 s · $0.0136

### 0182 · autor_dodatków · dział 02 · pytanie 12

- Wynik: „Poprawny algorytm”: dykteryjki: Brakujący grosz w zestawieniu miesięcznym
- [prompt i odpowiedź](_przebieg/0182-autor-dodatkow.md) · 10.3 s · $0.0406

### 0183 · weryfikator_dodatków · dział 02 · pytanie 12

- Wynik: odrzucone: 1; Brakujący grosz w zestawieniu miesięcznym: Dykteryjka tylko powtarza przykład z sekcji (odrzucana reszta z dzielenia całkowitego, test na danych niepodzielnych) i nie wnosi nowej sceny, do tego zawiera literówkę „dzielenim” zamiast „dzieleniem”.
- [prompt i odpowiedź](_przebieg/0183-weryfikator-dodatkow.md) · 9.6 s · $0.0366

### 0184 · autor_wstępu · dział 03 · próba 1

- Kolejka TODO (49): 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24 …
- Wynik: Wstęp: 67 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0184-autor-wstepu.md) · 4.7 s · $0.0181

### 0185 · recenzent_wstępu · dział 03 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `wyjaśnienie` (sugestia) **„Wspólnej Kasy” i plik kasa.py**: Czytelnik może nie pamiętać, czym jest „Wspólna Kasa” z poprzednich działów. Warto dodać pół zdania przypominającego, np. że to przykład, który rozwijamy od początku tutoriala. Nazwa pliku kasa.py z rozszerzeniem .py jest niewyjaśniona, ale to zapowiedź, więc nie blokuje. _← recenzent_wstępu_
  - `diagram` (sugestia) **diagram: „kod w pliku → interpreter”**: Diagram jest zrozumiały i zgodny z tematem działu. Strzałki oznaczają kolejne etapy, a kierunek jest oczywisty. Można go ulepszyć przez etykiety przy strzałkach, np. „zapisujesz w edytorze” i „uruchamiasz”. Wtedy widać, że edytor też jest w tym procesie. Obecnie edytor, o którym mówi wstęp, na diagramie nie występuje. _← recenzent_wstępu_
  - `spójność` (sugestia) **„Po tym dziale będziesz wiedzieć … Nauczysz się też …”**: Dwa zdania z zapowiedzią umiejętności brzmią jak wyliczenie. Można je połączyć w jedno i zapowiedzieć działanie zamiast wiedzy, np. „napiszesz, uruchomisz i naprawisz krótki program”. To tylko poprawa stylu. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0185-recenzent-wstepu.md) · 7.5 s · $0.0187

### 0186 · pisarz · dział 03 · pytanie 13 · próba 1

- Kolejka TODO (48): 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25 …
- Wynik: „Czym jest kod źródłowy”: 149 słów prozy, ```python 3 linii, ```text 2 linii; nowe hasła: kod źródłowy; wątki: przykład dodaj rozlicz.py
- [prompt i odpowiedź](_przebieg/0186-pisarz.md) · 22.8 s · $0.0738

### 0187 · kontrola_deterministyczna · dział 03 · pytanie 13 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0188 · weryfikator_pojęć · dział 03 · pytanie 13 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **print**: W przykładzie pojawia się print(...) bez słowa wyjaśnienia. Wystarczy jedno zdanie, że print wyświetla na ekranie to, co jest w nawiasie. Print to funkcja, a jej pełne omówienie jest w pytaniu 38. Wynik można też zrozumieć z samego przykładu, więc to tylko sugestia. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0188-weryfikator-pojec.md) · 8.9 s · $0.0255

### 0189 · znudzony_czytelnik · dział 03 · pytanie 13 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **blok kodu rozlicz.py**: Kod używa print i dzielenia `/`, ale nie mówi, że print wyświetla tekst na ekranie. Warto dodać jedno zdanie pod wynikiem. Można też wyjaśnić, dlaczego wychodzi `100.0`, a nie `100`. Poprzednia sekcja użyła `//`, więc czytelnik może się zdziwić. _← znudzony_czytelnik_
  - `skrócenie` (sugestia) **akapit o rozszerzeniu .py**: Zdanie „Taki plik będzie miał nasz przykład, który będzie nam towarzyszył” jest niezgrabne i powtarza „będzie”. Lepiej: „Tak nazwiemy plik naszego przykładu „Wspólna Kasa”.” _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0189-znudzony-czytelnik.md) · 8.1 s · $0.0232

### 0190 · strażnik_przykład · dział 03 · pytanie 13 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0190-straznik-przyklad.md) · 5.2 s · $0.0198

### 0191 · weryfikator_odwołań · dział 03 · pytanie 13 · próba 1

- Wynik: 0 blokujących, 3 sugestii. (odwołania: 3)
- Nowe potrzeby (3):
  - `odwołanie` (sugestia) **Ten sam algorytm, który wcześniej opisywaliśmy**: Kod w przykładzie liczy tylko 300 / 3, a nie cały algorytm rozliczenia z czterech kroków, więc „ten sam algorytm” trochę przesadza. Lepiej napisać, że to pierwszy krok algorytmu (podział sumy przez liczbę osób) zapisany w Pythonie. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **print(300 / 3)**: Czytelnik spoza IT nie wie, co robi print ani skąd wynik 100.0 (kropka, „.0”). Jedno zdanie pod kodem by to wyjaśniło: print wyświetla tekst lub wynik na ekranie, a 300 / 3 to dzielenie. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **rozszerzeniu zależnym od języka**: „Rozszerzenie pliku” (.py) nie jest wyjaśnione. Wystarczy dopisać, że to końcówka nazwy po kropce, po której widać rodzaj pliku. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0191-weryfikator-odwolan.md) · 14.2 s · $0.0400

### 0192 · sprawdzacz_wyników · dział 03 · pytanie 13 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0192-sprawdzacz-wynikow.md) · 3.7 s · $0.0135

### 0193 · weryfikator_faktów · dział 03 · pytanie 13 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0193-weryfikator-faktow.md) · 5.0 s · $0.0276

### 0194 · decyzja · dział 03 · pytanie 13 · próba 1

- Wynik: Sekcja przyjęta; 6 sugestii trafia do raportu.
- 0.0 s

### 0195 · akceptacja · dział 03 · pytanie 13

- Wynik: Sekcja [sec-03-czym-jest-kod-zrodlowy] dopisana do działu 03; hasła w glosariuszu: kod źródłowy; kanony: przykład:+rozlicz.py; odwołania: wstecz „Ten sam algorytm, który wcześniej opisywaliśmy słowami i schematem”, w przód „jak to działa, pokażemy przy uruchamianiu programu”, w przód „nasz przykład, który będzie nam towarzyszył”; punkty zaczepienia: kod jako zwykły plik tekstowy; w TODO zostało 48.
- 0.0 s

### 0196 · łowca_pułapek · dział 03 · pytanie 13

- Wynik: „Czym jest kod źródłowy”: brak pułapek
- [prompt i odpowiedź](_przebieg/0196-lowca-pulapek.md) · 2.1 s · $0.0127

### 0197 · autor_dodatków · dział 03 · pytanie 13

- Wynik: „Czym jest kod źródłowy”: wtręty: Marta zapisuje program jak dokument, dykteryjki: Cudzysłowy skopiowane z dokumentu
- [prompt i odpowiedź](_przebieg/0197-autor-dodatkow.md) · 15.4 s · $0.0449

### 0198 · weryfikator_dodatków · dział 03 · pytanie 13

- Wynik: odrzucone: 1; Marta zapisuje program jak dokument: Python nie otwiera pliku .docx i nie "znajduje" w nim ustawień stron, tylko zgłasza błąd, bo .docx to spakowany format, więc opis jest technicznie nieprawdziwy i niespójny (plik .py zapisany jako .docx).
- [prompt i odpowiedź](_przebieg/0198-weryfikator-dodatkow.md) · 8.0 s · $0.0350

### 0199 · pisarz · dział 03 · pytanie 14 · próba 1

- Kolejka TODO (47): 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26 …
- Wynik: „Do czego służy edytor”: 200 słów prozy, bez kodu; nowe hasła: edytor kodu, podświetlanie składni; warsztat: $ python --version, kasa.py
- [prompt i odpowiedź](_przebieg/0199-pisarz.md) · 18.6 s · $0.0705

### 0200 · kontrola_deterministyczna · dział 03 · pytanie 14 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **sec-03-czym-jest-kod-zrodlowy**: Oznaczenie [[sec-03-czym-jest-kod-zrodlowy]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 0201 · weryfikator_pojęć · dział 03 · pytanie 14 · próba 1

- Wynik: 1 blokujących, 1 sugestii. (eskalowano 1 powtarzających się braków do blokujących)
- Nowe potrzeby (2):
  - `wyjaśnienie` (blokująca) **Pythona**: Python pojawia się w ostatnim zdaniu bez wyjaśnienia. Wystarczy pół zdania, np. że to jeden z języków programowania, którego użyje kurs. [Eskalacja: zgłaszane już w sekcji „Przepis jako algorytm”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **błąd w linii 3**: wystarczy jedno zdanie; pełne omówienie w pytaniu 17. „Błąd w linii 3” to komunikat o pomyłce w kodzie, którą program zgłasza. Tekst nie mówi, skąd taki komunikat się bierze. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0201-weryfikator-pojec.md) · 10.0 s · $0.0269

### 0202 · znudzony_czytelnik · dział 03 · pytanie 14 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **Podświetlanie składni i numery linii**: Sedno sekcji, czyli pomoc w zauważaniu pomyłek, jest opisane tylko ogólnie („literówka często zmienia kolor”). Wystarczy krótki blok text z numerami linii dla rozlicz.py, gdzie w linii 3 stoi prnt zamiast print. Obok byłby komunikat „błąd w linii 3”. Kolorów w tekście nie da się pokazać, ale numery linii i literówkę tak. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0202-znudzony-czytelnik.md) · 9.7 s · $0.0225

### 0203 · strażnik_przykład · dział 03 · pytanie 14 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **wątek przewodni (rozlicz.py)**: Sekcja nie zawiera kodu, więc nie ma sprzeczności z kanonem (rozlicz.py, print("Wspólna Kasa"), print(300 / 3)). Zapowiedź „zapiszesz pierwszy plik” jest zgodna z wątkiem działu. Można dodać jedno zdanie, że pierwszym plikiem będzie rozlicz.py z programu Wspólna Kasa, aby połączyć edytor z przykładem przewodnim. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0203-straznik-przyklad.md) · 5.5 s · $0.0199

### 0204 · strażnik_warsztat · dział 03 · pytanie 14 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `wynik` (sugestia) **Krok 1: python --version**: Numer wersji może się różnić od 3.13.5 (np. 3.13.1 albo 3.13.7). Dopisz, że ważne jest, by zaczynało się od „Python 3.13”, a ostatnia liczba może być inna. Dodaj też, że na macOS/Linux trzeba wpisać python3 --version, jeśli python nie działa. _← strażnik_warsztat_
  - `spójność` (sugestia) **Krok 2: kasa.py**: Krok nie mówi, gdzie zapisać plik. Dopisz: „Zapisz plik jako kasa.py w katalogu ~/wspolna_kasa (tym samym, w którym masz otwarty terminal)”. W Notatniku warto dodać, żeby wybrać „Wszystkie pliki” i kodowanie UTF-8, żeby nie powstało kasa.py.txt. _← strażnik_warsztat_
  - `spójność` (sugestia) **Akapit o podświetlaniu składni**: Zdanie „Literówka w nazwie polecenia często od razu zmienia kolor” jest niepewne. W VS Code literówka w print (np. prnit) zwykle nie zmienia koloru, bo edytor traktuje ją jak zwykłą nazwę. Zastąp je przykładem, który jest prawdziwy: brakujący cudzysłów zamykający zmienia kolor reszty linii na kolor tekstu. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0204-straznik-warsztat.md) · 13.2 s · $0.0259

### 0205 · weryfikator_odwołań · dział 03 · pytanie 14 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **podświetlanie składni**: Podświetlanie składni jest opisane tylko słowami. Dodaj krótki przykład, np. jedna linia kodu z opisem, że polecenie jest w jednym kolorze, a tekst w cudzysłowie w innym. Pokaż też literówkę, która zmienia kolor. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **Pythona**: Zdanie „U siebie sprawdzisz teraz Pythona i zapiszesz pierwszy plik” nie mówi, czym jest Python (język programowania) ani jak sprawdzić, że jest zainstalowany. Czytelnik spoza IT może się zgubić. Dodaj jedno zdanie wyjaśnienia albo konkretny krok. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0205-weryfikator-odwolan.md) · 12.1 s · $0.0374

### 0206 · decyzja · dział 03 · pytanie 14 · próba 1

- Potrzeby w kolejce przed krokiem (2):
  - `wyjaśnienie` (blokująca) **sec-03-czym-jest-kod-zrodlowy**: Oznaczenie [[sec-03-czym-jest-kod-zrodlowy]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `wyjaśnienie` (blokująca) **Pythona**: Python pojawia się w ostatnim zdaniu bez wyjaśnienia. Wystarczy pół zdania, np. że to jeden z języków programowania, którego użyje kurs. [Eskalacja: zgłaszane już w sekcji „Przepis jako algorytm”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Do poprawy: 2 blokujących potrzeb wraca do pisarza; 8 sugestii trafia do raportu.
- 0.0 s

### 0207 · pisarz · dział 03 · pytanie 14 · próba 2

- Kolejka TODO (47): 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26 …
- Potrzeby w kolejce przed krokiem (2):
  - `wyjaśnienie` (blokująca) **sec-03-czym-jest-kod-zrodlowy**: Oznaczenie [[sec-03-czym-jest-kod-zrodlowy]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `wyjaśnienie` (blokująca) **Pythona**: Python pojawia się w ostatnim zdaniu bez wyjaśnienia. Wystarczy pół zdania, np. że to jeden z języków programowania, którego użyje kurs. [Eskalacja: zgłaszane już w sekcji „Przepis jako algorytm”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: „Do czego służy edytor”: 210 słów prozy, bez kodu; nowe hasła: edytor kodu, podświetlanie składni, Python; warsztat: $ python --version, kasa.py
- [prompt i odpowiedź](_przebieg/0207-pisarz.md) · 17.7 s · $0.0773

### 0208 · kontrola_deterministyczna · dział 03 · pytanie 14 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0209 · weryfikator_pojęć · dział 03 · pytanie 14 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **Pythona**: Python pojawia się w ostatnim zdaniu bez wyjaśnienia. Wystarczy pół zdania, np. że to jeden z języków programowania, którego użyje kurs. [Eskalacja: zgłaszane już w sekcji „Przepis jako algorytm”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0209-weryfikator-pojec.md) · 2.7 s · $0.0219

### 0210 · znudzony_czytelnik · dział 03 · pytanie 14 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **Literówka w nazwie polecenia często od razu zmienia kolor**: Najważniejsza obietnica edytora, czyli zauważanie pomyłek, jest podana ogólnikiem. Wystarczy krótki blok text z plikiem rozlicz.py: poprawne `print(300 / 3)` i błędne `pritn(300 / 3)` z opisem, że pierwsze słowo ma kolor polecenia, a drugie zostaje zwykłym tekstem. Zamiast tego można pokazać komunikat „błąd w linii 2” obok numerów linii. _← znudzony_czytelnik_
  - `tempo` (sugestia) **ostatni akapit**: „Sprawdzisz teraz, czy działa Python i zapiszesz pierwszy plik” pojawia się nagle, bez kroków. Instalacja edytora i Pythona to osobna czynność, więc zdanie tylko zapowiada, co będzie dalej. Lepiej jedno zdanie zapowiedzi kolejnej sekcji albo pominąć, a nie dopisywać instrukcji w tej sekcji. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0210-znudzony-czytelnik.md) · 11.2 s · $0.0247

### 0211 · strażnik_przykład · dział 03 · pytanie 14 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **rozlicz.py**: Sekcja nie zawiera bloków kodu, więc nie ma sprzeczności z kanonem. Wątek Wspólnej Kasy pojawia się tylko pośrednio (pierwszy plik). Można dodać jedno zdanie, że zapisywanym plikiem będzie rozlicz.py z kanonu (print("Wspólna Kasa")), żeby sekcja wyraźniej wiązała się z przykładem przewodnim. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0211-straznik-przyklad.md) · 4.2 s · $0.0196

### 0212 · strażnik_warsztat · dział 03 · pytanie 14 · próba 2

- Wynik: 0 blokujących, 3 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (3):
  - `wynik` (sugestia) **krok 1: python --version**: Numer po drugiej kropce zależy od zainstalowanej wersji 3.13.x. Dodaj zdanie: „Ostatnia cyfra może być inna, ważne, że wynik zaczyna się od Python 3.13”. Dodaj też, że na macOS/Linux trzeba wpisać python3 --version, jeśli python nie działa. _← strażnik_warsztat_
  - `spójność` (sugestia) **krok 2: kasa.py**: Krok 2 nie mówi, gdzie zapisać kasa.py. Dopisz: „Zapisz plik jako kasa.py w katalogu ~/wspolna_kasa (tam, gdzie otwarty jest terminal)”. Dla Notatnika dodaj ostrzeżenie, żeby plik nie nazywał się kasa.py.txt. _← strażnik_warsztat_
  - `spójność` (sugestia) **definicja edytora kodu**: Zdanie „Sam kodu nie uruchamia” jest zbyt kategoryczne, bo VS Code z rozszerzeniami potrafi uruchamiać kod. Zmień na: „Sam z siebie nie służy do uruchamiania kodu; uruchomimy go w terminalu”. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0212-straznik-warsztat.md) · 15.7 s · $0.0376

### 0213 · weryfikator_odwołań · dział 03 · pytanie 14 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/0213-weryfikator-odwolan.md) · 7.4 s · $0.0330

### 0214 · decyzja · dział 03 · pytanie 14 · próba 2

- Wynik: Sekcja przyjęta; 6 sugestii trafia do raportu.
- 0.0 s

### 0215 · akceptacja · dział 03 · pytanie 14

- Wynik: Sekcja [sec-03-do-czego-sluzy-edytor] dopisana do działu 03; hasła w glosariuszu: edytor kodu, podświetlanie składni, Python; odwołania: wstecz „Skoro kod jest zwykłym plikiem tekstowym”, w przód „gdy wyjaśnimy, co to znaczy uruchomić program”; punkty zaczepienia: literówka zmienia kolor; w TODO zostało 47.
- 0.0 s

### 0216 · autor_dodatków · dział 03 · pytanie 14

- Wynik: „Do czego służy edytor”: dowcipy: Numery linii jak numery domów, rysunki: Pomocnik z zakreślaczami
- [prompt i odpowiedź](_przebieg/0216-autor-dodatkow.md) · 15.4 s · $0.0471

### 0217 · weryfikator_dodatków · dział 03 · pytanie 14

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0217-weryfikator-dodatkow.md) · 6.9 s · $0.0360

### 0218 · pisarz · dział 03 · pytanie 15 · próba 1

- Kolejka TODO (46): 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27 …
- Wynik: „Co znaczy uruchomić program”: 162 słów prozy, ```python 3 linii, ```text 2 linii; nowe hasła: uruchamianie programu, terminal; warsztat: $ python --version, $ python kasa.py, kasa.py, $ python kasa.py (błąd), kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0218-pisarz.md) · 26.9 s · $0.0825

### 0219 · kontrola_deterministyczna · dział 03 · pytanie 15 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **kasa.py**: Treść pliku się nie zmienia; usuń ten krok albo wprowadź zmianę, o której mówi sekcja. _← kontrola_warsztat_
- 0.0 s

### 0220 · weryfikator_pojęć · dział 03 · pytanie 15 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **kompilatora**: wystarczy jedno zdanie; pełne omówienie w pytaniu 16. Tekst zapowiada, że wykonawca „różni się od kompilatora”, ale nie mówi, czym jest kompilator. Wystarczy krótkie zdanie, np. że kompilator tłumaczy cały program na postać zrozumiałą dla komputera przed jego uruchomieniem. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0220-weryfikator-pojec.md) · 9.1 s · $0.0272

### 0221 · znudzony_czytelnik · dział 03 · pytanie 15 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **terminal / python rozlicz.py**: Nie jest jasne, gdzie wpisać polecenie ani czy terminal trzeba otworzyć w folderze z plikiem. Początkujący może dostać błąd „nie znaleziono pliku”. Wystarczy jedno zdanie, np. że terminal otwieramy w folderze z rozlicz.py. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0221-znudzony-czytelnik.md) · 4.2 s · $0.0182

### 0222 · strażnik_przykład · dział 03 · pytanie 15 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **rozlicz.py**: Kod i wynik zgadzają się z kanonem (print("Wspólna Kasa"), print(300 / 3) → 100.0). Opis 'podzielone na trzy osoby' jest zgodny z wątkiem. Wątek zapowiada w tym dziale edytor VS Code i pierwszy celowy błąd; sekcja ich nie dotyka, więc można je dodać w kolejnych sekcjach działu. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0222-straznik-przyklad.md) · 4.3 s · $0.0194

### 0223 · strażnik_warsztat · dział 03 · pytanie 15 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **tekst sekcji: przykład rozlicz.py**: Tekst sekcji mówi o pliku `rozlicz.py` (z `print(300 / 3)` i wynikiem `100.0`), a czytelnik ma w katalogu tylko `kasa.py` z jedną linią `print("Wspólna Kasa")`. Polecenie `python rozlicz.py` zakończy się błędem: can't open file ... No such file or directory. Popraw przykład w tekście na `kasa.py`: blok kodu `# kasa.py - pierwszy skrypt Wspólnej Kasy` + `print("Wspólna Kasa")`, polecenie `python kasa.py`, wynik samo `Wspólna Kasa`. Zdanie o `100.0` i kolejności linii usuń albo przenieś do osobnego przykładu jawnie oznaczonego jako niewykonywany w krokach. _← strażnik_warsztat_
  - `spójność` (sugestia) **tekst sekcji**: Tekst sekcji nie wspomina o celowym błędzie z kroków 3–5 (literówka `prnt`, NameError, przywrócenie). Dodaj krótki akapit: Python zatrzymuje się na błędnej linii i podaje numer linii oraz podpowiedź `Did you mean: 'print'?`; po poprawce skrypt działa. _← strażnik_warsztat_
  - `wynik` (sugestia) **krok 4**: Ścieżka w tracebacku `/home/ola/wspolna_kasa/kasa.py` będzie u czytelnika inna (jego katalog domowy i nazwa użytkownika, na Windows np. C:\Users\...\wspolna_kasa\kasa.py). Dopisz uwagę, że ścieżka w pierwszej linii będzie się różnić, a ważne są numer linii `line 2` i ostatnia linia z NameError. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0223-straznik-warsztat.md) · 14.1 s · $0.0299

### 0224 · weryfikator_odwołań · dział 03 · pytanie 15 · próba 1

- Wynik: 1 blokujących, 2 sugestii. (odwołania: 2)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **[[uruchamianie-programu|uruchamiany]]**: Link wskazuje hasło „uruchamianie-programu”, którego nie ma w glosariuszu. Usuń znacznik linku (pojęcie i tak jest zdefiniowane w pierwszym zdaniu sekcji) albo dodaj hasło do glosariusza. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **lm-15**: Deklarowane nawiązanie „Sam kod źródłowy” to zwykłe użycie pojęcia, a zdanie nie odnosi się do miejsca, gdzie mowa o pliku tekstowym. Można je zostawić lub dopisać „jak wiesz, zwykły plik tekstowy”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **terminal**: „Terminal” jest zdefiniowany w tekście, ale nie ma go w glosariuszu; warto dodać hasło, bo pojęcie wróci w kolejnych sekcjach. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0224-weryfikator-odwolan.md) · 17.3 s · $0.0446

### 0225 · sprawdzacz_wyników · dział 03 · pytanie 15 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wynik` (sugestia) **edytor**: Słowo „edytor” pada bez wyjaśnienia. Wystarczy krótkie dopowiedzenie, np. „w edytorze, czyli programie do pisania kodu”. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **100.0**: Czytelnik może zapytać, dlaczego wynik to 100.0, a nie 100. Jedno zdanie o tym, że dzielenie w Pythonie daje liczbę z częścią dziesiętną, wyjaśniłoby to. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0225-sprawdzacz-wynikow.md) · 6.7 s · $0.0168

### 0226 · weryfikator_faktów · dział 03 · pytanie 15 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0226-weryfikator-faktow.md) · 6.7 s · $0.0286

### 0227 · decyzja · dział 03 · pytanie 15 · próba 1

- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (sugestia) **kasa.py**: Treść pliku się nie zmienia; usuń ten krok albo wprowadź zmianę, o której mówi sekcja. _← kontrola_warsztat_
  - `spójność` (blokująca) **tekst sekcji: przykład rozlicz.py**: Tekst sekcji mówi o pliku `rozlicz.py` (z `print(300 / 3)` i wynikiem `100.0`), a czytelnik ma w katalogu tylko `kasa.py` z jedną linią `print("Wspólna Kasa")`. Polecenie `python rozlicz.py` zakończy się błędem: can't open file ... No such file or directory. Popraw przykład w tekście na `kasa.py`: blok kodu `# kasa.py - pierwszy skrypt Wspólnej Kasy` + `print("Wspólna Kasa")`, polecenie `python kasa.py`, wynik samo `Wspólna Kasa`. Zdanie o `100.0` i kolejności linii usuń albo przenieś do osobnego przykładu jawnie oznaczonego jako niewykonywany w krokach. _← strażnik_warsztat_
  - `odwołanie` (blokująca) **[[uruchamianie-programu|uruchamiany]]**: Link wskazuje hasło „uruchamianie-programu”, którego nie ma w glosariuszu. Usuń znacznik linku (pojęcie i tak jest zdefiniowane w pierwszym zdaniu sekcji) albo dodaj hasło do glosariusza. _← weryfikator_odwołań_
- Wynik: Do poprawy: 3 blokujących potrzeb wraca do pisarza; 9 sugestii trafia do raportu.
- 0.0 s

### 0228 · pisarz · dział 03 · pytanie 15 · próba 2

- Kolejka TODO (46): 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27 …
- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (sugestia) **kasa.py**: Treść pliku się nie zmienia; usuń ten krok albo wprowadź zmianę, o której mówi sekcja. _← kontrola_warsztat_
  - `spójność` (blokująca) **tekst sekcji: przykład rozlicz.py**: Tekst sekcji mówi o pliku `rozlicz.py` (z `print(300 / 3)` i wynikiem `100.0`), a czytelnik ma w katalogu tylko `kasa.py` z jedną linią `print("Wspólna Kasa")`. Polecenie `python rozlicz.py` zakończy się błędem: can't open file ... No such file or directory. Popraw przykład w tekście na `kasa.py`: blok kodu `# kasa.py - pierwszy skrypt Wspólnej Kasy` + `print("Wspólna Kasa")`, polecenie `python kasa.py`, wynik samo `Wspólna Kasa`. Zdanie o `100.0` i kolejności linii usuń albo przenieś do osobnego przykładu jawnie oznaczonego jako niewykonywany w krokach. _← strażnik_warsztat_
  - `odwołanie` (blokująca) **[[uruchamianie-programu|uruchamiany]]**: Link wskazuje hasło „uruchamianie-programu”, którego nie ma w glosariuszu. Usuń znacznik linku (pojęcie i tak jest zdefiniowane w pierwszym zdaniu sekcji) albo dodaj hasło do glosariusza. _← weryfikator_odwołań_
- Wynik: „Co znaczy uruchomić program”: 161 słów prozy, ```python 2 linii, ```text 1 linii; nowe hasła: terminal; warsztat: $ python kasa.py
- [prompt i odpowiedź](_przebieg/0228-pisarz.md) · 14.3 s · $0.0759

### 0229 · kontrola_deterministyczna · dział 03 · pytanie 15 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0230 · weryfikator_pojęć · dział 03 · pytanie 15 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0230-weryfikator-pojec.md) · 5.4 s · $0.0224

### 0231 · znudzony_czytelnik · dział 03 · pytanie 15 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0231-znudzony-czytelnik.md) · 4.8 s · $0.0186

### 0232 · strażnik_przykład · dział 03 · pytanie 15 · próba 2

- Wynik: 2 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **kasa.py**: Kanon deklaruje plik programu `rozlicz.py` (skrypt główny) z zawartością: `# rozlicz.py`, `print("Wspólna Kasa")`, `print(300 / 3)`. Sekcja wprowadza inny plik `kasa.py` z innym komentarzem i bez linii `print(300 / 3)`, bez deklaracji zmiany w canon_changes. Popraw: użyj `rozlicz.py` (komentarz `# rozlicz.py`) i polecenia `python rozlicz.py`, a wynik uzgodnij z kodem z kanonu (jeśli dodasz `print(300 / 3)`, wynik to `Wspólna Kasa` i `100.0`). Alternatywnie zadeklaruj zmianę z reason. _← strażnik_przykład_
  - `spójność` (blokująca) **rozlicz.py**: Tekst mówi „U siebie masz już plik kasa.py”, a wątek działu mówi o powstaniu pierwszego pliku rozlicz.py w VS Code. Ujednolić nazwę pliku w całym tekście i poleceniu uruchomienia. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0232-straznik-przyklad.md) · 6.4 s · $0.0220

### 0233 · strażnik_warsztat · dział 03 · pytanie 15 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **tekst sekcji: przykład rozlicz.py**: Tekst sekcji mówi o pliku `rozlicz.py` (z `print(300 / 3)` i wynikiem `100.0`), a czytelnik ma w katalogu tylko `kasa.py` z jedną linią `print("Wspólna Kasa")`. Polecenie `python rozlicz.py` zakończy się błędem: can't open file ... No such file or directory. Popraw przykład w tekście na `kasa.py`: blok kodu `# kasa.py - pierwszy skrypt Wspólnej Kasy` + `print("Wspólna Kasa")`, polecenie `python kasa.py`, wynik samo `Wspólna Kasa`. Zdanie o `100.0` i kolejności linii usuń albo przenieś do osobnego przykładu jawnie oznaczonego jako niewykonywany w krokach. _← strażnik_warsztat_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0233-straznik-warsztat.md) · 4.4 s · $0.0188

### 0234 · weryfikator_odwołań · dział 03 · pytanie 15 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **[[uruchamianie-programu|uruchamiany]]**: Link wskazuje hasło „uruchamianie-programu”, którego nie ma w glosariuszu. Usuń znacznik linku (pojęcie i tak jest zdefiniowane w pierwszym zdaniu sekcji) albo dodaj hasło do glosariusza. _← weryfikator_odwołań_
- Wynik: 3 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **[[terminal|terminalu]]**: Znacznik linku wskazuje hasło „terminal”, którego nie ma w glosariuszu (ten sam błąd co poprzednio przy innym haśle). Pojęcie jest zdefiniowane w tekście („okno, w którym komputer przyjmuje polecenia pisane tekstem”), więc usuń znacznik linku i zostaw zwykły tekst „terminalu”, albo dodaj hasło do glosariusza. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie masz już plik `kasa.py`**: Zdanie nawiązuje do wcześniejszego utworzenia pliku kasa.py, ale w poprzednich sekcjach nie ma takiego miejsca. Czytelnik nie wie, skąd ma ten plik. Zamień na polecenie na miejscu, np. „Utwórz w edytorze plik kasa.py i wpisz do niego:”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie masz już plik `kasa.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/0234-weryfikator-odwolan.md) · 13.2 s · $0.0404

### 0235 · sprawdzacz_wyników · dział 03 · pytanie 15 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0235-sprawdzacz-wynikow.md) · 4.2 s · $0.0137

### 0236 · weryfikator_faktów · dział 03 · pytanie 15 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 2)
- [prompt i odpowiedź](_przebieg/0236-weryfikator-faktow.md) · 14.0 s · $0.0655

### 0237 · decyzja · dział 03 · pytanie 15 · próba 2

- Potrzeby w kolejce przed krokiem (5):
  - `spójność` (blokująca) **kasa.py**: Kanon deklaruje plik programu `rozlicz.py` (skrypt główny) z zawartością: `# rozlicz.py`, `print("Wspólna Kasa")`, `print(300 / 3)`. Sekcja wprowadza inny plik `kasa.py` z innym komentarzem i bez linii `print(300 / 3)`, bez deklaracji zmiany w canon_changes. Popraw: użyj `rozlicz.py` (komentarz `# rozlicz.py`) i polecenia `python rozlicz.py`, a wynik uzgodnij z kodem z kanonu (jeśli dodasz `print(300 / 3)`, wynik to `Wspólna Kasa` i `100.0`). Alternatywnie zadeklaruj zmianę z reason. _← strażnik_przykład_
  - `spójność` (blokująca) **rozlicz.py**: Tekst mówi „U siebie masz już plik kasa.py”, a wątek działu mówi o powstaniu pierwszego pliku rozlicz.py w VS Code. Ujednolić nazwę pliku w całym tekście i poleceniu uruchomienia. _← strażnik_przykład_
  - `odwołanie` (blokująca) **[[terminal|terminalu]]**: Znacznik linku wskazuje hasło „terminal”, którego nie ma w glosariuszu (ten sam błąd co poprzednio przy innym haśle). Pojęcie jest zdefiniowane w tekście („okno, w którym komputer przyjmuje polecenia pisane tekstem”), więc usuń znacznik linku i zostaw zwykły tekst „terminalu”, albo dodaj hasło do glosariusza. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie masz już plik `kasa.py`**: Zdanie nawiązuje do wcześniejszego utworzenia pliku kasa.py, ale w poprzednich sekcjach nie ma takiego miejsca. Czytelnik nie wie, skąd ma ten plik. Zamień na polecenie na miejscu, np. „Utwórz w edytorze plik kasa.py i wpisz do niego:”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie masz już plik `kasa.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Limit prób (2) wyczerpany; 5 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0238 · akceptacja · dział 03 · pytanie 15

- Wynik: Sekcja [sec-03-co-znaczy-uruchomic-program] dopisana do działu 03; hasła w glosariuszu: terminal; odwołania: w przód „wyjaśnimy w następnej części”; punkty zaczepienia: przepis w szufladzie, zapisz, uruchom, przeczytaj; w TODO zostało 46.
- 0.0 s

### 0239 · łowca_pułapek · dział 03 · pytanie 15

- Wynik: „Co znaczy uruchomić program”: brak pułapek
- [prompt i odpowiedź](_przebieg/0239-lowca-pulapek.md) · 2.3 s · $0.0128

### 0240 · autor_dodatków · dział 03 · pytanie 15

- Wynik: „Co znaczy uruchomić program”: wtręty: Marta czeka, aż plik sam zadziała, dygresje: Skąd Python wziął swoją nazwę
- [prompt i odpowiedź](_przebieg/0240-autor-dodatkow.md) · 12.5 s · $0.0466

### 0241 · weryfikator_dodatków · dział 03 · pytanie 15

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0241-weryfikator-dodatkow.md) · 15.8 s · $0.0804

### 0242 · pisarz · dział 03 · pytanie 16 · próba 1

- Kolejka TODO (45): 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28 …
- Wynik: „Kompilator i interpreter”: 148 słów prozy, ```text 2 linii; nowe hasła: kompilator, interpreter; warsztat: $ python --version
- [prompt i odpowiedź](_przebieg/0242-pisarz.md) · 20.3 s · $0.0755

### 0243 · kontrola_deterministyczna · dział 03 · pytanie 16 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0244 · weryfikator_pojęć · dział 03 · pytanie 16 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **procesor**: Pojęcie pada w uzasadnieniu, po co w ogóle jest tłumaczenie kodu, a nie ma go w glosariuszu ani wyjaśnienia w tekście. Wystarczy krótkie zdanie: procesor to układ, który wykonuje działania komputera i rozumie tylko bardzo proste polecenia w własnym zapisie. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **kroku budowania**: „Budowanie” nie jest wyjaśnione. Można dopisać, że chodzi o kompilację, czyli osobny etap przygotowania pliku do uruchomienia opisany wyżej. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0244-weryfikator-pojec.md) · 7.8 s · $0.0258

### 0245 · znudzony_czytelnik · dział 03 · pytanie 16 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **Kompilator / osobny plik programu**: Kompilator jest opisany tylko ogólnie. Warto podać jedną nazwę języka kompilowanego (np. C albo Go) i nazwę pliku wynikowego (np. program.exe), żeby czytelnik miał do czego odnieść „osobny plik do uruchomienia”. Można to zrobić, zastępując jedno zdanie, bez wydłużania sekcji. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0245-znudzony-czytelnik.md) · 6.7 s · $0.0205

### 0246 · strażnik_przykład · dział 03 · pytanie 16 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **kasa.py**: Sekcja używa nazwy pliku `kasa.py` (w `python kasa.py` i w akapicie o Wspólnej Kasie), a kanon deklaruje plik programu jako `rozlicz.py`. To niezadeklarowana sprzeczność z kanonem. Zamień wszystkie wystąpienia `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
  - `spójność` (sugestia) **python rozlicz.py**: Polecenie uruchomienia powinno brzmieć `python rozlicz.py`, czyli uruchamiać skrypt z kanonu. Można też pokazać efekt: wypisze `Wspólna Kasa` i `100.0`, żeby wątek był konkretny. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0246-straznik-przyklad.md) · 5.4 s · $0.0205

### 0247 · strażnik_warsztat · dział 03 · pytanie 16 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **krok 1 / tekst sekcji**: Krok `python --version` nie jest omówiony w tekście sekcji. Dodaj zdanie, np. „Wynik `Python 3.13.1` potwierdza, że masz zainstalowany interpreter Pythona (numer po drugiej kropce może być inny).”. Bez niego czytelnik nie wie, po co wykonał to polecenie. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0247-straznik-warsztat.md) · 7.3 s · $0.0202

### 0248 · weryfikator_odwołań · dział 03 · pytanie 16 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 1)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **kompilator, interpreter**: Znaczniki [[kompilator|...]] i [[interpreter|...]] wskazują hasła, których nie ma w glosariuszu. Oba pojęcia są zdefiniowane w tekście, więc nie blokuje to zrozumienia. Dodaj hasła do glosariusza albo usuń znaczniki linków. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **procesor**: Słowo „procesor” pojawia się bez wyjaśnienia. Czytelnik spoza IT może potrzebować krótkiego dopowiedzenia, np. „układ w komputerze, który wykonuje najprostsze polecenia”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0248-weryfikator-odwolan.md) · 13.0 s · $0.0409

### 0249 · weryfikator_faktów · dział 03 · pytanie 16 · próba 1

- Wynik: Brak uwag. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0249-weryfikator-faktow.md) · 14.3 s · $0.0751

### 0250 · decyzja · dział 03 · pytanie 16 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Sekcja używa nazwy pliku `kasa.py` (w `python kasa.py` i w akapicie o Wspólnej Kasie), a kanon deklaruje plik programu jako `rozlicz.py`. To niezadeklarowana sprzeczność z kanonem. Zamień wszystkie wystąpienia `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 7 sugestii trafia do raportu.
- 0.0 s

### 0251 · pisarz · dział 03 · pytanie 16 · próba 2

- Kolejka TODO (45): 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28 …
- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Sekcja używa nazwy pliku `kasa.py` (w `python kasa.py` i w akapicie o Wspólnej Kasie), a kanon deklaruje plik programu jako `rozlicz.py`. To niezadeklarowana sprzeczność z kanonem. Zamień wszystkie wystąpienia `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
- Wynik: „Kompilator i interpreter”: 148 słów prozy, ```text 2 linii; nowe hasła: kompilator, interpreter
- [prompt i odpowiedź](_przebieg/0251-pisarz.md) · 12.8 s · $0.0742

### 0252 · kontrola_deterministyczna · dział 03 · pytanie 16 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0253 · weryfikator_pojęć · dział 03 · pytanie 16 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0253-weryfikator-pojec.md) · 5.1 s · $0.0221

### 0254 · znudzony_czytelnik · dział 03 · pytanie 16 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **Kompilator**: Teza o kompilatorze jest podana tylko abstrakcyjnie. Jeden krótki przykład z nazwą (np. program w języku C kompilowany do pliku .exe) pokazałby, jak wygląda „osobny plik programu”. Dziś czytelnik zna tylko interpreter. _← znudzony_czytelnik_
  - `skrócenie` (sugestia) **W praktyce Python najpierw przekłada plik na pośredni zapis**: Zdanie o pośrednim zapisie w Pythonie wprowadza nowe pojęcie bez wyjaśnienia i miesza obraz „interpreter nie tworzy pliku”. Można je usunąć albo dopowiedzieć w jednym zdaniu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0254-znudzony-czytelnik.md) · 4.9 s · $0.0189

### 0255 · strażnik_przykład · dział 03 · pytanie 16 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Sekcja używa nazwy pliku `kasa.py` (w `python kasa.py` i w akapicie o Wspólnej Kasie), a kanon deklaruje plik programu jako `rozlicz.py`. To niezadeklarowana sprzeczność z kanonem. Zamień wszystkie wystąpienia `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0255-straznik-przyklad.md) · 2.5 s · $0.0188

### 0256 · weryfikator_odwołań · dział 03 · pytanie 16 · próba 2

- Wynik: 0 blokujących, 3 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- Nowe potrzeby (3):
  - `odwołanie` (sugestia) **procesor**: „Procesor” pojawia się bez wyjaśnienia. Wystarczy dopisać np. „układ, który wykonuje polecenia w komputerze”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **pośredni zapis**: „Pośredni zapis”, na który Python przekłada plik, jest wspomniany bez wyjaśnienia. Można dodać jedno zdanie, że to wewnętrzna, pomocnicza forma kodu, o którą czytelnik nie musi się martwić. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **Wspólna Kasa**: „Wspólna Kasa” i „rozlicz.py” są użyte jako znany przykład bez przypomnienia. Warto krótko nazwać projekt, np. „program do rozliczania wyjazdu”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0256-weryfikator-odwolan.md) · 12.5 s · $0.0404

### 0257 · decyzja · dział 03 · pytanie 16 · próba 2

- Wynik: Sekcja przyjęta; 5 sugestii trafia do raportu.
- 0.0 s

### 0258 · akceptacja · dział 03 · pytanie 16

- Wynik: Sekcja [sec-03-kompilator-i-interpreter] dopisana do działu 03; hasła w glosariuszu: kompilator, interpreter; odwołania: wstecz „To ten wykonawca, o którym była mowa przy uruchamianiu programu”, wstecz „Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie”; punkty zaczepienia: brak kroku budowania; w TODO zostało 45.
- 0.0 s

### 0259 · autor_dodatków · dział 03 · pytanie 16

- Wynik: „Kompilator i interpreter”: dowcipy: Tłumacz książki i tłumacz symultaniczny
- [prompt i odpowiedź](_przebieg/0259-autor-dodatkow.md) · 6.3 s · $0.0430

### 0260 · weryfikator_dodatków · dział 03 · pytanie 16

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0260-weryfikator-dodatkow.md) · 7.3 s · $0.0384

### 0261 · pisarz · dział 03 · pytanie 17 · próba 1

- Kolejka TODO (44): 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29 …
- Wynik: „Co to jest błąd w programie”: 157 słów prozy, ```python 3 linii, ```text 2 linii; nowe hasła: błąd w programie; warsztat: kasa.py, $ python kasa.py (błąd), kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0261-pisarz.md) · 27.8 s · $0.0831

### 0262 · kontrola_deterministyczna · dział 03 · pytanie 17 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **kasa.py**: Treść pliku się nie zmienia; usuń ten krok albo wprowadź zmianę, o której mówi sekcja. _← kontrola_warsztat_
- 0.0 s

### 0263 · weryfikator_pojęć · dział 03 · pytanie 17 · próba 1

- Wynik: 1 blokujących, 0 sugestii. (eskalowano 1 powtarzających się braków do blokujących)
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **print**: Słowo `print` pojawia się w tekście i w kodzie, ale nie jest wyjaśnione. Wystarczy jedno zdanie, że `print` każe programowi wypisać coś na ekranie. Czytelnik może to zgadnąć z wyniku, więc to tylko sugestia. [Eskalacja: zgłaszane już w sekcji „Czym jest kod źródłowy”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0263-weryfikator-pojec.md) · 8.9 s · $0.0253

### 0264 · znudzony_czytelnik · dział 03 · pytanie 17 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **Pierwszy rodzaj błędu: literówka print/prnt**: Pierwszy rodzaj błędu (literówka `prnt`) jest opisany, ale nie pokazany. Krótki blok text z komunikatem Pythona (np. NameError: name 'prnt' is not defined, z numerem linii) pokazałby, jak wygląda komunikat wskazujący linię i powód. Wymaga miejsca na drugi blok kodu, więc tylko sugestia. _← znudzony_czytelnik_
  - `konkret` (sugestia) **Przykład z dzieleniem 300 / 2**: Zdanie 'na troje trzeba dzielić przez 3' pojawia się dopiero po wyniku. Warto dodać oczekiwany wynik (100.0), żeby czytelnik od razu zobaczył różnicę między 150.0 a 100.0. Dodatkowo komentarz w kodzie mówi 'na troje osób', a kod dzieli przez 2, co można zaznaczyć wprost. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0264-znudzony-czytelnik.md) · 6.2 s · $0.0201

### 0265 · strażnik_przykład · dział 03 · pytanie 17 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0265-straznik-przyklad.md) · 6.5 s · $0.0205

### 0266 · strażnik_warsztat · dział 03 · pytanie 17 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **interpreter**: W tekście pada słowo „interpreter” bez definicji. Można zastąpić je słowem „Python” („Python nie zna takiego słowa”) albo dodać krótkie wyjaśnienie. _← strażnik_warsztat_
  - `spójność` (sugestia) **przykład z dzieleniem**: Komentarz „# poza kanonem: błąd w dzieleniu” w przykładzie z dzieleniem to notatka techniczna, która trafi do czytelnika. Lepiej go usunąć albo zastąpić np. „# błąd w dzieleniu”. Sam wynik 150.0 jest poprawny. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0266-straznik-warsztat.md) · 12.4 s · $0.0262

### 0267 · weryfikator_odwołań · dział 03 · pytanie 17 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 1)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **Pierwszy rodzaj błędu**: Pierwszy rodzaj błędu (zatrzymanie z komunikatem) jest opisany tylko słowami. Warto pokazać krótki kod z `prnt` i wypisany komunikat, tak jak dla drugiego rodzaju. Czytelnik zobaczy wtedy, że komunikat wskazuje linię i powód. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **komentarz w bloku kodu**: Komentarz w kodzie „# poza kanonem: błąd w dzieleniu” to żargon redakcyjny, którego czytelnik nie zna. Lepiej go usunąć albo zastąpić np. „# błąd: powinno być dzielenie przez 3”. Komentarz zdradza też błąd, zanim czytelnik go zauważy. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0267-weryfikator-odwolan.md) · 10.6 s · $0.0384

### 0268 · sprawdzacz_wyników · dział 03 · pytanie 17 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wynik` (sugestia) **Pierwszy rodzaj błędu**: Pierwszy rodzaj błędu (zatrzymanie z komunikatem) ma tylko opis literówki `prnt`, bez pokazanego komunikatu. Krótki blok kodu z `prnt("Wspólna Kasa")` i blok text z komunikatem (NameError: name 'prnt' is not defined, z numerem linii) pokazałby, że komunikat wskazuje linię i powód. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **interpreter**: Słowo „interpreter” pojawia się bez wyjaśnienia, a czytelnik spoza IT może go nie znać. Wystarczy dodać „interpreter, czyli program, który czyta i wykonuje kod” albo użyć słowa „Python”. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0268-sprawdzacz-wynikow.md) · 8.0 s · $0.0182

### 0269 · weryfikator_faktów · dział 03 · pytanie 17 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 0)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Python czyta plik od góry i gdy trafi na coś, czego nie rozumie, przerywa pracę... literówka zmieni `print` w `prnt`: interpreter nie zna takiego słowa**: Literówka `prnt("x")` nie jest błędem składni, tylko NameError zgłaszanym w trakcie wykonania (name 'prnt' is not defined). Python najpierw kompiluje cały plik, więc wcześniejsze poprawne linie zdążą się wykonać, a dopiero potem program zatrzyma się na tej linii. Opis "czyta od góry i przerywa" jest uproszczeniem, które nie prowadzi do błędu. Dla ścisłości można napisać, że Python wykonuje instrukcje po kolei i zatrzymuje się na pierwszej, której nie potrafi wykonać. Nie sprawdzałem tego w dokumentacji online, opieram się na znanym zachowaniu interpretera. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0269-weryfikator-faktow.md) · 10.6 s · $0.0334

### 0270 · decyzja · dział 03 · pytanie 17 · próba 1

- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (sugestia) **kasa.py**: Treść pliku się nie zmienia; usuń ten krok albo wprowadź zmianę, o której mówi sekcja. _← kontrola_warsztat_
  - `wyjaśnienie` (blokująca) **print**: Słowo `print` pojawia się w tekście i w kodzie, ale nie jest wyjaśnione. Wystarczy jedno zdanie, że `print` każe programowi wypisać coś na ekranie. Czytelnik może to zgadnąć z wyniku, więc to tylko sugestia. [Eskalacja: zgłaszane już w sekcji „Czym jest kod źródłowy”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Do poprawy: 2 blokujących potrzeb wraca do pisarza; 9 sugestii trafia do raportu.
- 0.0 s

### 0271 · pisarz · dział 03 · pytanie 17 · próba 2

- Kolejka TODO (44): 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29 …
- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (sugestia) **kasa.py**: Treść pliku się nie zmienia; usuń ten krok albo wprowadź zmianę, o której mówi sekcja. _← kontrola_warsztat_
  - `wyjaśnienie` (blokująca) **print**: Słowo `print` pojawia się w tekście i w kodzie, ale nie jest wyjaśnione. Wystarczy jedno zdanie, że `print` każe programowi wypisać coś na ekranie. Czytelnik może to zgadnąć z wyniku, więc to tylko sugestia. [Eskalacja: zgłaszane już w sekcji „Czym jest kod źródłowy”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: „Co to jest błąd w programie”: 175 słów prozy, ```python 3 linii, ```text 2 linii; nowe hasła: błąd w programie, print; warsztat: kasa.py, $ python kasa.py (błąd)
- [prompt i odpowiedź](_przebieg/0271-pisarz.md) · 20.0 s · $0.0828

### 0272 · kontrola_deterministyczna · dział 03 · pytanie 17 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0273 · weryfikator_pojęć · dział 03 · pytanie 17 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **print**: Słowo `print` pojawia się w tekście i w kodzie, ale nie jest wyjaśnione. Wystarczy jedno zdanie, że `print` każe programowi wypisać coś na ekranie. Czytelnik może to zgadnąć z wyniku, więc to tylko sugestia. [Eskalacja: zgłaszane już w sekcji „Czym jest kod źródłowy”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0273-weryfikator-pojec.md) · 3.8 s · $0.0230

### 0274 · znudzony_czytelnik · dział 03 · pytanie 17 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0274-znudzony-czytelnik.md) · 5.4 s · $0.0184

### 0275 · strażnik_przykład · dział 03 · pytanie 17 · próba 2

- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **rozlicz.py**: Tekst mówi, że błąd czytelnik zobaczy „w `kasa.py`”, ale plik programu w kanonie nazywa się `rozlicz.py` (skrypt główny). Nazwa `kasa.py` nie została zadeklarowana jako zmiana. Zamień na `rozlicz.py`. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0275-straznik-przyklad.md) · 6.1 s · $0.0209

### 0276 · strażnik_warsztat · dział 03 · pytanie 17 · próba 2

- Wynik: 0 blokujących, 3 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (3):
  - `wynik` (sugestia) **krok 2**: Ścieżka w tracebacku (/home/ala/wspolna_kasa/kasa.py) będzie u czytelnika inna (jego katalog domowy, na Windows np. C:\Users\...\wspolna_kasa\kasa.py). Dodaj jedno zdanie, że ścieżka w pierwszej linii File będzie u niego inna i to normalne; ważne są numer linii i ostatnia linia komunikatu. Reszta wyniku (NameError, karety pod prnt, podpowiedź Did you mean: 'print'?) jest zgodna z Pythonem 3.13. _← strażnik_warsztat_
  - `spójność` (sugestia) **akapit „Pierwszy rodzaj”**: Zdanie „gdy trafi na coś, czego nie rozumie” jest nieścisłe: `prnt(...)` jest poprawnie zapisane, Python dowiaduje się o braku nazwy dopiero przy wykonaniu tej linii. Lepiej: „gdy trafi na coś, z czym nie umie się zmierzyć (np. nazwę, której nie zna)”. _← strażnik_warsztat_
  - `spójność` (sugestia) **interpreter**: Słowo „interpreter” pojawia się bez wyjaśnienia. Zamień na „Python” albo dodaj krótką definicję (program, który czyta i wykonuje kod). _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0276-straznik-warsztat.md) · 12.5 s · $0.0270

### 0277 · weryfikator_odwołań · dział 03 · pytanie 17 · próba 2

- Wynik: 1 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **# poza kanonem: błąd w dzieleniu**: Komentarz w kodzie „poza kanonem” to wewnętrzny żargon autora, którego czytelnik nie zna. Usuń go albo zastąp zwykłym opisem, np. „# błąd: dzielimy przez 2 zamiast przez 3”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **`kasa.py`**: Zapowiedź „za chwilę w kasa.py” nie mówi, kiedy i w jakim miejscu to nastąpi, a plik kasa.py nie pojawił się wcześniej (wcześniej był `rozlicz.py`). Zapowiedz to jako temat, np. „gdy za chwilę zaczniesz pisać własny program, sam zobaczysz taki komunikat”, albo pokaż plik. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **literówka prnt**: Pierwszy rodzaj błędu jest opisany bez przykładu. Pokaż krótki kod z `prnt` i przykładowy komunikat (linia, nazwa błędu), tak jak zrobiono to dla drugiego rodzaju. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0277-weryfikator-odwolan.md) · 15.3 s · $0.0438

### 0278 · sprawdzacz_wyników · dział 03 · pytanie 17 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0278-sprawdzacz-wynikow.md) · 4.0 s · $0.0138

### 0279 · weryfikator_faktów · dział 03 · pytanie 17 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0279-weryfikator-faktow.md) · 6.8 s · $0.0292

### 0280 · decyzja · dział 03 · pytanie 17 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (blokująca) **rozlicz.py**: Tekst mówi, że błąd czytelnik zobaczy „w `kasa.py`”, ale plik programu w kanonie nazywa się `rozlicz.py` (skrypt główny). Nazwa `kasa.py` nie została zadeklarowana jako zmiana. Zamień na `rozlicz.py`. _← strażnik_przykład_
  - `odwołanie` (blokująca) **# poza kanonem: błąd w dzieleniu**: Komentarz w kodzie „poza kanonem” to wewnętrzny żargon autora, którego czytelnik nie zna. Usuń go albo zastąp zwykłym opisem, np. „# błąd: dzielimy przez 2 zamiast przez 3”. _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 2 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0281 · akceptacja · dział 03 · pytanie 17

- Wynik: Sekcja [sec-03-co-to-jest-blad-w-programie] dopisana do działu 03; hasła w glosariuszu: błąd w programie, print; odwołania: w przód „U siebie zobaczysz to za chwilę w `kasa.py`”, w przód „omówimy osobno, w dziale o poprawianiu programów”; punkty zaczepienia: dzielenie przez 2 zamiast 3, prnt zamiast print; w TODO zostało 44.
- 0.0 s

### 0282 · łowca_pułapek · dział 03 · pytanie 17

- Wynik: „Co to jest błąd w programie”: Brak komunikatu nie oznacza poprawnego wyniku
- [prompt i odpowiedź](_przebieg/0282-lowca-pulapek.md) · 4.4 s · $0.0173

### 0283 · autor_dodatków · dział 03 · pytanie 17

- Wynik: „Co to jest błąd w programie”: wtręty: Marta widzi komunikat i odsuwa się od klawiatury, dykteryjki: Raport, który liczył bez błędu i bez sensu
- [prompt i odpowiedź](_przebieg/0283-autor-dodatkow.md) · 10.6 s · $0.0474

### 0284 · weryfikator_dodatków · dział 03 · pytanie 17

- Wynik: odrzucone: 1; Raport, który liczył bez błędu i bez sensu: Powtarza motyw wcześniejszej dykteryjki o archiwizacji: skrypt raportowy bez błędu, a z niepoprawnym wynikiem i wnioskiem o fałszywym poczuciu pewności.
- [prompt i odpowiedź](_przebieg/0284-weryfikator-dodatkow.md) · 8.2 s · $0.0424

### 0285 · pisarz · dział 03 · pytanie 18 · próba 1

- Kolejka TODO (43): 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30 …
- Wynik: „Do czego służą komentarze”: 144 słów prozy, ```python 4 linii, ```text 2 linii; nowe hasła: komentarz; wątki: przykład zmień rozlicz.py; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0285-pisarz.md) · 17.9 s · $0.0763

### 0286 · kontrola_deterministyczna · dział 03 · pytanie 18 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0287 · weryfikator_pojęć · dział 03 · pytanie 18 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0287-weryfikator-pojec.md) · 5.5 s · $0.0222

### 0288 · znudzony_czytelnik · dział 03 · pytanie 18 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0288-znudzony-czytelnik.md) · 6.3 s · $0.0197

### 0289 · strażnik_przykład · dział 03 · pytanie 18 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **kasa.py**: Ostatni akapit odwołuje się do pliku `kasa.py` z komentarzem w pierwszej linii. W kanonie jest tylko `rozlicz.py`, a jego pierwsza linia (`# rozlicz.py - rozliczenie wspólnych wydatków`) jest aktualna, nie przestarzała. Zamień na `rozlicz.py` i dopasuj resztę zdania. Można np. zapowiedzieć, że czytelnik zmieni komentarz w `rozlicz.py`, uruchomi plik i sprawdzi, że wynik się nie zmienił. _← strażnik_przykład_
  - `spójność` (sugestia) **rozlicz.py**: Blok kodu ma czwartą linię `# print(300 / 2)  <- ta linia jest wyłączona`, której nie ma w zadeklarowanej zmianie `rozlicz.py`. Dodaj ją do deklaracji zmiany albo oznacz ten fragment jako demonstrację poza kanonem, żeby plik czytelnika nie rozjechał się z kanonem. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0289-straznik-przyklad.md) · 9.4 s · $0.0254

### 0290 · strażnik_warsztat · dział 03 · pytanie 18 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **ostatni akapit sekcji vs krok 1**: Ostatni akapit mówi, że pierwsza linia kasa.py to komentarz, który czytelnik „za chwilę poprawi”. Krok 1 nie zmienia tej linii (`# kasa.py - pierwszy skrypt Wspólnej Kasy` zostaje bez zmian). Dopisuje nową linię `# Poprawka: literówka prnt zamieniona na print` i zamienia `prnt` na `print`. Ten pierwszy komentarz też nie jest przestarzały. Zamień ostatnie dwa zdania na: „U siebie masz już taki komentarz w pierwszej linii `kasa.py`. Za chwilę dopiszesz pod nim drugi, o poprawce, i sprawdzisz, że żaden z nich nie wpływa na wynik.” Możesz też usunąć zdanie o „starzeniu się” komentarza z odniesienia do pliku. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0290-straznik-warsztat.md) · 10.7 s · $0.0246

### 0291 · weryfikator_odwołań · dział 03 · pytanie 18 · próba 1

- Wynik: 3 blokujących, 1 sugestii. (odwołania: 1)
- Nowe potrzeby (4):
  - `odwołanie` (blokująca) **U siebie masz już taki komentarz w pierwszej linii `kasa.py`**: Nawiązanie bez celu: żaden wcześniejszy dział nie tworzy pliku `kasa.py` ani komentarza w jego pierwszej linii (wcześniej jest `rozlicz.py`, a przykład w tej sekcji też go używa). Czytelnik nie ma takiego komentarza. Usuń zdanie albo zastąp je przykładem podanym na miejscu, np. pokaż linię `# udział na dwie osoby` nad `print(300 / 3)` i wyjaśnij, czemu jest nieaktualna. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Za chwilę go poprawisz i sprawdzisz, że nie wpływa na wynik**: Obietnica bez pokrycia: nic dalej nie prowadzi czytelnika przez poprawianie komentarza, a w planie nie ma tematu, który to spełni. Usuń zapowiedź albo od razu pokaż to w sekcji (kod z poprawionym komentarzem i ten sam wynik `100.0`). _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **komentarz może się zestarzeć**: Teza o starzeniu się komentarza jest podana bez przykładu. Dodaj krótki kod, w którym komentarz mówi „na troje”, a kod dzieli przez 2. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie masz już taki komentarz w pierwszej linii `kasa.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/0291-weryfikator-odwolan.md) · 16.7 s · $0.0459

### 0292 · sprawdzacz_wyników · dział 03 · pytanie 18 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0292-sprawdzacz-wynikow.md) · 4.2 s · $0.0137

### 0293 · weryfikator_faktów · dział 03 · pytanie 18 · próba 1

- Wynik: Brak uwag. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0293-weryfikator-faktow.md) · 12.4 s · $0.0549

### 0294 · decyzja · dział 03 · pytanie 18 · próba 1

- Potrzeby w kolejce przed krokiem (4):
  - `spójność` (blokująca) **kasa.py**: Ostatni akapit odwołuje się do pliku `kasa.py` z komentarzem w pierwszej linii. W kanonie jest tylko `rozlicz.py`, a jego pierwsza linia (`# rozlicz.py - rozliczenie wspólnych wydatków`) jest aktualna, nie przestarzała. Zamień na `rozlicz.py` i dopasuj resztę zdania. Można np. zapowiedzieć, że czytelnik zmieni komentarz w `rozlicz.py`, uruchomi plik i sprawdzi, że wynik się nie zmienił. _← strażnik_przykład_
  - `odwołanie` (blokująca) **U siebie masz już taki komentarz w pierwszej linii `kasa.py`**: Nawiązanie bez celu: żaden wcześniejszy dział nie tworzy pliku `kasa.py` ani komentarza w jego pierwszej linii (wcześniej jest `rozlicz.py`, a przykład w tej sekcji też go używa). Czytelnik nie ma takiego komentarza. Usuń zdanie albo zastąp je przykładem podanym na miejscu, np. pokaż linię `# udział na dwie osoby` nad `print(300 / 3)` i wyjaśnij, czemu jest nieaktualna. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Za chwilę go poprawisz i sprawdzisz, że nie wpływa na wynik**: Obietnica bez pokrycia: nic dalej nie prowadzi czytelnika przez poprawianie komentarza, a w planie nie ma tematu, który to spełni. Usuń zapowiedź albo od razu pokaż to w sekcji (kod z poprawionym komentarzem i ten sam wynik `100.0`). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie masz już taki komentarz w pierwszej linii `kasa.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Do poprawy: 4 blokujących potrzeb wraca do pisarza; 3 sugestii trafia do raportu.
- 0.0 s

### 0295 · pisarz · dział 03 · pytanie 18 · próba 2

- Kolejka TODO (43): 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30 …
- Potrzeby w kolejce przed krokiem (4):
  - `spójność` (blokująca) **kasa.py**: Ostatni akapit odwołuje się do pliku `kasa.py` z komentarzem w pierwszej linii. W kanonie jest tylko `rozlicz.py`, a jego pierwsza linia (`# rozlicz.py - rozliczenie wspólnych wydatków`) jest aktualna, nie przestarzała. Zamień na `rozlicz.py` i dopasuj resztę zdania. Można np. zapowiedzieć, że czytelnik zmieni komentarz w `rozlicz.py`, uruchomi plik i sprawdzi, że wynik się nie zmienił. _← strażnik_przykład_
  - `odwołanie` (blokująca) **U siebie masz już taki komentarz w pierwszej linii `kasa.py`**: Nawiązanie bez celu: żaden wcześniejszy dział nie tworzy pliku `kasa.py` ani komentarza w jego pierwszej linii (wcześniej jest `rozlicz.py`, a przykład w tej sekcji też go używa). Czytelnik nie ma takiego komentarza. Usuń zdanie albo zastąp je przykładem podanym na miejscu, np. pokaż linię `# udział na dwie osoby` nad `print(300 / 3)` i wyjaśnij, czemu jest nieaktualna. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Za chwilę go poprawisz i sprawdzisz, że nie wpływa na wynik**: Obietnica bez pokrycia: nic dalej nie prowadzi czytelnika przez poprawianie komentarza, a w planie nie ma tematu, który to spełni. Usuń zapowiedź albo od razu pokaż to w sekcji (kod z poprawionym komentarzem i ten sam wynik `100.0`). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie masz już taki komentarz w pierwszej linii `kasa.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: „Do czego służą komentarze”: 167 słów prozy, ```python 5 linii, ```text 2 linii; nowe hasła: komentarz; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0295-pisarz.md) · 18.6 s · $0.0850

### 0296 · kontrola_deterministyczna · dział 03 · pytanie 18 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0297 · weryfikator_pojęć · dział 03 · pytanie 18 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0297-weryfikator-pojec.md) · 5.0 s · $0.0223

### 0298 · znudzony_czytelnik · dział 03 · pytanie 18 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0298-znudzony-czytelnik.md) · 6.1 s · $0.0199

### 0299 · strażnik_przykład · dział 03 · pytanie 18 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Ostatni akapit odwołuje się do pliku `kasa.py` z komentarzem w pierwszej linii. W kanonie jest tylko `rozlicz.py`, a jego pierwsza linia (`# rozlicz.py - rozliczenie wspólnych wydatków`) jest aktualna, nie przestarzała. Zamień na `rozlicz.py` i dopasuj resztę zdania. Można np. zapowiedzieć, że czytelnik zmieni komentarz w `rozlicz.py`, uruchomi plik i sprawdzi, że wynik się nie zmienił. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0299-straznik-przyklad.md) · 6.1 s · $0.0229

### 0300 · strażnik_warsztat · dział 03 · pytanie 18 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0300-straznik-warsztat.md) · 7.4 s · $0.0204

### 0301 · weryfikator_odwołań · dział 03 · pytanie 18 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **U siebie masz już taki komentarz w pierwszej linii `kasa.py`**: Nawiązanie bez celu: żaden wcześniejszy dział nie tworzy pliku `kasa.py` ani komentarza w jego pierwszej linii (wcześniej jest `rozlicz.py`, a przykład w tej sekcji też go używa). Czytelnik nie ma takiego komentarza. Usuń zdanie albo zastąp je przykładem podanym na miejscu, np. pokaż linię `# udział na dwie osoby` nad `print(300 / 3)` i wyjaśnij, czemu jest nieaktualna. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Za chwilę go poprawisz i sprawdzisz, że nie wpływa na wynik**: Obietnica bez pokrycia: nic dalej nie prowadzi czytelnika przez poprawianie komentarza, a w planie nie ma tematu, który to spełni. Usuń zapowiedź albo od razu pokaż to w sekcji (kod z poprawionym komentarzem i ten sam wynik `100.0`). _← weryfikator_odwołań_
- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 1. (odwołania: 1)
- Nowe potrzeby (1):
  - `odwołanie` (blokująca, niespełniona) **U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej**: Nawiązanie do literówki `prnt` (dział 03) jest poprawne, ale zdanie nadal zakłada, że czytelnik ma w pierwszej linii swojego pliku komentarz. Żaden wcześniejszy dział go nie tworzy, więc to niezgodne z tym, co czytelnik ma w pliku. Usuń „komentarz w pierwszej linii” i zostaw samą literówkę `prnt`, albo pokaż na miejscu krótki kod: `# rozlicz.py` nad `prnt(...)`, z poprawką na `print` i wynikiem. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0301-weryfikator-odwolan.md) · 12.8 s · $0.0448

### 0302 · sprawdzacz_wyników · dział 03 · pytanie 18 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt`**: Ostatni akapit mówi o pliku czytelnika z literówką `prnt` w drugiej linii. Ta sekcja tego nie pokazuje. Warto dodać krótkie przypomnienie, o który plik chodzi, albo przykład z kodem i komunikatem błędu. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0302-sprawdzacz-wynikow.md) · 7.0 s · $0.0175

### 0303 · weryfikator_faktów · dział 03 · pytanie 18 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0303-weryfikator-faktow.md) · 14.2 s · $0.0622

### 0304 · decyzja · dział 03 · pytanie 18 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca, niespełniona) **U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej**: Nawiązanie do literówki `prnt` (dział 03) jest poprawne, ale zdanie nadal zakłada, że czytelnik ma w pierwszej linii swojego pliku komentarz. Żaden wcześniejszy dział go nie tworzy, więc to niezgodne z tym, co czytelnik ma w pliku. Usuń „komentarz w pierwszej linii” i zostaw samą literówkę `prnt`, albo pokaż na miejscu krótki kod: `# rozlicz.py` nad `prnt(...)`, z poprawką na `print` i wynikiem. _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0305 · akceptacja · dział 03 · pytanie 18

- Wynik: Sekcja [sec-03-do-czego-sluza-komentarze] dopisana do działu 03; hasła w glosariuszu: komentarz; kanony: przykład:+osoby; odwołania: wstecz „U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej”; punkty zaczepienia: nieaktualny komentarz o dwóch osobach, wyłączona instrukcja; w TODO zostało 43.
- 0.0 s

### 0306 · łowca_pułapek · dział 03 · pytanie 18

- Wynik: „Do czego służą komentarze”: brak pułapek
- [prompt i odpowiedź](_przebieg/0306-lowca-pulapek.md) · 3.6 s · $0.0168

### 0307 · autor_dodatków · dział 03 · pytanie 18

- Wynik: „Do czego służą komentarze”: dykteryjki: Komentarz, który przestał mówić prawdę
- [prompt i odpowiedź](_przebieg/0307-autor-dodatkow.md) · 7.7 s · $0.0461

### 0308 · weryfikator_dodatków · dział 03 · pytanie 18

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0308-weryfikator-dodatkow.md) · 6.4 s · $0.0405

### 0309 · autor_wstępu · dział 04 · próba 1

- Kolejka TODO (43): 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30 …
- Wynik: Wstęp: 94 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0309-autor-wstepu.md) · 6.2 s · $0.0224

### 0310 · recenzent_wstępu · dział 04 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `diagram` (sugestia) **kwota ← 45.50 (liczba) itd.**: Strzałka ← nie jest nigdzie wyjaśniona, a w pierwszej linii diagramu strzałka → znaczy coś innego (składanie w program). Dodaj krótki podpis, np. „nazwa ← wartość (wartość trafia pod nazwę)”, albo narysuj pudełka z etykietą: [kwota: 45.50]. Warto też oddzielić wizualnie dwie części albo dać im nagłówki, żeby nie wyglądały na jeden przepływ. _← recenzent_wstępu_
  - `diagram` (sugestia) **instrukcje (dział 03) + dane (dział 04) → program**: Pierwsza linia mówi to samo co zdanie „Do tej pory pisaliśmy instrukcje… teraz dostaną dane” i niewiele dodaje. Można ją usunąć albo połączyć z drugą częścią, tak by diagram pokazywał dane wchodzące do instrukcji. _← recenzent_wstępu_
  - `język` (sugestia) **True, 45.50**: Czytelnik spoza IT zobaczy w diagramie „True” i kropkę dziesiętną zamiast przecinka bez żadnego sygnału, że tak wygląda zapis w Pythonie. Dodaj podpis, np. „zapis w Pythonie”, żeby nie wyglądało to na błąd. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0310-recenzent-wstepu.md) · 12.7 s · $0.0241

### 0311 · pisarz · dział 04 · pytanie 19 · próba 1

- Kolejka TODO (42): 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31 …
- Wynik: „Czym jest dana”: 151 słów prozy, ```python 3 linii, ```text 3 linii; nowe hasła: dana; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0311-pisarz.md) · 22.0 s · $0.0778

### 0312 · kontrola_deterministyczna · dział 04 · pytanie 19 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **wydatku**: „wydatku” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
- 0.0 s

### 0313 · weryfikator_pojęć · dział 04 · pytanie 19 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0313-weryfikator-pojec.md) · 5.4 s · $0.0224

### 0314 · znudzony_czytelnik · dział 04 · pytanie 19 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **dostajesz z zewnątrz**: Zdanie „dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz” jest ogólnikowe. Wystarczy jedno konkretne wskazanie, np. „wpisane z klawiatury lub wczytane z pliku”. Można też usunąć „albo dostajesz z zewnątrz”, skoro w tutorialu nie ma o tym przykładu. Zdanie „imion nie da się dodać” jest też uproszczone, bo napisy można łączyć, ale dla początkującego to zrozumiałe. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0314-znudzony-czytelnik.md) · 7.4 s · $0.0210

### 0315 · strażnik_przykład · dział 04 · pytanie 19 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **kasa.py**: Tekst mówi, że czytelnik dopisze dane „u siebie w `kasa.py`”, ale w kanonie plik programu nazywa się `rozlicz.py` (skrypt główny, w folderze wspolna_kasa). Nazwa `kasa.py` nie została zadeklarowana jako zmiana. Zamień na `rozlicz.py`. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0315-straznik-przyklad.md) · 6.1 s · $0.0209

### 0316 · strażnik_warsztat · dział 04 · pytanie 19 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **krok 1 (zmienne i type())**: Krok 1 używa zmiennych (nazwa_wyjazdu = "Mazury") i funkcji type(), a tekst tylko zapowiada zmienną w następnej sekcji. Dodaj jedno zdanie, np.: „W kodzie użyjemy nazw, pod którymi Python zapamięta dane (o zmiennych więcej w następnej sekcji), oraz type(), które pokazuje rodzaj danej.” _← strażnik_warsztat_
  - `spójność` (sugestia) **wynik kroku 2 (str, float, bool)**: Wynik zawiera nazwy str, float i bool, a tekst ich nie objaśnia. Dodaj zdanie, np.: „str to tekst, float to liczba z przecinkiem, bool to prawda/fałsz.” _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0316-straznik-warsztat.md) · 10.5 s · $0.0245

### 0317 · weryfikator_odwołań · dział 04 · pytanie 19 · próba 1

- Wynik: 2 blokujących, 1 sugestii. (odwołania: 3)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **kwoty da się dodać, imion nie**: Zdanie „kwoty da się dodać, imion nie” jest nieprecyzyjne i wprowadza w błąd: teksty też można „dodawać” (łączyć: "Ania" + "Kowalska"), a program o tym mówi osobno. Zmienić na przykład na: „kwoty da się dodać i podzielić, a imion nie da się ich podzielić ani odjąć” albo „kwoty da się dodać jako liczby, a imiona można tylko zestawić lub porównać”. Najlepiej dać jeden krótki przykład, co wolno z liczbą (np. 45.5 + 10), a czego nie z tekstem (np. dzielenie imienia). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie w `kasa.py` dopiszesz za chwilę**: Zapowiedź „dopiszesz za chwilę … w kasa.py … sprawdzisz, jak Python je nazywa” nie wskazuje żadnego znanego miejsca: plik kasa.py nie pojawił się w poprzednim dziale (był rozlicz.py), a „za chwilę” nie ma pokrycia w tej sekcji. Usunąć zdanie albo napisać, o jakim temacie wróci (np. „w osobnej sekcji sprawdzisz, jak Python nazywa rodzaje danych”), bez zakładania pliku, którego czytelnik nie zna. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **typów**: Słowo „typów” w zapowiedzi „gdy przejdziemy do typów” nie jest wcześniej wprowadzone; lepiej napisać „rodzaje danych (nazywane typami) omówimy osobno”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0317-weryfikator-odwolan.md) · 19.7 s · $0.0452

### 0318 · sprawdzacz_wyników · dział 04 · pytanie 19 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0318-sprawdzacz-wynikow.md) · 2.8 s · $0.0103

### 0319 · weryfikator_faktów · dział 04 · pytanie 19 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0319-weryfikator-faktow.md) · 5.5 s · $0.0276

### 0320 · decyzja · dział 04 · pytanie 19 · próba 1

- Potrzeby w kolejce przed krokiem (4):
  - `spójność` (blokująca) **wydatku**: „wydatku” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
  - `spójność` (blokująca) **kasa.py**: Tekst mówi, że czytelnik dopisze dane „u siebie w `kasa.py`”, ale w kanonie plik programu nazywa się `rozlicz.py` (skrypt główny, w folderze wspolna_kasa). Nazwa `kasa.py` nie została zadeklarowana jako zmiana. Zamień na `rozlicz.py`. _← strażnik_przykład_
  - `odwołanie` (blokująca) **kwoty da się dodać, imion nie**: Zdanie „kwoty da się dodać, imion nie” jest nieprecyzyjne i wprowadza w błąd: teksty też można „dodawać” (łączyć: "Ania" + "Kowalska"), a program o tym mówi osobno. Zmienić na przykład na: „kwoty da się dodać i podzielić, a imion nie da się ich podzielić ani odjąć” albo „kwoty da się dodać jako liczby, a imiona można tylko zestawić lub porównać”. Najlepiej dać jeden krótki przykład, co wolno z liczbą (np. 45.5 + 10), a czego nie z tekstem (np. dzielenie imienia). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie w `kasa.py` dopiszesz za chwilę**: Zapowiedź „dopiszesz za chwilę … w kasa.py … sprawdzisz, jak Python je nazywa” nie wskazuje żadnego znanego miejsca: plik kasa.py nie pojawił się w poprzednim dziale (był rozlicz.py), a „za chwilę” nie ma pokrycia w tej sekcji. Usunąć zdanie albo napisać, o jakim temacie wróci (np. „w osobnej sekcji sprawdzisz, jak Python nazywa rodzaje danych”), bez zakładania pliku, którego czytelnik nie zna. _← weryfikator_odwołań_
- Wynik: Do poprawy: 4 blokujących potrzeb wraca do pisarza; 4 sugestii trafia do raportu.
- 0.0 s

### 0321 · pisarz · dział 04 · pytanie 19 · próba 2

- Kolejka TODO (42): 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31 …
- Potrzeby w kolejce przed krokiem (4):
  - `spójność` (blokująca) **wydatku**: „wydatku” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
  - `spójność` (blokująca) **kasa.py**: Tekst mówi, że czytelnik dopisze dane „u siebie w `kasa.py`”, ale w kanonie plik programu nazywa się `rozlicz.py` (skrypt główny, w folderze wspolna_kasa). Nazwa `kasa.py` nie została zadeklarowana jako zmiana. Zamień na `rozlicz.py`. _← strażnik_przykład_
  - `odwołanie` (blokująca) **kwoty da się dodać, imion nie**: Zdanie „kwoty da się dodać, imion nie” jest nieprecyzyjne i wprowadza w błąd: teksty też można „dodawać” (łączyć: "Ania" + "Kowalska"), a program o tym mówi osobno. Zmienić na przykład na: „kwoty da się dodać i podzielić, a imion nie da się ich podzielić ani odjąć” albo „kwoty da się dodać jako liczby, a imiona można tylko zestawić lub porównać”. Najlepiej dać jeden krótki przykład, co wolno z liczbą (np. 45.5 + 10), a czego nie z tekstem (np. dzielenie imienia). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie w `kasa.py` dopiszesz za chwilę**: Zapowiedź „dopiszesz za chwilę … w kasa.py … sprawdzisz, jak Python je nazywa” nie wskazuje żadnego znanego miejsca: plik kasa.py nie pojawił się w poprzednim dziale (był rozlicz.py), a „za chwilę” nie ma pokrycia w tej sekcji. Usunąć zdanie albo napisać, o jakim temacie wróci (np. „w osobnej sekcji sprawdzisz, jak Python nazywa rodzaje danych”), bez zakładania pliku, którego czytelnik nie zna. _← weryfikator_odwołań_
- Wynik: „Czym jest dana”: 151 słów prozy, ```python 5 linii, ```text 4 linii; nowe hasła: dana
- [prompt i odpowiedź](_przebieg/0321-pisarz.md) · 16.7 s · $0.0790

### 0322 · kontrola_deterministyczna · dział 04 · pytanie 19 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0323 · weryfikator_pojęć · dział 04 · pytanie 19 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0323-weryfikator-pojec.md) · 4.6 s · $0.0219

### 0324 · znudzony_czytelnik · dział 04 · pytanie 19 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **akapit „Każda z tych trzech wartości…”**: Teza, że rodzaj danej decyduje o tym, co da się z nią zrobić, jest pokazana tylko od strony „działa” (45.5 + 10). Brakuje krótkiego przeciwprzykładu, np. print("Ania" + 10) i komunikatu o błędzie. Wtedy czytelnik zobaczy, że program naprawdę odmawia, a nie tylko usłyszy, że „to nie ma sensu”. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0324-znudzony-czytelnik.md) · 7.7 s · $0.0212

### 0325 · strażnik_przykład · dział 04 · pytanie 19 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Tekst mówi, że czytelnik dopisze dane „u siebie w `kasa.py`”, ale w kanonie plik programu nazywa się `rozlicz.py` (skrypt główny, w folderze wspolna_kasa). Nazwa `kasa.py` nie została zadeklarowana jako zmiana. Zamień na `rozlicz.py`. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0325-straznik-przyklad.md) · 3.6 s · $0.0200

### 0326 · weryfikator_odwołań · dział 04 · pytanie 19 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **kwoty da się dodać, imion nie**: Zdanie „kwoty da się dodać, imion nie” jest nieprecyzyjne i wprowadza w błąd: teksty też można „dodawać” (łączyć: "Ania" + "Kowalska"), a program o tym mówi osobno. Zmienić na przykład na: „kwoty da się dodać i podzielić, a imion nie da się ich podzielić ani odjąć” albo „kwoty da się dodać jako liczby, a imiona można tylko zestawić lub porównać”. Najlepiej dać jeden krótki przykład, co wolno z liczbą (np. 45.5 + 10), a czego nie z tekstem (np. dzielenie imienia). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **U siebie w `kasa.py` dopiszesz za chwilę**: Zapowiedź „dopiszesz za chwilę … w kasa.py … sprawdzisz, jak Python je nazywa” nie wskazuje żadnego znanego miejsca: plik kasa.py nie pojawił się w poprzednim dziale (był rozlicz.py), a „za chwilę” nie ma pokrycia w tej sekcji. Usunąć zdanie albo napisać, o jakim temacie wróci (np. „w osobnej sekcji sprawdzisz, jak Python nazywa rodzaje danych”), bez zakładania pliku, którego czytelnik nie zna. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/0326-weryfikator-odwolan.md) · 3.8 s · $0.0321

### 0327 · sprawdzacz_wyników · dział 04 · pytanie 19 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0327-sprawdzacz-wynikow.md) · 4.2 s · $0.0139

### 0328 · weryfikator_faktów · dział 04 · pytanie 19 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0328-weryfikator-faktow.md) · 5.2 s · $0.0276

### 0329 · decyzja · dział 04 · pytanie 19 · próba 2

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 0330 · akceptacja · dział 04 · pytanie 19

- Wynik: Sekcja [sec-04-czym-jest-dana] dopisana do działu 04; hasła w glosariuszu: dana; odwołania: w przód „Do tego służy zmienna, którą poznasz w następnej sekcji”, w przód „wyjaśnimy przy typach danych”; punkty zaczepienia: imienia nie da się podzielić; w TODO zostało 42.
- 0.0 s

### 0331 · łowca_pułapek · dział 04 · pytanie 19

- Wynik: „Czym jest dana”: brak pułapek
- [prompt i odpowiedź](_przebieg/0331-lowca-pulapek.md) · 2.2 s · $0.0127

### 0332 · autor_dodatków · dział 04 · pytanie 19

- Wynik: „Czym jest dana”: dowcipy: Program bez danych jak kuchnia bez produktów
- [prompt i odpowiedź](_przebieg/0332-autor-dodatkow.md) · 14.3 s · $0.0539

### 0333 · weryfikator_dodatków · dział 04 · pytanie 19

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0333-weryfikator-dodatkow.md) · 4.6 s · $0.0404

### 0334 · pisarz · dział 04 · pytanie 20 · próba 1

- Kolejka TODO (41): 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 …
- Wynik: „Czym jest zmienna”: 159 słów prozy, ```python 6 linii, ```text 2 linii; nowe hasła: zmienna; wątki: przykład dodaj imie, przykład dodaj kwota, przykład dodaj zaplacono; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0334-pisarz.md) · 26.2 s · $0.0861

### 0335 · kontrola_deterministyczna · dział 04 · pytanie 20 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0336 · weryfikator_pojęć · dział 04 · pytanie 20 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **True**: wystarczy jedno zdanie; pełne omówienie w pytaniu 24. W kodzie pojawia się `True` bez wyjaśnienia. Wystarczy dopisać, że to wartość logiczna „prawda” (odpowiedź tak/nie), tu: czy zapłacono. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **"Ania"**: wystarczy jedno zdanie; pełne omówienie w pytaniu 22. Czytelnik może nie wiedzieć, dlaczego "Ania" jest w cudzysłowie, a 45.5 nie. Wystarczy krótka uwaga, że cudzysłów oznacza tekst. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0336-weryfikator-pojec.md) · 10.9 s · $0.0277

### 0337 · znudzony_czytelnik · dział 04 · pytanie 20 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `skrócenie` (sugestia) **Ostatni akapit (kasa.py)**: Ostatni akapit o tym, że w `kasa.py` zobaczysz rodzaj danej każdej zmiennej, jest niejasny. Nie wiadomo, czym jest `kasa.py` ani jak coś w nim „zobaczysz”. Odsyła też do typów danych, które już padły w poprzedniej sekcji. Można go usunąć, a zaoszczędzone słowa przeznaczyć na domknięcie wątku „Wspólnej Kasy”. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0337-znudzony-czytelnik.md) · 7.6 s · $0.0215

### 0338 · strażnik_przykład · dział 04 · pytanie 20 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a w kanonie program to `rozlicz.py` (wspolna_kasa/rozlicz.py). Zmiana nie jest zadeklarowana w canon_changes. Zamień na `rozlicz.py`. _← strażnik_przykład_
  - `spójność` (sugestia) **zmienne w rozlicz.py**: Zdanie „u siebie zobaczysz, jakiego rodzaju daną trzyma każda zmienna” sugeruje, że plik pokazuje typy, a w kodzie tego nie ma. Przeformułuj: „każda dana ma swój rodzaj (tekst, liczba, prawda/fałsz); nazwy wyjaśnimy przy typach danych”. Możesz dodać do przykładu `print(type(kwota))`, jeśli chcesz to pokazać. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0338-straznik-przyklad.md) · 8.3 s · $0.0245

### 0339 · strażnik_warsztat · dział 04 · pytanie 20 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0339-straznik-warsztat.md) · 6.1 s · $0.0199

### 0340 · weryfikator_odwołań · dział 04 · pytanie 20 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 5)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **kasa.py**: Zdanie „U siebie w `kasa.py` zobaczysz też, jakiego rodzaju daną trzyma każda zmienna” nie mówi, jak to zobaczyć, a plik `kasa.py` nie został wcześniej przedstawiony w tej sekcji. Dodaj krótki przykład albo usuń zdanie i zostaw samą zapowiedź typów. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **komórka w arkuszu**: Porównanie „nazwałeś” zakłada rodzaj męski czytelnika. Lepiej: „komórka arkusza, która ma nazwę »kwota«”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0340-weryfikator-odwolan.md) · 16.0 s · $0.0442

### 0341 · sprawdzacz_wyników · dział 04 · pytanie 20 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **To trochę jak komórka w arkuszu, którą nazwałeś „kwota”**: Zwrot „którą nazwałeś” zakłada płeć czytelnika. Lepiej użyć formy neutralnej, np. „komórka, której nadano nazwę „kwota”” albo „komórka o nazwie „kwota””. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0341-sprawdzacz-wynikow.md) · 6.0 s · $0.0156

### 0342 · weryfikator_faktów · dział 04 · pytanie 20 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0342-weryfikator-faktow.md) · 5.4 s · $0.0277

### 0343 · decyzja · dział 04 · pytanie 20 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a w kanonie program to `rozlicz.py` (wspolna_kasa/rozlicz.py). Zmiana nie jest zadeklarowana w canon_changes. Zamień na `rozlicz.py`. _← strażnik_przykład_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 7 sugestii trafia do raportu.
- 0.0 s

### 0344 · pisarz · dział 04 · pytanie 20 · próba 2

- Kolejka TODO (41): 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32 …
- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a w kanonie program to `rozlicz.py` (wspolna_kasa/rozlicz.py). Zmiana nie jest zadeklarowana w canon_changes. Zamień na `rozlicz.py`. _← strażnik_przykład_
- Wynik: „Czym jest zmienna”: 142 słów prozy, ```python 6 linii, ```text 2 linii; nowe hasła: zmienna; wątki: przykład dodaj imie, przykład dodaj kwota, przykład dodaj zaplacono
- [prompt i odpowiedź](_przebieg/0344-pisarz.md) · 16.1 s · $0.0795

### 0345 · kontrola_deterministyczna · dział 04 · pytanie 20 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0346 · weryfikator_pojęć · dział 04 · pytanie 20 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **True**: wystarczy jedno zdanie; pełne omówienie w pytaniu 24. W przykładzie `zaplacono = True` i w wyniku pojawia się `True` bez wyjaśnienia, że to wartość logiczna (prawda/fałsz, tu: „tak, zapłacono”). _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **imie = "Ania"**: wystarczy jedno zdanie; pełne omówienie w pytaniu 22. Nie wyjaśniono, że cudzysłów w `"Ania"` oznacza tekst, a `45.5` to liczba (z kropką zamiast przecinka). _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0346-weryfikator-pojec.md) · 9.8 s · $0.0267

### 0347 · znudzony_czytelnik · dział 04 · pytanie 20 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0347-znudzony-czytelnik.md) · 5.7 s · $0.0188

### 0348 · strażnik_przykład · dział 04 · pytanie 20 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a w kanonie program to `rozlicz.py` (wspolna_kasa/rozlicz.py). Zmiana nie jest zadeklarowana w canon_changes. Zamień na `rozlicz.py`. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0348-straznik-przyklad.md) · 2.8 s · $0.0191

### 0349 · weryfikator_odwołań · dział 04 · pytanie 20 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **komórka w arkuszu**: „którą nazwałeś” zakłada rodzaj męski czytelnika. Lepiej bezosobowo: „którą nazwano »kwota«” albo „komórka nazwana »kwota«”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0349-weryfikator-odwolan.md) · 11.4 s · $0.0374

### 0350 · sprawdzacz_wyników · dział 04 · pytanie 20 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0350-sprawdzacz-wynikow.md) · 4.3 s · $0.0141

### 0351 · weryfikator_faktów · dział 04 · pytanie 20 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0351-weryfikator-faktow.md) · 4.8 s · $0.0273

### 0352 · decyzja · dział 04 · pytanie 20 · próba 2

- Wynik: Sekcja przyjęta; 3 sugestii trafia do raportu.
- 0.0 s

### 0353 · akceptacja · dział 04 · pytanie 20

- Wynik: Sekcja [sec-04-czym-jest-zmienna] dopisana do działu 04; hasła w glosariuszu: zmienna; kanony: przykład:+imie przykład:+kwota przykład:+zaplacono; odwołania: wstecz „Pamiętasz, że dane trzeba gdzieś przechowywać”, w przód „Dokładniej opiszemy to przy przypisaniu”; punkty zaczepienia: zmiana kwoty; w TODO zostało 41.
- 0.0 s

### 0354 · łowca_pułapek · dział 04 · pytanie 20

- Wynik: „Czym jest zmienna”: Zmiana wartości zmienia też typ
- [prompt i odpowiedź](_przebieg/0354-lowca-pulapek.md) · 3.9 s · $0.0167

### 0355 · autor_dodatków · dział 04 · pytanie 20

- Wynik: „Czym jest zmienna”: wtręty: Marta wpisuje kwotę w pięciu miejscach, rysunki: Pudełko z etykietą zamiast liczby
- [prompt i odpowiedź](_przebieg/0355-autor-dodatkow.md) · 11.0 s · $0.0527

### 0356 · weryfikator_dodatków · dział 04 · pytanie 20

- Wynik: odrzucone: 1; Pudełko z etykietą zamiast liczby: Etykiety są „puste”, a zmienna to miejsce z nazwą, więc rysunek przeczy sekcji (nazwa jest jej sednem) i własnemu tytułowi „pudełko z etykietą”.
- [prompt i odpowiedź](_przebieg/0356-weryfikator-dodatkow.md) · 8.4 s · $0.0459

### 0357 · pisarz · dział 04 · pytanie 21 · próba 1

- Kolejka TODO (40): 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33 …
- Wynik: „Zmienna jako pudełko z etykietą”: 128 słów prozy, ```text 4 linii, ```python 5 linii, ```text 1 linii; nowe hasła: wartość zmiennej; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0357-pisarz.md) · 21.7 s · $0.0783

### 0358 · kontrola_deterministyczna · dział 04 · pytanie 21 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0359 · weryfikator_pojęć · dział 04 · pytanie 21 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0359-weryfikator-pojec.md) · 4.5 s · $0.0215

### 0360 · znudzony_czytelnik · dział 04 · pytanie 21 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `tempo` (sugestia) **akapit „Porównanie tłumaczy trzy rzeczy”**: Nadpisywanie wartości i stała nazwa były już w poprzedniej sekcji („stara kwota znika, a nowa zajmuje jej miejsce”). Nowe jest głównie to, że kopia jest niezależna. Warto skrócić powtórkę i położyć nacisk na kopiowanie. _← znudzony_czytelnik_
  - `konkret` (sugestia) **zdanie „Obraz jest uproszczony… Ważna konsekwencja”**: „Pod spodem Python działa nieco inaczej” jest ogólnikiem. Wniosek o czytelnej etykiecie nie wynika z porównania z pudełkiem. Można go połączyć z jednym konkretnym przykładem, np. `kwota` kontra `x`, albo pominąć. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0360-znudzony-czytelnik.md) · 7.7 s · $0.0219

### 0361 · strażnik_przykład · dział 04 · pytanie 21 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0361-straznik-przyklad.md) · 5.7 s · $0.0209

### 0362 · strażnik_warsztat · dział 04 · pytanie 21 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **akapit „Porównanie tłumaczy trzy rzeczy”**: Tekst mówi o „zmianie kwoty z poprzedniej sekcji”, ale w stanie czytelnika jest tylko print("Wspólna Kasa"), więc żadnej zmiany kwoty jeszcze nie było. Zamień na: „jak w przypadku zmiany wartości, którą pokażemy za chwilę” albo usuń odwołanie. _← strażnik_warsztat_
  - `spójność` (sugestia) **ostatni akapit i diagram**: Tekst i diagram używają nazwy `kwota`, a w kasa.py zmienna nazywa się `kwota_wydatku`. Zamień w zdaniu o „Wspólnej Kasie” `kwota` na `kwota_wydatku` (albo w diagramie etykietę na `kwota_wydatku`). _← strażnik_warsztat_
  - `spójność` (sugestia) **blok kodu poza kanonem**: Przykład „poza kanonem” nie jest krokiem warsztatu i nie zmienia kasa.py. Dodaj zdanie, że można go uruchomić w osobnym pliku, albo że to tylko ilustracja. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0362-straznik-warsztat.md) · 11.3 s · $0.0250

### 0363 · weryfikator_odwołań · dział 04 · pytanie 21 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **„Wspólnej Kasie”**: Nazwa „Wspólna Kasa” nie ma punktu zaczepienia w tym ani poprzednim dziale. Jeśli to program przewodni, dodaj pół zdania przypominającego, czym jest (np. „w programie do rozliczania wspólnych wydatków”). Czytelnik spoza IT może nie kojarzyć nazwy. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0363-weryfikator-odwolan.md) · 12.6 s · $0.0386

### 0364 · sprawdzacz_wyników · dział 04 · pytanie 21 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0364-sprawdzacz-wynikow.md) · 4.1 s · $0.0138

### 0365 · weryfikator_faktów · dział 04 · pytanie 21 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0365-weryfikator-faktow.md) · 6.9 s · $0.0293

### 0366 · decyzja · dział 04 · pytanie 21 · próba 1

- Wynik: Sekcja przyjęta; 6 sugestii trafia do raportu.
- 0.0 s

### 0367 · akceptacja · dział 04 · pytanie 21

- Wynik: Sekcja [sec-04-zmienna-jako-pudelko-z-etykieta] dopisana do działu 04; hasła w glosariuszu: wartość zmiennej; odwołania: wstecz „zmiany kwoty z poprzedniej sekcji”, poza tutorialem „W „Wspólnej Kasie” pudełko `kwota`”; punkty zaczepienia: pudełko i kopia; w TODO zostało 40.
- 0.0 s

### 0368 · łowca_pułapek · dział 04 · pytanie 21

- Wynik: „Zmienna jako pudełko z etykietą”: brak pułapek
- [prompt i odpowiedź](_przebieg/0368-lowca-pulapek.md) · 2.4 s · $0.0129

### 0369 · autor_dodatków · dział 04 · pytanie 21

- Wynik: „Zmienna jako pudełko z etykietą”: dykteryjki: Zmienna o nazwie x, rysunki: Dwa pudełka, dwie etykiety
- [prompt i odpowiedź](_przebieg/0369-autor-dodatkow.md) · 13.9 s · $0.0563

### 0370 · weryfikator_dodatków · dział 04 · pytanie 21

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0370-weryfikator-dodatkow.md) · 10.9 s · $0.0497

### 0371 · pisarz · dział 04 · pytanie 22 · próba 1

- Kolejka TODO (39): 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34 …
- Wynik: „Liczba a tekst”: 155 słów prozy, ```python 4 linii, ```text 2 linii; warsztat: kasa.py, $ python kasa.py (błąd), kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0371-pisarz.md) · 35.9 s · $0.0961

### 0372 · kontrola_deterministyczna · dział 04 · pytanie 22 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0373 · weryfikator_pojęć · dział 04 · pytanie 22 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **TypeError**: wystarczy jedno zdanie; pełne omówienie w pytaniu 51. Warto dodać, że TypeError to nazwa błędu w rodzaju „ta operacja nie pasuje do tego rodzaju danych”. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0373-weryfikator-pojec.md) · 7.2 s · $0.0243

### 0374 · znudzony_czytelnik · dział 04 · pytanie 22 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `fakt` (blokująca) **zdanie o działaniach na tekście**: Zdanie „Liczbę można dzielić, mnożyć i dodawać. Tekstu nie” jest nieprawdziwe. W Pythonie "Ania" + "Kowalska" skleja teksty, a "Ha" * 3 daje "HaHaHa". Czytelnik wyniesie błędne przekonanie, a potem się zdziwi. Trzeba zawęzić do dzielenia, które tabela już pokazuje: „Tekstu nie da się dzielić”. Można też dodać, że plus skleja teksty zamiast liczyć. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0374-znudzony-czytelnik.md) · 11.8 s · $0.0238

### 0375 · strażnik_przykład · dział 04 · pytanie 22 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a plik programu w kanonie nazywa się `rozlicz.py` (wspolna_kasa/rozlicz.py). Zamień `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0375-straznik-przyklad.md) · 7.0 s · $0.0225

### 0376 · strażnik_warsztat · dział 04 · pytanie 22 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **zdanie o kropce dziesiętnej / kasa.py**: Tekst pisze, że w „Wspólnej Kasie” jest `kwota = 45.5`, ale w kasa.py zmienna nazywa się `kwota_wydatku`. Popraw na: „tak jak `kwota_wydatku = 45.5` w „Wspólnej Kasie”” albo napisz, że przykład używa krótszej nazwy. _← strażnik_warsztat_
  - `spójność` (sugestia) **akapit „Liczbę można dzielić…”**: Zdanie o błędzie mówi o imieniu „Ania”, a w kasa.py błąd powstaje na `nazwa_wyjazdu` ("Mazury"). Zmień na np.: „u siebie zobaczysz to za chwilę w kasa.py, gdy spróbujesz podzielić nazwę wyjazdu”. _← strażnik_warsztat_
  - `wynik` (sugestia) **krok 2**: Ścieżka w tracebacku (/home/user/wspolna_kasa/kasa.py) będzie u czytelnika inna (np. /home/<nazwa>/wspolna_kasa/kasa.py albo C:\Users\...). Warto dodać uwagę, że ścieżka w pierwszej linii będzie się różnić. Reszta wyniku (numer linii 7, znaczniki ~~~^~~, treść TypeError) jest zgodna z Pythonem 3.13. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0376-straznik-warsztat.md) · 16.1 s · $0.0313

### 0377 · weryfikator_odwołań · dział 04 · pytanie 22 · próba 1

- Wynik: 1 blokujących, 2 sugestii. (odwołania: 4)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie**: Zdanie „Liczbę można dzielić, mnożyć i dodawać. Tekstu nie” oraz „tekst… program tylko przechowuje, wypisuje i porównuje” jest nieprawdziwe: teksty można dodawać (łączyć), np. "Ala" + "Ola", a nawet mnożyć przez liczbę całkowitą. Czytelnik wyniesie błędne przekonanie i pomyli się przy późniejszym łączeniu tekstów. Popraw na: tekstu nie da się dzielić (ani odejmować); dodawanie tekstów ma inne znaczenie (łączenie) i omówimy je osobno. Usuń też „tylko” z definicji tekstu albo dodaj „łączy”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **TypeError**: `TypeError` pojawia się bez wyjaśnienia. Dodaj krótko, że to nazwa komunikatu o błędzie oznaczającego „zła rodzaj danych do tego działania”, albo napisz zwyczajnie „komunikat o błędzie”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **Tekstu nie**: Teza, że tekstu nie da się dzielić, nie ma pokazanego przykładu w kodzie. Dodaj krótki blok z `print(imie / 2)` i fragmentem komunikatu błędu, zamiast odsyłać do kasa.py. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0377-weryfikator-odwolan.md) · 22.1 s · $0.0506

### 0378 · sprawdzacz_wyników · dział 04 · pytanie 22 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `wynik` (blokująca) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie**: Zdanie sugeruje, że tekstu nie da się dodawać ani mnożyć, a w Pythonie się da: "Ania" + "Kasia" skleja teksty, a "Ha" * 3 daje "HaHaHa". Trzeba zawęzić twierdzenie do dzielenia albo do liczenia na wartościach, np. „Liczbę można dzielić. Tekstu nie: "Ania" / 2 kończy się błędem TypeError”. Ta sama nieścisłość jest w zdaniu „program tylko przechowuje, wypisuje i porównuje”, bo tekst można też sklejać. Sugerowana poprawka: dopisać „i skleja”, albo pominąć dodawanie. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **[[imienia nie da się podzielić|imię „Ania” nie do podzielenia przez 2]]**: Zdanie „to ta sama myśl co …” jest niezgrabne, a etykieta odwołania jest po polsku nieprawidłowa („nie do podzielenia przez 2”). Lepiej: „tak jak imienia „Ania” nie da się podzielić przez 2”. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **Tekstu nie [można dzielić]**: Teza, że tekstu nie da się dzielić, nie ma tu własnego przykładu kodu z błędem. Tekst odsyła do późniejszego kasa.py. Warto dać jedną linię, np. print("Ania" / 2), i wskazać, że kończy się TypeError. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0378-sprawdzacz-wynikow.md) · 14.9 s · $0.0250

### 0379 · weryfikator_faktów · dział 04 · pytanie 22 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 2)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie:**: Dokumentacja Pythona 3.13 (https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/introduction.rst) pokazuje, że teksty można dodawać (`'Py' + 'thon'` daje 'Python', czyli sklejanie) i mnożyć przez liczbę całkowitą (`3 * 'un'` daje 'unununium'). Zdanie 'Tekstu nie' jest więc nieścisłe. Popraw na: 'Tekstu nie da się dzielić (ani odejmować); dodawanie i mnożenie działają na tekście inaczej niż na liczbach.' Albo ogranicz zdanie do dzielenia: 'Liczbę można dzielić, tekstu nie.' Tabela ('Można dzielić?') jest poprawna. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0379-weryfikator-faktow.md) · 18.1 s · $0.0712

### 0380 · decyzja · dział 04 · pytanie 22 · próba 1

- Potrzeby w kolejce przed krokiem (4):
  - `fakt` (blokująca) **zdanie o działaniach na tekście**: Zdanie „Liczbę można dzielić, mnożyć i dodawać. Tekstu nie” jest nieprawdziwe. W Pythonie "Ania" + "Kowalska" skleja teksty, a "Ha" * 3 daje "HaHaHa". Czytelnik wyniesie błędne przekonanie, a potem się zdziwi. Trzeba zawęzić do dzielenia, które tabela już pokazuje: „Tekstu nie da się dzielić”. Można też dodać, że plus skleja teksty zamiast liczyć. _← znudzony_czytelnik_
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a plik programu w kanonie nazywa się `rozlicz.py` (wspolna_kasa/rozlicz.py). Zamień `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
  - `odwołanie` (blokująca) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie**: Zdanie „Liczbę można dzielić, mnożyć i dodawać. Tekstu nie” oraz „tekst… program tylko przechowuje, wypisuje i porównuje” jest nieprawdziwe: teksty można dodawać (łączyć), np. "Ala" + "Ola", a nawet mnożyć przez liczbę całkowitą. Czytelnik wyniesie błędne przekonanie i pomyli się przy późniejszym łączeniu tekstów. Popraw na: tekstu nie da się dzielić (ani odejmować); dodawanie tekstów ma inne znaczenie (łączenie) i omówimy je osobno. Usuń też „tylko” z definicji tekstu albo dodaj „łączy”. _← weryfikator_odwołań_
  - `wynik` (blokująca) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie**: Zdanie sugeruje, że tekstu nie da się dodawać ani mnożyć, a w Pythonie się da: "Ania" + "Kasia" skleja teksty, a "Ha" * 3 daje "HaHaHa". Trzeba zawęzić twierdzenie do dzielenia albo do liczenia na wartościach, np. „Liczbę można dzielić. Tekstu nie: "Ania" / 2 kończy się błędem TypeError”. Ta sama nieścisłość jest w zdaniu „program tylko przechowuje, wypisuje i porównuje”, bo tekst można też sklejać. Sugerowana poprawka: dopisać „i skleja”, albo pominąć dodawanie. _← sprawdzacz_wyników_
- Wynik: Do poprawy: 4 blokujących potrzeb wraca do pisarza; 9 sugestii trafia do raportu.
- 0.0 s

### 0381 · pisarz · dział 04 · pytanie 22 · próba 2

- Kolejka TODO (39): 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34 …
- Potrzeby w kolejce przed krokiem (4):
  - `fakt` (blokująca) **zdanie o działaniach na tekście**: Zdanie „Liczbę można dzielić, mnożyć i dodawać. Tekstu nie” jest nieprawdziwe. W Pythonie "Ania" + "Kowalska" skleja teksty, a "Ha" * 3 daje "HaHaHa". Czytelnik wyniesie błędne przekonanie, a potem się zdziwi. Trzeba zawęzić do dzielenia, które tabela już pokazuje: „Tekstu nie da się dzielić”. Można też dodać, że plus skleja teksty zamiast liczyć. _← znudzony_czytelnik_
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a plik programu w kanonie nazywa się `rozlicz.py` (wspolna_kasa/rozlicz.py). Zamień `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
  - `odwołanie` (blokująca) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie**: Zdanie „Liczbę można dzielić, mnożyć i dodawać. Tekstu nie” oraz „tekst… program tylko przechowuje, wypisuje i porównuje” jest nieprawdziwe: teksty można dodawać (łączyć), np. "Ala" + "Ola", a nawet mnożyć przez liczbę całkowitą. Czytelnik wyniesie błędne przekonanie i pomyli się przy późniejszym łączeniu tekstów. Popraw na: tekstu nie da się dzielić (ani odejmować); dodawanie tekstów ma inne znaczenie (łączenie) i omówimy je osobno. Usuń też „tylko” z definicji tekstu albo dodaj „łączy”. _← weryfikator_odwołań_
  - `wynik` (blokująca) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie**: Zdanie sugeruje, że tekstu nie da się dodawać ani mnożyć, a w Pythonie się da: "Ania" + "Kasia" skleja teksty, a "Ha" * 3 daje "HaHaHa". Trzeba zawęzić twierdzenie do dzielenia albo do liczenia na wartościach, np. „Liczbę można dzielić. Tekstu nie: "Ania" / 2 kończy się błędem TypeError”. Ta sama nieścisłość jest w zdaniu „program tylko przechowuje, wypisuje i porównuje”, bo tekst można też sklejać. Sugerowana poprawka: dopisać „i skleja”, albo pominąć dodawanie. _← sprawdzacz_wyników_
- Wynik: „Liczba a tekst”: 172 słów prozy, ```python 4 linii, ```text 2 linii; warsztat: kasa.py, $ python kasa.py (błąd)
- [prompt i odpowiedź](_przebieg/0381-pisarz.md) · 21.5 s · $0.0915

### 0382 · kontrola_deterministyczna · dział 04 · pytanie 22 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0383 · weryfikator_pojęć · dział 04 · pytanie 22 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0383-weryfikator-pojec.md) · 6.0 s · $0.0227

### 0384 · znudzony_czytelnik · dział 04 · pytanie 22 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `fakt` (blokująca) **zdanie o działaniach na tekście**: Zdanie „Liczbę można dzielić, mnożyć i dodawać. Tekstu nie” jest nieprawdziwe. W Pythonie "Ania" + "Kowalska" skleja teksty, a "Ha" * 3 daje "HaHaHa". Czytelnik wyniesie błędne przekonanie, a potem się zdziwi. Trzeba zawęzić do dzielenia, które tabela już pokazuje: „Tekstu nie da się dzielić”. Można też dodać, że plus skleja teksty zamiast liczyć. _← znudzony_czytelnik_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0384-znudzony-czytelnik.md) · 4.4 s · $0.0195

### 0385 · strażnik_przykład · dział 04 · pytanie 22 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a plik programu w kanonie nazywa się `rozlicz.py` (wspolna_kasa/rozlicz.py). Zamień `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0385-straznik-przyklad.md) · 5.4 s · $0.0218

### 0386 · strażnik_warsztat · dział 04 · pytanie 22 · próba 2

- Wynik: 1 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **zdanie o `kwota = 45.5`**: Tekst mówi, że w „Wspólnej Kasie” jest `kwota = 45.5`, a w kasa.py czytelnik ma `kwota_wydatku = 45.5`. Popraw na: „tak jak `kwota_wydatku = 45.5` w „Wspólnej Kasie”” albo napisz, że poniższy przykład używa krótszej nazwy `kwota`. _← strażnik_warsztat_
  - `wynik` (sugestia) **krok 2, ścieżka w tracebacku**: W tracebacku jest ścieżka /home/ania/wspolna_kasa/kasa.py. U czytelnika będzie ona inna (jego katalog domowy, na Windows np. C:\Users\...\wspolna_kasa\kasa.py). Dodaj zdanie, że ścieżka w pierwszej linii `File ...` będzie u niego inna, a liczy się `line 7` i ostatnia linia z TypeError. _← strażnik_warsztat_
  - `spójność` (sugestia) **TypeError**: Nazwa `TypeError` pojawia się bez wyjaśnienia. Dodaj krótko, że to „błąd typu”: Python informuje, że działanie nie pasuje do rodzaju wartości. Sam typ jest omówiony w następnej sekcji. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0386-straznik-warsztat.md) · 15.1 s · $0.0300

### 0387 · weryfikator_odwołań · dział 04 · pytanie 22 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie**: Zdanie „Liczbę można dzielić, mnożyć i dodawać. Tekstu nie” oraz „tekst… program tylko przechowuje, wypisuje i porównuje” jest nieprawdziwe: teksty można dodawać (łączyć), np. "Ala" + "Ola", a nawet mnożyć przez liczbę całkowitą. Czytelnik wyniesie błędne przekonanie i pomyli się przy późniejszym łączeniu tekstów. Popraw na: tekstu nie da się dzielić (ani odejmować); dodawanie tekstów ma inne znaczenie (łączenie) i omówimy je osobno. Usuń też „tylko” z definicji tekstu albo dodaj „łączy”. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 5)
- [prompt i odpowiedź](_przebieg/0387-weryfikator-odwolan.md) · 10.2 s · $0.0410

### 0388 · sprawdzacz_wyników · dział 04 · pytanie 22 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wynik` (blokująca) **Liczbę można dzielić, mnożyć i dodawać. Tekstu nie**: Zdanie sugeruje, że tekstu nie da się dodawać ani mnożyć, a w Pythonie się da: "Ania" + "Kasia" skleja teksty, a "Ha" * 3 daje "HaHaHa". Trzeba zawęzić twierdzenie do dzielenia albo do liczenia na wartościach, np. „Liczbę można dzielić. Tekstu nie: "Ania" / 2 kończy się błędem TypeError”. Ta sama nieścisłość jest w zdaniu „program tylko przechowuje, wypisuje i porównuje”, bo tekst można też sklejać. Sugerowana poprawka: dopisać „i skleja”, albo pominąć dodawanie. _← sprawdzacz_wyników_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0388-sprawdzacz-wynikow.md) · 4.6 s · $0.0167

### 0389 · weryfikator_faktów · dział 04 · pytanie 22 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0389-weryfikator-faktow.md) · 13.4 s · $0.0675

### 0390 · decyzja · dział 04 · pytanie 22 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **zdanie o `kwota = 45.5`**: Tekst mówi, że w „Wspólnej Kasie” jest `kwota = 45.5`, a w kasa.py czytelnik ma `kwota_wydatku = 45.5`. Popraw na: „tak jak `kwota_wydatku = 45.5` w „Wspólnej Kasie”” albo napisz, że poniższy przykład używa krótszej nazwy `kwota`. _← strażnik_warsztat_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0391 · akceptacja · dział 04 · pytanie 22

- Wynik: Sekcja [sec-04-liczba-a-tekst] dopisana do działu 04; odwołania: wstecz „imię „Ania” nie do podzielenia przez 2”, w przód „U siebie zobaczysz to za chwilę”, w przód „Tym zajmiemy się osobno.”, w przód „omówimy w następnej sekcji”, wstecz „tak jak `kwota = 45.5` w „Wspólnej Kasie””; punkty zaczepienia: cztery znaki zamiast kwoty; w TODO zostało 39.
- 0.0 s

### 0392 · łowca_pułapek · dział 04 · pytanie 22

- Wynik: „Liczba a tekst”: brak pułapek
- [prompt i odpowiedź](_przebieg/0392-lowca-pulapek.md) · 2.3 s · $0.0128

### 0393 · autor_dodatków · dział 04 · pytanie 22

- Wynik: „Liczba a tekst”: wtręty: Marta bierze kwotę w cudzysłów
- [prompt i odpowiedź](_przebieg/0393-autor-dodatkow.md) · 9.8 s · $0.0560

### 0394 · weryfikator_dodatków · dział 04 · pytanie 22

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0394-weryfikator-dodatkow.md) · 6.9 s · $0.0482

### 0395 · pisarz · dział 04 · pytanie 23 · próba 1

- Kolejka TODO (38): 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35 …
- Wynik: „Czym jest typ danych”: 185 słów prozy, ```python 6 linii, ```text 3 linii; nowe hasła: typ danych; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0395-pisarz.md) · 20.9 s · $0.0832

### 0396 · kontrola_deterministyczna · dział 04 · pytanie 23 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0397 · weryfikator_pojęć · dział 04 · pytanie 23 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0397-weryfikator-pojec.md) · 4.6 s · $0.0219

### 0398 · znudzony_czytelnik · dział 04 · pytanie 23 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0398-znudzony-czytelnik.md) · 5.7 s · $0.0190

### 0399 · strażnik_przykład · dział 04 · pytanie 23 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Typ decyduje o tym, co program może zrobić z wartością**: Teza, że typ decyduje o dozwolonych działaniach (imienia nie podzielisz przez 2, kwotę tak), jest podana tylko słowami. Warto dodać krótki blok, np. `print(kwota / 2)` i `print(imie / 2)` z komunikatem TypeError, oznaczony pierwszą linią „# poza kanonem” dla błędnej linii. Tekst jest zrozumiały bez tego, więc to tylko sugestia. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0399-straznik-przyklad.md) · 6.6 s · $0.0227

### 0400 · strażnik_warsztat · dział 04 · pytanie 23 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **zdanie „Typ decyduje o tym…”**: Teza „typ decyduje o tym, co program może zrobić z wartością” ma tylko zdanie o dzieleniu imienia przez 2. Dobrze byłoby dodać krótki kod, np. print(kwota / 2) z wynikiem 22.75 oraz odwołanie do wcześniejszego błędu przy nazwa_wyjazdu / 2. Nic tu nie jest błędne, to tylko sugestia. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0400-straznik-warsztat.md) · 8.5 s · $0.0222

### 0401 · weryfikator_odwołań · dział 04 · pytanie 23 · próba 1

- Wynik: Brak uwag. (odwołania: 4)
- [prompt i odpowiedź](_przebieg/0401-weryfikator-odwolan.md) · 8.8 s · $0.0385

### 0402 · sprawdzacz_wyników · dział 04 · pytanie 23 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wynik` (sugestia) **imienia nie podzielisz przez 2**: Teza „imienia nie podzielisz przez 2, a kwotę tak” jest podana bez kodu. Można dodać krótki przykład, np. `print(45.5 / 2)` z wynikiem 22.75 oraz `"Ania" / 2` z błędem TypeError. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **rozpoznawanie typu po zapisie**: Zdanie „Python rozpoznaje go po zapisie” pomija `int`, np. cyfry bez kropki to liczba całkowita. Tabela to uzupełnia, ale warto dodać to zdanie w tekście. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0402-sprawdzacz-wynikow.md) · 5.0 s · $0.0155

### 0403 · weryfikator_faktów · dział 04 · pytanie 23 · próba 1

- Wynik: Brak uwag. (źródła: 2)
- [prompt i odpowiedź](_przebieg/0403-weryfikator-faktow.md) · 15.0 s · $0.0637

### 0404 · decyzja · dział 04 · pytanie 23 · próba 1

- Wynik: Sekcja przyjęta; 4 sugestii trafia do raportu.
- 0.0 s

### 0405 · akceptacja · dział 04 · pytanie 23

- Wynik: Sekcja [sec-04-czym-jest-typ-danych] dopisana do działu 04; hasła w glosariuszu: typ danych; odwołania: wstecz „Wcześniej pisaliśmy po prostu „rodzaj danych””, wstecz „tylko cztery znaki: 4, 5, kropka, 5”, wstecz „imienia nie podzielisz przez 2”, w przód „Typem `bool` zajmiemy się osobno, w kolejnej sekcji”; punkty zaczepienia: type() pokazuje typ, tabela typów Pythona; w TODO zostało 38.
- 0.0 s

### 0406 · łowca_pułapek · dział 04 · pytanie 23

- Wynik: „Czym jest typ danych”: brak pułapek
- [prompt i odpowiedź](_przebieg/0406-lowca-pulapek.md) · 2.1 s · $0.0133

### 0407 · autor_dodatków · dział 04 · pytanie 23

- Wynik: „Czym jest typ danych”: dygresje: Rakieta, która pomyliła typy liczb
- [prompt i odpowiedź](_przebieg/0407-autor-dodatkow.md) · 15.0 s · $0.0629

### 0408 · weryfikator_dodatków · dział 04 · pytanie 23

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0408-weryfikator-dodatkow.md) · 11.6 s · $0.1097

### 0409 · pisarz · dział 04 · pytanie 24 · próba 1

- Kolejka TODO (37): 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36 …
- Wynik: „Wartość logiczna prawda/fałsz”: 127 słów prozy, ```python 5 linii, ```text 3 linii; nowe hasła: wartość logiczna; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0409-pisarz.md) · 22.5 s · $0.0867

### 0410 · kontrola_deterministyczna · dział 04 · pytanie 24 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0411 · weryfikator_pojęć · dział 04 · pytanie 24 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **po drugim przypisaniu**: wystarczy jedno zdanie; pełne omówienie w pytaniu 25. Tekst używa słowa „przypisanie” bez wyjaśnienia. Wystarczy dopisać, że to zapisanie wartości do zmiennej znakiem =. Kod pokazuje to pośrednio, więc to tylko sugestia. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0411-weryfikator-pojec.md) · 7.9 s · $0.0245

### 0412 · znudzony_czytelnik · dział 04 · pytanie 24 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `skrócenie` (sugestia) **akapit o wielkiej literze i cudzysłowie**: Sekcja w dużej mierze powtarza poprzednią (bool, True/False, cudzysłów vs tekst, ten sam kod z type). Można skrócić akapit o cudzysłowie lub odwołać się do niego jednym zdaniem. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0412-znudzony-czytelnik.md) · 4.2 s · $0.0176

### 0413 · strażnik_przykład · dział 04 · pytanie 24 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0413-straznik-przyklad.md) · 4.3 s · $0.0192

### 0414 · strażnik_warsztat · dział 04 · pytanie 24 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0414-straznik-warsztat.md) · 5.4 s · $0.0182

### 0415 · weryfikator_odwołań · dział 04 · pytanie 24 · próba 1

- Wynik: Brak uwag. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0415-weryfikator-odwolan.md) · 8.5 s · $0.0373

### 0416 · sprawdzacz_wyników · dział 04 · pytanie 24 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0416-sprawdzacz-wynikow.md) · 3.7 s · $0.0128

### 0417 · weryfikator_faktów · dział 04 · pytanie 24 · próba 1

- Wynik: Brak uwag. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0417-weryfikator-faktow.md) · 13.7 s · $0.0837

### 0418 · decyzja · dział 04 · pytanie 24 · próba 1

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 0419 · akceptacja · dział 04 · pytanie 24

- Wynik: Sekcja [sec-04-wartosc-logiczna-prawda-falsz] dopisana do działu 04; hasła w glosariuszu: wartość logiczna; odwołania: wstecz „Ta sama zasada, co przy `"45.5"`”, wstecz „Zmienną logiczną podmieniasz jak każdą inną: po drugim przypisaniu `True` znika”, w przód „Jak to zapisać, pokażemy przy instrukcji warunkowej”; punkty zaczepienia: pole wyboru, True w cudzysłowie; w TODO zostało 37.
- 0.0 s

### 0420 · łowca_pułapek · dział 04 · pytanie 24

- Wynik: „Wartość logiczna prawda/fałsz”: brak pułapek
- [prompt i odpowiedź](_przebieg/0420-lowca-pulapek.md) · 2.6 s · $0.0149

### 0421 · autor_dodatków · dział 04 · pytanie 24

- Wynik: „Wartość logiczna prawda/fałsz”: dowcipy: Odpowiedź „no, prawie”
- [prompt i odpowiedź](_przebieg/0421-autor-dodatkow.md) · 6.8 s · $0.0544

### 0422 · weryfikator_dodatków · dział 04 · pytanie 24

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0422-weryfikator-dodatkow.md) · 2.5 s · $0.0451

### 0423 · pisarz · dział 04 · pytanie 25 · próba 1

- Kolejka TODO (36): 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37 …
- Wynik: „Przypisanie wartości do zmiennej”: 142 słów prozy, ```python 5 linii, ```text 2 linii; nowe hasła: przypisanie; wątki: przykład dodaj kwota_stara; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0423-pisarz.md) · 21.5 s · $0.0865

### 0424 · kontrola_deterministyczna · dział 04 · pytanie 25 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **sec-04-zmienna-jako-pudelko-z-etykieta**: Oznaczenie [[sec-04-zmienna-jako-pudelko-z-etykieta]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 0425 · weryfikator_pojęć · dział 04 · pytanie 25 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0425-weryfikator-pojec.md) · 2.8 s · $0.0196

### 0426 · znudzony_czytelnik · dział 04 · pytanie 25 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **pierwszy akapit**: Pytanie brzmi „do czego służy”, a odpowiedź to jedno ogólne zdanie („program zapamiętuje daną i może do niej wrócić”). Brakuje krótkiego, życiowego powodu, np. jedna liczba użyta w wielu miejscach (kwota użyta do podatku i sumy) i zmieniana w jednym miejscu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0426-znudzony-czytelnik.md) · 4.7 s · $0.0173

### 0427 · strażnik_przykład · dział 04 · pytanie 25 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **kwota**: Kod używa `kwota = 45.5` zgodnie z kanonem, a `kwota_stara = kwota` jest zadeklarowane przez autora. `kwota = 60` zmienia wartość z liczby zmiennoprzecinkowej na całkowitą, co nadal jest liczbą, więc nie łamie kanonu. Dla spójności z 45.5 można wpisać `60.0`, ale nie trzeba. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0427-straznik-przyklad.md) · 7.0 s · $0.0224

### 0428 · strażnik_warsztat · dział 04 · pytanie 25 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **akapit „Przypisanie działa od prawej do lewej”**: Zdanie „Python kopiuje jej aktualną wartość” jest uproszczeniem. Python w rzeczywistości wiąże drugą nazwę z tym samym obiektem. Dla liczb, tekstów i wartości logicznych, czyli w tej sekcji, nie ma to widocznej różnicy. Można dodać zastrzeżenie, np. „(dla liczb i tekstów działa to jak kopia)”, żeby czytelnik nie przeniósł tego przekonania na listy w późniejszych działach. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0428-straznik-warsztat.md) · 8.1 s · $0.0218

### 0429 · weryfikator_odwołań · dział 04 · pytanie 25 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **przypisanie**: Hasło „przypisanie” nie ma wpisu w glosariuszu, ale sekcja definiuje je na miejscu (pierwsze zdanie), więc nie blokuje. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0429-weryfikator-odwolan.md) · 5.2 s · $0.0348

### 0430 · sprawdzacz_wyników · dział 04 · pytanie 25 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0430-sprawdzacz-wynikow.md) · 4.8 s · $0.0145

### 0431 · weryfikator_faktów · dział 04 · pytanie 25 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 0)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Python kopiuje jej aktualną wartość**: Oficjalna dokumentacja Pythona (https://docs.python.org/3/reference/simple_stmts.html#assignment-statements) opisuje przypisanie jako wiązanie nazwy z obiektem, a nie kopiowanie wartości. Dla liczb (float, int) skutek jest taki, jak opisano w sekcji, więc kod i wynik (60 i 45.5) są poprawne. Nieścisłość ujawni się dopiero przy listach, gdzie zmiana przez jedną nazwę jest widoczna przez drugą. Można dopisać "dla liczb i tekstów" albo zostawić i wyjaśnić przy listach. Nie opieram tego na zapytaniu do dokumentacji w tej sesji, tylko na znajomości semantyki języka. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0431-weryfikator-faktow.md) · 9.3 s · $0.0315

### 0432 · decyzja · dział 04 · pytanie 25 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **sec-04-zmienna-jako-pudelko-z-etykieta**: Oznaczenie [[sec-04-zmienna-jako-pudelko-z-etykieta]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 5 sugestii trafia do raportu.
- 0.0 s

### 0433 · pisarz · dział 04 · pytanie 25 · próba 2

- Kolejka TODO (36): 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37 …
- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **sec-04-zmienna-jako-pudelko-z-etykieta**: Oznaczenie [[sec-04-zmienna-jako-pudelko-z-etykieta]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- Wynik: „Przypisanie wartości do zmiennej”: 142 słów prozy, ```python 5 linii, ```text 2 linii; nowe hasła: przypisanie; wątki: przykład dodaj kwota_stara
- [prompt i odpowiedź](_przebieg/0433-pisarz.md) · 13.8 s · $0.0822

### 0434 · kontrola_deterministyczna · dział 04 · pytanie 25 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0435 · weryfikator_pojęć · dział 04 · pytanie 25 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0435-weryfikator-pojec.md) · 2.7 s · $0.0194

### 0436 · znudzony_czytelnik · dział 04 · pytanie 25 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0436-znudzony-czytelnik.md) · 4.4 s · $0.0170

### 0437 · strażnik_przykład · dział 04 · pytanie 25 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **kwota**: W przykładzie `kwota = 60` zmienia 45.5 (liczba z ułamkiem) na całkowitą 60. Nie przeczy to kanonowi (nadal liczba), ale dla spójności kwoty pieniężnej lepiej użyć np. `kwota = 60.0`. Wtedy wynik to `60.0`, a nie `60`. _← strażnik_przykład_
  - `spójność` (sugestia) **kopiowanie wartości**: Zdanie „Python kopiuje jej aktualną wartość” jest prawdziwe dla liczb i tekstów. Dla list, np. kanonicznej `osoby`, przypisanie kopiuje tylko odwołanie. Warto dodać jedno zdanie w rodzaju „dotyczy liczb i tekstów, o listach później” albo odesłać do późniejszego działu, żeby nie utrwalać błędnego uogólnienia. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0437-straznik-przyklad.md) · 10.0 s · $0.0253

### 0438 · weryfikator_odwołań · dział 04 · pytanie 25 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/0438-weryfikator-odwolan.md) · 7.4 s · $0.0367

### 0439 · sprawdzacz_wyników · dział 04 · pytanie 25 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0439-sprawdzacz-wynikow.md) · 4.0 s · $0.0135

### 0440 · weryfikator_faktów · dział 04 · pytanie 25 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Python kopiuje jej aktualną wartość**: Dokumentacja Pythona (Data model / Assignment statements, https://docs.python.org/3/reference/simple_stmts.html#assignment-statements) mówi, że przypisanie wiąże nazwę z obiektem, a nie kopiuje wartości. Dla liczb (float, int) efekt w przykładzie jest identyczny, więc kod i wynik (60 oraz 45.5) są poprawne. Jeśli tutorial później wprowadzi listy, warto wtedy doprecyzować. Tu wystarczy zostawić lub dodać „(dla liczb i tekstów działa to jak kopia)”. Nie sprawdzałem tego w Context7 ani przez WebFetch, opieram się na znanej semantyce języka. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0440-weryfikator-faktow.md) · 10.5 s · $0.0325

### 0441 · decyzja · dział 04 · pytanie 25 · próba 2

- Wynik: Sekcja przyjęta; 3 sugestii trafia do raportu.
- 0.0 s

### 0442 · akceptacja · dział 04 · pytanie 25

- Wynik: Sekcja [sec-04-przypisanie-wartosci-do-zmiennej] dopisana do działu 04; hasła w glosariuszu: przypisanie; kanony: przykład:+kwota_stara; odwołania: wstecz „tak jak przy pudełku z etykietą”, poza tutorialem „To nie jest równanie ze szkoły”; punkty zaczepienia: zmiana kwoty i kopia; w TODO zostało 36.
- 0.0 s

### 0443 · łowca_pułapek · dział 04 · pytanie 25

- Wynik: „Przypisanie wartości do zmiennej”: brak pułapek
- [prompt i odpowiedź](_przebieg/0443-lowca-pulapek.md) · 2.4 s · $0.0150

### 0444 · autor_dodatków · dział 04 · pytanie 25

- Wynik: „Przypisanie wartości do zmiennej”: dykteryjki: Cena brutto, która nie nadążała
- [prompt i odpowiedź](_przebieg/0444-autor-dodatkow.md) · 13.6 s · $0.0622

### 0445 · weryfikator_dodatków · dział 04 · pytanie 25

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0445-weryfikator-dodatkow.md) · 5.8 s · $0.0502

### 0446 · autor_wstępu · dział 05 · próba 1

- Kolejka TODO (36): 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37 …
- Wynik: Wstęp: 86 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0446-autor-wstepu.md) · 5.6 s · $0.0247

### 0447 · recenzent_wstępu · dział 05 · próba 1

- Wynik: 2 blokujących, 3 sugestii.
- Nowe potrzeby (5):
  - `diagram` (blokująca) **diagram: „> ?” pod „porównanie” i „if / else” pod „decyzja”**: Diagram używa skrótów, których czytelnik jeszcze nie zna: „if / else” (angielskie słowa, w tekście wstępu w ogóle nie padają) i „> ?”. Zastąp je opisami po polsku, spójnymi z pytaniami działu, np. „jeśli… to… / w przeciwnym razie”, a porównanie zapisz zrozumiale, np. „czy kwota jest większa niż…?”. Ukośnik w „kwota / osoby” może się kojarzyć z „albo”; lepiej użyć „kwota ÷ osoby” lub „kwota podzielona na osoby”. _← recenzent_wstępu_
  - `diagram` (blokująca) **diagram: układ etykiet pod strzałkami**: Przykładowe wartości („kwota, osoby”, „kwota / osoby”, „> ?”, „if / else”) są ustawione w drugiej linii bez jasnego przypisania do etapów; w terminalu spacje łatwo się rozjadą i nie widać, która etykieta należy do którego pola. Narysuj pionowo albo w pudełkach, tak by każdy przykład był bezpośrednio pod swoim etapem. Dodaj też, co wynika z porównania (dwie ścieżki: tak/nie), bo dziś „decyzja” wisi bez wyniku. _← recenzent_wstępu_
  - `konkret` (sugestia) **„zdecyduje, czy ktoś jest winien pieniądze, czy ma dostać zwrot”**: Przykład „Wspólna Kasa” pojawia się bez zarysu sytuacji (kto komu płaci). Jedno krótkie zdanie o tym, czym jest ta kasa (np. wspólny wyjazd, wydatki dzielone na osoby), pomoże czytelnikowi wyobrazić sobie scenariusz. Uwaga: „zwrot” i „jest winien” to dwa wyniki, a w diagramie jest jedno porównanie „>” – upewnij się, że zgadza się to z przykładem. _← recenzent_wstępu_
  - `wyjaśnienie` (sugestia) **„rozgałęzienia ze schematów blokowych z działu 2”**: Wstęp nie mówi, jak to nawiązanie się przyda (np. „decyzja w programie to ten sam romb ze schematu, tylko zapisany kodem”). Jedno takie zdanie wzmocni związek z poprzednimi działami. _← recenzent_wstępu_
  - `tempo` (sugestia) **ostatnie zdanie („w warsztacie oceni, czy wydatek jest duży”)**: Zdanie jest długie, a pojęcie „warsztat” nie zostało wprowadzone; zapis „oceni, czy wydatek jest duży” nie mówi, względem czego. Rozważ skrócenie lub doprecyzowanie („w warsztacie sam napiszesz program sprawdzający, czy wydatek przekracza ustalony próg”). _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0447-recenzent-wstepu.md) · 14.2 s · $0.0244

### 0448 · decyzja · dział 05 · próba 1

- Wynik: Wstęp wraca do autora.
- Nowe potrzeby (2):
  - `diagram` (blokująca) **diagram: „> ?” pod „porównanie” i „if / else” pod „decyzja”**: Diagram używa skrótów, których czytelnik jeszcze nie zna: „if / else” (angielskie słowa, w tekście wstępu w ogóle nie padają) i „> ?”. Zastąp je opisami po polsku, spójnymi z pytaniami działu, np. „jeśli… to… / w przeciwnym razie”, a porównanie zapisz zrozumiale, np. „czy kwota jest większa niż…?”. Ukośnik w „kwota / osoby” może się kojarzyć z „albo”; lepiej użyć „kwota ÷ osoby” lub „kwota podzielona na osoby”. _← recenzent_wstępu_
  - `diagram` (blokująca) **diagram: układ etykiet pod strzałkami**: Przykładowe wartości („kwota, osoby”, „kwota / osoby”, „> ?”, „if / else”) są ustawione w drugiej linii bez jasnego przypisania do etapów; w terminalu spacje łatwo się rozjadą i nie widać, która etykieta należy do którego pola. Narysuj pionowo albo w pudełkach, tak by każdy przykład był bezpośrednio pod swoim etapem. Dodaj też, co wynika z porównania (dwie ścieżki: tak/nie), bo dziś „decyzja” wisi bez wyniku. _← recenzent_wstępu_
- 0.0 s

### 0449 · autor_wstępu · dział 05 · próba 2

- Kolejka TODO (36): 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37 …
- Potrzeby w kolejce przed krokiem (2):
  - `diagram` (blokująca) **diagram: „> ?” pod „porównanie” i „if / else” pod „decyzja”**: Diagram używa skrótów, których czytelnik jeszcze nie zna: „if / else” (angielskie słowa, w tekście wstępu w ogóle nie padają) i „> ?”. Zastąp je opisami po polsku, spójnymi z pytaniami działu, np. „jeśli… to… / w przeciwnym razie”, a porównanie zapisz zrozumiale, np. „czy kwota jest większa niż…?”. Ukośnik w „kwota / osoby” może się kojarzyć z „albo”; lepiej użyć „kwota ÷ osoby” lub „kwota podzielona na osoby”. _← recenzent_wstępu_
  - `diagram` (blokująca) **diagram: układ etykiet pod strzałkami**: Przykładowe wartości („kwota, osoby”, „kwota / osoby”, „> ?”, „if / else”) są ustawione w drugiej linii bez jasnego przypisania do etapów; w terminalu spacje łatwo się rozjadą i nie widać, która etykieta należy do którego pola. Narysuj pionowo albo w pudełkach, tak by każdy przykład był bezpośrednio pod swoim etapem. Dodaj też, co wynika z porównania (dwie ścieżki: tak/nie), bo dziś „decyzja” wisi bez wyniku. _← recenzent_wstępu_
- Wynik: Wstęp: 86 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0449-autor-wstepu.md) · 4.7 s · $0.0292

### 0450 · recenzent_wstępu · dział 05 · próba 2

- Wynik: 0 blokujących, 0 sugestii.
- [prompt i odpowiedź](_przebieg/0450-recenzent-wstepu.md) · 2.3 s · $0.0170

### 0451 · pisarz · dział 05 · pytanie 26 · próba 1

- Kolejka TODO (35): 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38 …
- Wynik: „Działania matematyczne w programie”: 165 słów prozy, ```python 8 linii, ```text 7 linii; nowe hasła: operator arytmetyczny; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0451-pisarz.md) · 22.0 s · $0.0823

### 0452 · kontrola_deterministyczna · dział 05 · pytanie 26 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0453 · weryfikator_pojęć · dział 05 · pytanie 26 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0453-weryfikator-pojec.md) · 4.4 s · $0.0217

### 0454 · znudzony_czytelnik · dział 05 · pytanie 26 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **`//` i `%` – „bardzo przydatne”**: Zdanie o dzieleniu kwoty między osoby jest ogólne, a wyniki 33 i 1 nie są z nim połączone. Wystarczy jedno zdanie: 100 zł na 3 osoby to po 33 zł (`//`) i 1 zł zostaje (`%`). _← znudzony_czytelnik_
  - `przykład` (sugestia) **kolejność działań i nawiasy**: Kolejność działań jest tylko stwierdzona. Krótki przykład, np. `2 + 3 * 4` daje 14, a `(2 + 3) * 4` daje 20, pokazałby to od razu. Wystarczy jedna linia w bloku kodu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0454-znudzony-czytelnik.md) · 9.1 s · $0.0231

### 0455 · strażnik_przykład · dział 05 · pytanie 26 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **Konsekwencja: działania mają sens tylko na liczbach**: Twierdzenie jest nieprawdziwe w tej ogólności. W Pythonie `+` skleja teksty (`"Ania" + "Bartek"`), a `*` powtarza tekst (`"Ania" * 2`). Ten dział właśnie uczy sklejania tekstu podsumowania, więc czytelnik wyniósłby błędne przekonanie. Popraw np.: „Dzielenia, odejmowania i potęgowania nie da się zastosować do tekstu (`"Ania" / 3` to błąd). `+` i `*` działają na tekście inaczej niż na liczbach: sklejają i powtarzają.” _← strażnik_przykład_
  - `spójność` (sugestia) **kwota**: Kanon deklaruje `kwota = 45.5` (liczba zmiennoprzecinkowa), a przykład nadaje `kwota = 100` (int). Typ „liczba” się zgadza, więc to nie sprzeczność. Zaznacz jednak w tekście, że to nowa wartość, np. „załóżmy, że wydatek wyniósł 100 zł”, i najlepiej wiąż przykład z wątkiem: dzielenie 100 zł na 3 osoby (`osoby` z kanonu). _← strażnik_przykład_
  - `spójność` (sugestia) **wątek Wspólna Kasa**: Sekcja prawie nie korzysta z wątku. Wspomina tylko dzielenie kwoty między osoby, ale bez kodu. Dodaj krótki przykład, w którym `//` i `%` liczą, ile pełnych złotych przypada na osobę i ile zostaje, np. `kwota // len(osoby)` i `kwota % len(osoby)`. Wszystko na nazwach z kanonu, więc canon_changes nie jest potrzebne. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0455-straznik-przyklad.md) · 14.9 s · $0.0310

### 0456 · strażnik_warsztat · dział 05 · pytanie 26 · próba 1

- Wynik: 2 blokujących, 1 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **Ostatnie zdania sekcji („działania mają sens tylko na liczbach…”)**: Błąd merytoryczny: w Pythonie `+` i `*` działają też na tekstach (`"Ania" + "Kowalska"` daje `AniaKowalska`, `"Ha" * 3` daje `HaHaHa`). Poprawka: zamień zdanie na np. „Operatory `-`, `/`, `//`, `%`, `**` mają sens tylko na liczbach. Tekstu w rodzaju `"Ania"` nie podzielisz (`"Ania" / 2` kończy się błędem `TypeError`), a `+` i `*` na tekście działają inaczej niż na liczbach”. Dodaj krótki przykład kodu z tą tezą. _← strażnik_warsztat_
  - `spójność` (blokująca) **Odwołanie „co widzieliśmy przy typach danych”**: W stanie czytelnika (kasa.py) nigdzie nie dzielono tekstu; czytelnik widział tylko `type(...)` zwracające `<class 'str'>`. Zdanie odwołuje się do czegoś, czego nie było. Usuń „co widzieliśmy przy typach danych” albo zastąp je zdaniem: „Wiemy już, że `nazwa_wyjazdu` jest tekstem (`str`), więc `nazwa_wyjazdu / 2` się nie uda”. _← strażnik_warsztat_
  - `spójność` (sugestia) **Zdanie o dzieleniu `/`**: „zawsze daje liczbę z częścią ułamkową” bywa mylące: `100 / 4` daje `25.0`, `kwota_wydatku * 2` w kasa.py daje `91.0`. Lepiej: „Dzielenie `/` zawsze daje liczbę ułamkową (typ `float`), np. `100 / 4` to `25.0`”. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0456-straznik-warsztat.md) · 14.9 s · $0.0304

### 0457 · weryfikator_odwołań · dział 05 · pytanie 26 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 1)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **kolejność działań**: Zdanie o kolejności działań i nawiasach nie ma przykładu. Wystarczy jedna linia, np. print(2 + 3 * 4) daje 14, a print((2 + 3) * 4) daje 20. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **dzielenie kwoty między osoby**: Zdanie „Przy dzieleniu kwoty między osoby to bardzo przydatne” jest ogólnikowe. Można je powiązać z wynikiem: 100 zł na 3 osoby to 33 zł dla każdego (//) i 1 zł reszty (%). _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0457-weryfikator-odwolan.md) · 9.8 s · $0.0351

### 0458 · sprawdzacz_wyników · dział 05 · pytanie 26 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wynik` (sugestia) **Kolejność działań**: Kolejność działań (mnożenie przed dodawaniem, nawiasy) jest opisana tylko słowami. Krótki przykład, np. print(2 + 3 * 4) daje 14, a print((2 + 3) * 4) daje 20, pomógłby czytelnikowi. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **Konsekwencja: działania tylko na liczbach**: Zdanie, że tekstu typu "Ania" nie da się podzielić, nie ma przykładu. Można dodać print("Ania" / 2) i pokazać, że kończy się błędem. Przy okazji warto zaznaczyć, że to odwołanie do wcześniejszej sekcji o typach danych. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0458-sprawdzacz-wynikow.md) · 6.9 s · $0.0178

### 0459 · weryfikator_faktów · dział 05 · pytanie 26 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (źródła: 1)
- Nowe potrzeby (2):
  - `fakt` (sugestia) **Dzielenie `/` zawsze daje liczbę z częścią ułamkową.**: Dokumentacja: dzielenie liczb całkowitych daje float (np. 10 / 2 to 5.0). Wynik jest więc zawsze typu float, ale nie zawsze ma niezerową część ułamkową. Lepiej: „Dzielenie / zawsze daje liczbę zmiennoprzecinkową, np. 6 / 3 to 2.0”. Źródło: https://docs.python.org/3.13/reference/expressions.html _← weryfikator_faktów_
  - `fakt` (sugestia) **`//` zostawia samą część całkowitą**: Dokumentacja: `//` to dzielenie z zaokrągleniem w dół (floor), np. -10 // 3 daje -4, a nie -3. Dla liczb dodatnich w przykładzie opis jest poprawny. Jeśli kiedyś pojawią się liczby ujemne, mów „zaokrągla w dół”. Źródło: https://docs.python.org/3.13/reference/expressions.html _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0459-weryfikator-faktow.md) · 22.9 s · $0.0855

### 0460 · decyzja · dział 05 · pytanie 26 · próba 1

- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (blokująca) **Konsekwencja: działania mają sens tylko na liczbach**: Twierdzenie jest nieprawdziwe w tej ogólności. W Pythonie `+` skleja teksty (`"Ania" + "Bartek"`), a `*` powtarza tekst (`"Ania" * 2`). Ten dział właśnie uczy sklejania tekstu podsumowania, więc czytelnik wyniósłby błędne przekonanie. Popraw np.: „Dzielenia, odejmowania i potęgowania nie da się zastosować do tekstu (`"Ania" / 3` to błąd). `+` i `*` działają na tekście inaczej niż na liczbach: sklejają i powtarzają.” _← strażnik_przykład_
  - `spójność` (blokująca) **Ostatnie zdania sekcji („działania mają sens tylko na liczbach…”)**: Błąd merytoryczny: w Pythonie `+` i `*` działają też na tekstach (`"Ania" + "Kowalska"` daje `AniaKowalska`, `"Ha" * 3` daje `HaHaHa`). Poprawka: zamień zdanie na np. „Operatory `-`, `/`, `//`, `%`, `**` mają sens tylko na liczbach. Tekstu w rodzaju `"Ania"` nie podzielisz (`"Ania" / 2` kończy się błędem `TypeError`), a `+` i `*` na tekście działają inaczej niż na liczbach”. Dodaj krótki przykład kodu z tą tezą. _← strażnik_warsztat_
  - `spójność` (blokująca) **Odwołanie „co widzieliśmy przy typach danych”**: W stanie czytelnika (kasa.py) nigdzie nie dzielono tekstu; czytelnik widział tylko `type(...)` zwracające `<class 'str'>`. Zdanie odwołuje się do czegoś, czego nie było. Usuń „co widzieliśmy przy typach danych” albo zastąp je zdaniem: „Wiemy już, że `nazwa_wyjazdu` jest tekstem (`str`), więc `nazwa_wyjazdu / 2` się nie uda”. _← strażnik_warsztat_
- Wynik: Do poprawy: 3 blokujących potrzeb wraca do pisarza; 11 sugestii trafia do raportu.
- 0.0 s

### 0461 · pisarz · dział 05 · pytanie 26 · próba 2

- Kolejka TODO (35): 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38 …
- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (blokująca) **Konsekwencja: działania mają sens tylko na liczbach**: Twierdzenie jest nieprawdziwe w tej ogólności. W Pythonie `+` skleja teksty (`"Ania" + "Bartek"`), a `*` powtarza tekst (`"Ania" * 2`). Ten dział właśnie uczy sklejania tekstu podsumowania, więc czytelnik wyniósłby błędne przekonanie. Popraw np.: „Dzielenia, odejmowania i potęgowania nie da się zastosować do tekstu (`"Ania" / 3` to błąd). `+` i `*` działają na tekście inaczej niż na liczbach: sklejają i powtarzają.” _← strażnik_przykład_
  - `spójność` (blokująca) **Ostatnie zdania sekcji („działania mają sens tylko na liczbach…”)**: Błąd merytoryczny: w Pythonie `+` i `*` działają też na tekstach (`"Ania" + "Kowalska"` daje `AniaKowalska`, `"Ha" * 3` daje `HaHaHa`). Poprawka: zamień zdanie na np. „Operatory `-`, `/`, `//`, `%`, `**` mają sens tylko na liczbach. Tekstu w rodzaju `"Ania"` nie podzielisz (`"Ania" / 2` kończy się błędem `TypeError`), a `+` i `*` na tekście działają inaczej niż na liczbach”. Dodaj krótki przykład kodu z tą tezą. _← strażnik_warsztat_
  - `spójność` (blokująca) **Odwołanie „co widzieliśmy przy typach danych”**: W stanie czytelnika (kasa.py) nigdzie nie dzielono tekstu; czytelnik widział tylko `type(...)` zwracające `<class 'str'>`. Zdanie odwołuje się do czegoś, czego nie było. Usuń „co widzieliśmy przy typach danych” albo zastąp je zdaniem: „Wiemy już, że `nazwa_wyjazdu` jest tekstem (`str`), więc `nazwa_wyjazdu / 2` się nie uda”. _← strażnik_warsztat_
- Wynik: „Działania matematyczne w programie”: 166 słów prozy, ```python 4 linii, ```text 3 linii, ```python 2 linii, ```text 2 linii; nowe hasła: operator arytmetyczny; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0461-pisarz.md) · 20.5 s · $0.0898

### 0462 · kontrola_deterministyczna · dział 05 · pytanie 26 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0463 · weryfikator_pojęć · dział 05 · pytanie 26 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **TypeError**: wystarczy jedno zdanie; pełne omówienie w pytaniu 51. Np. że TypeError to nazwa błędu, który Python zgłasza, gdy działanie nie pasuje do typu wartości (tu: dzielenie tekstu). _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0463-weryfikator-pojec.md) · 7.4 s · $0.0250

### 0464 · znudzony_czytelnik · dział 05 · pytanie 26 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **potęgowanie i kolejność działań**: Potęgowanie `**` i nawiasy zmieniające kolejność działań są tylko wymienione, bez żadnego wyniku. Wystarczą dwie linie w pierwszym bloku, np. `print(2 ** 3)` i `print((2 + 3) * 4)`, z wynikami 8 i 20. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0464-znudzony-czytelnik.md) · 7.1 s · $0.0207

### 0465 · strażnik_przykład · dział 05 · pytanie 26 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **Konsekwencja: działania mają sens tylko na liczbach**: Twierdzenie jest nieprawdziwe w tej ogólności. W Pythonie `+` skleja teksty (`"Ania" + "Bartek"`), a `*` powtarza tekst (`"Ania" * 2`). Ten dział właśnie uczy sklejania tekstu podsumowania, więc czytelnik wyniósłby błędne przekonanie. Popraw np.: „Dzielenia, odejmowania i potęgowania nie da się zastosować do tekstu (`"Ania" / 3` to błąd). `+` i `*` działają na tekście inaczej niż na liczbach: sklejają i powtarzają.” _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0465-straznik-przyklad.md) · 5.5 s · $0.0238

### 0466 · strażnik_warsztat · dział 05 · pytanie 26 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (blokująca) **Ostatnie zdania sekcji („działania mają sens tylko na liczbach…”)**: Błąd merytoryczny: w Pythonie `+` i `*` działają też na tekstach (`"Ania" + "Kowalska"` daje `AniaKowalska`, `"Ha" * 3` daje `HaHaHa`). Poprawka: zamień zdanie na np. „Operatory `-`, `/`, `//`, `%`, `**` mają sens tylko na liczbach. Tekstu w rodzaju `"Ania"` nie podzielisz (`"Ania" / 2` kończy się błędem `TypeError`), a `+` i `*` na tekście działają inaczej niż na liczbach”. Dodaj krótki przykład kodu z tą tezą. _← strażnik_warsztat_
  - `spójność` (blokująca) **Odwołanie „co widzieliśmy przy typach danych”**: W stanie czytelnika (kasa.py) nigdzie nie dzielono tekstu; czytelnik widział tylko `type(...)` zwracające `<class 'str'>`. Zdanie odwołuje się do czegoś, czego nie było. Usuń „co widzieliśmy przy typach danych” albo zastąp je zdaniem: „Wiemy już, że `nazwa_wyjazdu` jest tekstem (`str`), więc `nazwa_wyjazdu / 2` się nie uda”. _← strażnik_warsztat_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0466-straznik-warsztat.md) · 7.1 s · $0.0246

### 0467 · weryfikator_odwołań · dział 05 · pytanie 26 · próba 2

- Wynik: 2 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **[[operator-arytmetyczny|operatorów arytmetycznych]]**: Hasło „operator-arytmetyczny” nie istnieje w glosariuszu, więc link byłby martwy. Usuń znacznik [[...]] (definicja jest już w zdaniu: „znaków, które mówią Pythonowi, jakie działanie wykonać”) albo dodaj hasło do glosariusza. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **`nazwa_wyjazdu`**: Zmienna `nazwa_wyjazdu` pojawia się bez wprowadzenia, a żaden punkt zaczepienia jej nie definiuje. Wyjaśnij na miejscu, np. dodaj `nazwa_wyjazdu = "Mazury"` przed użyciem, albo zastąp przykładem z tekstem podanym wprost, np. `"Ania" / 2`. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **kolejność działań**: Dodaj krótki przykład, np. `print(2 + 3 * 4)` daje 14, a `print((2 + 3) * 4)` daje 20. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0467-weryfikator-odwolan.md) · 17.9 s · $0.0439

### 0468 · sprawdzacz_wyników · dział 05 · pytanie 26 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0468-sprawdzacz-wynikow.md) · 4.8 s · $0.0150

### 0469 · weryfikator_faktów · dział 05 · pytanie 26 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 2)
- Nowe potrzeby (2):
  - `fakt` (sugestia) **`//` zostawia samą część całkowitą**: Dokumentacja (https://docs.python.org/3.13/reference/expressions.html) opisuje `//` jako dzielenie z zaokrągleniem w dół (floor), a nie odcięcie części ułamkowej. Dla liczb dodatnich wynik jest ten sam, ale `-7 // 2` daje `-4`, nie `-3`. Dla początkującego opis jest wystarczający, więc można go zostawić. Jeśli chcesz go uściślić, napisz „zaokrągla w dół do liczby całkowitej”. _← weryfikator_faktów_
  - `fakt` (sugestia) **`/` zawsze daje liczbę z częścią ułamkową**: Dokumentacja (https://docs.python.org/3.13/reference/expressions.html) mówi, że dzielenie liczb całkowitych daje float. Nie musi to jednak być liczba z niezerową częścią ułamkową: `10 / 2` daje `5.0`. Dokładniejsze sformułowanie: „zawsze daje liczbę zapisaną z ułamkiem (np. `5.0`)”. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0469-weryfikator-faktow.md) · 21.9 s · $0.1024

### 0470 · decyzja · dział 05 · pytanie 26 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **[[operator-arytmetyczny|operatorów arytmetycznych]]**: Hasło „operator-arytmetyczny” nie istnieje w glosariuszu, więc link byłby martwy. Usuń znacznik [[...]] (definicja jest już w zdaniu: „znaków, które mówią Pythonowi, jakie działanie wykonać”) albo dodaj hasło do glosariusza. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **`nazwa_wyjazdu`**: Zmienna `nazwa_wyjazdu` pojawia się bez wprowadzenia, a żaden punkt zaczepienia jej nie definiuje. Wyjaśnij na miejscu, np. dodaj `nazwa_wyjazdu = "Mazury"` przed użyciem, albo zastąp przykładem z tekstem podanym wprost, np. `"Ania" / 2`. _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 2 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0471 · akceptacja · dział 05 · pytanie 26

- Wynik: Sekcja [sec-05-dzialania-matematyczne-w-programie] dopisana do działu 05; hasła w glosariuszu: operator arytmetyczny; odwołania: wstecz „Skoro `nazwa_wyjazdu` jest tekstem”; punkty zaczepienia: nieścisłość ułamka; w TODO zostało 35.
- 0.0 s

### 0472 · łowca_pułapek · dział 05 · pytanie 26

- Wynik: „Działania matematyczne w programie”: brak pułapek
- [prompt i odpowiedź](_przebieg/0472-lowca-pulapek.md) · 3.8 s · $0.0169

### 0473 · autor_dodatków · dział 05 · pytanie 26

- Wynik: „Działania matematyczne w programie”: dowcipy: Reszta z dzielenia to ostatni kawałek pizzy
- [prompt i odpowiedź](_przebieg/0473-autor-dodatkow.md) · 11.4 s · $0.0636

### 0474 · weryfikator_dodatków · dział 05 · pytanie 26

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0474-weryfikator-dodatkow.md) · 8.5 s · $0.0551

### 0475 · pisarz · dział 05 · pytanie 27 · próba 1

- Kolejka TODO (34): 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39 …
- Wynik: „Łączenie tekstów”: 142 słów prozy, ```python 4 linii, ```text 2 linii; nowe hasła: konkatenacja; warsztat: kasa.py, $ python kasa.py (błąd), kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0475-pisarz.md) · 39.3 s · $0.1037

### 0476 · kontrola_deterministyczna · dział 05 · pytanie 27 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0477 · weryfikator_pojęć · dział 05 · pytanie 27 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **f"{imie} zapłaciła {kwota} zł"**: Zapis z literą f jest podany tylko w jednym wierszu, bez wyniku. Warto pokazać krótki blok kodu z wynikiem (np. „Ania zapłaciła 45.5 zł”), żeby było widać, że nie trzeba tu użyć str(). _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0477-weryfikator-pojec.md) · 7.5 s · $0.0241

### 0478 · znudzony_czytelnik · dział 05 · pytanie 27 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `skrócenie` (sugestia) **zdanie o obietnicy z poprzedniej sekcji**: Zdanie „Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono” nic nie wnosi. Poprzednia sekcja nie zawiera takiej obietnicy, więc zdanie może zmylić czytelnika. Warto je usunąć. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0478-znudzony-czytelnik.md) · 9.1 s · $0.0233

### 0479 · strażnik_przykład · dział 05 · pytanie 27 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a w kanonie plik programu (skrypt główny) nazywa się `rozlicz.py` (w katalogu wspolna_kasa). Nie ma zadeklarowanej zmiany nazwy. Popraw na `rozlicz.py`. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0479-straznik-przyklad.md) · 6.8 s · $0.0229

### 0480 · strażnik_warsztat · dział 05 · pytanie 27 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `wynik` (blokująca) **krok 2, traceback**: Podany wynik nie zgadza się znak w znak z tym, co wypisze Python 3.13. (1) Linia ze ścieżką: od Pythona 3.9 skrypt uruchomiony jako `python kasa.py` ma ścieżkę bezwzględną, więc czytelnik zobaczy `File "/…/wspolna_kasa/kasa.py", line 8, in <module>`, a nie `File "kasa.py"`. Podaj przykładową ścieżkę, np. `File "/home/ania/wspolna_kasa/kasa.py", line 8, in <module>`, i dopisz, że ścieżka u czytelnika będzie inna. (2) Podkreślenie pod wyrażeniem `"Kwota: " + kwota_wydatku` ma za dużo znaków `~`. Wyrażenie ma 25 znaków: 10 znaków przed `+` (`"Kwota: "` i spacja), `+` oraz 14 znaków po nim (spacja i `kwota_wydatku`). Poprawna linia: 10 spacji wcięcia, potem `~~~~~~~~~~^~~~~~~~~~~~~~~` (10 tyldek, `^`, 14 tyldek). _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0480-straznik-warsztat.md) · 20.9 s · $0.0375

### 0481 · weryfikator_odwołań · dział 05 · pytanie 27 · próba 1

- Wynik: 1 blokujących, 2 sugestii. (odwołania: 2)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **kasa.py**: Zdanie „U siebie zobaczysz ten błąd za chwilę w `kasa.py`” zapowiada plik i ćwiczenie, których czytelnik nie zna, a żaden punkt ani sekcja tego nie wprowadza. Usuń zdanie albo zastąp je tym, co czytelnik może zrobić od razu, np. „Wpisz `"Kwota: " + 45.5` w terminalu, a zobaczysz ten błąd”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **TypeError**: Błąd `TypeError` jest opisany, ale nie pokazano jego komunikatu. Dodaj krótki blok z przykładowym komunikatem, żeby czytelnik rozpoznał go u siebie. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **f-string**: Zapis z literą `f` nie ma pokazanego wyniku. Dodaj linię wyniku, np. `Ania zapłaciła 45.5 zł`, żeby było widać, że efekt jest ten sam. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0481-weryfikator-odwolan.md) · 16.7 s · $0.0439

### 0482 · sprawdzacz_wyników · dział 05 · pytanie 27 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0482-sprawdzacz-wynikow.md) · 4.5 s · $0.0144

### 0483 · weryfikator_faktów · dział 05 · pytanie 27 · próba 1

- Wynik: Brak uwag. (źródła: 2)
- [prompt i odpowiedź](_przebieg/0483-weryfikator-faktow.md) · 12.9 s · $0.0666

### 0484 · decyzja · dział 05 · pytanie 27 · próba 1

- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a w kanonie plik programu (skrypt główny) nazywa się `rozlicz.py` (w katalogu wspolna_kasa). Nie ma zadeklarowanej zmiany nazwy. Popraw na `rozlicz.py`. _← strażnik_przykład_
  - `wynik` (blokująca) **krok 2, traceback**: Podany wynik nie zgadza się znak w znak z tym, co wypisze Python 3.13. (1) Linia ze ścieżką: od Pythona 3.9 skrypt uruchomiony jako `python kasa.py` ma ścieżkę bezwzględną, więc czytelnik zobaczy `File "/…/wspolna_kasa/kasa.py", line 8, in <module>`, a nie `File "kasa.py"`. Podaj przykładową ścieżkę, np. `File "/home/ania/wspolna_kasa/kasa.py", line 8, in <module>`, i dopisz, że ścieżka u czytelnika będzie inna. (2) Podkreślenie pod wyrażeniem `"Kwota: " + kwota_wydatku` ma za dużo znaków `~`. Wyrażenie ma 25 znaków: 10 znaków przed `+` (`"Kwota: "` i spacja), `+` oraz 14 znaków po nim (spacja i `kwota_wydatku`). Poprawna linia: 10 spacji wcięcia, potem `~~~~~~~~~~^~~~~~~~~~~~~~~` (10 tyldek, `^`, 14 tyldek). _← strażnik_warsztat_
  - `odwołanie` (blokująca) **kasa.py**: Zdanie „U siebie zobaczysz ten błąd za chwilę w `kasa.py`” zapowiada plik i ćwiczenie, których czytelnik nie zna, a żaden punkt ani sekcja tego nie wprowadza. Usuń zdanie albo zastąp je tym, co czytelnik może zrobić od razu, np. „Wpisz `"Kwota: " + 45.5` w terminalu, a zobaczysz ten błąd”. _← weryfikator_odwołań_
- Wynik: Do poprawy: 3 blokujących potrzeb wraca do pisarza; 4 sugestii trafia do raportu.
- 0.0 s

### 0485 · pisarz · dział 05 · pytanie 27 · próba 2

- Kolejka TODO (34): 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39 …
- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a w kanonie plik programu (skrypt główny) nazywa się `rozlicz.py` (w katalogu wspolna_kasa). Nie ma zadeklarowanej zmiany nazwy. Popraw na `rozlicz.py`. _← strażnik_przykład_
  - `wynik` (blokująca) **krok 2, traceback**: Podany wynik nie zgadza się znak w znak z tym, co wypisze Python 3.13. (1) Linia ze ścieżką: od Pythona 3.9 skrypt uruchomiony jako `python kasa.py` ma ścieżkę bezwzględną, więc czytelnik zobaczy `File "/…/wspolna_kasa/kasa.py", line 8, in <module>`, a nie `File "kasa.py"`. Podaj przykładową ścieżkę, np. `File "/home/ania/wspolna_kasa/kasa.py", line 8, in <module>`, i dopisz, że ścieżka u czytelnika będzie inna. (2) Podkreślenie pod wyrażeniem `"Kwota: " + kwota_wydatku` ma za dużo znaków `~`. Wyrażenie ma 25 znaków: 10 znaków przed `+` (`"Kwota: "` i spacja), `+` oraz 14 znaków po nim (spacja i `kwota_wydatku`). Poprawna linia: 10 spacji wcięcia, potem `~~~~~~~~~~^~~~~~~~~~~~~~~` (10 tyldek, `^`, 14 tyldek). _← strażnik_warsztat_
  - `odwołanie` (blokująca) **kasa.py**: Zdanie „U siebie zobaczysz ten błąd za chwilę w `kasa.py`” zapowiada plik i ćwiczenie, których czytelnik nie zna, a żaden punkt ani sekcja tego nie wprowadza. Usuń zdanie albo zastąp je tym, co czytelnik może zrobić od razu, np. „Wpisz `"Kwota: " + 45.5` w terminalu, a zobaczysz ten błąd”. _← weryfikator_odwołań_
- Wynik: „Łączenie tekstów”: 152 słów prozy, ```python 4 linii, ```text 2 linii; nowe hasła: konkatenacja; warsztat: kasa.py, $ python kasa.py (błąd), kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0485-pisarz.md) · 32.5 s · $0.1078

### 0486 · kontrola_deterministyczna · dział 05 · pytanie 27 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0487 · weryfikator_pojęć · dział 05 · pytanie 27 · próba 2

- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 0. (eskalowano 1 powtarzających się braków do blokujących)
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **skryptu**: Słowo „skrypt” pojawia się w ostatnim zdaniu bez definicji i bez hasła w glosariuszu. Wystarczy dopisać „(krótki program w pliku)” albo zastąpić je słowem „program”. [Eskalacja: zgłaszane już w sekcji „Program a aplikacja”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0487-weryfikator-pojec.md) · 7.1 s · $0.0239

### 0488 · znudzony_czytelnik · dział 05 · pytanie 27 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `skrócenie` (sugestia) **Akapit otwierający**: Zdanie „Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno, więc oto ono” nic nie wnosi. Można je usunąć, a zaoszczędzone słowa przeznaczyć na jedno zdanie o tym, po co jest f-zapis (mniej `+` i spacji do pilnowania). _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0488-znudzony-czytelnik.md) · 7.7 s · $0.0217

### 0489 · strażnik_przykład · dział 05 · pytanie 27 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Tekst odsyła do pliku `kasa.py`, a w kanonie plik programu (skrypt główny) nazywa się `rozlicz.py` (w katalogu wspolna_kasa). Nie ma zadeklarowanej zmiany nazwy. Popraw na `rozlicz.py`. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0489-straznik-przyklad.md) · 5.3 s · $0.0227

### 0490 · strażnik_warsztat · dział 05 · pytanie 27 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wynik` (blokująca) **krok 2, traceback**: Podany wynik nie zgadza się znak w znak z tym, co wypisze Python 3.13. (1) Linia ze ścieżką: od Pythona 3.9 skrypt uruchomiony jako `python kasa.py` ma ścieżkę bezwzględną, więc czytelnik zobaczy `File "/…/wspolna_kasa/kasa.py", line 8, in <module>`, a nie `File "kasa.py"`. Podaj przykładową ścieżkę, np. `File "/home/ania/wspolna_kasa/kasa.py", line 8, in <module>`, i dopisz, że ścieżka u czytelnika będzie inna. (2) Podkreślenie pod wyrażeniem `"Kwota: " + kwota_wydatku` ma za dużo znaków `~`. Wyrażenie ma 25 znaków: 10 znaków przed `+` (`"Kwota: "` i spacja), `+` oraz 14 znaków po nim (spacja i `kwota_wydatku`). Poprawna linia: 10 spacji wcięcia, potem `~~~~~~~~~~^~~~~~~~~~~~~~~` (10 tyldek, `^`, 14 tyldek). _← strażnik_warsztat_
- Wynik: 3 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 2.
- Nowe potrzeby (3):
  - `wynik` (blokująca, niespełniona) **krok 2, traceback**: Podkreślenie nadal ma za dużo znaków ~. Wyrażenie `"Kwota: " + kwota_wydatku` ma 25 znaków, więc linia ma być: 10 spacji wcięcia, potem 10 tyldek, `^`, 14 tyldek: `          ~~~~~~~~~~^~~~~~~~~~~~~~`. Teraz po `^` stoi 15 tyldek. _← strażnik_warsztat_
  - `wynik` (blokująca) **krok 2, traceback**: Numer linii jest zły. Po dopisaniu nowa linia `print("Kwota: " + kwota_wydatku)` jest w kasa.py linią 16 (poprzednia, `print(kwota_wydatku % liczba_osob)`, to linia 15). Popraw na `File "/home/ania/wspolna_kasa/kasa.py", line 16, in <module>`. _← strażnik_warsztat_
  - `spójność` (blokująca, niespełniona) **krok 2, traceback**: Ścieżka jest już bezwzględna, ale nigdzie nie napisano, że u czytelnika będzie inna (inny użytkownik, na Windows np. C:\Users\...\wspolna_kasa\kasa.py). Dopisz jedno zdanie przy kroku 2. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0490-straznik-warsztat.md) · 20.9 s · $0.0423

### 0491 · weryfikator_odwołań · dział 05 · pytanie 27 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **kasa.py**: Zdanie „U siebie zobaczysz ten błąd za chwilę w `kasa.py`” zapowiada plik i ćwiczenie, których czytelnik nie zna, a żaden punkt ani sekcja tego nie wprowadza. Usuń zdanie albo zastąp je tym, co czytelnik może zrobić od razu, np. „Wpisz `"Kwota: " + 45.5` w terminalu, a zobaczysz ten błąd”. _← weryfikator_odwołań_
- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 1. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (blokująca, niespełniona) **kasa.py**: Poprawka nie została wprowadzona w istocie: zdanie o „kasa.py” zniknęło, ale zastąpiło je „w warsztacie poniżej dopisujesz do swojego skryptu linię…”. To nadal zapowiedź ćwiczenia i skryptu, których czytelnik nie zna, a żaden punkt ani sekcja ich nie wprowadza. Usuń zdanie albo zastąp je czymś do zrobienia od razu, np. „Wpisz w terminalu `"Kwota: " + 45.5`, a zobaczysz ten błąd.” _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0491-weryfikator-odwolan.md) · 11.0 s · $0.0393

### 0492 · sprawdzacz_wyników · dział 05 · pytanie 27 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0492-sprawdzacz-wynikow.md) · 4.8 s · $0.0145

### 0493 · weryfikator_faktów · dział 05 · pytanie 27 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 2)
- [prompt i odpowiedź](_przebieg/0493-weryfikator-faktow.md) · 14.4 s · $0.0670

### 0494 · decyzja · dział 05 · pytanie 27 · próba 2

- Potrzeby w kolejce przed krokiem (5):
  - `wyjaśnienie` (blokująca) **skryptu**: Słowo „skrypt” pojawia się w ostatnim zdaniu bez definicji i bez hasła w glosariuszu. Wystarczy dopisać „(krótki program w pliku)” albo zastąpić je słowem „program”. [Eskalacja: zgłaszane już w sekcji „Program a aplikacja”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
  - `wynik` (blokująca, niespełniona) **krok 2, traceback**: Podkreślenie nadal ma za dużo znaków ~. Wyrażenie `"Kwota: " + kwota_wydatku` ma 25 znaków, więc linia ma być: 10 spacji wcięcia, potem 10 tyldek, `^`, 14 tyldek: `          ~~~~~~~~~~^~~~~~~~~~~~~~`. Teraz po `^` stoi 15 tyldek. _← strażnik_warsztat_
  - `wynik` (blokująca) **krok 2, traceback**: Numer linii jest zły. Po dopisaniu nowa linia `print("Kwota: " + kwota_wydatku)` jest w kasa.py linią 16 (poprzednia, `print(kwota_wydatku % liczba_osob)`, to linia 15). Popraw na `File "/home/ania/wspolna_kasa/kasa.py", line 16, in <module>`. _← strażnik_warsztat_
  - `spójność` (blokująca, niespełniona) **krok 2, traceback**: Ścieżka jest już bezwzględna, ale nigdzie nie napisano, że u czytelnika będzie inna (inny użytkownik, na Windows np. C:\Users\...\wspolna_kasa\kasa.py). Dopisz jedno zdanie przy kroku 2. _← strażnik_warsztat_
  - `odwołanie` (blokująca, niespełniona) **kasa.py**: Poprawka nie została wprowadzona w istocie: zdanie o „kasa.py” zniknęło, ale zastąpiło je „w warsztacie poniżej dopisujesz do swojego skryptu linię…”. To nadal zapowiedź ćwiczenia i skryptu, których czytelnik nie zna, a żaden punkt ani sekcja ich nie wprowadza. Usuń zdanie albo zastąp je czymś do zrobienia od razu, np. „Wpisz w terminalu `"Kwota: " + 45.5`, a zobaczysz ten błąd.” _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 5 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0495 · akceptacja · dział 05 · pytanie 27

- Wynik: Sekcja [sec-05-laczenie-tekstow] dopisana do działu 05; hasła w glosariuszu: konkatenacja; odwołania: wstecz „Obiecaliśmy w poprzedniej sekcji, że zajmiemy się tym osobno”, w przód „w warsztacie poniżej dopisujesz do swojego skryptu linię”; punkty zaczepienia: zlepione słowa; w TODO zostało 34.
- 0.0 s

### 0496 · łowca_pułapek · dział 05 · pytanie 27

- Wynik: „Łączenie tekstów”: brak pułapek
- [prompt i odpowiedź](_przebieg/0496-lowca-pulapek.md) · 2.5 s · $0.0155

### 0497 · autor_dodatków · dział 05 · pytanie 27

- Wynik: „Łączenie tekstów”: wtręty: Marta skleja jak w arkuszu, dykteryjki: Zapytanie sklejone bez spacji
- [prompt i odpowiedź](_przebieg/0497-autor-dodatkow.md) · 16.1 s · $0.0682

### 0498 · weryfikator_dodatków · dział 05 · pytanie 27

- Wynik: odrzucone: 1; Zapytanie sklejone bez spacji: Dykteryjka pokazuje składanie zapytań SQL przez sklejanie tekstu i poleca do tego f-string, co jest złą praktyką (podatność na SQL injection), a czytelnik spoza IT mógłby ją przejąć.
- [prompt i odpowiedź](_przebieg/0498-weryfikator-dodatkow.md) · 10.8 s · $0.0591

### 0499 · pisarz · dział 05 · pytanie 28 · próba 1

- Kolejka TODO (33): 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40 …
- Wynik: „Porównywanie wartości”: 157 słów prozy, ```python 7 linii, ```text 6 linii; nowe hasła: operator porównania; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0499-pisarz.md) · 24.7 s · $0.0909

### 0500 · kontrola_deterministyczna · dział 05 · pytanie 28 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0501 · weryfikator_pojęć · dział 05 · pytanie 28 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0501-weryfikator-pojec.md) · 5.2 s · $0.0217

### 0502 · znudzony_czytelnik · dział 05 · pytanie 28 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **wartość logiczna**: Tekst zapowiada, że wynik jest wartością, ale nie pokazuje, że można ją zapisać w zmiennej, np. `czy_drogo = kwota > 50`. Jedna linia kodu pomogłaby zrozumieć, że True/False to zwykła wartość, a nie tylko wydruk. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0502-znudzony-czytelnik.md) · 4.2 s · $0.0181

### 0503 · strażnik_przykład · dział 05 · pytanie 28 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0503-straznik-przyklad.md) · 4.2 s · $0.0196

### 0504 · strażnik_warsztat · dział 05 · pytanie 28 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0504-straznik-warsztat.md) · 5.4 s · $0.0202

### 0505 · weryfikator_odwołań · dział 05 · pytanie 28 · próba 1

- Wynik: Brak uwag. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0505-weryfikator-odwolan.md) · 11.2 s · $0.0391

### 0506 · sprawdzacz_wyników · dział 05 · pytanie 28 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0506-sprawdzacz-wynikow.md) · 4.3 s · $0.0138

### 0507 · weryfikator_faktów · dział 05 · pytanie 28 · próba 1

- Wynik: Brak uwag. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0507-weryfikator-faktow.md) · 13.1 s · $0.0808

### 0508 · decyzja · dział 05 · pytanie 28 · próba 1

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 0509 · akceptacja · dział 05 · pytanie 28

- Wynik: Sekcja [sec-05-porownywanie-wartosci] dopisana do działu 05; hasła w glosariuszu: operator porównania; odwołania: wstecz „pojedynczy znak `=` to przypisanie”, wstecz „Tekst `"45.5"` i liczba 45.5 to różne typy”, w przód „instrukcja warunkowa, o której będzie następna sekcja”; punkty zaczepienia: tekst nie równa się liczbie; w TODO zostało 33.
- 0.0 s

### 0510 · łowca_pułapek · dział 05 · pytanie 28

- Wynik: „Porównywanie wartości”: brak pułapek
- [prompt i odpowiedź](_przebieg/0510-lowca-pulapek.md) · 2.3 s · $0.0153

### 0511 · autor_dodatków · dział 05 · pytanie 28

- Wynik: „Porównywanie wartości”: dykteryjki: Status zapisany małą literą
- [prompt i odpowiedź](_przebieg/0511-autor-dodatkow.md) · 12.6 s · $0.0668

### 0512 · weryfikator_dodatków · dział 05 · pytanie 28

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0512-weryfikator-dodatkow.md) · 6.4 s · $0.0562

### 0513 · pisarz · dział 05 · pytanie 29 · próba 1

- Kolejka TODO (32): 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41 …
- Wynik: „Instrukcja warunkowa „jeśli… to…””: 126 słów prozy, ```python 6 linii, ```text 2 linii; nowe hasła: instrukcja warunkowa, wcięcie; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0513-pisarz.md) · 23.8 s · $0.0917

### 0514 · kontrola_deterministyczna · dział 05 · pytanie 29 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **wydatek**: „wydatek” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
- 0.0 s

### 0515 · weryfikator_pojęć · dział 05 · pytanie 29 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0515-weryfikator-pojec.md) · 2.7 s · $0.0163

### 0516 · znudzony_czytelnik · dział 05 · pytanie 29 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `diagram` (sugestia) **przepływ warunku**: Można dodać krótki rysunek tekstowy przepływu: warunek -> True: wykonaj wcięte linie / False: pomiń. Ale sekcja jest zrozumiała także bez niego, a limit słów jest bliski. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0516-znudzony-czytelnik.md) · 4.1 s · $0.0172

### 0517 · strażnik_przykład · dział 05 · pytanie 29 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0517-straznik-przyklad.md) · 5.0 s · $0.0198

### 0518 · strażnik_warsztat · dział 05 · pytanie 29 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0518-straznik-warsztat.md) · 5.0 s · $0.0201

### 0519 · weryfikator_odwołań · dział 05 · pytanie 29 · próba 1

- Wynik: Brak uwag. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/0519-weryfikator-odwolan.md) · 7.5 s · $0.0343

### 0520 · sprawdzacz_wyników · dział 05 · pytanie 29 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0520-sprawdzacz-wynikow.md) · 5.0 s · $0.0147

### 0521 · weryfikator_faktów · dział 05 · pytanie 29 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 0)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Które linie należą do warunku, pokazuje wcięcie: przesunięcie linii o cztery spacje w prawo.**: Cztery spacje to konwencja (PEP 8), a nie wymóg języka. Python wymaga tylko, by wcięcie bloku było większe niż linii z `if` i spójne w całym bloku. Kod z sekcji działa poprawnie, a jego wynik jest zgodny z tym, co pokazano. Można to doprecyzować: „zwykle o cztery spacje”. Tego punktu nie sprawdzałem w dokumentacji, oceniam go z wiedzy o języku. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0521-weryfikator-faktow.md) · 8.2 s · $0.0306

### 0522 · decyzja · dział 05 · pytanie 29 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **wydatek**: „wydatek” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 2 sugestii trafia do raportu.
- 0.0 s

### 0523 · pisarz · dział 05 · pytanie 29 · próba 2

- Kolejka TODO (32): 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41 …
- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **wydatek**: „wydatek” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
- Wynik: „Instrukcja warunkowa „jeśli… to…””: 126 słów prozy, ```python 6 linii, ```text 2 linii; nowe hasła: instrukcja warunkowa, wcięcie; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0523-pisarz.md) · 20.4 s · $0.0949

### 0524 · kontrola_deterministyczna · dział 05 · pytanie 29 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0525 · weryfikator_pojęć · dział 05 · pytanie 29 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0525-weryfikator-pojec.md) · 2.8 s · $0.0194

### 0526 · znudzony_czytelnik · dział 05 · pytanie 29 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **wcięcie i dwukropek**: Sekcja mówi, że warunek to „zwykle porównanie”, ale nie wspomina, że po `if` można użyć dowolnej wartości logicznej ani co się stanie przy pominięciu dwukropka lub wcięcia. Można dodać jedno zdanie o typowym błędzie (brak dwukropka/wcięcia daje komunikat błędu), żeby początkujący nie wpadł w panikę. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0526-znudzony-czytelnik.md) · 4.8 s · $0.0179

### 0527 · strażnik_przykład · dział 05 · pytanie 29 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0527-straznik-przyklad.md) · 4.7 s · $0.0202

### 0528 · strażnik_warsztat · dział 05 · pytanie 29 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **przykład kodu w sekcji**: Przykład w tekście używa zmiennej `kwota`, a w kasa.py jest `kwota_wydatku`. Można użyć `kwota_wydatku` w przykładzie albo dodać zdanie, że to ten sam warunek zapisany krócej. Wynik jest taki sam. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0528-straznik-warsztat.md) · 6.8 s · $0.0219

### 0529 · weryfikator_odwołań · dział 05 · pytanie 29 · próba 2

- Wynik: 1 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **warunek**: Pojęcie „warunek” jest kluczowe dla sekcji, a nie ma hasła w glosariuszu. Tekst mówi tylko „zwykle porównanie”. Trzeba je zdefiniować na miejscu, np.: „Warunek to pytanie, na które odpowiedź brzmi True albo False, np. kwota > 40”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **wcięcie**: „Wcięcie” ma definicję w tekście (cztery spacje w prawo), ale brak hasła w glosariuszu. Wystarczy definicja w tekście, ale hasło „wcięcie” warto dodać. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **zależy od danych**: Sekcja pokazuje tylko przypadek, gdy warunek jest prawdziwy albo fałszywy w jednym programie. Brakuje przykładu, w którym zmiana danych (np. kwota = 20) zmienia wynik. Zdanie „to, co wykona, zależy od danych” jest bez pokazania. Dodaj krótki przykład albo zdanie z innym wynikiem. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0529-weryfikator-odwolan.md) · 7.3 s · $0.0351

### 0530 · sprawdzacz_wyników · dział 05 · pytanie 29 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0530-sprawdzacz-wynikow.md) · 3.5 s · $0.0129

### 0531 · weryfikator_faktów · dział 05 · pytanie 29 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Wcięcie: „przesunięcie linii o cztery spacje w prawo”**: Dokumentacja Pythona (https://docs.python.org/3.13/reference/compound_stmts.html) nie wymaga czterech spacji. Wymaga spójnego wcięcia w całym bloku, a cztery spacje to konwencja z PEP 8. Kod z sekcji działa poprawnie. Warto napisać np. „zwykle o cztery spacje (przyjęta konwencja); ważne, by w bloku było tak samo”. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0531-weryfikator-faktow.md) · 16.3 s · $0.0764

### 0532 · decyzja · dział 05 · pytanie 29 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **warunek**: Pojęcie „warunek” jest kluczowe dla sekcji, a nie ma hasła w glosariuszu. Tekst mówi tylko „zwykle porównanie”. Trzeba je zdefiniować na miejscu, np.: „Warunek to pytanie, na które odpowiedź brzmi True albo False, np. kwota > 40”. _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0533 · akceptacja · dział 05 · pytanie 29

- Wynik: Sekcja [sec-05-instrukcja-warunkowa-jesli-to] dopisana do działu 05; hasła w glosariuszu: instrukcja warunkowa, wcięcie; odwołania: wstecz „porównanie z poprzedniej sekcji”, w przód „pokażemy w następnej sekcji”; punkty zaczepienia: wcięcie i ostatni print; w TODO zostało 32.
- 0.0 s

### 0534 · łowca_pułapek · dział 05 · pytanie 29

- Wynik: „Instrukcja warunkowa „jeśli… to…””: brak pułapek
- [prompt i odpowiedź](_przebieg/0534-lowca-pulapek.md) · 2.3 s · $0.0127

### 0535 · autor_dodatków · dział 05 · pytanie 29

- Wynik: „Instrukcja warunkowa „jeśli… to…””: rysunki: Bramka, która przepuszcza tylko prawdę, wtręty: Marta wcina tylko jedną linię
- [prompt i odpowiedź](_przebieg/0535-autor-dodatkow.md) · 14.9 s · $0.0697

### 0536 · weryfikator_dodatków · dział 05 · pytanie 29

- Wynik: odrzucone: 1; Bramka, która przepuszcza tylko prawdę: Piesek jednocześnie niesie jedną piłkę boczną dróżką, a drugą główną ścieżką, co w jednej scenie jest fizycznie niespójne i mąci obraz: wcięta dróżka to wykonanie warunku, a nie jedna z dwóch tras.
- [prompt i odpowiedź](_przebieg/0536-weryfikator-dodatkow.md) · 11.4 s · $0.0634

### 0537 · pisarz · dział 05 · pytanie 30 · próba 1

- Kolejka TODO (31): 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42 …
- Wynik: „Część „w przeciwnym razie””: 151 słów prozy, ```python 6 linii, ```text 2 linii; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0537-pisarz.md) · 40.4 s · $0.1341

### 0538 · kontrola_deterministyczna · dział 05 · pytanie 30 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0539 · weryfikator_pojęć · dział 05 · pytanie 30 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0539-weryfikator-pojec.md) · 2.7 s · $0.0195

### 0540 · znudzony_czytelnik · dział 05 · pytanie 30 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0540-znudzony-czytelnik.md) · 2.6 s · $0.0135

### 0541 · strażnik_przykład · dział 05 · pytanie 30 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **kwota**: Kod używa `kwota = 45.5` zgodnie z kanonem, bez konfliktów. Drobna sugestia: dział dotyczy ustalenia, czy ktoś jest winien pieniądze, czy ma dostać zwrot. Przykład z „dużą/zwykłą kwotą” jest tylko luźno związany z wątkiem. Można w przyszłości pokazać `else` na rozróżnieniu „winien” / „dostaje zwrot”, np. na zmiennej salda. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0541-straznik-przyklad.md) · 6.7 s · $0.0226

### 0542 · strażnik_warsztat · dział 05 · pytanie 30 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0542-straznik-warsztat.md) · 5.0 s · $0.0205

### 0543 · weryfikator_odwołań · dział 05 · pytanie 30 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **Gdyby kwota wynosiła 150**: Można dodać krótki przykład z kwotą 150, pokazujący wynik drugiej ścieżki (obecnie tylko opisany słownie). _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0543-weryfikator-odwolan.md) · 4.9 s · $0.0327

### 0544 · sprawdzacz_wyników · dział 05 · pytanie 30 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0544-sprawdzacz-wynikow.md) · 3.8 s · $0.0131

### 0545 · weryfikator_faktów · dział 05 · pytanie 30 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0545-weryfikator-faktow.md) · 5.2 s · $0.0274

### 0546 · decyzja · dział 05 · pytanie 30 · próba 1

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 0547 · akceptacja · dział 05 · pytanie 30

- Wynik: Sekcja [sec-05-czesc-w-przeciwnym-razie] dopisana do działu 05; odwołania: wstecz „jak w poprzedniej sekcji, działa zawsze”, w przód „pokażemy w następnej sekcji”; punkty zaczepienia: dwie drogi if/else; w TODO zostało 31.
- 0.0 s

### 0548 · łowca_pułapek · dział 05 · pytanie 30

- Wynik: „Część „w przeciwnym razie””: brak pułapek
- [prompt i odpowiedź](_przebieg/0548-lowca-pulapek.md) · 2.3 s · $0.0129

### 0549 · autor_dodatków · dział 05 · pytanie 30

- Wynik: „Część „w przeciwnym razie””: dygresje: Skąd wzięło się „w przeciwnym razie”, rysunki: Rozwidlenie drogi bez trzeciej ścieżki
- [prompt i odpowiedź](_przebieg/0549-autor-dodatkow.md) · 12.3 s · $0.0702

### 0550 · weryfikator_dodatków · dział 05 · pytanie 30

- Wynik: odrzucone: 1; Skąd wzięło się „w przeciwnym razie”: Otwarte źródła (Wikipedia: Conditional i ALGOL 60) nie potwierdzają, że konstrukcja trafiła do języków w latach 50. i 60. ani że raport ALGOL 60 z 1960 roku zapisywał ją jako if…then…else.
- [prompt i odpowiedź](_przebieg/0550-weryfikator-dodatkow.md) · 17.1 s · $0.1669

### 0551 · pisarz · dział 05 · pytanie 31 · próba 1

- Kolejka TODO (30): 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43 …
- Wynik: „Operatory „i” oraz „lub””: 167 słów prozy, ```python 8 linii, ```text 3 linii; nowe hasła: operator logiczny; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0551-pisarz.md) · 25.8 s · $0.0976

### 0552 · kontrola_deterministyczna · dział 05 · pytanie 31 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **wydatek**: „wydatek” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
- 0.0 s

### 0553 · weryfikator_pojęć · dział 05 · pytanie 31 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0553-weryfikator-pojec.md) · 3.2 s · $0.0165

### 0554 · znudzony_czytelnik · dział 05 · pytanie 31 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **blok kodu z if ... or**: Pierwszy przykład kodu jest poprawny, ale przykład z `if` łączy dwa warunki, które oba są fałszywe, więc nie pokazuje, że `or` wystarczy jeden prawdziwy warunek w `if`. Można zmienić `liczba_osob > 5` na `liczba_osob == 3`, żeby wypisało się „Duży wydatek”. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0554-znudzony-czytelnik.md) · 5.2 s · $0.0181

### 0555 · strażnik_przykład · dział 05 · pytanie 31 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **liczba_osob**: Zmienna liczba_osob = 3 jest nowa i nie ma jej w kanonie ani w canon_changes. Zadeklaruj ją z module="przykład" jako „dodaj” (zmienna (liczba), wspolna_kasa/rozlicz.py, powód: liczba osób dzielących wydatek) albo użyj len(osoby), co pasuje do kanonicznej listy trzech osób. Wartość 3 zgadza się z kanonem. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0555-straznik-przyklad.md) · 8.6 s · $0.0247

### 0556 · strażnik_warsztat · dział 05 · pytanie 31 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0556-straznik-warsztat.md) · 8.9 s · $0.0249

### 0557 · weryfikator_odwołań · dział 05 · pytanie 31 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 1)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **Każdy z połączonych warunków zapisujemy w całości**: Można dodać krótki przykład typowego błędu, np. `kwota > 40 and < 100` zamiast `kwota > 40 and kwota < 100`, żeby zilustrować zdanie o zapisywaniu każdego warunku w całości. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0557-weryfikator-odwolan.md) · 9.2 s · $0.0380

### 0558 · sprawdzacz_wyników · dział 05 · pytanie 31 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0558-sprawdzacz-wynikow.md) · 4.6 s · $0.0142

### 0559 · weryfikator_faktów · dział 05 · pytanie 31 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 1)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Dzięki nim program sprawdza kilka rzeczy naraz i dostaje jedną odpowiedź: True albo False. / and daje True tylko wtedy... or daje True...**: Dokumentacja Pythona 3.13 (https://docs.python.org/3.13/reference/expressions.html, sekcja Boolean operations) mówi, że and i or nie ograniczają zwracanej wartości do True/False, lecz zwracają ostatnio obliczony operand (np. `s or 'foo'`). Dla warunków będących porównaniami, jak w tej sekcji, wynik jest faktycznie True/False, więc kod i wyniki są poprawne. Można dodać zastrzeżenie, np. „gdy łączymy porównania, wynik to True albo False”, żeby czytelnik nie uogólnił tego później na inne wartości. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0559-weryfikator-faktow.md) · 18.1 s · $0.0798

### 0560 · decyzja · dział 05 · pytanie 31 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **wydatek**: „wydatek” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 4 sugestii trafia do raportu.
- 0.0 s

### 0561 · pisarz · dział 05 · pytanie 31 · próba 2

- Kolejka TODO (30): 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43 …
- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **wydatek**: „wydatek” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („wydatki”), ale ma inną nazwę. Użyj „wydatki” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
- Wynik: „Operatory „i” oraz „lub””: 177 słów prozy, ```python 8 linii, ```text 3 linii; nowe hasła: operator logiczny; wątki: przykład dodaj liczba_osob; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0561-pisarz.md) · 24.1 s · $0.1024

### 0562 · kontrola_deterministyczna · dział 05 · pytanie 31 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0563 · weryfikator_pojęć · dział 05 · pytanie 31 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0563-weryfikator-pojec.md) · 2.9 s · $0.0197

### 0564 · znudzony_czytelnik · dział 05 · pytanie 31 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **przykład kodu**: Przykład w kodzie ma mało życiowy sens: progi 40 i 5 osób są losowe. Warto jednym zdaniem wskazać, co oznacza każdy warunek w kasie (np. „wysoka kwota lub dużo osób”), albo dać codzienne porównanie („i” = bilet ORAZ dokument). _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0564-znudzony-czytelnik.md) · 4.5 s · $0.0182

### 0565 · strażnik_przykład · dział 05 · pytanie 31 · próba 2

- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **kasa.py**: Tekst każe dopisać kod w `kasa.py`, a w kanonie plik programu to `rozlicz.py` (wspolna_kasa/rozlicz.py). Nazwa pliku nie została zadeklarowana jako zmiana. Zamień `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0565-straznik-przyklad.md) · 6.6 s · $0.0235

### 0566 · strażnik_warsztat · dział 05 · pytanie 31 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Przykład w tekście sekcji**: Przykład w tekście używa zmiennej `kwota`, a w kasa.py jest `kwota_wydatku`. Można dodać zdanie, że w kasa.py nazwa jest dłuższa (kwota_wydatku), żeby czytelnik nie przepisał `kwota` do pliku. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0566-straznik-warsztat.md) · 8.7 s · $0.0257

### 0567 · weryfikator_odwołań · dział 05 · pytanie 31 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- [prompt i odpowiedź](_przebieg/0567-weryfikator-odwolan.md) · 10.6 s · $0.0389

### 0568 · sprawdzacz_wyników · dział 05 · pytanie 31 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0568-sprawdzacz-wynikow.md) · 4.2 s · $0.0144

### 0569 · weryfikator_faktów · dział 05 · pytanie 31 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0569-weryfikator-faktow.md) · 5.3 s · $0.0278

### 0570 · decyzja · dział 05 · pytanie 31 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Tekst każe dopisać kod w `kasa.py`, a w kanonie plik programu to `rozlicz.py` (wspolna_kasa/rozlicz.py). Nazwa pliku nie została zadeklarowana jako zmiana. Zamień `kasa.py` na `rozlicz.py`. _← strażnik_przykład_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0571 · akceptacja · dział 05 · pytanie 31

- Wynik: Sekcja [sec-05-operatory-i-oraz-lub] dopisana do działu 05; hasła w glosariuszu: operator logiczny; kanony: przykład:+liczba_osob; odwołania: wstecz „tak jak w porównywaniu wartości”; punkty zaczepienia: kwota duża lub dzielona przez wielu; w TODO zostało 30.
- 0.0 s

### 0572 · łowca_pułapek · dział 05 · pytanie 31

- Wynik: „Operatory „i” oraz „lub””: brak pułapek
- [prompt i odpowiedź](_przebieg/0572-lowca-pulapek.md) · 2.4 s · $0.0156

### 0573 · autor_dodatków · dział 05 · pytanie 31

- Wynik: „Operatory „i” oraz „lub””: dygresje: Skąd „i” oraz „lub” w logice
- [prompt i odpowiedź](_przebieg/0573-autor-dodatkow.md) · 12.7 s · $0.0721

### 0574 · weryfikator_dodatków · dział 05 · pytanie 31

- Wynik: odrzucone: 1; Skąd „i” oraz „lub” w logice: Błąd w liczbach: Boole zmarł w 1864 r., a praca Shannona z 1937 r. powstała 73 lata później (ponad siedem dekad), nie „niemal cztery dekady”.
- [prompt i odpowiedź](_przebieg/0574-weryfikator-dodatkow.md) · 14.7 s · $0.1753

### 0575 · autor_wstępu · dział 06 · próba 1

- Kolejka TODO (30): 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43 …
- Wynik: Wstęp: 85 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0575-autor-wstepu.md) · 5.9 s · $0.0278

### 0576 · recenzent_wstępu · dział 06 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `diagram` (blokująca) **diagram**: Diagram jest niejasny dla laika: nie widać, że pętla wykonuje się wielokrotnie (jeden przebieg na każdy wydatek), a wynik 125 pojawia się dopiero po wszystkich krokach. Strzałka '--> 125' przy jednej linii sugeruje, że wynik daje pojedyncze wykonanie. Zmienna 'suma' nie ma wartości początkowej (0). Przerysuj: pokaż start suma = 0, kolejne przebiegi (40 -> suma 40, 25 -> suma 65, 60 -> suma 125) i strzałkę powrotną z 'suma = suma + wydatek' do 'for każdy wydatek', albo diagram usuń. _← recenzent_wstępu_
  - `wyjaśnienie` (sugestia) **diagram i jego związek ze wstępem**: Diagram używa zapisów (`for`, nawiasy kwadratowe, 'suma = suma + wydatek') bez wyjaśnienia; czytelnik nie wie, że '=' to przypisanie, a nie równość. Wstęp nie zapowiada, że diagram to ilustracja sumowania. Dodaj jedno zdanie wprowadzające pod diagramem lub podpis, np. 'Pętla bierze po kolei każdy wydatek z listy i dodaje go do sumy'. _← recenzent_wstępu_
  - `konkret` (sugestia) **„Wspólnej Kasie”**: 'Wspólna Kasa' pojawia się bez wprowadzenia; jeśli to projekt przewijający się przez tutorial, wystarczy krótkie dopowiedzenie (np. 'nasza aplikacja do rozliczania wydatków'), by czytelnik nie zastanawiał się, co to. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0576-recenzent-wstepu.md) · 8.4 s · $0.0199

### 0577 · decyzja · dział 06 · próba 1

- Wynik: Wstęp wraca do autora.
- Nowe potrzeby (1):
  - `diagram` (blokująca) **diagram**: Diagram jest niejasny dla laika: nie widać, że pętla wykonuje się wielokrotnie (jeden przebieg na każdy wydatek), a wynik 125 pojawia się dopiero po wszystkich krokach. Strzałka '--> 125' przy jednej linii sugeruje, że wynik daje pojedyncze wykonanie. Zmienna 'suma' nie ma wartości początkowej (0). Przerysuj: pokaż start suma = 0, kolejne przebiegi (40 -> suma 40, 25 -> suma 65, 60 -> suma 125) i strzałkę powrotną z 'suma = suma + wydatek' do 'for każdy wydatek', albo diagram usuń. _← recenzent_wstępu_
- 0.0 s

### 0578 · autor_wstępu · dział 06 · próba 2

- Kolejka TODO (30): 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43 …
- Potrzeby w kolejce przed krokiem (1):
  - `diagram` (blokująca) **diagram**: Diagram jest niejasny dla laika: nie widać, że pętla wykonuje się wielokrotnie (jeden przebieg na każdy wydatek), a wynik 125 pojawia się dopiero po wszystkich krokach. Strzałka '--> 125' przy jednej linii sugeruje, że wynik daje pojedyncze wykonanie. Zmienna 'suma' nie ma wartości początkowej (0). Przerysuj: pokaż start suma = 0, kolejne przebiegi (40 -> suma 40, 25 -> suma 65, 60 -> suma 125) i strzałkę powrotną z 'suma = suma + wydatek' do 'for każdy wydatek', albo diagram usuń. _← recenzent_wstępu_
- Wynik: Wstęp: 86 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0578-autor-wstepu.md) · 5.7 s · $0.0317

### 0579 · recenzent_wstępu · dział 06 · próba 2

- Wynik: 0 blokujących, 0 sugestii.
- [prompt i odpowiedź](_przebieg/0579-recenzent-wstepu.md) · 2.4 s · $0.0160

### 0580 · pisarz · dział 06 · pytanie 32 · próba 1

- Kolejka TODO (29): 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44 …
- Wynik: „Czym jest pętla”: 157 słów prozy, ```python 4 linii, ```text 4 linii; nowe hasła: pętla, iteracja; wątki: przykład dodaj imie; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0580-pisarz.md) · 28.2 s · $0.0965

### 0581 · kontrola_deterministyczna · dział 06 · pytanie 32 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0582 · weryfikator_pojęć · dział 06 · pytanie 32 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0582-weryfikator-pojec.md) · 5.2 s · $0.0217

### 0583 · znudzony_czytelnik · dział 06 · pytanie 32 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0583-znudzony-czytelnik.md) · 5.8 s · $0.0191

### 0584 · strażnik_przykład · dział 06 · pytanie 32 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **imie**: Kanon ma już `imie` jako zmienną (tekst) `imie = "Ania"`. Zmiana zadeklarowana jako „dodaj” powinna być „zmień”: `imie` jest teraz zmienną pętli `for imie in osoby:`, która w każdej iteracji dostaje kolejną wartość tekstową. Typ (tekst) się zgadza, więc to tylko sprawa poprawnej etykiety i uzasadnienia w canon_changes. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0584-straznik-przyklad.md) · 8.8 s · $0.0246

### 0585 · strażnik_warsztat · dział 06 · pytanie 32 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0585-straznik-warsztat.md) · 11.8 s · $0.0295

### 0586 · weryfikator_odwołań · dział 06 · pytanie 32 · próba 1

- Wynik: Brak uwag. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0586-weryfikator-odwolan.md) · 12.6 s · $0.0363

### 0587 · sprawdzacz_wyników · dział 06 · pytanie 32 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **pierwsze zdanie sekcji**: Sformułowanie „ile razy albo dla czego ją powtórzyć” jest niejasne (czytelnik może odczytać je jako „dlaczego”). Lepiej: „ile razy albo dla jakich danych ją powtórzyć”. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0587-sprawdzacz-wynikow.md) · 6.7 s · $0.0163

### 0588 · weryfikator_faktów · dział 06 · pytanie 32 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0588-weryfikator-faktow.md) · 5.8 s · $0.0278

### 0589 · decyzja · dział 06 · pytanie 32 · próba 1

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 0590 · akceptacja · dział 06 · pytanie 32

- Wynik: Sekcja [sec-06-czym-jest-petla] dopisana do działu 06; hasła w glosariuszu: pętla, iteracja; kanony: przykład:~imie; odwołania: w przód „jej zapis omówimy osobno”, wstecz „tak samo jak przy `if`”, wstecz „Ostatni `print` nie ma wcięcia”; punkty zaczepienia: pętla po osobach; w TODO zostało 29.
- 0.0 s

### 0591 · łowca_pułapek · dział 06 · pytanie 32

- Wynik: „Czym jest pętla”: brak pułapek
- [prompt i odpowiedź](_przebieg/0591-lowca-pulapek.md) · 2.3 s · $0.0130

### 0592 · autor_dodatków · dział 06 · pytanie 32

- Wynik: „Czym jest pętla”: wtręty: Marta kopiuje linię dla każdej osoby, dykteryjki: Pięć skopiowanych linii zamiast pętli
- [prompt i odpowiedź](_przebieg/0592-autor-dodatkow.md) · 12.6 s · $0.0703

### 0593 · weryfikator_dodatków · dział 06 · pytanie 32

- Wynik: odrzucone: 1; Pięć skopiowanych linii zamiast pętli: Powtarza motyw wcześniejszego wpisu „Marta wpisuje kwotę w pięciu miejscach” (ta sama rzecz skopiowana w pięciu miejscach, w jednym zostaje stara wartość) oraz motyw nieaktualnej kopii z wpisów o komentarzu i cenie brutto.
- [prompt i odpowiedź](_przebieg/0593-weryfikator-dodatkow.md) · 12.5 s · $0.0670

### 0594 · pisarz · dział 06 · pytanie 33 · próba 1

- Kolejka TODO (28): 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45 …
- Wynik: „Kiedy sięgnąć po pętlę”: 147 słów prozy, ```python 4 linii, ```text 3 linii
- [prompt i odpowiedź](_przebieg/0594-pisarz.md) · 25.3 s · $0.1060

### 0595 · kontrola_deterministyczna · dział 06 · pytanie 33 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0596 · weryfikator_pojęć · dział 06 · pytanie 33 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **for**: wystarczy jedno zdanie; pełne omówienie w pytaniu 37. Przy kodzie warto napisać, że linia `for imie in osoby:` znaczy „dla każdego imienia z zestawu osoby wykonaj wcięte poniżej linie, za każdym razem podstawiając kolejne imię pod nazwę imie”. Bez tego czytelnik musi się domyślać, co robi `for` i `in`. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0596-weryfikator-pojec.md) · 11.3 s · $0.0265

### 0597 · znudzony_czytelnik · dział 06 · pytanie 33 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **przykład z liczba_osob = 3**: Tekst twierdzi, że pętla dopasowuje się do danych i obsłuży czwartą osobę. W przykładzie liczba_osob = 3 jest wpisana ręcznie, więc po dodaniu czwartej osoby wynik byłby błędny (300/3). Warto to zauważyć w jednym zdaniu, np. że tę liczbę też trzeba by zmienić, a jak liczyć elementy listy, pokażemy później. Albo dać przykład, w którym liczba osób nie jest potrzebna. _← znudzony_czytelnik_
  - `przykład` (sugestia) **Poprawka wzoru to jedna zmiana zamiast trzech**: Zdanie o poprawce wzoru w jednym miejscu zamiast trzech odwołuje się do wersji bez pętli, której czytelnik nie widzi. Wystarczą trzy linie print z powtórzonym wzorem, żeby zobaczyć, co pętla oszczędza. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0597-znudzony-czytelnik.md) · 10.4 s · $0.0234

### 0598 · strażnik_przykład · dział 06 · pytanie 33 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **powtarzanie ręczne**: Sekcja twierdzi, że kopiowanie linii ze zmianą jednej wartości to sygnał do pętli, ale nie pokazuje wersji ręcznej. Warto dodać krótki blok „poza kanonem” z trzema prawie identycznymi wywołaniami print (Ania, Bartek, Celina) tuż przed wersją z pętlą. Kontrast byłby wtedy widoczny. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0598-straznik-przyklad.md) · 7.4 s · $0.0228

### 0599 · weryfikator_odwołań · dział 06 · pytanie 33 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **Powtarzanie ręczne ma dwie wady**: Wady ręcznego powtarzania (poprawka w wielu miejscach, kod na trzy osoby nie obsłuży czwartej) są tylko opisane. Warto pokazać krótką wersję z trzema skopiowanymi liniami print, żeby czytelnik zobaczył, co zastępuje pętla. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **osoby = ["Ania", "Bartek", "Celina"]**: W przykładzie pojawia się lista w nawiasach kwadratowych, a sekcja mówi o „zestawie danych”. Jedno zdanie, że to lista imion, ułatwiłoby zrozumienie. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0599-weryfikator-odwolan.md) · 12.4 s · $0.0366

### 0600 · sprawdzacz_wyników · dział 06 · pytanie 33 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **Powtarzanie ręczne / przykład z pętlą**: Sygnał 'kopiujesz linię i zmieniasz jedną wartość' nie ma pokazanego kodu. Warto dać wersję ręczną (trzy razy print z inną nazwą) przed pętlą, żeby czytelnik zobaczył kontrast. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0600-sprawdzacz-wynikow.md) · 7.2 s · $0.0163

### 0601 · weryfikator_faktów · dział 06 · pytanie 33 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 0)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Pętla `for` ma z góry znany koniec.**: Dla list i zakresów (range) to prawda, ale dokumentacja Pythona (https://docs.python.org/3/reference/compound_stmts.html#the-for-statement) mówi, że `for` iteruje po dowolnym iterowalnym obiekcie, a taki obiekt może nie mieć końca (np. itertools.count()). Dla początkującego zdanie jest bezpieczne; dokładniej: „`for` przechodzi po elementach zestawu, więc kończy się razem z nim”. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0601-weryfikator-faktow.md) · 9.1 s · $0.0308

### 0602 · decyzja · dział 06 · pytanie 33 · próba 1

- Wynik: Sekcja przyjęta; 8 sugestii trafia do raportu.
- 0.0 s

### 0603 · akceptacja · dział 06 · pytanie 33

- Wynik: Sekcja [sec-06-kiedy-siegnac-po-petle] dopisana do działu 06; odwołania: wstecz „potrzebna jest pętla”, w przód „Pętlę, która nigdy się nie kończy, omówimy w następnej kolejności”; punkty zaczepienia: zmienia się tylko imię; w TODO zostało 28.
- 0.0 s

### 0604 · łowca_pułapek · dział 06 · pytanie 33

- Wynik: „Kiedy sięgnąć po pętlę”: brak pułapek
- [prompt i odpowiedź](_przebieg/0604-lowca-pulapek.md) · 2.3 s · $0.0128

### 0605 · autor_dodatków · dział 06 · pytanie 33

- Wynik: „Kiedy sięgnąć po pętlę”: dowcipy: Owce liczone na palcach
- [prompt i odpowiedź](_przebieg/0605-autor-dodatkow.md) · 14.9 s · $0.0743

### 0606 · weryfikator_dodatków · dział 06 · pytanie 33

- Wynik: odrzucone: 1; Owce liczone na palcach: Puenta „zaśniesz szybciej niż one” jest niespójna (owce nie zasypiają, liczy się je, żeby zasnąć), a temat kopiowania linii zamiast pętli powtarza wcześniejszy wpis „Marta kopiuje linię dla każdej osoby”.
- [prompt i odpowiedź](_przebieg/0606-weryfikator-dodatkow.md) · 5.7 s · $0.0605

### 0607 · pisarz · dział 06 · pytanie 34 · próba 1

- Kolejka TODO (27): 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46 …
- Wynik: „Pętla nieskończona”: 170 słów prozy, ```python 3 linii; nowe hasła: pętla nieskończona; warsztat: nieskonczona.py, $ python nieskonczona.py
- [prompt i odpowiedź](_przebieg/0607-pisarz.md) · 24.6 s · $0.0894

### 0608 · kontrola_deterministyczna · dział 06 · pytanie 34 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **nieskonczona.py**: Treść pliku zawiera `...`: czytelnik przepisuje plik dosłownie, podaj pełną treść. _← kontrola_warsztat_
- 0.0 s

### 0609 · weryfikator_pojęć · dział 06 · pytanie 34 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **koniec listy**: wystarczy jedno zdanie; pełne omówienie w pytaniu 35. „Lista” występuje w sensie programistycznym (zestaw danych z końcem), bez wyjaśnienia przy pierwszym użyciu. Zdanie mówiące, że lista to uporządkowany zestaw danych, ułatwiłoby zrozumienie analogii z „Wspólną Kasą”. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **w ciele**: „Ciało pętli” nie jest nazwane ani zdefiniowane. Z kontekstu (wcięte linie) da się je odgadnąć, ale warto dopisać, że ciało to wcięte linie powtarzane w pętli. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0609-weryfikator-pojec.md) · 9.8 s · $0.0272

### 0610 · znudzony_czytelnik · dział 06 · pytanie 34 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **blok kodu `while True` i zdanie o pomyłce**: Najczęstszy przypadek, czyli pętla nieskończona przez pomyłkę, jest opisany tylko słowami („zmienna, której pętla nigdy nie zmienia”). Kod ma wyłącznie sztuczne `while True`. Można zamienić go na 3-liniowy przykład, np. `liczba = 3` / `while liczba > 0:` / `print(liczba)` bez zmniejszania. Wtedy początkujący zobaczy, jak sam napisze taką pętlę. Do tego `...` w ciele pętli może być niezrozumiałe. Lepiej wstawić tam realną linię. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0610-znudzony-czytelnik.md) · 8.8 s · $0.0217

### 0611 · strażnik_przykład · dział 06 · pytanie 34 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0611-straznik-przyklad.md) · 5.4 s · $0.0205

### 0612 · strażnik_warsztat · dział 06 · pytanie 34 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **akapit „Problem jest praktyczny”**: Zdanie „zajmuje procesor” nie zgadza się z przykładem: dzięki time.sleep(0.5) ten skrypt prawie nie obciąża procesora. Popraw np. na: „Program wygląda na zawieszony i nigdy nie pokaże sumy wydatków (bez pauzy w pętli zająłby też cały procesor).” _← strażnik_warsztat_
  - `spójność` (sugestia) **nieskonczona.py**: Plik zawiera import time i time.sleep(0.5), których tekst nie tłumaczy. Dodaj jedno zdanie: „time.sleep(0.5) robi pół sekundy przerwy, żeby napisy nie zalały ekranu; sama pętla działałaby tak samo bez niej.” _← strażnik_warsztat_
  - `spójność` (sugestia) **fragment kodu w sekcji**: Fragment kodu w tekście ma „...” w miejscu time.sleep(0.5), a plik go nie zawiera. Zastąp „...” linią `time.sleep(0.5)` albo dopisz, że „...” oznacza pominięty kod. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0612-straznik-warsztat.md) · 18.7 s · $0.0358

### 0613 · weryfikator_odwołań · dział 06 · pytanie 34 · próba 1

- Wynik: 0 blokujących, 3 sugestii. (odwołania: 2)
- Nowe potrzeby (3):
  - `odwołanie` (sugestia) **warunek zależny od zmiennej**: Druga przyczyna (warunek zależy od zmiennej, której pętla nie zmienia) jest opisana tylko słowami. Warto dodać krótki kod, np. `licznik = 0` i `while licznik < 3:` bez zmiany licznika, oraz wersję poprawną z `licznik = licznik + 1`. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **opis problemu**: Przykład `while True` z `print` wypisywałby tekst bez przerwy, więc program nie „wygląda na zawieszony”. Warto dopisać, że ekran zapełnia się powtarzanym napisem, albo pominąć print w przykładzie. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **ciało, procesor**: Słowa „ciało” (pętli) i „procesor” pojawiają się bez wyjaśnienia; wystarczy krótkie objaśnienie, np. „wcięte linie pętli” i „zajmuje moc komputera”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0613-weryfikator-odwolan.md) · 18.9 s · $0.0450

### 0614 · sprawdzacz_wyników · dział 06 · pytanie 34 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0614-sprawdzacz-wynikow.md) · 4.2 s · $0.0137

### 0615 · weryfikator_faktów · dział 06 · pytanie 34 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 2)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Python przerywa wtedy działanie i wypisuje komunikat `KeyboardInterrupt`**: Dokumentacja (https://docs.python.org/3.13/library/exceptions.html): KeyboardInterrupt to wyjątek zgłaszany po naciśnięciu klawisza przerwania, zwykle Ctrl+C. Twierdzenie jest poprawne. Dokładniej: Python wypisuje też traceback i kończy się linią `KeyboardInterrupt`. Można dodać, że zobaczy się traceback, żeby czytelnik nie był zaskoczony. Poprawka nie jest konieczna. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0615-weryfikator-faktow.md) · 16.6 s · $0.0941

### 0616 · decyzja · dział 06 · pytanie 34 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **nieskonczona.py**: Treść pliku zawiera `...`: czytelnik przepisuje plik dosłownie, podaj pełną treść. _← kontrola_warsztat_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 10 sugestii trafia do raportu.
- 0.0 s

### 0617 · pisarz · dział 06 · pytanie 34 · próba 2

- Kolejka TODO (27): 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46 …
- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **nieskonczona.py**: Treść pliku zawiera `...`: czytelnik przepisuje plik dosłownie, podaj pełną treść. _← kontrola_warsztat_
- Wynik: „Pętla nieskończona”: 181 słów prozy, ```python 4 linii; nowe hasła: pętla nieskończona; warsztat: nieskonczona.py, $ python nieskonczona.py
- [prompt i odpowiedź](_przebieg/0617-pisarz.md) · 20.3 s · $0.0919

### 0618 · kontrola_deterministyczna · dział 06 · pytanie 34 · próba 2

- Wynik: 2 problemów wykrytych bez modelu.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **time**: „time” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („imie”), ale ma inną nazwę. Użyj „imie” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
  - `spójność` (blokująca, niespełniona) **nieskonczona.py**: Treść pliku zawiera `...`: czytelnik przepisuje plik dosłownie, podaj pełną treść. _← kontrola_warsztat_
- 0.0 s

### 0619 · weryfikator_pojęć · dział 06 · pytanie 34 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **import time**: Kod zaczyna się od `import time`, a tekst nie mówi, co ta linia robi. Wystarczy jedno zdanie, że wczytuje dodatkowe narzędzia, w tym `time.sleep`. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **w ciele**: Zwrot „w ciele” pętli nie jest zdefiniowany. Czytelnik może się domyślić, ale warto napisać „w wciętych liniach pętli”. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0619-weryfikator-pojec.md) · 7.1 s · $0.0246

### 0620 · znudzony_czytelnik · dział 06 · pytanie 34 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **pomyłkowa pętla nieskończona**: Pętla z `while True` jest celowo nieskończona. Zdanie o pomyłce (warunek zależy od zmiennej, której pętla nie zmienia) nie ma przykładu, a to właśnie tak czytelnik trafi na problem. Wystarczą 3–4 linie, np. `wydano = 0`, `while wydano < 300:` i `print(wydano)` bez zmiany `wydano`. Wtedy da się zobaczyć, że warunek zawsze daje True. _← znudzony_czytelnik_
  - `wyjaśnienie` (sugestia) **ciało pętli**: Sformułowanie „w ciele nic go nie zmienia” używa słowa „ciało” bez wyjaśnienia. Lepiej napisać „we wciętych liniach”, tak jak w zdaniu wyżej. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0620-znudzony-czytelnik.md) · 9.9 s · $0.0231

### 0621 · strażnik_przykład · dział 06 · pytanie 34 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0621-straznik-przyklad.md) · 5.3 s · $0.0212

### 0622 · strażnik_warsztat · dział 06 · pytanie 34 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **akapit „Problem jest praktyczny”**: Tekst mówi, że program „zajmuje procesor”, ale przykład z time.sleep(1) prawie go nie obciąża. Można zmienić na: „Program wygląda na zawieszony (a pętla bez sleep zajęłaby procesor) i nigdy nie pokaże sumy wydatków.” _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0622-straznik-warsztat.md) · 18.8 s · $0.0356

### 0623 · weryfikator_odwołań · dział 06 · pytanie 34 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **procesor, import time**: Słowo „procesor” i `import time` pojawiają się bez objaśnienia. Wystarczy jedno zdanie, np. że `import time` udostępnia funkcje związane z czasem, a procesor to „układ, który wykonuje obliczenia”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0623-weryfikator-odwolan.md) · 11.9 s · $0.0372

### 0624 · sprawdzacz_wyników · dział 06 · pytanie 34 · próba 2

- Wynik: 1 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `wynik` (blokująca) **blok kodu z while True i time.sleep(1)**: Pod blokiem kodu brakuje bloku ```text z wynikiem. Kod jest samodzielny i wypisuje tekst, więc trzeba dopisać np. (jedna linia na sekundę, bez końca, aż do Ctrl+C):
```text
Liczę wydatki...
Liczę wydatki...
Liczę wydatki...
...
```
Warto dodać zdanie, że linie pojawiają się co sekundę i nigdy się nie kończą. Ewentualnie pokazać też, co widać po Ctrl+C: 'Traceback (most recent call last): ... KeyboardInterrupt'. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **zajmuje procesor**: W podanym przykładzie z time.sleep(1) program prawie nie obciąża procesora, bo większość czasu śpi. Zdanie 'zajmuje procesor' jest prawdziwe dla pętli bez sleep. Warto doprecyzować: 'pętla bez przerwy zajmowałaby procesor'. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0624-sprawdzacz-wynikow.md) · 9.4 s · $0.0200

### 0625 · weryfikator_faktów · dział 06 · pytanie 34 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 3)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Program wygląda na zawieszony, zajmuje procesor i nigdy nie pokaże sumy wydatków.**: Dokumentacja time.sleep (https://docs.python.org/3.13/library/time.html) mówi, że sleep zawiesza wykonanie wątku na podany czas. Pętla z przykładu, z time.sleep(1), prawie nie obciąża procesora. Twierdzenie o zajmowaniu procesora jest prawdziwe dla pętli bez sleep. Można dopisać „pętla bez przerwy zajmuje procesor” albo „program bez sleep zajmuje procesor”. Przykład ze sleep nie wygląda też na zawieszony, bo wypisuje napisy. To tylko nieścisłość, kod działa zgodnie z opisem. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0625-weryfikator-faktow.md) · 18.4 s · $0.1147

### 0626 · decyzja · dział 06 · pytanie 34 · próba 2

- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (blokująca) **time**: „time” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („imie”), ale ma inną nazwę. Użyj „imie” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
  - `spójność` (blokująca, niespełniona) **nieskonczona.py**: Treść pliku zawiera `...`: czytelnik przepisuje plik dosłownie, podaj pełną treść. _← kontrola_warsztat_
  - `wynik` (blokująca) **blok kodu z while True i time.sleep(1)**: Pod blokiem kodu brakuje bloku ```text z wynikiem. Kod jest samodzielny i wypisuje tekst, więc trzeba dopisać np. (jedna linia na sekundę, bez końca, aż do Ctrl+C):
```text
Liczę wydatki...
Liczę wydatki...
Liczę wydatki...
...
```
Warto dodać zdanie, że linie pojawiają się co sekundę i nigdy się nie kończą. Ewentualnie pokazać też, co widać po Ctrl+C: 'Traceback (most recent call last): ... KeyboardInterrupt'. _← sprawdzacz_wyników_
- Wynik: Limit prób (2) wyczerpany; 3 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0627 · akceptacja · dział 06 · pytanie 34

- Wynik: Sekcja [sec-06-petla-nieskonczona] dopisana do działu 06; hasła w glosariuszu: pętla nieskończona; kanony: przykład:+wydatki; odwołania: wstecz „Pętla `for`, którą znasz, kończy się sama”, wstecz „„Wspólna Kasa”, która czeka na koniec listy”; punkty zaczepienia: pytanie przy while; w TODO zostało 27.
- 0.0 s

### 0628 · łowca_pułapek · dział 06 · pytanie 34

- Wynik: „Pętla nieskończona”: brak pułapek
- [prompt i odpowiedź](_przebieg/0628-lowca-pulapek.md) · 2.4 s · $0.0157

### 0629 · autor_dodatków · dział 06 · pytanie 34

- Wynik: „Pętla nieskończona”: dykteryjki: Ponawianie, które nigdy się nie kończyło, rysunki: Chomik w kole bez wyjścia
- [prompt i odpowiedź](_przebieg/0629-autor-dodatkow.md) · 14.1 s · $0.0737

### 0630 · weryfikator_dodatków · dział 06 · pytanie 34

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0630-weryfikator-dodatkow.md) · 10.7 s · $0.0667

### 0631 · pisarz · dział 06 · pytanie 35 · próba 1

- Kolejka TODO (26): 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47 …
- Wynik: „Czym jest lista danych”: 159 słów prozy, ```python 3 linii, ```text 2 linii; nowe hasła: lista danych, element listy; warsztat: listy.py, $ python listy.py
- [prompt i odpowiedź](_przebieg/0631-pisarz.md) · 25.1 s · $0.0935

### 0632 · kontrola_deterministyczna · dział 06 · pytanie 35 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **sec-06-czym-jest-petla**: Oznaczenie [[sec-06-czym-jest-petla]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 0633 · weryfikator_pojęć · dział 06 · pytanie 35 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0633-weryfikator-pojec.md) · 4.9 s · $0.0214

### 0634 · znudzony_czytelnik · dział 06 · pytanie 35 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **wydatki / Wspólna Kasa**: Lista `wydatki` pojawia się tylko w jednym zdaniu, bez żadnych wartości. Warto pokazać ją w jednej linii, np. `wydatki = [45.50, 120, 30]`. Czytelnik zobaczyłby, że lista może zawierać liczby, a nie tylko teksty, i że wiąże się to z projektem „Wspólna Kasa”. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0634-znudzony-czytelnik.md) · 7.0 s · $0.0212

### 0635 · strażnik_przykład · dział 06 · pytanie 35 · próba 1

- Wynik: 2 blokujących, 1 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **kasa.py**: Tekst odwołuje się do pliku „kasa.py”, a w kanonie plik programu to rozlicz.py (wspolna_kasa/rozlicz.py). Popraw nazwę na rozlicz.py. _← strażnik_przykład_
  - `spójność` (blokująca) **lista kwot**: Zdanie „w kasa.py miałeś jedną listę kwot” przeczy kanonowi: w kanonie kwota to pojedyncza zmienna (kwota = 45.5), a listy to osoby i wydatki (lista słowników). Zamień na „miałeś pojedyncze zmienne, np. kwota” albo pomiń to zdanie. _← strażnik_przykład_
  - `spójność` (sugestia) **osoby**: Kod używa osoby = ["Ania", "Bartek", "Celina"] zgodnie z kanonem. Wzmianka o „trzech zmiennych z imionami” jest niespójna z kanonem, gdzie imię było wcześniej tylko zmienną pętli (imie). Sugestia: sformułować ogólnie („zamiast osobnych zmiennych na każde imię”). _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0635-straznik-przyklad.md) · 6.8 s · $0.0238

### 0636 · strażnik_warsztat · dział 06 · pytanie 35 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **zdanie o `osoby` i `wydatki`**: Tekst mówi o zmiennej `wydatki`, a w listy.py takiej zmiennej nie ma; jest `kwoty`. Zamień w zdaniu „`wydatki` to wszystkie zapłacone rachunki” na „`kwoty` to kwoty zapłaconych rachunków, których przybywa”. _← strażnik_warsztat_
  - `spójność` (sugestia) **lista `kwoty`**: Krok 1 tworzy też listę `kwoty` i wypisuje ją jako [45.5, 20, 12.5], ale tekst tego nie omawia. Dodaj jedno zdanie, że lista może zawierać liczby i że Python wypisuje je bez apostrofów. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0636-straznik-warsztat.md) · 9.1 s · $0.0262

### 0637 · weryfikator_odwołań · dział 06 · pytanie 35 · próba 1

- Wynik: 2 blokujących, 0 sugestii. (odwołania: 3)
- Nowe potrzeby (2):
  - `odwołanie` (blokująca) **Do tej pory w kasa.py miałeś jedną listę kwot**: Nawiązanie bez celu: w poprzednim i tym dziale nie ma punktu ani sekcji o liście kwot w kasa.py. Wcześniejsza pętla (dział 06) szła po liście osób, a nie kwot. Popraw na to, co faktycznie było (pętla po osobach), albo usuń zdanie i wyjaśnij na miejscu, że pętla dotąd chodziła po zestawie wartości, czyli po liście. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **w kasa.py miałeś jedną listę kwot**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/0637-weryfikator-odwolan.md) · 12.1 s · $0.0391

### 0638 · sprawdzacz_wyników · dział 06 · pytanie 35 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **To właśnie po takim zestawie chodzi pętla for**: Zdanie „To właśnie po takim zestawie chodzi pętla `for`” brzmi niezręcznie. Lepiej: „Właśnie takie zestawy przechodzi pętla `for`”. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0638-sprawdzacz-wynikow.md) · 5.4 s · $0.0153

### 0639 · weryfikator_faktów · dział 06 · pytanie 35 · próba 1

- Wynik: Brak uwag. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0639-weryfikator-faktow.md) · 13.5 s · $0.0648

### 0640 · decyzja · dział 06 · pytanie 35 · próba 1

- Potrzeby w kolejce przed krokiem (5):
  - `wyjaśnienie` (blokująca) **sec-06-czym-jest-petla**: Oznaczenie [[sec-06-czym-jest-petla]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `spójność` (blokująca) **kasa.py**: Tekst odwołuje się do pliku „kasa.py”, a w kanonie plik programu to rozlicz.py (wspolna_kasa/rozlicz.py). Popraw nazwę na rozlicz.py. _← strażnik_przykład_
  - `spójność` (blokująca) **lista kwot**: Zdanie „w kasa.py miałeś jedną listę kwot” przeczy kanonowi: w kanonie kwota to pojedyncza zmienna (kwota = 45.5), a listy to osoby i wydatki (lista słowników). Zamień na „miałeś pojedyncze zmienne, np. kwota” albo pomiń to zdanie. _← strażnik_przykład_
  - `odwołanie` (blokująca) **Do tej pory w kasa.py miałeś jedną listę kwot**: Nawiązanie bez celu: w poprzednim i tym dziale nie ma punktu ani sekcji o liście kwot w kasa.py. Wcześniejsza pętla (dział 06) szła po liście osób, a nie kwot. Popraw na to, co faktycznie było (pętla po osobach), albo usuń zdanie i wyjaśnij na miejscu, że pętla dotąd chodziła po zestawie wartości, czyli po liście. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **w kasa.py miałeś jedną listę kwot**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Do poprawy: 5 blokujących potrzeb wraca do pisarza; 5 sugestii trafia do raportu.
- 0.0 s

### 0641 · pisarz · dział 06 · pytanie 35 · próba 2

- Kolejka TODO (26): 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47 …
- Potrzeby w kolejce przed krokiem (5):
  - `wyjaśnienie` (blokująca) **sec-06-czym-jest-petla**: Oznaczenie [[sec-06-czym-jest-petla]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `spójność` (blokująca) **kasa.py**: Tekst odwołuje się do pliku „kasa.py”, a w kanonie plik programu to rozlicz.py (wspolna_kasa/rozlicz.py). Popraw nazwę na rozlicz.py. _← strażnik_przykład_
  - `spójność` (blokująca) **lista kwot**: Zdanie „w kasa.py miałeś jedną listę kwot” przeczy kanonowi: w kanonie kwota to pojedyncza zmienna (kwota = 45.5), a listy to osoby i wydatki (lista słowników). Zamień na „miałeś pojedyncze zmienne, np. kwota” albo pomiń to zdanie. _← strażnik_przykład_
  - `odwołanie` (blokująca) **Do tej pory w kasa.py miałeś jedną listę kwot**: Nawiązanie bez celu: w poprzednim i tym dziale nie ma punktu ani sekcji o liście kwot w kasa.py. Wcześniejsza pętla (dział 06) szła po liście osób, a nie kwot. Popraw na to, co faktycznie było (pętla po osobach), albo usuń zdanie i wyjaśnij na miejscu, że pętla dotąd chodziła po zestawie wartości, czyli po liście. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **w kasa.py miałeś jedną listę kwot**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: „Czym jest lista danych”: 154 słów prozy, ```python 3 linii, ```text 2 linii; nowe hasła: lista danych, element listy
- [prompt i odpowiedź](_przebieg/0641-pisarz.md) · 15.2 s · $0.0907

### 0642 · kontrola_deterministyczna · dział 06 · pytanie 35 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0643 · weryfikator_pojęć · dział 06 · pytanie 35 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0643-weryfikator-pojec.md) · 4.4 s · $0.0207

### 0644 · znudzony_czytelnik · dział 06 · pytanie 35 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **akapit „Właśnie po takim zestawie chodzi pętla for…”**: Zdanie jest mętne („teraz przyglądamy się samej liście”) i nic nie wnosi. Można je zastąpić w kodzie drugą listą, np. wydatki = [45.50, 120, 30], która pokaże liczby bez cudzysłowu. Wtedy zdanie o „Wspólnej Kasie” na końcu będzie miało pokrycie w przykładzie. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0644-znudzony-czytelnik.md) · 8.8 s · $0.0221

### 0645 · strażnik_przykład · dział 06 · pytanie 35 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (blokująca) **kasa.py**: Tekst odwołuje się do pliku „kasa.py”, a w kanonie plik programu to rozlicz.py (wspolna_kasa/rozlicz.py). Popraw nazwę na rozlicz.py. _← strażnik_przykład_
  - `spójność` (blokująca) **lista kwot**: Zdanie „w kasa.py miałeś jedną listę kwot” przeczy kanonowi: w kanonie kwota to pojedyncza zmienna (kwota = 45.5), a listy to osoby i wydatki (lista słowników). Zamień na „miałeś pojedyncze zmienne, np. kwota” albo pomiń to zdanie. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0645-straznik-przyklad.md) · 3.8 s · $0.0219

### 0646 · weryfikator_odwołań · dział 06 · pytanie 35 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Do tej pory w kasa.py miałeś jedną listę kwot**: Nawiązanie bez celu: w poprzednim i tym dziale nie ma punktu ani sekcji o liście kwot w kasa.py. Wcześniejsza pętla (dział 06) szła po liście osób, a nie kwot. Popraw na to, co faktycznie było (pętla po osobach), albo usuń zdanie i wyjaśnij na miejscu, że pętla dotąd chodziła po zestawie wartości, czyli po liście. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0646-weryfikator-odwolan.md) · 8.0 s · $0.0368

### 0647 · sprawdzacz_wyników · dział 06 · pytanie 35 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0647-sprawdzacz-wynikow.md) · 4.3 s · $0.0141

### 0648 · weryfikator_faktów · dział 06 · pytanie 35 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0648-weryfikator-faktow.md) · 12.9 s · $0.0558

### 0649 · decyzja · dział 06 · pytanie 35 · próba 2

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 0650 · akceptacja · dział 06 · pytanie 35

- Wynik: Sekcja [sec-06-czym-jest-lista-danych] dopisana do działu 06; hasła w glosariuszu: lista danych, element listy; odwołania: wstecz „wcześniej szła po imionach uczestników”, w przód „Jak sięgnąć po jeden element, omówimy osobno”, w przód „przy przechodzeniu przez wszystkie elementy”; punkty zaczepienia: kolejność na liście; w TODO zostało 26.
- 0.0 s

### 0651 · łowca_pułapek · dział 06 · pytanie 35

- Wynik: „Czym jest lista danych”: brak pułapek
- [prompt i odpowiedź](_przebieg/0651-lowca-pulapek.md) · 2.3 s · $0.0130

### 0652 · autor_dodatków · dział 06 · pytanie 35

- Wynik: „Czym jest lista danych”: dowcipy: Pusta lista to torba przed sklepem
- [prompt i odpowiedź](_przebieg/0652-autor-dodatkow.md) · 11.4 s · $0.0741

### 0653 · weryfikator_dodatków · dział 06 · pytanie 35

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0653-weryfikator-dodatkow.md) · 5.5 s · $0.0616

### 0654 · pisarz · dział 06 · pytanie 36 · próba 1

- Kolejka TODO (25): 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48 …
- Wynik: „Odczyt elementu listy”: 132 słów prozy, ```python 4 linii, ```text 3 linii; nowe hasła: indeks; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0654-pisarz.md) · 24.3 s · $0.0978

### 0655 · kontrola_deterministyczna · dział 06 · pytanie 36 · próba 1

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **sec-06-czym-jest-lista-danych**: Oznaczenie [[sec-06-czym-jest-lista-danych]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 0656 · weryfikator_pojęć · dział 06 · pytanie 36 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **len(osoby) - 1**: Funkcja `len` pojawia się bez wyjaśnienia. Wystarczy jedno zdanie, że `len(osoby)` podaje liczbę elementów listy (tu 3), więc `len(osoby) - 1` daje 2. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0656-weryfikator-pojec.md) · 7.5 s · $0.0232

### 0657 · znudzony_czytelnik · dział 06 · pytanie 36 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0657-znudzony-czytelnik.md) · 5.4 s · $0.0185

### 0658 · strażnik_przykład · dział 06 · pytanie 36 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0658-straznik-przyklad.md) · 5.6 s · $0.0215

### 0659 · strażnik_warsztat · dział 06 · pytanie 36 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Ostatni akapit sekcji**: Zdanie „dostajesz tylko kopię wartości” jest uproszczeniem. Python zwraca odwołanie do tego samego obiektu, co ma znaczenie przy listach zagnieżdżonych. Bezpieczniejsze sformułowanie: „Odczyt niczego nie zmienia: lista zostaje taka sama, a Ty dostajesz wartość elementu”. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0659-straznik-warsztat.md) · 9.7 s · $0.0259

### 0660 · weryfikator_odwołań · dział 06 · pytanie 36 · próba 1

- Wynik: 0 blokujących, 3 sugestii. (odwołania: 1)
- Nowe potrzeby (3):
  - `odwołanie` (sugestia) **[[indeks|indeksem]]**: Znacznik wskazuje na hasło „indeks”, którego nie ma w glosariuszu. Pojęcie jest zdefiniowane w tekście, więc jest zrozumiałe. Warto dodać hasło do glosariusza albo zostawić zwykły tekst bez znacznika linku. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **len(osoby) - 1**: Funkcja `len` pojawia się bez wyjaśnienia. Dodaj krótką wzmiankę, że zwraca liczbę elementów listy (np. len(osoby) daje 3), albo przykład z wynikiem. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **IndexError**: Błąd jest opisany słowami. Przydałby się krótki przykład z `print(osoby[3])` i wyglądem komunikatu. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0660-weryfikator-odwolan.md) · 11.2 s · $0.0373

### 0661 · sprawdzacz_wyników · dział 06 · pytanie 36 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wynik` (sugestia) **IndexError**: Błąd IndexError opisany tylko słowami. Można dodać krótki blok z osoby[3] i wynikiem błędu (Traceback... IndexError: list index out of range), żeby czytelnik zobaczył, jak on wygląda. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **len(osoby) - 1**: Funkcja len() pojawia się bez wyjaśnienia. Warto dodać jedno zdanie, że len(osoby) daje liczbę elementów (tu 3), albo odesłać do sekcji, w której len() jest omówione. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0661-sprawdzacz-wynikow.md) · 6.6 s · $0.0163

### 0662 · weryfikator_faktów · dział 06 · pytanie 36 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 2)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **dostajesz tylko kopię wartości**: W Pythonie odczyt `lista[i]` zwraca odwołanie do tego samego obiektu, nie jego kopię. Dla liczb i napisów (niezmiennych) różnicy nie widać, ale dla elementu-listy zmiana zwróconego obiektu zmieni też listę. Dla poziomu początkującego bezpieczniej: „dostajesz wartość elementu, lista się nie zmienia”. Zob. https://docs.python.org/3.13/reference/datamodel.html _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0662-weryfikator-faktow.md) · 16.4 s · $0.0690

### 0663 · decyzja · dział 06 · pytanie 36 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **sec-06-czym-jest-lista-danych**: Oznaczenie [[sec-06-czym-jest-lista-danych]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 8 sugestii trafia do raportu.
- 0.0 s

### 0664 · pisarz · dział 06 · pytanie 36 · próba 2

- Kolejka TODO (25): 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48 …
- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **sec-06-czym-jest-lista-danych**: Oznaczenie [[sec-06-czym-jest-lista-danych]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- Wynik: „Odczyt elementu listy”: 125 słów prozy, ```python 4 linii, ```text 3 linii; nowe hasła: indeks; warsztat: kasa.py, $ python kasa.py
- [prompt i odpowiedź](_przebieg/0664-pisarz.md) · 21.3 s · $0.1000

### 0665 · kontrola_deterministyczna · dział 06 · pytanie 36 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0666 · weryfikator_pojęć · dział 06 · pytanie 36 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **len(osoby)**: Zapis `len(osoby)` pojawia się bez wyjaśnienia. Wystarczy jedno zdanie, że `len` zwraca liczbę elementów listy (dla trzech osób 3), więc `len(osoby) - 1` daje 2. Pełne omówienie funkcji jest w pytaniu 38. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0666-weryfikator-pojec.md) · 8.6 s · $0.0241

### 0667 · znudzony_czytelnik · dział 06 · pytanie 36 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `skrócenie` (sugestia) **Kolejność zostaje taka, jak w sekcji Czym jest lista danych.**: Zdanie „Kolejność zostaje taka, jak w sekcji Czym jest lista danych” nic nie wnosi. Można je usunąć, a zaoszczędzone miejsce wykorzystać na jedno zdanie o tym, po co w „Wspólnej Kasie” sięgać po pojedynczy element. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0667-znudzony-czytelnik.md) · 6.8 s · $0.0196

### 0668 · strażnik_przykład · dział 06 · pytanie 36 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Odczyt niczego nie zmienia**: Zdanie „dostajesz tylko kopię wartości” jest nieścisłe: odczyt zwraca ten sam obiekt, nie kopię (dla tekstów nie ma to znaczenia, ale dla elementów zmienialnych, np. słowników z `wydatki`, tak). Lepiej: „dostajesz element, a lista zostaje bez zmian”. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0668-straznik-przyklad.md) · 7.2 s · $0.0224

### 0669 · strażnik_warsztat · dział 06 · pytanie 36 · próba 2

- Wynik: 0 blokujących, 3 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **Tekst sekcji vs krok 1**: Tekst tłumaczy indeksy na liście osoby, a krok dopisuje kwoty_wydatkow[0] i kwoty_wydatkow[-1]. Warto dodać jedno zdanie po kroku: pierwszy wydatek to 45.5, ostatni to 12.5, zgodnie z dwoma nowymi wierszami przed Koniec. _← strażnik_warsztat_
  - `spójność` (sugestia) **IndexError**: Błąd IndexError jest opisany, ale nie pokazany. Można dodać krótki przykład print(osoby[3]) z komunikatem: IndexError: list index out of range. _← strażnik_warsztat_
  - `spójność` (sugestia) **Odczyt niczego nie zmienia**: Zdanie „dostajesz tylko kopię wartości” jest nieprecyzyjne. Lepiej: „dostajesz wartość tego elementu, a lista zostaje bez zmian”. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0669-straznik-warsztat.md) · 10.9 s · $0.0273

### 0670 · weryfikator_odwołań · dział 06 · pytanie 36 · próba 2

- Wynik: 1 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- Nowe potrzeby (3):
  - `odwołanie` (sugestia) **indeks**: Pojęcie „indeks” jest kluczowe dla sekcji, nie ma hasła w glosariuszu, a definicja w tekście jest tylko częściowa. Jest tłumaczone (numer, przesunięcie od początku), więc to spełnia definicję w tekście. Nie blokuje, ale warto dodać hasło do glosariusza. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **len(osoby) - 1**: Funkcja `len()` pojawia się bez wyjaśnienia (zwraca liczbę elementów listy). Czytelnik spoza IT nie wie, co to robi. Dodać jedno zdanie: `len(osoby)` daje liczbę elementów, tu 3, więc 3 - 1 = 2. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **IndexError**: Teza o błędzie IndexError nie ma przykładu kodu ani komunikatu. Pokazać `print(osoby[3])` i przykładowy komunikat: IndexError: list index out of range. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0670-weryfikator-odwolan.md) · 8.4 s · $0.0345

### 0671 · sprawdzacz_wyników · dział 06 · pytanie 36 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **Odczyt niczego nie zmienia: ... kopię wartości**: Zdanie „dostajesz tylko kopię wartości” jest nieścisłe: Python zwraca odwołanie do tego samego obiektu, nie kopię. Dla tekstów z przykładu nie ma to znaczenia. Można napisać: „dostajesz wartość, a lista zostaje bez zmian”. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0671-sprawdzacz-wynikow.md) · 6.4 s · $0.0157

### 0672 · weryfikator_faktów · dział 06 · pytanie 36 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **dostajesz tylko kopię wartości**: Dokumentacja opisuje indeksowanie (https://docs.python.org/3.13/tutorial/introduction.html), ale w Pythonie odczyt zwraca referencję do tego samego obiektu, nie kopię. Dla liczb i napisów (niezmiennych) różnica jest niewidoczna, a dla zagnieżdżonych list byłaby. Bezpieczniej: „dostajesz wartość tego elementu, lista się nie zmienia”. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0672-weryfikator-faktow.md) · 15.2 s · $0.0570

### 0673 · decyzja · dział 06 · pytanie 36 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **len(osoby) - 1**: Funkcja `len()` pojawia się bez wyjaśnienia (zwraca liczbę elementów listy). Czytelnik spoza IT nie wie, co to robi. Dodać jedno zdanie: `len(osoby)` daje liczbę elementów, tu 3, więc 3 - 1 = 2. _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0674 · akceptacja · dział 06 · pytanie 36

- Wynik: Sekcja [sec-06-odczyt-elementu-listy] dopisana do działu 06; hasła w glosariuszu: indeks; odwołania: wstecz „Kolejność zostaje taka, jak w sekcji Czym jest lista danych”; punkty zaczepienia: liczenie od zera; w TODO zostało 25.
- 0.0 s

### 0675 · łowca_pułapek · dział 06 · pytanie 36

- Wynik: „Odczyt elementu listy”: brak pułapek
- [prompt i odpowiedź](_przebieg/0675-lowca-pulapek.md) · 3.5 s · $0.0159

### 0676 · autor_dodatków · dział 06 · pytanie 36

- Wynik: „Odczyt elementu listy”: dygresje: Dlaczego liczenie zaczyna się od zera, wtręty: Marta prosi o czwartego, którego nie ma
- [prompt i odpowiedź](_przebieg/0676-autor-dodatkow.md) · 11.9 s · $0.0751

### 0677 · weryfikator_dodatków · dział 06 · pytanie 36

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0677-weryfikator-dodatkow.md) · 13.6 s · $0.1041

### 0678 · pisarz · dział 06 · pytanie 37 · próba 1

- Kolejka TODO (24): 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49 …
- Wynik: „Pętla po elementach listy”: 141 słów prozy, ```python 4 linii, ```text 4 linii
- [prompt i odpowiedź](_przebieg/0678-pisarz.md) · 23.9 s · $0.1077

### 0679 · kontrola_deterministyczna · dział 06 · pytanie 37 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0680 · weryfikator_pojęć · dział 06 · pytanie 37 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0680-weryfikator-pojec.md) · 2.7 s · $0.0190

### 0681 · znudzony_czytelnik · dział 06 · pytanie 37 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0681-znudzony-czytelnik.md) · 5.8 s · $0.0179

### 0682 · strażnik_przykład · dział 06 · pytanie 37 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **kasa.py**: Tekst mówi o pliku „Twój `kasa.py`”, a w kanonie skrypt główny nazywa się `rozlicz.py` (repozytorium wspolna_kasa). Nazwa pliku jest niezgodna z kanonem i niezadeklarowana. Zamień na `rozlicz.py`. Dodatkowo nic w kanonie nie pokazuje, by rozlicz.py wypisywał każdą kwotę i sumował – lepiej opisać to na liście `wydatki` (np. `for wydatek in wydatki: suma += wydatek["kwota"]`). _← strażnik_przykład_
  - `spójność` (sugestia) **pętla zbierająca sumę**: Sekcja zapowiada w ostatnim akapicie pętlę sumującą kwoty, ale nie pokazuje jej kodu. To główny motyw działu (pętla for sumuje kwoty z listy wydatków), a przykład w sekcji używa tylko `print(imie)`. Dodaj krótki blok z `wydatki` i sumowaniem kwot albo usuń zapowiedź. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0682-straznik-przyklad.md) · 6.7 s · $0.0233

### 0683 · weryfikator_odwołań · dział 06 · pytanie 37 · próba 1

- Wynik: 1 blokujących, 1 sugestii. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (blokująca) **Tak robi Twój `kasa.py`**: Nawiązanie do `kasa.py` nie ma celu w sekcjach ani punktach zaczepienia tego i poprzedniego działu, a opisuje sumowanie kwot, którego tu nie pokazano. Usuń to zdanie albo wyjaśnij na miejscu, dając krótki przykład pętli sumującej (np. `suma = 0`, `for kwota in kwoty: suma = suma + kwota`, `print(suma)` po pętli). _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **tak jak w sekcji o liście**: Nawiązanie jest poprawne, ale zgrabniej wskazać sam fakt: „kolejność listy jest stała, więc Ania jest pierwsza”. Fraza „Kolejność ma znaczenie” zadeklarowana przez autora nie występuje w tekście. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0683-weryfikator-odwolan.md) · 12.9 s · $0.0399

### 0684 · sprawdzacz_wyników · dział 06 · pytanie 37 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0684-sprawdzacz-wynikow.md) · 3.8 s · $0.0133

### 0685 · weryfikator_faktów · dział 06 · pytanie 37 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 1)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **po pętli zachowuje wartość ostatniego elementu**: Dokumentacja (https://docs.python.org/3.13/reference/compound_stmts.html, instrukcja for) potwierdza, że nazwy z pętli nie są usuwane po jej zakończeniu. Dodaje jednak, że dla pustej listy zmienna nie zostanie w ogóle przypisana (późniejsze użycie da NameError). Twierdzenie jest poprawne dla listy z elementami; można dodać zastrzeżenie „jeśli lista nie była pusta”. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0685-weryfikator-faktow.md) · 16.3 s · $0.0755

### 0686 · decyzja · dział 06 · pytanie 37 · próba 1

- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (blokująca) **kasa.py**: Tekst mówi o pliku „Twój `kasa.py`”, a w kanonie skrypt główny nazywa się `rozlicz.py` (repozytorium wspolna_kasa). Nazwa pliku jest niezgodna z kanonem i niezadeklarowana. Zamień na `rozlicz.py`. Dodatkowo nic w kanonie nie pokazuje, by rozlicz.py wypisywał każdą kwotę i sumował – lepiej opisać to na liście `wydatki` (np. `for wydatek in wydatki: suma += wydatek["kwota"]`). _← strażnik_przykład_
  - `odwołanie` (blokująca) **Tak robi Twój `kasa.py`**: Nawiązanie do `kasa.py` nie ma celu w sekcjach ani punktach zaczepienia tego i poprzedniego działu, a opisuje sumowanie kwot, którego tu nie pokazano. Usuń to zdanie albo wyjaśnij na miejscu, dając krótki przykład pętli sumującej (np. `suma = 0`, `for kwota in kwoty: suma = suma + kwota`, `print(suma)` po pętli). _← weryfikator_odwołań_
- Wynik: Do poprawy: 2 blokujących potrzeb wraca do pisarza; 3 sugestii trafia do raportu.
- 0.0 s

### 0687 · pisarz · dział 06 · pytanie 37 · próba 2

- Kolejka TODO (24): 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49 …
- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (blokująca) **kasa.py**: Tekst mówi o pliku „Twój `kasa.py`”, a w kanonie skrypt główny nazywa się `rozlicz.py` (repozytorium wspolna_kasa). Nazwa pliku jest niezgodna z kanonem i niezadeklarowana. Zamień na `rozlicz.py`. Dodatkowo nic w kanonie nie pokazuje, by rozlicz.py wypisywał każdą kwotę i sumował – lepiej opisać to na liście `wydatki` (np. `for wydatek in wydatki: suma += wydatek["kwota"]`). _← strażnik_przykład_
  - `odwołanie` (blokująca) **Tak robi Twój `kasa.py`**: Nawiązanie do `kasa.py` nie ma celu w sekcjach ani punktach zaczepienia tego i poprzedniego działu, a opisuje sumowanie kwot, którego tu nie pokazano. Usuń to zdanie albo wyjaśnij na miejscu, dając krótki przykład pętli sumującej (np. `suma = 0`, `for kwota in kwoty: suma = suma + kwota`, `print(suma)` po pętli). _← weryfikator_odwołań_
- Wynik: „Pętla po elementach listy”: 121 słów prozy, ```python 4 linii, ```text 4 linii, ```python 5 linii; wątki: przykład dodaj wydatek, przykład dodaj suma
- [prompt i odpowiedź](_przebieg/0687-pisarz.md) · 18.6 s · $0.0941

### 0688 · kontrola_deterministyczna · dział 06 · pytanie 37 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0689 · weryfikator_pojęć · dział 06 · pytanie 37 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0689-weryfikator-pojec.md) · 5.6 s · $0.0216

### 0690 · znudzony_czytelnik · dział 06 · pytanie 37 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **blok kodu z sumą wydatków**: Drugi blok zaczyna się od `wydatki = ...`, więc czytelnik nie widzi, jak wyglądają dane, i nie może sprawdzić wyniku. Dajcie 2–3 konkretne wydatki, np. `{"nazwa": "chleb", "kwota": 5}`, i pokażcie wynik w bloku text. Wtedy zapis `wydatek["kwota"]` będzie zrozumiały bez zgadywania. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0690-znudzony-czytelnik.md) · 8.0 s · $0.0211

### 0691 · strażnik_przykład · dział 06 · pytanie 37 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **kasa.py**: Tekst mówi o pliku „Twój `kasa.py`”, a w kanonie skrypt główny nazywa się `rozlicz.py` (repozytorium wspolna_kasa). Nazwa pliku jest niezgodna z kanonem i niezadeklarowana. Zamień na `rozlicz.py`. Dodatkowo nic w kanonie nie pokazuje, by rozlicz.py wypisywał każdą kwotę i sumował – lepiej opisać to na liście `wydatki` (np. `for wydatek in wydatki: suma += wydatek["kwota"]`). _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0691-straznik-przyklad.md) · 2.7 s · $0.0211

### 0692 · weryfikator_odwołań · dział 06 · pytanie 37 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Tak robi Twój `kasa.py`**: Nawiązanie do `kasa.py` nie ma celu w sekcjach ani punktach zaczepienia tego i poprzedniego działu, a opisuje sumowanie kwot, którego tu nie pokazano. Usuń to zdanie albo wyjaśnij na miejscu, dając krótki przykład pętli sumującej (np. `suma = 0`, `for kwota in kwoty: suma = suma + kwota`, `print(suma)` po pętli). _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- [prompt i odpowiedź](_przebieg/0692-weryfikator-odwolan.md) · 3.5 s · $0.0317

### 0693 · sprawdzacz_wyników · dział 06 · pytanie 37 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0693-sprawdzacz-wynikow.md) · 3.6 s · $0.0129

### 0694 · weryfikator_faktów · dział 06 · pytanie 37 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 2)
- [prompt i odpowiedź](_przebieg/0694-weryfikator-faktow.md) · 14.5 s · $0.0695

### 0695 · decyzja · dział 06 · pytanie 37 · próba 2

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 0696 · akceptacja · dział 06 · pytanie 37

- Wynik: Sekcja [sec-06-petla-po-elementach-listy] dopisana do działu 06; kanony: przykład:+wydatek przykład:+suma; odwołania: wstecz „więc „Ania” jest pierwsza”; punkty zaczepienia: suma zbierana w pętli; w TODO zostało 24.
- 0.0 s

### 0697 · łowca_pułapek · dział 06 · pytanie 37

- Wynik: „Pętla po elementach listy”: brak pułapek
- [prompt i odpowiedź](_przebieg/0697-lowca-pulapek.md) · 2.2 s · $0.0128

### 0698 · autor_dodatków · dział 06 · pytanie 37

- Wynik: „Pętla po elementach listy”: dowcipy: Lista obecności bez wołania w próżnię
- [prompt i odpowiedź](_przebieg/0698-autor-dodatkow.md) · 7.8 s · $0.0728

### 0699 · weryfikator_dodatków · dział 06 · pytanie 37

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0699-weryfikator-dodatkow.md) · 4.6 s · $0.0642

### 0700 · autor_wstępu · dział 07 · próba 1

- Kolejka TODO (24): 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49 …
- Wynik: Wstęp: 88 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0700-autor-wstepu.md) · 5.7 s · $0.0308

### 0701 · recenzent_wstępu · dział 07 · próba 1

- Wynik: 2 blokujących, 2 sugestii.
- Nowe potrzeby (4):
  - `diagram` (blokująca) **Diagram: „suma, osoby ──► na_osobe(suma, osoby) ──► kwota”**: Diagram jest niespójny z wstępem i wprowadza w błąd. Dwie linie wyglądają na dwa osobne, niepowiązane przepływy; nie widać, że wynik pierwszej funkcji (suma) trafia do drugiej. Etykieta „kwota” nie pojawia się w tekście (wstęp mówi o udziale na osobę), a „osoby” nie ma skąd się wziąć. Pominięto też saldo_osoby, choć wstęp ją zapowiada. Przerysuj jako jeden ciąg: wydatki ──► suma(wydatki) ──► suma ──► na_osobe(suma, osoby) ──► udział na osobę, z dopiskiem, że osoby (liczba osób) wchodzi do na_osobe z boku (np. strzałka z góry). Użyj tych samych nazw co w tekście albo krótko opisz, co znaczą strzałki (dane wchodzą / wynik wychodzi). _← recenzent_wstępu_
  - `spójność` (blokująca) **nazwy funkcji: suma_wydatkow, udzial_na_osobe, saldo_osoby vs suma(wydatki), na_osobe(suma, osoby)**: We wstępie te same funkcje występują pod dwoma różnymi zestawami nazw (suma_wydatkow/udzial_na_osobe vs suma/na_osobe), bez wyjaśnienia. Początkujący pomyśli, że to sześć różnych funkcji albo pomyłka. Ujednolić nazwy albo jedno zdanie: warsztat to uproszczona wersja przykładu. Diagram też używa krótkich nazw. _← recenzent_wstępu_
  - `tempo` (sugestia) **Wymienione nazwy funkcji i zapisy typu suma(wydatki), na_osobe(suma, osoby)**: Wstęp jest gęsty od zapisów kodu, a czytelnik nie zna jeszcze nawiasów w wywołaniu funkcji. Zostaw w tekście nazwy zapowiadające scenariusz (Wspólna Kasa, dwa wyjazdy), a zapisy kodu zostaw diagramowi lub sekcjom. _← recenzent_wstępu_
  - `wyjaśnienie` (sugestia) **„Wspólnej Kasy”**: Jeśli „Wspólna Kasa” nie była wprowadzona w poprzednich działach, dodaj pół zdania: kto z kim się rozlicza (np. wspólne wydatki na wyjeździe). Wtedy hasło „saldo osoby” będzie zrozumiałe. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0701-recenzent-wstepu.md) · 11.1 s · $0.0233

### 0702 · decyzja · dział 07 · próba 1

- Wynik: Wstęp wraca do autora.
- Nowe potrzeby (2):
  - `diagram` (blokująca) **Diagram: „suma, osoby ──► na_osobe(suma, osoby) ──► kwota”**: Diagram jest niespójny z wstępem i wprowadza w błąd. Dwie linie wyglądają na dwa osobne, niepowiązane przepływy; nie widać, że wynik pierwszej funkcji (suma) trafia do drugiej. Etykieta „kwota” nie pojawia się w tekście (wstęp mówi o udziale na osobę), a „osoby” nie ma skąd się wziąć. Pominięto też saldo_osoby, choć wstęp ją zapowiada. Przerysuj jako jeden ciąg: wydatki ──► suma(wydatki) ──► suma ──► na_osobe(suma, osoby) ──► udział na osobę, z dopiskiem, że osoby (liczba osób) wchodzi do na_osobe z boku (np. strzałka z góry). Użyj tych samych nazw co w tekście albo krótko opisz, co znaczą strzałki (dane wchodzą / wynik wychodzi). _← recenzent_wstępu_
  - `spójność` (blokująca) **nazwy funkcji: suma_wydatkow, udzial_na_osobe, saldo_osoby vs suma(wydatki), na_osobe(suma, osoby)**: We wstępie te same funkcje występują pod dwoma różnymi zestawami nazw (suma_wydatkow/udzial_na_osobe vs suma/na_osobe), bez wyjaśnienia. Początkujący pomyśli, że to sześć różnych funkcji albo pomyłka. Ujednolić nazwy albo jedno zdanie: warsztat to uproszczona wersja przykładu. Diagram też używa krótkich nazw. _← recenzent_wstępu_
- 0.0 s

### 0703 · autor_wstępu · dział 07 · próba 2

- Kolejka TODO (24): 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49 …
- Potrzeby w kolejce przed krokiem (2):
  - `diagram` (blokująca) **Diagram: „suma, osoby ──► na_osobe(suma, osoby) ──► kwota”**: Diagram jest niespójny z wstępem i wprowadza w błąd. Dwie linie wyglądają na dwa osobne, niepowiązane przepływy; nie widać, że wynik pierwszej funkcji (suma) trafia do drugiej. Etykieta „kwota” nie pojawia się w tekście (wstęp mówi o udziale na osobę), a „osoby” nie ma skąd się wziąć. Pominięto też saldo_osoby, choć wstęp ją zapowiada. Przerysuj jako jeden ciąg: wydatki ──► suma(wydatki) ──► suma ──► na_osobe(suma, osoby) ──► udział na osobę, z dopiskiem, że osoby (liczba osób) wchodzi do na_osobe z boku (np. strzałka z góry). Użyj tych samych nazw co w tekście albo krótko opisz, co znaczą strzałki (dane wchodzą / wynik wychodzi). _← recenzent_wstępu_
  - `spójność` (blokująca) **nazwy funkcji: suma_wydatkow, udzial_na_osobe, saldo_osoby vs suma(wydatki), na_osobe(suma, osoby)**: We wstępie te same funkcje występują pod dwoma różnymi zestawami nazw (suma_wydatkow/udzial_na_osobe vs suma/na_osobe), bez wyjaśnienia. Początkujący pomyśli, że to sześć różnych funkcji albo pomyłka. Ujednolić nazwy albo jedno zdanie: warsztat to uproszczona wersja przykładu. Diagram też używa krótkich nazw. _← recenzent_wstępu_
- Wynik: Wstęp: 90 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0703-autor-wstepu.md) · 5.3 s · $0.0360

### 0704 · recenzent_wstępu · dział 07 · próba 2

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `diagram` (blokująca, niespełniona) **diagram: strzałka „osoby” do na_osobe**: Strzałka z góry („osoby” i ▼) jest przesunięta w lewo. Wypada nad połączeniem suma(wydatki) ──► suma, a nie nad na_osobe(suma, osoby). Czytelnik może uznać, że liczba osób wchodzi do funkcji suma albo do samej strzałki. Przesuń „osoby” i ▼ tak, żeby stały dokładnie nad na_osobe(...), np. nad literami „na_osobe”. Reszta diagramu jest już spójna: jeden ciąg, te same nazwy co w warsztacie i legenda strzałek. Nazwy funkcji też są wyjaśnione, bo warsztat to „uproszczona wersja”. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0704-recenzent-wstepu.md) · 10.8 s · $0.0265

### 0705 · decyzja · dział 07 · próba 2

- Wynik: Limit prób wyczerpany, wstęp zostaje.
- Nowe potrzeby (1):
  - `diagram` (blokująca, niespełniona) **diagram: strzałka „osoby” do na_osobe**: Strzałka z góry („osoby” i ▼) jest przesunięta w lewo. Wypada nad połączeniem suma(wydatki) ──► suma, a nie nad na_osobe(suma, osoby). Czytelnik może uznać, że liczba osób wchodzi do funkcji suma albo do samej strzałki. Przesuń „osoby” i ▼ tak, żeby stały dokładnie nad na_osobe(...), np. nad literami „na_osobe”. Reszta diagramu jest już spójna: jeden ciąg, te same nazwy co w warsztacie i legenda strzałek. Nazwy funkcji też są wyjaśnione, bo warsztat to „uproszczona wersja”. _← recenzent_wstępu_
- 0.0 s

### 0706 · pisarz · dział 07 · pytanie 38 · próba 1

- Kolejka TODO (23): 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50 …
- Wynik: „Czym jest funkcja”: 136 słów prozy, ```python 9 linii, ```text 1 linii; nowe hasła: definicja funkcji, wywołanie funkcji; wątki: przykład dodaj suma_wydatkow; warsztat: funkcje.py, $ python funkcje.py
- [prompt i odpowiedź](_przebieg/0706-pisarz.md) · 24.3 s · $0.0930

### 0707 · kontrola_deterministyczna · dział 07 · pytanie 38 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0708 · weryfikator_pojęć · dział 07 · pytanie 38 · próba 1

- Wynik: 2 blokujących, 0 sugestii. (eskalowano 1 powtarzających się braków do blokujących)
- Nowe potrzeby (2):
  - `wyjaśnienie` (blokująca) **wydatek["kwota"]**: W przykładzie każdy wydatek to zapis w klamrach {"kto": ..., "kwota": ...}, a kwotę czytamy przez wydatek["kwota"]. Takiej struktury (słownika: pary klucz–wartość) nie ma w glosariuszu ani w tekście. Czytelnik zna tylko listy z indeksami, więc nie zrozumie, czym jest wydatek["kwota"] ani skąd wynik 320.5. Wystarczy jedno zdanie, np. że wydatek to karteczka z podpisanymi polami, a wydatek["kwota"] odczytuje pole „kwota”. Można też uprościć przykład do samych liczb. _← weryfikator_pojęć_
  - `wyjaśnienie` (blokująca) **skryptu**: Słowo „skrypt” nie jest w glosariuszu ani wyjaśnione. Można je zastąpić słowem „program” albo dodać krótkie wyjaśnienie. [Eskalacja: zgłaszane już w sekcji „Łączenie tekstów”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0708-weryfikator-pojec.md) · 10.1 s · $0.0276

### 0709 · znudzony_czytelnik · dział 07 · pytanie 38 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **Konsekwencja: kod ... bez kopiowania**: Końcowa teza, że funkcję można wywołać w wielu miejscach bez kopiowania, nie ma pokazu. W istniejącym bloku kodu wystarczy dodać drugie wywołanie z inną listą, np. print(suma_wydatkow([])) z wynikiem 0. Wtedy widać, po co jest nazwa i że funkcja pracuje na różnych danych. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0709-znudzony-czytelnik.md) · 6.9 s · $0.0209

### 0710 · strażnik_przykład · dział 07 · pytanie 38 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0710-straznik-przyklad.md) · 5.5 s · $0.0227

### 0711 · strażnik_warsztat · dział 07 · pytanie 38 · próba 1

- Wynik: 2 blokujących, 0 sugestii.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **przykład w tekście sekcji vs plik funkcje.py**: Tekst pokazuje funkcję `suma_wydatkow` z listą słowników (`wydatek["kwota"]`, wynik 320.5). Krok 1 tworzy jednak `funkcje.py` z funkcją `suma`, listą liczb [45.5, 20, 12.5] i wynikiem 78.0. Czytelnik nie napisze i nie uruchomi przykładu z tekstu, a nazwy i wartości się rozjeżdżają. Popraw tekst tak, żeby pokazywał ten sam kod co `funkcje.py`: `def suma(wydatki):` z pętlą `for kwota in wydatki:` i `print(suma([45.5, 20, 12.5]))`, a jako wynik podaj `78.0`. Możesz też zmienić plik w kroku 1 na wersję z tekstu i dopasować wynik do `320.5`. _← strażnik_warsztat_
  - `spójność` (blokująca) **zdanie „pętlę, która zbiera sumę wydatków, jak w poprzedniej sekcji”**: Pętla z `kasa.py` działa na liście liczb `kwoty_wydatkow` i zmiennej `suma`, a nie na słownikach z kluczem `"kwota"`. Po ujednoliceniu przykładu z `funkcje.py` zdanie będzie prawdziwe: funkcja `suma` powtarza pętlę z `kasa.py` (`for kwota in kwoty_wydatkow`). _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0711-straznik-warsztat.md) · 13.1 s · $0.0302

### 0712 · weryfikator_odwołań · dział 07 · pytanie 38 · próba 1

- Wynik: 1 blokujących, 2 sugestii. (odwołania: 3)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **kod przykładu z wydatkami**: Przykład używa `wydatek["kwota"]` i elementów w nawiasach klamrowych z kluczami ("kto", "opis", "kwota"). Tutorial dotąd wprowadził tylko listy z indeksami liczbowymi; zapis z kluczami jest nieznany czytelnikowi. Uprość przykład do listy liczb (np. `wydatki = [120.50, 200]` i `suma = suma + wydatek`) albo wyjaśnij na miejscu, czym jest taki zapis. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **str()**: Zdanie „Znasz już ... `str()`” zakłada, że czytelnik poznał `str()`, a nie ma na to punktu zaczepienia ani hasła glosariusza. Usuń `str()` albo krótko wyjaśnij, co robi. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **wydatki**: Zmienna globalna i parametr mają tę samą nazwę `wydatki`, co może mylić początkującego. Rozważ inną nazwę parametru albo jedno zdanie wyjaśnienia. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0712-weryfikator-odwolan.md) · 16.8 s · $0.0406

### 0713 · sprawdzacz_wyników · dział 07 · pytanie 38 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0713-sprawdzacz-wynikow.md) · 3.5 s · $0.0135

### 0714 · weryfikator_faktów · dział 07 · pytanie 38 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 1)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **`print()` i `str()` to funkcje napisane przez twórców Pythona**: Dokumentacja Pythona 3.13 (https://docs.python.org/3.13/library/functions.html) opisuje `print` jako funkcję wbudowaną, ale `str` jako klasę (`class str(object='')`). Dla początkującego różnica jest nieistotna, a `str()` wywołuje się tak samo jak funkcję. Można zostawić albo zamienić przykład na `print()` i `len()` (`len` to funkcja wbudowana), albo napisać „gotowe kawałki, np. `print()` i `len()`”. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0714-weryfikator-faktow.md) · 16.3 s · $0.0807

### 0715 · decyzja · dział 07 · pytanie 38 · próba 1

- Potrzeby w kolejce przed krokiem (5):
  - `wyjaśnienie` (blokująca) **wydatek["kwota"]**: W przykładzie każdy wydatek to zapis w klamrach {"kto": ..., "kwota": ...}, a kwotę czytamy przez wydatek["kwota"]. Takiej struktury (słownika: pary klucz–wartość) nie ma w glosariuszu ani w tekście. Czytelnik zna tylko listy z indeksami, więc nie zrozumie, czym jest wydatek["kwota"] ani skąd wynik 320.5. Wystarczy jedno zdanie, np. że wydatek to karteczka z podpisanymi polami, a wydatek["kwota"] odczytuje pole „kwota”. Można też uprościć przykład do samych liczb. _← weryfikator_pojęć_
  - `wyjaśnienie` (blokująca) **skryptu**: Słowo „skrypt” nie jest w glosariuszu ani wyjaśnione. Można je zastąpić słowem „program” albo dodać krótkie wyjaśnienie. [Eskalacja: zgłaszane już w sekcji „Łączenie tekstów”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
  - `spójność` (blokująca) **przykład w tekście sekcji vs plik funkcje.py**: Tekst pokazuje funkcję `suma_wydatkow` z listą słowników (`wydatek["kwota"]`, wynik 320.5). Krok 1 tworzy jednak `funkcje.py` z funkcją `suma`, listą liczb [45.5, 20, 12.5] i wynikiem 78.0. Czytelnik nie napisze i nie uruchomi przykładu z tekstu, a nazwy i wartości się rozjeżdżają. Popraw tekst tak, żeby pokazywał ten sam kod co `funkcje.py`: `def suma(wydatki):` z pętlą `for kwota in wydatki:` i `print(suma([45.5, 20, 12.5]))`, a jako wynik podaj `78.0`. Możesz też zmienić plik w kroku 1 na wersję z tekstu i dopasować wynik do `320.5`. _← strażnik_warsztat_
  - `spójność` (blokująca) **zdanie „pętlę, która zbiera sumę wydatków, jak w poprzedniej sekcji”**: Pętla z `kasa.py` działa na liście liczb `kwoty_wydatkow` i zmiennej `suma`, a nie na słownikach z kluczem `"kwota"`. Po ujednoliceniu przykładu z `funkcje.py` zdanie będzie prawdziwe: funkcja `suma` powtarza pętlę z `kasa.py` (`for kwota in kwoty_wydatkow`). _← strażnik_warsztat_
  - `odwołanie` (blokująca) **kod przykładu z wydatkami**: Przykład używa `wydatek["kwota"]` i elementów w nawiasach klamrowych z kluczami ("kto", "opis", "kwota"). Tutorial dotąd wprowadził tylko listy z indeksami liczbowymi; zapis z kluczami jest nieznany czytelnikowi. Uprość przykład do listy liczb (np. `wydatki = [120.50, 200]` i `suma = suma + wydatek`) albo wyjaśnij na miejscu, czym jest taki zapis. _← weryfikator_odwołań_
- Wynik: Do poprawy: 5 blokujących potrzeb wraca do pisarza; 4 sugestii trafia do raportu.
- 0.0 s

### 0716 · pisarz · dział 07 · pytanie 38 · próba 2

- Kolejka TODO (23): 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50 …
- Potrzeby w kolejce przed krokiem (5):
  - `wyjaśnienie` (blokująca) **wydatek["kwota"]**: W przykładzie każdy wydatek to zapis w klamrach {"kto": ..., "kwota": ...}, a kwotę czytamy przez wydatek["kwota"]. Takiej struktury (słownika: pary klucz–wartość) nie ma w glosariuszu ani w tekście. Czytelnik zna tylko listy z indeksami, więc nie zrozumie, czym jest wydatek["kwota"] ani skąd wynik 320.5. Wystarczy jedno zdanie, np. że wydatek to karteczka z podpisanymi polami, a wydatek["kwota"] odczytuje pole „kwota”. Można też uprościć przykład do samych liczb. _← weryfikator_pojęć_
  - `wyjaśnienie` (blokująca) **skryptu**: Słowo „skrypt” nie jest w glosariuszu ani wyjaśnione. Można je zastąpić słowem „program” albo dodać krótkie wyjaśnienie. [Eskalacja: zgłaszane już w sekcji „Łączenie tekstów”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
  - `spójność` (blokująca) **przykład w tekście sekcji vs plik funkcje.py**: Tekst pokazuje funkcję `suma_wydatkow` z listą słowników (`wydatek["kwota"]`, wynik 320.5). Krok 1 tworzy jednak `funkcje.py` z funkcją `suma`, listą liczb [45.5, 20, 12.5] i wynikiem 78.0. Czytelnik nie napisze i nie uruchomi przykładu z tekstu, a nazwy i wartości się rozjeżdżają. Popraw tekst tak, żeby pokazywał ten sam kod co `funkcje.py`: `def suma(wydatki):` z pętlą `for kwota in wydatki:` i `print(suma([45.5, 20, 12.5]))`, a jako wynik podaj `78.0`. Możesz też zmienić plik w kroku 1 na wersję z tekstu i dopasować wynik do `320.5`. _← strażnik_warsztat_
  - `spójność` (blokująca) **zdanie „pętlę, która zbiera sumę wydatków, jak w poprzedniej sekcji”**: Pętla z `kasa.py` działa na liście liczb `kwoty_wydatkow` i zmiennej `suma`, a nie na słownikach z kluczem `"kwota"`. Po ujednoliceniu przykładu z `funkcje.py` zdanie będzie prawdziwe: funkcja `suma` powtarza pętlę z `kasa.py` (`for kwota in kwoty_wydatkow`). _← strażnik_warsztat_
  - `odwołanie` (blokująca) **kod przykładu z wydatkami**: Przykład używa `wydatek["kwota"]` i elementów w nawiasach klamrowych z kluczami ("kto", "opis", "kwota"). Tutorial dotąd wprowadził tylko listy z indeksami liczbowymi; zapis z kluczami jest nieznany czytelnikowi. Uprość przykład do listy liczb (np. `wydatki = [120.50, 200]` i `suma = suma + wydatek`) albo wyjaśnij na miejscu, czym jest taki zapis. _← weryfikator_odwołań_
- Wynik: „Czym jest funkcja”: 144 słów prozy, ```python 7 linii, ```text 1 linii; nowe hasła: definicja funkcji, wywołanie funkcji; wątki: warsztat dodaj suma; warsztat: funkcje.py, $ python funkcje.py
- [prompt i odpowiedź](_przebieg/0716-pisarz.md) · 18.2 s · $0.0973

### 0717 · kontrola_deterministyczna · dział 07 · pytanie 38 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0718 · weryfikator_pojęć · dział 07 · pytanie 38 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `wyjaśnienie` (blokująca) **wydatek["kwota"]**: W przykładzie każdy wydatek to zapis w klamrach {"kto": ..., "kwota": ...}, a kwotę czytamy przez wydatek["kwota"]. Takiej struktury (słownika: pary klucz–wartość) nie ma w glosariuszu ani w tekście. Czytelnik zna tylko listy z indeksami, więc nie zrozumie, czym jest wydatek["kwota"] ani skąd wynik 320.5. Wystarczy jedno zdanie, np. że wydatek to karteczka z podpisanymi polami, a wydatek["kwota"] odczytuje pole „kwota”. Można też uprościć przykład do samych liczb. _← weryfikator_pojęć_
  - `wyjaśnienie` (blokująca) **skryptu**: Słowo „skrypt” nie jest w glosariuszu ani wyjaśnione. Można je zastąpić słowem „program” albo dodać krótkie wyjaśnienie. [Eskalacja: zgłaszane już w sekcji „Łączenie tekstów”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0718-weryfikator-pojec.md) · 3.9 s · $0.0229

### 0719 · znudzony_czytelnik · dział 07 · pytanie 38 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `skrócenie` (sugestia) **Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy**: Zdanie „Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek” jest zawiłe i mętnie odwołuje się do zapowiedzi. Wystarczy: „Zamieńmy tę pętlę w funkcję.” _← znudzony_czytelnik_
  - `przykład` (sugestia) **Konsekwencja: kod ... można go wywołać w wielu miejscach**: Końcowa teza, że funkcję wywołasz w wielu miejscach bez kopiowania, nie ma pokazu. Wystarczy drugie wywołanie, np. print(suma([10, 5])), z wynikiem 15, zamiast osobnego zdania podsumowania. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0719-znudzony-czytelnik.md) · 8.4 s · $0.0220

### 0720 · strażnik_przykład · dział 07 · pytanie 38 · próba 2

- Wynik: 2 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **suma (funkcja)**: Kanon ma już `suma` jako zmienną (liczbę: `suma = 0` w pętli po `wydatki`). Funkcja `def suma(wydatki)` nadaje tę samą nazwę innemu bytowi, a czytelnik ma w programie obie rzeczy. Plan wątku przewiduje funkcję `suma_wydatkow`. Zmień na `def suma_wydatkow(wydatki):` i zadeklaruj ją w canon_changes (module="przykład", dodaj, np. `suma_wydatkow(wydatki)` · funkcja · wspolna_kasa/rozlicz.py, zwraca liczbę). _← strażnik_przykład_
  - `spójność` (blokująca) **wydatki**: W kanonie `wydatki` to lista słowników (`{"kto", "opis", "kwota"}`), a pętla używa `wydatek["kwota"]`. Tu `wydatki` to lista samych liczb (`[45.5, 20, 12.5]`), a pętla ma `for kwota in wydatki`. To inny typ argumentu pod tą samą nazwą, a `kwota` w kanonie jest zmienną liczbową, nie zmienną pętli. Popraw ciało na `for wydatek in wydatki: suma = suma + wydatek["kwota"]`, a wywołanie na liście słowników, np. `[{"kto": "Ania", "opis": "zakupy", "kwota": 45.5}, ...]`. Wynik 78.0 zostaje. _← strażnik_przykład_
  - `spójność` (sugestia) **razem**: Nowa zmienna `razem` dubluje kanoniczną `suma` z pętli, na którą tekst się powołuje („taką jak w sekcji o pętli”). Użyj `suma` wewnątrz funkcji (nie koliduje, jeśli funkcja nazywa się `suma_wydatkow`), żeby czytelnik widział ten sam kod przeniesiony do funkcji. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0720-straznik-przyklad.md) · 14.3 s · $0.0323

### 0721 · strażnik_warsztat · dział 07 · pytanie 38 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (blokująca) **przykład w tekście sekcji vs plik funkcje.py**: Tekst pokazuje funkcję `suma_wydatkow` z listą słowników (`wydatek["kwota"]`, wynik 320.5). Krok 1 tworzy jednak `funkcje.py` z funkcją `suma`, listą liczb [45.5, 20, 12.5] i wynikiem 78.0. Czytelnik nie napisze i nie uruchomi przykładu z tekstu, a nazwy i wartości się rozjeżdżają. Popraw tekst tak, żeby pokazywał ten sam kod co `funkcje.py`: `def suma(wydatki):` z pętlą `for kwota in wydatki:` i `print(suma([45.5, 20, 12.5]))`, a jako wynik podaj `78.0`. Możesz też zmienić plik w kroku 1 na wersję z tekstu i dopasować wynik do `320.5`. _← strażnik_warsztat_
  - `spójność` (blokująca) **zdanie „pętlę, która zbiera sumę wydatków, jak w poprzedniej sekcji”**: Pętla z `kasa.py` działa na liście liczb `kwoty_wydatkow` i zmiennej `suma`, a nie na słownikach z kluczem `"kwota"`. Po ujednoliceniu przykładu z `funkcje.py` zdanie będzie prawdziwe: funkcja `suma` powtarza pętlę z `kasa.py` (`for kwota in kwoty_wydatkow`). _← strażnik_warsztat_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0721-straznik-warsztat.md) · 4.8 s · $0.0249

### 0722 · weryfikator_odwołań · dział 07 · pytanie 38 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **kod przykładu z wydatkami**: Przykład używa `wydatek["kwota"]` i elementów w nawiasach klamrowych z kluczami ("kto", "opis", "kwota"). Tutorial dotąd wprowadził tylko listy z indeksami liczbowymi; zapis z kluczami jest nieznany czytelnikowi. Uprość przykład do listy liczb (np. `wydatki = [120.50, 200]` i `suma = suma + wydatek`) albo wyjaśnij na miejscu, czym jest taki zapis. _← weryfikator_odwołań_
- Wynik: 2 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 3)
- Nowe potrzeby (2):
  - `odwołanie` (blokująca) **robimy to, co zapowiadaliśmy**: Zdanie „robimy to, co zapowiadaliśmy” odsyła do sekcji o podziale problemu na części (sec-02), która nie należy do tego ani poprzedniego działu, więc nie ma poprawnego celu nawiązania i czytelnik nie wie, co było zapowiedziane. Usuń to sformułowanie albo wyjaśnij na miejscu, np. „Zamieniamy ją w osobną funkcję: wydzielamy tę część programu w osobny, nazwany kawałek”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **robimy to, co zapowiadaliśmy**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/0722-weryfikator-odwolan.md) · 12.0 s · $0.0384

### 0723 · sprawdzacz_wyników · dział 07 · pytanie 38 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0723-sprawdzacz-wynikow.md) · 3.8 s · $0.0137

### 0724 · weryfikator_faktów · dział 07 · pytanie 38 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **`print()` i `str()` napisali twórcy Pythona**: W dokumentacji Pythona (docs.python.org/3/library/functions.html) `str` jest klasą (typem), a nie zwykłą funkcją; `print` jest funkcją. Dla początkującego przybliżenie „gotowa funkcja” jest w porządku i kod się nie zmienia. Ewentualnie zamień `str()` na `len()` albo `input()`, które są funkcjami. Nie sprawdzałem tego w dokumentacji online w tej sesji, to wiedza własna. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0724-weryfikator-faktow.md) · 8.8 s · $0.0314

### 0725 · decyzja · dział 07 · pytanie 38 · próba 2

- Potrzeby w kolejce przed krokiem (4):
  - `spójność` (blokująca) **suma (funkcja)**: Kanon ma już `suma` jako zmienną (liczbę: `suma = 0` w pętli po `wydatki`). Funkcja `def suma(wydatki)` nadaje tę samą nazwę innemu bytowi, a czytelnik ma w programie obie rzeczy. Plan wątku przewiduje funkcję `suma_wydatkow`. Zmień na `def suma_wydatkow(wydatki):` i zadeklaruj ją w canon_changes (module="przykład", dodaj, np. `suma_wydatkow(wydatki)` · funkcja · wspolna_kasa/rozlicz.py, zwraca liczbę). _← strażnik_przykład_
  - `spójność` (blokująca) **wydatki**: W kanonie `wydatki` to lista słowników (`{"kto", "opis", "kwota"}`), a pętla używa `wydatek["kwota"]`. Tu `wydatki` to lista samych liczb (`[45.5, 20, 12.5]`), a pętla ma `for kwota in wydatki`. To inny typ argumentu pod tą samą nazwą, a `kwota` w kanonie jest zmienną liczbową, nie zmienną pętli. Popraw ciało na `for wydatek in wydatki: suma = suma + wydatek["kwota"]`, a wywołanie na liście słowników, np. `[{"kto": "Ania", "opis": "zakupy", "kwota": 45.5}, ...]`. Wynik 78.0 zostaje. _← strażnik_przykład_
  - `odwołanie` (blokująca) **robimy to, co zapowiadaliśmy**: Zdanie „robimy to, co zapowiadaliśmy” odsyła do sekcji o podziale problemu na części (sec-02), która nie należy do tego ani poprzedniego działu, więc nie ma poprawnego celu nawiązania i czytelnik nie wie, co było zapowiedziane. Usuń to sformułowanie albo wyjaśnij na miejscu, np. „Zamieniamy ją w osobną funkcję: wydzielamy tę część programu w osobny, nazwany kawałek”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **robimy to, co zapowiadaliśmy**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Limit prób (2) wyczerpany; 4 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0726 · akceptacja · dział 07 · pytanie 38

- Wynik: Sekcja [sec-07-czym-jest-funkcja] dopisana do działu 07; hasła w glosariuszu: definicja funkcji, wywołanie funkcji; kanony: warsztat:+suma; odwołania: wstecz „taką jak w sekcji o pętli po elementach listy”, w przód „Oba mechanizmy omówimy osobno w kolejnych sekcjach”, w przód „Oba mechanizmy omówimy osobno w kolejnych sekcjach”; punkty zaczepienia: suma jako funkcja; w TODO zostało 23.
- 0.0 s

### 0727 · łowca_pułapek · dział 07 · pytanie 38

- Wynik: „Czym jest funkcja”: brak pułapek
- [prompt i odpowiedź](_przebieg/0727-lowca-pulapek.md) · 2.4 s · $0.0130

### 0728 · autor_dodatków · dział 07 · pytanie 38

- Wynik: „Czym jest funkcja”: wtręty: Marta opisuje funkcję i czeka na wynik, dykteryjki: Poprawka w trzech miejscach z czterech
- [prompt i odpowiedź](_przebieg/0728-autor-dodatkow.md) · 10.3 s · $0.0773

### 0729 · weryfikator_dodatków · dział 07 · pytanie 38

- Wynik: odrzucone: 2; Marta opisuje funkcję i czeka na wynik: Powtarza motyw wcześniejszego wpisu „Marta czeka, aż plik sam zadziała”: zapisany plik, pusty ekran bez błędu, Marta uznaje, że coś zepsuła.; Poprawka w trzech miejscach z czterech: Powtarza motyw wpisu „Marta wpisuje kwotę w pięciu miejscach”: ta sama rzecz skopiowana w kilku miejscach, poprawka pominięta w jednej kopii.
- [prompt i odpowiedź](_przebieg/0729-weryfikator-dodatkow.md) · 9.2 s · $0.0721

### 0730 · pisarz · dział 07 · pytanie 39 · próba 1

- Kolejka TODO (22): 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51 …
- Wynik: „Po co dzielić program na funkcje”: 128 słów prozy, ```python 13 linii, ```text 2 linii; wątki: przykład dodaj suma_wydatkow, przykład dodaj udzial_na_osobe; warsztat: funkcje.py, $ python funkcje.py
- [prompt i odpowiedź](_przebieg/0730-pisarz.md) · 39.4 s · $0.1343

### 0731 · kontrola_deterministyczna · dział 07 · pytanie 39 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0732 · weryfikator_pojęć · dział 07 · pytanie 39 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (blokująca) **wydatek["kwota"]**: Kod używa słowników ({"kto": "Ania", "kwota": 120.5}) i odczytu wartości po kluczu, ale nie ma tego pojęcia w glosariuszu ani wyjaśnienia w tekście. Czytelnik nie wie, czym jest taki nawias klamrowy z nazwami i co robi wydatek["kwota"]. Potrzeba jednego zdania: słownik to zestaw podpisanych wartości, a wydatek["kwota"] wyciąga wartość podpisaną „kwota”. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **return**: wystarczy jedno zdanie; pełne omówienie w pytaniu 41. Przy pierwszym użyciu trzeba napisać, że return oddaje wynik funkcji temu, kto ją wywołał (dlatego print może wypisać wynik udzial_na_osobe). _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0732-weryfikator-pojec.md) · 11.0 s · $0.0279

### 0733 · znudzony_czytelnik · dział 07 · pytanie 39 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Wprowadzenie do przykładu i funkcja suma_wydatkow**: Tekst pisze, że sumę wydatków „wydzieliliśmy już do funkcji”. Ale poprzednia funkcja nazywała się `suma(wydatki)` i liczyła listę liczb. Tutaj jest `suma_wydatkow` i słowniki z kluczem `"kwota"`. Czytelnik może się zastanawiać, czy to ta sama funkcja. Wystarczy jedno zdanie, że to przerobiona wersja, która działa na wydatkach zapisanych jako słowniki. Można też zostać przy liście liczb. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0733-znudzony-czytelnik.md) · 11.6 s · $0.0253

### 0734 · strażnik_przykład · dział 07 · pytanie 39 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **funkcje.py**: Ostatni akapit mówi o pliku `funkcje.py`, którego nie ma w kanonie ani wśród zmian autora. Program „Wspólnej Kasy” jest w `wspolna_kasa/rozlicz.py`. Zmień na `rozlicz.py` albo zadeklaruj nowy plik z powodem. Zdanie „masz już … z jedną funkcją” też nie pasuje do kanonu, bo w `rozlicz.py` jest na razie tylko pętla z `suma`. Lepiej napisać, że sumę z pętli zamieniasz teraz w funkcję. _← strażnik_przykład_
  - `spójność` (sugestia) **suma_wydatkow**: Tekst mówi „Sumę wydatków wydzieliliśmy już do funkcji”, a `suma_wydatkow` jest w tej sekcji dodawana po raz pierwszy (kanon pokazuje tylko pętlę z `suma`). Przeformułuj, np. „Pętlę z `suma` zapisujemy jako funkcję `suma_wydatkow`”. _← strażnik_przykład_
  - `spójność` (sugestia) **mazury, tatry**: Zmienne `mazury` i `tatry` to nowe nazwy poza kanonem i nie zostały zadeklarowane. Zadeklaruj je jako „dodaj” albo zaznacz, że to dane przykładowe tylko do tej sekcji. Kanoniczna lista to `wydatki`, więc można też użyć jej dla jednego wyjazdu. Wpisy nie mają klucza `opis` z kanonu (`{"kto", "opis", "kwota"}`), co jest tylko drobną różnicą. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0734-straznik-przyklad.md) · 13.9 s · $0.0330

### 0735 · strażnik_warsztat · dział 07 · pytanie 39 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **Przykład kodu i wyniku w sekcji**: Kod w tekście sekcji nie zgadza się z krokami czytelnika. Sekcja używa funkcji `suma_wydatkow` i `udzial_na_osobe`, a plik czytelnika ma `suma` i `na_osobe`. Sekcja podaje wyjazdy jako listy słowników (`{"kto": ..., "kwota": ...}`, `wydatek["kwota"]`), a czytelnik ma zwykłe listy liczb (`[45.5, 20, 12.5]`). Słowniki nie zostały wcześniej wprowadzone. Wyniki też się różnią: sekcja podaje 100.0 i 150.0, a krok 2 wypisuje `Mazury: 26.0` i `Tatry: 112.5`. Popraw przykład w tekście tak, żeby był tym samym kodem co w kroku 1: `def suma(wydatki): ...`, `def na_osobe(suma, osoby): return suma / osoby`, `mazury = [45.5, 20, 12.5]`, `tatry = [300, 150]`, `print("Mazury:", na_osobe(suma(mazury), 3))`, `print("Tatry:", na_osobe(suma(tatry), 4))`. Blok wyniku ma wtedy brzmieć `Mazury: 26.0` i `Tatry: 112.5`. Wywołanie w zdaniu o czytelności zmień na `na_osobe(suma(mazury), 3)`. Nie wprowadzaj słowników. _← strażnik_warsztat_
  - `spójność` (sugestia) **Zdanie o drugiej funkcji**: Zdanie „Sumę wydatków wydzieliliśmy już do funkcji, a teraz dokładamy drugą, która z niej korzysta” jest prawdziwe tylko po zmianie przykładu na kod z kroku 1. Wtedy druga funkcja `na_osobe` dostaje wynik `suma(...)` jako argument. Nie wywołuje `suma` w środku, więc doprecyzuj: „druga dzieli wynik pierwszej”. _← strażnik_warsztat_
  - `spójność` (sugestia) **krok 1, def na_osobe**: W `na_osobe(suma, osoby)` parametr `suma` ma taką samą nazwę jak funkcja `suma`. Działa to poprawnie, bo wewnątrz `na_osobe` nazwa oznacza liczbę. Początkującego może to jednak zmylić. Rozważ nazwę parametru `razem` (`def na_osobe(razem, osoby): return razem / osoby`). _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0735-straznik-warsztat.md) · 16.9 s · $0.0366

### 0736 · weryfikator_odwołań · dział 07 · pytanie 39 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 5)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **wydatek["kwota"]**: W kodzie pojawia się `wydatek["kwota"]` i zapis w nawiasach klamrowych (słownik), których nie ma w glosariuszu ani w tej sekcji. Dodaj jedno zdanie, że każdy wydatek to zestaw opisanych pól (kto, kwota) i że `["kwota"]` pobiera kwotę. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **Wspólna Kasa**: „Wspólna Kasa” to przykład przewodni bez punktu zaczepienia; dodaj krótkie przypomnienie, czym jest (np. „program do rozliczania wspólnych wydatków z wyjazdów”). _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0736-weryfikator-odwolan.md) · 16.0 s · $0.0409

### 0737 · sprawdzacz_wyników · dział 07 · pytanie 39 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0737-sprawdzacz-wynikow.md) · 4.2 s · $0.0143

### 0738 · weryfikator_faktów · dział 07 · pytanie 39 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0738-weryfikator-faktow.md) · 5.4 s · $0.0281

### 0739 · decyzja · dział 07 · pytanie 39 · próba 1

- Potrzeby w kolejce przed krokiem (3):
  - `wyjaśnienie` (blokująca) **wydatek["kwota"]**: Kod używa słowników ({"kto": "Ania", "kwota": 120.5}) i odczytu wartości po kluczu, ale nie ma tego pojęcia w glosariuszu ani wyjaśnienia w tekście. Czytelnik nie wie, czym jest taki nawias klamrowy z nazwami i co robi wydatek["kwota"]. Potrzeba jednego zdania: słownik to zestaw podpisanych wartości, a wydatek["kwota"] wyciąga wartość podpisaną „kwota”. _← weryfikator_pojęć_
  - `spójność` (blokująca) **funkcje.py**: Ostatni akapit mówi o pliku `funkcje.py`, którego nie ma w kanonie ani wśród zmian autora. Program „Wspólnej Kasy” jest w `wspolna_kasa/rozlicz.py`. Zmień na `rozlicz.py` albo zadeklaruj nowy plik z powodem. Zdanie „masz już … z jedną funkcją” też nie pasuje do kanonu, bo w `rozlicz.py` jest na razie tylko pętla z `suma`. Lepiej napisać, że sumę z pętli zamieniasz teraz w funkcję. _← strażnik_przykład_
  - `spójność` (blokująca) **Przykład kodu i wyniku w sekcji**: Kod w tekście sekcji nie zgadza się z krokami czytelnika. Sekcja używa funkcji `suma_wydatkow` i `udzial_na_osobe`, a plik czytelnika ma `suma` i `na_osobe`. Sekcja podaje wyjazdy jako listy słowników (`{"kto": ..., "kwota": ...}`, `wydatek["kwota"]`), a czytelnik ma zwykłe listy liczb (`[45.5, 20, 12.5]`). Słowniki nie zostały wcześniej wprowadzone. Wyniki też się różnią: sekcja podaje 100.0 i 150.0, a krok 2 wypisuje `Mazury: 26.0` i `Tatry: 112.5`. Popraw przykład w tekście tak, żeby był tym samym kodem co w kroku 1: `def suma(wydatki): ...`, `def na_osobe(suma, osoby): return suma / osoby`, `mazury = [45.5, 20, 12.5]`, `tatry = [300, 150]`, `print("Mazury:", na_osobe(suma(mazury), 3))`, `print("Tatry:", na_osobe(suma(tatry), 4))`. Blok wyniku ma wtedy brzmieć `Mazury: 26.0` i `Tatry: 112.5`. Wywołanie w zdaniu o czytelności zmień na `na_osobe(suma(mazury), 3)`. Nie wprowadzaj słowników. _← strażnik_warsztat_
- Wynik: Do poprawy: 3 blokujących potrzeb wraca do pisarza; 8 sugestii trafia do raportu.
- 0.0 s

### 0740 · pisarz · dział 07 · pytanie 39 · próba 2

- Kolejka TODO (22): 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51 …
- Potrzeby w kolejce przed krokiem (3):
  - `wyjaśnienie` (blokująca) **wydatek["kwota"]**: Kod używa słowników ({"kto": "Ania", "kwota": 120.5}) i odczytu wartości po kluczu, ale nie ma tego pojęcia w glosariuszu ani wyjaśnienia w tekście. Czytelnik nie wie, czym jest taki nawias klamrowy z nazwami i co robi wydatek["kwota"]. Potrzeba jednego zdania: słownik to zestaw podpisanych wartości, a wydatek["kwota"] wyciąga wartość podpisaną „kwota”. _← weryfikator_pojęć_
  - `spójność` (blokująca) **funkcje.py**: Ostatni akapit mówi o pliku `funkcje.py`, którego nie ma w kanonie ani wśród zmian autora. Program „Wspólnej Kasy” jest w `wspolna_kasa/rozlicz.py`. Zmień na `rozlicz.py` albo zadeklaruj nowy plik z powodem. Zdanie „masz już … z jedną funkcją” też nie pasuje do kanonu, bo w `rozlicz.py` jest na razie tylko pętla z `suma`. Lepiej napisać, że sumę z pętli zamieniasz teraz w funkcję. _← strażnik_przykład_
  - `spójność` (blokująca) **Przykład kodu i wyniku w sekcji**: Kod w tekście sekcji nie zgadza się z krokami czytelnika. Sekcja używa funkcji `suma_wydatkow` i `udzial_na_osobe`, a plik czytelnika ma `suma` i `na_osobe`. Sekcja podaje wyjazdy jako listy słowników (`{"kto": ..., "kwota": ...}`, `wydatek["kwota"]`), a czytelnik ma zwykłe listy liczb (`[45.5, 20, 12.5]`). Słowniki nie zostały wcześniej wprowadzone. Wyniki też się różnią: sekcja podaje 100.0 i 150.0, a krok 2 wypisuje `Mazury: 26.0` i `Tatry: 112.5`. Popraw przykład w tekście tak, żeby był tym samym kodem co w kroku 1: `def suma(wydatki): ...`, `def na_osobe(suma, osoby): return suma / osoby`, `mazury = [45.5, 20, 12.5]`, `tatry = [300, 150]`, `print("Mazury:", na_osobe(suma(mazury), 3))`, `print("Tatry:", na_osobe(suma(tatry), 4))`. Blok wyniku ma wtedy brzmieć `Mazury: 26.0` i `Tatry: 112.5`. Wywołanie w zdaniu o czytelności zmień na `na_osobe(suma(mazury), 3)`. Nie wprowadzaj słowników. _← strażnik_warsztat_
- Wynik: „Po co dzielić program na funkcje”: 128 słów prozy, ```python 13 linii, ```text 2 linii; wątki: przykład dodaj suma, przykład dodaj na_osobe; warsztat: funkcje.py, $ python funkcje.py
- [prompt i odpowiedź](_przebieg/0740-pisarz.md) · 18.1 s · $0.0975

### 0741 · kontrola_deterministyczna · dział 07 · pytanie 39 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0742 · weryfikator_pojęć · dział 07 · pytanie 39 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **wydatek["kwota"]**: Kod używa słowników ({"kto": "Ania", "kwota": 120.5}) i odczytu wartości po kluczu, ale nie ma tego pojęcia w glosariuszu ani wyjaśnienia w tekście. Czytelnik nie wie, czym jest taki nawias klamrowy z nazwami i co robi wydatek["kwota"]. Potrzeba jednego zdania: słownik to zestaw podpisanych wartości, a wydatek["kwota"] wyciąga wartość podpisaną „kwota”. _← weryfikator_pojęć_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0742-weryfikator-pojec.md) · 3.5 s · $0.0222

### 0743 · znudzony_czytelnik · dział 07 · pytanie 39 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `konkret` (sugestia) **na_osobe(suma, osoby)**: W `na_osobe(suma, osoby)` parametr nazywa się tak samo jak funkcja `suma`. Początkujący może się zastanawiać, czy to ta sama rzecz i czy `suma(mazury)` jeszcze zadziała. Lepiej nazwać parametr np. `razem` albo `kwota`. _← znudzony_czytelnik_
  - `przykład` (sugestia) **Gdyby liczenie sumy trzeba było kiedyś zmienić**: Teza o „poprawce raz, nie w pięciu kopiach” nie jest pokazana w kontraście. Przykład pokazuje ponowne użycie, ale nie to, jak wyglądałby kod bez funkcji (pętla skopiowana dla Mazur i Tatr). Wystarczy jedno zdanie: „bez funkcji pętla stałaby dwa razy”. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0743-znudzony-czytelnik.md) · 9.4 s · $0.0236

### 0744 · strażnik_przykład · dział 07 · pytanie 39 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **funkcje.py**: Ostatni akapit mówi o pliku `funkcje.py`, którego nie ma w kanonie ani wśród zmian autora. Program „Wspólnej Kasy” jest w `wspolna_kasa/rozlicz.py`. Zmień na `rozlicz.py` albo zadeklaruj nowy plik z powodem. Zdanie „masz już … z jedną funkcją” też nie pasuje do kanonu, bo w `rozlicz.py` jest na razie tylko pętla z `suma`. Lepiej napisać, że sumę z pętli zamieniasz teraz w funkcję. _← strażnik_przykład_
- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 1.
- Nowe potrzeby (1):
  - `spójność` (blokująca, niespełniona) **funkcje.py**: Poprzednia uwaga nie została uwzględniona. Ostatni akapit nadal mówi: „U siebie masz już `funkcje.py` z funkcją `suma`”. Takiego pliku nie ma w kanonie ani wśród zmian autora. Program „Wspólnej Kasy” jest w `wspolna_kasa/rozlicz.py`. Kanon zna też tylko zmienną `suma` z pętli, a nie funkcję. Podobnie zdanie „Funkcja `suma` już jest” przeczy kanonowi. Popraw akapit, np.: „W `rozlicz.py` masz pętlę licząca `suma`. Zamieniasz ją teraz w funkcję `suma`, dopisujesz `na_osobe` i używasz obu dla dwóch wyjazdów.” Zmień też początek: zamiast „Funkcja `suma` już jest” napisz, że sumę z pętli zamieniamy w funkcję. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0744-straznik-przyklad.md) · 9.7 s · $0.0293

### 0745 · strażnik_warsztat · dział 07 · pytanie 39 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **Przykład kodu i wyniku w sekcji**: Kod w tekście sekcji nie zgadza się z krokami czytelnika. Sekcja używa funkcji `suma_wydatkow` i `udzial_na_osobe`, a plik czytelnika ma `suma` i `na_osobe`. Sekcja podaje wyjazdy jako listy słowników (`{"kto": ..., "kwota": ...}`, `wydatek["kwota"]`), a czytelnik ma zwykłe listy liczb (`[45.5, 20, 12.5]`). Słowniki nie zostały wcześniej wprowadzone. Wyniki też się różnią: sekcja podaje 100.0 i 150.0, a krok 2 wypisuje `Mazury: 26.0` i `Tatry: 112.5`. Popraw przykład w tekście tak, żeby był tym samym kodem co w kroku 1: `def suma(wydatki): ...`, `def na_osobe(suma, osoby): return suma / osoby`, `mazury = [45.5, 20, 12.5]`, `tatry = [300, 150]`, `print("Mazury:", na_osobe(suma(mazury), 3))`, `print("Tatry:", na_osobe(suma(tatry), 4))`. Blok wyniku ma wtedy brzmieć `Mazury: 26.0` i `Tatry: 112.5`. Wywołanie w zdaniu o czytelności zmień na `na_osobe(suma(mazury), 3)`. Nie wprowadzaj słowników. _← strażnik_warsztat_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0745-straznik-warsztat.md) · 5.1 s · $0.0257

### 0746 · weryfikator_odwołań · dział 07 · pytanie 39 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 4)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **na_osobe(suma, osoby)**: W `na_osobe(suma, osoby)` parametr nazywa się tak samo jak funkcja `suma`. Dla nowicjusza to mylące. Lepiej nazwać go `kwota_razem`. Warto też jednym zdaniem wyjaśnić, że `na_osobe(suma(mazury), 3)` najpierw liczy sumę, a jej wynik trafia do drugiej funkcji. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0746-weryfikator-odwolan.md) · 13.3 s · $0.0378

### 0747 · sprawdzacz_wyników · dział 07 · pytanie 39 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **na_osobe(suma, osoby)**: W funkcji `na_osobe(suma, osoby)` parametr nazywa się `suma`, tak samo jak funkcja `suma`. Wewnątrz `na_osobe` nazwa zasłania funkcję, a początkujący czytelnik może się pomylić. Lepiej nazwać parametr np. `kwota`. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0747-sprawdzacz-wynikow.md) · 6.0 s · $0.0160

### 0748 · weryfikator_faktów · dział 07 · pytanie 39 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **def na_osobe(suma, osoby)**: Parametr `suma` przesłania w funkcji globalną funkcję `suma`. Kod działa poprawnie, bo `na_osobe` nie wywołuje `suma`, ale początkujący może się pomylić. Warto rozważyć nazwę `razem` albo `kwota`. Zgodnie z dokumentacją Pythona nazwa lokalna (parametr) zasłania nazwę globalną w zakresie funkcji: https://docs.python.org/3/tutorial/controlflow.html#defining-functions _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0748-weryfikator-faktow.md) · 7.0 s · $0.0304

### 0749 · decyzja · dział 07 · pytanie 39 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca, niespełniona) **funkcje.py**: Poprzednia uwaga nie została uwzględniona. Ostatni akapit nadal mówi: „U siebie masz już `funkcje.py` z funkcją `suma`”. Takiego pliku nie ma w kanonie ani wśród zmian autora. Program „Wspólnej Kasy” jest w `wspolna_kasa/rozlicz.py`. Kanon zna też tylko zmienną `suma` z pętli, a nie funkcję. Podobnie zdanie „Funkcja `suma` już jest” przeczy kanonowi. Popraw akapit, np.: „W `rozlicz.py` masz pętlę licząca `suma`. Zamieniasz ją teraz w funkcję `suma`, dopisujesz `na_osobe` i używasz obu dla dwóch wyjazdów.” Zmień też początek: zamiast „Funkcja `suma` już jest” napisz, że sumę z pętli zamieniamy w funkcję. _← strażnik_przykład_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0750 · akceptacja · dział 07 · pytanie 39

- Wynik: Sekcja [sec-07-po-co-dzielic-program-na-funkcje] dopisana do działu 07; kanony: przykład:~suma przykład:+na_osobe; odwołania: wstecz „Funkcja `suma` już jest”, w przód „do czego wrócimy przy testowaniu programu”, wstecz „U siebie masz już `funkcje.py` z funkcją `suma`”, w przód „Za chwilę dopiszesz `na_osobe` i użyjesz obu”; punkty zaczepienia: dwa wyjazdy, jedna logika; w TODO zostało 22.
- 0.0 s

### 0751 · łowca_pułapek · dział 07 · pytanie 39

- Wynik: „Po co dzielić program na funkcje”: Parametr przesłania funkcję o tej samej nazwie
- [prompt i odpowiedź](_przebieg/0751-lowca-pulapek.md) · 6.3 s · $0.0196

### 0752 · autor_dodatków · dział 07 · pytanie 39

- Wynik: „Po co dzielić program na funkcje”: wtręty: Marta poprawia tylko jedną kopię, dykteryjki: Stawka rabatu w czterech skryptach
- [prompt i odpowiedź](_przebieg/0752-autor-dodatkow.md) · 12.5 s · $0.0800

### 0753 · weryfikator_dodatków · dział 07 · pytanie 39

- Wynik: odrzucone: 2; Marta poprawia tylko jedną kopię: Powtarza motyw wcześniejszego wtrętu „Marta wpisuje kwotę w pięciu miejscach” (poprawka wprowadzona tylko w części kopii, reszta zapomniana).; Stawka rabatu w czterech skryptach: Powtarza ten sam motyw poprawki w części kopii (trzy z czterech skryptów) co wcześniejszy wpis o kwocie wpisanej w pięciu miejscach i dubluje pierwszy dodatek.
- [prompt i odpowiedź](_przebieg/0753-weryfikator-dodatkow.md) · 10.1 s · $0.0734

### 0754 · pisarz · dział 07 · pytanie 40 · próba 1

- Kolejka TODO (21): 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52 …
- Wynik: „Czym są argumenty funkcji”: 142 słów prozy, ```python 5 linii, ```text 2 linii; nowe hasła: argument funkcji, parametr; warsztat: funkcje.py, $ python funkcje.py
- [prompt i odpowiedź](_przebieg/0754-pisarz.md) · 20.9 s · $0.0921

### 0755 · kontrola_deterministyczna · dział 07 · pytanie 40 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0756 · weryfikator_pojęć · dział 07 · pytanie 40 · próba 1

- Wynik: 1 blokujących, 1 sugestii. (eskalowano 1 powtarzających się braków do blokujących)
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **return**: wystarczy jedno zdanie; pełne omówienie w pytaniu 41. Przy pierwszym użyciu w kodzie warto dodać, że return oddaje wynik z funkcji miejscu, w którym ją wywołano, np. do print. _← weryfikator_pojęć_
  - `wyjaśnienie` (blokująca) **TypeError**: wystarczy jedno zdanie; pełne omówienie w pytaniu 51. Warto dopisać, że TypeError to nazwa komunikatu o błędzie, tu znaczy: funkcję wywołano w niewłaściwy sposób. [Eskalacja: zgłaszane już w sekcji „Działania matematyczne w programie”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0756-weryfikator-pojec.md) · 9.4 s · $0.0256

### 0757 · znudzony_czytelnik · dział 07 · pytanie 40 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0757-znudzony-czytelnik.md) · 4.7 s · $0.0181

### 0758 · strażnik_przykład · dział 07 · pytanie 40 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0758-straznik-przyklad.md) · 5.7 s · $0.0222

### 0759 · strażnik_warsztat · dział 07 · pytanie 40 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0759-straznik-warsztat.md) · 5.8 s · $0.0225

### 0760 · weryfikator_odwołań · dział 07 · pytanie 40 · próba 1

- Wynik: 0 blokujących, 3 sugestii. (odwołania: 1)
- Nowe potrzeby (3):
  - `odwołanie` (sugestia) **TypeError**: Błąd `TypeError` pojawia się bez wyjaśnienia. Wystarczy pół zdania, np. że to nazwa rodzaju błędu, a Python w komunikacie pisze, że brakuje argumentu. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **Funkcja bez argumentów robi zawsze to samo**: Zdanie o funkcji bez argumentów, która robi zawsze to samo, nie ma przykładu. Wystarczy krótki kontrast, np. funkcja wypisująca stały napis i `na_osobe` z różnymi liczbami. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **return suma / osoby**: `return` w przykładzie pojawia się bez komentarza. Można dodać zdanie, że `return` oddaje wynik, a szczegóły są w dalszej części tutoriala. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0760-weryfikator-odwolan.md) · 12.2 s · $0.0364

### 0761 · sprawdzacz_wyników · dział 07 · pytanie 40 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0761-sprawdzacz-wynikow.md) · 4.5 s · $0.0139

### 0762 · weryfikator_faktów · dział 07 · pytanie 40 · próba 1

- Wynik: Brak uwag. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0762-weryfikator-faktow.md) · 15.6 s · $0.0643

### 0763 · decyzja · dział 07 · pytanie 40 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **TypeError**: wystarczy jedno zdanie; pełne omówienie w pytaniu 51. Warto dopisać, że TypeError to nazwa komunikatu o błędzie, tu znaczy: funkcję wywołano w niewłaściwy sposób. [Eskalacja: zgłaszane już w sekcji „Działania matematyczne w programie”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 4 sugestii trafia do raportu.
- 0.0 s

### 0764 · pisarz · dział 07 · pytanie 40 · próba 2

- Kolejka TODO (21): 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52 …
- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **TypeError**: wystarczy jedno zdanie; pełne omówienie w pytaniu 51. Warto dopisać, że TypeError to nazwa komunikatu o błędzie, tu znaczy: funkcję wywołano w niewłaściwy sposób. [Eskalacja: zgłaszane już w sekcji „Działania matematyczne w programie”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: „Czym są argumenty funkcji”: 172 słów prozy, ```python 5 linii, ```text 2 linii; nowe hasła: argument funkcji, parametr, TypeError; warsztat: funkcje.py, $ python funkcje.py (błąd)
- [prompt i odpowiedź](_przebieg/0764-pisarz.md) · 21.9 s · $0.1011

### 0765 · kontrola_deterministyczna · dział 07 · pytanie 40 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0766 · weryfikator_pojęć · dział 07 · pytanie 40 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wyjaśnienie` (blokująca) **TypeError**: wystarczy jedno zdanie; pełne omówienie w pytaniu 51. Warto dopisać, że TypeError to nazwa komunikatu o błędzie, tu znaczy: funkcję wywołano w niewłaściwy sposób. [Eskalacja: zgłaszane już w sekcji „Działania matematyczne w programie”; dodaj hasło do new_terms.] _← weryfikator_pojęć_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0766-weryfikator-pojec.md) · 2.8 s · $0.0212

### 0767 · znudzony_czytelnik · dział 07 · pytanie 40 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0767-znudzony-czytelnik.md) · 5.3 s · $0.0192

### 0768 · strażnik_przykład · dział 07 · pytanie 40 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **na_osobe(suma, osoby)**: Kod zgadza się z kanonem (nazwa, parametry, wynik). Drobna uwaga: w kanonie `osoby` to lista tekstów, a w `na_osobe` ten sam identyfikator jest liczbą (dzielnikiem). Warto jednym zdaniem zaznaczyć, że parametr to tylko nazwa lokalna, niezwiązana ze zmienną `osoby`, albo pokazać wywołanie `na_osobe(300, liczba_osob)` z kanonicznym `liczba_osob = 3`. _← strażnik_przykład_
  - `spójność` (sugestia) **U siebie zobaczysz TypeError za chwilę w funkcje.py**: Zdanie jest niejasne i nie pasuje do sekcji: `funkcje.py` nie zawiera wywołania `na_osobe(300)`, a „za chwilę” nie wskazuje miejsca. Usuń je albo zastąp poleceniem: „Dopisz na końcu funkcje.py wywołanie na_osobe(300) i uruchom plik”. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0768-straznik-przyklad.md) · 12.1 s · $0.0300

### 0769 · strażnik_warsztat · dział 07 · pytanie 40 · próba 2

- Wynik: 1 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `wynik` (blokująca) **krok 2, traceback, linia 'File "funkcje.py", line 16'**: Numer linii w tracebacku jest błędny. Po dopisaniu `print(na_osobe(300))` ten wiersz jest w pliku piętnasty (1 komentarz, 2-6 suma, 7 pusta, 8-9 na_osobe, 10 pusta, 11 mazury, 12 tatry, 13 print Mazury, 14 print Tatry, 15 nowa linia). Popraw na: `  File "funkcje.py", line 15, in <module>`. Reszta wyniku (Mazury: 26.0, Tatry: 112.5, ~~~~~~~~^^^^^, treść TypeError) jest zgodna z Pythonem 3.13. _← strażnik_warsztat_
  - `wynik` (sugestia) **krok 2, ścieżka w tracebacku**: Od Pythona 3.9 traceback pokazuje pełną, bezwzględną ścieżkę skryptu (np. /home/ania/wspolna_kasa/funkcje.py albo C:\Users\ania\wspolna_kasa\funkcje.py), a nie samo `funkcje.py`. Dodaj jedno zdanie, że ścieżka u czytelnika będzie inna (jego katalog), a liczy się numer linii i ostatnia linia z TypeError. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0769-straznik-warsztat.md) · 15.6 s · $0.0343

### 0770 · weryfikator_odwołań · dział 07 · pytanie 40 · próba 2

- Wynik: 1 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 3)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`**: Zdanie „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” zapowiada plik i ćwiczenie, których nigdzie nie wprowadzono i które nie wynikają z tej sekcji. Usuń zdanie albo wyjaśnij na miejscu: pokaż krótki kod z wywołaniem `na_osobe(300)` i jego wynik, bez odsyłania do pliku. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **na_osobe(300) i TypeError**: Błąd `TypeError` jest opisany, ale nie pokazano, jak wygląda komunikat po `na_osobe(300)`. Warto dodać blok `text` z krótkim komunikatem (np. brakujący argument `osoby`), by czytelnik rozpoznał go u siebie. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **na_osobe(4, 300)**: Zły wynik `na_osobe(4, 300)` jest tylko opisany. Można podać wartość (ok. 0.0133), by pokazać, że program działa bez błędu, ale liczy źle. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0770-weryfikator-odwolan.md) · 15.7 s · $0.0413

### 0771 · sprawdzacz_wyników · dział 07 · pytanie 40 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `wynik` (sugestia) **funkcje.py**: Zdanie „U siebie zobaczysz TypeError za chwilę w funkcje.py” odsyła do pliku, którego czytelnik nie zna z tej sekcji. Warto wskazać, gdzie i jak go uruchomi, albo zdanie usunąć. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **na_osobe(300) i na_osobe(4, 300)**: Warto pokazać, jak wygląda komunikat TypeError dla na_osobe(300), oraz wynik na_osobe(4, 300), czyli 0.013333333333333334. Wtedy „zły wynik” byłby widoczny. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0771-sprawdzacz-wynikow.md) · 8.3 s · $0.0187

### 0772 · weryfikator_faktów · dział 07 · pytanie 40 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0772-weryfikator-faktow.md) · 6.5 s · $0.0292

### 0773 · decyzja · dział 07 · pytanie 40 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `wynik` (blokująca) **krok 2, traceback, linia 'File "funkcje.py", line 16'**: Numer linii w tracebacku jest błędny. Po dopisaniu `print(na_osobe(300))` ten wiersz jest w pliku piętnasty (1 komentarz, 2-6 suma, 7 pusta, 8-9 na_osobe, 10 pusta, 11 mazury, 12 tatry, 13 print Mazury, 14 print Tatry, 15 nowa linia). Popraw na: `  File "funkcje.py", line 15, in <module>`. Reszta wyniku (Mazury: 26.0, Tatry: 112.5, ~~~~~~~~^^^^^, treść TypeError) jest zgodna z Pythonem 3.13. _← strażnik_warsztat_
  - `odwołanie` (blokująca) **U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`**: Zdanie „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” zapowiada plik i ćwiczenie, których nigdzie nie wprowadzono i które nie wynikają z tej sekcji. Usuń zdanie albo wyjaśnij na miejscu: pokaż krótki kod z wywołaniem `na_osobe(300)` i jego wynik, bez odsyłania do pliku. _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 2 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0774 · akceptacja · dział 07 · pytanie 40

- Wynik: Sekcja [sec-07-czym-sa-argumenty-funkcji] dopisana do działu 07; hasła w glosariuszu: argument funkcji, parametr, TypeError; odwołania: w przód „Czytanie takich komunikatów omówimy przy błędach”, wstecz „tak samo jak przy przypisaniu”, w przód „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`”; punkty zaczepienia: argumenty po nazwie, zamieniona kolejność; w TODO zostało 21.
- 0.0 s

### 0775 · łowca_pułapek · dział 07 · pytanie 40

- Wynik: „Czym są argumenty funkcji”: brak pułapek
- [prompt i odpowiedź](_przebieg/0775-lowca-pulapek.md) · 3.1 s · $0.0170

### 0776 · autor_dodatków · dział 07 · pytanie 40

- Wynik: „Czym są argumenty funkcji”: dowcipy: Formularz nie zna Twojego nazwiska
- [prompt i odpowiedź](_przebieg/0776-autor-dodatkow.md) · 10.7 s · $0.0776

### 0777 · weryfikator_dodatków · dział 07 · pytanie 40

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0777-weryfikator-dodatkow.md) · 5.6 s · $0.0674

### 0778 · pisarz · dział 07 · pytanie 41 · próba 1

- Kolejka TODO (20): 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53 …
- Wynik: „Zwracanie wyniku przez funkcję”: 132 słów prozy, ```python 10 linii, ```text 3 linii; nowe hasła: return (zwracanie wyniku), None; warsztat: funkcje.py, $ python funkcje.py
- [prompt i odpowiedź](_przebieg/0778-pisarz.md) · 22.2 s · $0.0969

### 0779 · kontrola_deterministyczna · dział 07 · pytanie 41 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0780 · weryfikator_pojęć · dział 07 · pytanie 41 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0780-weryfikator-pojec.md) · 5.0 s · $0.0211

### 0781 · znudzony_czytelnik · dział 07 · pytanie 41 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **na_osobe(suma(mazury), 3)**: Ostatnie zdanie używa `na_osobe(suma(mazury), 3)`. Funkcja `suma` i zmienna `mazury` nie pojawiają się w tej sekcji ani w poprzedniej. Czytelnik nie wie, czym są, więc jedyny przykład łączenia funkcji nie jest do sprawdzenia. Lepiej użyć wywołania, które da się zrozumieć od razu, np. `na_osobe(na_osobe(300, 4), 3)`, albo `wynik = na_osobe(300, 4)`. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0781-znudzony-czytelnik.md) · 9.7 s · $0.0228

### 0782 · strażnik_przykład · dział 07 · pytanie 41 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **wypisz_na_osobe**: Nowa funkcja pojawia się w kodzie bez deklaracji w canon_changes (module="przykład", „dodaj”, pełna deklaracja: funkcja, plik, argumenty suma i osoby, brak return). Zadeklaruj ją albo zrób z niej kontrprzykład i oznacz pierwszą linią bloku „# poza kanonem”. Zmienne a i b są tu tylko przykładem, ale też warto je nazwać jako lokalne dla ilustracji. _← strażnik_przykład_
  - `spójność` (sugestia) **mazury**: W ostatnim zdaniu `suma(mazury)` używa nazwy spoza kanonu, niezdefiniowanej i sugerującej obcą dziedzinę (wyjazd). Zastąp ją kanonicznym `wydatki` albo listą kwot, tak by pasowało do `suma(wydatki)` z kanonu. Lepiej pokazać to też w kodzie, nie tylko w prozie. _← strażnik_przykład_
  - `spójność` (sugestia) **na_osobe**: Przykład używa 300 i 4, a wątek ma 300 / 3 i liczba_osob = 3. Rozważ `na_osobe(300, 3)` (wynik 100.0) lub przekazanie `liczba_osob`, by trzymać się Wspólnej Kasy. Dział zapowiada też suma_wydatkow i udzial_na_osobe; można zaznaczyć, że to kolejny krok. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0782-straznik-przyklad.md) · 14.1 s · $0.0306

### 0783 · strażnik_warsztat · dział 07 · pytanie 41 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **akapit o `return` kończącym funkcję**: Zdanie, że po `return` funkcja od razu kończy pracę i nic pod nim się nie wykona, nie ma przykładu. Można dodać krótki kod, np. funkcję z `return 1` i `print("tu nie dojdziemy")` pod spodem, i pokazać, że napis się nie wypisze. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0783-straznik-warsztat.md) · 10.1 s · $0.0278

### 0784 · weryfikator_odwołań · dział 07 · pytanie 41 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 1)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **Po return funkcja od razu kończy pracę**: Zdanie „Po `return` funkcja od razu kończy pracę” nie ma przykładu. Wystarczy dwulinijkowy kod, w którym `print` pod `return` się nie wykonuje. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **na_osobe(suma(mazury), 3)**: Przykład końcowy używa `suma(mazury)`, ale `suma` i `mazury` nie są w tej sekcji zdefiniowane. Czytelnik może ich nie pamiętać. Lepiej dodać krótkie przypomnienie („funkcja `suma` z wcześniejszego przykładu sumuje wydatki”) albo pokazać definicję. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0784-weryfikator-odwolan.md) · 11.8 s · $0.0367

### 0785 · sprawdzacz_wyników · dział 07 · pytanie 41 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0785-sprawdzacz-wynikow.md) · 4.8 s · $0.0146

### 0786 · weryfikator_faktów · dział 07 · pytanie 41 · próba 1

- Wynik: Brak uwag. (źródła: 2)
- [prompt i odpowiedź](_przebieg/0786-weryfikator-faktow.md) · 13.5 s · $0.0660

### 0787 · decyzja · dział 07 · pytanie 41 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **wypisz_na_osobe**: Nowa funkcja pojawia się w kodzie bez deklaracji w canon_changes (module="przykład", „dodaj”, pełna deklaracja: funkcja, plik, argumenty suma i osoby, brak return). Zadeklaruj ją albo zrób z niej kontrprzykład i oznacz pierwszą linią bloku „# poza kanonem”. Zmienne a i b są tu tylko przykładem, ale też warto je nazwać jako lokalne dla ilustracji. _← strażnik_przykład_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 6 sugestii trafia do raportu.
- 0.0 s

### 0788 · pisarz · dział 07 · pytanie 41 · próba 2

- Kolejka TODO (20): 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53 …
- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **wypisz_na_osobe**: Nowa funkcja pojawia się w kodzie bez deklaracji w canon_changes (module="przykład", „dodaj”, pełna deklaracja: funkcja, plik, argumenty suma i osoby, brak return). Zadeklaruj ją albo zrób z niej kontrprzykład i oznacz pierwszą linią bloku „# poza kanonem”. Zmienne a i b są tu tylko przykładem, ale też warto je nazwać jako lokalne dla ilustracji. _← strażnik_przykład_
- Wynik: „Zwracanie wyniku przez funkcję”: 145 słów prozy, ```python 10 linii, ```text 3 linii; nowe hasła: wartość zwracana, None; wątki: przykład dodaj wypisz_na_osobe
- [prompt i odpowiedź](_przebieg/0788-pisarz.md) · 17.4 s · $0.0954

### 0789 · kontrola_deterministyczna · dział 07 · pytanie 41 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0790 · weryfikator_pojęć · dział 07 · pytanie 41 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **ciele funkcji**: Pojęcie „ciało funkcji” nie ma hasła w glosariuszu ani wyjaśnienia w tekście. Wystarczy krótkie dopowiedzenie, że to wcięte linijki pod linią z `def`. Czytelnik pewnie się domyśli z kontekstu, więc to tylko sugestia. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0790-weryfikator-pojec.md) · 6.9 s · $0.0241

### 0791 · znudzony_czytelnik · dział 07 · pytanie 41 · próba 2

- Wynik: 1 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `konkret` (blokująca) **na_osobe(suma(mazury), 3)**: Jedyny przykład użycia zwróconej wartości „dalej” opiera się na czymś, czego czytelnik nie zna: `suma(mazury)` to nieznana funkcja i nieznana zmienna. Do tego `suma` było dotąd nazwą parametru, więc łatwo o pomyłkę. Zamień to na wywołanie złożone z funkcji już pokazanych, np. `print(na_osobe(300, 4) * 2)` albo `na_osobe(na_osobe(600, 2), 3)`, i dopisz jedno zdanie, ile wyjdzie. _← znudzony_czytelnik_
  - `skrócenie` (sugestia) **Po return funkcja od razu kończy pracę**: Teza o natychmiastowym końcu funkcji po `return` nie ma żadnego przykładu, a kod jej nie pokazuje. Jeśli zostanie miejsce, usuń zdanie „Nazwy wynik i nic służą tylko tej ilustracji” i dodaj w bloku kodu jedną linię `print` pod `return`, żeby było widać, że się nie wypisze. Jeśli nie ma miejsca, zostaw samo zdanie. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0791-znudzony-czytelnik.md) · 12.7 s · $0.0265

### 0792 · strażnik_przykład · dział 07 · pytanie 41 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **wypisz_na_osobe**: Nowa funkcja pojawia się w kodzie bez deklaracji w canon_changes (module="przykład", „dodaj”, pełna deklaracja: funkcja, plik, argumenty suma i osoby, brak return). Zadeklaruj ją albo zrób z niej kontrprzykład i oznacz pierwszą linią bloku „# poza kanonem”. Zmienne a i b są tu tylko przykładem, ale też warto je nazwać jako lokalne dla ilustracji. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0792-straznik-przyklad.md) · 6.2 s · $0.0255

### 0793 · weryfikator_odwołań · dział 07 · pytanie 41 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **na_osobe(suma(mazury), 3)**: Ostatni przykład używa `suma(mazury)` bez przypomnienia, czym jest `mazury` i co robi `suma`. Dodaj jedno zdanie (np. „`suma` dodaje wydatki z listy `mazury`”) albo pokaż to w kodzie. Dodatkowo `suma` jest tu też nazwą parametru w `na_osobe`, co może mylić. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0793-weryfikator-odwolan.md) · 11.4 s · $0.0362

### 0794 · sprawdzacz_wyników · dział 07 · pytanie 41 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **na_osobe(suma(mazury), 3)**: Przykład `na_osobe(suma(mazury), 3)` używa `suma` i `mazury`, które nie są zdefiniowane w tej sekcji. Czytelnik może nie wiedzieć, skąd się wzięły. Warto przypomnieć, że to funkcja i zmienna z wcześniejszego działu, albo podać krótki samodzielny przykład. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0794-sprawdzacz-wynikow.md) · 6.3 s · $0.0168

### 0795 · weryfikator_faktów · dział 07 · pytanie 41 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0795-weryfikator-faktow.md) · 5.9 s · $0.0285

### 0796 · decyzja · dział 07 · pytanie 41 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `konkret` (blokująca) **na_osobe(suma(mazury), 3)**: Jedyny przykład użycia zwróconej wartości „dalej” opiera się na czymś, czego czytelnik nie zna: `suma(mazury)` to nieznana funkcja i nieznana zmienna. Do tego `suma` było dotąd nazwą parametru, więc łatwo o pomyłkę. Zamień to na wywołanie złożone z funkcji już pokazanych, np. `print(na_osobe(300, 4) * 2)` albo `na_osobe(na_osobe(600, 2), 3)`, i dopisz jedno zdanie, ile wyjdzie. _← znudzony_czytelnik_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0797 · akceptacja · dział 07 · pytanie 41

- Wynik: Sekcja [sec-07-zwracanie-wyniku-przez-funkcje] dopisana do działu 07; hasła w glosariuszu: None, wartość zwracana; kanony: przykład:+wypisz_na_osobe; odwołania: wstecz „na_osobe(suma(mazury), 3)”; punkty zaczepienia: wypisanie kontra zwrócenie; w TODO zostało 20.
- 0.0 s

### 0798 · łowca_pułapek · dział 07 · pytanie 41

- Wynik: „Zwracanie wyniku przez funkcję”: brak pułapek
- [prompt i odpowiedź](_przebieg/0798-lowca-pulapek.md) · 2.3 s · $0.0156

### 0799 · autor_dodatków · dział 07 · pytanie 41

- Wynik: „Zwracanie wyniku przez funkcję”: wtręty: Marta dostaje z funkcji „nic”, dykteryjki: Raport z wartością None
- [prompt i odpowiedź](_przebieg/0799-autor-dodatkow.md) · 11.5 s · $0.0798

### 0800 · weryfikator_dodatków · dział 07 · pytanie 41

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0800-weryfikator-dodatkow.md) · 8.3 s · $0.0722

### 0801 · pisarz · dział 07 · pytanie 42 · próba 1

- Kolejka TODO (19): 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54 …
- Wynik: „Czytelne nazwy zmiennych i funkcji”: 152 słów prozy, ```python 10 linii, ```text 1 linii; wątki: przykład dodaj suma_wydatkow, przykład dodaj udzial_na_osobe
- [prompt i odpowiedź](_przebieg/0801-pisarz.md) · 25.4 s · $0.0997

### 0802 · kontrola_deterministyczna · dział 07 · pytanie 42 · próba 1

- Wynik: 2 problemów wykrytych bez modelu.
- Nowe potrzeby (2):
  - `wyjaśnienie` (blokująca) **sec-07-czym-sa-argumenty-funkcji**: Oznaczenie [[sec-07-czym-sa-argumenty-funkcji]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `wyjaśnienie` (blokująca) **sec-07-po-co-dzielic-program-na-funkcje**: Oznaczenie [[sec-07-po-co-dzielic-program-na-funkcje]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 0803 · weryfikator_pojęć · dział 07 · pytanie 42 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **ponowne użycie kodu**: wystarczy jedno zdanie; pełne omówienie w pytaniu 43. Tekst tylko zapowiada „ponowne użycie kodu” bez powiedzenia, co to znaczy (np. że raz napisaną funkcję wywołuje się w wielu miejscach zamiast pisać ją od nowa). _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0803-weryfikator-pojec.md) · 7.0 s · $0.0252

### 0804 · znudzony_czytelnik · dział 07 · pytanie 42 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0804-znudzony-czytelnik.md) · 5.5 s · $0.0203

### 0805 · strażnik_przykład · dział 07 · pytanie 42 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **suma_wydatkow(wydatki)**: W kanonie `wydatki` to lista słowników ({"kto", "opis", "kwota"}), a tu parametr `wydatki` dostaje listę samych liczb ([45.5, 20, 12.5]). Czytelnik może spróbować przekazać kanoniczną `wydatki` i dostać błąd. Popraw: nazwij parametr `kwoty` albo dodaj zdanie, że funkcja bierze listę kwot, nie listę słowników. Ta sama uwaga dotyczy nazwy `kwoty_wydatkow` w tabeli, której nie ma w kanonie. _← strażnik_przykład_
  - `spójność` (sugestia) **udzial_na_osobe(suma, liczba_osob)**: Parametr `suma` ma tę samą nazwę co element kanonu `suma` (funkcja z funkcje.py). Jest to zgodne z kanonowym `na_osobe(suma, osoby)`, więc to tylko drobna różnica. Warto dodać jedno zdanie, że `udzial_na_osobe` i `suma_wydatkow` to nowe, czytelniejsze nazwy dawnych `na_osobe` i `suma`, żeby czytelnik nie szukał dwóch wersji. _← strażnik_przykład_
  - `spójność` (sugestia) **f(300, 4)**: Liczby 300 i 4 nie pasują do dalszego przykładu (45.5, 20, 12.5 i 3 osoby). Lepiej użyć `f(78, 3)`, żeby wątek był ciągły. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0805-straznik-przyklad.md) · 12.2 s · $0.0328

### 0806 · weryfikator_odwołań · dział 07 · pytanie 42 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 3)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **f(300, 4) i udzial_na_osobe**: Zdanie „Nazwa udzial_na_osobe mówi to od razu” jest lekkim nadmiarem: sama nazwa funkcji nie mówi, która liczba jest sumą, a która liczbą osób. Warto dodać wywołanie z nazwami (np. udzial_na_osobe(suma=300, liczba_osob=4)) albo doprecyzować, że nazwy parametrów podpowiadają kolejność. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0806-weryfikator-odwolan.md) · 11.9 s · $0.0406

### 0807 · sprawdzacz_wyników · dział 07 · pytanie 42 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0807-sprawdzacz-wynikow.md) · 3.9 s · $0.0145

### 0808 · weryfikator_faktów · dział 07 · pytanie 42 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0808-weryfikator-faktow.md) · 5.1 s · $0.0284

### 0809 · decyzja · dział 07 · pytanie 42 · próba 1

- Potrzeby w kolejce przed krokiem (2):
  - `wyjaśnienie` (blokująca) **sec-07-czym-sa-argumenty-funkcji**: Oznaczenie [[sec-07-czym-sa-argumenty-funkcji]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `wyjaśnienie` (blokująca) **sec-07-po-co-dzielic-program-na-funkcje**: Oznaczenie [[sec-07-po-co-dzielic-program-na-funkcje]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- Wynik: Do poprawy: 2 blokujących potrzeb wraca do pisarza; 5 sugestii trafia do raportu.
- 0.0 s

### 0810 · pisarz · dział 07 · pytanie 42 · próba 2

- Kolejka TODO (19): 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54 …
- Potrzeby w kolejce przed krokiem (2):
  - `wyjaśnienie` (blokująca) **sec-07-czym-sa-argumenty-funkcji**: Oznaczenie [[sec-07-czym-sa-argumenty-funkcji]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `wyjaśnienie` (blokująca) **sec-07-po-co-dzielic-program-na-funkcje**: Oznaczenie [[sec-07-po-co-dzielic-program-na-funkcje]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- Wynik: „Czytelne nazwy zmiennych i funkcji”: 152 słów prozy, ```python 10 linii, ```text 1 linii; wątki: przykład dodaj suma_wydatkow, przykład dodaj udzial_na_osobe
- [prompt i odpowiedź](_przebieg/0810-pisarz.md) · 26.4 s · $0.1290

### 0811 · kontrola_deterministyczna · dział 07 · pytanie 42 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0812 · weryfikator_pojęć · dział 07 · pytanie 42 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0812-weryfikator-pojec.md) · 4.6 s · $0.0217

### 0813 · znudzony_czytelnik · dział 07 · pytanie 42 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `tempo` (sugestia) **suma_wydatkow (drugi blok kodu)**: Drugi blok kodu wprowadza pętlę `for` i akumulator `razem`, choć sekcja jest o nazwach. Jeśli pętla nie była wcześniej omówiona, czytelnik gubi wątek. Można skrócić funkcję do jednej linii, np. `return sum(wydatki)`, albo zostawić tylko `udzial_na_osobe`. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0813-znudzony-czytelnik.md) · 7.6 s · $0.0222

### 0814 · strażnik_przykład · dział 07 · pytanie 42 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **suma_wydatkow(wydatki)**: W kanonie zmienna `wydatki` to lista słowników (`{"kto", "opis", "kwota"}`), a `suma_wydatkow(wydatki)` dodaje elementy jak liczby i wywołanie dostaje listę liczb `[45.5, 20, 12.5]`. Dla kanonicznej `wydatki` kod by się wywalił. Zmień nazwę parametru na `kwoty` (zgodnie z tabelą z `kwoty_wydatkow`) albo dodaj zdanie, że funkcja dostaje listę samych kwot. _← strażnik_przykład_
  - `spójność` (sugestia) **suma / na_osobe**: Kanon ma już `suma` i `na_osobe` w funkcje.py. Nowe `suma_wydatkow` i `udzial_na_osobe` są ich zamiennikami pod czytelniejszymi nazwami. Napisz jednym zdaniem, że to zmiana nazw (`suma` na `suma_wydatkow`, `na_osobe` na `udzial_na_osobe`), żeby czytelnik nie szukał dwóch wersji. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0814-straznik-przyklad.md) · 11.0 s · $0.0304

### 0815 · weryfikator_odwołań · dział 07 · pytanie 42 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0815-weryfikator-odwolan.md) · 9.0 s · $0.0370

### 0816 · sprawdzacz_wyników · dział 07 · pytanie 42 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0816-sprawdzacz-wynikow.md) · 4.0 s · $0.0144

### 0817 · weryfikator_faktów · dział 07 · pytanie 42 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0817-weryfikator-faktow.md) · 5.2 s · $0.0285

### 0818 · decyzja · dział 07 · pytanie 42 · próba 2

- Wynik: Sekcja przyjęta; 3 sugestii trafia do raportu.
- 0.0 s

### 0819 · akceptacja · dział 07 · pytanie 42

- Wynik: Sekcja [sec-07-czytelne-nazwy-zmiennych-i-funkcji] dopisana do działu 07; kanony: przykład:+suma_wydatkow przykład:+udzial_na_osobe; odwołania: wstecz „To ryzyko z zamienioną kolejnością, które znasz z argumentów funkcji”, wstecz „przy dzieleniu programu na funkcje”, w przód „przy ponownym użyciu kodu, które omówimy za chwilę”; punkty zaczepienia: zdanie w kodzie; w TODO zostało 19.
- 0.0 s

### 0820 · łowca_pułapek · dział 07 · pytanie 42

- Wynik: „Czytelne nazwy zmiennych i funkcji”: brak pułapek
- [prompt i odpowiedź](_przebieg/0820-lowca-pulapek.md) · 2.2 s · $0.0159

### 0821 · autor_dodatków · dział 07 · pytanie 42

- Wynik: „Czytelne nazwy zmiennych i funkcji”: rysunki: Klucze z oznaczeniami, dowcipy: Dane numer dwa
- [prompt i odpowiedź](_przebieg/0821-autor-dodatkow.md) · 16.9 s · $0.0854

### 0822 · weryfikator_dodatków · dział 07 · pytanie 42

- Wynik: odrzucone: 2; Klucze z oznaczeniami: Motyw podpisanych zawieszek/etykiet na przedmiotach (jedna bez opisu) powtarza wcześniejszy rysunek „Dwa pudełka, dwie etykiety”, który już ilustrował nazwy zmiennych jako etykiety.; Dane numer dwa: Powtarza temat wcześniejszej dykteryjki „Zmienna o nazwie x” (x, x2, tmp, nikt nie wie, czym się różnią) i tylko przepisuje przykład `dane2` z tabeli sekcji, nie dodając nowej puenty.
- [prompt i odpowiedź](_przebieg/0822-weryfikator-dodatkow.md) · 9.6 s · $0.0759

### 0823 · pisarz · dział 07 · pytanie 43 · próba 1

- Kolejka TODO (18): 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55 …
- Wynik: „Ponowne użycie kodu”: 129 słów prozy, ```python 13 linii, ```text 2 linii; warsztat: funkcje.py, $ python funkcje.py
- [prompt i odpowiedź](_przebieg/0823-pisarz.md) · 17.8 s · $0.0951

### 0824 · kontrola_deterministyczna · dział 07 · pytanie 43 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0825 · weryfikator_pojęć · dział 07 · pytanie 43 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0825-weryfikator-pojec.md) · 6.8 s · $0.0232

### 0826 · znudzony_czytelnik · dział 07 · pytanie 43 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `skrócenie` (sugestia) **ostatni akapit (funkcje.py, celowy błąd)**: Ostatni akapit odwołuje się do pliku `funkcje.py` i „celowego błędu”, o których w tej sekcji nie było mowy. Czytelnik nie wie, o jaki błąd chodzi ani gdzie go szukać. Usuń akapit albo powiedz jednym zdaniem, jaki to błąd. Zwolnione miejsce wystarczy na resztę tekstu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0826-znudzony-czytelnik.md) · 9.3 s · $0.0229

### 0827 · strażnik_przykład · dział 07 · pytanie 43 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `spójność` (blokująca) **funkcje.py / suma_wydatkow**: Zdanie „U siebie w `funkcje.py` masz to już gotowe, tylko z celowym błędem na końcu. Poprawiamy go poniżej” przeczy kanonowi. Pokazana czytelnikowi `suma_wydatkow` w `funkcje.py` jest poprawna: `return razem` stoi po pętli, a `udzial_na_osobe` też nie ma błędu. Poza tym w sekcji nie ma nic „poniżej”, co by coś poprawiało. Czytelnik będzie szukał nieistniejącego błędu. Usuń to zdanie albo zastąp je zgodnym z kanonem, np. „To te same funkcje, które masz w `funkcje.py`”. _← strażnik_przykład_
  - `spójność` (sugestia) **mazury, tatry**: Nowe zmienne `mazury` i `tatry` (listy liczb) nie są w kanonie ani w canon_changes. Zadeklaruj je jako „dodaj” w module „przykład”. Warto też zaznaczyć w tekście, że to uproszczone listy samych kwot, a nie lista słowników `wydatki` z kanonu. Tak samo działa `suma_wydatkow` w kanonie, więc kod jest poprawny. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0827-straznik-przyklad.md) · 14.0 s · $0.0334

### 0828 · strażnik_warsztat · dział 07 · pytanie 43 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Ostatni akapit sekcji / przykład kodu**: Tekst sekcji używa nazw suma_wydatkow i udzial_na_osobe oraz wypisuje same liczby (26.0, 112.5). W funkcje.py funkcje nazywają się suma i na_osobe, a print dodaje etykiety (Mazury:, Tatry:). Zdanie „U siebie w funkcje.py masz to już gotowe” jest więc tylko z grubsza prawdziwe. Popraw je na: „U siebie w funkcje.py masz tę samą logikę, tylko funkcje nazywają się suma i na_osobe, a wyniki są opisane etykietami Mazury: i Tatry:.” Można też zmienić kod w sekcji na nazwy suma i na_osobe. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0828-straznik-warsztat.md) · 10.7 s · $0.0283

### 0829 · weryfikator_odwołań · dział 07 · pytanie 43 · próba 1

- Wynik: 2 blokujących, 0 sugestii. (odwołania: 3)
- Nowe potrzeby (2):
  - `odwołanie` (blokująca) **Poprawiamy go poniżej.**: Zapowiedź „poniżej” nie ma pokrycia: w tej sekcji nic nie jest poprawiane, a żaden późniejszy dział nie omawia poprawy tego konkretnego błędu. Usuń zdanie albo od razu pokaż poprawkę (np. wywołanie z argumentami we właściwej kolejności lub po nazwie). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **celowym błędem na końcu**: Czytelnik nie wie, o jaki błąd chodzi. Nazwij go na miejscu (kolejność argumentów zamieniona: 4 zł podzielone na 300 osób) albo usuń odwołanie do `funkcje.py` i jego błędu. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0829-weryfikator-odwolan.md) · 14.6 s · $0.0421

### 0830 · sprawdzacz_wyników · dział 07 · pytanie 43 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **parametry**: Słowo „parametry” pojawia się w ostatnim akapicie bez oznaczenia [[...]] i bez krótkiej definicji. Warto dodać hasło albo jedno zdanie, że parametr to nazwa w nawiasie definicji (wydatki, suma, liczba_osob), do której wchodzą dane przy wywołaniu. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0830-sprawdzacz-wynikow.md) · 9.1 s · $0.0200

### 0831 · weryfikator_faktów · dział 07 · pytanie 43 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0831-weryfikator-faktow.md) · 5.7 s · $0.0284

### 0832 · decyzja · dział 07 · pytanie 43 · próba 1

- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (blokująca) **funkcje.py / suma_wydatkow**: Zdanie „U siebie w `funkcje.py` masz to już gotowe, tylko z celowym błędem na końcu. Poprawiamy go poniżej” przeczy kanonowi. Pokazana czytelnikowi `suma_wydatkow` w `funkcje.py` jest poprawna: `return razem` stoi po pętli, a `udzial_na_osobe` też nie ma błędu. Poza tym w sekcji nie ma nic „poniżej”, co by coś poprawiało. Czytelnik będzie szukał nieistniejącego błędu. Usuń to zdanie albo zastąp je zgodnym z kanonem, np. „To te same funkcje, które masz w `funkcje.py`”. _← strażnik_przykład_
  - `odwołanie` (blokująca) **Poprawiamy go poniżej.**: Zapowiedź „poniżej” nie ma pokrycia: w tej sekcji nic nie jest poprawiane, a żaden późniejszy dział nie omawia poprawy tego konkretnego błędu. Usuń zdanie albo od razu pokaż poprawkę (np. wywołanie z argumentami we właściwej kolejności lub po nazwie). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **celowym błędem na końcu**: Czytelnik nie wie, o jaki błąd chodzi. Nazwij go na miejscu (kolejność argumentów zamieniona: 4 zł podzielone na 300 osób) albo usuń odwołanie do `funkcje.py` i jego błędu. _← weryfikator_odwołań_
- Wynik: Do poprawy: 3 blokujących potrzeb wraca do pisarza; 4 sugestii trafia do raportu.
- 0.0 s

### 0833 · pisarz · dział 07 · pytanie 43 · próba 2

- Kolejka TODO (18): 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55 …
- Potrzeby w kolejce przed krokiem (3):
  - `spójność` (blokująca) **funkcje.py / suma_wydatkow**: Zdanie „U siebie w `funkcje.py` masz to już gotowe, tylko z celowym błędem na końcu. Poprawiamy go poniżej” przeczy kanonowi. Pokazana czytelnikowi `suma_wydatkow` w `funkcje.py` jest poprawna: `return razem` stoi po pętli, a `udzial_na_osobe` też nie ma błędu. Poza tym w sekcji nie ma nic „poniżej”, co by coś poprawiało. Czytelnik będzie szukał nieistniejącego błędu. Usuń to zdanie albo zastąp je zgodnym z kanonem, np. „To te same funkcje, które masz w `funkcje.py`”. _← strażnik_przykład_
  - `odwołanie` (blokująca) **Poprawiamy go poniżej.**: Zapowiedź „poniżej” nie ma pokrycia: w tej sekcji nic nie jest poprawiane, a żaden późniejszy dział nie omawia poprawy tego konkretnego błędu. Usuń zdanie albo od razu pokaż poprawkę (np. wywołanie z argumentami we właściwej kolejności lub po nazwie). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **celowym błędem na końcu**: Czytelnik nie wie, o jaki błąd chodzi. Nazwij go na miejscu (kolejność argumentów zamieniona: 4 zł podzielone na 300 osób) albo usuń odwołanie do `funkcje.py` i jego błędu. _← weryfikator_odwołań_
- Wynik: „Ponowne użycie kodu”: 142 słów prozy, ```python 13 linii, ```text 2 linii; warsztat: funkcje.py, $ python funkcje.py
- [prompt i odpowiedź](_przebieg/0833-pisarz.md) · 16.8 s · $0.1013

### 0834 · kontrola_deterministyczna · dział 07 · pytanie 43 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0835 · weryfikator_pojęć · dział 07 · pytanie 43 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0835-weryfikator-pojec.md) · 6.6 s · $0.0228

### 0836 · znudzony_czytelnik · dział 07 · pytanie 43 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `skrócenie` (sugestia) **akapit o funkcje.py**: Ostatni akapit (o pliku funkcje.py, krótszych nazwach i błędzie w ostatniej linii) odciąga od tematu ponownego użycia i odsyła do warsztatu. Można go skrócić do jednego zdania albo przenieść do warsztatu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0836-znudzony-czytelnik.md) · 7.9 s · $0.0226

### 0837 · strażnik_przykład · dział 07 · pytanie 43 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **funkcje.py / suma_wydatkow**: Zdanie „U siebie w `funkcje.py` masz to już gotowe, tylko z celowym błędem na końcu. Poprawiamy go poniżej” przeczy kanonowi. Pokazana czytelnikowi `suma_wydatkow` w `funkcje.py` jest poprawna: `return razem` stoi po pętli, a `udzial_na_osobe` też nie ma błędu. Poza tym w sekcji nie ma nic „poniżej”, co by coś poprawiało. Czytelnik będzie szukał nieistniejącego błędu. Usuń to zdanie albo zastąp je zgodnym z kanonem, np. „To te same funkcje, które masz w `funkcje.py`”. _← strażnik_przykład_
- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 1.
- Nowe potrzeby (1):
  - `spójność` (blokująca, niespełniona) **funkcje.py / suma_wydatkow**: Nowa wersja nadal mówi o błędzie w funkcje.py, którego nie ma w kanonie: ostatnia linia z `na_osobe(300)` nie została nigdzie pokazana, a pokazane `suma_wydatkow` i `udzial_na_osobe` są poprawne. Odsyła też do „warsztatu poniżej”, którego w sekcji nie ma. Dodatkowo „pod krótszymi nazwami” nie zgadza się z kanonem, bo `suma_wydatkow` i `udzial_na_osobe` istnieją w funkcje.py pod pełnymi nazwami. Usuń całe ostatnie zdanie albo zastąp je zgodnym z kanonem, np. „To te same funkcje, które masz w `funkcje.py`.” _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0837-straznik-przyklad.md) · 8.5 s · $0.0304

### 0838 · strażnik_warsztat · dział 07 · pytanie 43 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **parametry / argument**: Słowa „parametry” i „argument” pojawiają się bez definicji w tekście (ostatni akapit: „z jednym argumentem zamiast dwóch”). Jeśli nie ma ich w glosariuszu, dodaj jedno zdanie, np.: „Parametr to nazwa w definicji (np. wydatki), a argument to wartość podana przy wywołaniu (np. mazury).” _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0838-straznik-warsztat.md) · 9.4 s · $0.0278

### 0839 · weryfikator_odwołań · dział 07 · pytanie 43 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **Poprawiamy go poniżej.**: Zapowiedź „poniżej” nie ma pokrycia: w tej sekcji nic nie jest poprawiane, a żaden późniejszy dział nie omawia poprawy tego konkretnego błędu. Usuń zdanie albo od razu pokaż poprawkę (np. wywołanie z argumentami we właściwej kolejności lub po nazwie). _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **celowym błędem na końcu**: Czytelnik nie wie, o jaki błąd chodzi. Nazwij go na miejscu (kolejność argumentów zamieniona: 4 zł podzielone na 300 osób) albo usuń odwołanie do `funkcje.py` i jego błędu. _← weryfikator_odwołań_
- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 1. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (blokująca, niespełniona) **Usuwamy ją w warsztacie poniżej.**: Zapowiedź „Usuwamy ją w warsztacie poniżej” nadal nie ma pokrycia: poniżej nie ma warsztatu, a żaden późniejszy dział nie omawia usunięcia tego błędu. Usuń zdanie albo od razu pokaż poprawkę, np. `print(na_osobe(300, 4))`. Nazwa błędu i jego przyczyna (jeden argument zamiast dwóch) są już podane, więc wystarczy zamienić zapowiedź na konkretną poprawioną linię lub ją pominąć. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0839-weryfikator-odwolan.md) · 12.1 s · $0.0415

### 0840 · sprawdzacz_wyników · dział 07 · pytanie 43 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0840-sprawdzacz-wynikow.md) · 5.4 s · $0.0153

### 0841 · weryfikator_faktów · dział 07 · pytanie 43 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0841-weryfikator-faktow.md) · 5.3 s · $0.0281

### 0842 · decyzja · dział 07 · pytanie 43 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (blokująca, niespełniona) **funkcje.py / suma_wydatkow**: Nowa wersja nadal mówi o błędzie w funkcje.py, którego nie ma w kanonie: ostatnia linia z `na_osobe(300)` nie została nigdzie pokazana, a pokazane `suma_wydatkow` i `udzial_na_osobe` są poprawne. Odsyła też do „warsztatu poniżej”, którego w sekcji nie ma. Dodatkowo „pod krótszymi nazwami” nie zgadza się z kanonem, bo `suma_wydatkow` i `udzial_na_osobe` istnieją w funkcje.py pod pełnymi nazwami. Usuń całe ostatnie zdanie albo zastąp je zgodnym z kanonem, np. „To te same funkcje, które masz w `funkcje.py`.” _← strażnik_przykład_
  - `odwołanie` (blokująca, niespełniona) **Usuwamy ją w warsztacie poniżej.**: Zapowiedź „Usuwamy ją w warsztacie poniżej” nadal nie ma pokrycia: poniżej nie ma warsztatu, a żaden późniejszy dział nie omawia usunięcia tego błędu. Usuń zdanie albo od razu pokaż poprawkę, np. `print(na_osobe(300, 4))`. Nazwa błędu i jego przyczyna (jeden argument zamiast dwóch) są już podane, więc wystarczy zamienić zapowiedź na konkretną poprawioną linię lub ją pominąć. _← weryfikator_odwołań_
- Wynik: Limit prób (2) wyczerpany; 2 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 0843 · akceptacja · dział 07 · pytanie 43

- Wynik: Sekcja [sec-07-ponowne-uzycie-kodu] dopisana do działu 07; odwołania: wstecz „U siebie w `funkcje.py` masz te same funkcje”, w przód „Usuwamy ją w warsztacie poniżej.”; punkty zaczepienia: dwa wyjazdy, ta sama funkcja; w TODO zostało 18.
- 0.0 s

### 0844 · łowca_pułapek · dział 07 · pytanie 43

- Wynik: „Ponowne użycie kodu”: brak pułapek
- [prompt i odpowiedź](_przebieg/0844-lowca-pulapek.md) · 2.2 s · $0.0134

### 0845 · autor_dodatków · dział 07 · pytanie 43

- Wynik: „Ponowne użycie kodu”: dygresje: Podprogramy: pomysł z pierwszych komputerów, rysunki: Jedna foremka, wiele ciastek
- [prompt i odpowiedź](_przebieg/0845-autor-dodatkow.md) · 13.8 s · $0.0836

### 0846 · weryfikator_dodatków · dział 07 · pytanie 43

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0846-weryfikator-dodatkow.md) · 24.2 s · $0.2200

### 0847 · autor_wstępu · dział 08 · próba 1

- Kolejka TODO (18): 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55 …
- Wynik: Wstęp: 88 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0847-autor-wstepu.md) · 5.8 s · $0.0334

### 0848 · recenzent_wstępu · dział 08 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `diagram` (sugestia) **strzałki wczytuje/zapisuje**: Etykiety stoją obok dwóch pionowych strzałek i trzeba się domyślać, która należy do której. Lepiej narysować dwie oddzielne strzałki z etykietami przy nich, np. 'program --zapisuje--> [ plik ]' oraz '[ plik ] --wczytuje--> program'. Wtedy kierunek przepływu jest oczywisty. _← recenzent_wstępu_
  - `diagram` (sugestia) **etykiety wpisuje/pokazuje**: Strzałki nie mówią, co przepływa. Dopisz 'wpisuje dane' i 'pokazuje wyniki'. To ułatwi później powiązanie diagramu z pojęciami dane wejściowe i wyjściowe, a czytelnik bez tego nie zauważy, że użytkownik po obu stronach to ta sama osoba. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0848-recenzent-wstepu.md) · 8.8 s · $0.0211

### 0849 · pisarz · dział 08 · pytanie 44 · próba 1

- Kolejka TODO (17): 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56 …
- Wynik: „Dane wejściowe programu”: 180 słów prozy, ```python 4 linii; nowe hasła: dane wejściowe; wątki: przykład dodaj zapytaj_o_wydatek
- [prompt i odpowiedź](_przebieg/0849-pisarz.md) · 21.4 s · $0.0941

### 0850 · kontrola_deterministyczna · dział 08 · pytanie 44 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0851 · weryfikator_pojęć · dział 08 · pytanie 44 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **input**: wystarczy jedno zdanie; pełne omówienie w pytaniu 46. Przy pierwszym użyciu w szkicu warto dodać, że input(...) to polecenie, które wyświetla podany tekst, czeka, aż użytkownik coś wpisze i zatwierdzi Enterem, po czym oddaje to jako wartość. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **wydatki.csv**: Format .csv nie jest znany początkującemu. Wystarczy pół zdania, np. że to zwykły plik tekstowy z danymi w wierszach, otwierany też w arkuszu kalkulacyjnym. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0851-weryfikator-pojec.md) · 10.7 s · $0.0274

### 0852 · znudzony_czytelnik · dział 08 · pytanie 44 · próba 1

- Wynik: 1 blokujących, 1 sugestii.
- Nowe potrzeby (2):
  - `odwołanie` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Fraza „danych wyjściowych” ma ten sam identyfikator hasła co dane wejściowe: [[dane-wejsciowe|danych wyjściowych]]. Kliknięcie prowadzi do złego hasła i miesza dwa przeciwne pojęcia. Trzeba podać osobny identyfikator (np. dane-wyjsciowe) z własnym hasłem w glosariuszu albo usunąć link i zostawić samą zapowiedź. _← znudzony_czytelnik_
  - `wyjaśnienie` (sugestia) **input w szkicu zapytaj_o_wydatek**: W szkicu `input(...)` pojawia się bez słowa wyjaśnienia. Wystarczy jedno zdanie pod kodem: `input` wyświetla pytanie, czeka na wpisanie tekstu i oddaje to, co wpisano. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0852-znudzony-czytelnik.md) · 10.0 s · $0.0243

### 0853 · strażnik_przykład · dział 08 · pytanie 44 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **mazury**: Tekst mówi „do tej pory kwoty wpisywaliśmy w kodzie, np. mazury = [45.5, 20, 12.5]”, ale w kanonie nie ma zmiennej mazury. Kanon pokazał wydatki (lista słowników) i kwota = 45.5. Lepiej użyć wydatki albo kwota, np. wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.50}], albo zaznaczyć, że to nowy, luźny przykład. _← strażnik_przykład_
  - `spójność` (sugestia) **zapytaj_o_wydatek**: W szkicu kwota to wynik input(), czyli tekst. W kanonie kwota to liczba (kwota = 45.5). Nie ma to znaczenia dla szkicu, ale warto dodać zdanie, że input zwraca tekst, który trzeba zamienić na liczbę i sprawdzić. To przygotuje grunt pod sprawdz_kwote. _← strażnik_przykład_
  - `spójność` (sugestia) **[[dane-wejsciowe|danych wyjściowych]]**: Odsyłacz „dane wyjściowe” prowadzi do hasła dane-wejsciowe, czyli do tej samej sekcji. Powinien wskazywać osobne hasło (np. dane-wyjsciowe) albo być zwykłym tekstem bez linku. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0853-straznik-przyklad.md) · 13.1 s · $0.0320

### 0854 · weryfikator_odwołań · dział 08 · pytanie 44 · próba 1

- Wynik: 1 blokujących, 2 sugestii. (odwołania: 3)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Znacznik w ostatnim zdaniu wskazuje id „dane-wejsciowe”, czyli tę samą sekcję, a tekst mówi o danych wyjściowych. Zamień znacznik na zwykły tekst („o danych wyjściowych opowiemy osobno”) albo wskaż właściwe hasło. Zdanie ma mówić o temacie, nie linkować do bieżącej sekcji. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **input**: W szkicu pojawia się `input` bez słowa wyjaśnienia. Dodaj krótkie zdanie, np. że `input` wyświetla pytanie i czeka na wpisanie odpowiedzi. Szczegóły są w późniejszej części. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **wydatki.csv**: Czytelnik spoza IT nie zna rozszerzenia .csv. Dopisz, że to zwykły plik tekstowy z danymi w wierszach, albo użyj nazwy `wydatki.txt`. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0854-weryfikator-odwolan.md) · 15.2 s · $0.0401

### 0855 · sprawdzacz_wyników · dział 08 · pytanie 44 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `wynik` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Odsyłacz [[dane-wejsciowe|danych wyjściowych]] wskazuje na hasło „dane-wejsciowe”, czyli na tę samą sekcję. Tekst mówi o danych wyjściowych, więc czytelnik kliknie i dostanie definicję danych wejściowych. Trzeba zmienić cel na właściwe hasło (np. [[dane-wyjsciowe|danych wyjściowych]]) i sprawdzić, że takie hasło jest w glosariuszu. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0855-sprawdzacz-wynikow.md) · 7.6 s · $0.0177

### 0856 · weryfikator_faktów · dział 08 · pytanie 44 · próba 1

- Wynik: Brak uwag. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0856-weryfikator-faktow.md) · 13.3 s · $0.0610

### 0857 · decyzja · dział 08 · pytanie 44 · próba 1

- Potrzeby w kolejce przed krokiem (3):
  - `odwołanie` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Fraza „danych wyjściowych” ma ten sam identyfikator hasła co dane wejściowe: [[dane-wejsciowe|danych wyjściowych]]. Kliknięcie prowadzi do złego hasła i miesza dwa przeciwne pojęcia. Trzeba podać osobny identyfikator (np. dane-wyjsciowe) z własnym hasłem w glosariuszu albo usunąć link i zostawić samą zapowiedź. _← znudzony_czytelnik_
  - `odwołanie` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Znacznik w ostatnim zdaniu wskazuje id „dane-wejsciowe”, czyli tę samą sekcję, a tekst mówi o danych wyjściowych. Zamień znacznik na zwykły tekst („o danych wyjściowych opowiemy osobno”) albo wskaż właściwe hasło. Zdanie ma mówić o temacie, nie linkować do bieżącej sekcji. _← weryfikator_odwołań_
  - `wynik` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Odsyłacz [[dane-wejsciowe|danych wyjściowych]] wskazuje na hasło „dane-wejsciowe”, czyli na tę samą sekcję. Tekst mówi o danych wyjściowych, więc czytelnik kliknie i dostanie definicję danych wejściowych. Trzeba zmienić cel na właściwe hasło (np. [[dane-wyjsciowe|danych wyjściowych]]) i sprawdzić, że takie hasło jest w glosariuszu. _← sprawdzacz_wyników_
- Wynik: Do poprawy: 3 blokujących potrzeb wraca do pisarza; 8 sugestii trafia do raportu.
- 0.0 s

### 0858 · pisarz · dział 08 · pytanie 44 · próba 2

- Kolejka TODO (17): 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56 …
- Potrzeby w kolejce przed krokiem (3):
  - `odwołanie` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Fraza „danych wyjściowych” ma ten sam identyfikator hasła co dane wejściowe: [[dane-wejsciowe|danych wyjściowych]]. Kliknięcie prowadzi do złego hasła i miesza dwa przeciwne pojęcia. Trzeba podać osobny identyfikator (np. dane-wyjsciowe) z własnym hasłem w glosariuszu albo usunąć link i zostawić samą zapowiedź. _← znudzony_czytelnik_
  - `odwołanie` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Znacznik w ostatnim zdaniu wskazuje id „dane-wejsciowe”, czyli tę samą sekcję, a tekst mówi o danych wyjściowych. Zamień znacznik na zwykły tekst („o danych wyjściowych opowiemy osobno”) albo wskaż właściwe hasło. Zdanie ma mówić o temacie, nie linkować do bieżącej sekcji. _← weryfikator_odwołań_
  - `wynik` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Odsyłacz [[dane-wejsciowe|danych wyjściowych]] wskazuje na hasło „dane-wejsciowe”, czyli na tę samą sekcję. Tekst mówi o danych wyjściowych, więc czytelnik kliknie i dostanie definicję danych wejściowych. Trzeba zmienić cel na właściwe hasło (np. [[dane-wyjsciowe|danych wyjściowych]]) i sprawdzić, że takie hasło jest w glosariuszu. _← sprawdzacz_wyników_
- Wynik: „Dane wejściowe programu”: 184 słów prozy, ```python 4 linii; nowe hasła: dane wejściowe; wątki: przykład dodaj zapytaj_o_wydatek
- [prompt i odpowiedź](_przebieg/0858-pisarz.md) · 13.4 s · $0.0960

### 0859 · kontrola_deterministyczna · dział 08 · pytanie 44 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0860 · weryfikator_pojęć · dział 08 · pytanie 44 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **input**: wystarczy jedno zdanie; pełne omówienie w pytaniu 46. Przy pierwszym użyciu w kodzie trzeba dopisać, że input wyświetla pytanie i czeka na wpisanie tekstu, a wpisana odpowiedź trafia do zmiennej. Z kontekstu da się to zgadnąć, ale tekst nie mówi tego wprost. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0860-weryfikator-pojec.md) · 9.2 s · $0.0258

### 0861 · znudzony_czytelnik · dział 08 · pytanie 44 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Fraza „danych wyjściowych” ma ten sam identyfikator hasła co dane wejściowe: [[dane-wejsciowe|danych wyjściowych]]. Kliknięcie prowadzi do złego hasła i miesza dwa przeciwne pojęcia. Trzeba podać osobny identyfikator (np. dane-wyjsciowe) z własnym hasłem w glosariuszu albo usunąć link i zostawić samą zapowiedź. _← znudzony_czytelnik_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0861-znudzony-czytelnik.md) · 3.7 s · $0.0199

### 0862 · strażnik_przykład · dział 08 · pytanie 44 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **mazury**: W tekście pojawia się `mazury = [45.5, 20, 12.5]`. Zmiennej `mazury` nie ma w kanonie. Kanon zna `wydatki` (lista słowników) i `kwota`. Lepiej napisać, że dotąd kwoty wpisywaliśmy w kodzie, np. `wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.50}]`. Można też zaznaczyć, że to luźny przykład. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0862-straznik-przyklad.md) · 7.5 s · $0.0261

### 0863 · weryfikator_odwołań · dział 08 · pytanie 44 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Znacznik w ostatnim zdaniu wskazuje id „dane-wejsciowe”, czyli tę samą sekcję, a tekst mówi o danych wyjściowych. Zamień znacznik na zwykły tekst („o danych wyjściowych opowiemy osobno”) albo wskaż właściwe hasło. Zdanie ma mówić o temacie, nie linkować do bieżącej sekcji. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 3)
- [prompt i odpowiedź](_przebieg/0863-weryfikator-odwolan.md) · 8.6 s · $0.0342

### 0864 · sprawdzacz_wyników · dział 08 · pytanie 44 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wynik` (blokująca) **[[dane-wejsciowe|danych wyjściowych]]**: Odsyłacz [[dane-wejsciowe|danych wyjściowych]] wskazuje na hasło „dane-wejsciowe”, czyli na tę samą sekcję. Tekst mówi o danych wyjściowych, więc czytelnik kliknie i dostanie definicję danych wejściowych. Trzeba zmienić cel na właściwe hasło (np. [[dane-wyjsciowe|danych wyjściowych]]) i sprawdzić, że takie hasło jest w glosariuszu. _← sprawdzacz_wyników_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0864-sprawdzacz-wynikow.md) · 4.3 s · $0.0165

### 0865 · weryfikator_faktów · dział 08 · pytanie 44 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0865-weryfikator-faktow.md) · 12.5 s · $0.0757

### 0866 · decyzja · dział 08 · pytanie 44 · próba 2

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 0867 · akceptacja · dział 08 · pytanie 44

- Wynik: Sekcja [sec-08-dane-wejsciowe-programu] dopisana do działu 08; hasła w glosariuszu: dane wejściowe; kanony: przykład:+zapytaj_o_wydatek; odwołania: wstecz „Do tej pory kwoty wpisywaliśmy w kodzie”, w przód „gdy zajmiemy się pytaniem użytkownika o informację”, w przód „opowiemy osobno, przy danych wyjściowych”; punkty zaczepienia: kod stały, dane zmienne; w TODO zostało 17.
- 0.0 s

### 0868 · łowca_pułapek · dział 08 · pytanie 44

- Wynik: „Dane wejściowe programu”: `input` zawsze zwraca tekst, nawet dla liczb
- [prompt i odpowiedź](_przebieg/0868-lowca-pulapek.md) · 8.1 s · $0.0215

### 0869 · autor_dodatków · dział 08 · pytanie 44

- Wynik: „Dane wejściowe programu”: dowcipy: Automat, który przyjmie wszystko
- [prompt i odpowiedź](_przebieg/0869-autor-dodatkow.md) · 12.5 s · $0.0842

### 0870 · weryfikator_dodatków · dział 08 · pytanie 44

- Wynik: odrzucone: 1; Automat, który przyjmie wszystko: Porównanie jest nietrafne (prawdziwy automat mechanicznie odrzuca guzik i kanapkę, więc tytuł „przyjmie wszystko” mija się z obrazem), a motyw „mechanizm nie sprawdza, co do niego wpisano” powtarza puentę wcześniejszego „Formularz nie zna Twojego nazwiska”.
- [prompt i odpowiedź](_przebieg/0870-weryfikator-dodatkow.md) · 9.1 s · $0.0755

### 0871 · pisarz · dział 08 · pytanie 45 · próba 1

- Kolejka TODO (16): 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57 …
- Wynik: „Dane wyjściowe programu”: 161 słów prozy, ```python 4 linii, ```text 1 linii; nowe hasła: dane wyjściowe
- [prompt i odpowiedź](_przebieg/0871-pisarz.md) · 18.1 s · $0.0917

### 0872 · kontrola_deterministyczna · dział 08 · pytanie 45 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0873 · weryfikator_pojęć · dział 08 · pytanie 45 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **interfejsie**: wystarczy jedno zdanie; pełne omówienie w pytaniu 48. Zdanie „wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie” częściowo wyjaśnia pojęcie, ale warto dodać krótkie: interfejs to sposób, w jaki program i użytkownik się ze sobą komunikują. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0873-weryfikator-pojec.md) · 8.0 s · $0.0252

### 0874 · znudzony_czytelnik · dział 08 · pytanie 45 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **blok kodu z wypisz_na_osobe i zdanie o opisie i jednostce**: Tekst mówi, że dobre wyjście ma opis i jednostkę, ale kod pokazuje tylko gołe „26.0”. Tabela obiecuje komunikat „Na osobę wychodzi 26.0”, a kod go nie wypisuje. Lepiej zamienić przykład na wersję z opisem, np. print("Na osobę wychodzi", suma / osoby, "zł"), i pokazać wynik „Na osobę wychodzi 26.0 zł”. Zmieści się w limicie, jeśli zastąpi obecny blok. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0874-znudzony-czytelnik.md) · 7.3 s · $0.0216

### 0875 · strażnik_przykład · dział 08 · pytanie 45 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0875-straznik-przyklad.md) · 4.6 s · $0.0229

### 0876 · weryfikator_odwołań · dział 08 · pytanie 45 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 3)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **dobre wyjście ma opis i jednostkę**: Teza o opisie i jednostce nie ma przykładu w kodzie. Dodaj wersję z opisem, np. print("Na osobę wychodzi", suma / osoby, "zł"), wraz z wynikiem, żeby czytelnik zobaczył różnicę względem „26.0”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **tabela i kod**: Tabela podaje komunikat „Na osobę wychodzi 26.0”, a kod wypisuje samo „26.0”. Ujednolić albo zaznaczyć, że tabela pokazuje wersję docelową. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0876-weryfikator-odwolan.md) · 13.9 s · $0.0388

### 0877 · sprawdzacz_wyników · dział 08 · pytanie 45 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0877-sprawdzacz-wynikow.md) · 4.0 s · $0.0137

### 0878 · weryfikator_faktów · dział 08 · pytanie 45 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0878-weryfikator-faktow.md) · 5.8 s · $0.0283

### 0879 · decyzja · dział 08 · pytanie 45 · próba 1

- Wynik: Sekcja przyjęta; 4 sugestii trafia do raportu.
- 0.0 s

### 0880 · akceptacja · dział 08 · pytanie 45

- Wynik: Sekcja [sec-08-dane-wyjsciowe-programu] dopisana do działu 08; hasła w glosariuszu: dane wyjściowe; odwołania: wstecz „o której mówiliśmy przy zwracaniu wyniku”, w przód „Do plików wrócimy osobno”, w przód „opiszemy przy interfejsie”; punkty zaczepienia: wynik bez opisu; w TODO zostało 16.
- 0.0 s

### 0881 · łowca_pułapek · dział 08 · pytanie 45

- Wynik: „Dane wyjściowe programu”: brak pułapek
- [prompt i odpowiedź](_przebieg/0881-lowca-pulapek.md) · 2.3 s · $0.0132

### 0882 · autor_dodatków · dział 08 · pytanie 45

- Wynik: „Dane wyjściowe programu”: dowcipy: Program jak drzewo w lesie
- [prompt i odpowiedź](_przebieg/0882-autor-dodatkow.md) · 10.2 s · $0.0819

### 0883 · weryfikator_dodatków · dział 08 · pytanie 45

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0883-weryfikator-dodatkow.md) · 5.6 s · $0.0720

### 0884 · pisarz · dział 08 · pytanie 46 · próba 1

- Kolejka TODO (15): 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58 …
- Wynik: „Pytanie użytkownika o informację”: 150 słów prozy, ```python 5 linii; nowe hasła: input; wątki: przykład zmień zapytaj_o_wydatek; warsztat: pytaj.py, $ python pytaj.py
- [prompt i odpowiedź](_przebieg/0884-pisarz.md) · 24.2 s · $0.1020

### 0885 · kontrola_deterministyczna · dział 08 · pytanie 46 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0886 · weryfikator_pojęć · dział 08 · pytanie 46 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0886-weryfikator-pojec.md) · 6.1 s · $0.0220

### 0887 · znudzony_czytelnik · dział 08 · pytanie 46 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **zapytaj_o_wydatek**: Kod pokazuje tylko pytania, ale nie widać, jak wygląda rozmowa w terminalu. Krótki blok text z przebiegiem (pytanie, wpisana odpowiedź) uświadomiłby, że program czeka i co widzi użytkownik. Można go zmieścić kosztem kropek '...' w kodzie. _← znudzony_czytelnik_
  - `konkret` (sugestia) **zapytaj_o_wydatek**: Kod kończy się na '...' i nie pokazuje, co funkcja robi z odpowiedziami (np. return kto, kwota). Czytelnik nie widzi, jak dane 'przychodzą' do programu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0887-znudzony-czytelnik.md) · 5.8 s · $0.0195

### 0888 · strażnik_przykład · dział 08 · pytanie 46 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **zapytaj_o_wydatek**: Kod zgadza się z kanonem i zadeklarowaną zmianą (dodane `kwota = float(kwota)`, reszta bez zmian). Sugestia: zdanie o kodzie „zostaje ten sam” jest w porządku, ale warto zaznaczyć, że funkcja nadal jest szkicem (`...`) i jeszcze nic nie zwraca ani nie zapisuje wydatku do listy `wydatki`. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0888-straznik-przyklad.md) · 4.6 s · $0.0239

### 0889 · strażnik_warsztat · dział 08 · pytanie 46 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **pytaj.py, return {"kto": ..., "kwota": ...}**: Funkcja zwraca słownik {"kto": kto, "kwota": kwota}, a potem czytamy go przez wydatek['kto']. Poprzednie pliki nie pokazują słowników, a sekcja ich nie tłumaczy. Warto dodać jedno zdanie, np. „Słownik to paczka wartości z etykietami: wydatek['kto'] wyjmuje wartość z etykietą kto.” _← strażnik_warsztat_
  - `spójność` (sugestia) **fragment kodu w tekście**: Fragment kodu w tekście (dwa kroki: kwota = input(...), potem kwota = float(kwota), na końcu „...”) różni się od pliku pytaj.py, gdzie jest float(input(...)) w jednej linii. Wynik jest ten sam, ale czytelnik może się zastanawiać, czy to błąd. Lepiej dodać zdanie, że plik skraca to do float(input("Ile zapłacił? ")), albo użyć w tekście tego samego zapisu. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0889-straznik-warsztat.md) · 12.0 s · $0.0299

### 0890 · weryfikator_odwołań · dział 08 · pytanie 46 · próba 1

- Wynik: 1 blokujących, 1 sugestii. (odwołania: 3)
- Nowe potrzeby (2):
  - `odwołanie` (blokująca) **„Wspólnej Kasy”**: Zdanie „To pierwsze z pytań do użytkownika, jakie dobudowujemy do „Wspólnej Kasy”” nawiązuje do projektu, którego nie ma na listach punktów zaczepienia ani sekcji. Czytelnik może nie wiedzieć, czym jest „Wspólna Kasa”. Wyjaśnij na miejscu jednym zdaniem (np. program do rozliczania wspólnych wydatków) albo usuń nazwę. Zapowiedź „pierwsze z pytań” też nic nie mówi bez tego kontekstu. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **kod przykładu**: Kod kończy się na „...”, a użytkownik nie widzi przykładowego przebiegu. Dodaj krótki zapis rozmowy (pytanie, wpisana odpowiedź) albo dokończ funkcję, np. return kto, kwota. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0890-weryfikator-odwolan.md) · 16.2 s · $0.0415

### 0891 · sprawdzacz_wyników · dział 08 · pytanie 46 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0891-sprawdzacz-wynikow.md) · 2.9 s · $0.0126

### 0892 · weryfikator_faktów · dział 08 · pytanie 46 · próba 1

- Wynik: Brak uwag. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0892-weryfikator-faktow.md) · 14.6 s · $0.0847

### 0893 · decyzja · dział 08 · pytanie 46 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **„Wspólnej Kasy”**: Zdanie „To pierwsze z pytań do użytkownika, jakie dobudowujemy do „Wspólnej Kasy”” nawiązuje do projektu, którego nie ma na listach punktów zaczepienia ani sekcji. Czytelnik może nie wiedzieć, czym jest „Wspólna Kasa”. Wyjaśnij na miejscu jednym zdaniem (np. program do rozliczania wspólnych wydatków) albo usuń nazwę. Zapowiedź „pierwsze z pytań” też nic nie mówi bez tego kontekstu. _← weryfikator_odwołań_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 6 sugestii trafia do raportu.
- 0.0 s

### 0894 · pisarz · dział 08 · pytanie 46 · próba 2

- Kolejka TODO (15): 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58 …
- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **„Wspólnej Kasy”**: Zdanie „To pierwsze z pytań do użytkownika, jakie dobudowujemy do „Wspólnej Kasy”” nawiązuje do projektu, którego nie ma na listach punktów zaczepienia ani sekcji. Czytelnik może nie wiedzieć, czym jest „Wspólna Kasa”. Wyjaśnij na miejscu jednym zdaniem (np. program do rozliczania wspólnych wydatków) albo usuń nazwę. Zapowiedź „pierwsze z pytań” też nic nie mówi bez tego kontekstu. _← weryfikator_odwołań_
- Wynik: „Pytanie użytkownika o informację”: 164 słów prozy, ```python 5 linii; nowe hasła: input; wątki: przykład zmień zapytaj_o_wydatek; warsztat: pytaj.py, $ python pytaj.py
- [prompt i odpowiedź](_przebieg/0894-pisarz.md) · 21.6 s · $0.1057

### 0895 · kontrola_deterministyczna · dział 08 · pytanie 46 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0896 · weryfikator_pojęć · dział 08 · pytanie 46 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0896-weryfikator-pojec.md) · 5.4 s · $0.0219

### 0897 · znudzony_czytelnik · dział 08 · pytanie 46 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **blok kodu zapytaj_o_wydatek**: Sekcja nie pokazuje, co użytkownik widzi na ekranie po uruchomieniu. Krótki blok `text` z rozmową (Kto zapłacił? Ola / Ile zapłacił? 45.5) uwidoczniłby oczekiwanie na Enter i to, że wpisany tekst trafia do zmiennej. Trzy kropki `...` w kodzie można zastąpić np. `return kto, kwota`. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0897-znudzony-czytelnik.md) · 8.2 s · $0.0221

### 0898 · strażnik_przykład · dział 08 · pytanie 46 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0898-straznik-przyklad.md) · 5.3 s · $0.0241

### 0899 · strażnik_warsztat · dział 08 · pytanie 46 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **fragment kodu w tekście vs pytaj.py**: Tekst pokazuje funkcję zapytaj_o_wydatek() z `...` i osobnym przypisaniem `kwota = float(kwota)`. Plik pytaj.py w krokach jest skryptem bez funkcji, z `float(input(...))` w jednej linii. Warto dodać zdanie, że w warsztacie zapisujemy to krócej, w jednej linii, albo ujednolicić kod. _← strażnik_warsztat_
  - `spójność` (sugestia) **input zawsze zwraca tekst**: Teza „input zawsze zwraca tekst” nie ma w krokach żadnego sprawdzenia. Można dodać `print(type(kwota))` przed konwersją albo pokazać błąd po pominięciu float(), np. `kwota / 2` daje `TypeError: unsupported operand type(s) for /: 'str' and 'int'`. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0899-straznik-warsztat.md) · 9.9 s · $0.0281

### 0900 · weryfikator_odwołań · dział 08 · pytanie 46 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **„Wspólnej Kasy”**: Zdanie „To pierwsze z pytań do użytkownika, jakie dobudowujemy do „Wspólnej Kasy”” nawiązuje do projektu, którego nie ma na listach punktów zaczepienia ani sekcji. Czytelnik może nie wiedzieć, czym jest „Wspólna Kasa”. Wyjaśnij na miejscu jednym zdaniem (np. program do rozliczania wspólnych wydatków) albo usuń nazwę. Zapowiedź „pierwsze z pytań” też nic nie mówi bez tego kontekstu. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/0900-weryfikator-odwolan.md) · 8.1 s · $0.0357

### 0901 · sprawdzacz_wyników · dział 08 · pytanie 46 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0901-sprawdzacz-wynikow.md) · 5.1 s · $0.0143

### 0902 · weryfikator_faktów · dział 08 · pytanie 46 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0902-weryfikator-faktow.md) · 14.8 s · $0.0846

### 0903 · decyzja · dział 08 · pytanie 46 · próba 2

- Wynik: Sekcja przyjęta; 3 sugestii trafia do raportu.
- 0.0 s

### 0904 · akceptacja · dział 08 · pytanie 46

- Wynik: Sekcja [sec-08-pytanie-uzytkownika-o-informacje] dopisana do działu 08; hasła w glosariuszu: input; kanony: przykład:~zapytaj_o_wydatek; odwołania: wstecz „kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne”, w przód „przykładzie, który będzie nam towarzyszył”; punkty zaczepienia: input zwraca tekst; w TODO zostało 15.
- 0.0 s

### 0905 · łowca_pułapek · dział 08 · pytanie 46

- Wynik: „Pytanie użytkownika o informację”: brak pułapek
- [prompt i odpowiedź](_przebieg/0905-lowca-pulapek.md) · 2.2 s · $0.0136

### 0906 · autor_dodatków · dział 08 · pytanie 46

- Wynik: „Pytanie użytkownika o informację”: wtręty: Marta myśli, że program się zawiesił, dykteryjki: Suma, która wyszła jako sklejenie
- [prompt i odpowiedź](_przebieg/0906-autor-dodatkow.md) · 15.5 s · $0.0862

### 0907 · weryfikator_dodatków · dział 08 · pytanie 46

- Wynik: odrzucone: 1; Marta myśli, że program się zawiesił: Powtarza motyw wpisu „Marta czeka, aż plik sam zadziała”: Marta patrzy w ekran, nic się nie dzieje, więc uznaje, że komputer jest wolny albo zawieszony.
- [prompt i odpowiedź](_przebieg/0907-weryfikator-dodatkow.md) · 11.1 s · $0.0801

### 0908 · pisarz · dział 08 · pytanie 47 · próba 1

- Kolejka TODO (14): 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59 …
- Wynik: „Czym jest plik”: 181 słów prozy, ```python 7 linii, ```text 2 linii; nowe hasła: plik, tryb otwarcia pliku; warsztat: pytaj.py, $ python pytaj.py, $ python pytaj.py
- [prompt i odpowiedź](_przebieg/0908-pisarz.md) · 25.6 s · $0.1067

### 0909 · kontrola_deterministyczna · dział 08 · pytanie 47 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0910 · weryfikator_pojęć · dział 08 · pytanie 47 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odrzucono 1 zgłoszeń o pojęciach spoza tekstu albo już w glosariuszu)
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **float()**: float() nie ma hasła w glosariuszu ani wyjaśnienia. Wystarczy jedno zdanie, że zamienia tekst na liczbę z przecinkiem (ułamek dziesiętny). Odwołanie do input jest tylko wskazówką. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **with ... as plik**: Nazwa po `as` (plik) i wywołania plik.write oraz plik.read nie są wyjaśnione. Wystarczy jedno zdanie, że `as plik` nadaje otwartemu plikowi nazwę, przez którą się do niego odwołujemy. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0910-weryfikator-pojec.md) · 12.0 s · $0.0294

### 0911 · znudzony_czytelnik · dział 08 · pytanie 47 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `fakt` (sugestia) **Uwaga: plik przechowuje wyłącznie tekst**: Zdanie „plik przechowuje wyłącznie tekst” jest za mocne: pliki (zdjęcia, arkusze) mogą zawierać nie tylko tekst. Lepiej: „plik tekstowy otwarty tak jak tu zwraca tekst”. _← znudzony_czytelnik_
  - `konkret` (sugestia) **blok kodu z write i print**: `\n` i `end=""` pojawiają się bez wyjaśnienia. Wystarczy pół zdania: `\n` to koniec wiersza, a `end=""` zapobiega pustej linii po wypisaniu. Warto też napisać, że wydatki.txt powstaje w folderze, z którego uruchomiono program. _← znudzony_czytelnik_
  - `skrócenie` (sugestia) **Pułapką jest tryb "w"**: Ostatnie zdanie o sprawdzaniu danych jest luźno związane z plikami. Lepiej zastąpić je konkretem o tym, że ponowne uruchomienie kodu z trybem "w" zeruje plik wydatki.txt. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0911-znudzony-czytelnik.md) · 13.2 s · $0.0274

### 0912 · strażnik_przykład · dział 08 · pytanie 47 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **wydatki.txt**: Przykład zapisuje plik „wydatki.txt” ze średnikami, a wątek planuje „wydatki.csv” jako plik danych programu. Zmień nazwę na „wydatki.csv” albo zadeklaruj „wydatki.txt” jako osobny plik pomocniczy (canon_changes, module="przykład", dodaj). Możesz też dodać zdanie, że to plik ćwiczebny, a właściwy „wydatki.csv” pojawi się później. Dzięki temu czytelnik nie pomyśli, że są to dwa różne pliki programu. _← strażnik_przykład_
  - `spójność` (sugestia) **plik, tekst**: Zmienne „plik” (uchwyt z with open) i „tekst” są nowe i niezadeklarowane w canon_changes. Zadeklaruj je jako „dodaj” albo zaznacz, że to lokalne nazwy przykładu. Nie koliduje to z kanonem, bo „kwota” i „wydatki” nie są użyte w innym znaczeniu. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0912-straznik-przyklad.md) · 10.4 s · $0.0302

### 0913 · strażnik_warsztat · dział 08 · pytanie 47 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0913-straznik-warsztat.md) · 6.4 s · $0.0262

### 0914 · weryfikator_odwołań · dział 08 · pytanie 47 · próba 1

- Wynik: 2 blokujących, 1 sugestii. (odwołania: 2)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **To odpowiedź na problem zmiennych**: Nawiązanie do „problemu zmiennych” nie ma celu wśród punktów zaczepienia ani sekcji: żaden wcześniejszy fragment nie mówił, że zmienne znikają po zakończeniu programu. Wyjaśnij to na miejscu, np. „Zmienne istnieją tylko, gdy program działa, i znikają wraz z jego zakończeniem, a plik zostaje”, i usuń zdanie o „problemie zmiennych”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **tryb "w"**: Pułapkę trybu "w" opisano tylko słowami. Wystarczy jedno zdanie: ponowne otwarcie wydatki.txt w trybie "w" zostawi pusty plik. Warto też jednym zdaniem wyjaśnić \n jako koniec wiersza. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **To odpowiedź na problem zmiennych**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/0914-weryfikator-odwolan.md) · 14.3 s · $0.0416

### 0915 · sprawdzacz_wyników · dział 08 · pytanie 47 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0915-sprawdzacz-wynikow.md) · 4.6 s · $0.0148

### 0916 · weryfikator_faktów · dział 08 · pytanie 47 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (źródła: 1)
- Nowe potrzeby (2):
  - `fakt` (sugestia) **Uwaga: plik przechowuje wyłącznie tekst, więc kwotę po wczytaniu trzeba znów zamienić przez `float()`**: Dokumentacja open() (https://docs.python.org/3.13/library/functions.html#open) opisuje też tryb binarny ('b'), więc plik nie przechowuje wyłącznie tekstu. Tekstowy tryb (domyślny) zwraca str, więc wniosek o float() jest poprawny. Wystarczy zawęzić: „plik otwarty w trybie tekstowym daje tekst”. _← weryfikator_faktów_
  - `fakt` (sugestia) **Tabela trybów: "w" i "a"**: Dokumentacja podaje, że "w" obcina plik, a "a" dopisuje na końcu. Oba tryby tworzą plik, gdy go nie ma, a tabela tego nie mówi. Nie blokuje to kodu, w którym "w" tworzy wydatki.txt. Można dodać „plik zostanie utworzony, jeśli go nie ma”. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0916-weryfikator-faktow.md) · 19.1 s · $0.0910

### 0917 · decyzja · dział 08 · pytanie 47 · próba 1

- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **To odpowiedź na problem zmiennych**: Nawiązanie do „problemu zmiennych” nie ma celu wśród punktów zaczepienia ani sekcji: żaden wcześniejszy fragment nie mówił, że zmienne znikają po zakończeniu programu. Wyjaśnij to na miejscu, np. „Zmienne istnieją tylko, gdy program działa, i znikają wraz z jego zakończeniem, a plik zostaje”, i usuń zdanie o „problemie zmiennych”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **To odpowiedź na problem zmiennych**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Do poprawy: 2 blokujących potrzeb wraca do pisarza; 10 sugestii trafia do raportu.
- 0.0 s

### 0918 · pisarz · dział 08 · pytanie 47 · próba 2

- Kolejka TODO (14): 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59 …
- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **To odpowiedź na problem zmiennych**: Nawiązanie do „problemu zmiennych” nie ma celu wśród punktów zaczepienia ani sekcji: żaden wcześniejszy fragment nie mówił, że zmienne znikają po zakończeniu programu. Wyjaśnij to na miejscu, np. „Zmienne istnieją tylko, gdy program działa, i znikają wraz z jego zakończeniem, a plik zostaje”, i usuń zdanie o „problemie zmiennych”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **To odpowiedź na problem zmiennych**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: „Czym jest plik”: 180 słów prozy, ```python 7 linii, ```text 2 linii; nowe hasła: plik, tryb otwarcia pliku; wątki: przykład dodaj wydatki.txt; warsztat: plik.py, $ python plik.py
- [prompt i odpowiedź](_przebieg/0918-pisarz.md) · 19.4 s · $0.1070

### 0919 · kontrola_deterministyczna · dział 08 · pytanie 47 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0920 · weryfikator_pojęć · dział 08 · pytanie 47 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0. (odrzucono 1 zgłoszeń o pojęciach spoza tekstu albo już w glosariuszu)
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **float()**: `float()` nie ma hasła w glosariuszu, a tekst mówi tylko, że zamienia kwotę. Wystarczy dodać, że `float()` zamienia tekst na liczbę z ułamkiem dziesiętnym. Pełne omówienie jest w innym miejscu kursu. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **end=""**: `end=""` w `print` nie jest wyjaśnione. Czytelnik nie wie, że wyłącza dodatkowe przejście do nowej linii, bo tekst z pliku już je zawiera. Wystarczy jedno zdanie. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0920-weryfikator-pojec.md) · 12.8 s · $0.0298

### 0921 · znudzony_czytelnik · dział 08 · pytanie 47 · próba 2

- Wynik: 0 blokujących, 3 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (3):
  - `skrócenie` (sugestia) **Ostatni akapit (Uwaga)**: Ostatni akapit powtarza prawie dosłownie pułapkę z poprzedniej sekcji (input zwraca tekst, nawet gdy ktoś wpisze 45.5), choć tu dane pochodzą z pliku, nie z input. Zdanie o sprawdzaniu danych też nie wnosi nic nowego. Warto zostawić tylko: z pliku wraca tekst, więc trzeba float(), oraz ostrzeżenie o trybie "w". _← znudzony_czytelnik_
  - `przykład` (sugestia) **Tryb "a" (dopisywanie)**: Tryby "a" i "r" są w tabeli, ale kod pokazuje tylko "w" i "r". Można w jednej linijce dodać przykład dopisania ("a") kolejnego wydatku, np. Celina;30.0, co pokazałoby różnicę wobec "w". Pamiętaj o limicie kodu. _← znudzony_czytelnik_
  - `wyjaśnienie` (sugestia) **\n oraz end=""**: Zapis "\n" w kodzie i end="" w print pojawiają się bez objaśnienia. Wystarczy pół zdania: \n oznacza koniec wiersza, a end="" zapobiega dodatkowej pustej linii. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0921-znudzony-czytelnik.md) · 7.3 s · $0.0231

### 0922 · strażnik_przykład · dział 08 · pytanie 47 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **wydatki.txt**: Wątek zakłada plik danych wydatki.csv, który program wczytuje w tym dziale. Sekcja i zadeklarowana zmiana wprowadzają wydatki.txt z separatorem ';' i bez pola opis (kanon: kto, opis, kwota). Zmiana jest zadeklarowana, więc to nie sprzeczność, ale czytelnik może się pogubić, gdy później pojawi się wydatki.csv. Rozważ użycie od razu wydatki.csv, np. 'Ania,zakupy,120.5', albo dodaj jedno zdanie, że .txt służy tu tylko do ćwiczenia, a docelowy plik to wydatki.csv. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0922-straznik-przyklad.md) · 12.6 s · $0.0374

### 0923 · strażnik_warsztat · dział 08 · pytanie 47 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0923-straznik-warsztat.md) · 8.1 s · $0.0278

### 0924 · weryfikator_odwołań · dział 08 · pytanie 47 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **To odpowiedź na problem zmiennych**: Nawiązanie do „problemu zmiennych” nie ma celu wśród punktów zaczepienia ani sekcji: żaden wcześniejszy fragment nie mówił, że zmienne znikają po zakończeniu programu. Wyjaśnij to na miejscu, np. „Zmienne istnieją tylko, gdy program działa, i znikają wraz z jego zakończeniem, a plik zostaje”, i usuń zdanie o „problemie zmiennych”. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/0924-weryfikator-odwolan.md) · 9.1 s · $0.0376

### 0925 · sprawdzacz_wyników · dział 08 · pytanie 47 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0925-sprawdzacz-wynikow.md) · 4.7 s · $0.0151

### 0926 · weryfikator_faktów · dział 08 · pytanie 47 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- [prompt i odpowiedź](_przebieg/0926-weryfikator-faktow.md) · 15.3 s · $0.0803

### 0927 · decyzja · dział 08 · pytanie 47 · próba 2

- Wynik: Sekcja przyjęta; 6 sugestii trafia do raportu.
- 0.0 s

### 0928 · akceptacja · dział 08 · pytanie 47

- Wynik: Sekcja [sec-08-czym-jest-plik] dopisana do działu 08; hasła w glosariuszu: plik, tryb otwarcia pliku; kanony: przykład:+wydatki.txt; odwołania: wstecz „`input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`”, w przód „o czym powiemy przy sprawdzaniu danych użytkownika”; punkty zaczepienia: tryb w kasuje, plik zostaje; w TODO zostało 14.
- 0.0 s

### 0929 · łowca_pułapek · dział 08 · pytanie 47

- Wynik: „Czym jest plik”: Ścieżka względna zależy od folderu uruchomienia
- [prompt i odpowiedź](_przebieg/0929-lowca-pulapek.md) · 7.1 s · $0.0211

### 0930 · autor_dodatków · dział 08 · pytanie 47

- Wynik: „Czym jest plik”: wtręty: Marta dopisuje wydatek i kasuje resztę, rysunki: Tablica się kończy, zeszyt zostaje
- [prompt i odpowiedź](_przebieg/0930-autor-dodatkow.md) · 10.7 s · $0.0838

### 0931 · weryfikator_dodatków · dział 08 · pytanie 47

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0931-weryfikator-dodatkow.md) · 4.9 s · $0.0740

### 0932 · pisarz · dział 08 · pytanie 48 · próba 1

- Kolejka TODO (13): 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60 …
- Wynik: „Czym jest interfejs użytkownika”: 156 słów prozy, ```python 8 linii, ```text 3 linii; nowe hasła: interfejs użytkownika, interfejs tekstowy; wątki: przykład dodaj wypisz_podsumowanie; warsztat: interfejs.py, $ python interfejs.py
- [prompt i odpowiedź](_przebieg/0932-pisarz.md) · 25.7 s · $0.1089

### 0933 · kontrola_deterministyczna · dział 08 · pytanie 48 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0934 · weryfikator_pojęć · dział 08 · pytanie 48 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0934-weryfikator-pojec.md) · 5.4 s · $0.0224

### 0935 · znudzony_czytelnik · dział 08 · pytanie 48 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **wejście interfejsu (input)**: Kod pokazuje tylko wyjście (print). Strona wejściowa, czyli pytanie i odpowiedź człowieka, jest tylko opisana. Wystarczyłby krótki blok text z rozmową, np. „Kto płacił? Ania / Ile zapłacił? 120.5”, zamiast jednego z opisów. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0935-znudzony-czytelnik.md) · 7.3 s · $0.0224

### 0936 · strażnik_przykład · dział 08 · pytanie 48 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0936-straznik-przyklad.md) · 6.6 s · $0.0257

### 0937 · strażnik_warsztat · dział 08 · pytanie 48 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **interfejs.py / wydatki (słownik)**: Kod używa słowników ({"kto": ..., "kwota": ...}) i odczytu wartości przez wydatek['kto'], a w dotychczasowych plikach ich nie było. Dodaj jedno zdanie: nawiasy {} grupują dane pod nazwami (kto, opis, kwota), a wydatek['kto'] wyciąga wartość o tej nazwie. Można też dopisać, że pole „opis” na razie nie jest używane. Kod działa, a wynik jest poprawny. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0937-straznik-warsztat.md) · 11.2 s · $0.0305

### 0938 · weryfikator_odwołań · dział 08 · pytanie 48 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 3)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **wejście interfejsu**: Sekcja mówi, że interfejs ma stronę wejścia (pytania), ale przykład kodu pokazuje tylko wyjście. Warto dodać krótki fragment z input, np. kwota = float(input("Ile zapłacił? ")), i pokazać rozmowę w terminalu. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **ostatnie zdanie**: Ostatnie zdanie zapowiada, że użytkownik może wpisać coś nieoczekiwanego, ale nie daje przykładu (np. tekst zamiast liczby). Jedno zdanie z przykładem pomogłoby, choć temat wróci osobno. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0938-weryfikator-odwolan.md) · 12.9 s · $0.0420

### 0939 · sprawdzacz_wyników · dział 08 · pytanie 48 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0939-sprawdzacz-wynikow.md) · 4.1 s · $0.0146

### 0940 · weryfikator_faktów · dział 08 · pytanie 48 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0940-weryfikator-faktow.md) · 5.3 s · $0.0286

### 0941 · decyzja · dział 08 · pytanie 48 · próba 1

- Wynik: Sekcja przyjęta; 4 sugestii trafia do raportu.
- 0.0 s

### 0942 · akceptacja · dział 08 · pytanie 48

- Wynik: Sekcja [sec-08-czym-jest-interfejs-uzytkownika] dopisana do działu 08; hasła w glosariuszu: interfejs użytkownika, interfejs tekstowy; kanony: przykład:+wypisz_podsumowanie; odwołania: wstecz „dwie znane już rzeczy: input do pytań i print do wyników”, wstecz „suchy wynik nic nie mówi komuś, kto nie zna kodu”, w przód „człowiek po drugiej stronie potrafi wpisać coś nieoczekiwanego”; punkty zaczepienia: interfejs to jedyne, co widzi użytkownik; w TODO zostało 13.
- 0.0 s

### 0943 · łowca_pułapek · dział 08 · pytanie 48

- Wynik: „Czym jest interfejs użytkownika”: brak pułapek
- [prompt i odpowiedź](_przebieg/0943-lowca-pulapek.md) · 2.3 s · $0.0167

### 0944 · autor_dodatków · dział 08 · pytanie 48

- Wynik: „Czym jest interfejs użytkownika”: dygresje: Mysz i okna na pokazie z 1968 roku, dowcipy: Interfejs to lada w sklepie
- [prompt i odpowiedź](_przebieg/0944-autor-dodatkow.md) · 10.7 s · $0.0865

### 0945 · weryfikator_dodatków · dział 08 · pytanie 48

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0945-weryfikator-dodatkow.md) · 14.8 s · $0.1319

### 0946 · pisarz · dział 08 · pytanie 49 · próba 1

- Kolejka TODO (12): 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61
- Wynik: „Po co sprawdzać dane użytkownika”: 155 słów prozy, ```python 7 linii, ```text 5 linii; nowe hasła: walidacja danych; wątki: przykład dodaj sprawdz_kwote; warsztat: pytaj.py, $ python pytaj.py
- [prompt i odpowiedź](_przebieg/0946-pisarz.md) · 27.5 s · $0.1151

### 0947 · kontrola_deterministyczna · dział 08 · pytanie 49 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0948 · weryfikator_pojęć · dział 08 · pytanie 49 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **repr**: Kod używa `repr(tekst)` bez wyjaśnienia. Wystarczy jedno zdanie: `repr` pokazuje tekst w cudzysłowie, żeby było widać także pusty tekst `''`. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **isdigit**: Zapis `tekst.replace(".", "", 1).isdigit()` jest opisany tylko ogólnie („sprawdza, czy tekst składa się z cyfr”). Nie widać, że `replace` usuwa jedną kropkę, a `isdigit` odpowiada, czy zostały same cyfry. Wystarczy jedno zdanie. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/0948-weryfikator-pojec.md) · 11.2 s · $0.0289

### 0949 · znudzony_czytelnik · dział 08 · pytanie 49 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **zakończenie sekcji**: Końcowe zdanie obiecuje, że zły wpis dostaje komunikat i kolejną szansę, ale kod tego nie pokazuje. Pokazuje tylko True/False. Wystarczy zastąpić pętlę testową krótką pętlą while z input(), która pyta ponownie po złym wpisie. Można też dopisać, że pętlę poznamy w następnej sekcji. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0949-znudzony-czytelnik.md) · 8.9 s · $0.0234

### 0950 · strażnik_przykład · dział 08 · pytanie 49 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **sprawdz_kwote**: Kod zgadza się z deklaracją autora, a wypisany wynik jest poprawny dla wszystkich pięciu wejść. Nie ma tu sprzeczności z kanonem. _← strażnik_przykład_
  - `spójność` (sugestia) **zapytaj_o_wydatek**: Tekst obiecuje, że zły wpis dostaje komunikat i kolejną szansę, ale nie pokazuje, jak sprawdz_kwote wchodzi do kanonicznej zapytaj_o_wydatek. Wystarczy szkic pętli: `kwota = input("Ile zapłacił? ")`, potem `while not sprawdz_kwote(kwota): ...`, na końcu `float(kwota)`. Wtedy wątek dochodzi do celu działu. Jeśli to pojawi się w kolejnej sekcji, wystarczy jedno zdanie zapowiedzi. _← strażnik_przykład_
  - `spójność` (sugestia) **opis kodu (Pierwsza linia / Druga)**: Warunek `if` zajmuje dwie linie, a liczenie `float(tekst) > 0` to trzecia. Lepiej napisać „pierwszy warunek” i „ostatnia linia”. Warto też dodać, że `-5` odpada na pierwszym warunku, bo znak minusa nie jest cyfrą. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0950-straznik-przyklad.md) · 12.0 s · $0.0320

### 0951 · strażnik_warsztat · dział 08 · pytanie 49 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0951-straznik-warsztat.md) · 7.9 s · $0.0294

### 0952 · weryfikator_odwołań · dział 08 · pytanie 49 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 1)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **Konsekwencja: zły wpis nie kończy programu**: Końcowa teza, że zły wpis dostaje komunikat i kolejną szansę, nie ma pokazu w kodzie. Warto dodać krótką pętlę while z input, która pyta ponownie, aż sprawdz_kwote zwróci True. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **Pierwsza linia sprawdza**: „Pierwsza linia” i „Druga” to w kodzie pierwszy i drugi warunek w funkcji, bo pierwsza linia to def. Lepiej napisać „pierwszy warunek” i „drugi”. Warto też jednym zdaniem wyjaśnić repr, które pokazuje apostrofy wokół tekstu i odróżnia pusty tekst od braku wypisu. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0952-weryfikator-odwolan.md) · 13.6 s · $0.0415

### 0953 · sprawdzacz_wyników · dział 08 · pytanie 49 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wynik` (sugestia) **repr**: W kodzie jest `repr(tekst)`, a czytelnik spoza IT nie wie, czemu wynik ma apostrofy. Wystarczy jedno zdanie, np. że `repr` pokazuje tekst w apostrofach, dzięki czemu widać także pusty wpis `''`. _← sprawdzacz_wyników_
  - `wynik` (sugestia) **Konsekwencja**: Zdanie o złym wpisie, który dostaje komunikat i kolejną szansę, nie ma pokrycia w kodzie. Można dodać krótką pętlę z `input` i `sprawdz_kwote`, która ponawia pytanie. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0953-sprawdzacz-wynikow.md) · 9.7 s · $0.0203

### 0954 · weryfikator_faktów · dział 08 · pytanie 49 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (źródła: 0)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **if not tekst.replace(".", "", 1).isdigit()**: Dokumentacja Pythona (https://docs.python.org/3/library/stdtypes.html#str.isdigit) mówi, że str.isdigit() zwraca True także dla znaków takich jak indeksy górne (np. "²"), a float("²") zgłasza ValueError. Dla zwykłych danych z klawiatury początkującego kod działa poprawnie i cały wynik w bloku text jest zgodny z tym, co program wypisze. Jeśli sekcja ma twierdzić, że funkcja chroni przed każdym błędem konwersji, warto to złagodzić albo w przyszłości użyć try/except ValueError. Nie było sprawdzane w dokumentacji online w tej sesji; wniosek wynika ze znajomości dokumentacji. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0954-weryfikator-faktow.md) · 12.3 s · $0.0352

### 0955 · decyzja · dział 08 · pytanie 49 · próba 1

- Wynik: Sekcja przyjęta; 11 sugestii trafia do raportu.
- 0.0 s

### 0956 · akceptacja · dział 08 · pytanie 49

- Wynik: Sekcja [sec-08-po-co-sprawdzac-dane-uzytkownika] dopisana do działu 08; hasła w glosariuszu: walidacja danych; kanony: przykład:+sprawdz_kwote; odwołania: wstecz „zawsze zwraca tekst”; punkty zaczepienia: cichy błąd z minusem, zły wpis dostaje drugą szansę; w TODO zostało 12.
- 0.0 s

### 0957 · łowca_pułapek · dział 08 · pytanie 49

- Wynik: „Po co sprawdzać dane użytkownika”: Sprawdzenie przepuszcza tekst, którego float nie przyjmie
- [prompt i odpowiedź](_przebieg/0957-lowca-pulapek.md) · 8.7 s · $0.0225

### 0958 · autor_dodatków · dział 08 · pytanie 49

- Wynik: „Po co sprawdzać dane użytkownika”: wtręty: Marta wpisuje kwotę z przecinkiem
- [prompt i odpowiedź](_przebieg/0958-autor-dodatkow.md) · 11.0 s · $0.0858

### 0959 · weryfikator_dodatków · dział 08 · pytanie 49

- Wynik: odrzucone: 1; Marta wpisuje kwotę z przecinkiem: Wyjaśnienie jest odwrócone: w wpisie `45,5` nie ma kropki, tylko przecinek, więc `False` bierze się stąd, że w tekście został przecinek zamiast kropki, a nie odwrotnie.
- [prompt i odpowiedź](_przebieg/0959-weryfikator-dodatkow.md) · 5.5 s · $0.0756

### 0960 · autor_wstępu · dział 09 · próba 1

- Kolejka TODO (12): 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61
- Wynik: Wstęp: 84 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0960-autor-wstepu.md) · 5.8 s · $0.0364

### 0961 · recenzent_wstępu · dział 09 · próba 1

- Wynik: 1 blokujących, 3 sugestii.
- Nowe potrzeby (4):
  - `diagram` (blokująca) **diagram**: Diagram jest mylący: strzałka powrotna z „zapisu wersji” wraca do „błędu” bez etykiety, więc nie wiadomo, co znaczy (po zapisie pojawia się nowy błąd? cykl trwa w nieskończoność?). Test stoi po komunikacie, choć testy służą do wykrywania błędów, a komunikat pojawia się przy uruchomieniu; kolejność jest niejasna. Przerysuj: np. „uruchomienie → komunikat lub zły wynik → szukanie przyczyny (debugowanie) → poprawka → test → zapis wersji”, a strzałkę powrotną opisz („test nadal nie przechodzi → wracamy do szukania przyczyny”) i poprowadź z testu, nie z zapisu. Albo usuń diagram. _← recenzent_wstępu_
  - `wyjaśnienie` (sugestia) **zapiszemy poprawkę w Git**: Wstęp używa nieznanych czytelnikowi skrótów bez zapowiedzi: „Git” pojawia się na końcu bez słowa, czym jest (wystarczy krótkie „w systemie do zapisywania wersji kodu, Git”). Podobnie „testami” i „krok po kroku” są zrozumiałe, ale Git nie. _← recenzent_wstępu_
  - `konkret` (sugestia) **„Wspólnej Kasy”**: Nie wiadomo, czym jest „Wspólna Kasa” (czytelnik mógł ją poznać wcześniej, ale wstęp jej nie przypomina). Dodaj pół zdania, np. „naszej aplikacji do dzielenia wydatków”, jeśli tak jest w tutorialu. _← recenzent_wstępu_
  - `język` (sugestia) **a Ty dotąd wiedziałeś**: Zwrot „Ty dotąd wiedziałeś” zakłada płeć czytelnika i jest niespójny z resztą wstępu (my/naprawimy). Lepiej bezosobowo: „Gdy program działa źle, często wiadomo tylko, że coś poszło nie tak”. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/0961-recenzent-wstepu.md) · 9.7 s · $0.0211

### 0962 · decyzja · dział 09 · próba 1

- Wynik: Wstęp wraca do autora.
- Nowe potrzeby (1):
  - `diagram` (blokująca) **diagram**: Diagram jest mylący: strzałka powrotna z „zapisu wersji” wraca do „błędu” bez etykiety, więc nie wiadomo, co znaczy (po zapisie pojawia się nowy błąd? cykl trwa w nieskończoność?). Test stoi po komunikacie, choć testy służą do wykrywania błędów, a komunikat pojawia się przy uruchomieniu; kolejność jest niejasna. Przerysuj: np. „uruchomienie → komunikat lub zły wynik → szukanie przyczyny (debugowanie) → poprawka → test → zapis wersji”, a strzałkę powrotną opisz („test nadal nie przechodzi → wracamy do szukania przyczyny”) i poprowadź z testu, nie z zapisu. Albo usuń diagram. _← recenzent_wstępu_
- 0.0 s

### 0963 · autor_wstępu · dział 09 · próba 2

- Kolejka TODO (12): 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61
- Potrzeby w kolejce przed krokiem (1):
  - `diagram` (blokująca) **diagram**: Diagram jest mylący: strzałka powrotna z „zapisu wersji” wraca do „błędu” bez etykiety, więc nie wiadomo, co znaczy (po zapisie pojawia się nowy błąd? cykl trwa w nieskończoność?). Test stoi po komunikacie, choć testy służą do wykrywania błędów, a komunikat pojawia się przy uruchomieniu; kolejność jest niejasna. Przerysuj: np. „uruchomienie → komunikat lub zły wynik → szukanie przyczyny (debugowanie) → poprawka → test → zapis wersji”, a strzałkę powrotną opisz („test nadal nie przechodzi → wracamy do szukania przyczyny”) i poprowadź z testu, nie z zapisu. Albo usuń diagram. _← recenzent_wstępu_
- Wynik: Wstęp: 83 słów, z diagramem
- [prompt i odpowiedź](_przebieg/0963-autor-wstepu.md) · 4.8 s · $0.0400

### 0964 · recenzent_wstępu · dział 09 · próba 2

- Wynik: 0 blokujących, 0 sugestii.
- [prompt i odpowiedź](_przebieg/0964-recenzent-wstepu.md) · 2.3 s · $0.0134

### 0965 · pisarz · dział 09 · pytanie 50 · próba 1

- Kolejka TODO (11): 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61
- Wynik: „Błąd składni a błąd logiczny”: 225 słów prozy, ```python 2 linii, ```text 1 linii; nowe hasła: błąd składni, błąd logiczny; warsztat: blad_skladni.py, $ python blad_skladni.py (błąd), blad_logiczny.py, $ python blad_logiczny.py
- [prompt i odpowiedź](_przebieg/0965-pisarz.md) · 27.0 s · $0.1097

### 0966 · kontrola_deterministyczna · dział 09 · pytanie 50 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0967 · weryfikator_pojęć · dział 09 · pytanie 50 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0967-weryfikator-pojec.md) · 5.8 s · $0.0229

### 0968 · znudzony_czytelnik · dział 09 · pytanie 50 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `przykład` (blokująca) **Błąd składni**: Błąd logiczny ma pełny przykład (kod i wynik), a błąd składni tylko wyliczankę w prozie. Nie widzę, jak wygląda zły zapis ani komunikat Pythona ze wskazaną linią. Twierdzenie, że Python nie wykona nawet linii przed błędem, jest nieprzekonujące bez pokazania. Wystarczy 2–3 linie, np. `print("start")` i `if suma > 10` bez dwukropka, do tego wynik `text` z komunikatem, w którym nie ma wypisanego „start”. Żeby zmieścić się w limicie, można skrócić tabelę albo powtórzenie w pierwszym akapicie. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0968-znudzony-czytelnik.md) · 9.8 s · $0.0244

### 0969 · strażnik_przykład · dział 09 · pytanie 50 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **suma / liczba_osob**: Przykład używa gołych liczb (`suma / 2`) i lokalnej `suma` bez kontekstu. Dla spójności z kanonem można napisać `liczba_osob = 3` i `suma / 2` zastąpić błędnym dzielnikiem, np. `liczba_osob = 2` z komentarzem, że powinno być 3. Albo użyć `udzial_na_osobe(suma, 2)`. Wtedy błąd logiczny dotyczy znanych nazw z wątku. Obliczenia są poprawne (78 / 2 = 39.0, 78 / 3 = 26.0). _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0969-straznik-przyklad.md) · 9.7 s · $0.0303

### 0970 · strażnik_warsztat · dział 09 · pytanie 50 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `spójność` (blokująca) **zdanie „Podobnie działał zły wpis `-5` z poprzedniej sekcji”**: Odwołanie nie zgadza się ze stanem czytelnika. W pytaj.py funkcja sprawdz_kwote odrzuca „-5”, bo "-5".isdigit() daje False. Program wypisze wtedy „To nie jest poprawna kwota...” i zapyta ponownie. Nie będzie więc ani braku komunikatu, ani złego wyniku. Czytelnik, który wpisze -5, zobaczy coś przeciwnego niż w tekście. Zastąp to zdanie odwołaniem prawdziwym dla tego stanu, np. „Tak samo zachowałby się program, który przyjmuje dowolną kwotę bez sprawdzania: zapisałby złą wartość bez ostrzeżenia”. Możesz też po prostu usunąć to zdanie. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0970-straznik-warsztat.md) · 12.6 s · $0.0351

### 0971 · weryfikator_odwołań · dział 09 · pytanie 50 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **Tabela, wiersz „Kiedy wychodzi”**: „w trakcie i po nim” jest mało konkretne. Lepiej: „dopiero gdy porównasz wynik z oczekiwanym”, bo błąd logiczny sam się nie ujawnia. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0971-weryfikator-odwolan.md) · 16.1 s · $0.0498

### 0972 · sprawdzacz_wyników · dział 09 · pytanie 50 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0972-sprawdzacz-wynikow.md) · 4.4 s · $0.0153

### 0973 · weryfikator_faktów · dział 09 · pytanie 50 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/0973-weryfikator-faktow.md) · 6.1 s · $0.0294

### 0974 · decyzja · dział 09 · pytanie 50 · próba 1

- Potrzeby w kolejce przed krokiem (2):
  - `przykład` (blokująca) **Błąd składni**: Błąd logiczny ma pełny przykład (kod i wynik), a błąd składni tylko wyliczankę w prozie. Nie widzę, jak wygląda zły zapis ani komunikat Pythona ze wskazaną linią. Twierdzenie, że Python nie wykona nawet linii przed błędem, jest nieprzekonujące bez pokazania. Wystarczy 2–3 linie, np. `print("start")` i `if suma > 10` bez dwukropka, do tego wynik `text` z komunikatem, w którym nie ma wypisanego „start”. Żeby zmieścić się w limicie, można skrócić tabelę albo powtórzenie w pierwszym akapicie. _← znudzony_czytelnik_
  - `spójność` (blokująca) **zdanie „Podobnie działał zły wpis `-5` z poprzedniej sekcji”**: Odwołanie nie zgadza się ze stanem czytelnika. W pytaj.py funkcja sprawdz_kwote odrzuca „-5”, bo "-5".isdigit() daje False. Program wypisze wtedy „To nie jest poprawna kwota...” i zapyta ponownie. Nie będzie więc ani braku komunikatu, ani złego wyniku. Czytelnik, który wpisze -5, zobaczy coś przeciwnego niż w tekście. Zastąp to zdanie odwołaniem prawdziwym dla tego stanu, np. „Tak samo zachowałby się program, który przyjmuje dowolną kwotę bez sprawdzania: zapisałby złą wartość bez ostrzeżenia”. Możesz też po prostu usunąć to zdanie. _← strażnik_warsztat_
- Wynik: Do poprawy: 2 blokujących potrzeb wraca do pisarza; 2 sugestii trafia do raportu.
- 0.0 s

### 0975 · pisarz · dział 09 · pytanie 50 · próba 2

- Kolejka TODO (11): 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61
- Potrzeby w kolejce przed krokiem (2):
  - `przykład` (blokująca) **Błąd składni**: Błąd logiczny ma pełny przykład (kod i wynik), a błąd składni tylko wyliczankę w prozie. Nie widzę, jak wygląda zły zapis ani komunikat Pythona ze wskazaną linią. Twierdzenie, że Python nie wykona nawet linii przed błędem, jest nieprzekonujące bez pokazania. Wystarczy 2–3 linie, np. `print("start")` i `if suma > 10` bez dwukropka, do tego wynik `text` z komunikatem, w którym nie ma wypisanego „start”. Żeby zmieścić się w limicie, można skrócić tabelę albo powtórzenie w pierwszym akapicie. _← znudzony_czytelnik_
  - `spójność` (blokująca) **zdanie „Podobnie działał zły wpis `-5` z poprzedniej sekcji”**: Odwołanie nie zgadza się ze stanem czytelnika. W pytaj.py funkcja sprawdz_kwote odrzuca „-5”, bo "-5".isdigit() daje False. Program wypisze wtedy „To nie jest poprawna kwota...” i zapyta ponownie. Nie będzie więc ani braku komunikatu, ani złego wyniku. Czytelnik, który wpisze -5, zobaczy coś przeciwnego niż w tekście. Zastąp to zdanie odwołaniem prawdziwym dla tego stanu, np. „Tak samo zachowałby się program, który przyjmuje dowolną kwotę bez sprawdzania: zapisałby złą wartość bez ostrzeżenia”. Możesz też po prostu usunąć to zdanie. _← strażnik_warsztat_
- Wynik: „Błąd składni a błąd logiczny”: 149 słów prozy, ```python 4 linii, ```text 4 linii, ```python 2 linii, ```text 1 linii; nowe hasła: błąd składni, błąd logiczny
- [prompt i odpowiedź](_przebieg/0975-pisarz.md) · 19.6 s · $0.1096

### 0976 · kontrola_deterministyczna · dział 09 · pytanie 50 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0977 · weryfikator_pojęć · dział 09 · pytanie 50 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0977-weryfikator-pojec.md) · 5.7 s · $0.0222

### 0978 · znudzony_czytelnik · dział 09 · pytanie 50 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `przykład` (blokująca) **Błąd składni**: Błąd logiczny ma pełny przykład (kod i wynik), a błąd składni tylko wyliczankę w prozie. Nie widzę, jak wygląda zły zapis ani komunikat Pythona ze wskazaną linią. Twierdzenie, że Python nie wykona nawet linii przed błędem, jest nieprzekonujące bez pokazania. Wystarczy 2–3 linie, np. `print("start")` i `if suma > 10` bez dwukropka, do tego wynik `text` z komunikatem, w którym nie ma wypisanego „start”. Żeby zmieścić się w limicie, można skrócić tabelę albo powtórzenie w pierwszym akapicie. _← znudzony_czytelnik_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0978-znudzony-czytelnik.md) · 4.7 s · $0.0211

### 0979 · strażnik_przykład · dział 09 · pytanie 50 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **liczba_osob**: W przykładzie błędu logicznego dzielnik 2 jest wpisany na sztywno. Kanon ma zmienną liczba_osob = 3. Można zapisać liczba_osob = 2 (pomyłka) i suma / liczba_osob. Wtedy przykład pokazuje, że błąd tkwi w wartości, a nie w zapisie, i pasuje do wątku. Nazwy i typy z kanonu (suma jako liczba, kwota 45.5) są zgodne. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0979-straznik-przyklad.md) · 10.4 s · $0.0299

### 0980 · strażnik_warsztat · dział 09 · pytanie 50 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **zdanie „Podobnie działał zły wpis `-5` z poprzedniej sekcji”**: Odwołanie nie zgadza się ze stanem czytelnika. W pytaj.py funkcja sprawdz_kwote odrzuca „-5”, bo "-5".isdigit() daje False. Program wypisze wtedy „To nie jest poprawna kwota...” i zapyta ponownie. Nie będzie więc ani braku komunikatu, ani złego wyniku. Czytelnik, który wpisze -5, zobaczy coś przeciwnego niż w tekście. Zastąp to zdanie odwołaniem prawdziwym dla tego stanu, np. „Tak samo zachowałby się program, który przyjmuje dowolną kwotę bez sprawdzania: zapisałby złą wartość bez ostrzeżenia”. Możesz też po prostu usunąć to zdanie. _← strażnik_warsztat_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0980-straznik-warsztat.md) · 5.0 s · $0.0270

### 0981 · weryfikator_odwołań · dział 09 · pytanie 50 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- [prompt i odpowiedź](_przebieg/0981-weryfikator-odwolan.md) · 8.6 s · $0.0320

### 0982 · sprawdzacz_wyników · dział 09 · pytanie 50 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/0982-sprawdzacz-wynikow.md) · 4.8 s · $0.0147

### 0983 · weryfikator_faktów · dział 09 · pytanie 50 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **Komunikat SyntaxError: expected ':' i pozycja karetki**: Dokumentacja (https://docs.python.org/3.13/tutorial/errors.html) pokazuje format: plik i linia, powtórzona linia kodu, strzałki, typ i komunikat; sama nie podaje dokładnego tekstu 'expected ':''. Ten komunikat dla brakującego dwukropka po if jest w Pythonie 3.10+ zgodny z 3.13, ale karetka bywa dokładnie pod miejscem błędu (tu za '10'), a plik w prawdziwym uruchomieniu pokaże pełną ścieżkę. Szkic jest akceptowalny; można dodać zastrzeżenie, że wygląd komunikatu może się nieco różnić. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0983-weryfikator-faktow.md) · 16.8 s · $0.0609

### 0984 · decyzja · dział 09 · pytanie 50 · próba 2

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 0985 · akceptacja · dział 09 · pytanie 50

- Wynik: Sekcja [sec-09-blad-skladni-a-blad-logiczny] dopisana do działu 09; hasła w glosariuszu: błąd składni, błąd logiczny; odwołania: w przód „Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu”; punkty zaczepienia: zły dzielnik: 39.0 zamiast 26.0, start nie wypisany; w TODO zostało 11.
- 0.0 s

### 0986 · łowca_pułapek · dział 09 · pytanie 50

- Wynik: „Błąd składni a błąd logiczny”: brak pułapek
- [prompt i odpowiedź](_przebieg/0986-lowca-pulapek.md) · 2.2 s · $0.0136

### 0987 · autor_dodatków · dział 09 · pytanie 50

- Wynik: „Błąd składni a błąd logiczny”: wtręty: Marta ufa ciszy zamiast rachunkowi, dykteryjki: Raport, który wyglądał wiarygodnie
- [prompt i odpowiedź](_przebieg/0987-autor-dodatkow.md) · 12.9 s · $0.0882

### 0988 · weryfikator_dodatków · dział 09 · pytanie 50

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/0988-weryfikator-dodatkow.md) · 8.8 s · $0.0802

### 0989 · pisarz · dział 09 · pytanie 51 · próba 1

- Kolejka TODO (10): 52, 53, 54, 55, 56, 57, 58, 59, 60, 61
- Wynik: „Jak czytać komunikat o błędzie”: 187 słów prozy, ```python 5 linii, ```text 9 linii; nowe hasła: Traceback, komunikat o błędzie; warsztat: blad_pusta.py, $ python blad_pusta.py (błąd), blad_pusta.py, $ python blad_pusta.py
- [prompt i odpowiedź](_przebieg/0989-pisarz.md) · 36.0 s · $0.1218

### 0990 · kontrola_deterministyczna · dział 09 · pytanie 51 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 0991 · weryfikator_pojęć · dział 09 · pytanie 51 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/0991-weryfikator-pojec.md) · 5.1 s · $0.0219

### 0992 · znudzony_czytelnik · dział 09 · pytanie 51 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `fakt` (blokująca) **blok text z tracebackiem, `line 6`**: Numer linii w tracebacku nie zgadza się z kodem. Wywołanie `print(na_osobe(0, 0))` jest w linii 5 (1 def, 2 return, 3 pusta, 4 print Start, 5 print(na_osobe...)), a komunikat pokazuje `line 6`. Sekcja uczy, żeby znaleźć numer linii w śladzie, więc czytelnik, który policzy linie, uzna, że robi coś źle. Popraw na `line 5`. Uwaga o innych numerach u czytelnika wtedy nie musi tego tłumaczyć. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/0992-znudzony-czytelnik.md) · 10.6 s · $0.0259

### 0993 · strażnik_przykład · dział 09 · pytanie 51 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **blad_pusta.py**: Nowy plik blad_pusta.py nie jest w kanonie ani w zadeklarowanych zmianach. Zadeklaruj go w canon_changes jako „dodaj” (plik programu, wspolna_kasa/blad_pusta.py) albo użyj kanonicznego rozlicz.py. _← strażnik_przykład_
  - `spójność` (sugestia) **ślad wywołań (numer linii)**: Wywołanie print(na_osobe(0, 0)) jest w pliku w linii 5 (1 def, 2 return, 3 pusta, 4 print Start, 5 print(na_osobe...)), a ślad pokazuje „line 6”. Popraw na line 5 albo dodaj pustą linię w kodzie. Uwaga o innych numerach linii nie usprawiedliwia niespójności w samym przykładzie. _← strażnik_przykład_
  - `spójność` (sugestia) **na_osobe**: Deklaracja zgodna z kanonem. Przykład dzieli 0 przez 0, a wątek działu mówi o pustej liście wydatków. Warto jednym zdaniem powiązać to z wątkiem, np. że pusta lista daje sumę 0 i liczbę osób 0. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/0993-straznik-przyklad.md) · 14.7 s · $0.0359

### 0994 · strażnik_warsztat · dział 09 · pytanie 51 · próba 1

- Wynik: 2 blokujących, 0 sugestii.
- Nowe potrzeby (2):
  - `wynik` (blokująca) **blok ```text w tekście sekcji, druga ramka śladu**: W tekście sekcji traceback ma przy funkcji na_osobe „line 2”, a w kroku 2 (i w prawdziwym wyniku) jest „line 3”. Poprawić na: `  File "/home/ania/wspolna_kasa/blad_pusta.py", line 3, in na_osobe`. _← strażnik_warsztat_
  - `spójność` (blokująca) **blok ```python w tekście sekcji**: Blok kodu w tekście sekcji nie ma pierwszej linii z komentarza `# blad_pusta.py - Traceback: dzielenie przez zero`, którą ma plik z kroku 1. Bez niej numery linii (6 i 3) nie zgadzają się z kodem: print(na_osobe(0, 0)) byłby w linii 5, a return w linii 2. Dodać ten komentarz jako pierwszą linię bloku kodu, wtedy numery 6 i 3 są prawdziwe. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/0994-straznik-warsztat.md) · 16.6 s · $0.0402

### 0995 · weryfikator_odwołań · dział 09 · pytanie 51 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **ślad: line 6, in <module>**: W przykładowym kodzie wywołanie `print(na_osobe(0, 0))` jest w linii 5 (def=1, return=2, pusta=3, print Start=4), a ślad mówi „line 6”. Czytelnik, który policzy linie, się zdziesiątkuje. Popraw numer w śladzie na 5 albo dodaj do kodu linię (np. pustą lub komentarz), by numer się zgadzał. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/0995-weryfikator-odwolan.md) · 13.0 s · $0.0395

### 0996 · sprawdzacz_wyników · dział 09 · pytanie 51 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `wynik` (blokująca) **Blok text z Traceback pod kodem na_osobe**: W pokazanym kodzie `print(na_osobe(0, 0))` jest w linii 5 (1: def, 2: return, 3: pusta, 4: print("Start"), 5: print(na_osobe...)). Wynik podaje `line 6, in <module>`. Popraw na `File "/home/ania/wspolna_kasa/blad_pusta.py", line 5, in <module>`. Reszta wyniku (Start, linia 2 w na_osobe, znaki ~ i ^, ZeroDivisionError: division by zero) zgadza się z kodem. Uwaga „numery linii będą inne” nie usprawiedliwia niezgodności z pokazanym kodem. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/0996-sprawdzacz-wynikow.md) · 11.8 s · $0.0235

### 0997 · weryfikator_faktów · dział 09 · pytanie 51 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (źródła: 2)
- Nowe potrzeby (2):
  - `fakt` (sugestia) **Znaki `^` i `~` wskazują fragment linii**: Dokumentacja (https://docs.python.org/3.13/tutorial/errors.html) pokazuje ten sam mechanizm, np. `~^~` pod `(1/0)`. Twoje znaczniki `~~~~~~~~^^^^^^` i `~~~~~^~~~~~~` są zgodne z zasadą działania Pythona 3.13. Dokładne rozmieszczenie zależy od wyrażenia, więc warto dopisać, że 'u Ciebie znaki mogą wyglądać nieco inaczej'. To nie błąd. _← weryfikator_faktów_
  - `fakt` (sugestia) **opis `division by zero`**: Dokumentacja pokazuje `ZeroDivisionError: division by zero` dla dzielenia `/` (tutorial errors). Strona wyjątków nie podaje dokładnego tekstu, ale przykład w tutorialu go potwierdza. Sekcja jest zgodna. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/0997-weryfikator-faktow.md) · 17.0 s · $0.0899

### 0998 · decyzja · dział 09 · pytanie 51 · próba 1

- Potrzeby w kolejce przed krokiem (4):
  - `fakt` (blokująca) **blok text z tracebackiem, `line 6`**: Numer linii w tracebacku nie zgadza się z kodem. Wywołanie `print(na_osobe(0, 0))` jest w linii 5 (1 def, 2 return, 3 pusta, 4 print Start, 5 print(na_osobe...)), a komunikat pokazuje `line 6`. Sekcja uczy, żeby znaleźć numer linii w śladzie, więc czytelnik, który policzy linie, uzna, że robi coś źle. Popraw na `line 5`. Uwaga o innych numerach u czytelnika wtedy nie musi tego tłumaczyć. _← znudzony_czytelnik_
  - `wynik` (blokująca) **blok ```text w tekście sekcji, druga ramka śladu**: W tekście sekcji traceback ma przy funkcji na_osobe „line 2”, a w kroku 2 (i w prawdziwym wyniku) jest „line 3”. Poprawić na: `  File "/home/ania/wspolna_kasa/blad_pusta.py", line 3, in na_osobe`. _← strażnik_warsztat_
  - `spójność` (blokująca) **blok ```python w tekście sekcji**: Blok kodu w tekście sekcji nie ma pierwszej linii z komentarza `# blad_pusta.py - Traceback: dzielenie przez zero`, którą ma plik z kroku 1. Bez niej numery linii (6 i 3) nie zgadzają się z kodem: print(na_osobe(0, 0)) byłby w linii 5, a return w linii 2. Dodać ten komentarz jako pierwszą linię bloku kodu, wtedy numery 6 i 3 są prawdziwe. _← strażnik_warsztat_
  - `wynik` (blokująca) **Blok text z Traceback pod kodem na_osobe**: W pokazanym kodzie `print(na_osobe(0, 0))` jest w linii 5 (1: def, 2: return, 3: pusta, 4: print("Start"), 5: print(na_osobe...)). Wynik podaje `line 6, in <module>`. Popraw na `File "/home/ania/wspolna_kasa/blad_pusta.py", line 5, in <module>`. Reszta wyniku (Start, linia 2 w na_osobe, znaki ~ i ^, ZeroDivisionError: division by zero) zgadza się z kodem. Uwaga „numery linii będą inne” nie usprawiedliwia niezgodności z pokazanym kodem. _← sprawdzacz_wyników_
- Wynik: Do poprawy: 4 blokujących potrzeb wraca do pisarza; 6 sugestii trafia do raportu.
- 0.0 s

### 0999 · pisarz · dział 09 · pytanie 51 · próba 2

- Kolejka TODO (10): 52, 53, 54, 55, 56, 57, 58, 59, 60, 61
- Potrzeby w kolejce przed krokiem (4):
  - `fakt` (blokująca) **blok text z tracebackiem, `line 6`**: Numer linii w tracebacku nie zgadza się z kodem. Wywołanie `print(na_osobe(0, 0))` jest w linii 5 (1 def, 2 return, 3 pusta, 4 print Start, 5 print(na_osobe...)), a komunikat pokazuje `line 6`. Sekcja uczy, żeby znaleźć numer linii w śladzie, więc czytelnik, który policzy linie, uzna, że robi coś źle. Popraw na `line 5`. Uwaga o innych numerach u czytelnika wtedy nie musi tego tłumaczyć. _← znudzony_czytelnik_
  - `wynik` (blokująca) **blok ```text w tekście sekcji, druga ramka śladu**: W tekście sekcji traceback ma przy funkcji na_osobe „line 2”, a w kroku 2 (i w prawdziwym wyniku) jest „line 3”. Poprawić na: `  File "/home/ania/wspolna_kasa/blad_pusta.py", line 3, in na_osobe`. _← strażnik_warsztat_
  - `spójność` (blokująca) **blok ```python w tekście sekcji**: Blok kodu w tekście sekcji nie ma pierwszej linii z komentarza `# blad_pusta.py - Traceback: dzielenie przez zero`, którą ma plik z kroku 1. Bez niej numery linii (6 i 3) nie zgadzają się z kodem: print(na_osobe(0, 0)) byłby w linii 5, a return w linii 2. Dodać ten komentarz jako pierwszą linię bloku kodu, wtedy numery 6 i 3 są prawdziwe. _← strażnik_warsztat_
  - `wynik` (blokująca) **Blok text z Traceback pod kodem na_osobe**: W pokazanym kodzie `print(na_osobe(0, 0))` jest w linii 5 (1: def, 2: return, 3: pusta, 4: print("Start"), 5: print(na_osobe...)). Wynik podaje `line 6, in <module>`. Popraw na `File "/home/ania/wspolna_kasa/blad_pusta.py", line 5, in <module>`. Reszta wyniku (Start, linia 2 w na_osobe, znaki ~ i ^, ZeroDivisionError: division by zero) zgadza się z kodem. Uwaga „numery linii będą inne” nie usprawiedliwia niezgodności z pokazanym kodem. _← sprawdzacz_wyników_
- Wynik: „Jak czytać komunikat o błędzie”: 185 słów prozy, ```python 6 linii, ```text 9 linii; nowe hasła: Traceback, komunikat o błędzie; warsztat: blad_pusta.py, $ python blad_pusta.py (błąd)
- [prompt i odpowiedź](_przebieg/0999-pisarz.md) · 21.0 s · $0.1166

### 1000 · kontrola_deterministyczna · dział 09 · pytanie 51 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1001 · weryfikator_pojęć · dział 09 · pytanie 51 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1001-weryfikator-pojec.md) · 5.6 s · $0.0231

### 1002 · znudzony_czytelnik · dział 09 · pytanie 51 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `fakt` (blokująca) **blok text z tracebackiem, `line 6`**: Numer linii w tracebacku nie zgadza się z kodem. Wywołanie `print(na_osobe(0, 0))` jest w linii 5 (1 def, 2 return, 3 pusta, 4 print Start, 5 print(na_osobe...)), a komunikat pokazuje `line 6`. Sekcja uczy, żeby znaleźć numer linii w śladzie, więc czytelnik, który policzy linie, uzna, że robi coś źle. Popraw na `line 5`. Uwaga o innych numerach u czytelnika wtedy nie musi tego tłumaczyć. _← znudzony_czytelnik_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1002-znudzony-czytelnik.md) · 5.1 s · $0.0221

### 1003 · strażnik_przykład · dział 09 · pytanie 51 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **blad_pusta.py**: Kod zgadza się z kanonem (na_osobe(suma, osoby) zwraca suma / osoby, numery linii w tracebacku pasują). Wątek z opisu działu to dzielenie przez zero przy pustej liście, a przykład wywołuje na_osobe(0, 0). Możesz to powiązać z wątkiem jednym zdaniem, np. że 0 to liczba osób na pustej liście. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1003-straznik-przyklad.md) · 10.1 s · $0.0309

### 1004 · strażnik_warsztat · dział 09 · pytanie 51 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `wynik` (blokująca) **blok ```text w tekście sekcji, druga ramka śladu**: W tekście sekcji traceback ma przy funkcji na_osobe „line 2”, a w kroku 2 (i w prawdziwym wyniku) jest „line 3”. Poprawić na: `  File "/home/ania/wspolna_kasa/blad_pusta.py", line 3, in na_osobe`. _← strażnik_warsztat_
  - `spójność` (blokująca) **blok ```python w tekście sekcji**: Blok kodu w tekście sekcji nie ma pierwszej linii z komentarza `# blad_pusta.py - Traceback: dzielenie przez zero`, którą ma plik z kroku 1. Bez niej numery linii (6 i 3) nie zgadzają się z kodem: print(na_osobe(0, 0)) byłby w linii 5, a return w linii 2. Dodać ten komentarz jako pierwszą linię bloku kodu, wtedy numery 6 i 3 są prawdziwe. _← strażnik_warsztat_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1004-straznik-warsztat.md) · 6.0 s · $0.0303

### 1005 · weryfikator_odwołań · dział 09 · pytanie 51 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/1005-weryfikator-odwolan.md) · 8.3 s · $0.0351

### 1006 · sprawdzacz_wyników · dział 09 · pytanie 51 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wynik` (blokująca) **Blok text z Traceback pod kodem na_osobe**: W pokazanym kodzie `print(na_osobe(0, 0))` jest w linii 5 (1: def, 2: return, 3: pusta, 4: print("Start"), 5: print(na_osobe...)). Wynik podaje `line 6, in <module>`. Popraw na `File "/home/ania/wspolna_kasa/blad_pusta.py", line 5, in <module>`. Reszta wyniku (Start, linia 2 w na_osobe, znaki ~ i ^, ZeroDivisionError: division by zero) zgadza się z kodem. Uwaga „numery linii będą inne” nie usprawiedliwia niezgodności z pokazanym kodem. _← sprawdzacz_wyników_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1006-sprawdzacz-wynikow.md) · 15.1 s · $0.0277

### 1007 · weryfikator_faktów · dział 09 · pytanie 51 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 2)
- [prompt i odpowiedź](_przebieg/1007-weryfikator-faktow.md) · 20.1 s · $0.1064

### 1008 · decyzja · dział 09 · pytanie 51 · próba 2

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 1009 · akceptacja · dział 09 · pytanie 51

- Wynik: Sekcja [sec-09-jak-czytac-komunikat-o-bledzie] dopisana do działu 09; hasła w glosariuszu: Traceback, komunikat o błędzie; odwołania: wstecz „Inaczej niż przy błędzie składni ze „Startem”, który się nie pojawił”, w przód „Szukanie przyczyny krok po kroku omówimy przy debugowaniu”; punkty zaczepienia: czytaj od dołu, start się wypisał; w TODO zostało 10.
- 0.0 s

### 1010 · łowca_pułapek · dział 09 · pytanie 51

- Wynik: „Jak czytać komunikat o błędzie”: brak pułapek
- [prompt i odpowiedź](_przebieg/1010-lowca-pulapek.md) · 2.2 s · $0.0170

### 1011 · autor_dodatków · dział 09 · pytanie 51

- Wynik: „Jak czytać komunikat o błędzie”: dowcipy: Ślad wywołań jako „to nie ja”, rysunki: Ślad stóp prowadzi do kałuży
- [prompt i odpowiedź](_przebieg/1011-autor-dodatkow.md) · 13.7 s · $0.0891

### 1012 · weryfikator_dodatków · dział 09 · pytanie 51

- Wynik: odrzucone: 1; Ślad stóp prowadzi do kałuży: Mokre ślady powstają po wejściu w wodę, więc nie mogą prowadzić od drzwi do kałuży (kot z mokrymi łapkami stoi na końcu), a zdanie o śladach „ponumerowanych tylko kształtem” jest niezrozumiałe, więc scena jest wewnętrznie niespójna.
- [prompt i odpowiedź](_przebieg/1012-weryfikator-dodatkow.md) · 13.2 s · $0.0844

### 1013 · pisarz · dział 09 · pytanie 52 · próba 1

- Kolejka TODO (9): 53, 54, 55, 56, 57, 58, 59, 60, 61
- Wynik: „Czym jest testowanie programu”: 149 słów prozy, ```python 7 linii, ```text 1 linii; nowe hasła: testowanie, assert; wątki: przykład dodaj test_rozlicz.py; warsztat: test_kasa.py, $ python test_kasa.py
- [prompt i odpowiedź](_przebieg/1013-pisarz.md) · 25.5 s · $0.1119

### 1014 · kontrola_deterministyczna · dział 09 · pytanie 52 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1015 · weryfikator_pojęć · dział 09 · pytanie 52 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1015-weryfikator-pojec.md) · 6.3 s · $0.0225

### 1016 · znudzony_czytelnik · dział 09 · pytanie 52 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `konkret` (sugestia) **przypadki brzegowe, pusta lista wydatków**: Przypadek brzegowy jest tylko wspomniany, a przykład (lista wydatków) nie pasuje do funkcji na_osobe, która listy nie przyjmuje. Lepiej wskazać brzeg z kodu: na_osobe(0, 0) z poprzedniej sekcji kończy się ZeroDivisionError, więc test pokazałby ten brzeg. Jedno zdanie wystarczy. _← znudzony_czytelnik_
  - `odwołanie` (sugestia) **jak przy błędzie z niewłaściwym dzielnikiem**: Odwołanie do błędu, którego czytelnik nie widział (poprzednia sekcja pokazywała dzielenie przez zero). Należy je zastąpić konkretem, np. „gdyby ktoś zamienił / na *”, albo odnieść się do dzielenia przez zero. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1016-znudzony-czytelnik.md) · 9.3 s · $0.0247

### 1017 · strażnik_przykład · dział 09 · pytanie 52 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `spójność` (sugestia) **test_rozlicz.py**: Autor zadeklarował dodanie test_rozlicz.py z dwoma asercjami (78/3 i 0/4). Blok w sekcji ma trzy asercje (dodatkowo na_osobe(100, 4) == 25) oraz print i nie mówi, że to zawartość test_rozlicz.py. Wpisz nazwę pliku w komentarzu na początku bloku i zrównaj zawartość z deklaracją albo zaktualizuj deklarację. Dopisz też, że definicja na_osobe jest tu tylko skrótem (w rzeczywistości byłby import z funkcje.py). _← strażnik_przykład_
  - `spójność` (sugestia) **pusta lista wydatków**: Tekst wymienia „pustą listę wydatków” jako przypadek brzegowy, ale test na_osobe(0, 4) == 0 sprawdza sumę równą 0, a nie pustą listę. Przypadek z wątku, czyli dzielenie przez zero (osoby = 0), nie jest pokazany. Zmień przykład na suma_wydatkow([]) == 0 albo opisz na_osobe(0, 4) jako „sumę zero”. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1017-straznik-przyklad.md) · 10.8 s · $0.0310

### 1018 · strażnik_warsztat · dział 09 · pytanie 52 · próba 1

- Wynik: 0 blokujących, 3 sugestii.
- Nowe potrzeby (3):
  - `spójność` (sugestia) **Sekcja: assert i AssertionError**: Tekst opisuje, że fałszywy assert zatrzymuje program błędem AssertionError i wskazuje linię, ale nie pokazuje takiego wyniku. Warto dodać krótki przykład, np. `assert na_osobe(100, 4) == 20`, i wynik: `Traceback (most recent call last): ... AssertionError`. _← strażnik_warsztat_
  - `spójność` (sugestia) **Akapit „Cisza po assert”**: Fraza „jak przy błędzie z niewłaściwym dzielnikiem” jest niejasna. Wcześniejszy błąd w stanie czytelnika to dzielenie przez zero (blad_pusta.py). Lepiej napisać konkretnie, np. „gdyby ktoś zamienił dzielenie na mnożenie”. _← strażnik_warsztat_
  - `spójność` (sugestia) **Akapit o przypadkach brzegowych**: Tekst wspomina o pustej liście wydatków jako przypadku brzegowym, ale kod w sekcji tego nie pokazuje (jest tam `na_osobe(0, 4)`). Można dodać przykład `assert suma([]) == 0`, który jest w test_kasa.py. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/1018-straznik-warsztat.md) · 15.8 s · $0.0392

### 1019 · weryfikator_odwołań · dział 09 · pytanie 52 · próba 1

- Wynik: 0 blokujących, 2 sugestii. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (sugestia) **Gdy test się wywali**: Potoczne „się wywali” zastąp neutralnym, np. „Gdy test się nie powiedzie”. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **przypadki brzegowe**: Przypadek brzegowy „pusta lista wydatków” jest tylko wspomniany, a kod testuje sumę 0. Można dodać jedno zdanie wiążące go z przykładem albo zamienić na „sumę równą 0”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/1019-weryfikator-odwolan.md) · 11.3 s · $0.0373

### 1020 · sprawdzacz_wyników · dział 09 · pytanie 52 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **przypadki brzegowe**: Przypadki brzegowe są wspomniane (pusta lista wydatków), ale kod ich nie pokazuje. Można dodać krótki test, np. co się dzieje przy `na_osobe(100, 0)` (ZeroDivisionError), albo zmienić przykład na taki, który występuje w kodzie (`na_osobe(0, 4)`). _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/1020-sprawdzacz-wynikow.md) · 6.6 s · $0.0164

### 1021 · weryfikator_faktów · dział 09 · pytanie 52 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/1021-weryfikator-faktow.md) · 5.1 s · $0.0277

### 1022 · decyzja · dział 09 · pytanie 52 · próba 1

- Wynik: Sekcja przyjęta; 10 sugestii trafia do raportu.
- 0.0 s

### 1023 · akceptacja · dział 09 · pytanie 52

- Wynik: Sekcja [sec-09-czym-jest-testowanie-programu] dopisana do działu 09; hasła w glosariuszu: testowanie, assert; kanony: przykład:+test_rozlicz.py; odwołania: wstecz „jak przy błędzie z niewłaściwym dzielnikiem”, w przód „szukanie przyczyny omówimy przy debugowaniu”; punkty zaczepienia: cisza po assert; w TODO zostało 9.
- 0.0 s

### 1024 · łowca_pułapek · dział 09 · pytanie 52

- Wynik: „Czym jest testowanie programu”: assert znika przy uruchomieniu z -O
- [prompt i odpowiedź](_przebieg/1024-lowca-pulapek.md) · 7.6 s · $0.0208

### 1025 · autor_dodatków · dział 09 · pytanie 52

- Wynik: „Czym jest testowanie programu”: rysunki: Mostek próbowany różnymi zabawkami, wtręty: Marta testuje tylko jedną, ulubioną liczbę
- [prompt i odpowiedź](_przebieg/1025-autor-dodatkow.md) · 15.9 s · $0.0890

### 1026 · weryfikator_dodatków · dział 09 · pytanie 52

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/1026-weryfikator-dodatkow.md) · 7.2 s · $0.0780

### 1027 · pisarz · dział 09 · pytanie 53 · próba 1

- Kolejka TODO (8): 54, 55, 56, 57, 58, 59, 60, 61
- Wynik: „Czym jest debugowanie”: 138 słów prozy, ```python 8 linii, ```text 3 linii; nowe hasła: debugowanie; warsztat: debug.py, $ python debug.py, debug.py, $ python debug.py
- [prompt i odpowiedź](_przebieg/1027-pisarz.md) · 28.2 s · $0.1163

### 1028 · kontrola_deterministyczna · dział 09 · pytanie 53 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1029 · weryfikator_pojęć · dział 09 · pytanie 53 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1029-weryfikator-pojec.md) · 4.5 s · $0.0206

### 1030 · znudzony_czytelnik · dział 09 · pytanie 53 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **przykład z na_osobe**: Przykład zaczyna od gotowego „wyniku 39.0 zamiast 26.0”, choć w poprzedniej sekcji test dawał 26 dla 78 i 3 osób; nie wiadomo, skąd wzięło się 2 osoby. Można jednym zdaniem zaznaczyć, że ktoś uruchomił program z błędną liczbą osób. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1030-znudzony-czytelnik.md) · 5.1 s · $0.0183

### 1031 · strażnik_przykład · dział 09 · pytanie 53 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1031-straznik-przyklad.md) · 7.7 s · $0.0271

### 1032 · strażnik_warsztat · dział 09 · pytanie 53 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Sekcja: przykład z wynikiem 39.0**: Tekst mówi „mają być trzy” osoby, ale nigdzie nie wyjaśnia skąd ta oczekiwana wartość (Mazury, 3 osoby, wynik 26.0). Warto dodać zdanie, np. „Na wyjazd na Mazury jedzie troje osób, więc oczekujemy 78.0 / 3 = 26.0”. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/1032-straznik-warsztat.md) · 8.2 s · $0.0318

### 1033 · weryfikator_odwołań · dział 09 · pytanie 53 · próba 1

- Wynik: Brak uwag. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/1033-weryfikator-odwolan.md) · 8.5 s · $0.0360

### 1034 · sprawdzacz_wyników · dział 09 · pytanie 53 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1034-sprawdzacz-wynikow.md) · 4.3 s · $0.0145

### 1035 · weryfikator_faktów · dział 09 · pytanie 53 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/1035-weryfikator-faktow.md) · 5.2 s · $0.0277

### 1036 · decyzja · dział 09 · pytanie 53 · próba 1

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 1037 · akceptacja · dział 09 · pytanie 53

- Wynik: Sekcja [sec-09-czym-jest-debugowanie] dopisana do działu 09; hasła w glosariuszu: debugowanie; odwołania: wstecz „błąd logiczny z wynikiem 39.0 zamiast 26.0”, wstecz „test z poprzedniej sekcji”; punkty zaczepienia: print pokazuje złą liczbę osób; w TODO zostało 8.
- 0.0 s

### 1038 · łowca_pułapek · dział 09 · pytanie 53

- Wynik: „Czym jest debugowanie”: brak pułapek
- [prompt i odpowiedź](_przebieg/1038-lowca-pulapek.md) · 2.4 s · $0.0162

### 1039 · autor_dodatków · dział 09 · pytanie 53

- Wynik: „Czym jest debugowanie”: dygresje: Ćma, która stała się słynnym „bugiem”
- [prompt i odpowiedź](_przebieg/1039-autor-dodatkow.md) · 15.9 s · $0.0913

### 1040 · weryfikator_dodatków · dział 09 · pytanie 53

- Wynik: odrzucone: 1; Ćma, która stała się słynnym „bugiem”: Nie udało się otworzyć wskazanego źródła (Smithsonian zwrócił 403, drugi adres też), więc twierdzeń o ćmie, Harvard Mark II i wrześniu 1947 nie mogę potwierdzić w źródle.
- [prompt i odpowiedź](_przebieg/1040-weryfikator-dodatkow.md) · 8.6 s · $0.1206

### 1041 · pisarz · dział 09 · pytanie 54 · próba 1

- Kolejka TODO (7): 55, 56, 57, 58, 59, 60, 61
- Wynik: „Po co zapisywać wersje kodu”: 170 słów prozy, ```text 3 linii; nowe hasła: Git, commit, repozytorium; wątki: przykład dodaj wspolna_kasa; warsztat: $ git init -b main, $ git add funkcje.py test_kasa.py, $ git commit -m "Funkcje Wspolnej Kasy i testy", $ git log --oneline
- [prompt i odpowiedź](_przebieg/1041-pisarz.md) · 24.5 s · $0.1126

### 1042 · kontrola_deterministyczna · dział 09 · pytanie 54 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1043 · weryfikator_pojęć · dział 09 · pytanie 54 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1043-weryfikator-pojec.md) · 5.0 s · $0.0212

### 1044 · znudzony_czytelnik · dział 09 · pytanie 54 · próba 1

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `przykład` (blokująca) **lista trzech sytuacji**: Sedno odpowiedzi to trzy ogólne punkty (wrócić do działającej wersji, znaleźć, kiedy pojawił się błąd, eksperymentować). Żaden nie ma konkretnego scenariusza, a kod pokazuje tylko, jak zapisać wersję, nie po co. Wystarczy jedno zdanie o „Wspólnej Kasie”. Na przykład: dopisujesz nową funkcję, testy przestają przechodzić, a wracasz do wczorajszego commita zamiast szukać własnych zmian. Można nim zastąpić jeden z punktów, na przykład trzeci, który tylko powtarza pierwszy. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1044-znudzony-czytelnik.md) · 12.1 s · $0.0253

### 1045 · strażnik_przykład · dział 09 · pytanie 54 · próba 1

- Wynik: 2 blokujących, 1 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **test_rozlicz.py**: W poleceniu `git add funkcje.py test_kasa.py` pojawia się plik `test_kasa.py`, a w kanonie plik testów nazywa się `test_rozlicz.py`. Nie ma deklaracji zmiany nazwy. Zamień na `git add funkcje.py test_rozlicz.py`, a komunikat commita dostosuj do tego, co faktycznie w nim jest. _← strażnik_przykład_
  - `spójność` (blokująca) **wspolna_kasa**: Tekst mówi, że repozytorium „będzie to `wspolna_kasa`”, ale `git init -b main` bez argumentu zakłada repozytorium w bieżącym katalogu i nie tworzy katalogu o tej nazwie. Dodaj `git init -b main wspolna_kasa` albo `mkdir wspolna_kasa && cd wspolna_kasa` przed `init`. W kanonie `wspolna_kasa/` jest też katalogiem z `rozlicz.py`, więc warto wyjaśnić, że to ten sam katalog. _← strażnik_przykład_
  - `spójność` (sugestia) **funkcje.py**: W kanonie `funkcje.py` i `test_rozlicz.py` leżą w katalogu głównym, a `rozlicz.py` w `wspolna_kasa/`. Polecenie `git add` nie obejmuje `rozlicz.py`, więc główny plik programu nie trafia do historii. Ujednolić układ plików względem repozytorium albo dodać `rozlicz.py` do `add` i napisać jedno zdanie, gdzie leżą pliki. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1045-straznik-przyklad.md) · 12.8 s · $0.0341

### 1046 · strażnik_warsztat · dział 09 · pytanie 54 · próba 1

- Wynik: 3 blokujących, 0 sugestii.
- Nowe potrzeby (3):
  - `wynik` (blokująca) **Krok 3: git commit**: Liczba wstawień jest błędna. funkcje.py ma 14 linii, a test_kasa.py 8, razem 22. Podana wartość to 21. Popraw drugą linię wyniku na: ` 2 files changed, 22 insertions(+)`. Hasz 3f2a9c1 może zostać, bo u czytelnika i tak będzie inny. _← strażnik_warsztat_
  - `spójność` (blokująca) **Krok 1 (git init) i punkt startowy**: Punkt startowy nie zawiera Gita, a żaden wcześniejszy krok go nie instaluje. Bez niego `git init` da błąd „command not found”. Dodaj przed krokiem 1 krok sprawdzający `git --version` (z przykładowym wynikiem, np. `git version 2.43.0`) i krótką instrukcję instalacji. Alternatywnie dopisz Git do wymagań. _← strażnik_warsztat_
  - `spójność` (blokująca) **Krok 3: git commit**: Na świeżej instalacji Gita `git commit` przerwie się z komunikatem „Author identity unknown *** Please tell me who you are”, dopóki nie ustawisz nazwy i e-maila. Dodaj przed commitem kroki: `git config --global user.name "Twoje Imię"` oraz `git config --global user.email "ty@example.com"` (oba bez wyniku). Możesz też dopisać zdanie, że robi się to jednorazowo. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/1046-straznik-warsztat.md) · 15.6 s · $0.0398

### 1047 · weryfikator_odwołań · dział 09 · pytanie 54 · próba 1

- Wynik: 4 blokujących, 0 sugestii. (odwołania: 2)
- Nowe potrzeby (4):
  - `odwołanie` (blokująca) **git**: Git, commit i repozytorium to kluczowe pojęcia sekcji, a nie mają haseł w glosariuszu. Są zdefiniowane w tekście jednym zdaniem każde, więc to wystarcza. Trzeba jednak dodać hasła do glosariusza albo zostawić definicje w tekście. Uwaga: 'migawka wybranych plików' jest metaforą i wymaga krótkiego dopowiedzenia, co to znaczy dla osoby spoza IT. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Wykonasz to u siebie w warsztacie.**: Obietnica odsyła do 'warsztatu', którego czytelnik może nie znać jako elementu tutorialu, i nie mówi o temacie. Zastąp zdaniem o temacie, np. 'Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym', albo usuń. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.**: 'Wspólna Kasa' to nawiązanie do projektu z wcześniejszych działów, ale żaden punkt zaczepienia ani sekcja tego nie potwierdza. Wyjaśnij na miejscu, że to przykładowy program do dzielenia wydatków, albo usuń nawiązanie. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/1047-weryfikator-odwolan.md) · 13.2 s · $0.0424

### 1048 · decyzja · dział 09 · pytanie 54 · próba 1

- Potrzeby w kolejce przed krokiem (10):
  - `przykład` (blokująca) **lista trzech sytuacji**: Sedno odpowiedzi to trzy ogólne punkty (wrócić do działającej wersji, znaleźć, kiedy pojawił się błąd, eksperymentować). Żaden nie ma konkretnego scenariusza, a kod pokazuje tylko, jak zapisać wersję, nie po co. Wystarczy jedno zdanie o „Wspólnej Kasie”. Na przykład: dopisujesz nową funkcję, testy przestają przechodzić, a wracasz do wczorajszego commita zamiast szukać własnych zmian. Można nim zastąpić jeden z punktów, na przykład trzeci, który tylko powtarza pierwszy. _← znudzony_czytelnik_
  - `spójność` (blokująca) **test_rozlicz.py**: W poleceniu `git add funkcje.py test_kasa.py` pojawia się plik `test_kasa.py`, a w kanonie plik testów nazywa się `test_rozlicz.py`. Nie ma deklaracji zmiany nazwy. Zamień na `git add funkcje.py test_rozlicz.py`, a komunikat commita dostosuj do tego, co faktycznie w nim jest. _← strażnik_przykład_
  - `spójność` (blokująca) **wspolna_kasa**: Tekst mówi, że repozytorium „będzie to `wspolna_kasa`”, ale `git init -b main` bez argumentu zakłada repozytorium w bieżącym katalogu i nie tworzy katalogu o tej nazwie. Dodaj `git init -b main wspolna_kasa` albo `mkdir wspolna_kasa && cd wspolna_kasa` przed `init`. W kanonie `wspolna_kasa/` jest też katalogiem z `rozlicz.py`, więc warto wyjaśnić, że to ten sam katalog. _← strażnik_przykład_
  - `wynik` (blokująca) **Krok 3: git commit**: Liczba wstawień jest błędna. funkcje.py ma 14 linii, a test_kasa.py 8, razem 22. Podana wartość to 21. Popraw drugą linię wyniku na: ` 2 files changed, 22 insertions(+)`. Hasz 3f2a9c1 może zostać, bo u czytelnika i tak będzie inny. _← strażnik_warsztat_
  - `spójność` (blokująca) **Krok 1 (git init) i punkt startowy**: Punkt startowy nie zawiera Gita, a żaden wcześniejszy krok go nie instaluje. Bez niego `git init` da błąd „command not found”. Dodaj przed krokiem 1 krok sprawdzający `git --version` (z przykładowym wynikiem, np. `git version 2.43.0`) i krótką instrukcję instalacji. Alternatywnie dopisz Git do wymagań. _← strażnik_warsztat_
  - `spójność` (blokująca) **Krok 3: git commit**: Na świeżej instalacji Gita `git commit` przerwie się z komunikatem „Author identity unknown *** Please tell me who you are”, dopóki nie ustawisz nazwy i e-maila. Dodaj przed commitem kroki: `git config --global user.name "Twoje Imię"` oraz `git config --global user.email "ty@example.com"` (oba bez wyniku). Możesz też dopisać zdanie, że robi się to jednorazowo. _← strażnik_warsztat_
  - `odwołanie` (blokująca) **git**: Git, commit i repozytorium to kluczowe pojęcia sekcji, a nie mają haseł w glosariuszu. Są zdefiniowane w tekście jednym zdaniem każde, więc to wystarcza. Trzeba jednak dodać hasła do glosariusza albo zostawić definicje w tekście. Uwaga: 'migawka wybranych plików' jest metaforą i wymaga krótkiego dopowiedzenia, co to znaczy dla osoby spoza IT. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Wykonasz to u siebie w warsztacie.**: Obietnica odsyła do 'warsztatu', którego czytelnik może nie znać jako elementu tutorialu, i nie mówi o temacie. Zastąp zdaniem o temacie, np. 'Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym', albo usuń. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.**: 'Wspólna Kasa' to nawiązanie do projektu z wcześniejszych działów, ale żaden punkt zaczepienia ani sekcja tego nie potwierdza. Wyjaśnij na miejscu, że to przykładowy program do dzielenia wydatków, albo usuń nawiązanie. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Do poprawy: 10 blokujących potrzeb wraca do pisarza; 1 sugestii trafia do raportu.
- 0.0 s

### 1049 · pisarz · dział 09 · pytanie 54 · próba 2

- Kolejka TODO (7): 55, 56, 57, 58, 59, 60, 61
- Potrzeby w kolejce przed krokiem (10):
  - `przykład` (blokująca) **lista trzech sytuacji**: Sedno odpowiedzi to trzy ogólne punkty (wrócić do działającej wersji, znaleźć, kiedy pojawił się błąd, eksperymentować). Żaden nie ma konkretnego scenariusza, a kod pokazuje tylko, jak zapisać wersję, nie po co. Wystarczy jedno zdanie o „Wspólnej Kasie”. Na przykład: dopisujesz nową funkcję, testy przestają przechodzić, a wracasz do wczorajszego commita zamiast szukać własnych zmian. Można nim zastąpić jeden z punktów, na przykład trzeci, który tylko powtarza pierwszy. _← znudzony_czytelnik_
  - `spójność` (blokująca) **test_rozlicz.py**: W poleceniu `git add funkcje.py test_kasa.py` pojawia się plik `test_kasa.py`, a w kanonie plik testów nazywa się `test_rozlicz.py`. Nie ma deklaracji zmiany nazwy. Zamień na `git add funkcje.py test_rozlicz.py`, a komunikat commita dostosuj do tego, co faktycznie w nim jest. _← strażnik_przykład_
  - `spójność` (blokująca) **wspolna_kasa**: Tekst mówi, że repozytorium „będzie to `wspolna_kasa`”, ale `git init -b main` bez argumentu zakłada repozytorium w bieżącym katalogu i nie tworzy katalogu o tej nazwie. Dodaj `git init -b main wspolna_kasa` albo `mkdir wspolna_kasa && cd wspolna_kasa` przed `init`. W kanonie `wspolna_kasa/` jest też katalogiem z `rozlicz.py`, więc warto wyjaśnić, że to ten sam katalog. _← strażnik_przykład_
  - `wynik` (blokująca) **Krok 3: git commit**: Liczba wstawień jest błędna. funkcje.py ma 14 linii, a test_kasa.py 8, razem 22. Podana wartość to 21. Popraw drugą linię wyniku na: ` 2 files changed, 22 insertions(+)`. Hasz 3f2a9c1 może zostać, bo u czytelnika i tak będzie inny. _← strażnik_warsztat_
  - `spójność` (blokująca) **Krok 1 (git init) i punkt startowy**: Punkt startowy nie zawiera Gita, a żaden wcześniejszy krok go nie instaluje. Bez niego `git init` da błąd „command not found”. Dodaj przed krokiem 1 krok sprawdzający `git --version` (z przykładowym wynikiem, np. `git version 2.43.0`) i krótką instrukcję instalacji. Alternatywnie dopisz Git do wymagań. _← strażnik_warsztat_
  - `spójność` (blokująca) **Krok 3: git commit**: Na świeżej instalacji Gita `git commit` przerwie się z komunikatem „Author identity unknown *** Please tell me who you are”, dopóki nie ustawisz nazwy i e-maila. Dodaj przed commitem kroki: `git config --global user.name "Twoje Imię"` oraz `git config --global user.email "ty@example.com"` (oba bez wyniku). Możesz też dopisać zdanie, że robi się to jednorazowo. _← strażnik_warsztat_
  - `odwołanie` (blokująca) **git**: Git, commit i repozytorium to kluczowe pojęcia sekcji, a nie mają haseł w glosariuszu. Są zdefiniowane w tekście jednym zdaniem każde, więc to wystarcza. Trzeba jednak dodać hasła do glosariusza albo zostawić definicje w tekście. Uwaga: 'migawka wybranych plików' jest metaforą i wymaga krótkiego dopowiedzenia, co to znaczy dla osoby spoza IT. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Wykonasz to u siebie w warsztacie.**: Obietnica odsyła do 'warsztatu', którego czytelnik może nie znać jako elementu tutorialu, i nie mówi o temacie. Zastąp zdaniem o temacie, np. 'Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym', albo usuń. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.**: 'Wspólna Kasa' to nawiązanie do projektu z wcześniejszych działów, ale żaden punkt zaczepienia ani sekcja tego nie potwierdza. Wyjaśnij na miejscu, że to przykładowy program do dzielenia wydatków, albo usuń nawiązanie. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: „Po co zapisywać wersje kodu”: 200 słów prozy, ```text 3 linii; nowe hasła: Git, commit, repozytorium; wątki: przykład dodaj wspolna_kasa; warsztat: $ git --version, $ git config --global user.name "Twoje Imie", $ git config --global user.email "ty@example.com", $ git init -b main, $ git add funkcje.py test_kasa.py, $ git commit -m "Funkcje Wspolnej Kasy i testy"
- [prompt i odpowiedź](_przebieg/1049-pisarz.md) · 28.3 s · $0.1328

### 1050 · kontrola_deterministyczna · dział 09 · pytanie 54 · próba 2

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `wyjaśnienie` (blokująca) **sec-09-czym-jest-testowanie-programu**: Oznaczenie [[sec-09-czym-jest-testowanie-programu]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
- 0.0 s

### 1051 · weryfikator_pojęć · dział 09 · pytanie 54 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1051-weryfikator-pojec.md) · 4.9 s · $0.0214

### 1052 · znudzony_czytelnik · dział 09 · pytanie 54 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `przykład` (blokująca) **lista trzech sytuacji**: Sedno odpowiedzi to trzy ogólne punkty (wrócić do działającej wersji, znaleźć, kiedy pojawił się błąd, eksperymentować). Żaden nie ma konkretnego scenariusza, a kod pokazuje tylko, jak zapisać wersję, nie po co. Wystarczy jedno zdanie o „Wspólnej Kasie”. Na przykład: dopisujesz nową funkcję, testy przestają przechodzić, a wracasz do wczorajszego commita zamiast szukać własnych zmian. Można nim zastąpić jeden z punktów, na przykład trzeci, który tylko powtarza pierwszy. _← znudzony_czytelnik_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1052-znudzony-czytelnik.md) · 4.2 s · $0.0212

### 1053 · strażnik_przykład · dział 09 · pytanie 54 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `spójność` (blokująca) **test_rozlicz.py**: W poleceniu `git add funkcje.py test_kasa.py` pojawia się plik `test_kasa.py`, a w kanonie plik testów nazywa się `test_rozlicz.py`. Nie ma deklaracji zmiany nazwy. Zamień na `git add funkcje.py test_rozlicz.py`, a komunikat commita dostosuj do tego, co faktycznie w nim jest. _← strażnik_przykład_
  - `spójność` (blokująca) **wspolna_kasa**: Tekst mówi, że repozytorium „będzie to `wspolna_kasa`”, ale `git init -b main` bez argumentu zakłada repozytorium w bieżącym katalogu i nie tworzy katalogu o tej nazwie. Dodaj `git init -b main wspolna_kasa` albo `mkdir wspolna_kasa && cd wspolna_kasa` przed `init`. W kanonie `wspolna_kasa/` jest też katalogiem z `rozlicz.py`, więc warto wyjaśnić, że to ten sam katalog. _← strażnik_przykład_
- Wynik: 1 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 1.
- Nowe potrzeby (1):
  - `spójność` (blokująca, niespełniona) **wspolna_kasa**: Tekst nadal nie mówi, że polecenie `git init -b main` trzeba uruchomić w folderze `wspolna_kasa`. Samo `init` zakłada repozytorium w bieżącym folderze i nie tworzy folderu o tej nazwie. Dodaj jedno zdanie, np. „Uruchom polecenia w folderze `wspolna_kasa`”, albo linię `cd wspolna_kasa` przed `git init`. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1053-straznik-przyklad.md) · 9.3 s · $0.0323

### 1054 · strażnik_warsztat · dział 09 · pytanie 54 · próba 2

- Potrzeby w kolejce przed krokiem (3):
  - `wynik` (blokująca) **Krok 3: git commit**: Liczba wstawień jest błędna. funkcje.py ma 14 linii, a test_kasa.py 8, razem 22. Podana wartość to 21. Popraw drugą linię wyniku na: ` 2 files changed, 22 insertions(+)`. Hasz 3f2a9c1 może zostać, bo u czytelnika i tak będzie inny. _← strażnik_warsztat_
  - `spójność` (blokująca) **Krok 1 (git init) i punkt startowy**: Punkt startowy nie zawiera Gita, a żaden wcześniejszy krok go nie instaluje. Bez niego `git init` da błąd „command not found”. Dodaj przed krokiem 1 krok sprawdzający `git --version` (z przykładowym wynikiem, np. `git version 2.43.0`) i krótką instrukcję instalacji. Alternatywnie dopisz Git do wymagań. _← strażnik_warsztat_
  - `spójność` (blokująca) **Krok 3: git commit**: Na świeżej instalacji Gita `git commit` przerwie się z komunikatem „Author identity unknown *** Please tell me who you are”, dopóki nie ustawisz nazwy i e-maila. Dodaj przed commitem kroki: `git config --global user.name "Twoje Imię"` oraz `git config --global user.email "ty@example.com"` (oba bez wyniku). Możesz też dopisać zdanie, że robi się to jednorazowo. _← strażnik_warsztat_
- Wynik: 2 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 1.
- Nowe potrzeby (2):
  - `wynik` (blokująca, niespełniona) **git commit**: Krok 6 (git commit): druga linia wyniku podaje 22 wstawienia, a naprawdę będzie 21. funkcje.py ma 14 linii (komentarz, 5 linii funkcji suma, pusta, 2 linie na_osobe, pusta, mazury, tatry, 2 printy). test_kasa.py ma 7 linii (komentarz, import, 4 assert, print), bez pustych. Razem 21. Poprzednia uwaga błędnie zakładała 8 linii w test_kasa.py, więc nie należało zmieniać wartości. Przywróć drugą linię wyniku: ` 2 files changed, 21 insertions(+)`. _← strażnik_warsztat_
  - `spójność` (blokująca) **blok kodu „Sam zapis wygląda tak”**: Blok kodu w tekście sekcji używa nieistniejącego pliku `test_rozlicz.py` i innego opisu commita. Czytelnik ma w katalogu `test_kasa.py`, więc `git add` z tego bloku zakończy się błędem „pathspec did not match any files”. Popraw w bloku linię na `git add funkcje.py test_kasa.py` oraz `git commit -m "Funkcje Wspolnej Kasy i testy"`, żeby zgadzała się z krokami. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/1054-straznik-warsztat.md) · 13.6 s · $0.0423

### 1055 · weryfikator_odwołań · dział 09 · pytanie 54 · próba 2

- Potrzeby w kolejce przed krokiem (3):
  - `odwołanie` (blokująca) **git**: Git, commit i repozytorium to kluczowe pojęcia sekcji, a nie mają haseł w glosariuszu. Są zdefiniowane w tekście jednym zdaniem każde, więc to wystarcza. Trzeba jednak dodać hasła do glosariusza albo zostawić definicje w tekście. Uwaga: 'migawka wybranych plików' jest metaforą i wymaga krótkiego dopowiedzenia, co to znaczy dla osoby spoza IT. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Wykonasz to u siebie w warsztacie.**: Obietnica odsyła do 'warsztatu', którego czytelnik może nie znać jako elementu tutorialu, i nie mówi o temacie. Zastąp zdaniem o temacie, np. 'Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym', albo usuń. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.**: 'Wspólna Kasa' to nawiązanie do projektu z wcześniejszych działów, ale żaden punkt zaczepienia ani sekcja tego nie potwierdza. Wyjaśnij na miejscu, że to przykładowy program do dzielenia wydatków, albo usuń nawiązanie. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- [prompt i odpowiedź](_przebieg/1055-weryfikator-odwolan.md) · 8.2 s · $0.0399

### 1056 · weryfikator_faktów · dział 09 · pytanie 54 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0. (źródła: 1)
- Nowe potrzeby (1):
  - `fakt` (sugestia) **git init -b main**: Dokumentacja git-init (https://git-scm.com/docs/git-init) potwierdza opcję `-b <branch-name>` / `--initial-branch=<branch-name>`. Opcja pojawiła się w Git 2.28 (ta informacja pochodzi z mojej wiedzy, strona ze Context7 jej nie podaje). Sekcja deklaruje tylko „Git 2.x”, więc na starszym Gicie 2.x (do 2.27) `git init -b main` zwróci błąd nieznanej opcji. Popraw deklarację wersji na „Git 2.28 lub nowszy” albo dopisz w tekście, że polecenie wymaga nowszego Gita. _← weryfikator_faktów_
- [prompt i odpowiedź](_przebieg/1056-weryfikator-faktow.md) · 16.2 s · $0.0676

### 1057 · decyzja · dział 09 · pytanie 54 · próba 2

- Potrzeby w kolejce przed krokiem (4):
  - `wyjaśnienie` (blokująca) **sec-09-czym-jest-testowanie-programu**: Oznaczenie [[sec-09-czym-jest-testowanie-programu]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `spójność` (blokująca, niespełniona) **wspolna_kasa**: Tekst nadal nie mówi, że polecenie `git init -b main` trzeba uruchomić w folderze `wspolna_kasa`. Samo `init` zakłada repozytorium w bieżącym folderze i nie tworzy folderu o tej nazwie. Dodaj jedno zdanie, np. „Uruchom polecenia w folderze `wspolna_kasa`”, albo linię `cd wspolna_kasa` przed `git init`. _← strażnik_przykład_
  - `wynik` (blokująca, niespełniona) **git commit**: Krok 6 (git commit): druga linia wyniku podaje 22 wstawienia, a naprawdę będzie 21. funkcje.py ma 14 linii (komentarz, 5 linii funkcji suma, pusta, 2 linie na_osobe, pusta, mazury, tatry, 2 printy). test_kasa.py ma 7 linii (komentarz, import, 4 assert, print), bez pustych. Razem 21. Poprzednia uwaga błędnie zakładała 8 linii w test_kasa.py, więc nie należało zmieniać wartości. Przywróć drugą linię wyniku: ` 2 files changed, 21 insertions(+)`. _← strażnik_warsztat_
  - `spójność` (blokująca) **blok kodu „Sam zapis wygląda tak”**: Blok kodu w tekście sekcji używa nieistniejącego pliku `test_rozlicz.py` i innego opisu commita. Czytelnik ma w katalogu `test_kasa.py`, więc `git add` z tego bloku zakończy się błędem „pathspec did not match any files”. Popraw w bloku linię na `git add funkcje.py test_kasa.py` oraz `git commit -m "Funkcje Wspolnej Kasy i testy"`, żeby zgadzała się z krokami. _← strażnik_warsztat_
- Wynik: Limit prób (2) wyczerpany; 4 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 1058 · akceptacja · dział 09 · pytanie 54

- Wynik: Sekcja [sec-09-po-co-zapisywac-wersje-kodu] dopisana do działu 09; hasła w glosariuszu: Git, commit, repozytorium; kanony: przykład:+wspolna_kasa; odwołania: w przód „pokażemy w ćwiczeniu praktycznym”; punkty zaczepienia: cofnięcie do wczorajszego commita; w TODO zostało 7.
- 0.0 s

### 1059 · autor_dodatków · dział 09 · pytanie 54

- Wynik: „Po co zapisywać wersje kodu”: dygresje: Git powstał w kilka tygodni z konfliktu
- [prompt i odpowiedź](_przebieg/1059-autor-dodatkow.md) · 13.7 s · $0.0899

### 1060 · weryfikator_dodatków · dział 09 · pytanie 54

- Wynik: odrzucone: 1; Git powstał w kilka tygodni z konfliktu: Źródło potwierdza rok 2005, Torvaldsa, BitKeepera i cofnięcie darmowego dostępu, ale nie mówi nic o „kilku tygodniach” z tytułu ani o tym, że Git zapisuje historię „niemal wszystkich”, więc te twierdzenia nie mają potwierdzenia.
- [prompt i odpowiedź](_przebieg/1060-weryfikator-dodatkow.md) · 13.9 s · $0.1237

### 1061 · pisarz · dział 09 · pytanie 55 · próba 1

- Kolejka TODO (6): 56, 57, 58, 59, 60, 61
- Wynik: „Szukanie rozwiązań w internecie”: 186 słów prozy, ```text 1 linii; nowe hasła: dokumentacja
- [prompt i odpowiedź](_przebieg/1061-pisarz.md) · 16.4 s · $0.1050

### 1062 · kontrola_deterministyczna · dział 09 · pytanie 55 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1063 · weryfikator_pojęć · dział 09 · pytanie 55 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **'str' and 'int'**: W przykładowym komunikacie występują 'str' i 'int' bez wyjaśnienia. Wystarczy jedno zdanie, że str to tekst, a int to liczba całkowita (oba to typy danych). Dzięki temu czytelnik zobaczy, że błąd dotyczy dzielenia tekstu przez liczbę. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/1063-weryfikator-pojec.md) · 6.5 s · $0.0237

### 1064 · znudzony_czytelnik · dział 09 · pytanie 55 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1064-znudzony-czytelnik.md) · 5.3 s · $0.0200

### 1065 · strażnik_przykład · dział 09 · pytanie 55 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1065-straznik-przyklad.md) · 4.5 s · $0.0236

### 1066 · weryfikator_odwołań · dział 09 · pytanie 55 · próba 1

- Wynik: 1 blokujących, 0 sugestii. (odwołania: 1)
- Nowe potrzeby (1):
  - `odwołanie` (blokująca) **dokumentacja**: Hasło „dokumentacja” jest użyte jako kluczowe pojęcie w tabeli ([[dokumentacja|dokumentacja]]), ale nie ma go w glosariuszu ani definicji w tekście. Link do nieistniejącego hasła się nie zadziała. Dodaj hasło do glosariusza albo wyjaśnij na miejscu (np. „dokumentacja to oficjalny opis, jak działa język i jego funkcje”) i usuń link. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/1066-weryfikator-odwolan.md) · 5.6 s · $0.0341

### 1067 · decyzja · dział 09 · pytanie 55 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **dokumentacja**: Hasło „dokumentacja” jest użyte jako kluczowe pojęcie w tabeli ([[dokumentacja|dokumentacja]]), ale nie ma go w glosariuszu ani definicji w tekście. Link do nieistniejącego hasła się nie zadziała. Dodaj hasło do glosariusza albo wyjaśnij na miejscu (np. „dokumentacja to oficjalny opis, jak działa język i jego funkcje”) i usuń link. _← weryfikator_odwołań_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 1 sugestii trafia do raportu.
- 0.0 s

### 1068 · pisarz · dział 09 · pytanie 55 · próba 2

- Kolejka TODO (6): 56, 57, 58, 59, 60, 61
- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **dokumentacja**: Hasło „dokumentacja” jest użyte jako kluczowe pojęcie w tabeli ([[dokumentacja|dokumentacja]]), ale nie ma go w glosariuszu ani definicji w tekście. Link do nieistniejącego hasła się nie zadziała. Dodaj hasło do glosariusza albo wyjaśnij na miejscu (np. „dokumentacja to oficjalny opis, jak działa język i jego funkcje”) i usuń link. _← weryfikator_odwołań_
- Wynik: „Szukanie rozwiązań w internecie”: 190 słów prozy, ```text 1 linii
- [prompt i odpowiedź](_przebieg/1068-pisarz.md) · 8.9 s · $0.1046

### 1069 · kontrola_deterministyczna · dział 09 · pytanie 55 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1070 · weryfikator_pojęć · dział 09 · pytanie 55 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1070-weryfikator-pojec.md) · 5.8 s · $0.0219

### 1071 · znudzony_czytelnik · dział 09 · pytanie 55 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `konkret` (sugestia) **tabela źródeł, Stack Overflow**: Wskazówka „duża liczba głosów” i „sprawdź datę” jest ogólnikowa. Warto podać, co uznać za świeże (np. nie starsze niż kilka lat, bo Python 2 działa inaczej niż Python 3) albo że zielony ptaszek oznacza odpowiedź przyjętą przez autora pytania. Stack Overflow jest wymieniony bez wyjaśnienia, że to serwis pytań i odpowiedzi programistów. _← znudzony_czytelnik_
  - `przykład` (sugestia) **własne pytanie, najmniejszy kod**: „Najmniejszy kod, który błąd wywołuje” to abstrakcja dla początkującego. Wystarczyłyby dwie linie, np. wynik = input() / 2, pokazujące, jak z dłuższego programu zostaje samo sedno błędu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1071-znudzony-czytelnik.md) · 9.3 s · $0.0243

### 1072 · strażnik_przykład · dział 09 · pytanie 55 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Przykład przewodni**: Sekcja nie odwołuje się do Wspólnej Kasy. Komunikat TypeError (str / int) i opis „input zwraca tekst zamiast liczby” pasują do wątku: dodaj jedno zdanie, że taki błąd wystąpiłby w na_osobe(suma, osoby), gdyby suma była tekstem z input() bez float(), tak jak w zapytaj_o_wydatek. Nie zmieniaj przy tym deklaracji kanonu. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1072-straznik-przyklad.md) · 7.1 s · $0.0269

### 1073 · weryfikator_odwołań · dział 09 · pytanie 55 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **dokumentacja**: Hasło „dokumentacja” jest użyte jako kluczowe pojęcie w tabeli ([[dokumentacja|dokumentacja]]), ale nie ma go w glosariuszu ani definicji w tekście. Link do nieistniejącego hasła się nie zadziała. Dodaj hasło do glosariusza albo wyjaśnij na miejscu (np. „dokumentacja to oficjalny opis, jak działa język i jego funkcje”) i usuń link. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- [prompt i odpowiedź](_przebieg/1073-weryfikator-odwolan.md) · 3.5 s · $0.0336

### 1074 · decyzja · dział 09 · pytanie 55 · próba 2

- Wynik: Sekcja przyjęta; 3 sugestii trafia do raportu.
- 0.0 s

### 1075 · akceptacja · dział 09 · pytanie 55

- Wynik: Sekcja [sec-09-szukanie-rozwiazan-w-internecie] dopisana do działu 09; odwołania: wstecz „jak w sekcji o czytaniu komunikatów, czytasz od dołu”; punkty zaczepienia: kopiuj ostatnią linię bez ścieżek; w TODO zostało 6.
- 0.0 s

### 1076 · autor_dodatków · dział 09 · pytanie 55

- Wynik: „Szukanie rozwiązań w internecie”: dygresje: Serwis pytań, który zmienił codzienność programistów
- [prompt i odpowiedź](_przebieg/1076-autor-dodatkow.md) · 14.2 s · $0.0906

### 1077 · weryfikator_dodatków · dział 09 · pytanie 55

- Wynik: odrzucone: 1; Serwis pytań, który zmienił codzienność programistów: Wikipedia potwierdza założycieli, rok 2008 i głosowanie, ale nie potwierdza, że odpowiedzi z największą liczbą głosów lądują na górze ani że był to zamysł serwisu od początku, więc źródło nie pokrywa tych twierdzeń.
- [prompt i odpowiedź](_przebieg/1077-weryfikator-dodatkow.md) · 11.4 s · $0.1294

### 1078 · autor_wstępu · dział 10 · próba 1

- Kolejka TODO (6): 56, 57, 58, 59, 60, 61
- Wynik: Wstęp: 80 słów, z diagramem
- [prompt i odpowiedź](_przebieg/1078-autor-wstepu.md) · 5.0 s · $0.0393

### 1079 · recenzent_wstępu · dział 10 · próba 1

- Wynik: 3 blokujących, 2 sugestii.
- Nowe potrzeby (5):
  - `wyjaśnienie` (blokująca) **„zapiszesz ją jako kolejny commit”**: Czytelnik spoza IT może nie znać słowa „commit”. We wstępie nie ma wyjaśnienia ani odwołania do działu, w którym je poznał. Dodaj krótkie odwołanie („zapiszesz ją w historii zmian, jako kolejny commit, jak w dziale X”) albo zastąp to opisem. _← recenzent_wstępu_
  - `odwołanie` (blokująca) **„gotową Wspólną Kasę”**: Wspólna Kasa pojawia się bez wprowadzenia. Czytelnik nie wie, że to projekt z poprzednich działów. Dodaj, że to program budowany w poprzednich działach (np. do rozliczania wspólnych wydatków), i wskaż, który dział. _← recenzent_wstępu_
  - `diagram` (blokująca) **diagram: pomysł → … → commit → następny pomysł**: Diagram jest pojedynczą linią i nie ma zamknięcia pętli. Ostatnia strzałka „następny pomysł” wisi w powietrzu, bo nie wraca do początku. Etykiety „plan kroków” i „commit” nie są wyjaśnione. Nie wiadomo, co się dzieje, gdy test nie przejdzie. Przerysuj jako cykl ze strzałką powrotną z „test” do „kod” („nie działa – popraw”) i z „następny pomysł” do „pomysł”. Dodaj jedno zdanie we wstępie wprowadzające diagram, np. „tak wygląda droga od pomysłu do działającego programu”. _← recenzent_wstępu_
  - `pokrycie` (sugestia) **cały wstęp**: Wstęp mówi o automatyzacji, pomysłach i dalszej nauce, ale prawie nie zapowiada różnicy między stroną a aplikacją mobilną ani umiejętności poza kodowaniem. Wystarczy jedna fraza, np. „i jakie inne umiejętności się przydadzą”. _← recenzent_wstępu_
  - `konkret` (sugestia) **„kto komu ile jest winien”**: Przykład jest dobry, ale zdanie „Dzięki temu zobaczysz, jak automatyzować drobne zadania z własnej pracy” jest skokiem. Dodaj łącznik: taki sam tok pracy da się zastosować do własnych zadań, np. zestawień w arkuszu. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/1079-recenzent-wstepu.md) · 10.8 s · $0.0226

### 1080 · decyzja · dział 10 · próba 1

- Wynik: Wstęp wraca do autora.
- Nowe potrzeby (3):
  - `wyjaśnienie` (blokująca) **„zapiszesz ją jako kolejny commit”**: Czytelnik spoza IT może nie znać słowa „commit”. We wstępie nie ma wyjaśnienia ani odwołania do działu, w którym je poznał. Dodaj krótkie odwołanie („zapiszesz ją w historii zmian, jako kolejny commit, jak w dziale X”) albo zastąp to opisem. _← recenzent_wstępu_
  - `odwołanie` (blokująca) **„gotową Wspólną Kasę”**: Wspólna Kasa pojawia się bez wprowadzenia. Czytelnik nie wie, że to projekt z poprzednich działów. Dodaj, że to program budowany w poprzednich działach (np. do rozliczania wspólnych wydatków), i wskaż, który dział. _← recenzent_wstępu_
  - `diagram` (blokująca) **diagram: pomysł → … → commit → następny pomysł**: Diagram jest pojedynczą linią i nie ma zamknięcia pętli. Ostatnia strzałka „następny pomysł” wisi w powietrzu, bo nie wraca do początku. Etykiety „plan kroków” i „commit” nie są wyjaśnione. Nie wiadomo, co się dzieje, gdy test nie przejdzie. Przerysuj jako cykl ze strzałką powrotną z „test” do „kod” („nie działa – popraw”) i z „następny pomysł” do „pomysł”. Dodaj jedno zdanie we wstępie wprowadzające diagram, np. „tak wygląda droga od pomysłu do działającego programu”. _← recenzent_wstępu_
- 0.0 s

### 1081 · autor_wstępu · dział 10 · próba 2

- Kolejka TODO (6): 56, 57, 58, 59, 60, 61
- Potrzeby w kolejce przed krokiem (3):
  - `wyjaśnienie` (blokująca) **„zapiszesz ją jako kolejny commit”**: Czytelnik spoza IT może nie znać słowa „commit”. We wstępie nie ma wyjaśnienia ani odwołania do działu, w którym je poznał. Dodaj krótkie odwołanie („zapiszesz ją w historii zmian, jako kolejny commit, jak w dziale X”) albo zastąp to opisem. _← recenzent_wstępu_
  - `odwołanie` (blokująca) **„gotową Wspólną Kasę”**: Wspólna Kasa pojawia się bez wprowadzenia. Czytelnik nie wie, że to projekt z poprzednich działów. Dodaj, że to program budowany w poprzednich działach (np. do rozliczania wspólnych wydatków), i wskaż, który dział. _← recenzent_wstępu_
  - `diagram` (blokująca) **diagram: pomysł → … → commit → następny pomysł**: Diagram jest pojedynczą linią i nie ma zamknięcia pętli. Ostatnia strzałka „następny pomysł” wisi w powietrzu, bo nie wraca do początku. Etykiety „plan kroków” i „commit” nie są wyjaśnione. Nie wiadomo, co się dzieje, gdy test nie przejdzie. Przerysuj jako cykl ze strzałką powrotną z „test” do „kod” („nie działa – popraw”) i z „następny pomysł” do „pomysł”. Dodaj jedno zdanie we wstępie wprowadzające diagram, np. „tak wygląda droga od pomysłu do działającego programu”. _← recenzent_wstępu_
- Wynik: Wstęp: 102 słów, z diagramem
- [prompt i odpowiedź](_przebieg/1081-autor-wstepu.md) · 5.6 s · $0.0441

### 1082 · recenzent_wstępu · dział 10 · próba 2

- Wynik: 1 blokujących, 0 sugestii.
- Nowe potrzeby (1):
  - `diagram` (blokująca, niespełniona) **diagram: pomysł → … → commit → następny pomysł**: Pętla „następny pomysł” nadal nie jest domknięta czytelnie. Dolna linia kończy się pod „test”, a nie pod „commit”, i nie ma strzałki w górę do „commit”. Wygląda to tak, jakby wychodziła z „test”, a nie z „commit”. Dolny róg jest też przesunięty o jedną kolumnę względem pionowej kreski „│” nad nim. Popraw: przedłuż dolną linię pod „commit”, dodaj tam „↑” lub „│” prowadzące do „commit” i oznacz kierunek powrotu do „pomysł” strzałką „↑” przy „pomysł”, którą już masz. Wyrównaj znaki w kolumnach. Najprościej dopisz „→ następny pomysł (wracamy na początek)” i narysuj go jako osobną pętlę wychodzącą z „commit”. _← recenzent_wstępu_
- [prompt i odpowiedź](_przebieg/1082-recenzent-wstepu.md) · 18.6 s · $0.0329

### 1083 · decyzja · dział 10 · próba 2

- Wynik: Limit prób wyczerpany, wstęp zostaje.
- Nowe potrzeby (1):
  - `diagram` (blokująca, niespełniona) **diagram: pomysł → … → commit → następny pomysł**: Pętla „następny pomysł” nadal nie jest domknięta czytelnie. Dolna linia kończy się pod „test”, a nie pod „commit”, i nie ma strzałki w górę do „commit”. Wygląda to tak, jakby wychodziła z „test”, a nie z „commit”. Dolny róg jest też przesunięty o jedną kolumnę względem pionowej kreski „│” nad nim. Popraw: przedłuż dolną linię pod „commit”, dodaj tam „↑” lub „│” prowadzące do „commit” i oznacz kierunek powrotu do „pomysł” strzałką „↑” przy „pomysł”, którą już masz. Wyrównaj znaki w kolumnach. Najprościej dopisz „→ następny pomysł (wracamy na początek)” i narysuj go jako osobną pętlę wychodzącą z „commit”. _← recenzent_wstępu_
- 0.0 s

### 1084 · pisarz · dział 10 · pytanie 56 · próba 1

- Kolejka TODO (5): 57, 58, 59, 60, 61
- Wynik: „Programy używane na co dzień”: 244 słów prozy, bez kodu
- [prompt i odpowiedź](_przebieg/1084-pisarz.md) · 26.7 s · $0.1275

### 1085 · kontrola_deterministyczna · dział 10 · pytanie 56 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1086 · weryfikator_pojęć · dział 10 · pytanie 56 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1086-weryfikator-pojec.md) · 5.8 s · $0.0231

### 1087 · znudzony_czytelnik · dział 10 · pytanie 56 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **Pod spodem są te same klocki**: Teza, że bank czy nawigacja składa się z tych samych klocków (if, pętla, funkcja), jest podana tylko słowami. Krótki fragment kodu w Pythonie (np. 5 linii sprawdzających saldo przed przelewem: if saldo >= kwota: ...) pokazałby, że to naprawdę te same klocki co w skryptach czytelnika. _← znudzony_czytelnik_
  - `skrócenie` (sugestia) **tabela i zakończenie**: Tabela ma 5 wierszy, a przykłady są w większości podobne (wejście-przetwarzanie-wyjście). Można zostawić 3-4 wiersze i zyskać miejsce na krótki kod. Zdanie o następnej sekcji i końcowa „konsekwencja” niewiele wnoszą. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1087-znudzony-czytelnik.md) · 5.7 s · $0.0208

### 1088 · strażnik_przykład · dział 10 · pytanie 56 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Wspólna Kasa**: Sekcja nie zawiera kodu, więc nie ma sprzeczności z kanonem. Opis „bierze wydatki, liczy i wypisuje, kto ile zapłacił” zgadza się z wypisz_podsumowanie i udzial_na_osobe. Można dodać do tabeli wiersz „Wspólna Kasa”: wejście to wydatki z wydatki.txt, przetwarzanie to sumowanie i podział na osoby (suma_wydatkow, udzial_na_osobe), wyjście to podsumowanie. Zdanie o banku, który sprawdza dane od użytkownika, można powiązać z sprawdz_kwote. Wtedy przykład przewodni byłby faktycznie wpleciony, a nie tylko wspomniany. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1088-straznik-przyklad.md) · 8.3 s · $0.0297

### 1089 · weryfikator_odwołań · dział 10 · pytanie 56 · próba 1

- Wynik: 1 blokujących, 0 sugestii. (odwołania: 2)
- Nowe potrzeby (1):
  - `odwołanie` (blokująca) **Twoja „Wspólna Kasa”**: Nawiązanie do „Wspólnej Kasy” nie ma celu w dostępnych punktach zaczepienia ani sekcjach: najbliższy lm-60 mówi tylko o złym dzielniku w wyniku 26.0, a nazwy programu nie wprowadza. Czytelnik może nie wiedzieć, co to jest. Popraw: wyjaśnij na miejscu, jednym zdaniem, czym jest ten program (np. „program do dzielenia wspólnych wydatków między osoby, który pisaliśmy wcześniej”), albo usuń nazwę i zostaw sam opis. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/1089-weryfikator-odwolan.md) · 16.1 s · $0.0404

### 1090 · decyzja · dział 10 · pytanie 56 · próba 1

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Twoja „Wspólna Kasa”**: Nawiązanie do „Wspólnej Kasy” nie ma celu w dostępnych punktach zaczepienia ani sekcjach: najbliższy lm-60 mówi tylko o złym dzielniku w wyniku 26.0, a nazwy programu nie wprowadza. Czytelnik może nie wiedzieć, co to jest. Popraw: wyjaśnij na miejscu, jednym zdaniem, czym jest ten program (np. „program do dzielenia wspólnych wydatków między osoby, który pisaliśmy wcześniej”), albo usuń nazwę i zostaw sam opis. _← weryfikator_odwołań_
- Wynik: Do poprawy: 1 blokujących potrzeb wraca do pisarza; 3 sugestii trafia do raportu.
- 0.0 s

### 1091 · pisarz · dział 10 · pytanie 56 · próba 2

- Kolejka TODO (5): 57, 58, 59, 60, 61
- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Twoja „Wspólna Kasa”**: Nawiązanie do „Wspólnej Kasy” nie ma celu w dostępnych punktach zaczepienia ani sekcjach: najbliższy lm-60 mówi tylko o złym dzielniku w wyniku 26.0, a nazwy programu nie wprowadza. Czytelnik może nie wiedzieć, co to jest. Popraw: wyjaśnij na miejscu, jednym zdaniem, czym jest ten program (np. „program do dzielenia wspólnych wydatków między osoby, który pisaliśmy wcześniej”), albo usuń nazwę i zostaw sam opis. _← weryfikator_odwołań_
- Wynik: „Programy używane na co dzień”: 256 słów prozy, bez kodu
- [prompt i odpowiedź](_przebieg/1091-pisarz.md) · 9.2 s · $0.1016

### 1092 · kontrola_deterministyczna · dział 10 · pytanie 56 · próba 2

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `tempo` (blokująca) **długość sekcji**: Proza ma 256 słów, limit to 250. Usuń powtórzenia i zdania ogólne. _← kontrola_długości_
- 0.0 s

### 1093 · weryfikator_pojęć · dział 10 · pytanie 56 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wyjaśnienie` (sugestia) **własnych skryptów**: Słowo „skrypt” nie ma hasła w glosariuszu i nie jest wyjaśnione. Wystarczy zastąpić je słowem „program” albo dodać krótkie objaśnienie, np. „skrypt to mały program napisany do jednego zadania”. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/1093-weryfikator-pojec.md) · 6.9 s · $0.0241

### 1094 · znudzony_czytelnik · dział 10 · pytanie 56 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `przykład` (sugestia) **Pod spodem są te same klocki**: Teza, że pod spodem są zmienne, if, pętle i funkcje, jest podana ogólnie. Przydałby się krótki kod (kilka linii Pythona) pokazujący np. alarm: porównanie godziny z zegarem przez if, żeby czytelnik zobaczył ten sam schemat w małym programie. _← znudzony_czytelnik_
  - `tempo` (sugestia) **Konsekwencja: ... zautomatyzować**: Sekcja w dużej części powtarza schemat wejście–przetwarzanie–wyjście, który czytelnik zna z własnych skryptów, a nowe pojęcia (aplikacja, interfejs) są wprowadzone jednym zdaniem. Ostatnie zdanie o automatyzacji pracy pojawia się nagle bez przykładu. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1094-znudzony-czytelnik.md) · 5.9 s · $0.0211

### 1095 · strażnik_przykład · dział 10 · pytanie 56 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1095-straznik-przyklad.md) · 4.5 s · $0.0253

### 1096 · weryfikator_odwołań · dział 10 · pytanie 56 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **Twoja „Wspólna Kasa”**: Nawiązanie do „Wspólnej Kasy” nie ma celu w dostępnych punktach zaczepienia ani sekcjach: najbliższy lm-60 mówi tylko o złym dzielniku w wyniku 26.0, a nazwy programu nie wprowadza. Czytelnik może nie wiedzieć, co to jest. Popraw: wyjaśnij na miejscu, jednym zdaniem, czym jest ten program (np. „program do dzielenia wspólnych wydatków między osoby, który pisaliśmy wcześniej”), albo usuń nazwę i zostaw sam opis. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 2)
- [prompt i odpowiedź](_przebieg/1096-weryfikator-odwolan.md) · 9.7 s · $0.0366

### 1097 · decyzja · dział 10 · pytanie 56 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `tempo` (blokująca) **długość sekcji**: Proza ma 256 słów, limit to 250. Usuń powtórzenia i zdania ogólne. _← kontrola_długości_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 1098 · akceptacja · dział 10 · pytanie 56

- Wynik: Sekcja [sec-10-programy-uzywane-na-co-dzien] dopisana do działu 10; odwołania: w przód „Czym różni się strona internetowa od aplikacji mobilnej, wyjaśnimy w następnej sekcji”, wstecz „Program do dzielenia wspólnych wydatków między osoby, który budujesz w warsztacie”; w TODO zostało 5.
- 0.0 s

### 1099 · autor_dodatków · dział 10 · pytanie 56

- Wynik: „Programy używane na co dzień”: dowcipy: Alarm: wejście godzina, wyjście irytacja
- [prompt i odpowiedź](_przebieg/1099-autor-dodatkow.md) · 13.5 s · $0.0899

### 1100 · weryfikator_dodatków · dział 10 · pytanie 56

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/1100-weryfikator-dodatkow.md) · 5.7 s · $0.0761

### 1101 · pisarz · dział 10 · pytanie 57 · próba 1

- Kolejka TODO (4): 58, 59, 60, 61
- Wynik: „Strona internetowa a aplikacja mobilna”: 229 słów prozy, bez kodu; nowe hasła: serwer
- [prompt i odpowiedź](_przebieg/1101-pisarz.md) · 13.1 s · $0.0996

### 1102 · kontrola_deterministyczna · dział 10 · pytanie 57 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1103 · weryfikator_pojęć · dział 10 · pytanie 57 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1103-weryfikator-pojec.md) · 4.6 s · $0.0211

### 1104 · znudzony_czytelnik · dział 10 · pytanie 57 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `przykład` (sugestia) **tabela porównawcza**: Różnice są podane ogólnie. Wystarczy jedno zdanie ze znanym przykładem, np. bank, który masz i jako stronę w przeglądarce, i jako aplikację w telefonie. Pokaże, że jedna usługa może działać w obu formach, a aplikacja może np. logować się odciskiem palca albo wysyłać powiadomienia o przelewie. Bez tego tabela pozostaje suchą listą cech. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1104-znudzony-czytelnik.md) · 7.4 s · $0.0228

### 1105 · strażnik_przykład · dział 10 · pytanie 57 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Wspólna Kasa**: Sekcja nie zawiera kodu, więc nie ma sprzeczności z kanonem. Nawiązanie do „Wspólnej Kasy” jest ogólnikowe; można dodać krótki szkic pokazujący, że np. suma_wydatkow i udzial_na_osobe zostają bez zmian, a zmienia się tylko warstwa wejścia i wyjścia (input/print zastąpione formularzem lub ekranem). _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1105-straznik-przyklad.md) · 4.3 s · $0.0247

### 1106 · weryfikator_odwołań · dział 10 · pytanie 57 · próba 1

- Wynik: 2 blokujących, 1 sugestii. (odwołania: 3)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **przeglądarka**: „Przeglądarka” jest kluczowym pojęciem sekcji (strona działa w przeglądarce), a nie ma jej w glosariuszu ani definicji w tekście. Dodaj krótkie wyjaśnienie na miejscu, np. „przeglądarka (program do otwierania stron, np. Chrome czy Firefox)”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Zasada pod spodem jest ta sama**: Zdanie „Zasada pod spodem jest ta sama: dane wejściowe, przetwarzanie, dane wyjściowe” to teza bez przykładu. Dodaj krótki przykład dla Wspólnej Kasy: wejście to kwoty wpisane przez znajomych, przetwarzanie to podział rachunku, wyjście to wynik na ekranie strony albo aplikacji. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **zapytania**: „Serwer” ma definicję w nawiasie, ale „zapytania”, na które odpowiada, nie są wyjaśnione. Sugestia: „gdy przeglądarka o coś poprosi”. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/1106-weryfikator-odwolan.md) · 9.9 s · $0.0365

### 1107 · decyzja · dział 10 · pytanie 57 · próba 1

- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **przeglądarka**: „Przeglądarka” jest kluczowym pojęciem sekcji (strona działa w przeglądarce), a nie ma jej w glosariuszu ani definicji w tekście. Dodaj krótkie wyjaśnienie na miejscu, np. „przeglądarka (program do otwierania stron, np. Chrome czy Firefox)”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Zasada pod spodem jest ta sama**: Zdanie „Zasada pod spodem jest ta sama: dane wejściowe, przetwarzanie, dane wyjściowe” to teza bez przykładu. Dodaj krótki przykład dla Wspólnej Kasy: wejście to kwoty wpisane przez znajomych, przetwarzanie to podział rachunku, wyjście to wynik na ekranie strony albo aplikacji. _← weryfikator_odwołań_
- Wynik: Do poprawy: 2 blokujących potrzeb wraca do pisarza; 3 sugestii trafia do raportu.
- 0.0 s

### 1108 · pisarz · dział 10 · pytanie 57 · próba 2

- Kolejka TODO (4): 58, 59, 60, 61
- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **przeglądarka**: „Przeglądarka” jest kluczowym pojęciem sekcji (strona działa w przeglądarce), a nie ma jej w glosariuszu ani definicji w tekście. Dodaj krótkie wyjaśnienie na miejscu, np. „przeglądarka (program do otwierania stron, np. Chrome czy Firefox)”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Zasada pod spodem jest ta sama**: Zdanie „Zasada pod spodem jest ta sama: dane wejściowe, przetwarzanie, dane wyjściowe” to teza bez przykładu. Dodaj krótki przykład dla Wspólnej Kasy: wejście to kwoty wpisane przez znajomych, przetwarzanie to podział rachunku, wyjście to wynik na ekranie strony albo aplikacji. _← weryfikator_odwołań_
- Wynik: „Strona internetowa a aplikacja mobilna”: 256 słów prozy, bez kodu; nowe hasła: przeglądarka, serwer
- [prompt i odpowiedź](_przebieg/1108-pisarz.md) · 14.4 s · $0.1094

### 1109 · kontrola_deterministyczna · dział 10 · pytanie 57 · próba 2

- Wynik: 1 problemów wykrytych bez modelu.
- Nowe potrzeby (1):
  - `tempo` (blokująca) **długość sekcji**: Proza ma 256 słów, limit to 250. Usuń powtórzenia i zdania ogólne. _← kontrola_długości_
- 0.0 s

### 1110 · weryfikator_pojęć · dział 10 · pytanie 57 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1110-weryfikator-pojec.md) · 4.5 s · $0.0217

### 1111 · znudzony_czytelnik · dział 10 · pytanie 57 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `tempo` (sugestia) **akapit „Pod spodem obie robią to samo”**: Akapit „Pod spodem obie robią to samo…” powtarza schemat wejście–przetwarzanie–wyjście z poprzedniej sekcji. Wystarczy jedno zdanie o tym, że „Wspólna Kasa” może stać się stroną albo aplikacją. Zaoszczędzone słowa można przeznaczyć na konkretny przykład różnicy, np. że strona banku otworzy się na każdym telefonie bez instalacji, a aplikacja banku wyśle powiadomienie o przelewie. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1111-znudzony-czytelnik.md) · 7.4 s · $0.0233

### 1112 · strażnik_przykład · dział 10 · pytanie 57 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1112-straznik-przyklad.md) · 4.0 s · $0.0244

### 1113 · weryfikator_odwołań · dział 10 · pytanie 57 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca) **przeglądarka**: „Przeglądarka” jest kluczowym pojęciem sekcji (strona działa w przeglądarce), a nie ma jej w glosariuszu ani definicji w tekście. Dodaj krótkie wyjaśnienie na miejscu, np. „przeglądarka (program do otwierania stron, np. Chrome czy Firefox)”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Zasada pod spodem jest ta sama**: Zdanie „Zasada pod spodem jest ta sama: dane wejściowe, przetwarzanie, dane wyjściowe” to teza bez przykładu. Dodaj krótki przykład dla Wspólnej Kasy: wejście to kwoty wpisane przez znajomych, przetwarzanie to podział rachunku, wyjście to wynik na ekranie strony albo aplikacji. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- [prompt i odpowiedź](_przebieg/1113-weryfikator-odwolan.md) · 6.9 s · $0.0343

### 1114 · decyzja · dział 10 · pytanie 57 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `tempo` (blokująca) **długość sekcji**: Proza ma 256 słów, limit to 250. Usuń powtórzenia i zdania ogólne. _← kontrola_długości_
- Wynik: Limit prób (2) wyczerpany; 1 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 1115 · akceptacja · dział 10 · pytanie 57

- Wynik: Sekcja [sec-10-strona-internetowa-a-aplikacja-mobilna] dopisana do działu 10; hasła w glosariuszu: serwer, przeglądarka; odwołania: wstecz „dane wejściowe, przetwarzanie, dane wyjściowe”; punkty zaczepienia: Kasa jako strona lub aplikacja; w TODO zostało 4.
- 0.0 s

### 1116 · autor_dodatków · dział 10 · pytanie 57

- Wynik: „Strona internetowa a aplikacja mobilna”: dykteryjki: Strona, która nie działała w magazynie, wtręty: Marta rozsyła program mailem
- [prompt i odpowiedź](_przebieg/1116-autor-dodatkow.md) · 14.2 s · $0.0899

### 1117 · weryfikator_dodatków · dział 10 · pytanie 57

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/1117-weryfikator-dodatkow.md) · 2.6 s · $0.0753

### 1118 · pisarz · dział 10 · pytanie 58 · próba 1

- Kolejka TODO (3): 59, 60, 61
- Wynik: „Od pomysłu do działającego programu”: 152 słów prozy, ```text 3 linii, ```python 3 linii; wątki: przykład dodaj saldo_osoby; warsztat: kto_komu.py, $ python kto_komu.py, $ git add kto_komu.py, $ git commit -m "Dodaj saldo_osoby: kto komu ile jest winien"
- [prompt i odpowiedź](_przebieg/1118-pisarz.md) · 49.5 s · $0.1694

### 1119 · kontrola_deterministyczna · dział 10 · pytanie 58 · próba 1

- Wynik: 2 problemów wykrytych bez modelu.
- Nowe potrzeby (2):
  - `wyjaśnienie` (blokująca) **sec-09-po-co-zapisywac-wersje-kodu**: Oznaczenie [[sec-09-po-co-zapisywac-wersje-kodu]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `spójność` (blokująca) **osoba**: „osoba” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („osoby”), ale ma inną nazwę. Użyj „osoby” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
- 0.0 s

### 1120 · weryfikator_pojęć · dział 10 · pytanie 58 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1120-weryfikator-pojec.md) · 5.3 s · $0.0213

### 1121 · znudzony_czytelnik · dział 10 · pytanie 58 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **saldo_osoby / sprawdzenie na danych z kartki**: Przykład funkcji ma tylko `...` i brak przykładowych danych. Czytelnik nie widzi, jak „sprawdzasz na danych z kartki”. Można w komentarzu dodać np. wydatki: Ania 60, Bartek 0, Celina 30 → saldo Ani +20 (3 osoby, udział 30), bez wydłużania sekcji. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1121-znudzony-czytelnik.md) · 4.5 s · $0.0194

### 1122 · strażnik_przykład · dział 10 · pytanie 58 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1122-straznik-przyklad.md) · 5.5 s · $0.0252

### 1123 · strażnik_warsztat · dział 10 · pytanie 58 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1123-straznik-warsztat.md) · 12.9 s · $0.0386

### 1124 · weryfikator_odwołań · dział 10 · pytanie 58 · próba 1

- Wynik: 2 blokujących, 0 sugestii. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (blokująca) **jak przy podziale problemu na części**: Nawiązanie do wcześniejszego omówienia dzielenia problemu na części nie ma celu na liście punktów zaczepienia ani sekcji z tego i poprzedniego działu ani w glosariuszu. Czytelnik nie ma dokąd wrócić. Usuń nawiązanie albo wyjaśnij na miejscu jednym zdaniem, np. „rozbij zadanie na kroki, z których każdy da się zrobić osobno”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **jak przy podziale problemu na części**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/1124-weryfikator-odwolan.md) · 13.2 s · $0.0376

### 1125 · sprawdzacz_wyników · dział 10 · pytanie 58 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1125-sprawdzacz-wynikow.md) · 2.9 s · $0.0127

### 1126 · weryfikator_faktów · dział 10 · pytanie 58 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/1126-weryfikator-faktow.md) · 4.8 s · $0.0275

### 1127 · decyzja · dział 10 · pytanie 58 · próba 1

- Potrzeby w kolejce przed krokiem (4):
  - `wyjaśnienie` (blokująca) **sec-09-po-co-zapisywac-wersje-kodu**: Oznaczenie [[sec-09-po-co-zapisywac-wersje-kodu]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `spójność` (blokująca) **osoba**: „osoba” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („osoby”), ale ma inną nazwę. Użyj „osoby” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
  - `odwołanie` (blokująca) **jak przy podziale problemu na części**: Nawiązanie do wcześniejszego omówienia dzielenia problemu na części nie ma celu na liście punktów zaczepienia ani sekcji z tego i poprzedniego działu ani w glosariuszu. Czytelnik nie ma dokąd wrócić. Usuń nawiązanie albo wyjaśnij na miejscu jednym zdaniem, np. „rozbij zadanie na kroki, z których każdy da się zrobić osobno”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **jak przy podziale problemu na części**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Do poprawy: 4 blokujących potrzeb wraca do pisarza; 1 sugestii trafia do raportu.
- 0.0 s

### 1128 · pisarz · dział 10 · pytanie 58 · próba 2

- Kolejka TODO (3): 59, 60, 61
- Potrzeby w kolejce przed krokiem (4):
  - `wyjaśnienie` (blokująca) **sec-09-po-co-zapisywac-wersje-kodu**: Oznaczenie [[sec-09-po-co-zapisywac-wersje-kodu]] nie ma hasła w glosariuszu. Dodaj je do new_terms albo użyj istniejącego id. _← kontrola_glosariusza_
  - `spójność` (blokująca) **osoba**: „osoba” wygląda jak element wątku „Rozliczenie wspólnych wydatków „Wspólna Kasa”” („osoby”), ale ma inną nazwę. Użyj „osoby” albo, jeśli to celowo inny element, zadeklaruj go w canon_changes. Bloki spoza wątku oznacz pierwszą linią-komentarzem „poza kanonem”. _← kontrola_przykład_
  - `odwołanie` (blokująca) **jak przy podziale problemu na części**: Nawiązanie do wcześniejszego omówienia dzielenia problemu na części nie ma celu na liście punktów zaczepienia ani sekcji z tego i poprzedniego działu ani w glosariuszu. Czytelnik nie ma dokąd wrócić. Usuń nawiązanie albo wyjaśnij na miejscu jednym zdaniem, np. „rozbij zadanie na kroki, z których każdy da się zrobić osobno”. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **jak przy podziale problemu na części**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: „Od pomysłu do działającego programu”: 155 słów prozy, ```text 3 linii, ```python 3 linii; wątki: przykład dodaj saldo_osoby
- [prompt i odpowiedź](_przebieg/1128-pisarz.md) · 17.1 s · $0.1121

### 1129 · kontrola_deterministyczna · dział 10 · pytanie 58 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1130 · weryfikator_pojęć · dział 10 · pytanie 58 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1130-weryfikator-pojec.md) · 4.4 s · $0.0201

### 1131 · znudzony_czytelnik · dział 10 · pytanie 58 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **blok kodu z saldo_osoby i zdanie o sprawdzaniu na danych z kartki**: Sekcja mówi o „najmniejszym kawałku, który coś robi” i o sprawdzaniu na danych z kartki, ale kod to pusty szkielet z „...”, a sprawdzenie nie ma liczb. Czytelnik nie widzi, jak wygląda „wydatki”, ani jak sprawdzenie wygląda w praktyce. Proponuję zastąpić szkielet krótką działającą funkcją i jedną linią sprawdzenia z liczbami. Przykład: wydatki = {"Ola": 60, "Tomek": 0, "Ewa": 30}, wynik dla Oli to 30, bo 60 minus 30 (równy udział z 90 zł na 3 osoby). Zmieści się w jednym bloku kodu, a opis wokół można lekko skrócić. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1131-znudzony-czytelnik.md) · 9.9 s · $0.0243

### 1132 · strażnik_przykład · dział 10 · pytanie 58 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1132-straznik-przyklad.md) · 5.7 s · $0.0256

### 1133 · weryfikator_odwołań · dział 10 · pytanie 58 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **jak przy podziale problemu na części**: Nawiązanie do wcześniejszego omówienia dzielenia problemu na części nie ma celu na liście punktów zaczepienia ani sekcji z tego i poprzedniego działu ani w glosariuszu. Czytelnik nie ma dokąd wrócić. Usuń nawiązanie albo wyjaśnij na miejscu jednym zdaniem, np. „rozbij zadanie na kroki, z których każdy da się zrobić osobno”. _← weryfikator_odwołań_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (odwołania: 1)
- [prompt i odpowiedź](_przebieg/1133-weryfikator-odwolan.md) · 3.6 s · $0.0301

### 1134 · sprawdzacz_wyników · dział 10 · pytanie 58 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1134-sprawdzacz-wynikow.md) · 2.8 s · $0.0126

### 1135 · weryfikator_faktów · dział 10 · pytanie 58 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/1135-weryfikator-faktow.md) · 4.3 s · $0.0270

### 1136 · decyzja · dział 10 · pytanie 58 · próba 2

- Wynik: Sekcja przyjęta; 1 sugestii trafia do raportu.
- 0.0 s

### 1137 · akceptacja · dział 10 · pytanie 58

- Wynik: Sekcja [sec-10-od-pomyslu-do-dzialajacego-programu] dopisana do działu 10; kanony: przykład:+saldo_osoby; odwołania: wstecz „jak w sekcji o zapisywaniu wersji kodu”; punkty zaczepienia: pętla budowy programu; w TODO zostało 3.
- 0.0 s

### 1138 · łowca_pułapek · dział 10 · pytanie 58

- Wynik: „Od pomysłu do działającego programu”: brak pułapek
- [prompt i odpowiedź](_przebieg/1138-lowca-pulapek.md) · 2.3 s · $0.0135

### 1139 · autor_dodatków · dział 10 · pytanie 58

- Wynik: „Od pomysłu do działającego programu”: rysunki: Haki co kilka kroków, dowcipy: Skarpetka w szufladzie, nie w mieszkaniu
- [prompt i odpowiedź](_przebieg/1139-autor-dodatkow.md) · 15.3 s · $0.0893

### 1140 · weryfikator_dodatków · dział 10 · pytanie 58

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/1140-weryfikator-dodatkow.md) · 6.3 s · $0.0782

### 1141 · pisarz · dział 10 · pytanie 59 · próba 1

- Kolejka TODO (2): 60, 61
- Wynik: „Umiejętności poza kodowaniem”: 222 słów prozy, bez kodu
- [prompt i odpowiedź](_przebieg/1141-pisarz.md) · 21.0 s · $0.1235

### 1142 · kontrola_deterministyczna · dział 10 · pytanie 59 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1143 · weryfikator_pojęć · dział 10 · pytanie 59 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1143-weryfikator-pojec.md) · 4.4 s · $0.0206

### 1144 · znudzony_czytelnik · dział 10 · pytanie 59 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **tabela: Szukanie informacji, Dokładność**: Wiersze „Szukanie informacji” i „Dokładność” są w tabeli szczątkowe i nie wracają w prozie. „Szukanie po ostatniej linii komunikatu” to zagadka dla osoby spoza IT (jaki komunikat? po co ostatnia linia?). Kwota „z kropką, nie z przecinkiem” nie mówi, dlaczego to ma znaczenie. Wystarczy jedno zdanie z przykładem, np. program zgłasza błąd, a jego ostatnia linia nazywa problem i można ją wpisać w wyszukiwarkę. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1144-znudzony-czytelnik.md) · 7.8 s · $0.0222

### 1145 · strażnik_przykład · dział 10 · pytanie 59 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `spójność` (sugestia) **Rozumienie problemu (tabela)**: Sekcja nie zawiera bloków kodu, więc nie ma sprzeczności z kanonem. Nawiązania do wątku (print, kwota z kropką, pytanie o podział po równo) są zgodne z kanonem (sprawdz_kwote, na_osobe). Opcjonalnie: wiersz o dokładności mógłby wskazać sprawdz_kwote jako miejsce, gdzie program pilnuje kropki. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1145-straznik-przyklad.md) · 4.1 s · $0.0249

### 1146 · weryfikator_odwołań · dział 10 · pytanie 59 · próba 1

- Wynik: 0 blokujących, 1 sugestii. (odwołania: 1)
- Nowe potrzeby (1):
  - `odwołanie` (sugestia) **Szukanie informacji, Dokładność**: Umiejętność „szukanie informacji” i „dokładność” pojawiają się tylko w tabeli, a tekst pod nią ich nie rozwija. Można dodać jedno zdanie o każdej. _← weryfikator_odwołań_
- [prompt i odpowiedź](_przebieg/1146-weryfikator-odwolan.md) · 11.9 s · $0.0382

### 1147 · decyzja · dział 10 · pytanie 59 · próba 1

- Wynik: Sekcja przyjęta; 3 sugestii trafia do raportu.
- 0.0 s

### 1148 · akceptacja · dział 10 · pytanie 59

- Wynik: Sekcja [sec-10-umiejetnosci-poza-kodowaniem] dopisana do działu 10; odwołania: wstecz „szukanie po ostatniej linii komunikatu”; punkty zaczepienia: zły problem kosztuje więcej niż literówka; w TODO zostało 2.
- 0.0 s

### 1149 · autor_dodatków · dział 10 · pytanie 59

- Wynik: „Umiejętności poza kodowaniem”: dygresje: Gumowa kaczuszka jako rozmówca
- [prompt i odpowiedź](_przebieg/1149-autor-dodatkow.md) · 13.0 s · $0.0887

### 1150 · weryfikator_dodatków · dział 10 · pytanie 59

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/1150-weryfikator-dodatkow.md) · 13.0 s · $0.1242

### 1151 · pisarz · dział 10 · pytanie 60 · próba 1

- Kolejka TODO (1): 61
- Wynik: „Od czego zacząć naukę”: 173 słów prozy, ```text 1 linii; wątki: przykład dodaj wypisz_dlugi; warsztat: dlugi.py, $ python dlugi.py, $ git add dlugi.py, $ git commit -m "Dodaj funkcję wypisz_dlugi"
- [prompt i odpowiedź](_przebieg/1151-pisarz.md) · 52.1 s · $0.1734

### 1152 · kontrola_deterministyczna · dział 10 · pytanie 60 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1153 · weryfikator_pojęć · dział 10 · pytanie 60 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1153-weryfikator-pojec.md) · 5.1 s · $0.0209

### 1154 · znudzony_czytelnik · dział 10 · pytanie 60 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `konkret` (sugestia) **Praktyczny początek / dobry pierwszy problem**: Rada „jeden mały problem” jest ogólna. Brakuje jednego zdania z konkretnym przykładem pierwszego kroku, np. „napisz kilka linii, które dzielą rachunek 90 zł na 3 osoby i wypisują 30 zł”. Bez tego początkujący nadal nie wie, co dokładnie zrobić w pierwszym tygodniu. Można to zrobić kosztem zdania o „kulawej wersji”. _← znudzony_czytelnik_
  - `tempo` (sugestia) **Akapity o szukaniu i kolejnych elementach**: Sekcja w dużej mierze powtarza wcześniejsze: pętlę od pomysłu, szukanie po ostatniej linii komunikatu i listę tematów. Akapit o „kolejnych elementach” można skrócić do jednego zdania. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1154-znudzony-czytelnik.md) · 6.2 s · $0.0205

### 1155 · strażnik_przykład · dział 10 · pytanie 60 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1155-straznik-przyklad.md) · 4.7 s · $0.0248

### 1156 · strażnik_warsztat · dział 10 · pytanie 60 · próba 1

- Wynik: Brak uwag.
- [prompt i odpowiedź](_przebieg/1156-straznik-warsztat.md) · 9.1 s · $0.0351

### 1157 · weryfikator_odwołań · dział 10 · pytanie 60 · próba 1

- Wynik: Brak uwag. (odwołania: 4)
- [prompt i odpowiedź](_przebieg/1157-weryfikator-odwolan.md) · 10.4 s · $0.0378

### 1158 · decyzja · dział 10 · pytanie 60 · próba 1

- Wynik: Sekcja przyjęta; 2 sugestii trafia do raportu.
- 0.0 s

### 1159 · akceptacja · dział 10 · pytanie 60

- Wynik: Sekcja [sec-10-od-czego-zaczac-nauke] dopisana do działu 10; kanony: przykład:+wypisz_dlugi; odwołania: wstecz „sekcji o budowie programu od pomysłu”, wstecz „w sekcji o rozwiązaniach w internecie: po ostatniej linii komunikatu”, wstecz „Wspólna Kasa to jej przykład”, w przód „W kolejnej sekcji zobaczysz, jak taki kawałek kodu zaczyna pracować za Ciebie”; punkty zaczepienia: pętla nauki; w TODO zostało 1.
- 0.0 s

### 1160 · autor_dodatków · dział 10 · pytanie 60

- Wynik: „Od czego zacząć naukę”: wtręty: Marta szuka idealnego kursu zamiast pisać
- [prompt i odpowiedź](_przebieg/1160-autor-dodatkow.md) · 7.8 s · $0.0849

### 1161 · weryfikator_dodatków · dział 10 · pytanie 60

- Wynik: odrzucone: 0
- [prompt i odpowiedź](_przebieg/1161-weryfikator-dodatkow.md) · 6.7 s · $0.0790

### 1162 · pisarz · dział 10 · pytanie 61 · próba 1

- Wynik: „Automatyzacja prostych zadań”: 141 słów prozy, ```python 8 linii, ```text 3 linii; nowe hasła: automatyzacja; warsztat: $ python dlugi.py, dlugi.py, $ python dlugi.py, $ git add dlugi.py && git commit -m "Rozliczenie: nagłówek w wypisz_dlugi"
- [prompt i odpowiedź](_przebieg/1162-pisarz.md) · 30.7 s · $0.1267

### 1163 · kontrola_deterministyczna · dział 10 · pytanie 61 · próba 1

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1164 · weryfikator_pojęć · dział 10 · pytanie 61 · próba 1

- Wynik: 0 blokujących, 2 sugestii.
- Nowe potrzeby (2):
  - `wyjaśnienie` (sugestia) **f"Netto: {razem} zł"**: Zapis f"...{razem}..." (wstawianie wartości zmiennej w tekst) nie ma hasła w glosariuszu ani wyjaśnienia. Wynik pod kodem pokazuje jego działanie, więc wystarczy jedno zdanie. _← weryfikator_pojęć_
  - `wyjaśnienie` (sugestia) **round(razem * 0.23, 2)**: Nie wiadomo, że round zaokrągla wynik do 2 miejsc po przecinku. Wystarczy krótki komentarz w kodzie albo jedno zdanie. _← weryfikator_pojęć_
- [prompt i odpowiedź](_przebieg/1164-weryfikator-pojec.md) · 9.4 s · $0.0248

### 1165 · znudzony_czytelnik · dział 10 · pytanie 61 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `konkret` (sugestia) **zdanie o mechanizmie i zdanie o 200 fakturach**: Tekst mówi, że mechanizm to pętla i funkcja, ale w przykładzie nie ma funkcji. Zdanie „Jutro lista ma 200 faktur, a kod zostaje ten sam” pomija to, skąd te 200 faktur się weźmie, bo lista jest wpisana na sztywno. Wystarczy zmienić „pętla i funkcja” na samą „pętlę” albo dodać pół zdania, że kwoty można wczytać np. z arkusza. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1165-znudzony-czytelnik.md) · 7.6 s · $0.0219

### 1166 · strażnik_przykład · dział 10 · pytanie 61 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `spójność` (blokująca) **blok python z faktury / VAT**: Przykład wprowadza obcą dziedzinę (faktury, netto, VAT 23%, brutto) bez oznaczenia. Albo dodaj w pierwszej linii bloku komentarz „# poza kanonem”, albo lepiej przepisz go na wątek Wspólnej Kasy: użyj listy `wydatki` lub `kwota` i `osoby`, policz sumę i `udzial_na_osobe` (np. `suma_wydatkow`, `udzial_na_osobe(suma, len(osoby))`). Wtedy „jutro lista ma 200 pozycji” działa na tych samych danych co reszta tutoriala. _← strażnik_przykład_
  - `spójność` (sugestia) **suma_wydatkow / udzial_na_osobe**: Tekst mówi, że mechanizm to pętla i funkcja, ale kod pokazuje tylko pętlę wpisaną wprost. Pętla sumująca to kanoniczna `suma_wydatkow` z funkcje.py; wywołaj ją zamiast powtarzać ciało albo zaznacz, że to ta sama pętla, którą zamknięto w funkcji. _← strażnik_przykład_
  - `spójność` (sugestia) **dlugi.py**: Zdanie „raz opisany podział rachunku liczy się sam” jest nieprecyzyjne. Kanoniczna `wypisz_dlugi(wydatki, osoby)` w dlugi.py wypisuje, kto ile dopłaca albo dostaje. Nazwij to wprost, np. „`wypisz_dlugi` raz opisane rozliczenie liczy dla dowolnej liczby wydatków”. _← strażnik_przykład_
- [prompt i odpowiedź](_przebieg/1166-straznik-przyklad.md) · 13.2 s · $0.0348

### 1167 · strażnik_warsztat · dział 10 · pytanie 61 · próba 1

- Wynik: 1 blokujących, 2 sugestii.
- Nowe potrzeby (3):
  - `wynik` (blokująca) **Krok 4: git add && git commit**: Punkt startowy nie obejmuje gita. W stanie nie ma repozytorium (brak `git init`) ani konfiguracji `user.name` i `user.email`, a git nie jest wymieniony jako zainstalowany. Bez tego `git add` zwróci `fatal: not a git repository`. Jeśli czytelnik zrobi `git init`, dlugi.py nie był wcześniej commitowany, więc podany wynik `1 file changed, 1 insertion(+)` jest nieprawdziwy. Pierwszy commit wypisze `[main (root-commit) <hash>] ...`, potem ` 1 file changed, 26 insertions(+)` i ` create mode 100644 dlugi.py`. Poprawka: przed krokiem 1 dodaj kroki instalacji i sprawdzenia gita (`git --version`), `git init -b main`, `git config user.name`/`user.email` oraz pierwszy commit dlugi.py bez nagłówka. Wtedy wynik kroku 4 (`1 file changed, 1 insertion(+)`) będzie poprawny. Alternatywnie zmień wynik kroku 4 na wersję z root-commit i 26 insertions. Hash jest zmienny, więc dodaj uwagę, że u czytelnika będzie inny. _← strażnik_warsztat_
  - `spójność` (sugestia) **Tekst sekcji: „pętla i funkcja”**: Tekst mówi, że mechanizmem jest pętla i funkcja, ale przykład z fakturami zawiera tylko pętlę, bez `def`. Dodaj funkcję (np. `def podsumuj(faktury):`) albo napisz, że w przykładzie użyto samej pętli. _← strażnik_warsztat_
  - `spójność` (sugestia) **„pętla nauki” i „commit”**: Zwrot „tą samą pętlą nauki” oraz słowo „commit” pojawiają się bez definicji i bez odnośnika do glosariusza. Dodaj krótkie wyjaśnienie albo odnośnik. _← strażnik_warsztat_
- [prompt i odpowiedź](_przebieg/1167-straznik-warsztat.md) · 19.7 s · $0.0462

### 1168 · weryfikator_odwołań · dział 10 · pytanie 61 · próba 1

- Wynik: 2 blokujących, 1 sugestii. (odwołania: 1)
- Nowe potrzeby (3):
  - `odwołanie` (blokująca) **`dlugi.py`**: Nawiązanie do „Twojego dlugi.py” nie ma celu: w żadnym punkcie zaczepienia ani sekcji tego i poprzedniego działu nie ma pliku o tej nazwie (jest tylko Kasa jako pomysł na stronę lub aplikację). Wyjaśnij na miejscu (np. „program dzielący rachunek między znajomych, jeśli taki napisałeś(-aś)”) albo usuń zdanie lub zastąp je nowym przykładem. _← weryfikator_odwołań_
  - `odwołanie` (sugestia) **Mechanizm znasz: to pętla i funkcja**: Tekst mówi o pętli i funkcji, ale kod używa tylko pętli (round to funkcja wbudowana, nie własna). Albo pokaż własną funkcję, albo napisz, że mechanizm to pętla, a round jest gotową funkcją. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Podobnie działa Twój `dlugi.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/1168-weryfikator-odwolan.md) · 13.7 s · $0.0413

### 1169 · sprawdzacz_wyników · dział 10 · pytanie 61 · próba 1

- Wynik: 0 blokujących, 1 sugestii.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **Mechanizm znasz: to pętla i funkcja**: Tekst mówi, że mechanizm to pętla i funkcja, ale w przykładzie jest tylko pętla (i wbudowane round). Warto albo pominąć funkcję w zdaniu, albo zapakować obliczenia w własną funkcję. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/1169-sprawdzacz-wynikow.md) · 6.4 s · $0.0163

### 1170 · weryfikator_faktów · dział 10 · pytanie 61 · próba 1

- Wynik: Brak uwag. (źródła: 0)
- [prompt i odpowiedź](_przebieg/1170-weryfikator-faktow.md) · 7.6 s · $0.0384

### 1171 · decyzja · dział 10 · pytanie 61 · próba 1

- Potrzeby w kolejce przed krokiem (4):
  - `spójność` (blokująca) **blok python z faktury / VAT**: Przykład wprowadza obcą dziedzinę (faktury, netto, VAT 23%, brutto) bez oznaczenia. Albo dodaj w pierwszej linii bloku komentarz „# poza kanonem”, albo lepiej przepisz go na wątek Wspólnej Kasy: użyj listy `wydatki` lub `kwota` i `osoby`, policz sumę i `udzial_na_osobe` (np. `suma_wydatkow`, `udzial_na_osobe(suma, len(osoby))`). Wtedy „jutro lista ma 200 pozycji” działa na tych samych danych co reszta tutoriala. _← strażnik_przykład_
  - `wynik` (blokująca) **Krok 4: git add && git commit**: Punkt startowy nie obejmuje gita. W stanie nie ma repozytorium (brak `git init`) ani konfiguracji `user.name` i `user.email`, a git nie jest wymieniony jako zainstalowany. Bez tego `git add` zwróci `fatal: not a git repository`. Jeśli czytelnik zrobi `git init`, dlugi.py nie był wcześniej commitowany, więc podany wynik `1 file changed, 1 insertion(+)` jest nieprawdziwy. Pierwszy commit wypisze `[main (root-commit) <hash>] ...`, potem ` 1 file changed, 26 insertions(+)` i ` create mode 100644 dlugi.py`. Poprawka: przed krokiem 1 dodaj kroki instalacji i sprawdzenia gita (`git --version`), `git init -b main`, `git config user.name`/`user.email` oraz pierwszy commit dlugi.py bez nagłówka. Wtedy wynik kroku 4 (`1 file changed, 1 insertion(+)`) będzie poprawny. Alternatywnie zmień wynik kroku 4 na wersję z root-commit i 26 insertions. Hash jest zmienny, więc dodaj uwagę, że u czytelnika będzie inny. _← strażnik_warsztat_
  - `odwołanie` (blokująca) **`dlugi.py`**: Nawiązanie do „Twojego dlugi.py” nie ma celu: w żadnym punkcie zaczepienia ani sekcji tego i poprzedniego działu nie ma pliku o tej nazwie (jest tylko Kasa jako pomysł na stronę lub aplikację). Wyjaśnij na miejscu (np. „program dzielący rachunek między znajomych, jeśli taki napisałeś(-aś)”) albo usuń zdanie lub zastąp je nowym przykładem. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Podobnie działa Twój `dlugi.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Do poprawy: 4 blokujących potrzeb wraca do pisarza; 9 sugestii trafia do raportu.
- 0.0 s

### 1172 · pisarz · dział 10 · pytanie 61 · próba 2

- Potrzeby w kolejce przed krokiem (4):
  - `spójność` (blokująca) **blok python z faktury / VAT**: Przykład wprowadza obcą dziedzinę (faktury, netto, VAT 23%, brutto) bez oznaczenia. Albo dodaj w pierwszej linii bloku komentarz „# poza kanonem”, albo lepiej przepisz go na wątek Wspólnej Kasy: użyj listy `wydatki` lub `kwota` i `osoby`, policz sumę i `udzial_na_osobe` (np. `suma_wydatkow`, `udzial_na_osobe(suma, len(osoby))`). Wtedy „jutro lista ma 200 pozycji” działa na tych samych danych co reszta tutoriala. _← strażnik_przykład_
  - `wynik` (blokująca) **Krok 4: git add && git commit**: Punkt startowy nie obejmuje gita. W stanie nie ma repozytorium (brak `git init`) ani konfiguracji `user.name` i `user.email`, a git nie jest wymieniony jako zainstalowany. Bez tego `git add` zwróci `fatal: not a git repository`. Jeśli czytelnik zrobi `git init`, dlugi.py nie był wcześniej commitowany, więc podany wynik `1 file changed, 1 insertion(+)` jest nieprawdziwy. Pierwszy commit wypisze `[main (root-commit) <hash>] ...`, potem ` 1 file changed, 26 insertions(+)` i ` create mode 100644 dlugi.py`. Poprawka: przed krokiem 1 dodaj kroki instalacji i sprawdzenia gita (`git --version`), `git init -b main`, `git config user.name`/`user.email` oraz pierwszy commit dlugi.py bez nagłówka. Wtedy wynik kroku 4 (`1 file changed, 1 insertion(+)`) będzie poprawny. Alternatywnie zmień wynik kroku 4 na wersję z root-commit i 26 insertions. Hash jest zmienny, więc dodaj uwagę, że u czytelnika będzie inny. _← strażnik_warsztat_
  - `odwołanie` (blokująca) **`dlugi.py`**: Nawiązanie do „Twojego dlugi.py” nie ma celu: w żadnym punkcie zaczepienia ani sekcji tego i poprzedniego działu nie ma pliku o tej nazwie (jest tylko Kasa jako pomysł na stronę lub aplikację). Wyjaśnij na miejscu (np. „program dzielący rachunek między znajomych, jeśli taki napisałeś(-aś)”) albo usuń zdanie lub zastąp je nowym przykładem. _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **Podobnie działa Twój `dlugi.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: „Automatyzacja prostych zadań”: 156 słów prozy, ```python 9 linii, ```text 2 linii; nowe hasła: automatyzacja; warsztat: $ git --version, $ git init -b main, $ git config user.name "Twoje Imię" && git config user.email "ty@example.com", $ git add dlugi.py && git commit -m "Dlugi: kto ile doplaca", dlugi.py, $ python dlugi.py, $ git add dlugi.py && git commit -m "Naglowek rozliczenia"
- [prompt i odpowiedź](_przebieg/1172-pisarz.md) · 32.6 s · $0.1397

### 1173 · kontrola_deterministyczna · dział 10 · pytanie 61 · próba 2

- Wynik: Kod, języki, długość i oznaczenia terminów w normie.
- 0.0 s

### 1174 · weryfikator_pojęć · dział 10 · pytanie 61 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1174-weryfikator-pojec.md) · 6.9 s · $0.0227

### 1175 · znudzony_czytelnik · dział 10 · pytanie 61 · próba 2

- Wynik: 0 blokujących, 2 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (2):
  - `konkret` (sugestia) **Ten sam mechanizm obsłuży arkusz z fakturami**: Czytelnik zna arkusz, więc zapyta: po co pętla, skoro SUMA w arkuszu robi to samo? Jedno zdanie o tym, kiedy kod wygrywa z arkuszem (np. zadanie powtarzane co tydzień na nowych plikach, bez klikania), dałoby realną decyzję zamiast ogólnika o arkuszu z fakturami. _← znudzony_czytelnik_
  - `odwołanie` (sugestia) **`dlugi.py`**: `dlugi.py` pojawia się bez wyjaśnienia. Poprzednia sekcja mówiła o funkcji dopisanej do Wspólnej Kasy. Warto jednym słowem powiedzieć, że to plik z funkcją liczącą, kto ile dopłaca. _← znudzony_czytelnik_
- [prompt i odpowiedź](_przebieg/1175-znudzony-czytelnik.md) · 9.7 s · $0.0240

### 1176 · strażnik_przykład · dział 10 · pytanie 61 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `spójność` (blokująca) **blok python z faktury / VAT**: Przykład wprowadza obcą dziedzinę (faktury, netto, VAT 23%, brutto) bez oznaczenia. Albo dodaj w pierwszej linii bloku komentarz „# poza kanonem”, albo lepiej przepisz go na wątek Wspólnej Kasy: użyj listy `wydatki` lub `kwota` i `osoby`, policz sumę i `udzial_na_osobe` (np. `suma_wydatkow`, `udzial_na_osobe(suma, len(osoby))`). Wtedy „jutro lista ma 200 pozycji” działa na tych samych danych co reszta tutoriala. _← strażnik_przykład_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1176-straznik-przyklad.md) · 4.9 s · $0.0278

### 1177 · strażnik_warsztat · dział 10 · pytanie 61 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `wynik` (blokująca) **Krok 4: git add && git commit**: Punkt startowy nie obejmuje gita. W stanie nie ma repozytorium (brak `git init`) ani konfiguracji `user.name` i `user.email`, a git nie jest wymieniony jako zainstalowany. Bez tego `git add` zwróci `fatal: not a git repository`. Jeśli czytelnik zrobi `git init`, dlugi.py nie był wcześniej commitowany, więc podany wynik `1 file changed, 1 insertion(+)` jest nieprawdziwy. Pierwszy commit wypisze `[main (root-commit) <hash>] ...`, potem ` 1 file changed, 26 insertions(+)` i ` create mode 100644 dlugi.py`. Poprawka: przed krokiem 1 dodaj kroki instalacji i sprawdzenia gita (`git --version`), `git init -b main`, `git config user.name`/`user.email` oraz pierwszy commit dlugi.py bez nagłówka. Wtedy wynik kroku 4 (`1 file changed, 1 insertion(+)`) będzie poprawny. Alternatywnie zmień wynik kroku 4 na wersję z root-commit i 26 insertions. Hash jest zmienny, więc dodaj uwagę, że u czytelnika będzie inny. _← strażnik_warsztat_
- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0.
- [prompt i odpowiedź](_przebieg/1177-straznik-warsztat.md) · 8.3 s · $0.0389

### 1178 · weryfikator_odwołań · dział 10 · pytanie 61 · próba 2

- Potrzeby w kolejce przed krokiem (1):
  - `odwołanie` (blokująca) **`dlugi.py`**: Nawiązanie do „Twojego dlugi.py” nie ma celu: w żadnym punkcie zaczepienia ani sekcji tego i poprzedniego działu nie ma pliku o tej nazwie (jest tylko Kasa jako pomysł na stronę lub aplikację). Wyjaśnij na miejscu (np. „program dzielący rachunek między znajomych, jeśli taki napisałeś(-aś)”) albo usuń zdanie lub zastąp je nowym przykładem. _← weryfikator_odwołań_
- Wynik: 2 blokujących, 0 sugestii. Niespełnione z poprzedniej recenzji: 1. (odwołania: 2)
- Nowe potrzeby (2):
  - `odwołanie` (blokująca, niespełniona) **W warsztacie zapisujesz w ten sposób swój `dlugi.py`**: Ostatnie zdanie nadal odwołuje się do „warsztatu” i pliku `dlugi.py`, których w tym ani poprzednim dziale nie ma. Czytelnik nie wie, o co chodzi. Usuń zdanie albo zastąp je przykładem wyjaśnionym na miejscu, np. „Możesz w ten sposób zapisać program dzielący rachunek między znajomych.” _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **W warsztacie zapisujesz w ten sposób swój `dlugi.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- [prompt i odpowiedź](_przebieg/1178-weryfikator-odwolan.md) · 10.2 s · $0.0406

### 1179 · sprawdzacz_wyników · dział 10 · pytanie 61 · próba 2

- Wynik: 0 blokujących, 1 sugestii. Niespełnione z poprzedniej recenzji: 0.
- Nowe potrzeby (1):
  - `wynik` (sugestia) **Mechanizm znasz: to pętla po danych i funkcja**: Tekst mówi, że mechanizm to pętla i funkcja, ale przykład zawiera tylko pętlę, bez żadnej funkcji (poza wbudowanymi print i len). Można dopisać, że tu funkcje to print i len, albo pokazać własną funkcję. _← sprawdzacz_wyników_
- [prompt i odpowiedź](_przebieg/1179-sprawdzacz-wynikow.md) · 6.1 s · $0.0167

### 1180 · weryfikator_faktów · dział 10 · pytanie 61 · próba 2

- Wynik: Brak uwag. Niespełnione z poprzedniej recenzji: 0. (źródła: 0)
- [prompt i odpowiedź](_przebieg/1180-weryfikator-faktow.md) · 5.8 s · $0.0287

### 1181 · decyzja · dział 10 · pytanie 61 · próba 2

- Potrzeby w kolejce przed krokiem (2):
  - `odwołanie` (blokująca, niespełniona) **W warsztacie zapisujesz w ten sposób swój `dlugi.py`**: Ostatnie zdanie nadal odwołuje się do „warsztatu” i pliku `dlugi.py`, których w tym ani poprzednim dziale nie ma. Czytelnik nie wie, o co chodzi. Usuń zdanie albo zastąp je przykładem wyjaśnionym na miejscu, np. „Możesz w ten sposób zapisać program dzielący rachunek między znajomych.” _← weryfikator_odwołań_
  - `odwołanie` (blokująca) **W warsztacie zapisujesz w ten sposób swój `dlugi.py`**: Nawiązanie do czegoś, czego czytelnik jeszcze nie widział: wyjaśnij na miejscu albo usuń nawiązanie. _← kontrola_odwołań_
- Wynik: Limit prób (2) wyczerpany; 2 blokujących potrzeb zostaje niespełnionych.
- 0.0 s

### 1182 · akceptacja · dział 10 · pytanie 61

- Wynik: Sekcja [sec-10-automatyzacja-prostych-zadan] dopisana do działu 10; hasła w glosariuszu: automatyzacja; odwołania: wstecz „tą samą pętlą nauki”, wstecz „Tak wygląda to we Wspólnej Kasie”; punkty zaczepienia: 200 wydatków, ten sam kod; w TODO zostało 0.
- 0.0 s

### 1183 · łowca_pułapek · dział 10 · pytanie 61

- Wynik: „Automatyzacja prostych zadań”: brak pułapek
- [prompt i odpowiedź](_przebieg/1183-lowca-pulapek.md) · 2.2 s · $0.0168

### 1184 · autor_dodatków · dział 10 · pytanie 61

- Wynik: „Automatyzacja prostych zadań”: dykteryjki: Automat sprawdzony na kartce
- [prompt i odpowiedź](_przebieg/1184-autor-dodatkow.md) · 9.5 s · $0.0864

### 1185 · weryfikator_dodatków · dział 10 · pytanie 61

- Wynik: odrzucone: 1; Automat sprawdzony na kartce: Powtarza motyw wcześniejszych wpisów („Raport, który wyglądał wiarygodnie” i „Marta ufa ciszy zamiast rachunkowi”): skrypt po cichu podaje zaniżony wynik, a błąd wychodzi dopiero po ręcznym sprawdzeniu.
- [prompt i odpowiedź](_przebieg/1185-weryfikator-dodatkow.md) · 7.6 s · $0.0811

### 1186 · audytor_pokrycia · dział 01

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 5 z 8 spełnione
- [prompt i odpowiedź](_przebieg/1186-audytor-pokrycia.md) · 13.9 s · $0.0611

### 1187 · audytor_pokrycia · dział 02

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 4 z 9 spełnione
- [prompt i odpowiedź](_przebieg/1187-audytor-pokrycia.md) · 14.0 s · $0.0542

### 1188 · audytor_pokrycia · dział 03

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 8 z 10 spełnione
- [prompt i odpowiedź](_przebieg/1188-audytor-pokrycia.md) · 15.9 s · $0.0555

### 1189 · audytor_pokrycia · dział 04

- Wynik: 7 pokryte, 0 częściowo, 0 brak; obietnice: 5 z 8 spełnione
- [prompt i odpowiedź](_przebieg/1189-audytor-pokrycia.md) · 11.4 s · $0.0509

### 1190 · audytor_pokrycia · dział 05

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 5 z 9 spełnione
- [prompt i odpowiedź](_przebieg/1190-audytor-pokrycia.md) · 13.0 s · $0.0515

### 1191 · audytor_pokrycia · dział 06

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 4 z 8 spełnione
- [prompt i odpowiedź](_przebieg/1191-audytor-pokrycia.md) · 10.8 s · $0.0460

### 1192 · audytor_pokrycia · dział 07

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 5 z 12 spełnione
- [prompt i odpowiedź](_przebieg/1192-audytor-pokrycia.md) · 17.2 s · $0.0593

### 1193 · audytor_pokrycia · dział 08

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 8 z 16 spełnione
- [prompt i odpowiedź](_przebieg/1193-audytor-pokrycia.md) · 14.7 s · $0.0596

### 1194 · audytor_pokrycia · dział 09

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 8 z 16 spełnione
- [prompt i odpowiedź](_przebieg/1194-audytor-pokrycia.md) · 16.7 s · $0.0631

### 1195 · audytor_pokrycia · dział 10

- Wynik: 6 pokryte, 0 częściowo, 0 brak; obietnice: 2 z 10 spełnione
- [prompt i odpowiedź](_przebieg/1195-audytor-pokrycia.md) · 12.6 s · $0.0545

### 1196 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1196-audytor-obietnic.md) · 2.4 s · $0.0405

### 1197 · audytor_obietnic

- Wynik: Obietnica „Na razie nie piszemy kodu” spełniona w [sec-03-czym-jest-kod-zrodlowy].
- [prompt i odpowiedź](_przebieg/1197-audytor-obietnic.md) · 6.3 s · $0.0224

### 1198 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1198-audytor-obietnic.md) · 2.4 s · $0.0289

### 1199 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1199-audytor-obietnic.md) · 4.4 s · $0.0138

### 1200 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1200-audytor-obietnic.md) · 2.5 s · $0.0265

### 1201 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1201-audytor-obietnic.md) · 4.1 s · $0.0136

### 1202 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1202-audytor-obietnic.md) · 5.9 s · $0.0274

### 1203 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1203-audytor-obietnic.md) · 3.8 s · $0.0127

### 1204 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1204-audytor-obietnic.md) · 2.6 s · $0.0155

### 1205 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1205-audytor-obietnic.md) · 4.3 s · $0.0132

### 1206 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1206-audytor-obietnic.md) · 4.0 s · $0.0194

### 1207 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1207-audytor-obietnic.md) · 4.0 s · $0.0127

### 1208 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1208-audytor-obietnic.md) · 5.5 s · $0.0193

### 1209 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1209-audytor-obietnic.md) · 3.8 s · $0.0125

### 1210 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1210-audytor-obietnic.md) · 3.9 s · $0.0118

### 1211 · audytor_obietnic

- [prompt i odpowiedź](_przebieg/1211-audytor-obietnic.md) · 3.9 s · $0.0125

### 1212 · redaktor_zdania

- Wynik: Usunięto niespełnioną obietnicę „U siebie zobaczysz to za chwilę w `kasa.py`”: „To jeszcze nie katastrofa, bo komunikat wskazuje linię i powód.”
- [prompt i odpowiedź](_przebieg/1212-redaktor-zdania.md) · 3.1 s · $0.0184

### 1213 · redaktor_zdania

- Wynik: Usunięto niespełnioną obietnicę „U siebie zobaczysz to za chwilę”: zdanie usunięte
- [prompt i odpowiedź](_przebieg/1213-redaktor-zdania.md) · 2.5 s · $0.0104

### 1214 · redaktor_zdania

- Wynik: Usunięto niespełnioną obietnicę „w warsztacie poniżej dopisujesz do swojego skryptu linię”: zdanie usunięte
- [prompt i odpowiedź](_przebieg/1214-redaktor-zdania.md) · 2.9 s · $0.0109

### 1215 · redaktor_zdania

- Wynik: Usunięto niespełnioną obietnicę „Za chwilę dopiszesz `na_osobe` i użyjesz obu”: „U siebie masz już `funkcje.py` z funkcją `suma`.”
- [prompt i odpowiedź](_przebieg/1215-redaktor-zdania.md) · 2.8 s · $0.0113

### 1216 · redaktor_zdania

- Wynik: Usunięto niespełnioną obietnicę „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`”: zdanie usunięte
- [prompt i odpowiedź](_przebieg/1216-redaktor-zdania.md) · 2.8 s · $0.0109

### 1217 · redaktor_zdania

- Wynik: Usunięto niespełnioną obietnicę „Usuwamy ją w warsztacie poniżej.”: zdanie usunięte
- [prompt i odpowiedź](_przebieg/1217-redaktor-zdania.md) · 3.2 s · $0.0116

### 1218 · redaktor_zdania

- Wynik: Usunięto niespełnioną obietnicę „pokażemy w ćwiczeniu praktycznym”: „Git trzeba mieć zainstalowanym (sprawdzisz to poleceniem `git --version`, a instalator jest na stronie git-scm.com).”
- [prompt i odpowiedź](_przebieg/1218-redaktor-zdania.md) · 3.2 s · $0.0124

### 1219 · klasyfikator_pułapek

- Wynik: 7 pułapek: temat 5, poboczne 2, bez klasyfikacji 0
- [prompt i odpowiedź](_przebieg/1219-klasyfikator-pulapek.md) · 3.1 s · $0.0220

### 1220 · redaktor_tytułów

- Wynik: Tytuły: 71 sprawdzonych, zmienionych 71: Czym jest programowanie → Wejdź w świat programowania; Czym jest program komputerowy → Zrozum, czym jest program; Czym jest programowanie → Odkryj sens programowania; Kim jest programista → Przyjrzyj się pracy programisty; Czym jest język programowania → Poznaj język programowania …
- [prompt i odpowiedź](_przebieg/1220-redaktor-tytulow.md) · 42.4 s · $0.1151

### 1221 · autor_ściągawki

- Wynik: Ściągawka: 45 pozycji w działach: 10 (bez sekcji: 0, ponad limit 50: 0, kod spoza sekcji usunięty: 0).
- [prompt i odpowiedź](_przebieg/1221-autor-sciagawki.md) · 40.8 s · $0.1201
