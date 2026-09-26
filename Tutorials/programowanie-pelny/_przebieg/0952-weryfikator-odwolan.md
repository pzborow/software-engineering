# Krok 0952 · weryfikator_odwołań

Węzeł: `review` · dział: 8 · pytanie: 49 · próba: 1

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
- wstecz: „zawsze zwraca tekst” → lm-54 (input zwraca tekst)

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
- dane-wyjsciowe: dane wyjściowe
- input: input
- plik: plik
- tryb-otwarcia-pliku: tryb otwarcia pliku
- interfejs-uzytkownika: interfejs użytkownika
- interfejs-tekstowy: interfejs tekstowy

PÓŹNIEJSZE PYTANIA:
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
- [lm-53] wynik bez opisu (dział 08): „Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu”
- [lm-54] input zwraca tekst (dział 08): „`input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`.”
- [lm-55] tryb w kasuje (dział 08): „Pułapką jest tryb `"w"`, który kasuje starą zawartość.”
- [lm-56] plik zostaje (dział 08): „Zmienne żyją tylko podczas pracy programu i znikają wraz z jego zakończeniem, a plik zostaje.”
- [lm-57] interfejs to jedyne, co widzi użytkownik (dział 08): „Użytkownik nie widzi kodu, widzi tylko interfejs.”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-07-czym-jest-funkcja] Czym jest funkcja (dział 07): Funkcję definiujesz raz przez def, a uruchamiasz każdym wywołaniem jej nazwy z nawiasami.
- [sec-07-po-co-dzielic-program-na-funkcje] Po co dzielić program na funkcje (dział 07): Funkcje dają kodowi nazwy i jedno miejsce na każdą logikę, więc program jest czytelniejszy, a poprawki robisz raz.
- [sec-07-czym-sa-argumenty-funkcji] Czym są argumenty funkcji (dział 07): Argumenty to wartości podane przy wywołaniu, które trafiają do parametrów funkcji według kolejności lub nazwy, a ich liczba musi pasować do definicji.
- [sec-07-zwracanie-wyniku-przez-funkcje] Zwracanie wyniku przez funkcję (dział 07): Return oddaje wartość wywołującemu, po czym kończy funkcję, a print tylko pokazuje tekst i niczego nie zwraca (funkcja bez return daje None).
- [sec-07-czytelne-nazwy-zmiennych-i-funkcji] Czytelne nazwy zmiennych i funkcji (dział 07): Nazywaj funkcję według tego, co robi, a zmienną według tego, co trzyma, bo kod czyta się częściej, niż pisze.
- [sec-07-ponowne-uzycie-kodu] Ponowne użycie kodu (dział 07): Funkcję piszesz raz, a wywołujesz z różnymi danymi, więc poprawka w jednym miejscu naprawia wszystkie użycia.
- [sec-08-dane-wejsciowe-programu] Dane wejściowe programu (dział 08): Dane wejściowe to wartości przychodzące do programu z zewnątrz (od użytkownika, z pliku, z innego programu), dzięki czemu kod zostaje ten sam, a dane się zmieniają.
- [sec-08-dane-wyjsciowe-programu] Dane wyjściowe programu (dział 08): Dane wyjściowe to wynik, który program oddaje na zewnątrz (ekran, plik, inny program), a dobre wyjście jest opisane tak, by zrozumiał je człowiek.
- [sec-08-pytanie-uzytkownika-o-informacje] Pytanie użytkownika o informację (dział 08): Funkcja input wypisuje pytanie i zwraca odpowiedź użytkownika zawsze jako tekst, więc liczbę trzeba zamienić przez float().
- [sec-08-czym-jest-plik] Czym jest plik (dział 08): Plik przechowuje dane na dysku po zakończeniu programu, a program otwiera go przez open (najlepiej z with) w trybie czytania, zapisu lub dopisywania i pamięta, że dostaje z niego tekst.
- [sec-08-czym-jest-interfejs-uzytkownika] Czym jest interfejs użytkownika (dział 08): Interfejs użytkownika to wszystko, przez co człowiek rozmawia z programem: pytania, które program zadaje, i wyniki, które pokazuje, więc powinny być jasne dla kogoś, kto nie zna kodu.

NOWA SEKCJA "Po co sprawdzać dane użytkownika":
Program powinien sprawdzać dane od użytkownika, bo człowiek potrafi wpisać coś, czego kod się nie spodziewał, a wtedy program albo się zatrzyma, albo policzy coś błędnego.

Ta kontrola to [[walidacja-danych|walidacja]]: sprawdzenie, czy wpisana wartość nadaje się do dalszej pracy, zanim program jej użyje. Pamiętasz, że [[input|input]] zawsze zwraca tekst. Gdy ktoś na pytanie „Ile zapłacił?” wpisze `abc`, samo `float("abc")` przerwie program komunikatem o błędzie. A gdy wpisze `-5`, program nie zgłosi żadnego błędu i po cichu policzy złe saldo.

Dlatego sprawdzamy dane w miejscu, gdzie wchodzą do programu. Pokazuje to funkcja `sprawdz_kwote`, która odpowiada `True` albo `False`:

```python
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

for tekst in ["45.5", "abc", "-5", "0", ""]:
    print(repr(tekst), sprawdz_kwote(tekst))
```

```text
'45.5' True
'abc' False
'-5' False
'0' False
'' False
```

Pierwsza linia sprawdza, czy tekst składa się z cyfr (z najwyżej jedną kropką). Druga dopiero wtedy zamienia go na liczbę i pyta, czy jest dodatnia.

Konsekwencja: zły wpis nie kończy programu, tylko dostaje komunikat i kolejną szansę. Program, który sprawdza dane, jest odporny na pomyłki, a Ty masz pewność, że reszta kodu dostaje wartości, na które jest przygotowana.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "zawsze zwraca tekst",
      "about": "input zawsze zwraca tekst, nawet gdy ktoś wpisze liczbę",
      "target": "lm-54",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "przykład",
      "detail": "Końcowa teza, że zły wpis dostaje komunikat i kolejną szansę, nie ma pokazu w kodzie. Warto dodać krótką pętlę while z input, która pyta ponownie, aż sprawdz_kwote zwróci True.",
      "severity": "sugestia",
      "target": "Konsekwencja: zły wpis nie kończy programu"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "„Pierwsza linia” i „Druga” to w kodzie pierwszy i drugi warunek w funkcji, bo pierwsza linia to def. Lepiej napisać „pierwszy warunek” i „drugi”. Warto też jednym zdaniem wyjaśnić repr, które pokazuje apostrofy wokół tekstu i odróżnia pusty tekst od braku wypisu.",
      "severity": "sugestia",
      "target": "Pierwsza linia sprawdza"
    }
  ]
}
````
