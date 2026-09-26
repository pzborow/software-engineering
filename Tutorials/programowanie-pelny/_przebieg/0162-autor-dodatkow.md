# Krok 0162 · autor_dodatków

Węzeł: `layers` · dział: 2 · pytanie: 11 · próba: —

## Prompt

````text
Dodajesz opcjonalne dodatki do sekcji tutorialu: Programowanie od podstaw.
Czytelnik: osoba spoza IT, poziom: początkujący.

Dodatki nie są potrzebne do zrozumienia sekcji; są dla przyjemności i pamięci. Każdy moduł ma cel: około tylu wpisów na dział, ile wynosi jego limit, rozłożonych na sekcje. Dodaj wpis, gdy ta sekcja daje dobrą okazję; kod pilnuje odstępów i limitów, weryfikator jakości. Nie wymyślaj na siłę: słaby dodatek zostanie odrzucony.
Każdy dodatek musi wynikać z treści TEJ sekcji i być poprawny: logicznie spójny, zgodny z faktami.
Nazwy z kodu pisz w backtickach.

Włączone moduły:
- module="dowcipy" (Z przymrużeniem oka): krótki żart, gra słów albo zabawna puenta o pojęciu z tej sekcji, najlepiej pomagająca je zapamiętać; 1-2 zdania. Ton dopasuj do czytelnika. Bez żartów z ludzi i grup. (w tej sekcji NIE dodawaj: za blisko dowcipy „Rondo bez zjazdu” w sekcji „Czym jest schemat blokowy” (odstęp 1, wymagany 2)).
- module="dygresje" (Na marginesie): ciekawostka, historia albo „a gdyby…” związane z sekcją; 2-4 zdania. Tylko gdy wnosi coś spoza głównego toku i nie jest potrzebna do zrozumienia sekcji. (w dziale jest już 1 z 2, zostało sekcji: 1). Podaj w sources wiarygodne źródło (encyklopedia, publikacja, oficjalna strona) z adresem; bez źródła nie dodawaj.
- module="dykteryjki" (Z życia wzięte): krótka historia z pracy opowiedziana w pierwszej osobie przez narratora z ustawień: realistyczna sytuacja, w której pojęcie z tej sekcji miało znaczenie, jaki był skutek i czego nauczyła; 3-5 zdań. To ilustracja typowej sytuacji, nie reportaż: bez nazw firm, ludzi i dat. (w dziale jest już 1 z 2, zostało sekcji: 1). Ustawienia: narrator: doświadczony Python developer, kilkanaście lat w projektach backendowych i automatyzacji; ton: poważny, rzeczowy, bez żartów.
- module="rysunki" (Ilustracja): pomysł na zabawny, prosty rysunek oparty na metaforze z tej sekcji. body: prompt dla generatora obrazów (scena, postacie, co ma być widać, bez tekstu na obrazku); caption: podpis pod rysunkiem; alt: opis dla osób niewidzących. Styl rysunku jest wspólny dla tutorialu. (w tym dziale limit jest wyczerpany: nie dodawaj). Ustawienia: styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.. W body opisz tylko scenę; styl dopisuje renderer.
- module="wtręty" (Wtręt): krótki wtręt (2-4 zdania), który demonstruje pojęcie z tej sekcji humorystycznie albo kontrprzykładem: co się stanie, gdy zrobić odwrotnie albo źle. Może nawiązywać do wcześniejszych wtrętów (ta sama postać, rozwinięcie sytuacji), żeby czytelnik czuł ciągłość; nie kopiuj ich. (w dziale jest już 1 z 2, zostało sekcji: 1). Ustawienia: bohater: Marta, 34-letnia specjalistka ds. kadr, która w arkuszu kalkulacyjnym radzi sobie świetnie, ale kodu nigdy nie pisała. Co miesiąc rozlicza wspólne wydatki z współlokatorami (czynsz, zakupy, wyjazdy) i chce zastąpić ręczne formuły programem, który policzy podział z napiwkiem i rabatem oraz zapisze wynik do pliku; kłopoty jej sprawiają błędy w składni, niezrozumiałe komunikaty i obawa, że zepsuje coś w komputerze..

