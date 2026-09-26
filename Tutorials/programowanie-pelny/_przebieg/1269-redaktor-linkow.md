# Krok 1269 · redaktor_linków

Węzeł: `review_links` · dział: 8 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 08 „Współpraca programu z użytkownikiem” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-103] fraza: „Do tej pory kwoty wpisywaliśmy w kodzie” (wstecz, wcześniejsze przykłady z kwotami wpisanymi na stałe w kodzie (wyjazdy))
  zdanie: Do tej pory kwoty wpisywaliśmy w kodzie, np. `mazury = [45.5, 20, 12.5]`. Wtedy każda zmiana danych wymagała edycji programu. Dane wejściowe rozdzielają obie sprawy: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne.
  cel: [Ponowne użycie kodu] Zmieniają się tylko dane: lista wydatków i liczba osób. Logika liczenia leży w jednym miejscu, więc nie kopiujesz pętli dla każdego wyjazdu.

[ref-104] fraza: „gdy zajmiemy się pytaniem użytkownika o informację” (w przód, input i zapytanie użytkownika)
  zdanie: Tak mogłoby wyglądać pobranie danych od użytkownika (szkic, do którego wrócimy, gdy zajmiemy się pytaniem użytkownika o informację):
  cel: [Pytanie użytkownika o informację] Program pyta użytkownika funkcją input: wypisuje pytanie, czeka, aż ktoś wpisze odpowiedź i naciśnie Enter, a potem oddaje tę odpowiedź jako wartość. To najprostszy sposób, by dane wejściowe przyszły od człowieka.

[ref-106] fraza: „o której mówiliśmy przy zwracaniu wyniku” (wstecz, print tylko pokazuje, nie zwraca)
  zdanie: Na razie znasz tylko pierwszą drogę: `print` pokazuje wartość w terminalu. Robiłeś to już w funkcji `wypisz_na_osobe`, o której mówiliśmy przy zwracaniu wyniku (przypomnienie: `print` tylko pokazuje tekst, niczego nie zwraca).
  cel: [Zwracanie wyniku przez funkcję] Pierwsza `75.0` pochodzi z `print` wewnątrz `wypisz_na_osobe`, w chwili wywołania. Druga to `wynik`, czyli wartość zwrócona i zapisana. Zmienna `nic` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła. Nazwy `wynik` i `nic` służą tylko tej ilustracji.

[ref-107] fraza: „Do plików wrócimy osobno” (w przód, pliki jako miejsce zapisu wyników)
  zdanie: Konsekwencja: o tym, co program wypisze, decydujesz Ty. Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. Do plików wrócimy osobno, a wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie.
  cel: [Czym jest plik] Plik to nazwana porcja danych zapisana na dysku, która istnieje także wtedy, gdy program już nie działa. Zmienne żyją tylko podczas pracy programu i znikają wraz z jego zakończeniem, a plik zostaje. Dlatego plik jest miejscem, z którego dane wejściowe przychodzą i do którego trafiają dane wyjściowe.

[ref-108] fraza: „opiszemy przy interfejsie” (w przód, interfejs użytkownika, rozmowa z użytkownikiem)
  zdanie: Konsekwencja: o tym, co program wypisze, decydujesz Ty. Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. Do plików wrócimy osobno, a wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie.
  cel: [Czym jest interfejs użytkownika] Interfejs użytkownika to część programu, przez którą człowiek się z nim komunikuje: to, co program wyświetla, oraz sposób, w jaki przyjmuje od człowieka dane i polecenia. Użytkownik nie widzi kodu, widzi tylko interfejs.

[ref-109] fraza: „kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne” (wstecz, kod stały, dane zmienne)
  zdanie: Konsekwencja: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne. Ale `float("abc")` przerwie program błędem. Jak się przed tym bronić, pokażemy przy sprawdzaniu danych wpisanych przez użytkownika.
  cel: [Dane wejściowe programu] Do tej pory kwoty wpisywaliśmy w kodzie, np. `mazury = [45.5, 20, 12.5]`. Wtedy każda zmiana danych wymagała edycji programu. Dane wejściowe rozdzielają obie sprawy: kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne.

[ref-110] fraza: „przykładzie, który będzie nam towarzyszył” (w przód, program „Wspólna Kasa” wracający w kolejnych sekcjach)
  zdanie: Pokażemy to na przykładzie, który będzie nam towarzyszył: „Wspólnej Kasie”, czyli programie do rozliczania wspólnych wydatków znajomych. Zaczynamy dobudowywać do niego pytania do użytkownika, a pierwsze dotyczy nowego wydatku:
  cel: [Po co zapisywać wersje kodu] Robi to Git, program do zapisywania historii plików. Zapis jednej wersji to commit: zdjęcie wybranych plików z danej chwili, z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię, to repozytorium. W przykładowym programie do dzielenia wydatków, „Wspólnej Kasie”, będzie nim folder `wspolna_kasa`, w którym leżą pliki programu.

[ref-111] fraza: „`input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`” (wstecz, input zwraca tekst)
  zdanie: Uwaga: plik przechowuje wyłącznie tekst, więc kwotę po wczytaniu trzeba znów zamienić przez `float()`, bo `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Pułapką jest tryb `"w"`, który kasuje starą zawartość. Zanim ktoś wpisze do pliku coś błędnego, warto dane sprawdzić, o czym powiemy przy sprawdzaniu danych użytkownika.
  cel: [Pytanie użytkownika o informację] Pułapka: `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Dla Pythona to wciąż „45.5” w cudzysłowie, czyli tekst, którego nie da się dzielić ani dodawać do liczb (skończyłoby się to błędem TypeError). Dlatego `float()` zamienia tekst na liczbę. Spacja na końcu pytania oddziela je od tego, co wpisze użytkownik.

