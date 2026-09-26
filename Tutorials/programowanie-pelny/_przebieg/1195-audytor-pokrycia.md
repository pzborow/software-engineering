# Krok 1195 · audytor_pokrycia

Węzeł: `coverage` · dział: 10 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 56. Jakie są przykłady programów używanych na co dzień?
  odpowiedź: Na co dzień używasz nawigacji, banku w telefonie, arkusza kalkulacyjnego, wyszukiwarki czy budzika. Każdy z nich przyjmuje dane wejściowe, przetwarza je i zwraca wynik. Pod spodem działają te same klocki co w Twoich skryptach: zmienne, decyzje, pętle, funkcje i pliki.
  sekcje pisarza: sec-10-programy-uzywane-na-co-dzien
- 57. Czym różni się strona internetowa od aplikacji mobilnej?
  odpowiedź: Strona internetowa działa w przeglądarce, jest pobierana z serwera przy każdym otwarciu i nie wymaga instalacji. Aplikacja mobilna jest zainstalowana w telefonie, ma szerszy dostęp do aparatu i czujników i często działa bez internetu, ale trzeba ją pobierać i aktualizować. Pod spodem obie robią to samo: przyjmują dane, przetwarzają je i pokazują wynik.
  sekcje pisarza: sec-10-strona-internetowa-a-aplikacja-mobilna
- 58. Jak od pomysłu dojść do działającego programu?
  odpowiedź: Dochodzi się do niego małymi krokami: opisujesz zadanie zwykłymi słowami, rozbijasz je na kroki i piszesz najmniejszy kawałek kodu. Sprawdzasz go na danych o znanym wyniku, zapisujesz commit i dopiero potem dokładasz następny kawałek. Dzięki temu błąd zawsze leży w ostatniej zmianie.
  sekcje pisarza: sec-10-od-pomyslu-do-dzialajacego-programu
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
  odpowiedź: Programiście oprócz kodowania przydają się: rozumienie problemu i potrzeb użytkownika, komunikacja (rozmowa, opisy zmian, komentarze), cierpliwość w szukaniu błędów, umiejętność szukania informacji i uczenia się oraz dokładność. Większość pracy to ustalanie, co program ma robić, i sprawdzanie, czy robi to dobrze. Wiele z tych umiejętności możesz mieć już z innych zajęć.
  sekcje pisarza: sec-10-umiejetnosci-poza-kodowaniem
- 60. Od czego zacząć samodzielną naukę programowania?
  odpowiedź: Zacznij od jednego małego problemu z własnego życia i jednego języka, np. Pythona. Pisz i uruchamiaj kod regularnie, małymi kawałkami: opis, kilka linii, uruchomienie, commit. Własna, nawet kulawa wersja uczy więcej niż wklejony gotowiec, a kolejne elementy (pętle, funkcje, pliki, testy) dokładasz po jednym.
  sekcje pisarza: sec-10-od-czego-zaczac-nauke
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?
  odpowiedź: Automatyzacja zleca komputerowi powtarzalne, jasno opisane czynności, np. sumowanie kwot czy podział rachunku. Oszczędza czas i eliminuje pomyłki przy dużej liczbie pozycji, bo pętla i funkcja robią to samo dla trzech danych i dla dwustu. Opłaca się zadanie częste, o jasnych regułach, które da się sprawdzić na kartce.
  sekcje pisarza: sec-10-automatyzacja-prostych-zadan

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-41: „U siebie zobaczysz to za chwilę w `kasa.py`” (zapowiedź, że czytelnik zobaczy komunikat o błędzie we własnym pliku kasa.py)
- ref-51: „U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika)
- ref-66: „w warsztacie poniżej dopisujesz do swojego skryptu linię” (zapowiedź warsztatu i skryptu, w którym czytelnik wywoła błąd TypeError)
- ref-93: „Za chwilę dopiszesz `na_osobe` i użyjesz obu” (zapowiedź ćwiczenia praktycznego z funkcją na_osobe)
- ref-96: „U siebie zobaczysz `TypeError` za chwilę w `funkcje.py`” (własny plik funkcje.py, w którym czytelnik zobaczy błąd)
- ref-102: „Usuwamy ją w warsztacie poniżej.” (zapowiedź poprawienia błędnej ostatniej linii w warsztacie)
- ref-124: „pokażemy w ćwiczeniu praktycznym” (praktyczne użycie Git na własnym komputerze)
- ref-126: „Czym różni się strona internetowa od aplikacji mobilnej, wyjaśnimy w następnej sekcji” (różnica między stroną internetową a aplikacją mobilną); ma ją spełnić pytanie 57
- ref-134: „W kolejnej sekcji zobaczysz, jak taki kawałek kodu zaczyna pracować za Ciebie” (automatyzacja prostych zadań); ma ją spełnić pytanie 61

