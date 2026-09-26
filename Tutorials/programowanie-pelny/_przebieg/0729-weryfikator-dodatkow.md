# Krok 0729 · weryfikator_dodatków

Węzeł: `layers` · dział: 7 · pytanie: 38 · próba: —

## Prompt

````text
Jesteś weryfikatorem dodatków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.
Sprawdź każdy dodatek (dygresję, żart, pomysł na ilustrację) do sekcji poniżej:
1. Logika: czy puenta, porównanie albo scena mają sens i są wewnętrznie spójne (np. żart mówi o literówce,
   a w jego przykładzie żadnej literówki nie ma, to błąd).
2. Zgodność z sekcją: czy dodatek naprawdę dotyczy tego, co sekcja mówi, i nie przeczy jej.
3. Fakty: daty, nazwiska, historie. Odrzuć, jeśli fakt jest błędny albo nie masz pewności, że jest prawdziwy.
4. Ton: bez żartów z ludzi i grup.
5. Rejestr: dodatek, który powtarza temat, puentę albo motyw wcześniejszego wpisu z zakazem powtórzeń, jest błędny;
   nawiązanie do wcześniejszego wpisu jest dobre tylko wtedy, gdy zgadza się z pierwowzorem.
6. Źródła: dodatek oznaczony [źródło wymagane] musi mieć źródło, które faktycznie otworzysz (WebFetch) i które
   potwierdza jego twierdzenia. Potwierdzone źródło podaj w source (title, url, supports). Bez potwierdzenia: ok=false.
