# Krok 0240 · autor_dodatków

Węzeł: `layers` · dział: 3 · pytanie: 15 · próba: —

## Prompt

````text
Dodajesz opcjonalne dodatki do sekcji tutorialu: Programowanie od podstaw.
Czytelnik: osoba spoza IT, poziom: początkujący.

Dodatki nie są potrzebne do zrozumienia sekcji; są dla przyjemności i pamięci. Każdy moduł ma cel: około tylu wpisów na dział, ile wynosi jego limit, rozłożonych na sekcje. Dodaj wpis, gdy ta sekcja daje dobrą okazję; kod pilnuje odstępów i limitów, weryfikator jakości. Nie wymyślaj na siłę: słaby dodatek zostanie odrzucony.
Każdy dodatek musi wynikać z treści TEJ sekcji i być poprawny: logicznie spójny, zgodny z faktami.
Nazwy z kodu pisz w backtickach.

Włączone moduły:
- module="dowcipy" (Z przymrużeniem oka): krótki żart, gra słów albo zabawna puenta o pojęciu z tej sekcji, najlepiej pomagająca je zapamiętać; 1-2 zdania. Ton dopasuj do czytelnika. Bez żartów z ludzi i grup. (w tej sekcji NIE dodawaj: za blisko dowcipy „Numery linii jak numery domów” w sekcji „Do czego służy edytor” (odstęp 1, wymagany 2)).
- module="dygresje" (Na marginesie): ciekawostka, historia albo „a gdyby…” związane z sekcją; 2-4 zdania. Tylko gdy wnosi coś spoza głównego toku i nie jest potrzebna do zrozumienia sekcji. (w dziale jest już 0 z 2, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji). Podaj w sources wiarygodne źródło (encyklopedia, publikacja, oficjalna strona) z adresem; bez źródła nie dodawaj.
- module="dykteryjki" (Z życia wzięte): krótka historia z pracy opowiedziana w pierwszej osobie przez narratora z ustawień: realistyczna sytuacja, w której pojęcie z tej sekcji miało znaczenie, jaki był skutek i czego nauczyła; 3-5 zdań. To ilustracja typowej sytuacji, nie reportaż: bez nazw firm, ludzi i dat. (w dziale jest już 1 z 2, zostało sekcji: 1). Ustawienia: narrator: doświadczony Python developer, kilkanaście lat w projektach backendowych i automatyzacji; ton: poważny, rzeczowy, bez żartów.
- module="rysunki" (Ilustracja): pomysł na zabawny, prosty rysunek oparty na metaforze z tej sekcji. body: prompt dla generatora obrazów (scena, postacie, co ma być widać, bez tekstu na obrazku); caption: podpis pod rysunkiem; alt: opis dla osób niewidzących. Styl rysunku jest wspólny dla tutorialu. (w tej sekcji NIE dodawaj: za blisko rysunki „Pomocnik z zakreślaczami” w sekcji „Do czego służy edytor” (odstęp 1, wymagany 3)). Ustawienia: styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.. W body opisz tylko scenę; styl dopisuje renderer.
- module="wtręty" (Wtręt): krótki wtręt (2-4 zdania), który demonstruje pojęcie z tej sekcji humorystycznie albo kontrprzykładem: co się stanie, gdy zrobić odwrotnie albo źle. Może nawiązywać do wcześniejszych wtrętów (ta sama postać, rozwinięcie sytuacji), żeby czytelnik czuł ciągłość; nie kopiuj ich. (w dziale jest już 0 z 2, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji). Ustawienia: bohater: Marta, 34-letnia specjalistka ds. kadr, która w arkuszu kalkulacyjnym radzi sobie świetnie, ale kodu nigdy nie pisała. Co miesiąc rozlicza wspólne wydatki z współlokatorami (czynsz, zakupy, wyjazdy) i chce zastąpić ręczne formuły programem, który policzy podział z napiwkiem i rabatem oraz zapisze wynik do pliku; kłopoty jej sprawiają błędy w składni, niezrozumiałe komunikaty i obawa, że zepsuje coś w komputerze..

Wcześniejsze wpisy, które widzi moduł "dowcipy" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dowcipy] Gramatyka bez taryfy ulgowej: W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyk
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
  - [wtręty] Marta odejmuje udział, zanim go policzy: Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wyno
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [dowcipy] Rondo bez zjazdu: Schemat blokowy bez strzałki „nie” wychodzącej z ostatniego rombu przypomina rondo bez zjazdów: wszystko jest poprawnie narysowane, tylko nikt stamtąd nie wyjed
  - [wtręty] Marta zleca całe rozliczenie jednym zdaniem: Marta wpisała jedną instrukcję: „rozlicz wyjazd”. Kiedy wynik się nie zgadzał, nie umiała powiedzieć, czy zawiodła suma, udział, czy porównanie z wpłatą, bo wsz
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
  - [dowcipy] Numery linii jak numery domów: Komunikat „błąd w linii 3” bez numerów linii to jak list z adresem „mieszkam na ulicy, po lewej”. Edytor kodu daje każdej linii numer, żeby listonosz nie musiał
