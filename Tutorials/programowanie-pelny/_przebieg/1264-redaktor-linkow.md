# Krok 1264 · redaktor_linków

Węzeł: `review_links` · dział: 3 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 03 „Kod i jego uruchamianie” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-33] fraza: „Ten sam algorytm, który wcześniej opisywaliśmy słowami i schematem” (wstecz, algorytm rozliczenia opisany wcześniej słowami i schematem blokowym)
  zdanie: Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to instrukcja zapisana według ścisłych reguł składni. Ten sam algorytm, który wcześniej opisywaliśmy słowami i schematem, tu dostaje zapis, którego nie da się zrozumieć na dwa sposoby.
  cel: [Czym jest algorytm] ```text dane: lista wydatków (kto, ile) i liczba osób 1. Zsumuj wszystkie wydatki. 2. Podziel sumę przez liczbę osób: to udział jednej osoby. 3. Dla każdej osoby odejmij udział od tego, ile wydała. 4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna. wynik: saldo każdej osoby ```

[ref-34] fraza: „jak to działa, pokażemy przy uruchamianiu programu” (w przód, czytanie i wykonywanie pliku z kodem przez osobny program)
  zdanie: Plik sam niczego nie robi. Dopiero osobny program czyta go i wykonuje linia po linii, a jak to działa, pokażemy przy uruchamianiu programu.
  cel: [Kompilator i interpreter] Kompilator i interpreter to programy, które przekładają kod źródłowy na działanie komputera, bo procesor sam nie rozumie tekstu z pliku. Kompilator tłumaczy cały kod naraz na osobny, gotowy do uruchomienia plik. Interpreter czyta kod i wykonuje go na bieżąco, instrukcja po instrukcji. To ten wykonawca, o którym była mowa przy uruchamianiu programu. Gdy wpisujesz `python rozlicz.py`, Python działa jako interpreter: bierze plik i wykonuje

[ref-35] fraza: „nasz przykład, który będzie nam towarzyszył” (w przód, Wspólna Kasa jako przykład wracający w kolejnych działach)
  zdanie: Kod źródłowy zapisujemy w pliku o rozszerzeniu zależnym od języka. Pliki Pythona kończą się na `.py`. Taki plik będzie miał nasz przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Zaczyna się od pliku `rozlicz.py`:
  cel: [Do czego służą komentarze] ```python # rozlicz.py - rozliczenie wspólnych wydatków print("Wspólna Kasa") # udział na dwie osoby print(300 / 3) # 300 zł na troje osób # print(300 / 2) <- ta linia jest wyłączona ```

[ref-36] fraza: „Skoro kod jest zwykłym plikiem tekstowym” (wstecz, kod źródłowy jako zwykły plik tekstowy)
  zdanie: Skoro kod jest zwykłym plikiem tekstowym, można go napisać nawet w Notatniku. Edytor kodu dodaje jednak rzeczy, które przy programowaniu bardzo oszczędzają czas:
  cel: [Czym jest kod źródłowy] Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to instrukcja zapisana według ścisłych reguł składni. Ten sam algorytm, który wcześniej opisywaliśmy słowami i schematem, tu dostaje zapis, którego nie da się zrozumieć na dwa sposoby.

[ref-39] fraza: „To ten wykonawca, o którym była mowa przy uruchamianiu programu” (wstecz, wykonawca kodu zapowiedziany w sekcji o uruchamianiu programu)
  zdanie: To ten wykonawca, o którym była mowa przy uruchamianiu programu. Gdy wpisujesz `python rozlicz.py`, Python działa jako interpreter: bierze plik i wykonuje go od góry.
  cel: [Co znaczy uruchomić program] Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam kod źródłowy leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś nie zacznie go realizować. Plik z kodem czyta i wykonuje linia po linii inny program. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części. Polecenie wpisujemy w [[terminal

[ref-40] fraza: „Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie” (wstecz, codzienny cykl pracy: zapisz, uruchom, przeczytaj wynik)
  zdanie: Konsekwencja dla Wspólnej Kasy: nie ma osobnego kroku budowania. Zmieniasz `rozlicz.py`, zapisujesz i uruchamiasz ponownie. W praktyce Python najpierw przekłada plik na pośredni zapis, ale z Twojej strony to jedno polecenie.
  cel: [Co znaczy uruchomić program] Uruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. Tak wygląda codzienna praca: zapisz, uruchom, przeczytaj wynik.

[ref-42] fraza: „omówimy osobno, w dziale o poprawianiu programów” (w przód, rodzaje błędów i czytanie komunikatów)
  zdanie: Konsekwencja: błąd to normalna część pracy, nie porażka. Komunikat to podpowiedź, a brak komunikatu nie znaczy, że wynik jest dobry. Jak rozróżniać te rodzaje błędów i czytać komunikaty, omówimy osobno, w dziale o poprawianiu programów.
  cel: [Błąd składni a błąd logiczny] Błąd składni łamie zasady zapisu, więc Python zatrzymuje się, zanim cokolwiek wykona. Błąd logiczny ma zapis poprawny, ale robi coś innego, niż zamierzałeś, więc program działa i po cichu podaje zły wynik.

[ref-43] fraza: „U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej” (wstecz, plik czytelnika z literówką prnt zamiast print)
  zdanie: U siebie w pliku masz komentarz w pierwszej linii i literówkę `prnt` w drugiej. Komentarz nie przeszkadza w znalezieniu błędu: popraw literówkę i uruchom plik ponownie.
  cel: [Co to jest błąd w programie] Pierwszy rodzaj widać od razu. Python czyta plik od góry i gdy trafi na coś, czego nie rozumie, przerywa pracę i wypisuje komunikat. Tak jest, gdy literówka zmieni print (polecenie, które każe programowi wypisać tekst lub liczbę na ekranie) w `prnt`: interpreter nie zna takiego słowa. To jeszcze nie katastrofa, bo komunikat wskazuje linię i powód.
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-33",
      "keep": true,
      "reason": "Cel to algorytm rozliczenia opisany słowami; czytelnik może chcieć go zobaczyć obok zapisu w kodzie."
    },
    {
      "id": "ref-34",
      "keep": true,
      "reason": "Cel wyjaśnia, jak program czyta i wykonuje plik, zgodnie z frazą."
    },
    {
      "id": "ref-35",
      "keep": false,
      "reason": "Cel to fragment o komentarzach, a fraza obiecuje przykład towarzyszący dalej; to zapowiedź ramowa, cel nie pasuje."
    },
    {
      "id": "ref-36",
      "keep": true,
      "reason": "Cel mówi wprost, że kod to zwykły plik tekstowy."
    },
    {
      "id": "ref-39",
      "keep": true,
      "reason": "Cel to sekcja o uruchamianiu programu, do której odsyła fraza."
    },
    {
      "id": "ref-40",
      "keep": true,
      "reason": "Cel opisuje cykl zapisz-uruchom-przeczytaj wynik, o którym mówi fraza."
    },
    {
      "id": "ref-42",
      "keep": true,
      "reason": "Cel wyjaśnia rodzaje błędów, o których mowa we frazie."
    },
    {
      "id": "ref-43",
      "keep": true,
      "reason": "Cel pokazuje, jak literówka prnt daje błąd i komunikat, co pomaga zrozumieć sytuację czytelnika."
    }
  ]
}
````
