# Krok 0370 · weryfikator_dodatków

Węzeł: `layers` · dział: 4 · pytanie: 21 · próba: —

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
  - [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech mie
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
  - [wtręty] Marta wpisuje kwotę w pięciu miejscach: Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech mie

DODATKI:
0. [dykteryjki] Zmienna o nazwie x: W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamówienie trafia do ręcznej weryfikacji, i przez pół dnia ustalałem, która z nich go przechowuje. Dopiero prześledzenie każdego użycia pokazało, że to `x2`, a `tmp` trzyma coś zupełnie innego. Zmieniłem nazwy na `prog_weryfikacji` i `liczba_zamowien`, a kolejna zmiana progu zajęła kilka minut. Od tamtej pory nazywam zmienne tak, żeby etykieta mówiła, co leży w środku.
1. [rysunki] Dwa pudełka, dwie etykiety: Jasny pokój z drewnianą półką. Na półce stoją obok siebie dwa kartonowe pudełka z doczepionymi papierowymi etykietami (puste kartki, bez tekstu). Uśmiechnięta osoba o prostych kształtach wkłada do pierwszego pudełka nową koralową kartkę, a stara musztardowa kartka wypada z niego i leży obok. Drugie pudełko stoi spokojnie i widać w nim wystającą musztardową kartkę, identyczną jak ta, która wypadła: to kopia, której zmiana w pierwszym pudełku nie dotknęła.

SEKCJA "Zmienna jako pudełko z etykietą":
[[zmienna|Zmienną]] można porównać do pudełka z etykietą: etykieta to nazwa, a w środku leży jedna [[dana|dana]], czyli [[wartosc-zmiennej|wartość zmiennej]] (to, co aktualnie jest w pudełku). Program szuka pudełka po etykiecie i zagląda do środka.

```text
etykieta: kwota      etykieta: imie
┌──────────┐         ┌──────────┐
│   45.5   │         │  "Ania"  │
└──────────┘         └──────────┘
```

Porównanie tłumaczy trzy rzeczy. Pudełko mieści jedną wartość naraz, więc nowa wartość wypiera starą, jak w przypadku zmiany kwoty z poprzedniej sekcji. Etykieta zostaje, zmienia się tylko zawartość. Wreszcie każde pudełko żyje własnym życiem: kopia wartości do drugiego pudełka nie łączy ich na stałe.

```python
# poza kanonem
kwota_stara = 45.5
kwota = kwota_stara
kwota = 60
print(kwota_stara, kwota)
```

```text
45.5 60
```

Zmiana `kwota` nie ruszyła `kwota_stara`, bo do drugiego pudełka trafiła kopia wartości.

Obraz jest uproszczony: pod spodem Python działa nieco inaczej, ale na tym etapie to nie ma znaczenia. Ważna konsekwencja: etykieta ma być czytelna. W „Wspólnej Kasie” pudełko `kwota` jest zrozumiałe, a `x` zmusza do zgadywania, co w środku.
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
      "ok": true
    }
  ]
}
````
