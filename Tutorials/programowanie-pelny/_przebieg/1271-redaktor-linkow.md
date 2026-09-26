# Krok 1271 · redaktor_linków

Węzeł: `review_links` · dział: 10 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 10 „Programowanie w praktyce” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-127] fraza: „Program do dzielenia wspólnych wydatków między osoby, który budujesz w warsztacie” (wstecz, program do dzielenia wydatków z wcześniejszych działów)
  zdanie: Różni je skala i interfejs: przyciski i mapy zamiast pytań w terminalu. Program do dzielenia wspólnych wydatków między osoby, który budujesz w warsztacie (nazywamy go „Wspólna Kasa”), należy do tej samej rodziny: bierze wydatki, liczy i wypisuje, kto ile zapłacił. Jest po prostu mały. Czym różni się strona internetowa od aplikacji mobilnej, wyjaśnimy w następnej sekcji.
  cel: [Błąd składni a błąd logiczny] Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.

[ref-128] fraza: „dane wejściowe, przetwarzanie, dane wyjściowe” (wstecz, schemat wejście-przetwarzanie-wyjście z poprzedniej sekcji)
  zdanie: Pod spodem obie robią to samo, co każdy program: dane wejściowe, przetwarzanie, dane wyjściowe. We „Wspólnej Kasie” wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.
  cel: [Programy używane na co dzień] Na co dzień używasz dziesiątek programów, choć rzadko o tym myślisz: komunikatora, mapy, banku w telefonie, arkusza kalkulacyjnego, przeglądarki. Każdy z nich to program albo aplikacja, czyli program z oprawą dla użytkownika, i działa według tego samego schematu, który znasz z własnych skryptów. Zawsze są dane wejściowe, jakieś przetwarzanie i dane wyjściowe: | Program | Wejście | Co robi | Wyjście | |---|---|---|---|

[ref-129] fraza: „jak w sekcji o zapisywaniu wersji kodu” (wstecz, commit jako działający punkt powrotu)
  zdanie: Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, jak w sekcji o zapisywaniu wersji kodu. Dzięki temu nie zgadujesz, gdzie szukać błędu.
  cel: [Po co zapisywać wersje kodu] Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast szukać własnych zmian z pamięci. Robi to Git, program do zapisywania historii plików. Zapis jednej wersji to commit: zdjęcie wybranych plików z danej chwili, z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię, to repozytorium. W przykładowym programie do dzielenia wydatków, „Ws

[ref-130] fraza: „szukanie po ostatniej linii komunikatu” (wstecz, szukanie rozwiązań w internecie po ostatniej linii komunikatu o błędzie)
  zdanie: | Umiejętność | Do czego służy | Przykład we Wspólnej Kasie | |---|---|---| | Rozumienie problemu | ustalenie, co program ma zrobić | „Kto komu ile jest winien?” zamiast „policz sumę” | | Komunikacja | pytania, opisy zmian | pytanie, czy dzielimy po równo | | Cierpliwość w szukaniu błędów | spokojne zawężanie przyczyny | sprawdzanie wartości wypisanych przez print | | Szukanie informacji | radzeni
  cel: [Szukanie rozwiązań w internecie] Ostatnia linia Tracebacku to ta, którą, jak w sekcji o czytaniu komunikatów, czytasz od dołu. Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych, bo nikt inny ich nie ma.

[ref-131] fraza: „sekcji o budowie programu od pomysłu” (wstecz, pętla budowy programu: pomysł, opis, kod, uruchomienie, commit)
  zdanie: To ta sama pętla, którą znasz z sekcji o budowie programu od pomysłu. Różnica jest tylko w tym, że teraz to Ty wybierasz pomysł. Dobry pierwszy problem jest mały, znany z życia i da się go sprawdzić na kartce: rozliczenie wydatków, lista zakupów, przeliczanie kwot z arkusza.
  cel: [Od pomysłu do działającego programu] ```text pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit ↑ | └──────────────────── następny kawałek ←─────────────────────┘ ```

