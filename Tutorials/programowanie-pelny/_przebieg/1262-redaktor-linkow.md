# Krok 1262 · redaktor_linków

Węzeł: `review_links` · dział: 1 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 01 „Czym jest programowanie” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-1] fraza: „osoba, która zamienia potrzebę na instrukcje” (w przód, rola programisty, omówiona później)
  zdanie: Program „Wspólna Kasa” zrobi to za ciebie. Na wejściu dostanie listę wydatków (kto zapłacił i ile), a na wyjściu poda rozliczenie. Napisze go programista, czyli osoba, która zamienia potrzebę na instrukcje zrozumiałe dla komputera. Na razie nie piszemy kodu; ważne, że raz zapisane instrukcje można uruchamiać bez końca.
  cel: [Kim jest programista] Programista to osoba, która zamienia potrzebę na instrukcje: bierze problem opisany zwykłymi słowami i tworzy program, który go rozwiązuje. Pisanie kodu, czyli zapisanych w języku programowania instrukcji programu, to tylko część tej pracy.

[ref-2] fraza: „przykład, który będzie nam towarzyszył” (w przód, zapowiedź, że „Wspólna Kasa” wróci w kolejnych działach)
  zdanie: Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.
  cel: [Czym jest program komputerowy] Program komputerowy to zapisany z góry ciąg poleceń, które komputer wykonuje krok po kroku, żeby zamienić dane na wynik. Komputer sam nic nie wie ani nie zgaduje: robi dokładnie to, co mu zapisano. Pojedyncze polecenie to instrukcja, czyli jeden mały, jednoznaczny krok, np. „dodaj dwie liczby” albo „wypisz tekst na ekranie”. Program to wiele takich instrukcji ułożonych w określonej kolejności. Kalkulator, przeglądarka i gra działają tak samo, tylko mają in

[ref-3] fraza: „Na razie nie piszemy kodu” (w przód, zapowiedź, że kod pojawi się później)
  zdanie: Program „Wspólna Kasa” zrobi to za ciebie. Na wejściu dostanie listę wydatków (kto zapłacił i ile), a na wyjściu poda rozliczenie. Napisze go programista, czyli osoba, która zamienia potrzebę na instrukcje zrozumiałe dla komputera. Na razie nie piszemy kodu; ważne, że raz zapisane instrukcje można uruchamiać bez końca.
  cel: [Kim jest programista] Na razie nie piszemy kodu. Ten problem z wydatkami będzie jednak przykładem, który będzie nam towarzyszył: program „Wspólna Kasa” zbudujemy razem, a ty przećwiczysz w tej roli.

[ref-5] fraza: „Tym językiem zajmiemy się osobno” (w przód, język programowania)
  zdanie: Wróćmy do czworga znajomych z wyjazdu. Najpierw trzeba dokładnie ustalić, co jest problemem: kto komu ile ma oddać, żeby każdy zapłacił tyle samo. Potem rozbijasz to na kroki, które wykonałbyś na kartce: zsumuj wydatki, podziel przez liczbę osób, porównaj z tym, co kto zapłacił. Dopiero taki opis zapisujesz w języku programowania, czyli w ściśle określonym języku, który komputer potrafi odczytać. 
  cel: [Czym jest język programowania] Język programowania to ściśle określony sposób zapisywania instrukcji, który potrafi zrozumieć komputer. Ma własne słowa i reguły zapisu, ale jest o wiele prostszy i bardziej rygorystyczny niż język polski.

[ref-6] fraza: „Weźmy czworo znajomych z wyjazdu” (wstecz, przykład czworga znajomych rozliczających wyjazd z poprzedniej sekcji)
  zdanie: Weźmy czworo znajomych z wyjazdu, którzy męczą się z rozliczaniem wydatków w arkuszu. Ktoś musi ustalić, czego naprawdę potrzebują: czy program ma tylko wyliczyć, kto komu ile oddaje, czy też pamiętać kolejne wyjazdy. Potem opisuje rozwiązanie krok po kroku, zapisuje je w języku programowania, sprawdza na kilku przykładach i poprawia błędy.
  cel: [Czym jest program komputerowy] Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