SEKCJE DZIAŁU 10 "Programowanie w praktyce":
[sec-10-programy-uzywane-na-co-dzien] ## Programy używane na co dzień
Na co dzień używasz dziesiątek programów, choć rzadko o tym myślisz: komunikatora, mapy, banku w telefonie, arkusza kalkulacyjnego, przeglądarki. Każdy z nich to [[program-komputerowy|program]] albo [[aplikacja|aplikacja]], czyli program z oprawą dla użytkownika, i działa według tego samego schematu, który znasz z własnych skryptów.

Zawsze są [[dane-wejsciowe|dane wejściowe]], jakieś przetwarzanie i [[dane-wyjsciowe|dane wyjściowe]]:

| Program | Wejście | Co robi | Wyjście |
|---|---|---|---|
| Nawigacja | cel podróży, Twoja pozycja | wybiera najkrótszą trasę | trasa na mapie |
| Bank w telefonie | kwota i numer konta | sprawdza saldo, księguje przelew | potwierdzenie |
| Arkusz kalkulacyjny | liczby w komórkach | liczy wzory | sumy i wykresy |
| Wyszukiwarka | wpisane słowa | szuka i układa wyniki | lista stron |
| Alarm w telefonie | ustawiona godzina | porównuje ją z zegarem | dzwonek |

Pod spodem są te same klocki, które już budowałeś: zmienne, decyzje (`if`), pętle po listach, funkcje i pliki. Nawigacja też przegląda listę dróg i wybiera jedną, a bank też sprawdza dane od użytkownika, zanim cokolwiek zaksięguje.

Różni je skala i [[interfejs-uzytkownika|interfejs]]: przyciski i mapy zamiast pytań w terminalu. Program do dzielenia wspólnych wydatków między osoby, który budujesz w warsztacie (nazywamy go „Wspólna Kasa”), należy do tej samej rodziny: bierze wydatki, liczy i wypisuje, kto ile zapłacił. Jest po prostu mały. Czym różni się strona internetowa od aplikacji mobilnej, wyjaśnimy w następnej sekcji.

Konsekwencja: skoro gotowe programy to złożone proste kroki, da się je zrozumieć, a proste zadania z Twojej pracy da się zautomatyzować własnym małym programem.

[sec-10-strona-internetowa-a-aplikacja-mobilna] ## Strona internetowa a aplikacja mobilna
Strona internetowa działa w [[przegladarka|przeglądarce]] (programie do otwierania stron, np. Chrome czy Firefox) i otwierasz ją przez adres, a aplikacja mobilna to program zainstalowany w telefonie, pobrany ze sklepu. Obie są [[aplikacja|aplikacjami]] w sensie oprawy dla użytkownika, ale trafiają do niego inaczej.

Strona leży na cudzym komputerze, czyli [[serwer|serwerze]] (komputerze w internecie, który przechowuje stronę i odpowiada na zapytania). Przeglądarka pobiera ją za każdym razem, więc nic nie instalujesz, a autor może ją poprawić dla wszystkich naraz. Ta sama strona działa na komputerze, tablecie i telefonie.