Wcześniejsze wpisy, które widzi moduł "dygresje" (nie powtarzaj ich tematów, puent ani motywów):
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
Wcześniejsze wpisy, które widzi moduł "dykteryjki" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [wtręty] Marta odejmuje udział, zanim go policzy: Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wyno
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [wtręty] Marta zleca całe rozliczenie jednym zdaniem: Marta wpisała jedną instrukcję: „rozlicz wyjazd”. Kiedy wynik się nie zgadzał, nie umiała powiedzieć, czy zawiodła suma, udział, czy porównanie z wpłatą, bo wsz
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
Wcześniejsze wpisy, które widzi moduł "rysunki" (nie powtarzaj ich tematów, puent ani motywów):
  - [rysunki] Pętla poprawek przy stole: Przy drewnianym stole siedzi uśmiechnięta kobieta z ołówkiem i gumką. Przed nią kartka z ręcznie narysowanymi kółkami połączonymi strzałkami, które tworzą zamkn
  - [rysunki] Przepis dla kogoś, kto nigdy nie gotował: Jasna kuchnia. Początkujący kucharz w fartuchu stoi przy piekarniku z otwartymi drzwiczkami i ostrożnie wbija cienki termometr w złocisty placek na blasze. Na b
  - [rysunki] Pomocnik z zakreślaczami: Ciepła scena przy biurku: uśmiechnięta osoba siedzi przed laptopem, na którego ekranie widać kilka linii abstrakcyjnego kodu jako kolorowe paski i kropki, bez c
Wcześniejsze wpisy, które widzi moduł "wtręty" (możesz do nich nawiązać, rozwijając postać albo sytuację; nie kopiuj):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dowcipy] Gramatyka bez taryfy ulgowej: W polskim brak przecinka najwyżej zmienia sens zdania, a w Pythonie brak jednego cudzysłowu zmienia „program” w komunikat o błędzie. Składnia to jedyna gramatyk
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
  - [wtręty] Marta odejmuje udział, zanim go policzy: Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wyno
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [dowcipy] Rondo bez zjazdu: Schemat blokowy bez strzałki „nie” wychodzącej z ostatniego rombu przypomina rondo bez zjazdów: wszystko jest poprawnie narysowane, tylko nikt stamtąd nie wyjed
  - [wtręty] Marta zleca całe rozliczenie jednym zdaniem: Marta wpisała jedną instrukcję: „rozlicz wyjazd”. Kiedy wynik się nie zgadzał, nie umiała powiedzieć, czy zawiodła suma, udział, czy porównanie z wpłatą, bo wsz
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
  - [dowcipy] Numery linii jak numery domów: Komunikat „błąd w linii 3” bez numerów linii to jak list z adresem „mieszkam na ulicy, po lewej”. Edytor kodu daje każdej linii numer, żeby listonosz nie musiał

W jednej sekcji najwyżej 2 dodatki łącznie; nie łącz w jednej sekcji modułów, które się nie lubią.
Dla każdego dodatku: module, title (maks. 8 słów), body; dla ilustracji także caption i alt.

SEKCJA "Co znaczy uruchomić program" (dział 03. Kod i jego uruchamianie):
Uruchomić program to polecić komputerowi, by zaczął wykonywać instrukcje zapisane w pliku, od pierwszej do ostatniej. Sam [[kod-zrodlowy|kod źródłowy]] leży wtedy jak przepis w szufladzie: nic się nie dzieje, dopóki ktoś nie zacznie go realizować.

Plik z kodem czyta i wykonuje linia po linii inny program. W Pythonie robi to sam Python, a my podajemy mu nazwę pliku. Czym dokładnie jest taki wykonawca i czym różni się od kompilatora, wyjaśnimy w następnej części.

Polecenie wpisujemy w [[terminal|terminalu]], czyli oknie, w którym komputer przyjmuje polecenia pisane tekstem i odpowiada tekstem. U siebie masz już plik `kasa.py`:

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
```

W terminalu, w katalogu z plikiem, wpisujemy `python kasa.py`, a program wypisuje:

```text
Wspólna Kasa
```

Linia z `#` to komentarz, który Python pomija, więc wykonuje się tylko `print`. Gdyby linii było więcej, wykonywałyby się jedna po drugiej, w kolejności zapisu.

Uruchomienie nie zmienia pliku. Możesz go uruchamiać dowolnie wiele razy, a po każdej poprawce w edytorze uruchomić ponownie i zobaczyć efekt. Tak wygląda codzienna praca: zapisz, uruchom, przeczytaj wynik.
````

## Odpowiedź

````json
{
  "items": [
    {
      "module": "wtręty",
      "title": "Marta czeka, aż plik sam zadziała",
      "body": "Marta wpisała w `kasa.py` cały podział wydatków, zapisała plik i patrzyła w ekran, czekając na wynik. Nic się nie działo, więc uznała, że komputer jest wolny, a potem, że coś zepsuła. Dopiero gdy wpisała w terminalu `python kasa.py`, pojawił się wynik: sam zapis pliku to tylko położenie przepisu w szufladzie, a gotować ktoś musi zacząć."
    },
    {
      "module": "dygresje",
      "title": "Skąd Python wziął swoją nazwę",
      "body": "Polecenie `python`, którego używamy do uruchamiania plików, ma nazwę nie od węża, lecz od brytyjskiego programu komediowego. Twórca języka, Guido van Rossum, czytał w czasie pracy nad nim scenariusze „Monty Python's Flying Circus” i chciał nazwy krótkiej, unikalnej i lekko tajemniczej. Stąd w dokumentacji języka i przykładach często pojawiają się żarty z tego programu.",
      "sources": [
        {
          "title": "Python FAQ: Why is it called Python?",
          "url": "https://docs.python.org/3/faq/general.html#why-is-it-called-python",
          "supports": "Guido van Rossum czytał scenariusze Monty Python's Flying Circus i stąd wzięła się nazwa języka."
        }
      ]
    }
  ]
}
````