Wcześniejsze wpisy, które widzi moduł "dowcipy" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dowcipy] Gramatyka bez taryfy ulgowej: W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyk
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
  - [wtręty] Marta odejmuje udział, zanim go policzy: Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wyno
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [dowcipy] Rondo bez zjazdu: Schemat blokowy bez strzałki „nie” wychodzącej z ostatniego rombu przypomina rondo bez zjazdów: wszystko jest poprawnie narysowane, tylko nikt stamtąd nie wyjed
Wcześniejsze wpisy, które widzi moduł "dygresje" (nie powtarzaj ich tematów, puent ani motywów):
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
Wcześniejsze wpisy, które widzi moduł "dykteryjki" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [wtręty] Marta odejmuje udział, zanim go policzy: Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wyno
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
Wcześniejsze wpisy, które widzi moduł "rysunki" (nie powtarzaj ich tematów, puent ani motywów):
  - [rysunki] Pętla poprawek przy stole: Przy drewnianym stole siedzi uśmiechnięta kobieta z ołówkiem i gumką. Przed nią kartka z ręcznie narysowanymi kółkami połączonymi strzałkami, które tworzą zamkn
  - [rysunki] Przepis dla kogoś, kto nigdy nie gotował: Jasna kuchnia. Początkujący kucharz w fartuchu stoi przy piekarniku z otwartymi drzwiczkami i ostrożnie wbija cienki termometr w złocisty placek na blasze. Na b
Wcześniejsze wpisy, które widzi moduł "wtręty" (możesz do nich nawiązać, rozwijając postać albo sytuację; nie kopiuj):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dowcipy] Gramatyka bez taryfy ulgowej: W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyk
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
  - [wtręty] Marta odejmuje udział, zanim go policzy: Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wyno
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [dowcipy] Rondo bez zjazdu: Schemat blokowy bez strzałki „nie” wychodzącej z ostatniego rombu przypomina rondo bez zjazdów: wszystko jest poprawnie narysowane, tylko nikt stamtąd nie wyjed

W jednej sekcji najwyżej 2 dodatki łącznie; nie łącz w jednej sekcji modułów, które się nie lubią.
Dla każdego dodatku: module, title (maks. 8 słów), body; dla ilustracji także caption i alt.

SEKCJA "Podział problemu na części" (dział 02. Algorytmy i myślenie krokowe):
Duży problem dzielisz tak, by każda część miała własne dane wejściowe, jedno zadanie i wynik, który da się sprawdzić osobno. Zaczynasz od całego zadania, a potem pytasz: z jakich mniejszych kroków się składa?

Weźmy „rozlicz wyjazd”. To za dużo naraz, więc rozbijamy to na trzy części. Wracamy tu do [[schemat-blokowy|schematu blokowego]] z poprzedniej sekcji: kroki w jego ramkach to gotowe kandydatki na części.

```text
Rozlicz wyjazd
  |-- 1. Zsumuj wydatki          (wydatki -> suma)
  |-- 2. Policz udział osoby     (suma, liczba osób -> udział)
  `-- 3. Porównaj wpłatę z udziałem
                                 (wpłata, udział -> saldo)
```

Każda część ma jasne wejście i wynik. Część 3 potrzebuje wyniku części 2, a ta wyniku części 1, więc kolejność wynika z tych zależności, tak jak w sekcji o kolejności kroków.

Jeśli część nadal jest zbyt duża, dziel ją dalej, aż każdą da się opisać jednym zdaniem. Dobra część daje się też przetestować samodzielnie: znasz jej dane i wiesz, jaki wynik ma wyjść.

Konsekwencja: w programie takie części zamienimy w osobne [[funkcja|funkcje]], czyli nazwane fragmenty kodu do wielokrotnego użycia. Ich nazwy, np. `suma_wydatkow`, poznasz później, gdy zaczniemy pisać „Wspólną Kasę”, przykład, który będzie nam towarzyszył w kolejnych działach.
````

## Odpowiedź

````json
{
  "items": [
    {
      "module": "wtręty",
      "title": "Marta zleca całe rozliczenie jednym zdaniem",
      "body": "Marta wpisała jedną instrukcję: „rozlicz wyjazd”. Kiedy wynik się nie zgadzał, nie umiała powiedzieć, czy zawiodła suma, udział, czy porównanie z wpłatą, bo wszystko siedziało w jednym kawałku. Dopiero podział na trzy części, każda z własnym wynikiem do sprawdzenia, pozwolił jej zajrzeć do sumy i zauważyć, że jeden rachunek został policzony dwa razy."
    },
    {
      "module": "dykteryjki",
      "title": "Funkcja, która robiła wszystko naraz",
      "body": "Odziedziczyłem skrypt do miesięcznych rozliczeń, w którym jedna funkcja wczytywała dane, liczyła kwoty i formatowała raport. Wynik był czasem błędny, ale nie dało się ustalić, na którym etapie. Rozbiłem ją na trzy części, każdą z jasnym wejściem i wynikiem, i dla każdej sprawdziłem osobno kilka przykładów z ręcznie policzonym rezultatem. Błąd okazał się w wczytywaniu, gdzie pomijany był ostatni wiersz. Od tego czasu dzielę zadanie, zanim zacznę pisać kod, bo część, którą da się sprawdzić osobno, skraca szukanie błędu z godzin do minut."
    }
  ]
}
````
