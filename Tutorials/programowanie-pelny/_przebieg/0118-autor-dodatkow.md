# Krok 0118 · autor_dodatków

Węzeł: `layers` · dział: 2 · pytanie: 8 · próba: —

## Prompt

````text
Dodajesz opcjonalne dodatki do sekcji tutorialu: Programowanie od podstaw.
Czytelnik: osoba spoza IT, poziom: początkujący.

Dodatki nie są potrzebne do zrozumienia sekcji; są dla przyjemności i pamięci. Każdy moduł ma cel: około tylu wpisów na dział, ile wynosi jego limit, rozłożonych na sekcje. Dodaj wpis, gdy ta sekcja daje dobrą okazję; kod pilnuje odstępów i limitów, weryfikator jakości. Nie wymyślaj na siłę: słaby dodatek zostanie odrzucony.
Każdy dodatek musi wynikać z treści TEJ sekcji i być poprawny: logicznie spójny, zgodny z faktami.
Nazwy z kodu pisz w backtickach.

Włączone moduły:
- module="dowcipy" (Z przymrużeniem oka): krótki żart, gra słów albo zabawna puenta o pojęciu z tej sekcji, najlepiej pomagająca je zapamiętać; 1-2 zdania. Ton dopasuj do czytelnika. Bez żartów z ludzi i grup. (w dziale jest już 0 z 2, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji).
- module="dygresje" (Na marginesie): ciekawostka, historia albo „a gdyby…” związane z sekcją; 2-4 zdania. Tylko gdy wnosi coś spoza głównego toku i nie jest potrzebna do zrozumienia sekcji. (w tej sekcji NIE dodawaj: za blisko dygresje „Skąd wzięło się słowo „algorytm”” w sekcji „Czym jest algorytm” (odstęp 1, wymagany 2)). Podaj w sources wiarygodne źródło (encyklopedia, publikacja, oficjalna strona) z adresem; bez źródła nie dodawaj.
- module="dykteryjki" (Z życia wzięte): krótka historia z pracy opowiedziana w pierwszej osobie przez narratora z ustawień: realistyczna sytuacja, w której pojęcie z tej sekcji miało znaczenie, jaki był skutek i czego nauczyła; 3-5 zdań. To ilustracja typowej sytuacji, nie reportaż: bez nazw firm, ludzi i dat. (w tej sekcji NIE dodawaj: za blisko dygresje „Skąd wzięło się słowo „algorytm”” w sekcji „Czym jest algorytm” (odstęp 1, wymagany 2)). Ustawienia: narrator: doświadczony Python developer, kilkanaście lat w projektach backendowych i automatyzacji; ton: poważny, rzeczowy, bez żartów.
- module="rysunki" (Ilustracja): pomysł na zabawny, prosty rysunek oparty na metaforze z tej sekcji. body: prompt dla generatora obrazów (scena, postacie, co ma być widać, bez tekstu na obrazku); caption: podpis pod rysunkiem; alt: opis dla osób niewidzących. Styl rysunku jest wspólny dla tutorialu. (w dziale jest już 0 z 1, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji). Ustawienia: styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.. W body opisz tylko scenę; styl dopisuje renderer.
- module="wtręty" (Wtręt): krótki wtręt (2-4 zdania), który demonstruje pojęcie z tej sekcji humorystycznie albo kontrprzykładem: co się stanie, gdy zrobić odwrotnie albo źle. Może nawiązywać do wcześniejszych wtrętów (ta sama postać, rozwinięcie sytuacji), żeby czytelnik czuł ciągłość; nie kopiuj ich. (w dziale jest już 0 z 2, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji). Ustawienia: bohater: Marta, 34-letnia specjalistka ds. kadr, która w arkuszu kalkulacyjnym radzi sobie świetnie, ale kodu nigdy nie pisała. Co miesiąc rozlicza wspólne wydatki z współlokatorami (czynsz, zakupy, wyjazdy) i chce zastąpić ręczne formuły programem, który policzy podział z napiwkiem i rabatem oraz zapisze wynik do pliku; kłopoty jej sprawiają błędy w składni, niezrozumiałe komunikaty i obawa, że zepsuje coś w komputerze..

