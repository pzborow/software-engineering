# Testowanie

Testowanie aplikacji warstwowej ma jedną charakterystyczną trudność: logika biznesowa zależy od warstwy dostępu do danych, a ta zależy od bazy. Test reguły „pacjent może mieć najwyżej trzy nadchodzące wizyty” musi więc w jakiś sposób poradzić sobie z bazą. Ten rozdział wyjaśnia, skąd ta trudność, jakie są sposoby jej obejścia i jak zbudować rozsądną strategię testów.

```text
test reguły ──► AppointmentService ──► AppointmentRepository ──► ORM ──► PostgreSQL
                     logika               dostęp do danych               baza

opcja 1: prawdziwa baza           wolniej, ale prawdziwie
opcja 2: mock repozytorium        szybko, ale test zna implementację
opcja 3: wydzielenie czystej logiki  szybko i prawdziwie, wymaga zmiany kodu
```

## Dlaczego reguły potrzebują bazy

W klasycznym układzie warstwa logiki importuje i tworzy obiekty warstwy dostępu do danych albo sama jest modelem ORM. Obie sytuacje wiążą test reguły z bazą:

```python
class AppointmentService:
    def __init__(self):
        self._repo = AppointmentRepository()             # konkretna klasa, nie da się podmienić

    def book(self, patient_id: int, doctor_id: int, starts_at: datetime) -> int:
        if self._repo.upcoming_count(patient_id) >= 3:   # reguła wymaga zapytania
            raise TooManyAppointments(patient_id)
        ...


class Appointment(models.Model):
    def can_be_rescheduled(self) -> bool:
        return self.doctor.schedule.has_free_slot_after(self.starts_at)   # relacje z bazy
```

Koszty testowania z bazą:

- czas: test z bazą trwa dziesiątki lub setki milisekund zamiast mikrosekund. Tysiąc testów to minuty zamiast sekund, więc programiści uruchamiają je rzadziej,
- przygotowanie danych: żeby sprawdzić limit wizyt, trzeba utworzyć przychodnię, specjalizację, lekarza, grafik, pacjenta i trzy wizyty. Fixtures rosną i stają się kruche,
- infrastruktura: CI potrzebuje bazy, migracji i czyszczenia stanu między testami,
- trudność przypadków brzegowych: symulowanie błędu bazy albo wyścigu dwóch transakcji jest skomplikowane,
- rozmyte granice: test „jednostkowy” reguły jest w praktyce testem integracyjnym całego stosu.

To główny argument, którym architektury hexagonal, onion i clean uzasadniają odwrócenie zależności. W aplikacji warstwowej problem da się jednak w dużej mierze złagodzić bez zmiany architektury.

## Mocki czy prawdziwa baza

Są trzy podejścia, a każde ma swoje miejsce.