[ref-8] fraza: „Na razie nie piszemy kodu” (w przód, kod pojawi się w dalszych działach)
  zdanie: Na razie nie piszemy kodu. Ten problem z wydatkami będzie jednak przykładem, który będzie nam towarzyszył: program „Wspólna Kasa” zbudujemy razem, a ty przećwiczysz w tej roli.
  cel: [Do czego służą komentarze] Komentarz to fragment pliku z kodem, który jest przeznaczony dla człowieka, a nie dla komputera. Służy do wyjaśnienia, po co coś jest napisane, bo sam kod pokazuje tylko, co robi. W Pythonie komentarz zaczyna się od znaku `#` i ciągnie do końca linii. Interpreter pomija go w całości, więc komentarz niczego nie zmienia w działaniu programu. Może stać w osobnej linii albo za instrukcją. ```python # rozlicz.py - rozliczenie wspólnych wydatków print("Wspólna Kasa") #

[ref-9] fraza: „języku, którego użyjemy w tym tutorialu” (w przód, Python jako język tutorialu)
  zdanie: Oto jedna instrukcja w Pythonie, języku, którego użyjemy w tym tutorialu:
  cel: [Czym jest kod źródłowy] Kod źródłowy to tekst programu zapisany w języku programowania, który czyta i pisze człowiek. To „źródło”, z którego komputer dopiero dostaje coś do wykonania. Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to instrukcja zapisana według ścisłych reguł składni. Ten sam algorytm, który wcześniej opisywaliśmy słowami i schematem, tu dost

[ref-10] fraza: „Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”” (w przód, Python i budowa programu „Wspólna Kasa” omówione później)
  zdanie: Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”.
  cel: [Czym jest funkcja] Funkcja to nazwany kawałek kodu, który raz opisujesz, a potem uruchamiasz, kiedy zechcesz, wpisując jego nazwę. Znasz już gotowe funkcje: `print()` i `str()` napisali twórcy Pythona. Własną funkcję zaczynasz od `def`, nazwy, nawiasów i dwukropka. Wcięty blok pod spodem to jej treść. Ten zapis to definicja funkcji: tylko opisuje, co funkcja robi, i niczego jeszcze nie wykonuje. Dopiero wywołanie, czyli nazwa z nawiasami, uruchamia treść. W

[ref-11] fraza: „Wróćmy do czworga znajomych na wyjeździe” (wstecz, przykład znajomych płacących na wyjeździe z działu 01)
  zdanie: Wróćmy do czworga znajomych na wyjeździe. Polecenie „podziel rachunek po równo” dla nich jest jasne. Dla komputera brakuje w nim niemal wszystkiego:
  cel: [Czym jest program komputerowy] Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

[ref-12] fraza: „„Wspólna Kasa”, przykład, który będzie nam towarzyszył” (wstecz, przykład Wspólnej Kasy wprowadzony w dziale 01 (wyjazd czworga znajomych rozliczających wydatki))
  zdanie: „Wspólna Kasa”, przykład, który będzie nam towarzyszył, zacznie jako mały program: wczyta wydatki i wypisze, kto komu ile jest winien. Nie będzie miała okna ani przycisków. Dopiero dobudowana oprawa (pytania do użytkownika, sprawdzanie danych) przybliży ją do aplikacji.
  cel: [Czym jest program komputerowy] Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

[ref-13] fraza: „pytania do użytkownika” (w przód, zapowiedź dobudowania pytań do użytkownika jako oprawy programu)
  zdanie: „Wspólna Kasa”, przykład, który będzie nam towarzyszył, zacznie jako mały program: wczyta wydatki i wypisze, kto komu ile jest winien. Nie będzie miała okna ani przycisków. Dopiero dobudowana oprawa (pytania do użytkownika, sprawdzanie danych) przybliży ją do aplikacji.
  cel: [Pytanie użytkownika o informację] Pokażemy to na przykładzie, który będzie nam towarzyszył: „Wspólnej Kasie”, czyli programie do rozliczania wspólnych wydatków znajomych. Zaczynamy dobudowywać do niego pytania do użytkownika, a pierwsze dotyczy nowego wydatku:

[ref-14] fraza: „sprawdzanie danych” (w przód, zapowiedź dobudowania sprawdzania danych wpisanych przez użytkownika)
  zdanie: „Wspólna Kasa”, przykład, który będzie nam towarzyszył, zacznie jako mały program: wczyta wydatki i wypisze, kto komu ile jest winien. Nie będzie miała okna ani przycisków. Dopiero dobudowana oprawa (pytania do użytkownika, sprawdzanie danych) przybliży ją do aplikacji.
  cel: [Po co sprawdzać dane użytkownika] Ta kontrola to walidacja: sprawdzenie, czy wpisana wartość nadaje się do dalszej pracy, zanim program jej użyje. Pamiętasz, że input zawsze zwraca tekst. Gdy ktoś na pytanie „Ile zapłacił?” wpisze `abc`, samo `float("abc")` przerwie program komunikatem o błędzie. A gdy wpisze `-5`, program nie zgłosi żadnego błędu i po cichu policzy złe saldo.
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-1",
      "keep": true,
      "reason": "Cel definiuje programistę dokładnie tak, jak fraza."
    },
    {
      "id": "ref-2",
      "keep": false,
      "reason": "Fraza to zapowiedź ramowa; cel to ogólna definicja programu, a nie przykład."
    },
    {
      "id": "ref-3",
      "keep": false,
      "reason": "Zapowiedź ramowa, a cel to tylko powtórzenie tego samego zdania."
    },
    {
      "id": "ref-5",
      "keep": true,
      "reason": "Cel wyjaśnia, czym jest język programowania."
    },
    {
      "id": "ref-6",
      "keep": true,
      "reason": "Cel to opis przykładu ze znajomymi, do którego odsyła fraza."
    },
    {
      "id": "ref-8",
      "keep": false,
      "reason": "Cel (komentarze) nie ma związku z frazą; link przypadkowy."
    },
    {
      "id": "ref-9",
      "keep": false,
      "reason": "Cel to kod źródłowy, a fraza obiecuje informację o Pythonie."
    },
    {
      "id": "ref-10",
      "keep": false,
      "reason": "Cel (funkcje) nie mówi o Pythonie ani o budowie Wspólnej Kasy."
    },
    {
      "id": "ref-11",
      "keep": true,
      "reason": "Czytelnik może wrócić do opisu przykładu ze znajomymi na wyjeździe."
    },
    {
      "id": "ref-12",
      "keep": true,
      "reason": "Cel to wprowadzenie przykładu Wspólnej Kasy, o który pyta fraza."
    },
    {
      "id": "ref-13",
      "keep": true,
      "reason": "Cel pokazuje dobudowywanie pytań do użytkownika."
    },
    {
      "id": "ref-14",
      "keep": true,
      "reason": "Cel wyjaśnia walidację, czyli sprawdzanie danych."
    }
  ]
}
````