Aplikacja mobilna jest zainstalowana na urządzeniu. Ma łatwiejszy dostęp do aparatu, powiadomień czy czujników i często działa bez internetu. Za to wymaga pobrania, aktualizacji i osobnej wersji dla każdego systemu, np. Androida i iOS.

| Cecha | Strona internetowa | Aplikacja mobilna |
|---|---|---|
| Uruchomienie | adres w przeglądarce | ikona na telefonie |
| Instalacja | brak | ze sklepu |
| Aktualizacja | automatyczna, u autora | pobierasz nową wersję |
| Dostęp do aparatu i czujników | ograniczony | szeroki |
| Bez internetu | zwykle nie działa | często działa |

Pod spodem obie robią to samo, co każdy program: dane wejściowe, przetwarzanie, dane wyjściowe. We „Wspólnej Kasie” wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.

Konsekwencja: rachunki możesz kiedyś udostępnić jako stronę, którą znajomi otworzą przez link, albo jako aplikację w telefonie. Na razie masz wersję w terminalu, a jej funkcje liczące przydałyby się w obu wariantach.

[sec-10-od-pomyslu-do-dzialajacego-programu] ## Od pomysłu do działającego programu
Od pomysłu do programu dochodzi się małymi krokami: opisujesz zadanie zwykłymi słowami, piszesz najmniejszy kawałek, który coś robi, sprawdzasz go i dopiero wtedy dokładasz następny. Cały program naraz zwykle nie działa, a szukanie błędu w stu liniach jest męczące.

```text
pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit
              ↑                                                            |
              └──────────────────── następny kawałek ←─────────────────────┘
```

Weźmy pomysł: „chcę wiedzieć, kto komu ile jest winien”. Opis krokowy to rozbicie zadania na kroki, z których każdy da się zrobić osobno: dla każdej osoby zsumuj to, co zapłaciła, odejmij jej równy udział i wypisz wynik. Z tego wychodzi jedna mała [[funkcja]]:

```python
def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...
```

Funkcję sprawdzasz na danych, których wynik znasz z kartki. Dopiero gdy się zgadza, zapisujesz [[commit]] (zapisaną wersję kodu z opisem) i myślisz o kolejnym kawałku, np. wczytaniu wydatków z pliku.

Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, jak w sekcji o zapisywaniu wersji kodu. Dzięki temu nie zgadujesz, gdzie szukać błędu.

[sec-10-umiejetnosci-poza-kodowaniem] ## Umiejętności poza kodowaniem
Poza samym pisaniem kodu programiście przydaje się przede wszystkim rozumienie problemu, jasne komunikowanie się i umiejętność uczenia się. Kod jest jednym z etapów pracy, a dużo czasu schodzi na to, co dzieje się przed nim i po nim.

| Umiejętność | Do czego służy | Przykład we Wspólnej Kasie |
|---|---|---|
| Rozumienie problemu | ustalenie, co program ma zrobić | „Kto komu ile jest winien?” zamiast „policz sumę” |
| Komunikacja | pytania, opisy zmian | pytanie, czy dzielimy po równo |
| Cierpliwość w szukaniu błędów | spokojne zawężanie przyczyny | sprawdzanie wartości wypisanych przez [[print]] |
| Szukanie informacji | radzenie sobie z nowym | szukanie po ostatniej linii komunikatu |
| Dokładność | pilnowanie szczegółów | kwota z kropką, nie z przecinkiem |

Rozumienie problemu oznacza rozmowę z osobą, dla której powstaje program. Zanim napiszesz [[funkcja|funkcję]], musisz wiedzieć, czy znajomi dzielą rachunek po równo i co ma się stać, gdy ktoś nie płaci. Błędne założenie kosztuje więcej niż literówka.

Komunikacja to także pisanie: czytelne nazwy, komentarze i opisy [[commit|commitów]] są wiadomością dla Ciebie za miesiąc i dla innych osób. Do tego dochodzi cierpliwość, bo błąd rzadko ustępuje od razu, oraz nawyk sprawdzania własnej pracy.

