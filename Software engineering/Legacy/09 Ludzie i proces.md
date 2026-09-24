# Ludzie i proces

Kod legacy to także problem wiedzy: kto wie, jak działa fakturowanie, dlaczego numeracja resetuje się w styczniu i co się stanie, jeśli KSeF nie odpowie. Ta wiedza jest często w głowach kilku osób albo tylko w kodzie. Ten rozdział opisuje, jak ją odzyskać i rozproszyć, jak wprowadzać nowe osoby i jak łączyć pracę nad długiem z dostarczaniem funkcji.

```text
ryzyko                               działanie
wiedza w jednej głowie               pary, mob, rotacja, zapis decyzji
wiedza tylko w kodzie                testy charakteryzujące, ADR z archeologii, słownik pojęć
nowa osoba nie wie, od czego zacząć  mapa systemu, pierwsze zadania w hotspotach z opiekunem
dług rośnie szybciej niż spłata      budżet na dług, refaktoryzacja przy zmianach, cele mierzalne
```

## Wiedza w kilku głowach

<a id="term-bus-factor"></a>[Bus factor](00%20Glossary%20Legacy.md#bus-factor) to liczba osób, których nagłe odejście z projektu (np. wpadnięcie pod autobus) zatrzymałoby rozwój. W wielu systemach legacy wynosi jeden. Jest jedna osoba, która „wie, jak działa fakturowanie”.

Bus factor można oszacować z historii gita. Pliki, w których jedna osoba jest autorem większości linii, to miejsca, gdzie wiedza jest skupiona:

```bash
# udział autorów w liniach pliku
git blame --line-porcelain billing/invoices.py | grep "^author " | sort | uniq -c | sort -rn

#  342 author Marek Nowak
#   41 author Anna Kowalska
#   17 author bot-dependabot
```

Techniki przenoszenia wiedzy z głów:

- <a id="term-pair-programming"></a>[programowanie w parach](00%20Glossary%20Legacy.md#pair-programming), w którym osoba znająca kod prowadzi, a druga przejmuje klawiaturę przy kolejnych zadaniach w tym obszarze,
- <a id="term-mob-programming"></a>[mob programming](00%20Glossary%20Legacy.md#mob-programming): cały zespół pracuje nad jednym zadaniem przy jednym ekranie. W legacy szczególnie skuteczny przy pierwszych zmianach w nieznanym module, bo wszyscy uczą się jednocześnie,
- nagrywane sesje, w których ekspert opowiada o module, przechodząc przez kod, z pytaniami zespołu,
- rotacja: zadania w danym obszarze celowo trafiają do osób, które go nie znają, z ekspertem jako recenzentem,
- testy charakteryzujące pisane razem z ekspertem. Każdy test to utrwalona wiedza: „ten przypadek tak działa, bo…”.

Gdy wiedza istnieje już tylko w kodzie, bo autorzy odeszli, źródłem jest archeologia z rozdziału 02 i testy z rozdziału 03. Wynik warto zapisać tak, żeby nie trzeba było go odtwarzać drugi raz.

<a id="term-adr"></a>[ADR](00%20Glossary%20Legacy.md#adr) (Architecture Decision Record), zaproponowany przez Michaela Nygarda, to krótki dokument opisujący jedną decyzję: kontekst, decyzję i konsekwencje. W legacy można je pisać także wstecz, dla decyzji odtworzonych z historii:

```markdown
# ADR-014: Numeracja faktur resetuje się 1 stycznia

Status: zaakceptowana (odtworzona w 2026 z historii repozytorium)

## Kontekst
Przepisy wymagają ciągłej numeracji faktur w ramach roku. Commit a3f9c21 (2015-01-02,
„fix numeracja nowy rok”) dodał rok do numeru po reklamacji biura rachunkowego.

## Decyzja
Numer ma format FV/<rok>/<kolejny numer w roku>. Sekwencja `invoice` jest resetowana
przez zadanie cron `reset_invoice_seq` 1 stycznia o 00:00.

## Konsekwencje
- Faktury wystawiane między 23:59 a 00:00 31 grudnia mogą dostać numer z nowego roku
  (znany problem, zgłoszenie INV-88).
- Zmiana formatu numeru wymaga zgody działu księgowości.
```

Obok ADR przydaje się słownik pojęć domeny (co znaczy „odwrotne obciążenie”, „korekta”, „faktura zaliczkowa”) oraz krótka mapa systemu: moduły, punkty wejścia, zależności, właściciele. Wszystkie te dokumenty trzymane w repozytorium, obok kodu, starzeją się wolniej niż wiki.

## Nowe osoby w starym kodzie

Onboarding do legacy trwa dłużej niż do nowego kodu, bo brakuje dokumentacji, testów i jasnych granic. Kilka praktyk znacznie go skraca:

- działające środowisko lokalne w jeden dzień. Jeśli uruchomienie systemu wymaga tygodnia i pomocy trzech osób, to jest pierwszy dług do spłacenia. Skrypt, Docker Compose i opis w README zwracają się przy każdej nowej osobie,
- mapa systemu i słownik pojęć zamiast „przeczytaj kod”,
- pierwsze zadania małe, ale prawdziwe, najlepiej w hotspotach, bo tam jest największa wartość wiedzy. Na przykład test charakteryzujący dla fragmentu `generate_invoice` albo mała poprawka z parą,
- opiekun (buddy), który odpowiada na pytania bez oceniania. W legacy „głupich pytań” jest dużo, bo kod często jest nieintuicyjny,
- nowa osoba zapisuje, co było niejasne, i poprawia dokumentację. Świeże spojrzenie jest najlepszym testem dokumentacji.

Bus factor zmniejsza się też organizacyjnie: każdy obszar ma co najmniej dwie osoby, które potrafią w nim pracować, code review w obszarach krytycznych wykonuje ktoś spoza „właściciela”, a urlop eksperta jest traktowany jako test, czy wiedza została rozproszona.

## Dług i funkcje równocześnie

Rzadko jest możliwe zatrzymanie funkcji na kwartał, żeby spłacić dług. Praca nad legacy musi toczyć się równolegle z rozwojem. Są trzy popularne podejścia, najlepiej łączone:

<a id="term-debt-budget"></a>[Budżet na dług](00%20Glossary%20Legacy.md#debt-budget): stały procent pojemności zespołu (często 15–20 procent) przeznaczony na pracę nad długiem, uzgodniony z biznesem z góry. Zespół sam decyduje, na co go przeznaczyć, zwykle na hotspoty. Zaletą jest przewidywalność, a ryzykiem to, że budżet jest pierwszą ofiarą presji terminów.

Refaktoryzacja przy zmianach: dług spłaca się tam, gdzie i tak toczy się praca, jako refaktoryzacja przygotowująca i zasada skauta z rozdziału 05. To najtańsze podejście, bo nie wymaga osobnej zgody, ale samo nie poradzi sobie z dużymi zmianami, takimi jak wymiana biblioteki czy modułu.

Zadania długu w backlogu obok funkcji, każde z uzasadnieniem biznesowym i miarą efektu, jak w rozdziale 08. Nadaje się do większych zmian, np. wydzielenia modułu fakturowania.

Niezależnie od podejścia pomagają mierzalne cele, które pokazują postęp:

| Miara | Przykład celu | Skąd dane |
|---|---|---|
| czas realizacji zmian w obszarze | zmiana reguły VAT z 8 dni do 2 | system zgłoszeń |
| liczba incydentów | błędne faktury z 12 do 3 miesięcznie | support, księgowość |
| pokrycie testami hotspotów | `billing/` z 0 do 70 procent | `coverage`, CI |
| złożoność hotspotu | `generate_invoice` z 110 do 30 | `radon`, skrypt z rozdziału 02 |
| bus factor krytycznych obszarów | co najmniej 2 osoby dla fakturowania | `git blame`, rotacja zadań |
| czas onboardingu | pierwsza zmiana na produkcji w 5 dni | obserwacja zespołu |

Cele warto przeglądać regularnie, np. co kwartał, razem z biznesem. Widoczny postęp buduje zaufanie, że czas poświęcony na legacy przynosi efekty, i ułatwia uzyskanie go w przyszłości.

## Co zapamiętać

- Bus factor pokazuje, ile osób może odejść, zanim projekt stanie. `git blame` pomaga go oszacować.
- Wiedzę przenosi się przez pary, mob programming, rotację, nagrania i testy pisane razem z ekspertami.
- ADR zapisują decyzje, także odtworzone wstecz z historii. Słownik pojęć i mapa systemu w repozytorium starzeją się wolniej niż wiki.
- Onboarding do legacy skraca działające środowisko w jeden dzień, mapa systemu, małe prawdziwe zadania w hotspotach i opiekun.
- Dług spłaca się równolegle z funkcjami: budżet na dług, refaktoryzacja przy zmianach i zadania długu z uzasadnieniem biznesowym.
- Mierzalne cele (czas zmian, incydenty, pokrycie, złożoność, bus factor) pokazują postęp i budują zaufanie biznesu.

## Pytania sprawdzające

### 35. Jak odzyskać wiedzę, która istnieje tylko w głowach kilku osób (albo już tylko w kodzie)?

<details>
<summary>Odpowiedź</summary>

Najpierw ocenić bus factor, np. przez udział autorów w liniach plików (`git blame --line-porcelain`). Wiedzę z głów przenosi się przez programowanie w parach, mob programming przy pierwszych zmianach, nagrywane sesje z ekspertem, rotację zadań z ekspertem jako recenzentem i testy charakteryzujące pisane razem z nim. Gdy wiedza jest tylko w kodzie, źródłem są archeologia w historii i testy. Wynik zapisuje się jako ADR (także wstecz, dla odtworzonych decyzji), słownik pojęć i mapę systemu w repozytorium.

Zobacz: sekcja „Wiedza w kilku głowach”.

</details>

### 36. Jak wprowadzić nowe osoby do zespołu pracującego z legacy i jak ograniczyć ryzyko wiedzy skupionej w jednej osobie?

<details>
<summary>Odpowiedź</summary>

Zapewnić działające środowisko lokalne w jeden dzień (skrypt, Docker Compose, README), mapę systemu i słownik pojęć, małe, ale prawdziwe pierwsze zadania w hotspotach, opiekuna odpowiadającego na pytania i zachętę, żeby nowa osoba poprawiała dokumentację. Ryzyko wiedzy w jednej osobie ogranicza się organizacyjnie: co najmniej dwie osoby na obszar, code review spoza „właściciela” w obszarach krytycznych, a urlop eksperta traktuje się jako test rozproszenia wiedzy.

Zobacz: sekcja „Nowe osoby w starym kodzie”.

</details>

### 37. Jak łączyć pracę nad długiem z dostarczaniem funkcji (budżet na dług, refaktoryzacja przy okazji zmian, cele mierzalne)?

<details>
<summary>Odpowiedź</summary>

Łącząc trzy podejścia. Budżet na dług to stały procent pojemności (15–20 procent) uzgodniony z biznesem: przewidywalny, ale pierwszy do ścięcia pod presją. Refaktoryzacja przy zmianach, czyli przygotowująca i zasada skauta: najtańsza, ale nie obsłuży dużych zmian. Zadania długu w backlogu z uzasadnieniem biznesowym dla większych prac. Postęp pokazują mierzalne cele: czas realizacji zmian, liczba incydentów, pokrycie testami hotspotów, złożoność, bus factor i czas onboardingu, przeglądane regularnie z biznesem.

Zobacz: sekcja „Dług i funkcje równocześnie”.

</details>
