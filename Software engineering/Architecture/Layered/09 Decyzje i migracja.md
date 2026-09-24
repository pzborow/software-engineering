# Decyzje i migracja

Architektura warstwowa nie jest ani dobra, ani zła sama w sobie. Jest świadomym wyborem dla pewnej klasy aplikacji i ograniczeniem dla innej. Ten rozdział pomaga ocenić, w której sytuacji jest dany system, pokazuje, jak stopniowo przejść na architekturę z odwróconą zależnością, i jak utrzymać czytelność dużej aplikacji warstwowej bez zmiany jej charakteru.

```text
decyzja                                   droga
aplikacja prosta, logika cienka      ──►  zostań przy warstwach, pilnuj granic
logika rośnie w jednym obszarze      ──►  odwróć zależność tylko tam (hexagonal w module)
aplikacja duża, trudno ją ogarnąć    ──►  podziel na moduły według funkcji, warstwy w środku
```

## Świadomy wybór czy ograniczenie

Architektura warstwowa jest dobrym wyborem, gdy:

- większość operacji to CRUD: formularz, walidacja, zapis, lista,
- reguły biznesowe są proste i stabilne, a raporty i ekrany odzwierciedlają strukturę danych,
- zespół jest mały albo zmienny i liczy się szybki onboarding,
- aplikacja jest wewnętrznym narzędziem, panelem administracyjnym albo prototypem, który ma szybko dowieść wartości,
- framework (Django, Rails) daje dużo gotowych elementów, które zakładają ten układ: panel administracyjny, formularze, serializery.

Staje się ograniczeniem, gdy pojawiają się objawy z rozdziałów 06 i 07:

| Objaw | Co oznacza |
|---|---|
| testy reguł trwają minuty, bo wszystkie wymagają bazy | logika jest związana z dostępem do danych |
| te same warunki w wielu serwisach, serwisy po tysiące linii | model jest anemiczny, a reguły nie mają domu |
| zmiana jednej funkcji dotyka widoków, serwisów, logiki i repozytoriów, a większość z nich tylko przekazuje wywołania | sinkhole, warstwy są ceremonią |
| zmiana biblioteki lub bazy wymaga zmian w logice | dziurawa abstrakcja warstwy danych |
| kilka zespołów wchodzi sobie w drogę w tych samych serwisach | warstwy nie dzielą systemu według obszarów odpowiedzialności |

Zwykle objawy nie dotyczą całej aplikacji, tylko jednego lub dwóch obszarów, w których rośnie złożoność. W wypadku przychodni może to być rejestracja wizyt z coraz bogatszymi regułami (grafiki, limity, priorytety, wizyty cykliczne), podczas gdy słowniki, rozliczenia i raporty pozostają proste. Decyzja nie musi więc dotyczyć całego systemu.

## Stopniowe przejście