<a id="term-mock"></a>[Mock](00%20Glossary%20Layered.md#mock) repozytorium to obiekt podstawiony zamiast prawdziwego repozytorium, który zwraca przygotowane odpowiedzi i nagrywa wywołania. Wymaga, żeby serwis przyjmował repozytorium z zewnątrz (wstrzykiwanie zależności przez konstruktor):

```python
def test_fourth_appointment_is_refused():
    repo = Mock()
    repo.upcoming_count.return_value = 3
    service = AppointmentService(appointments=repo, schedules=Mock(), patients=Mock())

    with pytest.raises(TooManyAppointments):
        service.book(patient_id=1, doctor_id=2, starts_at=MONDAY_10AM)

    repo.add.assert_not_called()
```

Mocki są szybkie, ale test zna szczegóły implementacji: wie, że serwis woła `upcoming_count`, a nie `list_upcoming`. Refaktoryzacja, która nie zmienia zachowania, psuje test. Mock może też zwracać wartości, których prawdziwe repozytorium nigdy by nie zwróciło, więc test przechodzi, a produkcja nie działa.

<a id="term-integration-test"></a>[Test integracyjny](00%20Glossary%20Layered.md#integration-test) z prawdziwą bazą sprawdza całą ścieżkę: serwis, repozytorium, ORM, zapytania i ograniczenia bazy. Najlepiej na tej samej bazie co produkcja, uruchamianej w kontenerze przez Testcontainers albo usługę CI. SQLite w pamięci zamiast PostgreSQL jest szybszy, ale ukrywa różnice: inne typy dat, brak niektórych ograniczeń, inna obsługa blokad.

```python
@pytest.mark.django_db
def test_fourth_appointment_is_refused(patient, doctor_with_schedule):
    for hour in (9, 10, 11):
        AppointmentService().book(patient.id, doctor_with_schedule.id, next_monday(hour))

    with pytest.raises(TooManyAppointments):
        AppointmentService().book(patient.id, doctor_with_schedule.id, next_monday(12))
```

Trzecie podejście to wydzielenie czystej logiki. Reguły, które nie potrzebują bazy, przenosi się do funkcji albo klas, które dostają dane jako argumenty. Serwis pobiera dane i przekazuje je do logiki, a sama logika jest testowana bez żadnych dublerów:

```python
# business/booking_rules.py: czysta logika, bez ORM
MAX_UPCOMING = 3

def check_can_book(upcoming_count: int, slot_taken: bool, within_hours: bool) -> None:
    if not within_hours:
        raise OutsideWorkingHours()
    if slot_taken:
        raise SlotTaken()
    if upcoming_count >= MAX_UPCOMING:
        raise TooManyAppointments()


def test_fourth_appointment_is_refused():
    with pytest.raises(TooManyAppointments):
        check_can_book(upcoming_count=3, slot_taken=False, within_hours=True)
```

| Podejście | Szybkość | Wierność | Kruchość | Kiedy |
|---|---|---|---|---|
| mock repozytorium | wysoka | niska, mock może kłamać | wysoka, zna implementację | pojedyncze interakcje, np. „nie zapisano przy błędzie” |
| prawdziwa baza | niska | wysoka | niska, sprawdza zachowanie | zapytania, ograniczenia, transakcje, przypadki użycia |
| czysta logika | najwyższa | wysoka dla reguł | niska | reguły biznesowe, obliczenia, walidacja |

## Strategia testów

Rozsądna strategia dla aplikacji warstwowej łączy te podejścia w proporcjach dopasowanych do tego, gdzie jest ryzyko:

```text
          ▲    kilka testów end-to-end przez HTTP (najważniejsze ścieżki)
         ▲▲▲   testy integracyjne serwisów z prawdziwą bazą (przypadki użycia)
        ▲▲▲▲▲  testy czystej logiki (reguły, obliczenia, walidacja)
```

Zasady:

- reguły biznesowe wydzielaj do czystych funkcji albo klas i testuj bez bazy. To największa grupa testów,
- przypadki użycia testuj integracyjnie przez serwis z prawdziwą bazą w kontenerze. Test sprawdza wynik (wizyta zapisana, wyjątek rzucony), a nie wywołania metod,
- mocki stosuj oszczędnie: dla usług zewnętrznych (e-mail, SMS, płatności) i pojedynczych interakcji, a nie dla repozytoriów w każdym teście,
- zapytania i repozytoria testuj z bazą, bo tam są prawdziwe błędy: złe JOIN-y, brakujące filtry, N+1,
- przyspieszaj testy z bazą transakcjami wycofywanymi po każdym teście (domyślne w `pytest-django` i Spring `@Transactional` w testach), bazą w kontenerze uruchamianą raz na sesję i fabrykami danych (`factory_boy`) zamiast wielkich fixtures,
- kilka testów end-to-end przez HTTP sprawdza, czy warstwy są poprawnie połączone: routing, serializacja, uprawnienia.

W aplikacji warstwowej testy integracyjne z bazą są normalną, dużą częścią zestawu, a nie wyjątkiem. To świadomy koszt tej architektury. Jeśli czas testów zaczyna przeszkadzać, pierwszym krokiem jest wydzielenie czystej logiki. Dopiero gdy to nie wystarcza, warto rozważyć odwrócenie zależności z rozdziału 08.

## Co zapamiętać

- W architekturze warstwowej logika zależy od dostępu do danych, więc testy reguł zwykle wymagają bazy.
- Koszty to czas, przygotowanie danych, infrastruktura w CI, trudne przypadki brzegowe i rozmyte granice testów.
- Mocki repozytoriów są szybkie, ale kruche i mogą kłamać.
- Testy integracyjne z prawdziwą bazą w kontenerze są wierne, a SQLite zamiast produkcyjnej bazy ukrywa różnice.
- Wydzielenie czystej logiki daje szybkie i wierne testy reguł bez zmiany architektury.
- Strategia: dużo testów czystej logiki, testy serwisów z bazą, mocki tylko dla usług zewnętrznych i kilka testów end-to-end.

## Pytania sprawdzające

### 17. Dlaczego testowanie logiki biznesowej w architekturze warstwowej zwykle wymaga bazy danych? Jakie są tego koszty?

<details>
<summary>Odpowiedź</summary>

Bo warstwa logiki zależy od warstwy dostępu do danych: tworzy konkretne repozytoria albo sama jest modelem ORM, a reguły wykonują zapytania lub czytają relacje. Koszty to wolne testy (minuty zamiast sekund), rozbudowane i kruche przygotowanie danych, infrastruktura w CI (baza, migracje, czyszczenie), trudne symulowanie błędów i wyścigów oraz rozmyte granice, bo test jednostkowy staje się integracyjnym. To główny argument architektur z odwróconą zależnością.

Zobacz: sekcja „Dlaczego reguły potrzebują bazy”.

</details>

### 18. Mocki repozytoriów czy testy integracyjne z prawdziwą bazą? Jak zbudować rozsądną strategię testów w aplikacji warstwowej?

<details>
<summary>Odpowiedź</summary>

Mocki są szybkie, ale kruche (znają implementację) i mogą kłamać. Testy z prawdziwą bazą w kontenerze (Testcontainers, ta sama baza co produkcja, nie SQLite) są wierne. Najlepiej wydzielić czystą logikę do funkcji testowanych bez dublerów. Strategia: najwięcej testów czystej logiki, przypadki użycia integracyjnie przez serwis z bazą, sprawdzające wynik, mocki tylko dla usług zewnętrznych, repozytoria i zapytania z bazą oraz kilka testów end-to-end. Testy z bazą przyspieszają rollback po teście, kontener raz na sesję i fabryki danych.

Zobacz: sekcje „Mocki czy prawdziwa baza” i „Strategia testów”.

</details>
