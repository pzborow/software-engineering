# Odpowiedzialności warstw

Nazwy warstw są proste, ale granice między nimi w praktyce się rozmywają. Walidacja trafia do widoków, transakcje do repozytoriów, a reguły biznesowe do zapytań SQL. Ten rozdział opisuje, za co odpowiada każda warstwa, na przykładzie umawiania wizyty w przychodni, oraz gdzie umieszczać walidację, transakcje i obsługę błędów.

```text
POST /appointments
      │
      ▼
prezentacja      views.py         parsowanie żądania, format, odpowiedź HTTP
      │
      ▼
serwisy          services.py      przypadek użycia „umów wizytę”, transakcja
      │
      ▼
logika           domain.py        reguły: grafik lekarza, limit wizyt, odwołanie
      │
      ▼
dostęp do danych repositories.py  zapytania, zapis, mapowanie na tabele
```

## Cztery typowe warstwy

<a id="term-presentation-layer"></a>[Warstwa prezentacji](00%20Glossary%20Layered.md#presentation-layer) obsługuje komunikację z użytkownikiem albo klientem API. Parsuje żądania, sprawdza format danych, wywołuje warstwę niżej i formatuje odpowiedź: HTML, JSON, kod statusu. Nie podejmuje decyzji biznesowych.

<a id="term-service-layer"></a>[Warstwa serwisów](00%20Glossary%20Layered.md#service-layer) (service layer, application layer) to wzorzec opisany przez Randy'ego Stafforda w książce Martina Fowlera „Patterns of Enterprise Application Architecture”. Definiuje operacje, które aplikacja udostępnia, czyli przypadki użycia: „umów wizytę”, „odwołaj wizytę”, „pokaż grafik”. Koordynuje pracę, wyznacza transakcje i sprawdza uprawnienia.

<a id="term-business-layer"></a>[Warstwa logiki biznesowej](00%20Glossary%20Layered.md#business-layer) zawiera reguły domeny: lekarz nie może mieć dwóch wizyt w tym samym czasie, pacjent może mieć najwyżej trzy nieodbyte wizyty, wizytę można odwołać najpóźniej 24 godziny wcześniej.

<a id="term-data-access-layer"></a>[Warstwa dostępu do danych](00%20Glossary%20Layered.md#data-access-layer) ukrywa szczegóły przechowywania: zapytania SQL albo ORM, mapowanie wierszy na obiekty, połączenia z bazą.

```python
# presentation/views.py
def book_appointment(request):
    form = BookAppointmentForm(request.POST)             # format i typy
    if not form.is_valid():
        return JsonResponse(form.errors, status=422)
    try:
        appointment_id = appointment_service.book(
            patient_id=request.user.patient_id,
            doctor_id=form.cleaned_data["doctor_id"],
            starts_at=form.cleaned_data["starts_at"],
        )
    except SlotTaken:
        return JsonResponse({"error": "Termin jest już zajęty"}, status=409)
    return JsonResponse({"id": appointment_id}, status=201)


# services/appointments.py
class AppointmentService:
    def book(self, patient_id: int, doctor_id: int, starts_at: datetime) -> int:
        with transaction.atomic():
            schedule = self._schedules.for_doctor(doctor_id, starts_at.date())
            patient = self._patients.get(patient_id)
            appointment = schedule.book(patient, starts_at)      # reguły w warstwie logiki
            self._appointments.add(appointment)
        self._notifications.appointment_booked(appointment)
        return appointment.id


# business/schedule.py
class DoctorSchedule:
    def book(self, patient: Patient, starts_at: datetime) -> Appointment:
        if not self.is_working_at(starts_at):
            raise OutsideWorkingHours(starts_at)
        if self.is_taken(starts_at):
            raise SlotTaken(starts_at)
        if patient.upcoming_appointments >= 3:
            raise TooManyAppointments(patient.id)
        return Appointment.new(patient.id, self.doctor_id, starts_at)
```

## Serwisy czy logika

Warstwa serwisów i warstwa logiki są często mylone, a w wielu projektach jedna z nich faktycznie nie istnieje. Fowler opisuje dwa sposoby organizacji logiki, które decydują o tym, czy potrzebne są obie.

<a id="term-transaction-script"></a>[Transaction script](00%20Glossary%20Layered.md#transaction-script) to procedura, która obsługuje jedno żądanie od początku do końca: pobiera dane, sprawdza reguły, zapisuje wynik. Logika siedzi w serwisie, a warstwa logiki jako osobny byt nie istnieje, bo reguły są w kodzie serwisu.

<a id="term-domain-model"></a>[Model domeny](00%20Glossary%20Layered.md#domain-model) w rozumieniu Fowlera to obiekty z danymi i zachowaniem, które same pilnują reguł. Serwis tylko je koordynuje.

| | Transaction script | Model domeny |
|---|---|---|
| Gdzie są reguły | w serwisie | w obiektach domeny |
| Warstwa logiki | praktycznie brak | wyraźna i bogata |
| Warstwa serwisów | cała logika | cienka koordynacja i transakcje |
| Dobre dla | prostych reguł, CRUD | złożonych, zmiennych reguł |
| Koszt przy wzroście | powielanie reguł między skryptami | więcej projektowania na starcie |

Czy zawsze potrzebne są obie warstwy? Nie. W prostej aplikacji transaction script wystarczy, a osobna warstwa logiki byłaby pusta. Gdy reguły rosną i zaczynają się powtarzać (`book`, `reschedule` i `book_for_family` sprawdzają ten sam grafik), warto je przenieść do obiektów domeny, a serwisom zostawić koordynację.

## Gdzie walidować

Walidacja ma trzy rodzaje i każdy ma swoje miejsce:

| Rodzaj | Przykład | Warstwa |
|---|---|---|
| Format | data ma poprawny format, `doctor_id` jest liczbą | prezentacja (formularz, serializer) |
| Reguły aplikacji | użytkownik ma prawo umawiać wizyty dla tego pacjenta | serwisy |
| Reguły biznesowe | termin jest w godzinach pracy, lekarz jest wolny | logika biznesowa |

Walidacja często trafia do złej warstwy z trzech powodów:

- frameworki ułatwiają walidację w formularzach i serializerach, więc reguły biznesowe trafiają do `clean()` formularza Django albo `validate()` serializera DRF. Wtedy działają tylko przy wywołaniu przez ten formularz, a nie przez API, import CSV ani zadanie w tle,
- baza danych daje ograniczenia (`CHECK`, `UNIQUE`), więc reguły lądują w schemacie bez odpowiednika w kodzie i bez czytelnego komunikatu dla użytkownika,
- brak warstwy logiki powoduje, że reguły trafiają tam, gdzie akurat pisze się kod.

Część walidacji jest celowo powtórzona. Formularz sprawdza, czy data jest w przyszłości, żeby dać szybki komunikat, a warstwa logiki sprawdza to ponownie, bo wywołanie może przyjść z innego miejsca. Ograniczenie w bazie jest ostatnią linią obrony, a nie jedynym miejscem reguły.

## Transakcje i wyjątki

<a id="term-transaction-boundary"></a>[Granica transakcji](00%20Glossary%20Layered.md#transaction-boundary) powinna odpowiadać przypadkowi użycia, dlatego wyznacza się ją w warstwie serwisów. Jeden przypadek użycia to jedna transakcja: wszystko albo nic.

Częste błędy:

- transakcja w repozytorium: każdy `save` to osobna transakcja, więc przypadek użycia zapisujący dwie rzeczy może zostawić dane w połowie,
- transakcja w widoku, np. `ATOMIC_REQUESTS` w Django: obejmuje całe żądanie, także renderowanie i wywołania zewnętrzne, więc jest za szeroka i trzyma połączenie z bazą za długo,
- wywołania zewnętrzne (e-mail, płatność) wewnątrz transakcji: rollback ich nie cofnie, a długie wywołanie blokuje bazę. Takie efekty wykonuje się po commicie, np. `transaction.on_commit()` w Django.

Wyjątki przechodzą przez warstwy w górę, ale każda warstwa tłumaczy je na swój język:

```text
dostęp do danych   IntegrityError (psycopg)       ──► tłumaczy na SlotTaken (wyjątek biznesowy)
logika             OutsideWorkingHours, SlotTaken ──► przepuszcza wyjątki biznesowe
serwisy            przepuszcza albo opakowuje w wyjątek aplikacji
prezentacja        SlotTaken ──► 409, OutsideWorkingHours ──► 422, nieznany ──► 500 i log
```

Wyjątek biblioteki bazy danych nie powinien dotrzeć do widoku. Widok, który łapie `IntegrityError`, zależy od szczegółów warstwy danych i łamie separację. Z kolei warstwa logiki nie powinna rzucać `Http404`, bo nie wie, że działa w kontekście HTTP.

## Co zapamiętać

- Prezentacja obsługuje format i protokół, serwisy przypadki użycia i transakcje, logika reguły biznesowe, a dostęp do danych zapis i odczyt.
- Warstwa serwisów to wzorzec Service Layer z książki Fowlera, a nie miejsce na całą logikę.
- Przy transaction script logika jest w serwisie, a przy modelu domeny w obiektach. Prosta aplikacja nie potrzebuje obu warstw.
- Format waliduje prezentacja, uprawnienia serwisy, reguły biznesowe warstwa logiki, a baza jest ostatnią linią obrony.
- Granica transakcji to przypadek użycia w warstwie serwisów. Efekty zewnętrzne wykonuje się po commicie.
- Każda warstwa tłumaczy wyjątki na swój język. Wyjątek bazy nie trafia do widoku, a `Http404` nie trafia do logiki.

## Pytania sprawdzające

### 4. Jakie są typowe warstwy (prezentacja, aplikacja lub serwisy, logika biznesowa, dostęp do danych) i za co odpowiada każda z nich?

<details>
<summary>Odpowiedź</summary>

Prezentacja parsuje żądania, sprawdza format, wywołuje serwisy i formatuje odpowiedź, bez decyzji biznesowych. Serwisy (Service Layer) definiują przypadki użycia, koordynują pracę, wyznaczają transakcje i sprawdzają uprawnienia. Logika biznesowa zawiera reguły domeny, np. grafik lekarza, limit wizyt czy termin odwołania. Dostęp do danych ukrywa zapytania, mapowanie i połączenia z bazą.

Zobacz: sekcja „Cztery typowe warstwy”.

</details>

### 5. Czym różni się warstwa serwisów aplikacyjnych od warstwy logiki biznesowej? Czy zawsze potrzebne są obie?

<details>
<summary>Odpowiedź</summary>

Serwisy odpowiadają na pytanie „co aplikacja robi” (przypadki użycia, transakcje, uprawnienia), a logika na pytanie „jakie reguły obowiązują” (niezmienniki domeny). Przy transaction script reguły są w serwisie, a warstwa logiki praktycznie nie istnieje. Przy modelu domeny reguły są w obiektach, a serwis jest cienki. Nie zawsze potrzebne są obie. Prosta aplikacja wystarczy z transaction script, a osobną warstwę logiki wprowadza się, gdy reguły rosną i zaczynają się powtarzać między przypadkami użycia.

Zobacz: sekcja „Serwisy czy logika”.

</details>

### 6. W której warstwie powinna odbywać się walidacja (format, reguły aplikacji, reguły biznesowe) i dlaczego często trafia do złej?

<details>
<summary>Odpowiedź</summary>

Format w prezentacji (formularz, serializer), reguły aplikacji i uprawnienia w serwisach, reguły biznesowe w warstwie logiki, a ograniczenia bazy jako ostatnia linia obrony. Walidacja trafia do złej warstwy, bo frameworki ułatwiają ją w formularzach i serializerach, gdzie działa tylko dla jednej ścieżki wywołania, bo ograniczenia bazy kuszą, żeby umieścić regułę tylko w schemacie, i bo przy braku warstwy logiki reguły lądują tam, gdzie akurat powstaje kod. Częściowe powtórzenie w prezentacji i logice jest celowe.

Zobacz: sekcja „Gdzie walidować”.

</details>

### 7. Gdzie w architekturze warstwowej wyznacza się granice transakcji i jak obsługuje się wyjątki między warstwami?

<details>
<summary>Odpowiedź</summary>

Granicę transakcji wyznacza warstwa serwisów, bo transakcja odpowiada przypadkowi użycia. Transakcja w repozytorium jest za wąska (zapis w połowie), a w widoku (`ATOMIC_REQUESTS`) za szeroka. Efekty zewnętrzne wykonuje się po commicie (`on_commit`). Wyjątki idą w górę, a każda warstwa tłumaczy je na swój język: dostęp do danych zamienia `IntegrityError` na wyjątek biznesowy, a prezentacja mapuje wyjątki biznesowe na kody HTTP. Wyjątek bazy nie trafia do widoku, a `Http404` nie trafia do logiki.

Zobacz: sekcja „Transakcje i wyjątki”.

</details>