Dla każdego podaj index, ok i przy ok=false jednozdaniowe problem.
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
  - [dowcipy] Program bez danych jak kuchnia bez produktów: Program bez danych to kucharz bez produktów: piec rozgrzany, fartuch wyprasowany, a obiadu i tak nie będzie.
  - [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech mie
  - [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamó
  - [wtręty] Marta bierze kwotę w cudzysłów: Marta wpisała kwotę jako `"45.5"`, bo w arkuszu tak oznaczała tekstowe komórki, i kazała programowi podzielić ją przez 2. Zamiast `22.75` dostała czerwony `Type
  - [dowcipy] Odpowiedź „no, prawie”: Zapytany, czy współlokator zwrócił pieniądze, program odpowiada `True` albo `False`. Odpowiedź „no, prawie oddał” nie należy do typu `bool`, choć w prawdziwych 
  - [dykteryjki] Cena brutto, która nie nadążała: W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach l
  - [dowcipy] Reszta z dzielenia to ostatni kawałek pizzy: Operator `%` to ten, kto liczy, ile kawałków pizzy zostanie, gdy każdy wziął po równo. Ludzie się wahają, czy sięgnąć po ostatni, ale Python nigdy nie ma z tym 
  - [wtręty] Marta skleja jak w arkuszu: W arkuszu Marta łączyła tekst z liczbą znakiem `&` i nigdy nie miała z tym kłopotu. Napisała więc w Pythonie `"Do zapłaty: " + udzial`, gdzie `udzial` było licz
  - [dykteryjki] Status zapisany małą literą: W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze sta
  - [wtręty] Marta wcina tylko jedną linię: Marta napisała: `if kwota > 100:`, pod spodem wcięte `print("Duża kwota")`, a linię `print("Sprawdź paragon")` zostawiła bez wcięcia, bo chciała ją pokazać tylk
  - [wtręty] Marta kopiuje linię dla każdej osoby: Marta chciała wypisać komunikat dla każdego współlokatora, więc trzy razy wkleiła linię `print("Cześć,", imie)`, za każdym razem z innym imieniem. Gdy w mieszka
  - [dykteryjki] Ponawianie, które nigdy się nie kończyło: Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciel
  - [dowcipy] Pusta lista to torba przed sklepem: Pusta lista `[]` to torba na zakupy przed wejściem do sklepu: już istnieje, ale nic w niej nie ma. `len()` odpowie uczciwie: 0.
  - [wtręty] Marta prosi o czwartego, którego nie ma: Marta miała listę czterech współlokatorów i chciała pokazać ostatniego, więc napisała `osoby[4]`, bo liczyła po ludzku: pierwszy, drugi, trzeci, czwarty. Progra
  - [dowcipy] Lista obecności bez wołania w próżnię: Pętla `for` działa jak nauczyciel z dziennikiem: woła każdego z listy po kolei i na ostatnim nazwisku kończy. Nie stoi potem w drzwiach z pytaniem „a nie ma tu 
Wcześniejsze wpisy, które widzi moduł "dygresje" (nie powtarzaj ich tematów, puent ani motywów):
  - [dygresje] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Be
  - [dygresje] Skąd wzięło się słowo „algorytm”: Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych c
  - [dykteryjki] Archiwizacja przed wygenerowaniem raportu: W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze ra
  - [dykteryjki] Cudzysłowy skopiowane z dokumentu: Kolega przesłał mi fragment skryptu w dokumencie tekstowym, a ja wkleiłem go do pliku `.py` i uruchomiłem. Skrypt zakończył się błędem składni w linii, która na
  - [dygresje] Skąd Python wziął swoją nazwę: Polecenie `python`, którego używamy do uruchamiania plików, ma nazwę nie od węża, lecz od brytyjskiego programu komediowego. Twórca języka, Guido van Rossum, cz
  - [dykteryjki] Komentarz, który przestał mówić prawdę: W skrypcie do automatyzacji raportów stał komentarz „limit: 30 dni”, a w kodzie obok liczba 90. Ktoś kiedyś zmienił wartość i nie ruszył opisu. Przez kilka tygo
  - [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamó
  - [dygresje] Rakieta, która pomyliła typy liczb: W 1996 roku pierwsza rakieta Ariane 5 rozpadła się po niespełna 40 sekundach lotu. Komisja badająca wypadek wskazała, że oprogramowanie zamieniało liczbę z ułam
  - [dykteryjki] Cena brutto, która nie nadążała: W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach l
  - [dykteryjki] Status zapisany małą literą: W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze sta
  - [dykteryjki] Ponawianie, które nigdy się nie kończyło: Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciel
  - [dygresje] Dlaczego liczenie zaczyna się od zera: Holenderski informatyk Edsger Dijkstra w krótkiej notatce z 1982 roku przekonywał, że numerację warto zaczynać od zera, a zakresy zapisywać tak, by początek był
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
  - [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech mie
  - [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamó
  - [wtręty] Marta bierze kwotę w cudzysłów: Marta wpisała kwotę jako `"45.5"`, bo w arkuszu tak oznaczała tekstowe komórki, i kazała programowi podzielić ją przez 2. Zamiast `22.75` dostała czerwony `Type
  - [dygresje] Rakieta, która pomyliła typy liczb: W 1996 roku pierwsza rakieta Ariane 5 rozpadła się po niespełna 40 sekundach lotu. Komisja badająca wypadek wskazała, że oprogramowanie zamieniało liczbę z ułam
  - [dykteryjki] Cena brutto, która nie nadążała: W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach l
  - [wtręty] Marta skleja jak w arkuszu: W arkuszu Marta łączyła tekst z liczbą znakiem `&` i nigdy nie miała z tym kłopotu. Napisała więc w Pythonie `"Do zapłaty: " + udzial`, gdzie `udzial` było licz
  - [dykteryjki] Status zapisany małą literą: W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze sta
  - [wtręty] Marta wcina tylko jedną linię: Marta napisała: `if kwota > 100:`, pod spodem wcięte `print("Duża kwota")`, a linię `print("Sprawdź paragon")` zostawiła bez wcięcia, bo chciała ją pokazać tylk
  - [wtręty] Marta kopiuje linię dla każdej osoby: Marta chciała wypisać komunikat dla każdego współlokatora, więc trzy razy wkleiła linię `print("Cześć,", imie)`, za każdym razem z innym imieniem. Gdy w mieszka
  - [dykteryjki] Ponawianie, które nigdy się nie kończyło: Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciel
  - [dygresje] Dlaczego liczenie zaczyna się od zera: Holenderski informatyk Edsger Dijkstra w krótkiej notatce z 1982 roku przekonywał, że numerację warto zaczynać od zera, a zakresy zapisywać tak, by początek był
  - [wtręty] Marta prosi o czwartego, którego nie ma: Marta miała listę czterech współlokatorów i chciała pokazać ostatniego, więc napisała `osoby[4]`, bo liczyła po ludzku: pierwszy, drugi, trzeci, czwarty. Progra
Wcześniejsze wpisy, które widzi moduł "rysunki" (nie powtarzaj ich tematów, puent ani motywów):
  - [rysunki] Pętla poprawek przy stole: Przy drewnianym stole siedzi uśmiechnięta kobieta z ołówkiem i gumką. Przed nią kartka z ręcznie narysowanymi kółkami połączonymi strzałkami, które tworzą zamkn
  - [rysunki] Przepis dla kogoś, kto nigdy nie gotował: Jasna kuchnia. Początkujący kucharz w fartuchu stoi przy piekarniku z otwartymi drzwiczkami i ostrożnie wbija cienki termometr w złocisty placek na blasze. Na b
  - [rysunki] Pomocnik z zakreślaczami: Ciepła scena przy biurku: uśmiechnięta osoba siedzi przed laptopem, na którego ekranie widać kilka linii abstrakcyjnego kodu jako kolorowe paski i kropki, bez c
  - [rysunki] Dwa pudełka, dwie etykiety: Jasny pokój z drewnianą półką. Na półce stoją obok siebie dwa kartonowe pudełka z doczepionymi papierowymi etykietami (puste kartki, bez tekstu). Uśmiechnięta o
  - [rysunki] Rozwidlenie drogi bez trzeciej ścieżki: Wiejska droga rozwidla się na dwie ścieżki: jedna prowadzi do niebieskiego domku z ogródkiem, druga na łąkę z drzewem. Przy rozwidleniu stoi uśmiechnięty wędrow
  - [rysunki] Chomik w kole bez wyjścia: Ciepła scena w pokoju: puszysty chomik biegnie w kole w klatce, z determinacją na pyszczku. Z boku koła widać wyraźnie otwarte małe drzwiczki, ale chomik patrzy
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
  - [dowcipy] Program bez danych jak kuchnia bez produktów: Program bez danych to kucharz bez produktów: piec rozgrzany, fartuch wyprasowany, a obiadu i tak nie będzie.
  - [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech mie
  - [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamó
  - [wtręty] Marta bierze kwotę w cudzysłów: Marta wpisała kwotę jako `"45.5"`, bo w arkuszu tak oznaczała tekstowe komórki, i kazała programowi podzielić ją przez 2. Zamiast `22.75` dostała czerwony `Type
  - [dowcipy] Odpowiedź „no, prawie”: Zapytany, czy współlokator zwrócił pieniądze, program odpowiada `True` albo `False`. Odpowiedź „no, prawie oddał” nie należy do typu `bool`, choć w prawdziwych 
  - [dykteryjki] Cena brutto, która nie nadążała: W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach l
  - [dowcipy] Reszta z dzielenia to ostatni kawałek pizzy: Operator `%` to ten, kto liczy, ile kawałków pizzy zostanie, gdy każdy wziął po równo. Ludzie się wahają, czy sięgnąć po ostatni, ale Python nigdy nie ma z tym 
  - [wtręty] Marta skleja jak w arkuszu: W arkuszu Marta łączyła tekst z liczbą znakiem `&` i nigdy nie miała z tym kłopotu. Napisała więc w Pythonie `"Do zapłaty: " + udzial`, gdzie `udzial` było licz
  - [dykteryjki] Status zapisany małą literą: W skrypcie do przetwarzania zamówień wybierałem rekordy warunkiem `status == "Aktywny"`. Po zmianie systemu źródłowego część rekordów zaczęła przychodzić ze sta
  - [wtręty] Marta wcina tylko jedną linię: Marta napisała: `if kwota > 100:`, pod spodem wcięte `print("Duża kwota")`, a linię `print("Sprawdź paragon")` zostawiła bez wcięcia, bo chciała ją pokazać tylk
  - [wtręty] Marta kopiuje linię dla każdej osoby: Marta chciała wypisać komunikat dla każdego współlokatora, więc trzy razy wkleiła linię `print("Cześć,", imie)`, za każdym razem z innym imieniem. Gdy w mieszka
  - [dykteryjki] Ponawianie, które nigdy się nie kończyło: Napisałem skrypt, który w pętli `while` czekał, aż w katalogu pojawi się plik z danymi od innego systemu. Warunek sprawdzał zmienną `gotowe`, ale nigdzie w ciel
  - [dowcipy] Pusta lista to torba przed sklepem: Pusta lista `[]` to torba na zakupy przed wejściem do sklepu: już istnieje, ale nic w niej nie ma. `len()` odpowie uczciwie: 0.
  - [wtręty] Marta prosi o czwartego, którego nie ma: Marta miała listę czterech współlokatorów i chciała pokazać ostatniego, więc napisała `osoby[4]`, bo liczyła po ludzku: pierwszy, drugi, trzeci, czwarty. Progra
  - [dowcipy] Lista obecności bez wołania w próżnię: Pętla `for` działa jak nauczyciel z dziennikiem: woła każdego z listy po kolei i na ostatnim nazwisku kończy. Nie stoi potem w drzwiach z pytaniem „a nie ma tu 

DODATKI:
0. [wtręty] Marta opisuje funkcję i czeka na wynik: Marta napisała w `kasa.py` `def suma(wydatki):` z całą pętlą w środku, zapisała plik i uruchomiła go. Ekran pozostał pusty, bez wyniku i bez błędu. Uznała, że coś zepsuła, a program po prostu nigdy nie dostał polecenia, by tę funkcję uruchomić. Dopiero linia `print(suma([45.5, 20, 12.5]))` pod definicją wypisała `78.0`.
1. [dykteryjki] Poprawka w trzech miejscach z czterech: W skrypcie do porządkowania danych klientów ta sama pięciolinijkowa logika czyszczenia numeru telefonu była wklejona w czterech miejscach. Gdy trzeba było obsłużyć numery z prefiksem kraju, poprawiłem trzy kopie, a czwartą pominąłem. Część rekordów trafiała do bazy w innym formacie i wychodziło to dopiero przy późniejszych porównaniach. Przeniosłem tę logikę do jednej funkcji i od tamtej pory poprawiam ją w jednym miejscu.

SEKCJA "Czym jest funkcja":
[[funkcja|Funkcja]] to nazwany kawałek kodu, który raz opisujesz, a potem uruchamiasz, kiedy zechcesz, wpisując jego nazwę. Znasz już gotowe funkcje: `print()` i `str()` napisali twórcy Pythona.

Własną funkcję zaczynasz od `def`, nazwy, nawiasów i dwukropka. Wcięty blok pod spodem to jej treść. Ten zapis to [[definicja-funkcji|definicja funkcji]]: tylko opisuje, co funkcja robi, i niczego jeszcze nie wykonuje. Dopiero [[wywolanie-funkcji|wywołanie]], czyli nazwa z nawiasami, uruchamia treść.

Weźmy pętlę zbierającą sumę, taką jak w sekcji o pętli po elementach listy. Zamieniamy ją w osobną funkcję, czyli robimy to, co zapowiadaliśmy: taką część programu wydzielamy w osobny kawałek:

```python
def suma(wydatki):
    razem = 0
    for kwota in wydatki:
        razem = razem + kwota
    return razem

print(suma([45.5, 20, 12.5]))
```

```text
78.0
```

Nawias po nazwie przyjmuje dane, na których funkcja pracuje (`wydatki`), a `return` oddaje wynik. Oba mechanizmy omówimy osobno w kolejnych sekcjach; na razie wystarczy, że dane wchodzą, a wynik wychodzi.

Konsekwencja: kod, który był kawałkiem długiego programu, ma teraz nazwę i można go wywołać w wielu miejscach, bez kopiowania.
````

## Odpowiedź

````json
{
  "verdicts": [
    {
      "index": 0,
      "ok": false,
      "problem": "Powtarza motyw wcześniejszego wpisu „Marta czeka, aż plik sam zadziała”: zapisany plik, pusty ekran bez błędu, Marta uznaje, że coś zepsuła."
    },
    {
      "index": 1,
      "ok": false,
      "problem": "Powtarza motyw wpisu „Marta wpisuje kwotę w pięciu miejscach”: ta sama rzecz skopiowana w kilku miejscach, poprawka pominięta w jednej kopii."
    }
  ]
}
````
