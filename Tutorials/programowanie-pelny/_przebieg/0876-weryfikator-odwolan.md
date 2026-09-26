# Krok 0876 · weryfikator_odwołań

Węzeł: `review` · dział: 8 · pytanie: 45 · próba: 1

## Prompt

````text
Jesteś weryfikatorem odwołań w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.

Znajdź w nowej sekcji WSZYSTKIE odwołania, także te, których autor nie zadeklarował:
- nawiązania do czegoś wcześniejszego („jak widzieliśmy”, „ten błąd z napiwkiem”, „wspomniany wcześniej”),
- obietnice czegoś późniejszego („powiemy osobno”, „wrócimy do tego”, „w dziale o pętlach”).
Zwykłe użycie pojęcia (np. „programu”, „listy”) NIE jest odwołaniem; nawiązanie odsyła do konkretnego miejsca albo zdarzenia,
a obietnica zapowiada, że temat wróci.

Dla każdego podaj w references: direction, phrase (dokładny fragment zdania z sekcji), about, target i quote:
- wstecz: target = id punktu zaczepienia (lm-N), a gdy żaden nie pasuje: id sekcji z listy niżej albo "glosariusz:<id>";
  quote puste (cytat punktu zaczepienia jest znany).
- w przód: target = numer późniejszego pytania, jeśli któreś wyraźnie to omówi, inaczej puste; quote puste.
- poza tutorialem: target i quote puste.
Wolno nawiązywać tylko do punktów i sekcji z list (ten i poprzedni dział) albo do haseł glosariusza. Nawiązanie, którego cel
nie istnieje albo mówi co innego, zgłoś jako potrzebę kind="odwołanie", severity="blokująca", detail = jak poprawić
(wyjaśnić na miejscu albo usunąć). Obietnicę, która odwołuje się do „pytań”, numerów albo list wewnętrznych,
zgłoś jako blokującą: czytelnik ich nie zna, zdanie ma mówić o temacie.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

ZADEKLAROWANE PRZEZ AUTORA:
- wstecz: „o których mówiliśmy przy zwracaniu wyniku” → lm-49 (print tylko pokazuje, nie zwraca)
- w przód: „Do plików wrócimy osobno” → 47 (pliki jako miejsce zapisu wyników)
- w przód: „opiszemy przy interfejsie” → 48 (interfejs użytkownika)

HASŁA GLOSARIUSZA (id: termin):
- program-komputerowy: program komputerowy
- instrukcja: instrukcja
- programista: programista
- programowanie: programowanie
- jezyk-programowania: język programowania
- kod: kod
- skladnia: składnia
- aplikacja: aplikacja
- algorytm: algorytm
- warunek-zakonczenia: warunek zakończenia
- schemat-blokowy: schemat blokowy
- funkcja: funkcja
- specyfikacja-wyniku: specyfikacja wyniku
- przypadek-brzegowy: przypadek brzegowy
- kod-zrodlowy: kod źródłowy
- edytor-kodu: edytor kodu
- podswietlanie-skladni: podświetlanie składni
- python: Python
- terminal: terminal
- kompilator: kompilator
- interpreter: interpreter
- blad-w-programie: błąd w programie
- print: print
- komentarz: komentarz
- dana: dana
- zmienna: zmienna
- wartosc-zmiennej: wartość zmiennej
- typ-danych: typ danych
- wartosc-logiczna: wartość logiczna
- przypisanie: przypisanie
- operator-arytmetyczny: operator arytmetyczny
- konkatenacja: konkatenacja
- operator-porownania: operator porównania
- instrukcja-warunkowa: instrukcja warunkowa
- wciecie: wcięcie
- operator-logiczny: operator logiczny
- petla: pętla
- iteracja: iteracja
- petla-nieskonczona: pętla nieskończona
- lista-danych: lista danych
- element-listy: element listy
- indeks: indeks
- definicja-funkcji: definicja funkcji
- wywolanie-funkcji: wywołanie funkcji
- argument-funkcji: argument funkcji
- parametr: parametr
- typeerror: TypeError
- none: None
- wartosc-zwracana: wartość zwracana
- dane-wejsciowe: dane wejściowe

PÓŹNIEJSZE PYTANIA:
- 46. Jak program może zapytać użytkownika o informację?
- 47. Czym jest plik i jak program może z niego korzystać?
- 48. Czym jest interfejs użytkownika?
- 49. Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?
- 50. Czym różni się błąd składni od błędu logicznego?
- 51. Jak przeczytać komunikat o błędzie?
- 52. Czym jest testowanie programu?
- 53. Czym jest debugowanie?
- 54. Dlaczego warto zapisywać kolejne wersje kodu?
- 55. Jak szukać rozwiązań problemów programistycznych w internecie?
- 56. Jakie są przykłady programów używanych na co dzień?
- 57. Czym różni się strona internetowa od aplikacji mobilnej?
- 58. Jak od pomysłu dojść do działającego programu?
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
- 60. Od czego zacząć samodzielną naukę programowania?
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