[ref-112] fraza: „o czym powiemy przy sprawdzaniu danych użytkownika” (w przód, walidacja danych wpisanych przez użytkownika)
  zdanie: Uwaga: plik przechowuje wyłącznie tekst, więc kwotę po wczytaniu trzeba znów zamienić przez `float()`, bo `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Pułapką jest tryb `"w"`, który kasuje starą zawartość. Zanim ktoś wpisze do pliku coś błędnego, warto dane sprawdzić, o czym powiemy przy sprawdzaniu danych użytkownika.
  cel: [Po co sprawdzać dane użytkownika] Program powinien sprawdzać dane od użytkownika, bo człowiek potrafi wpisać coś, czego kod się nie spodziewał, a wtedy program albo się zatrzyma, albo policzy coś błędnego.

[ref-113] fraza: „dwie znane już rzeczy: input do pytań i print do wyników” (wstecz, input i print poznane w wcześniejszych sekcjach)
  zdanie: Interfejs bywa różny. W interfejsie tekstowym, czyli takim, który działa w terminalu na samych napisach, program zadaje pytania, a Ty odpisujesz z klawiatury. W interfejsie graficznym są okna i przyciski. Nasza „Wspólna Kasa” zostaje przy wersji tekstowej, bo wystarczą do niej dwie znane już rzeczy: input do pytań i print do wyników.
  cel: [Pytanie użytkownika o informację] Program pyta użytkownika funkcją input: wypisuje pytanie, czeka, aż ktoś wpisze odpowiedź i naciśnie Enter, a potem oddaje tę odpowiedź jako wartość. To najprostszy sposób, by dane wejściowe przyszły od człowieka. Tekst w nawiasach to pytanie, które zobaczy użytkownik. Wynik `input` przypisujesz do zmiennej, jak każdą wartość zwracaną. Program stoi w miejscu, dopóki odpowiedź nie nadejdzie. Pokażemy to na przykładzie, który będzie nam towarzysz

[ref-114] fraza: „suchy wynik nic nie mówi komuś, kto nie zna kodu” (wstecz, wniosek o opisywaniu wyniku z sekcji o danych wyjściowych)
  zdanie: Interfejs ma dwie strony: **wejście** (pytania, odpowiedzi) i **wyjście** (wyniki, komunikaty). To dokładnie dane wejściowe i dane wyjściowe, tylko widziane oczami człowieka. Stąd wniosek z wcześniejszych sekcji: suchy wynik nic nie mówi komuś, kto nie zna kodu, więc trzeba go opisać.
  cel: [Dane wyjściowe programu] Konsekwencja: o tym, co program wypisze, decydujesz Ty. Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. Do plików wrócimy osobno, a wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie.

[ref-116] fraza: „zawsze zwraca tekst” (wstecz, input zawsze zwraca tekst, nawet gdy ktoś wpisze liczbę)
  zdanie: Ta kontrola to walidacja: sprawdzenie, czy wpisana wartość nadaje się do dalszej pracy, zanim program jej użyje. Pamiętasz, że input zawsze zwraca tekst. Gdy ktoś na pytanie „Ile zapłacił?” wpisze `abc`, samo `float("abc")` przerwie program komunikatem o błędzie. A gdy wpisze `-5`, program nie zgłosi żadnego błędu i po cichu policzy złe saldo.
  cel: [Pytanie użytkownika o informację] Pułapka: `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Dla Pythona to wciąż „45.5” w cudzysłowie, czyli tekst, którego nie da się dzielić ani dodawać do liczb (skończyłoby się to błędem TypeError). Dlatego `float()` zamienia tekst na liczbę. Spacja na końcu pytania oddziela je od tego, co wpisze użytkownik.
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-103",
      "keep": false,
      "reason": "Cel to ponowne użycie kodu, nie kwoty wpisane w kodzie; nie mówi tego, co fraza."
    },
    {
      "id": "ref-104",
      "keep": true,
      "reason": "Zapowiedź wraca do sekcji o input; cel trafny."
    },
    {
      "id": "ref-106",
      "keep": true,
      "reason": "Cel pokazuje print w wypisz_na_osobe kontra zwracanie wyniku."
    },
    {
      "id": "ref-107",
      "keep": true,
      "reason": "Cel wyjaśnia, czym jest plik, jako miejsce zapisu wyników."
    },
    {
      "id": "ref-108",
      "keep": true,
      "reason": "Cel definiuje interfejs użytkownika, o którym mowa."
    },
    {
      "id": "ref-109",
      "keep": true,
      "reason": "Cel to sekcja o danych wejściowych, gdzie stoi to zdanie; trafne."
    },
    {
      "id": "ref-110",
      "keep": false,
      "reason": "Cel to Git i wersje kodu; tylko przypadkowo wspomina Wspólną Kasę, nie jest to zapowiedź przykładu."
    },
    {
      "id": "ref-111",
      "keep": true,
      "reason": "Cel dokładnie tłumaczy, że input zwraca tekst."
    },
    {
      "id": "ref-112",
      "keep": true,
      "reason": "Cel wyjaśnia, po co sprawdzać dane użytkownika."
    },
    {
      "id": "ref-113",
      "keep": false,
      "reason": "Fraza to ogólnik o znanych rzeczach; cel input już wcześniej podlinkowany, rozprasza."
    },
    {
      "id": "ref-114",
      "keep": true,
      "reason": "Cel zawiera wniosek o opisywaniu wyniku."
    },
    {
      "id": "ref-116",
      "keep": true,
      "reason": "Przypomnienie, że input zwraca tekst; cel to wyjaśnia."
    }
  ]
}
````
