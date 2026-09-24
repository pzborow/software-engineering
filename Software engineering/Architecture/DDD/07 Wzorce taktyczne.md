# Wzorce taktyczne

Gdy granice kontekstów są ustalone, a język jest uzgodniony, zespół buduje model w kodzie. Wzorce taktyczne to sprawdzone sposoby wyrażania pojęć domeny: czym jest rzecz z tożsamością, czym wartość, gdzie umieścić regułę, która nie pasuje do żadnego obiektu, jak tworzyć złożone obiekty i jak je przechowywać. Ten rozdział skupia się na tym, kiedy i jak ich używać, a nie tylko na definicjach.

```text
wzorzec            pytanie, na które odpowiada
encja              co ma tożsamość, która trwa mimo zmian?
value object       co jest opisem, porównywanym po wartości?
serwis domenowy    gdzie umieścić regułę, która nie należy do jednego obiektu?
fabryka            jak zbudować złożony obiekt w poprawnym stanie?
repozytorium       jak pobrać i zapisać agregat, udając kolekcję w pamięci?
```

## Tożsamość czy wartość

<a id="term-entity"></a>[Encja](00%20Glossary%20DDD.md#entity) to obiekt, który ma tożsamość trwającą mimo zmian stanu. Umowa najmu `RA-2026-0412` pozostaje tą samą umową po przedłużeniu, zmianie kierowcy i zwrocie auta. Dwie encje są równe, gdy mają tę samą tożsamość, nawet jeśli różnią się wszystkimi innymi polami.

<a id="term-value-object"></a>[Value object](00%20Glossary%20DDD.md#value-object) nie ma tożsamości. Jest opisem, który porównuje się po wartości: dwie kwoty 300 PLN są tą samą kwotą. Value object jest niezmienny. Zamiast go modyfikować, tworzy się nowy.

```python
@dataclass(frozen=True)
class Money:
    amount: Decimal
    currency: str

    def __post_init__(self):
        if self.amount.as_tuple().exponent < -2:
            raise ValueError("Najwyżej dwa miejsca po przecinku")

    def __add__(self, other: "Money") -> "Money":
        if other.currency != self.currency:
            raise CurrencyMismatch(self.currency, other.currency)
        return Money(self.amount + other.amount, self.currency)


@dataclass(frozen=True)
class RentalPeriod:
    start: datetime
    end: datetime

    def __post_init__(self):
        if self.end <= self.start:
            raise ValueError("Zwrot musi być po odbiorze")

    @property
    def days(self) -> int:
        return math.ceil((self.end - self.start) / timedelta(days=1))

    def extended_to(self, new_end: datetime) -> "RentalPeriod":
        return RentalPeriod(self.start, new_end)
```

Czy dany koncept to encja, czy value object, zależy od kontekstu, a nie od natury rzeczy. Kryterium brzmi: czy biznes śledzi ten obiekt w czasie jako „ten konkretny”?

| Koncept | Kontekst | Encja czy VO | Dlaczego |
|---|---|---|---|
| Adres | rezerwacje (adres dostawy auta) | value object | liczy się treść, nie historia |
| Adres | zarządzanie oddziałami (oddział ma adres) | część encji `Branch` | adres opisuje oddział |
| Adres | firma kurierska | encja | punkty dostawy mają ID, historię, notatki kierowców |
| Kwota | wszędzie | value object | 300 PLN to 300 PLN |
| Numer telefonu | rezerwacje | value object | opis, z walidacją formatu |
| Samochód | rezerwacje | value object `VehicleClass` | rezerwuje się klasę, nie konkretne auto |
| Samochód | flota | encja `Vehicle` | śledzimy konkretny egzemplarz po VIN |

Domyślnie warto zaczynać od value objectu i zamieniać go w encję dopiero wtedy, gdy biznes potrzebuje śledzić tożsamość. Value objects są prostsze: nie mają cyklu życia, są bezpieczne do współdzielenia i łatwe do testowania.

## Wartości zamiast prymitywów

Value objects są niedoceniane, bo na pierwszy rzut oka wyglądają jak dodatkowy kod dla prostych danych. Alternatywa ma jednak nazwę: <a id="term-primitive-obsession"></a>[primitive obsession](00%20Glossary%20DDD.md#primitive-obsession), czyli przedstawianie pojęć domeny typami prostymi, takimi jak `str`, `int`, `float` i `Decimal`.

```python
# primitive obsession: kolejność argumentów, jednostki i walidacja na głowie wywołującego
def quote(vehicle_class: str, start: datetime, end: datetime, driver_age: int,
          price: float, currency: str, discount: float) -> float: ...

quote("SUV", end, start, 22, 180.0, "PLN", 15)      # zamienione daty, rabat 15 czy 0.15?


# value objects: błędy niemożliwe albo wykrywane przy tworzeniu
def quote(vehicle_class: VehicleClassCode, period: RentalPeriod, driver: DriverProfile,
          base_rate: Money, discount: Percentage) -> Money: ...
```

Co dają value objects:

- walidacja w jednym miejscu, przy tworzeniu. Niepoprawna wartość nie może istnieć,
- typy rozróżniają pojęcia. `CustomerId` i `VehicleId` nie dadzą się pomylić, choć oba są napisami,
- zachowanie jest przy danych: `period.days`, `money + money`, `percentage.of(money)`,
- jednostki są jawne. `Money` ma walutę, `Distance` ma kilometry, więc nie da się dodać złotówek do euro,
- niezmienność eliminuje błędy przypadkowego współdzielenia i modyfikacji.

W Pythonie `@dataclass(frozen=True)` sprawia, że value object kosztuje kilka linii. Nawet prosty typ `NewType("VehicleId", str)` pomaga mypy wyłapać pomyłki bez kosztu w czasie działania.

## Reguła bez domu

<a id="term-domain-service"></a>[Serwis domenowy](00%20Glossary%20DDD.md#domain-service) to bezstanowa operacja domeny, która nie należy naturalnie do żadnej encji ani value objectu. Nazywa się ją językiem domeny i umieszcza w modelu, a nie w warstwie aplikacji.

Serwis domenowy ma sens, gdy:

- operacja dotyczy kilku obiektów, z których żaden nie jest jej naturalnym właścicielem, np. przeniesienie rezerwacji z jednego auta na drugie z przeliczeniem różnicy w cenie,
- operacja wymaga wiedzy spoza jednego agregatu, np. sprawdzenie dostępności floty przy przedłużeniu,
- operacja jest pojęciem w języku ekspertów („wycena”, „kalkulacja kary”), a nie czynnością jednego obiektu.

```python
class DamageLiabilityCalculator:                      # pojęcie z języka likwidatorów
    def liability(self, damage: Damage, coverage: InsuranceCoverage, driver: DriverProfile) -> Money:
        base = damage.estimated_cost
        if coverage.includes(damage.category):
            base = min(base, coverage.deductible)
        if driver.is_young:
            base = base + coverage.young_driver_surcharge
        return base
```

Serwis domenowy bywa też sygnałem anemicznego modelu. Jeśli większość logiki trafia do serwisów o nazwach `ReservationService` czy `RentalManager`, a encje mają tylko gettery i settery, to nie jest DDD, tylko procedury operujące na strukturach danych. Pytanie kontrolne: czy ta reguła dotyczy stanu jednego obiektu? Jeśli tak, należy do tego obiektu. `agreement.can_be_extended(...)` należy do umowy, a nie do serwisu.

## Budowanie złożonych obiektów

<a id="term-factory"></a>[Fabryka](00%20Glossary%20DDD.md#factory) to obiekt albo metoda odpowiedzialna za utworzenie złożonego obiektu domeny w poprawnym stanie. Konstruktor wystarcza, gdy tworzenie jest proste: kilka pól i walidacja. Fabryka jest potrzebna, gdy:

- utworzenie wymaga kilku kroków albo danych z różnych źródeł,
- trzeba wybrać konkretny typ na podstawie danych (umowa krótkoterminowa, długoterminowa, flotowa),
- tworzenie jest pojęciem domeny, np. „zawarcie umowy na podstawie rezerwacji”,
- obiekt odtwarzany z bazy lub zdarzeń ma inne reguły niż nowo tworzony.

```python
class RentalAgreement:
    @classmethod
    def from_reservation(cls, reservation: Reservation, vehicle: RentedVehicle,
                         driver: Driver, now: datetime) -> "RentalAgreement":
        if reservation.status is not ReservationStatus.CONFIRMED:
            raise RentalError("Umowę zawiera się tylko dla potwierdzonej rezerwacji")
        if not driver.license_valid_on(reservation.period.end):
            raise RentalError("Prawo jazdy traci ważność przed końcem najmu")
        agreement = cls(
            id=AgreementId.new(),
            reservation_id=reservation.id,
            vehicle=vehicle,
            driver=driver,
            period=reservation.period,
            deposit=reservation.quote.deposit,
        )
        agreement._record(AgreementSigned(agreement.id, reservation.id, vehicle.vin, now))
        return agreement
```

Metoda fabrykująca na klasie (`from_reservation`) albo na innym agregacie (`reservation.convert_to_agreement(...)`) wystarcza w większości przypadków. Osobna klasa fabryki ma sens, gdy tworzenie wymaga zależności, np. generatora numerów umów zgodnych z przepisami.

## Kolekcja, a nie tabela

<a id="term-repository"></a>[Repozytorium](00%20Glossary%20DDD.md#repository) w DDD udaje kolekcję agregatów w pamięci. Pozwala pobrać agregat po identyfikatorze i zapisać go w całości. Istnieje tylko dla korzeni agregatów, nie dla każdej encji.

```python
class RentalAgreements(Protocol):                     # nazwa jak kolekcja, język domeny
    def get(self, agreement_id: AgreementId) -> RentalAgreement: ...
    def add(self, agreement: RentalAgreement) -> None: ...
    def active_for_vehicle(self, vin: Vin) -> RentalAgreement | None: ...
```

Repozytorium różni się od dwóch podobnych wzorców: <a id="term-dao"></a>[DAO](00%20Glossary%20DDD.md#dao) (Data Access Object), który opakowuje dostęp do jednej tabeli, i generycznego repozytorium CRUD dostarczanego przez framework:

| | Repozytorium DDD | DAO | Generyczne repozytorium CRUD |
|---|---|---|---|
| Operuje na | całych agregatach | wierszach tabel | dowolnych encjach |
| Metody | `get`, `add`, zapytania z języka domeny | `insert`, `update`, `select_by_x` | `find_all`, `find_by_id`, `save`, `delete` |
| Interfejs należy do | modelu domeny | warstwy danych | frameworka |
| Ile ich jest | jedno na korzeń agregatu | jedno na tabelę | jedno generyczne dla wszystkiego |
| Zna tabele i SQL | tylko implementacja | tak | przez ORM |

Generyczne repozytorium (`Repository[T]` z `find_all` i `delete`) wygląda na oszczędność, ale łamie model. Pozwala usunąć umowę najmu, choć biznes umów nie usuwa, tylko je anuluje lub zamyka. Pozwala pobrać wszystkie umowy, choć żaden przypadek użycia tego nie potrzebuje. Pozwala też zapisać encję wewnętrzną agregatu z pominięciem korzenia. Metody repozytorium DDD wynikają z potrzeb domeny i przypadków użycia, a nie z operacji na tabeli.

## Co zapamiętać

- Encja ma tożsamość trwającą mimo zmian, value object jest niezmiennym opisem porównywanym po wartości.
- To samo pojęcie może być encją w jednym kontekście i value objectem w innym. Domyślnie zaczynaj od value objectu.
- Value objects likwidują primitive obsession: walidacja przy tworzeniu, rozróżnione typy, jawne jednostki, zachowanie przy danych.
- Serwis domenowy jest dla reguł bez naturalnego właściciela. Nadmiar serwisów to sygnał anemicznego modelu.
- Fabryka tworzy złożone obiekty w poprawnym stanie, a zwykle wystarcza metoda fabrykująca.
- Repozytorium DDD udaje kolekcję agregatów, ma metody z języka domeny i istnieje tylko dla korzeni. To nie jest DAO ani generyczny CRUD.

## Pytania sprawdzające

### 30. Czym różni się encja od value object? Jak zdecydować, czym jest dany koncept (np. adres, kwota, numer telefonu)?

<details>
<summary>Odpowiedź</summary>

Encja ma tożsamość trwającą mimo zmian stanu i porównuje się ją po tożsamości. Value object nie ma tożsamości, jest niezmienny i porównuje się go po wartości. Decyduje kontekst i pytanie, czy biznes śledzi obiekt w czasie jako „ten konkretny”. Adres dostawy w rezerwacjach to value object, a punkt dostawy u kuriera to encja. Kwota i numer telefonu to zwykle value objects. Samochód to value object `VehicleClass` w rezerwacjach, a encja `Vehicle` we flocie. Domyślnie zaczyna się od value objectu.

Zobacz: sekcja „Tożsamość czy wartość”.

</details>

### 31. Dlaczego value objects są niedoceniane i jak zmniejszają liczbę błędów (primitive obsession)?

<details>
<summary>Odpowiedź</summary>

Wyglądają jak dodatkowy kod dla prostych danych, ale alternatywą jest primitive obsession: pojęcia jako `str`, `float` czy `int`, z pomylonymi argumentami, niejasnymi jednostkami i walidacją rozsianą po kodzie. Value objects walidują przy tworzeniu (niepoprawna wartość nie istnieje), rozróżniają typy (`CustomerId` i `VehicleId`), trzymają zachowanie przy danych, jawnie określają jednostki (waluta) i są niezmienne. W Pythonie kosztują kilka linii z `frozen=True`.

Zobacz: sekcja „Wartości zamiast prymitywów”.

</details>

### 32. Kiedy potrzebny jest serwis domenowy, a kiedy to sygnał anemicznego modelu?

<details>
<summary>Odpowiedź</summary>

Serwis domenowy jest potrzebny dla bezstanowej operacji, która nie należy do jednego obiektu: dotyczy kilku obiektów bez naturalnego właściciela, wymaga wiedzy spoza agregatu albo jest pojęciem z języka ekspertów (np. kalkulacja odpowiedzialności za szkodę). Jest sygnałem anemii, gdy większość logiki trafia do serwisów typu `ReservationService` czy `RentalManager`, a encje mają tylko gettery i settery. Test: jeśli reguła dotyczy stanu jednego obiektu, należy do tego obiektu.

Zobacz: sekcja „Reguła bez domu”.

</details>

### 33. Po co są fabryki w DDD i kiedy wystarczy zwykły konstruktor?

<details>
<summary>Odpowiedź</summary>

Fabryka tworzy złożony obiekt domeny w poprawnym stanie. Jest potrzebna, gdy tworzenie ma kilka kroków lub danych z różnych źródeł, trzeba wybrać konkretny typ, tworzenie jest pojęciem domeny (zawarcie umowy z rezerwacji) albo odtwarzanie z bazy ma inne reguły niż tworzenie nowego obiektu. Konstruktor wystarcza przy kilku polach i prostej walidacji. Zwykle wystarcza metoda fabrykująca, a osobna klasa fabryki ma sens, gdy tworzenie wymaga zależności.

Zobacz: sekcja „Budowanie złożonych obiektów”.

</details>

### 34. Czym repozytorium w DDD różni się od DAO i generycznego repozytorium CRUD?

<details>
<summary>Odpowiedź</summary>

Repozytorium DDD udaje kolekcję całych agregatów, istnieje tylko dla korzeni, a jego interfejs należy do modelu i ma metody z języka domeny (`get`, `add`, `active_for_vehicle`). DAO operuje na wierszach tabel (`insert`, `update`, `select_by_x`), jedno na tabelę, w warstwie danych. Generyczne repozytorium CRUD (`find_all`, `delete`) łamie model: pozwala usuwać to, czego biznes nie usuwa, pobierać wszystko bez potrzeby i zapisywać encje wewnętrzne z pominięciem korzenia.

Zobacz: sekcja „Kolekcja, a nie tabela”.

</details>
