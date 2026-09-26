# Krok 0356 · weryfikator_dodatków

Węzeł: `layers` · dział: 4 · pytanie: 20 · próba: —

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
  - [dowcipy] Program bez danych jak kuchnia bez produktów: Program bez danych to kucharz bez produktów: piec rozgrzany, fartuch wyprasowany, a obiadu i tak nie będzie.

DODATKI:
0. [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech miejscach i przeoczyła piąte. Komputer nie zgłosił błędu, tylko wykonał wszystko dokładnie: cztery obliczenia zgodne z paragonem i jedno nie. Gdyby kwota siedziała w zmiennej `kwota`, wystarczyłaby jedna poprawka.
1. [rysunki] Pudełko z etykietą zamiast liczby: Jasny pokój. Uśmiechnięta osoba stoi przy półce z kilkoma drewnianymi pudełkami, każde ma przyczepioną pustą papierową etykietę. Z jednego pudełka wyjmuje starą kartkę z liczbą i wkłada nową, a stara kartka leci do kosza obok. Na stole leży otwarty notes ze strzałkami od etykiet do pudełek.

SEKCJA "Czym jest zmienna":
[[zmienna|Zmienna]] to nazwane miejsce w pamięci programu, w którym leży jedna [[dana|dana]]. Dzięki nazwie możesz tę daną wielokrotnie odczytać, użyć w obliczeniach albo zastąpić inną.

Pamiętasz, że dane trzeba gdzieś przechowywać, żeby użyć ich więcej niż raz. Właśnie do tego służy zmienna. Zamiast wpisywać `45.5` w kilku miejscach, nadajesz kwocie nazwę i posługujesz się nią. To trochę jak komórka w arkuszu, którą nazwałeś „kwota”, a potem odwołujesz się do niej po nazwie.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(imie, kwota, zaplacono)
kwota = 60
print(kwota + 10)
```

```text
Ania 45.5 True
70
```

Znak `=` nie oznacza tu „równa się” jak w matematyce. Znaczy: „zapisz to, co po prawej, pod nazwą po lewej”. Dokładniej opiszemy to przy przypisaniu.

Wartość zmiennej może się zmieniać w trakcie działania programu, stąd nazwa: po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce. Nazwa zostaje ta sama. W „Wspólnej Kasie” takie zmienne w `rozlicz.py` opisują pojedynczy wydatek: kto zapłacił, ile i czy już się rozliczył.
````

## Odpowiedź

````json
{
  "verdicts": [
    {
      "index": 0,
      "ok": true
    },
    {
      "index": 1,
      "ok": false,
      "problem": "Etykiety są „puste”, a zmienna to miejsce z nazwą, więc rysunek przeczy sekcji (nazwa jest jej sednem) i własnemu tytułowi „pudełko z etykietą”."
    }
  ]
}
````
