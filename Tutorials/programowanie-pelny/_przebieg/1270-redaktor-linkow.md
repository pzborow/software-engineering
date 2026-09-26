# Krok 1270 · redaktor_linków

Węzeł: `review_links` · dział: 9 · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem linków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom: początkujący.
Dział 09 „Błędy i dobre praktyki” ma linki z fraz do innych miejsc tutorialu. Dla każdego zdecyduj, czy zostaje (keep):
- zostaje, gdy czytelnik w tym miejscu może chcieć sprawdzić cel i po kliknięciu dostanie to, o czym mówi fraza;
- odpada, gdy fraza to ogólnik albo zapowiedź ramowa („na razie nie piszemy kodu”), cel jest przypadkowy albo
  nie mówi tego, co obiecuje fraza, albo link tylko rozprasza.
Nie usuwaj linku tylko dlatego, że cel jest blisko: to już sprawdzono. reason: krótko.

LINKI:
[ref-117] fraza: „Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu” (w przód, czytanie komunikatów o błędach i debugowanie)
  zdanie: Konsekwencja: błędy składni są uciążliwe, ale łatwe, bo wskaże je Python. Za błędy logiczne odpowiadasz Ty, więc wynik porównuj z rachunkiem na kartce. Czytanie komunikatów i szukanie takich błędów omówimy w kolejnych sekcjach tego działu.
  cel: [Czym jest debugowanie] Debugowanie to szukanie przyczyny błędu i jej usuwanie. Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach. Metoda jest prosta. Najpierw odtwarzasz błąd na jednych, konkretnych danych. Potem zawężasz miejsce: przed podejrzanym krokiem wypisujesz wartości i porównujesz je z tym, czego oczekujesz. Pierwsze miejsce, w którym wartość jest inna niż powinna, wskazuje przyczynę. Na końcu poprawiasz jedną rzecz i uruchamiasz ponownie. Weźmy [

[ref-118] fraza: „Inaczej niż przy błędzie składni ze „Startem”, który się nie pojawił” (wstecz, błąd składni zatrzymuje program przed startem, więc słowo „Start” się nie wypisało)
  zdanie: Inaczej niż przy błędzie składni ze „Startem”, który się nie pojawił, tu „Start” się wypisał, bo program ruszył i padł dopiero w środku.
  cel: [Błąd składni a błąd logiczny] Słowo „start” się nie pojawiło, a komunikat wskazuje linię i miejsce.

[ref-119] fraza: „Szukanie przyczyny krok po kroku omówimy przy debugowaniu” (w przód, debugowanie: szukanie przyczyny błędu krok po kroku)
  zdanie: Konsekwencja: nie bój się czerwonego tekstu. Przeczytaj ostatnią linię, znajdź w śladzie własny plik i numer linii, a zwykle już wiesz, gdzie szukać. Szukanie przyczyny krok po kroku omówimy przy debugowaniu.
  cel: [Czym jest debugowanie] Debugowanie to szukanie przyczyny błędu i jej usuwanie. Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach.

[ref-120] fraza: „jak przy błędzie z niewłaściwym dzielnikiem” (wstecz, zły dzielnik dający 39.0 zamiast 26.0)
  zdanie: Cisza po `assert` znaczy „zgadza się”. Gdyby ktoś zmienił dzielenie tak, że wynik byłby zły, jak przy błędzie z niewłaściwym dzielnikiem, pierwszy test zatrzymałby program i wskazał linię, w której oczekiwanie przestało być prawdą.
  cel: [Błąd składni a błąd logiczny] Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.

[ref-122] fraza: „błąd logiczny z wynikiem 39.0 zamiast 26.0” (wstecz, błąd z dzielnikiem 2 zamiast 3, wynik 39.0 zamiast 26.0)
  zdanie: Weźmy błąd logiczny z wynikiem 39.0 zamiast 26.0. Podejrzewamy dwa dane wejściowe dzielenia, więc je wypisujemy:
  cel: [Błąd składni a błąd logiczny] Nie ma komunikatu, a wynik jest zły: powinno być 26.0, bo osób jest trzy.

[ref-123] fraza: „test z poprzedniej sekcji” (wstecz, testowanie programu opisane w poprzedniej sekcji)
  zdanie: Gdy test z poprzedniej sekcji zgłosi błąd, zaczynasz tak samo: odtwarzasz przypadek, który go wywołał, i patrzysz na wartości. Po naprawie usuń linie z `DEBUG`, żeby nie zaśmiecały wyniku.
  cel: [Czym jest testowanie programu] Testowanie to systematyczne sprawdzanie programu na wielu danych, dla których z góry znasz poprawny wynik. Zamiast raz spojrzeć na ekran i uznać, że „wygląda dobrze”, zapisujesz oczekiwania i pozwalasz komputerowi je porównać. Najprostszy test to jedno sprawdzenie małej funkcji. W Pythonie służy do tego assert: instrukcja, która nic nie robi, gdy warunek jest prawdziwy, a zatrzymuje program błędem `AssertionError`, gdy jest fałszywy. ```python def na_osobe(suma, osoby

[ref-125] fraza: „jak w sekcji o czytaniu komunikatów, czytasz od dołu” (wstecz, czytanie komunikatu o błędzie od dołu)
  zdanie: Ostatnia linia Tracebacku to ta, którą, jak w sekcji o czytaniu komunikatów, czytasz od dołu. Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych, bo nikt inny ich nie ma.
  cel: [Jak czytać komunikat o błędzie] Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak, a linie nad nią pokazują, gdzie to się stało. Komunikat nie jest wyrokiem, tylko wskazówką.
````

## Odpowiedź

````json
{
  "items": [
    {
      "id": "ref-117",
      "keep": false,
      "reason": "Zapowiedź ramowa; cel jest ogólnym początkiem debugowania, a nie czytaniem komunikatów."
    },
    {
      "id": "ref-118",
      "keep": true,
      "reason": "Czytelnik może chcieć porównać z przykładem błędu składni, gdzie „Start” się nie pojawił."
    },
    {
      "id": "ref-119",
      "keep": false,
      "reason": "Zapowiedź ramowa „omówimy przy debugowaniu”; link tylko rozprasza."
    },
    {
      "id": "ref-120",
      "keep": true,
      "reason": "Przywołuje konkretny przykład ze złym dzielnikiem; cel go pokazuje (26.0)."
    },
    {
      "id": "ref-122",
      "keep": true,
      "reason": "Fraza wskazuje konkretny przykład 39.0 zamiast 26.0, a cel go zawiera."
    },
    {
      "id": "ref-123",
      "keep": true,
      "reason": "Cel opisuje test z assert, do którego odnosi się fraza."
    },
    {
      "id": "ref-125",
      "keep": true,
      "reason": "Cel mówi dokładnie: czytaj komunikat od dołu."
    }
  ]
}
````