Przepisanie aplikacji na nową architekturę zwykle kończy się miesiącami pracy bez nowej wartości. Bezpieczniej jest przechodzić stopniowo, obszar po obszarze, według wzorca <a id="term-strangler-fig"></a>[strangler fig](00%20Glossary%20Layered.md#strangler-fig) Martina Fowlera: nowa struktura otacza starą i przejmuje jej funkcje, aż starą można usunąć.

Kolejne kroki dla jednego obszaru, np. rejestracji wizyt:

```text
krok 1  testy integracyjne     zamroź zachowanie przypadków użycia testami przez serwis z bazą
krok 2  serwisy jako wejście   cała logika rejestracji przechodzi przez serwisy, widoki są cienkie
krok 3  czysta logika          reguły wydzielone do klas i funkcji bez ORM-a (rozdział 06)
krok 4  interfejsy w logice    logika definiuje Appointments, Schedules jako Protocol
krok 5  adaptery               istniejące repozytoria implementują te interfejsy
krok 6  wstrzykiwanie          serwisy dostają repozytoria przez konstruktor, a nie tworzą ich same
krok 7  testy z fake'ami       reguły i przypadki użycia testowane bez bazy
krok 8  model niezależny od ORM (opcjonalnie)  encje domeny oddzielone od modeli Django
```

Kroki 4–6 to właściwe odwrócenie zależności. Nie wymagają przepisywania logiki. Istniejące repozytorium zaczyna spełniać interfejs zdefiniowany wyżej, a serwis zamiast `AppointmentRepository()` dostaje obiekt z zewnątrz:

```python
# krok 4: interfejs w warstwie logiki
class Appointments(Protocol):
    def upcoming_count(self, patient_id: int) -> int: ...
    def add(self, appointment: Appointment) -> None: ...


# krok 5: istniejące repozytorium spełnia interfejs bez zmian w kodzie
class AppointmentRepository:                          # to samo co wcześniej
    def upcoming_count(self, patient_id: int) -> int:
        return Appointment.objects.filter(patient_id=patient_id, starts_at__gt=now()).count()
    def add(self, appointment: Appointment) -> None:
        appointment.save()


# krok 6: serwis dostaje zależność z zewnątrz
class AppointmentService:
    def __init__(self, appointments: Appointments):
        self._appointments = appointments


# krok 7: test bez bazy
def test_fourth_appointment_is_refused():
    service = AppointmentService(appointments=InMemoryAppointments(upcoming=3))
    with pytest.raises(TooManyAppointments):
        service.book(patient_id=1, doctor_id=2, starts_at=MONDAY_10AM)
```

Krok 8, czyli oddzielenie encji domeny od modeli ORM, jest najdroższy i potrzebny tylko wtedy, gdy model ORM ogranicza logikę. W wielu projektach wystarczy zatrzymać się na kroku 7. Pozostałe obszary aplikacji mogą w tym czasie zostać w klasycznym układzie warstwowym. Szczegóły architektury docelowej są w tutorialach [hexagonal](../Hexagonal/) i [clean](../Clean/).

## Warstwy i funkcje razem

Duża aplikacja warstwowa podzielona tylko według warstw technicznych, czyli <a id="term-package-by-layer"></a>[package by layer](00%20Glossary%20Layered.md#package-by-layer), staje się trudna do ogarnięcia. Katalog `services/` ma sto plików, a zmiana jednej funkcji wymaga skakania po pięciu katalogach.

<a id="term-package-by-feature"></a>[Package by feature](00%20Glossary%20Layered.md#package-by-feature) odwraca priorytet: najpierw podział według funkcji albo obszarów biznesowych, a warstwy wewnątrz każdego z nich.

```text
Package by layer:                      Package by feature z warstwami w środku:

clinic/                                clinic/
├── views/                             ├── appointments/
│   ├── appointments.py                │   ├── __init__.py        publiczne API modułu
│   ├── doctors.py                     │   ├── views.py
│   ├── billing.py                     │   ├── services.py
│   └── ... (40 plików)                │   ├── domain.py
├── services/                          │   └── repositories.py
│   ├── appointments.py                ├── doctors/
│   └── ... (60 plików)                │   ├── views.py
└── repositories/                      │   ├── services.py
    └── ... (50 plików)                │   └── repositories.py
                                       └── billing/
                                           ├── views.py
                                           └── services.py    prosty moduł: dwie warstwy
```

Zasady, które utrzymują taki układ w porządku:

- każdy moduł ma publiczne API (np. funkcje eksportowane w `__init__.py` albo plik `api.py`), a inne moduły korzystają tylko z niego,
- moduł nie sięga do tabel i modeli innego modułu. Potrzebne dane pobiera przez API albo dostaje przez zdarzenie,
- warstwy wewnątrz modułu przestrzegają tych samych reguł zależności co wcześniej,
- moduły mogą mieć różną liczbę warstw: prosty moduł dwie, złożony cztery albo architekturę heksagonalną,
- granice między modułami i warstwami pilnuje `import-linter` w CI.

```toml
# pyproject.toml
[[tool.importlinter.contracts]]
name = "Moduły są niezależne"
type = "independence"
modules = ["clinic.appointments", "clinic.doctors", "clinic.billing"]
ignore_imports = ["clinic.appointments.services -> clinic.doctors"]   # tylko przez publiczne API

[[tool.importlinter.contracts]]
name = "Warstwy w module rejestracji"
type = "layers"
containers = ["clinic.appointments", "clinic.doctors", "clinic.billing"]
layers = ["views", "services", "domain", "repositories"]
```

Parametr `containers` pozwala zastosować ten sam kontrakt warstw do każdego modułu osobno. Taki układ to w praktyce modularny monolit z rozdziału 08 i najczęstsza docelowa postać dużej aplikacji Django lub Spring. Zachowuje prostotę warstw wewnątrz modułu, a skaluje się dzięki podziałowi według funkcji.

## Co zapamiętać

- Architektura warstwowa jest dobrym wyborem przy CRUD-zie, prostych regułach, małych zespołach i silnym wsparciu frameworka.
- Staje się ograniczeniem, gdy testy wymagają bazy, reguły się powtarzają, warstwy są ceremonią, a zespoły sobie przeszkadzają.
- Objawy zwykle dotyczą jednego obszaru, więc decyzja nie musi obejmować całego systemu.
- Migracja idzie obszar po obszarze: testy, serwisy jako wejście, czysta logika, interfejsy w logice, istniejące repozytoria jako adaptery, wstrzykiwanie, testy z fake'ami.
- Oddzielenie encji od modeli ORM jest opcjonalne i najdroższe.
- Duża aplikacja warstwowa pozostaje czytelna dzięki podziałowi według funkcji, z warstwami w środku modułów i publicznym API modułu.

## Pytania sprawdzające

### 26. Kiedy architektura warstwowa jest dobrym, świadomym wyborem, a kiedy staje się ograniczeniem?

<details>
<summary>Odpowiedź</summary>

Dobrym wyborem jest przy przewadze operacji CRUD, prostych i stabilnych regułach, małym lub zmiennym zespole, narzędziach wewnętrznych i prototypach oraz tam, gdzie framework daje dużo gotowych elementów. Ograniczeniem staje się, gdy testy reguł wymagają bazy i trwają minuty, reguły powtarzają się w wielu serwisach, zmiana funkcji dotyka wielu warstw bez logiki (sinkhole), zmiana biblioteki wymaga zmian w logice, a zespoły wchodzą sobie w drogę. Objawy zwykle dotyczą jednego obszaru, więc decyzja nie musi obejmować całego systemu.

Zobacz: sekcja „Świadomy wybór czy ograniczenie”.

</details>

### 27. Jak stopniowo przejść z architektury warstwowej na hexagonal albo clean bez przepisywania systemu?

<details>
<summary>Odpowiedź</summary>

Obszar po obszarze, według wzorca strangler fig. Kolejne kroki to testy integracyjne zamrażające zachowanie, cała logika przez serwisy, czyste reguły wydzielone bez ORM-a, interfejsy (`Protocol`) zdefiniowane w warstwie logiki, istniejące repozytoria jako ich implementacje, wstrzykiwanie zależności przez konstruktor i testy z fake'ami bez bazy. Odwrócenie zależności nie wymaga przepisywania logiki. Oddzielenie encji od modeli ORM jest opcjonalnym, najdroższym krokiem. Pozostałe obszary mogą zostać warstwowe.

Zobacz: sekcja „Stopniowe przejście”.

</details>

### 28. Jak połączyć warstwy z podziałem na funkcje (package by feature, moduły z warstwami w środku), żeby duża aplikacja warstwowa pozostała czytelna?

<details>
<summary>Odpowiedź</summary>

Zamiast package by layer z setkami plików w `services/` stosuje się package by feature: najpierw moduły według funkcji lub obszarów biznesowych, a w każdym warstwy. Każdy moduł ma publiczne API, nie sięga do cudzych tabel i modeli, a warstwy wewnątrz przestrzegają zwykłych reguł zależności. Moduły mogą mieć różną liczbę warstw. Granice pilnuje `import-linter` (kontrakt `independence` dla modułów i `layers` z `containers` dla warstw). To w praktyce modularny monolit.

Zobacz: sekcja „Warstwy i funkcje razem”.

</details>
