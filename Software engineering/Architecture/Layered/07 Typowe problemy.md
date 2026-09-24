# Typowe problemy

Architektura warstwowa działa dobrze, dopóki logika jest prosta. Gdy system rośnie, pojawia się kilka powtarzalnych problemów. Nie wynikają z błędów zespołu, tylko z tego, jak ta architektura rozkłada zależności i zachęca do określonych wyborów. Ten rozdział opisuje cztery najczęstsze problemy i pokazuje, jak ocenić, czy dany problem już jest poważny.

```text
problem                          objaw
anemiczny model                  encje z samymi polami, serwisy po 2000 linii
sinkhole                         żądanie przechodzi przez 4 warstwy, żadna nic nie robi
logika w bazie                   reguły w procedurach i triggerach, niewidoczne w kodzie
kosztowna wymiana technologii    zmiana ORM-a dotyka logiki biznesowej
```

## Encje bez zachowań

<a id="term-anemic-domain-model"></a>[Anemiczny model domeny](00%20Glossary%20Layered.md#anemic-domain-model) to termin Martina Fowlera na model, w którym obiekty biznesowe mają tylko dane, a cała logika jest w serwisach. Wygląda jak model obiektowy, ale działa jak procedury operujące na strukturach danych.

```python
# encja: tylko pola
class Appointment(models.Model):
    patient = models.ForeignKey(Patient, on_delete=models.PROTECT)
    doctor = models.ForeignKey(Doctor, on_delete=models.PROTECT)
    starts_at = models.DateTimeField()
    status = models.CharField(max_length=20)


# serwisy: cała logika, powtarzana w wielu miejscach
class AppointmentService:
    def cancel(self, appointment_id):
        a = Appointment.objects.get(id=appointment_id)
        if a.status != "booked": raise InvalidState()
        if a.starts_at - now() < timedelta(hours=24): raise TooLateToCancel()
        a.status = "cancelled"
        a.save()


class RescheduleService:
    def reschedule(self, appointment_id, new_time):
        a = Appointment.objects.get(id=appointment_id)
        if a.status != "booked": raise InvalidState()                   # ta sama reguła
        if a.starts_at - now() < timedelta(hours=24): raise TooLate()  # ta sama reguła, inny wyjątek
        ...
```

Dlaczego architektura warstwowa sprzyja anemii:

- podział „dane w warstwie dostępu do danych, logika w warstwie logiki” sugeruje, że obiekty z bazy mają być tylko danymi,
- modele ORM są generowane z tabel albo pisane jako odbicie tabel, więc od początku są strukturami danych,
- warstwa serwisów jest naturalnym miejscem na każdy nowy kod, bo tam przychodzi wywołanie z kontrolera,
- transaction script z rozdziału 02 jest najprostszym sposobem pisania logiki i w małej skali działa bez zarzutu.

Objawy, że anemia stała się problemem: te same warunki powtarzają się w kilku serwisach, serwisy mają tysiące linii, status i inne pola są ustawiane bezpośrednio z wielu miejsc, a zmiana reguły wymaga szukania wszystkich jej kopii. Naprawa polega na przenoszeniu reguł do obiektów, których dotyczą: `appointment.cancel(now)` zamiast warunków w serwisie. Anemia nie jest błędem, gdy logika jest naprawdę prosta. Wtedy transaction script jest uczciwym wyborem.

## Warstwy, które niczego nie robią

<a id="term-sinkhole-anti-pattern"></a>[Sinkhole anti-pattern](00%20Glossary%20Layered.md#sinkhole-anti-pattern) opisał Mark Richards w „Software Architecture Patterns”. Żądania przechodzą przez kolejne warstwy, a żadna z nich nie wykonuje żadnej logiki, tylko przekazuje wywołanie dalej:

```python
# widok
def doctor_detail(request, doctor_id):
    return JsonResponse(asdict(doctor_service.get(doctor_id)))

# serwis
class DoctorService:
    def get(self, doctor_id): return self._logic.get(doctor_id)

# logika
class DoctorLogic:
    def get(self, doctor_id): return self._repo.get(doctor_id)

# repozytorium
class DoctorRepository:
    def get(self, doctor_id): return Doctor.objects.get(id=doctor_id)
```

Część takich żądań jest normalna. Proste odczyty naturalnie nie mają logiki. Richards proponuje regułę 80–20: jeśli około 20 procent żądań to proste przejścia przez warstwy, to akceptowalne. Jeśli jest ich 80 procent, architektura warstwowa jest dla tej aplikacji złym wyborem albo warstwy są zbyt ściśle zamknięte.

Jak ocenić, czy sinkhole jest problemem:

- policz, ile metod serwisów i warstwy logiki tylko przekazuje wywołanie z tymi samymi argumentami,
- sprawdź, ile plików trzeba zmienić, żeby dodać jedno pole do odpowiedzi API. Jeśli cztery lub więcej, a żaden nie ma logiki, warstwy są ceremonią,
- zobacz, czy zespół zaczął omijać warstwy „na skróty”. To sygnał, że nie przynoszą wartości.

Rozwiązania: otworzyć warstwy dla prostych odczytów (rozdział 03), czyli pozwolić widokowi albo selektorowi odczytu pobierać dane bezpośrednio, połączyć puste warstwy (np. warstwę logiki z serwisami, gdy logika jest w transaction scripts) albo rozważyć podział według funkcji z rozdziału 08.

## Logika w bazie danych

W wielu systemach, zwłaszcza starszych, część logiki biznesowej jest w bazie: <a id="term-stored-procedure"></a>[procedury składowane](00%20Glossary%20Layered.md#stored-procedure), triggery, widoki z warunkami, ograniczenia `CHECK`. Czasem trafia też do zapytań SQL w warstwie dostępu do danych, np. `WHERE status = 'booked' AND starts_at > now() + interval '24 hours'` jako reguła „wizyty, które można odwołać”.

Skutki:

- reguły są niewidoczne dla programistów aplikacji. Ktoś zmienia warunek w serwisie, a trigger w bazie i tak robi co innego,
- reguła istnieje w dwóch miejscach, w kodzie i w bazie, i z czasem te miejsca się rozjeżdżają,
- testowanie wymaga bazy z pełnym schematem, procedurami i danymi,
- wersjonowanie i wdrażanie procedur jest trudniejsze niż kodu, a przegląd zmian w SQL-u rzadziej odbywa się w code review,
- aplikacja jest związana z jednym silnikiem bazy, bo PL/pgSQL, T-SQL i PL/SQL nie są przenośne,
- trudno skalować, bo cała logika obciąża jedną bazę.

Kiedy logika w bazie bywa uzasadniona:

- operacje na dużych zbiorach danych, gdzie przesłanie ich do aplikacji jest zbyt kosztowne: rozliczenia miesięczne, agregacje, migracje,
- gwarancje spójności, których nie da się bezpiecznie zapewnić w aplikacji: unikalność, klucze obce, ograniczenia wykluczające nakładanie się przedziałów (`EXCLUDE USING gist` w PostgreSQL, np. dla wizyt jednego lekarza),
- baza jest współdzielona przez wiele aplikacji, a reguła musi obowiązywać wszystkie. To raczej objaw innego problemu, ale czasem jest faktem,
- zespół i organizacja mają silne kompetencje bazodanowe, a reguły są stabilne.

Rozsądna zasada: reguły biznesowe w kodzie aplikacji, gwarancje spójności danych w bazie jako ostatnia linia obrony. Ograniczenie `EXCLUDE` na nakładających się wizytach jest dobrym uzupełnieniem sprawdzenia w logice, a nie jego zastępstwem.

## Dlaczego wymiana technologii boli

Jednym z obiecywanych zalet warstw była możliwość wymiany bazy danych albo frameworka przez wymianę jednej warstwy. W praktyce rzadko się to udaje. Powody:

- warstwa logiki zależy od warstwy dostępu do danych, więc zna jej typy: modele ORM, QuerySety, sesje, wyjątki bazy,
- modele ORM są jednocześnie modelem biznesowym (Active Record), więc wymiana ORM-a oznacza przepisanie klas biznesowych,
- zapytania wyciekają do warstw wyższych: `Appointment.objects.filter(...)` w serwisach, a nawet w widokach,
- logika bywa w bazie, więc wymiana silnika wymaga przepisania procedur,
- framework przenika wszystkie warstwy: formularze Django w serwisach, sygnały w modelach, `@Transactional` i adnotacje JPA w logice.

<a id="term-leaky-abstraction"></a>[Dziurawa abstrakcja](00%20Glossary%20Layered.md#leaky-abstraction) (leaky abstraction, termin Joela Spolsky'ego) dobrze opisuje ten stan: warstwa dostępu do danych miała ukrywać bazę, ale jej szczegóły przeciekają w górę przez typy, wyjątki, lazy loading i założenia o wydajności.

Główna przyczyna jest strukturalna: w architekturze warstwowej to logika zależy od dostępu do danych, a nie odwrotnie. Nawet idealnie utrzymane warstwy nie pozwolą wymienić bazy bez dotykania logiki, jeśli logika importuje typy tej warstwy. Rozdział 08 pokazuje, jak architektury z odwróconą zależnością rozwiązują dokładnie ten problem.

W praktyce wymiana bazy zdarza się rzadko, więc sam ten argument rzadko uzasadnia zmianę architektury. Te same przyczyny powodują jednak problemy, które zdarzają się codziennie: wolne testy, kruche zmiany i logikę rozsianą po warstwach.

## Co zapamiętać

- Architektura warstwowa sprzyja anemicznemu modelowi, bo oddziela dane od logiki. Problem pojawia się, gdy reguły się powtarzają.
- Sinkhole anti-pattern to żądania przechodzące przez warstwy bez logiki. Reguła 80–20 pomaga ocenić skalę.
- Logika w procedurach i triggerach jest niewidoczna, trudna do testowania i wiąże z silnikiem bazy. Baza powinna gwarantować spójność danych, a nie zawierać reguł biznesowych.
- Wymiana technologii boli, bo logika zależy od typów warstwy danych, a model ORM jest modelem biznesowym.
- Dziurawa abstrakcja: szczegóły bazy przeciekają w górę przez typy, wyjątki i lazy loading.
- Przyczyna jest strukturalna: kierunek zależności od logiki do danych.

## Pytania sprawdzające

### 19. Czym jest anemiczny model domeny w aplikacji warstwowej i dlaczego ten układ go promuje?

<details>
<summary>Odpowiedź</summary>

To model (termin Fowlera), w którym obiekty biznesowe mają tylko dane, a logika jest w serwisach. Architektura warstwowa go promuje, bo podział „dane niżej, logika wyżej” sugeruje, że obiekty z bazy to tylko dane, modele ORM są odbiciem tabel, serwisy są naturalnym miejscem na nowy kod, a transaction script jest najprostszy. Problem pojawia się, gdy te same reguły powtarzają się w wielu serwisach, a pola są ustawiane z wielu miejsc. Naprawa: reguły w obiektach, których dotyczą. Przy prostej logice anemia jest akceptowalna.

Zobacz: sekcja „Encje bez zachowań”.

</details>

### 20. Czym jest sinkhole anti-pattern (żądania przechodzące przez warstwy bez żadnej logiki) i jak ocenić, czy stał się problemem?

<details>
<summary>Odpowiedź</summary>

To opisany przez Marka Richardsa przypadek, w którym żądanie przechodzi przez kolejne warstwy, a każda tylko przekazuje wywołanie. Reguła 80–20: około 20 procent takich żądań jest normalne, a 80 procent oznacza złą architekturę lub zbyt zamknięte warstwy. Ocena: ile metod tylko przekazuje wywołanie, ile plików bez logiki trzeba zmienić, żeby dodać pole, i czy zespół zaczął omijać warstwy. Rozwiązania: otwarte warstwy dla prostych odczytów, połączenie pustych warstw albo podział według funkcji.

Zobacz: sekcja „Warstwy, które niczego nie robią”.

</details>

### 21. Co się dzieje, gdy logika biznesowa trafia do procedur składowanych, triggerów albo zapytań SQL? Kiedy bywa to uzasadnione?

<details>
<summary>Odpowiedź</summary>

Reguły stają się niewidoczne dla programistów aplikacji i istnieją w dwóch miejscach, które się rozjeżdżają. Testy wymagają pełnej bazy, wersjonowanie i przegląd zmian są trudniejsze, aplikacja jest związana z silnikiem bazy, a skalowanie obciąża jedną bazę. Uzasadnione przy operacjach na dużych zbiorach (rozliczenia, agregacje), gwarancjach spójności (unikalność, klucze obce, `EXCLUDE` dla nakładających się przedziałów), bazie współdzielonej przez wiele aplikacji oraz silnych kompetencjach bazodanowych i stabilnych regułach. Zasada: reguły w kodzie, a baza jako ostatnia linia obrony spójności.

Zobacz: sekcja „Logika w bazie danych”.

</details>

### 22. Dlaczego zmiana bazy danych albo frameworka w aplikacji warstwowej jest tak kosztowna, skoro warstwy miały to ułatwić?

<details>
<summary>Odpowiedź</summary>

Bo logika zależy od warstwy dostępu do danych i zna jej typy (modele ORM, QuerySety, sesje, wyjątki), model ORM jest jednocześnie modelem biznesowym, zapytania wyciekają do serwisów i widoków, część logiki bywa w bazie, a framework przenika wszystkie warstwy. To dziurawa abstrakcja: szczegóły bazy przeciekają w górę. Przyczyna jest strukturalna, bo zależność biegnie od logiki do danych, i rozwiązują ją architektury z odwróconą zależnością. Wymiana bazy jest rzadka, ale te same przyczyny powodują codzienne problemy: wolne testy i kruche zmiany.

Zobacz: sekcja „Dlaczego wymiana technologii boli”.

</details>