Wcześniejsze wpisy, które widzi moduł "dowcipy" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dowcipy] Gramatyka bez taryfy ulgowej: W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyk
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
Wcześniejsze wpisy, które widzi moduł "dygresje" (nie powtarzaj ich tematów, puent ani motywów):
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
Wcześniejsze wpisy, które widzi moduł "dykteryjki" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
Wcześniejsze wpisy, które widzi moduł "rysunki" (nie powtarzaj ich tematów, puent ani motywów):
  - [rysunki] Pętla poprawek przy stole: Przy drewnianym stole siedzi uśmiechnięta kobieta z ołówkiem i gumką. Przed nią kartka z ręcznie narysowanymi kółkami połączonymi strzałkami, które tworzą zamkn
Wcześniejsze wpisy, które widzi moduł "wtręty" (możesz do nich nawiązać, rozwijając postać albo sytuację; nie kopiuj):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dowcipy] Gramatyka bez taryfy ulgowej: W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyk
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 

W jednej sekcji najwyżej 2 dodatki łącznie; nie łącz w jednej sekcji modułów, które się nie lubią.
Dla każdego dodatku: module, title (maks. 8 słów), body; dla ilustracji także caption i alt.

SEKCJA "Przepis jako algorytm" (dział 02. Algorytmy i myślenie krokowe):
Przepis kulinarny to [[algorytm|algorytm]] zapisany dla kucharza: ma dane wejściowe (składniki), uporządkowane kroki i wynik (gotowe danie). Różnica polega na tym, że człowiek wybaczy przepisowi niedokładność, a komputer nie.

Zestawmy oba zapisy:

| Przepis | Algorytm |
|---|---|
| składniki i ich ilości | dane wejściowe |
| kolejne kroki: „pokrój”, „wymieszaj” | jednoznaczne instrukcje |
| „piecz 40 minut w 180°C” | [[warunek-zakonczenia|warunek zakończenia]] |
| gotowe ciasto | wynik |

Warunek zakończenia to sprawdzalny test „czy już koniec?”. „Piecz 40 minut” albo „piecz, aż termometr pokaże 95°C w środku” da się zmierzyć. „Piecz, aż się zrumieni” już nie, bo każdy inaczej oceni rumieniec.

Tak samo jest z „dodaj szczyptę soli” czy „smaż chwilę”: kucharz zinterpretuje to po swojemu. W algorytmie musi stać coś takiego jak „Podziel sumę przez liczbę osób”, bez pola na domysły.

Ten sam przepis mogą wykonać różne osoby w różnych kuchniach i wyjdzie to samo danie. Tak samo algorytm da się wykonać w Pythonie, w arkuszu albo na kartce.

Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”. Jej przepis to [[lm-8|cztery kroki rozliczenia, które już znasz]]: składniki to wydatki i liczba osób, a „danie” to saldo każdego.

Konsekwencja: pisząc algorytm, wyobraź sobie przepis dla kogoś, kto nigdy nie gotował. Jeśli taka osoba wykona go bez pytań, kroki są dość dokładne.
````

## Odpowiedź

````json
{
  "items": [
    {
      "module": "wtręty",
      "title": "Marta zapisuje warunek „aż będzie ładnie”",
      "body": "Marta napisała w programie: „odejmuj rabat od kolejnych rachunków, aż wynik będzie ładny”. Komputer nie miał jak sprawdzić, czy wynik jest „ładny”, bo to nie jest test, który da się zmierzyć. Marta zamieniła więc zdanie na „powtarzaj, aż suma przestanie się zmieniać albo skończą się rachunki”. Tym razem program wiedział, kiedy przestać.",
      "sources": []
    },
    {
      "module": "rysunki",
      "title": "Przepis dla kogoś, kto nigdy nie gotował",
      "body": "Jasna kuchnia. Początkujący kucharz w fartuchu stoi przy piekarniku z otwartymi drzwiczkami i ostrożnie wbija cienki termometr w złocisty placek na blasze. Na blacie obok stoją odmierzone miseczki ze składnikami, ustawione równo w rzędzie, oraz kuchenny minutnik. Za jego plecami uśmiechnięta przyjaciółka zagląda mu przez ramię z kartką przepisu w dłoni i unosi kciuk do góry. Nad piekarnikiem nie ma żadnych napisów, cała scena jest spokojna i uporządkowana.",
      "caption": "Jeśli ktoś, kto nigdy nie gotował, wykona przepis bez pytań, kroki są dość dokładne.",
      "alt": "Początkujący kucharz w fartuchu mierzy termometrem temperaturę ciasta w piekarniku, a przyjaciółka z kartką przepisu pokazuje uniesiony kciuk. Na blacie stoją odmierzone składniki i minutnik.",
      "sources": []
    }
  ]
}
````