PUNKTY ZACZEPIENIA (ten i poprzedni dział):
- [lm-45] suma jako funkcja (dział 07): „Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy”
- [lm-46] dwa wyjazdy, jedna logika (dział 07): „Ta sama logika obsłużyła dwa wyjazdy, choć zapisaliśmy ją raz.”
- [lm-47] argumenty po nazwie (dział 07): „Drugie podaje je z nazwą, więc kolejność nie gra roli”
- [lm-48] zamieniona kolejność (dział 07): „da wynik bez błędu, ale zły, bo 4 zł podzielisz na 300 osób”
- [lm-49] wypisanie kontra zwrócenie (dział 07): „Zmienna `nic` trzyma tylko `None`, bo ta funkcja niczego nie zwróciła.”
- [lm-50] zdanie w kodzie (dział 07): „Ostatnią linię czyta się prawie jak zdanie.”
- [lm-51] dwa wyjazdy, ta sama funkcja (dział 07): „Logika liczenia leży w jednym miejscu, więc nie kopiujesz pętli dla każdego wyjazdu.”
- [lm-52] kod stały, dane zmienne (dział 08): „kod zostaje ten sam, a dane przychodzą przy każdym uruchomieniu inne”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-07-czym-jest-funkcja] Czym jest funkcja (dział 07): Funkcję definiujesz raz przez def, a uruchamiasz każdym wywołaniem jej nazwy z nawiasami.
- [sec-07-po-co-dzielic-program-na-funkcje] Po co dzielić program na funkcje (dział 07): Funkcje dają kodowi nazwy i jedno miejsce na każdą logikę, więc program jest czytelniejszy, a poprawki robisz raz.
- [sec-07-czym-sa-argumenty-funkcji] Czym są argumenty funkcji (dział 07): Argumenty to wartości podane przy wywołaniu, które trafiają do parametrów funkcji według kolejności lub nazwy, a ich liczba musi pasować do definicji.
- [sec-07-zwracanie-wyniku-przez-funkcje] Zwracanie wyniku przez funkcję (dział 07): Return oddaje wartość wywołującemu, po czym kończy funkcję, a print tylko pokazuje tekst i niczego nie zwraca (funkcja bez return daje None).
- [sec-07-czytelne-nazwy-zmiennych-i-funkcji] Czytelne nazwy zmiennych i funkcji (dział 07): Nazywaj funkcję według tego, co robi, a zmienną według tego, co trzyma, bo kod czyta się częściej, niż pisze.
- [sec-07-ponowne-uzycie-kodu] Ponowne użycie kodu (dział 07): Funkcję piszesz raz, a wywołujesz z różnymi danymi, więc poprawka w jednym miejscu naprawia wszystkie użycia.
- [sec-08-dane-wejsciowe-programu] Dane wejściowe programu (dział 08): Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.

NOWA SEKCJA "Dane wyjściowe programu":
[[dane-wyjsciowe|Dane wyjściowe]] to wszystko, co program oddaje na zewnątrz: wynik obliczeń, komunikat, zapisany plik. To druga strona [[dane-wejsciowe|danych wejściowych]]: wejście wpuszcza informacje do programu, wyjście je z niego wypuszcza.

Bez wyjścia program mógłby liczyć, ale nikt by o tym nie wiedział. Wynik zamknięty w zmiennej znika, gdy program się kończy.

Wyjście ma kilka adresatów:

| Dokąd trafia wynik | Przykład we „Wspólnej Kasie” |
|---|---|
| ekran | komunikat „Na osobę wychodzi 26.0” |
| plik | zapisane rozliczenie wyjazdu |
| inny program | dane przekazane do aplikacji banku |

Na razie znasz tylko pierwszą drogę: `print` pokazuje wartość w terminalu. Robiłeś to już w funkcji `wypisz_na_osobe`, o której mówiliśmy przy zwracaniu wyniku (przypomnienie: `print` tylko pokazuje tekst, niczego nie zwraca).

```python
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wypisz_na_osobe(78, 3)
```

```text
26.0
```

Konsekwencja: o tym, co program wypisze, decydujesz Ty. Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. Do plików wrócimy osobno, a wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "o której mówiliśmy przy zwracaniu wyniku",
      "about": "print tylko pokazuje, nie zwraca",
      "target": "lm-49"
    },
    {
      "direction": "w przód",
      "phrase": "Do plików wrócimy osobno",
      "about": "pliki jako miejsce zapisu wyników",
      "target": "47"
    },
    {
      "direction": "w przód",
      "phrase": "opiszemy przy interfejsie",
      "about": "interfejs użytkownika, rozmowa z użytkownikiem",
      "target": "48"
    }
  ],
  "needs": [
    {
      "kind": "przykład",
      "severity": "sugestia",
      "target": "dobre wyjście ma opis i jednostkę",
      "detail": "Teza o opisie i jednostce nie ma przykładu w kodzie. Dodaj wersję z opisem, np. print(\"Na osobę wychodzi\", suma / osoby, \"zł\"), wraz z wynikiem, żeby czytelnik zobaczył różnicę względem „26.0”.",
      "source": "sekcja"
    },
    {
      "kind": "spójność",
      "severity": "sugestia",
      "target": "tabela i kod",
      "detail": "Tabela podaje komunikat „Na osobę wychodzi 26.0”, a kod wypisuje samo „26.0”. Ujednolić albo zaznaczyć, że tabela pokazuje wersję docelową.",
      "source": "sekcja"
    }
  ]
}
````
