# Krok 0332 · autor_dodatków

Węzeł: `layers` · dział: 4 · pytanie: 19 · próba: —

## Prompt

````text
Dodajesz opcjonalne dodatki do sekcji tutorialu: Programowanie od podstaw.
Czytelnik: osoba spoza IT, poziom: początkujący.

Dodatki nie są potrzebne do zrozumienia sekcji; są dla przyjemności i pamięci. Każdy moduł ma cel: około tylu wpisów na dział, ile wynosi jego limit, rozłożonych na sekcje. Dodaj wpis, gdy ta sekcja daje dobrą okazję; kod pilnuje odstępów i limitów, weryfikator jakości. Nie wymyślaj na siłę: słaby dodatek zostanie odrzucony.
Każdy dodatek musi wynikać z treści TEJ sekcji i być poprawny: logicznie spójny, zgodny z faktami.
Nazwy z kodu pisz w backtickach.

Włączone moduły:
- module="dowcipy" (Z przymrużeniem oka): krótki żart, gra słów albo zabawna puenta o pojęciu z tej sekcji, najlepiej pomagająca je zapamiętać; 1-2 zdania. Ton dopasuj do czytelnika. Bez żartów z ludzi i grup. (w dziale jest już 0 z 2, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji).
- module="dygresje" (Na marginesie): ciekawostka, historia albo „a gdyby…” związane z sekcją; 2-4 zdania. Tylko gdy wnosi coś spoza głównego toku i nie jest potrzebna do zrozumienia sekcji. (w tej sekcji NIE dodawaj: za blisko dykteryjki „Komentarz, który przestał mówić prawdę” w sekcji „Do czego służą komentarze” (odstęp 1, wymagany 2)). Podaj w sources wiarygodne źródło (encyklopedia, publikacja, oficjalna strona) z adresem; bez źródła nie dodawaj.
- module="dykteryjki" (Z życia wzięte): krótka historia z pracy opowiedziana w pierwszej osobie przez narratora z ustawień: realistyczna sytuacja, w której pojęcie z tej sekcji miało znaczenie, jaki był skutek i czego nauczyła; 3-5 zdań. To ilustracja typowej sytuacji, nie reportaż: bez nazw firm, ludzi i dat. (w tej sekcji NIE dodawaj: za blisko dykteryjki „Komentarz, który przestał mówić prawdę” w sekcji „Do czego służą komentarze” (odstęp 1, wymagany 2)). Ustawienia: narrator: doświadczony Python developer, kilkanaście lat w projektach backendowych i automatyzacji; ton: poważny, rzeczowy, bez żartów.
- module="rysunki" (Ilustracja): pomysł na zabawny, prosty rysunek oparty na metaforze z tej sekcji. body: prompt dla generatora obrazów (scena, postacie, co ma być widać, bez tekstu na obrazku); caption: podpis pod rysunkiem; alt: opis dla osób niewidzących. Styl rysunku jest wspólny dla tutorialu. (w dziale jest już 0 z 1, zostało sekcji: 1; PRIORYTET: w tym dziale jeszcze go nie ma, a zostało niewiele sekcji). Ustawienia: styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.. W body opisz tylko scenę; styl dopisuje renderer.
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
  - [wtręty] Marta czeka, aż plik sam zadziała: Marta wpisała w `kasa.py` cały podział wydatków, zapisała plik i patrzyła w ekran, czekając na wynik. Nic się nie działo, więc uznała, że komputer jest wolny, a
  - [dowcipy] Tłumacz książki i tłumacz symultaniczny: Kompilator to tłumacz, który zabiera całą książkę i oddaje ją przetłumaczoną dopiero na końcu. Interpreter to tłumacz symultaniczny: mówi na bieżąco, więc o błę
  - [wtręty] Marta widzi komunikat i odsuwa się od klawiatury: Marta zamiast `print` wpisała `prnt`, uruchomiła plik i zobaczyła czerwony komunikat o nieznanej nazwie. Cofnęła ręce z klawiatury jak spod gorącego piekarnika,
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo
Wcześniejsze wpisy, które widzi moduł "dygresje" (nie powtarzaj ich tematów, puent ani motywów):
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
  - [dygresje] Skąd Python wziął swoją nazwę: Polecenie `python`, którego używamy do uruchamiania plików, ma nazwę nie od węża, lecz od brytyjskiego programu komediowego. Twórca języka, Guido van Rossum, cz
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo
Wcześniejsze wpisy, które widzi moduł "dykteryjki" (nie powtarzaj ich tematów, puent ani motywów):
  - [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo,
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [wtręty] Marta wpisuje złą liczbę osób: Marta poprawiła instrukcję i wpisała ją precyzyjnie: „podziel sumę przez 3”. Zapomniała, że w mieszkaniu są cztery osoby, wliczając ją samą. Komputer podzielił 
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [wtręty] Marta odejmuje udział, zanim go policzy: Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wyno
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [wtręty] Marta zleca całe rozliczenie jednym zdaniem: Marta wpisała jedną instrukcję: „rozlicz wyjazd”. Kiedy wynik się nie zgadzał, nie umiała powiedzieć, czy zawiodła suma, udział, czy porównanie z wpłatą, bo wsz
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
  - [wtręty] Marta czeka, aż plik sam zadziała: Marta wpisała w `kasa.py` cały podział wydatków, zapisała plik i patrzyła w ekran, czekając na wynik. Nic się nie działo, więc uznała, że komputer jest wolny, a
  - [dygresje] Skąd Python wziął swoją nazwę: Polecenie `python`, którego używamy do uruchamiania plików, ma nazwę nie od węża, lecz od brytyjskiego programu komediowego. Twórca języka, Guido van Rossum, cz
  - [wtręty] Marta widzi komunikat i odsuwa się od klawiatury: Marta zamiast `print` wpisała `prnt`, uruchomiła plik i zobaczyła czerwony komunikat o nieznanej nazwie. Cofnęła ręce z klawiatury jak spod gorącego piekarnika,
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo
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
  - [wtręty] Marta czeka, aż plik sam zadziała: Marta wpisała w `kasa.py` cały podział wydatków, zapisała plik i patrzyła w ekran, czekając na wynik. Nic się nie działo, więc uznała, że komputer jest wolny, a
  - [dowcipy] Tłumacz książki i tłumacz symultaniczny: Kompilator to tłumacz, który zabiera całą książkę i oddaje ją przetłumaczoną dopiero na końcu. Interpreter to tłumacz symultaniczny: mówi na bieżąco, więc o błę
  - [wtręty] Marta widzi komunikat i odsuwa się od klawiatury: Marta zamiast `print` wpisała `prnt`, uruchomiła plik i zobaczyła czerwony komunikat o nieznanej nazwie. Cofnęła ręce z klawiatury jak spod gorącego piekarnika,
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo

W jednej sekcji najwyżej 2 dodatki łącznie; nie łącz w jednej sekcji modułów, które się nie lubią.
Dla każdego dodatku: module, title (maks. 8 słów), body; dla ilustracji także caption i alt.

SEKCJA "Czym jest dana" (dział 04. Dane i zmienne):
[[dana|Dana]] to każda informacja, na której pracuje program: imię, kwota, data, odpowiedź „tak” lub „nie”. Program bez danych nie miałby czego liczyć ani wypisać.

W arkuszu kalkulacyjnym danymi są wartości w komórkach: nazwisko w jednej, kwota w drugiej. W programie jest podobnie, tylko że dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz.

```python
# poza kanonem
print("Ania")       # tekst: imię
print(45.5)         # liczba: kwota
print(True)         # prawda albo fałsz: czy zapłacono
print(45.5 + 10)    # z liczbą można liczyć
```

```text
Ania
45.5
True
55.5
```

Każda z tych trzech wartości to jedna dana, ale każda jest innego rodzaju. Rodzaj danej decyduje o tym, co program może z nią zrobić. Do liczby 45.5 da się dodać 10 albo ją podzielić. Imienia „Ania” nie da się podzielić przez 2, bo to nie ma sensu; można je co najwyżej wypisać, porównać z innym albo połączyć z innym tekstem. Prawda lub fałsz odpowiada na pytanie tak/nie.

Dane trzeba też gdzieś przechowywać, żeby użyć ich więcej niż raz. Do tego służy zmienna, którą poznasz w następnej sekcji. To, jak Python nazywa poszczególne rodzaje danych, wyjaśnimy przy typach danych.
````

## Odpowiedź

````json
{
  "items": [
    {
      "module": "dowcipy",
      "title": "Program bez danych jak kuchnia bez produktów",
      "body": "Program bez danych to kucharz bez produktów: piec rozgrzany, fartuch wyprasowany, a obiadu i tak nie będzie."
    },
    {
      "module": "wtręty",
      "title": "Marta dzieli Anię przez dwa",
      "body": "Marta chciała rozliczyć udział Ani i w miejscu kwoty wpisała jej imię: „Ania” podzielone przez 2. Komputer odmówił z komunikatem o błędzie, bo imię jest daną innego rodzaju niż kwota i dzielić go się nie da. Marta odetchnęła: to nie ona zepsuła komputer, tylko pomyliła komórkę, tak samo jak zdarza się to w arkuszu."
    }
  ]
}
````
