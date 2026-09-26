# Krok 0082 · autor_dodatków

Węzeł: `layers` · dział: 1 · pytanie: 6 · próba: —

## Prompt

````text
Dodajesz opcjonalne dodatki do sekcji tutorialu: Programowanie od podstaw.
Czytelnik: osoba spoza IT, poziom: początkujący.

Dodatki nie są potrzebne do zrozumienia sekcji; są dla przyjemności i pamięci. Każdy moduł ma cel: około tylu wpisów na dział, ile wynosi jego limit, rozłożonych na sekcje. Dodaj wpis, gdy ta sekcja daje dobrą okazję; kod pilnuje odstępów i limitów, weryfikator jakości. Nie wymyślaj na siłę: słaby dodatek zostanie odrzucony.
Każdy dodatek musi wynikać z treści TEJ sekcji i być poprawny: logicznie spójny, zgodny z faktami.
Nazwy z kodu pisz w backtickach.

Włączone moduły:
- module="dowcipy" (Z przymrużeniem oka): krótki żart, gra słów albo zabawna puenta o pojęciu z tej sekcji, najlepiej pomagająca je zapamiętać; 1-2 zdania. Ton dopasuj do czytelnika. Bez żartów z ludzi i grup. (w dziale jest już 1 z 2, zostało sekcji: 1).
- module="dygresje" (Na marginesie): ciekawostka, historia albo „a gdyby…” związane z sekcją; 2-4 zdania. Tylko gdy wnosi coś spoza głównego toku i nie jest potrzebna do zrozumienia sekcji. (w dziale jest już 1 z 2, zostało sekcji: 1). Podaj w sources wiarygodne źródło (encyklopedia, publikacja, oficjalna strona) z adresem; bez źródła nie dodawaj.
- module="dykteryjki" (Z życia wzięte): krótka historia z pracy opowiedziana w pierwszej osobie przez narratora z ustawień: realistyczna sytuacja, w której pojęcie z tej sekcji miało znaczenie, jaki był skutek i czego nauczyła; 3-5 zdań. To ilustracja typowej sytuacji, nie reportaż: bez nazw firm, ludzi i dat. (w dziale jest już 0 z 2, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji). Ustawienia: narrator: doświadczony Python developer, kilkanaście lat w projektach backendowych i automatyzacji; ton: poważny, rzeczowy, bez żartów.
- module="rysunki" (Ilustracja): pomysł na zabawny, prosty rysunek oparty na metaforze z tej sekcji. body: prompt dla generatora obrazów (scena, postacie, co ma być widać, bez tekstu na obrazku); caption: podpis pod rysunkiem; alt: opis dla osób niewidzących. Styl rysunku jest wspólny dla tutorialu. (w tym dziale limit jest wyczerpany: nie dodawaj). Ustawienia: styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.. W body opisz tylko scenę; styl dopisuje renderer.
- module="wtręty" (Wtręt): krótki wtręt (2-4 zdania), który demonstruje pojęcie z tej sekcji humorystycznie albo kontrprzykładem: co się stanie, gdy zrobić odwrotnie albo źle. Może nawiązywać do wcześniejszych wtrętów (ta sama postać, rozwinięcie sytuacji), żeby czytelnik czuł ciągłość; nie kopiuj ich. (w tej sekcji NIE dodawaj: za blisko wtręty „Marta wpisuje złą liczbę osób” w sekcji „Po co komputerowi precyzja” (odstęp 1, wymagany 2)). Ustawienia: bohater: Marta, 34-letnia specjalistka ds. kadr, która w arkuszu kalkulacyjnym radzi sobie świetnie, ale kodu nigdy nie pisała. Co miesiąc rozlicza wspólne wydatki z współlokatorami (czynsz, zakupy, wyjazdy) i chce zastąpić ręczne formuły programem, który policzy podział z napiwkiem i rabatem oraz zapisze wynik do pliku; kłopoty jej sprawiają błędy w składni, niezrozumiałe komunikaty i obawa, że zepsuje coś w komputerze..