[ref-132] fraza: „w sekcji o rozwiązaniach w internecie: po ostatniej linii komunikatu” (wstecz, szukanie rozwiązania po ostatniej linii komunikatu)
  zdanie: Nie kopiuj gotowców bez zrozumienia. Lepiej napisać własną, kulawą wersję niż wkleić cudzą. Gdy utkniesz, szukaj tak, jak w sekcji o rozwiązaniach w internecie: po ostatniej linii komunikatu.
  cel: [Szukanie rozwiązań w internecie] Wpisz w wyszukiwarkę to, co widzisz: ostatnią linię komunikatu o błędzie i nazwę języka. Prawie każdy błąd ktoś już miał i ktoś już opisał, jak go naprawić. Ostatnia linia Tracebacku to ta, którą, jak w sekcji o czytaniu komunikatów, czytasz od dołu. Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych, bo nikt inny ich nie ma. ```text python TypeError: unsupported operand type(s) for /: 'str' and 'int' ``` Gdy nie ma ko

[ref-133] fraza: „Wspólna Kasa to jej przykład” (wstecz, Wspólna Kasa jako przykładowy program z tutoriala)
  zdanie: Kolejne elementy dokładaj po jednym: dane, decyzje, pętle, funkcje, pliki, testy. Ten tutorial jest taką drogą, a Wspólna Kasa to jej przykład.
  cel: [Strona internetowa a aplikacja mobilna] Pod spodem obie robią to samo, co każdy program: dane wejściowe, przetwarzanie, dane wyjściowe. We „Wspólnej Kasie” wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.

[ref-135] fraza: „tą samą pętlą nauki” (wstecz, pętla nauki: mały problem, opis, kod, uruchomienie, commit)
  zdanie: Konsekwencja jest praktyczna: zaczynasz od małego, nudnego zadania z własnej pracy i piszesz je tą samą pętlą nauki. Po commicie masz gotowe narzędzie, do którego możesz wracać. W warsztacie zapisujesz w ten sposób swój `dlugi.py`.
  cel: [Od czego zacząć naukę] ```text mały problem → opis krokowy → kilka linii kodu → uruchomienie → commit ```

[ref-136] fraza: „Tak wygląda to we Wspólnej Kasie” (wstecz, przykładowy program Kasa dzielący rachunek)
  zdanie: Mechanizm znasz: to pętla po danych i funkcja. Zamiast przepisywać kwoty do kalkulatora, opisujesz kroki raz, a program wykonuje je dla dowolnej liczby pozycji. Tak wygląda to we Wspólnej Kasie:
  cel: [Strona internetowa a aplikacja mobilna] Pod spodem obie robią to samo, co każdy program: dane wejściowe, przetwarzanie, dane wyjściowe. We „Wspólnej Kasie” wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-127",
      "keep": false,
      "reason": "Cel to przykład błędu logicznego, nie opis programu Wspólna Kasa; nie daje tego, co obiecuje fraza."
    },
    {
      "id": "ref-128",
      "keep": true,
      "reason": "Cel pokazuje schemat wejście-przetwarzanie-wyjście w tabeli; czytelnik może chcieć sprawdzić."
    },
    {
      "id": "ref-129",
      "keep": true,
      "reason": "Cel wyjaśnia commit jako punkt powrotu, dokładnie to, o czym mówi fraza."
    },
    {
      "id": "ref-130",
      "keep": true,
      "reason": "Cel mówi o kopiowaniu ostatniej linii komunikatu przy szukaniu w internecie."
    },
    {
      "id": "ref-131",
      "keep": true,
      "reason": "Cel to schemat pętli budowy programu od pomysłu, zgodny z frazą."
    },
    {
      "id": "ref-132",
      "keep": true,
      "reason": "Cel opisuje szukanie po ostatniej linii komunikatu, zgodnie z frazą."
    },
    {
      "id": "ref-133",
      "keep": false,
      "reason": "Fraza mówi o Wspólnej Kasie jako przykładzie tutorialu, a cel to sekcja o stronie i aplikacji mobilnej; nie pasuje."
    },
    {
      "id": "ref-135",
      "keep": true,
      "reason": "Cel pokazuje pętlę nauki: mały problem, opis, kod, uruchomienie, commit."
    },
    {
      "id": "ref-136",
      "keep": false,
      "reason": "Fraza zapowiada kod przykładu, a cel to ogólny akapit o stronie i aplikacji; nie pokazuje pętli ani funkcji."
    }
  ]
}
````
