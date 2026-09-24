# Modelowanie wspólne

Knowledge crunching z rozdziału 02 można prowadzić w rozmowach jeden na jeden, ale w dużej domenie to za wolno i za wąsko. Każdy ekspert zna tylko swój fragment, a najciekawsze problemy leżą na styku działów. Warsztaty modelowania zbierają wszystkich w jednym miejscu i pozwalają zbudować wspólny obraz w ciągu godzin, a nie tygodni. Ten rozdział opisuje dwie najpopularniejsze techniki i drogę od karteczek do kodu.

```text
warsztat                         wynik                               kod
Big Picture Event Storming  ──►  zdarzenia, zdarzenia przełomowe  ──► mapa kontekstów
Process Level               ──►  komendy, polityki, read modele   ──► przepływy, sagi
Design Level                ──►  agregaty, niezmienniki           ──► klasy domeny, testy
Domain Storytelling         ──►  historie z aktorami i obiektami  ──► język, scenariusze
```

## Karteczki na długiej ścianie

<a id="term-event-storming"></a>[Event Storming](00%20Glossary%20DDD.md#event-storming) to technika warsztatowa opracowana przez Alberta Brandoliniego. Uczestnicy, czyli eksperci z różnych działów, programiści, product owner i osoby z operacji, przyklejają na długiej ścianie karteczki ze zdarzeniami domenowymi w czasie przeszłym: „Rezerwacja potwierdzona”, „Auto wydane”, „Szkoda zgłoszona”. Potem układają je chronologicznie i uzupełniają o kolejne elementy, w tym <a id="term-hotspot"></a>[hotspoty](00%20Glossary%20DDD.md#hotspot), czyli miejsca problemów i niejasności.

Typowe elementy i ich umowne kolory (w różnych zespołach konwencje się różnią):

| Element | Kolor (typowo) | Przykład |
|---|---|---|
| Zdarzenie domenowe | pomarańczowy | „Auto zwrócone” |
| Komenda | niebieski | „Zwróć auto” |
| Aktor | mały żółty | „Pracownik oddziału” |
| Agregat / system decyzyjny | duży żółty | „Umowa najmu” |
| Polityka (reguła „kiedy X, to Y”) | fioletowy | „Gdy auto zwrócone z uszkodzeniem, zgłoś szkodę” |
| Model odczytu | zielony | „Lista aut do wydania dziś” |
| System zewnętrzny | różowy | „Bramka płatności” |
| Hotspot | czerwony lub jaskrawy | „Kto płaci za paliwo przy zwrocie w innym oddziale?” |

Hotspot oznacza problem, pytanie, konflikt albo niejasność. Hotspoty są najcenniejszym wynikiem warsztatu, bo pokazują, gdzie eksperci się nie zgadzają albo gdzie proces jest niejasny. Tam zwykle kryją się ukryte pojęcia i najważniejsze decyzje modelowe.

## Trzy poziomy

Brandolini opisuje trzy poziomy Event Stormingu, różniące się celem, uczestnikami i szczegółowością.

<a id="term-big-picture"></a>[Big Picture](00%20Glossary%20DDD.md#big-picture) obejmuje całą domenę albo duży jej fragment. Uczestniczą wszyscy, którzy coś wiedzą o procesie: od recepcji w oddziale po zarząd. Zdarzenia układa się w oś czasu, a potem szuka się zdarzeń przełomowych i hotspotów. Cel to wspólne zrozumienie całości, znalezienie granic kontekstów i miejsc, w których biznes najbardziej cierpi. Warsztat trwa od kilku godzin do dwóch dni.

Process Level skupia się na jednym procesie, np. „od rezerwacji do wydania auta”. Do zdarzeń dochodzą komendy, aktorzy, polityki, modele odczytu i systemy zewnętrzne. Powstaje gramatyka procesu:

```text
Aktor ──► Komenda ──► System ──► Zdarzenie ──► Polityka ──► Komenda ──► ...
                                     │
                                     └──► Model odczytu ──► Aktor (decyzja)

Pracownik ──► „Zwróć auto” ──► Umowa najmu ──► „Auto zwrócone”
                                                  │
                                                  ├──► Polityka „jeśli uszkodzenie, zgłoś szkodę” ──► „Zgłoś szkodę”
                                                  └──► Polityka „rozlicz najem” ──► „Wystaw fakturę”
```

<a id="term-design-level"></a>[Design Level](00%20Glossary%20DDD.md#design-level) to poziom projektowy, na którym przy procesie pracuje zespół programistów z ekspertem. Komendy i zdarzenia grupuje się wokół agregatów, a przy każdym agregacie spisuje się niezmienniki, czyli reguły, które musi pilnować. Wynik da się niemal bezpośrednio przełożyć na kod.

| Poziom | Uczestnicy | Pytanie | Wynik |
|---|---|---|---|
| Big Picture | wszyscy interesariusze | jak działa cały biznes? | oś zdarzeń, zdarzenia przełomowe, hotspoty, kandydaci na konteksty |
| Process Level | eksperci procesu, zespół, PO | jak działa ten proces? | komendy, polityki, modele odczytu, aktorzy |
| Design Level | zespół i ekspert | jak to zbudować? | agregaty, niezmienniki, granice transakcji |

## Historie zamiast osi czasu

<a id="term-domain-storytelling"></a>[Domain Storytelling](00%20Glossary%20DDD.md#domain-storytelling) to technika opisana przez Stefana Hofera i Henninga Schwentnera. Ekspert opowiada konkretną historię, a moderator na bieżąco rysuje ją prostym językiem obrazkowym: aktorzy (osoby, systemy), obiekty pracy (dokumenty, auta, formularze) i czynności, połączone ponumerowanymi strzałkami. Każde zdanie historii ma postać „kto robi co z czym”.

```text
(1) Klient ──► przekazuje ──► [kluczyki] ──► Pracownik oddziału
(2) Pracownik oddziału ──► sprawdza ──► [auto] ──► z [protokołem wydania]
(3) Pracownik oddziału ──► zaznacza ──► [uszkodzenie zderzaka] ──► w [protokole zwrotu]
(4) Pracownik oddziału ──► przekazuje ──► [protokół zwrotu] ──► Likwidatorowi szkód
(5) Likwidator ──► wycenia ──► [szkodę] ──► w [systemie szkód]
```

| | Event Storming | Domain Storytelling |
|---|---|---|
| Punkt wyjścia | zdarzenia, oś czasu | konkretna historia jednego scenariusza |
| Najlepszy do | szerokiego obrazu, wielu działów naraz, szukania granic | poznania jednego procesu, języka i obiektów pracy |
| Grupa | duża, do kilkudziesięciu osób | mała, jeden lub dwóch ekspertów |
| Mocna strona | hotspoty i konflikty między działami | naturalny język eksperta, łatwy start |
| Słabość | chaos na początku, wymaga doświadczonego moderatora | jedna historia naraz, trudniej zobaczyć całość |

Domain Storytelling sprawdza się lepiej, gdy ekspert ma trudność z abstrakcyjnym myśleniem o zdarzeniach, gdy trzeba szybko poznać język jednego procesu albo gdy liczy się porównanie stanu obecnego z docelowym, czyli dwie wersje tej samej historii. Obie techniki dobrze się uzupełniają: Big Picture pokazuje całość, a Domain Storytelling pozwala zejść w głąb wybranego procesu.

## Od karteczek do kodu

Wynik warsztatu nie jest projektem, tylko materiałem do projektowania. Droga do kodu zwykle wygląda tak:

1. Zdarzenia przełomowe i zmiany języka na osi Big Picture wyznaczają kandydatów na bounded contexty (rozdział 04). Grupy zdarzeń opisujące jeden etap i jeden język zakreśla się na ścianie jako obszary.
2. Hotspoty stają się listą pytań do ekspertów i decyzji do podjęcia. Hotspot, którego nikt nie potrafi rozwiązać, często wskazuje core domain.
3. Na Process Level komendy i zdarzenia jednego kontekstu stają się jego API: komendy to operacje, zdarzenia to publikowane fakty, polityki to handlery zdarzeń albo process managery.
4. Na Design Level grupy komend i zdarzeń wokół tego samego „dużego żółtego” stają się agregatami. Reguły wypisane przy agregacie stają się niezmiennikami i testami.
5. Modele odczytu z karteczek stają się read modelami i zapytaniami, co opisuje tutorial [cqrs](../CQRS/).

```python
# z karteczek Design Level: agregat „Umowa najmu”
# komendy: Zwróć auto, Przedłuż najem     zdarzenia: Auto zwrócone, Najem przedłużony
# niezmienniki: nie można przedłużyć zwróconej umowy; przedłużenie tylko, gdy auto wolne w nowym terminie
class RentalAgreement:
    def return_vehicle(self, at: BranchId, fuel: FuelLevel, mileage: int, damages: list[Damage]) -> None: ...
    def extend(self, new_return_date: datetime, availability: VehicleAvailability) -> None: ...


# polityka „Gdy auto zwrócone z uszkodzeniem, zgłoś szkodę”
class ReportDamageOnReturn:
    def handle(self, event: VehicleReturned) -> None:
        if event.damages:
            self._claims.open_claim(OpenClaim(event.agreement_id, event.damages))
```

Warsztat warto powtarzać. Pierwszy Big Picture pokazuje stan wiedzy na początku projektu, a kolejne pokazują, jak zmieniło się zrozumienie domeny. Zdjęcia ściany i lista hotspotów to cenna dokumentacja decyzji.

## Co zapamiętać

- Event Storming to warsztat Alberta Brandoliniego oparty na zdarzeniach domenowych na osi czasu.
- Hotspoty wskazują konflikty i niejasności, czyli miejsca najważniejszych decyzji modelowych.
- Big Picture szuka granic i problemów w całej domenie, Process Level opisuje gramatykę procesu, a Design Level wyznacza agregaty i niezmienniki.
- Domain Storytelling to historie ekspertów rysowane językiem obrazkowym, dobre do poznania jednego procesu i jego języka.
- Obie techniki się uzupełniają: szeroki obraz i zejście w głąb.
- Wyniki warsztatu przekładają się na konteksty, API kontekstu, polityki, agregaty, niezmienniki i modele odczytu.

## Pytania sprawdzające

### 27. Czym jest Event Storming i czym różnią się jego poziomy (Big Picture, Process Level, Design Level)?

<details>
<summary>Odpowiedź</summary>

To warsztat Alberta Brandoliniego, na którym uczestnicy z różnych działów układają na ścianie zdarzenia domenowe w czasie przeszłym i uzupełniają je o komendy, aktorów, polityki, modele odczytu, systemy zewnętrzne i hotspoty. Big Picture obejmuje całą domenę ze wszystkimi interesariuszami i daje oś zdarzeń, zdarzenia przełomowe, hotspoty i kandydatów na konteksty. Process Level opisuje jeden proces jego gramatyką: aktor, komenda, system, zdarzenie, polityka. Design Level to praca zespołu z ekspertem nad agregatami i niezmiennikami.

Zobacz: sekcje „Karteczki na długiej ścianie” i „Trzy poziomy”.

</details>

### 28. Czym jest Domain Storytelling i kiedy sprawdza się lepiej niż Event Storming?

<details>
<summary>Odpowiedź</summary>

To technika Hofera i Schwentnera, w której ekspert opowiada konkretną historię, a moderator rysuje ją językiem obrazkowym: aktorzy, obiekty pracy, czynności i ponumerowane zdania „kto robi co z czym”. Sprawdza się lepiej w małej grupie, przy poznawaniu jednego procesu i jego języka, gdy ekspertowi trudno myśleć abstrakcyjnymi zdarzeniami, albo przy porównaniu stanu obecnego z docelowym. Event Storming lepiej pokazuje całość i konflikty między działami, więc techniki się uzupełniają.

Zobacz: sekcja „Historie zamiast osi czasu”.

</details>

### 29. Jak przejść od wyników warsztatu (zdarzenia, komendy, polityki, hotspoty) do bounded contextów i agregatów?

<details>
<summary>Odpowiedź</summary>

Zdarzenia przełomowe i zmiany języka wyznaczają kandydatów na konteksty. Hotspoty stają się listą decyzji, a nierozwiązywalne często wskazują core domain. Komendy i zdarzenia kontekstu stają się jego API, a polityki handlerami zdarzeń lub process managerami. Grupy komend i zdarzeń wokół tego samego „dużego żółtego” stają się agregatami, a spisane przy nich reguły niezmiennikami i testami. Modele odczytu stają się read modelami. Warsztaty się powtarza, a zdjęcia ściany i hotspoty dokumentują decyzje.

Zobacz: sekcja „Od karteczek do kodu”.

</details>