Wcześniejsze wpisy, które widzi moduł "dowcipy" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dowcipy] Gramatyka bez taryfy ulgowej: W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyk
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
Wcześniejsze wpisy, które widzi moduł "dygresje" (nie powtarzaj ich tematów, puent ani motywów):
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
Wcześniejsze wpisy, które widzi moduł "dykteryjki" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
Wcześniejsze wpisy, które widzi moduł "rysunki" (nie powtarzaj ich tematów, puent ani motywów):
  - [rysunki] Pętla poprawek przy stole: Przy drewnianym stole siedzi uśmiechnięta kobieta z ołówkiem i gumką. Przed nią kartka z ręcznie narysowanymi kółkami połączonymi strzałkami, które tworzą zamkn
Wcześniejsze wpisy, które widzi moduł "wtręty" (możesz do nich nawiązać, rozwijając postać albo sytuację; nie kopiuj):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dowcipy] Gramatyka bez taryfy ulgowej: W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyk
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 

W jednej sekcji najwyżej 2 dodatki łącznie; nie łącz w jednej sekcji modułów, które się nie lubią.
Dla każdego dodatku: module, title (maks. 8 słów), body; dla ilustracji także caption i alt.

SEKCJA "Program a aplikacja" (dział 01. Czym jest programowanie):
Program to ciąg instrukcji, które komputer wykonuje. [[aplikacja|Aplikacja]] to program (albo zestaw programów) przygotowany tak, by zwykły użytkownik mógł z niego wygodnie korzystać: z oknem, przyciskami, zapisem danych i instrukcją obsługi. Każda aplikacja jest więc programem, ale nie każdy program jest aplikacją.

Różnica dotyczy głównie tego, dla kogo coś powstało. Program może być krótkim skryptem napisanym dla siebie, który robi jedną rzecz i nie ma żadnej oprawy. Aplikacja musi jeszcze radzić sobie z pomyłkami użytkownika, zapamiętywać jego dane i być zrozumiała bez znajomości kodu.

| | Program | Aplikacja |
|---|---|---|
| Dla kogo | często dla autora | dla wielu użytkowników |
| Wygląd | może być sam tekst w terminalu | okna, przyciski, menu |
| Obsługa błędów | minimalna | przewidziane komunikaty i pomoc |
| Przykład | kilka linii liczących rachunek | arkusz kalkulacyjny, aplikacja bankowa |

W praktyce granica jest płynna, a w mowie potocznej oba słowa często zamienia się miejscami. Ważne, by rozumieć, że wokół samych instrukcji można dobudować wiele warstw wygody.

„Wspólna Kasa”, przykład, który będzie nam towarzyszył, zacznie jako mały program: wczyta wydatki i wypisze, kto komu ile jest winien. Nie będzie miała okna ani przycisków. Dopiero dobudowana oprawa (pytania do użytkownika, sprawdzanie danych) przybliży ją do aplikacji.

Konsekwencja: zaczynamy od programu, bo to on jest rdzeniem. Oprawę dodaje się później, gdy rdzeń działa.
````

## Odpowiedź

````json
{
  "items": [
    {
      "module": "dykteryjki",
      "title": "Skrypt, który wyszedł poza biurko autora",
      "body": "Kiedyś napisałem dla siebie kilkadziesiąt linii w Pythonie, które zestawiały dwa eksporty z systemu i wskazywały rozbieżności. Działało bez zarzutu, dopóki kolega z działu nie poprosił o kopię. Podał programowi plik w innym układzie kolumn i dostał kilkanaście linii komunikatu o błędzie, z którego nic nie wynikało. Musiałem dopisać sprawdzanie formatu, czytelne komunikaty i krótką instrukcję. Wtedy zrozumiałem, że kod się nie zmienił, tylko zmienił się odbiorca, a razem z nim wymagania: to, co wystarczało mnie, dla kogoś innego było dopiero połową pracy."
    },
    {
      "module": "dowcipy",
      "title": "Działa u mnie",
      "body": "Program działa u autora. Aplikacja działa u kogoś, kto autora nigdy nie widział i nie zamierza go pytać, co miał na myśli."
    }
  ]
}
````
