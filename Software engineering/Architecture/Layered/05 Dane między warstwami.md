# Dane między warstwami

Warstwy komunikują się, przekazując sobie dane. W aplikacji warstwowej najłatwiej przekazywać wszędzie te same obiekty ORM: repozytorium zwraca model, serwis go zmienia, a widok renderuje. To wygodne, ale ma ukryte koszty. Ten rozdział opisuje, co może pójść źle, kiedy warto wprowadzić osobne obiekty transferowe i skąd bierze się najczęstszy problem wydajności w aplikacjach warstwowych.

```text
bez DTO:     baza ──► Appointment (ORM) ──► serwis ──► Appointment (ORM) ──► szablon / JSON
                         lazy relacje, wszystkie pola, metoda save() dostępna wszędzie

z DTO:       baza ──► Appointment (ORM) ──► serwis ──► AppointmentView (DTO) ──► szablon / JSON
                                                       tylko potrzebne pola, bez dostępu do bazy
```

## Encje ORM w widoku

Przekazanie obiektów ORM do warstwy prezentacji jest normą w Django i Rails. W małej aplikacji działa dobrze. Z czasem pojawiają się problemy.

Pierwszy problem to <a id="term-lazy-loading"></a>[lazy loading](00%20Glossary%20Layered.md#lazy-loading), czyli leniwe ładowanie relacji. ORM ładuje powiązane obiekty dopiero przy pierwszym dostępie. Szablon, który wyświetla `appointment.doctor.name`, wykonuje zapytanie do bazy w trakcie renderowania, choć warstwa prezentacji nie powinna rozmawiać z bazą. W Javie ten problem ma nazwę: <a id="term-open-session-in-view"></a>[Open Session in View](00%20Glossary%20Layered.md#open-session-in-view). Sesja Hibernate jest otwarta aż do końca renderowania, żeby leniwe relacje działały w widoku. Spring Boot włącza to domyślnie i wypisuje ostrzeżenie w logach. Bez tego widok rzuca `LazyInitializationException`, a z tym wykonuje ukryte zapytania poza transakcją serwisu.

Drugi problem to przeciekanie pól. Serializer, który zwraca model w całości (`fields = "__all__"` w DRF), wysyła do klienta wszystko, co jest w tabeli: notatki lekarza, dane wewnętrzne, a po dodaniu nowej kolumny także ją, bez decyzji, czy powinna być widoczna.

Trzeci problem to sprzężenie widoku ze schematem. Zmiana nazwy kolumny w bazie zmienia pole w modelu, a to zmienia API i szablony. Klienci API zależą od struktury tabel.

Czwarty problem to obiekty zdolne do zapisu w prezentacji. Szablon albo widok może wywołać `appointment.save()` albo zmienić pole, omijając serwis i jego reguły.

```python
# views.py: ORM do szablonu
def my_appointments(request):
    appointments = Appointment.objects.filter(patient=request.user.patient)
    return render(request, "appointments.html", {"appointments": appointments})

# appointments.html: każda iteracja to dodatkowe zapytania
# {% for a in appointments %}
#   {{ a.doctor.name }} {{ a.doctor.specialization.name }} {{ a.clinic.address }}
# {% endfor %}
```

## Obiekty transferowe

<a id="term-dto"></a>[DTO](00%20Glossary%20Layered.md#dto) (Data Transfer Object) to prosty obiekt bez zachowania, który przenosi dane między warstwami. Zawiera tylko pola potrzebne odbiorcy, nie ma relacji ładowanych leniwie i nie potrafi się zapisać.

```python
@dataclass(frozen=True)
class AppointmentView:                      # DTO dla ekranu „Moje wizyty”
    id: int
    starts_at: datetime
    doctor_name: str
    specialization: str
    clinic_address: str
    can_cancel: bool                        # decyzja policzona w serwisie, a nie w szablonie


class AppointmentQueries:
    def for_patient(self, patient_id: int, now: datetime) -> list[AppointmentView]:
        rows = (Appointment.objects
                .filter(patient_id=patient_id, starts_at__gte=now)
                .select_related("doctor__specialization", "clinic"))
        return [AppointmentView(
                    id=a.id, starts_at=a.starts_at, doctor_name=a.doctor.name,
                    specialization=a.doctor.specialization.name,
                    clinic_address=a.clinic.address,
                    can_cancel=a.starts_at - now > timedelta(hours=24),
                ) for a in rows]
```

Tłumaczenie między modelem ORM a DTO wykonuje <a id="term-mapper"></a>[mapper](00%20Glossary%20Layered.md#mapper): funkcja albo klasa, która przepisuje pola. Mapowanie może być ręczne (jak wyżej), przez serializer (DRF, Pydantic z `from_attributes=True`) albo przez bibliotekę (MapStruct w Javie, AutoMapper w .NET).

Kiedy DTO jest potrzebne:

- API publiczne albo używane przez inne zespoły, bo kontrakt nie może zależeć od schematu bazy,
- dane wrażliwe w modelu, bo DTO jawnie określa, co wychodzi na zewnątrz,
- ekran łączy dane z wielu modeli albo zawiera pola wyliczone,
- warstwa prezentacji nie powinna mieć dostępu do bazy, np. w aplikacji z zadaniami w tle i kolejkami, gdzie obiekt przechodzi przez serializację.

Kiedy DTO to niepotrzebne mapowanie:

- panel administracyjny albo wewnętrzny CRUD, w którym ekran pokazuje dokładnie pola tabeli,
- DTO jest kopią modelu 1:1 i zmienia się przy każdej zmianie modelu. Wtedy nie izoluje niczego, tylko podwaja kod,
- mapowanie przez trzy warstwy (ORM do DTO serwisu, do DTO API, do view modelu), gdzie każdy obiekt ma te same pola.

Rozsądny kompromis: DTO na granicy z klientem (API, szablony dla zewnętrznych użytkowników), a modele ORM wewnątrz serwisów i logiki.

## Zapytania w pętli

<a id="term-n-plus-one"></a>[Problem N+1](00%20Glossary%20Layered.md#n-plus-one) to sytuacja, w której aplikacja wykonuje jedno zapytanie po listę N obiektów, a potem po jednym dodatkowym zapytaniu dla każdego z nich, żeby pobrać powiązane dane. Lista 50 wizyt z nazwiskiem lekarza i adresem przychodni to 1 + 50 + 50 = 101 zapytań zamiast jednego.

W aplikacjach warstwowych N+1 pojawia się często, bo warstwy ukrywają przed sobą, co robią:

- repozytorium zwraca listę modeli bez załadowanych relacji, bo nie wie, czego potrzebuje ekran,
- serwis w pętli wywołuje metodę modelu, która czyta relację (`appointment.doctor.is_available()`),
- szablon albo serializer w pętli sięga po relacje (`a.doctor.name`),
- każda warstwa osobno wygląda poprawnie, a problem widać dopiero w logach zapytań.

Gdzie go rozwiązywać? W warstwie, która wie, jakie dane będą potrzebne, czyli najczęściej w zapytaniu dla konkretnego przypadku użycia, a nie w szablonie.

| Narzędzie | Django | Spring / JPA | Kiedy |
|---|---|---|---|
| JOIN dla relacji „jeden” | `select_related("doctor")` | `JOIN FETCH`, `@EntityGraph` | klucz obcy, relacja jeden-do-jednego |
| osobne zapytanie dla relacji „wiele” | `prefetch_related("tags")` | `@BatchSize`, osobne zapytanie | relacje jeden-do-wielu, wiele-do-wielu |
| projekcja tylko potrzebnych pól | `values()`, `only()`, adnotacje | projekcje interfejsowe, DTO w JPQL | listy, raporty |
| zapytanie pod ekran | selector lub query zwracający DTO | query service z DTO | ekrany łączące wiele modeli |

```python
# N+1: 1 zapytanie o wizyty + N o lekarzy + N o przychodnie
for a in Appointment.objects.filter(patient_id=patient_id):
    print(a.doctor.name, a.clinic.address)

# 1 zapytanie z JOIN-ami
for a in Appointment.objects.filter(patient_id=patient_id).select_related("doctor", "clinic"):
    print(a.doctor.name, a.clinic.address)
```

Zapobieganie jest łatwiejsze niż wykrywanie. Pomagają testy, które liczą zapytania (`assertNumQueries` w Django, `django-assert-num-queries`, Hibernate Statistics), narzędzia w trybie deweloperskim (Django Debug Toolbar, nplusone) i DTO zamiast modeli w prezentacji, bo DTO nie ma leniwych relacji, więc szablon nie może niczego doładować.

## Co zapamiętać

- Modele ORM w prezentacji dają lazy loading w widoku (Open Session in View), przeciekanie pól, sprzężenie API ze schematem i możliwość zapisu z pominięciem serwisu.
- DTO przenosi tylko potrzebne dane, bez relacji i bez zapisu. Mapper tłumaczy model na DTO.
- DTO warto stosować na granicy z klientem i przy danych wrażliwych, ale nie jako kopię modelu 1:1 w każdej warstwie.
- N+1 to jedno zapytanie po listę i N po relacje. Warstwy ukrywają go przed sobą.
- N+1 rozwiązuje się w zapytaniu dla konkretnego przypadku użycia: `select_related`, `prefetch_related`, projekcje, DTO.
- Testy liczące zapytania i DTO w prezentacji zapobiegają N+1, zanim trafi na produkcję.

## Pytania sprawdzające

### 14. Czy encje ORM mogą trafiać do warstwy prezentacji? Jakie problemy to powoduje (lazy loading, przeciekanie pól, sprzężenie widoku ze schematem)?

<details>
<summary>Odpowiedź</summary>

Mogą i w małych aplikacjach to norma, ale z czasem powoduje problemy. Lazy loading wykonuje zapytania w trakcie renderowania, a w Javie wymaga Open Session in View albo kończy się `LazyInitializationException`. Serializacja całego modelu wysyła do klienta wszystkie pola, także wewnętrzne i nowo dodane. API i szablony zależą od schematu bazy. Prezentacja dostaje obiekty, które mogą się zapisać z pominięciem serwisu i jego reguł.

Zobacz: sekcja „Encje ORM w widoku”.

</details>

### 15. Kiedy warto wprowadzić DTO między warstwami, a kiedy to niepotrzebne mapowanie?

<details>
<summary>Odpowiedź</summary>

Warto przy API publicznym lub używanym przez inne zespoły, przy danych wrażliwych w modelu, gdy ekran łączy wiele modeli lub pola wyliczone, i gdy prezentacja nie powinna mieć dostępu do bazy. Niepotrzebne w panelu administracyjnym i wewnętrznym CRUD-zie, gdy DTO jest kopią modelu 1:1 zmienianą razem z nim, i przy mapowaniu przez kilka warstw obiektów o identycznych polach. Kompromis: DTO na granicy z klientem, a modele ORM wewnątrz serwisów i logiki.

Zobacz: sekcja „Obiekty transferowe”.

</details>

### 16. Skąd bierze się problem N+1 w aplikacjach warstwowych i w której warstwie należy go rozwiązywać?

<details>
<summary>Odpowiedź</summary>

N+1 to jedno zapytanie po listę i N dodatkowych po relacje każdego elementu. W aplikacjach warstwowych powstaje, bo warstwy ukrywają przed sobą, co robią: repozytorium nie ładuje relacji, serwis i szablon sięgają po nie w pętli, a każda warstwa osobno wygląda poprawnie. Rozwiązuje się go w warstwie, która wie, jakich danych potrzeba, czyli w zapytaniu dla konkretnego przypadku użycia (`select_related`, `prefetch_related`, `JOIN FETCH`, projekcje, DTO), a nie w szablonie. Zapobiegają mu testy liczące zapytania i DTO w prezentacji.

Zobacz: sekcja „Zapytania w pętli”.

</details>