Żadna z tych umiejętności nie wymaga wiedzy technicznej, więc część z nich masz już z pracy i życia. Warto je ćwiczyć razem z kodowaniem.

[sec-10-od-czego-zaczac-nauke] ## Od czego zacząć naukę
Zacznij od jednego małego problemu, który naprawdę Cię dotyczy, i jednego języka, np. [[python|Pythona]]. Nie szukaj idealnego kursu ani najlepszego języka: liczy się to, żebyś pisał(a) kod co tydzień i uruchamiał(a) go u siebie.

Praktyczny początek wygląda tak:

```text
mały problem → opis krokowy → kilka linii kodu → uruchomienie → commit
```

To ta sama pętla, którą znasz z sekcji o budowie programu od pomysłu. Różnica jest tylko w tym, że teraz to Ty wybierasz pomysł. Dobry pierwszy problem jest mały, znany z życia i da się go sprawdzić na kartce: rozliczenie wydatków, lista zakupów, przeliczanie kwot z arkusza.

Nie kopiuj gotowców bez zrozumienia. Lepiej napisać własną, kulawą wersję niż wkleić cudzą. Gdy utkniesz, szukaj tak, jak w sekcji o rozwiązaniach w internecie: po ostatniej linii komunikatu.

Kolejne elementy dokładaj po jednym: dane, decyzje, pętle, funkcje, pliki, testy. Ten tutorial jest taką drogą, a Wspólna Kasa to jej przykład.

Warsztat poniżej to Twój pierwszy samodzielny krok: dopisujesz do Wspólnej Kasy jedną własną funkcję, która wypisuje, kto ile dopłaca albo dostaje, i zapisujesz ją jako [[commit]]. W kolejnej sekcji zobaczysz, jak taki kawałek kodu zaczyna pracować za Ciebie.

[sec-10-automatyzacja-prostych-zadan] ## Automatyzacja prostych zadań
[[automatyzacja|Automatyzacja]] to zlecenie komputerowi powtarzalnej czynności, którą wcześniej robiłeś(-aś) ręcznie. Osoba spoza IT zyskuje na niej czas i pewność: komputer nie nudzi się, nie myli przy setnej pozycji i robi to samo za każdym razem.

Mechanizm znasz: to [[petla|pętla]] po danych i [[funkcja|funkcja]]. Zamiast przepisywać kwoty do kalkulatora, opisujesz kroki raz, a program wykonuje je dla dowolnej liczby pozycji. Tak wygląda to we Wspólnej Kasie:

```python
wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.0},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.0},
           {"kto": "Celina", "opis": "bilety", "kwota": 15.0}]
osoby = ["Ania", "Bartek", "Celina"]
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(f"Razem: {suma} zł")
print(f"Na osobę: {suma / len(osoby)} zł")
```

```text
Razem: 180.0 zł
Na osobę: 60.0 zł
```

Jutro lista ma 200 wydatków zamiast trzech, a kod zostaje ten sam. Ten sam mechanizm obsłuży arkusz z fakturami czy listę zamówień w Twojej pracy.

Nie automatyzuj wszystkiego. Opłaca się zadanie, które powtarzasz często, ma jasne reguły i da się sprawdzić na kartce. Zadanie robione raz w roku lub wymagające oceny człowieka zwykle lepiej zostawić sobie.

Konsekwencja jest praktyczna: zaczynasz od małego, nudnego zadania z własnej pracy i piszesz je tą samą pętlą nauki. Po [[commit|commicie]] masz gotowe narzędzie, do którego możesz wracać. W warsztacie zapisujesz w ten sposób swój `dlugi.py`.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 56,
      "status": "covered",
      "section_ids": [
        "sec-10-programy-uzywane-na-co-dzien"
      ],
      "explanation": "Podaje przykłady (nawigacja, bank, arkusz, wyszukiwarka, alarm) z wejściem, przetwarzaniem i wyjściem oraz wskazuje wspólne klocki: zmienne, if, pętle, funkcje, pliki."
    },
    {
      "question_id": 57,
      "status": "covered",
      "section_ids": [
        "sec-10-strona-internetowa-a-aplikacja-mobilna"
      ],
      "explanation": "Wyjaśnia różnice: przeglądarka i serwer vs instalacja, aktualizacje, dostęp do aparatu i czujników, praca offline, plus tabela i wspólny schemat pod spodem."
    },
    {
      "question_id": 58,
      "status": "covered",
      "section_ids": [
        "sec-10-od-pomyslu-do-dzialajacego-programu"
      ],
      "explanation": "Opisuje cykl: opis słowami, rozbicie na kroki, mały kawałek kodu, sprawdzenie na znanych danych, commit, następny kawałek; uzasadnia, że błąd leży w ostatniej zmianie."
    },
    {
      "question_id": 59,
      "status": "covered",
      "section_ids": [
        "sec-10-umiejetnosci-poza-kodowaniem"
      ],
      "explanation": "Omawia rozumienie problemu, komunikację, cierpliwość, szukanie informacji i dokładność z przykładami; zaznacza, że część umiejętności czytelnik już ma."
    },
    {
      "question_id": 60,
      "status": "covered",
      "section_ids": [
        "sec-10-od-czego-zaczac-nauke"
      ],
      "explanation": "Radzi zacząć od małego problemu i jednego języka (Python), pisać regularnie małymi krokami, nie kopiować gotowców i dokładać elementy po jednym."
    },
    {
      "question_id": 61,
      "status": "covered",
      "section_ids": [
        "sec-10-automatyzacja-prostych-zadan"
      ],
      "explanation": "Definiuje automatyzację, pokazuje pętlę i funkcję na przykładzie, wyjaśnia zysk czasu i pewności oraz kiedy się opłaca (często, jasne reguły, sprawdzalne na kartce)."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-16",
      "status": "brak",
      "explanation": "Dział 10 nie odnosi się do zapowiedzi, że na razie nie ma kodu; to nie ta sekcja ją spełnia."
    },
    {
      "reference_id": "ref-41",
      "status": "brak",
      "explanation": "Brak komunikatu o błędzie w kasa.py w tym dziale."
    },
    {
      "reference_id": "ref-51",
      "status": "brak",
      "explanation": "Brak TypeError w pliku czytelnika w tym dziale."
    },
    {
      "reference_id": "ref-66",
      "status": "brak",
      "explanation": "Brak warsztatu z wywołaniem TypeError w tym dziale."
    },
    {
      "reference_id": "ref-93",
      "status": "brak",
      "explanation": "Brak funkcji na_osobe w tym dziale."
    },
    {
      "reference_id": "ref-96",
      "status": "brak",
      "explanation": "Brak funkcje.py i TypeError w tym dziale."
    },
    {
      "reference_id": "ref-102",
      "status": "brak",
      "explanation": "Brak usuwania błędnej ostatniej linii w tym dziale."
    },
    {
      "reference_id": "ref-124",
      "status": "brak",
      "explanation": "Git pojawia się tylko jako commit; brak ćwiczenia praktycznego z Git na własnym komputerze w sekcjach działu (warsztat jest tylko zapowiedziany)."
    },
    {
      "reference_id": "ref-126",
      "status": "spełniona",
      "section_id": "sec-10-strona-internetowa-a-aplikacja-mobilna",
      "quote": "Strona internetowa działa w przeglądarce",
      "explanation": "Sekcja wyjaśnia różnicę między stroną a aplikacją mobilną."
    },
    {
      "reference_id": "ref-134",
      "status": "spełniona",
      "section_id": "sec-10-automatyzacja-prostych-zadan",
      "quote": "Mechanizm znasz: to pętla po danych i funkcja.",
      "explanation": "Sekcja pokazuje kod, który sumuje wydatki i liczy podział, czyli pracuje za czytelnika."
    }
  ]
}
````
