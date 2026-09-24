# Warstwy we frameworkach

Mało kto buduje architekturę warstwową od zera. Zwykle robi to framework: Django, Spring, ASP.NET MVC albo Rails. Każdy z nich ma własne nazwy i własne domyślne miejsca na kod, a te nie zawsze pokrywają się z warstwami z podręcznika. Ten rozdział pokazuje, jak warstwy wyglądają w popularnych frameworkach i jakie problemy wynikają z ich domyślnych wyborów.

```text
warstwa             Django                   Spring                     ASP.NET MVC
prezentacja         views, templates, forms  @Controller, DTO, Thymeleaf Controller, Razor, ViewModel
serwisy             (brak, trzeba dodać)     @Service, @Transactional   Services (konwencja)
logika              models.Model (metody)    encje lub serwisy          encje lub serwisy
dostęp do danych    ORM, managers, QuerySet  @Repository, Spring Data   DbContext, EF Core
```

## Nazwy frameworków a warstwy

Większość frameworków webowych opiera się na <a id="term-mvc"></a>[Model–View–Controller](00%20Glossary%20Layered.md#mvc) (MVC). MVC to wzorzec warstwy prezentacji, a nie architektura całej aplikacji. Kontroler przyjmuje żądanie, widok renderuje odpowiedź, a model to dane, które widok pokazuje. Framework nie mówi, gdzie są reguły biznesowe, więc zespół musi o tym zdecydować.

Django nazywa swój wariant MTV (Model–Template–View). Widok Django pełni rolę kontrolera, szablon rolę widoku, a model to klasa ORM:

| Element Django | Warstwa | Uwagi |
|---|---|---|
| `urls.py`, `views.py` | prezentacja | przyjmuje żądanie, wybiera odpowiedź |
| `templates/`, serializery DRF | prezentacja | format odpowiedzi |
| `forms.py` | prezentacja | walidacja formatu, często niesłusznie też reguł |
| `models.py` (pola) | dostęp do danych | mapowanie na tabele |
| `models.py` (metody) | logika | reguły, jeśli zespół je tam umieszcza |
| `Manager`, `QuerySet` | dostęp do danych | zapytania |
| brak | serwisy | Django nie ma warstwy serwisów, zespoły dodają `services.py` |

Spring ma warstwy wprost w adnotacjach: `@Controller` albo `@RestController` to prezentacja, `@Service` to serwisy, `@Repository` to dostęp do danych, a `@Transactional` zwykle stoi na metodach serwisu. ASP.NET MVC ma kontrolery i widoki Razor, a warstwę serwisów i repozytoria dodaje się konwencją. `DbContext` z Entity Framework Core bywa używany bezpośrednio jako repozytorium i Unit of Work.

## Gdzie trafia logika bez serwisów

Gdy framework nie ma warstwy serwisów, logika musi gdzieś trafić. Zwykle trafia do jednego z dwóch miejsc.

<a id="term-fat-controller"></a>[Gruby kontroler](00%20Glossary%20Layered.md#fat-controller) (fat controller, fat view) to kontroler albo widok, który zawiera logikę biznesową, zapytania i formatowanie naraz:

```python
# views.py: gruby widok
def book_appointment(request):
    doctor = Doctor.objects.get(id=request.POST["doctor_id"])
    starts_at = parse_datetime(request.POST["starts_at"])
    if starts_at.hour < doctor.works_from or starts_at.hour >= doctor.works_to:
        return JsonResponse({"error": "Poza godzinami pracy"}, status=422)
    if Appointment.objects.filter(doctor=doctor, starts_at=starts_at).exists():
        return JsonResponse({"error": "Termin zajęty"}, status=409)
    if Appointment.objects.filter(patient=request.user.patient, starts_at__gt=now()).count() >= 3:
        return JsonResponse({"error": "Za dużo wizyt"}, status=422)
    a = Appointment.objects.create(doctor=doctor, patient=request.user.patient, starts_at=starts_at)
    send_mail("Wizyta umówiona", ..., [request.user.email])
    return JsonResponse({"id": a.id}, status=201)
```

<a id="term-fat-model"></a>[Gruby model](00%20Glossary%20Layered.md#fat-model) to klasa ORM z dziesiątkami metod biznesowych, która łączy mapowanie na tabelę, reguły, zapytania i często efekty uboczne. Django przez lata zalecało „fat models, thin views”, czyli gruby model i cienki widok.

```python
# models.py: gruby model
class Appointment(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.PROTECT)
    patient = models.ForeignKey(Patient, on_delete=models.PROTECT)
    starts_at = models.DateTimeField()

    @classmethod
    def book(cls, doctor, patient, starts_at):
        if not doctor.is_working_at(starts_at): raise OutsideWorkingHours()
        if cls.objects.filter(doctor=doctor, starts_at=starts_at).exists(): raise SlotTaken()
        if patient.upcoming_count() >= 3: raise TooManyAppointments()
        appointment = cls.objects.create(doctor=doctor, patient=patient, starts_at=starts_at)
        send_mail(...)                                   # efekt uboczny w modelu
        return appointment
```

Który jest mniejszym złem? Gruby model. Reguły są przy danych, więc widok WWW, API i polecenie CLI używają tej samej logiki. Gruby kontroler zamyka logikę w jednym punkcie wejścia, więc każdy inny punkt wejścia ją kopiuje albo omija.

Gruby model ma jednak własne problemy: klasa rośnie do tysięcy linii, łączy logikę z ORM-em (testy wymagają bazy), a efekty uboczne w `save()` albo w sygnałach są trudne do śledzenia. Przywracanie porządku zwykle przebiega tak:

1. Z grubego kontrolera przenieś logikę do funkcji serwisu (`services.py`). Widok zostaje z parsowaniem i formatowaniem.
2. Z grubego modelu przenieś przypadki użycia i efekty uboczne do serwisów. W modelu zostaw reguły dotyczące jednego obiektu (`appointment.can_be_cancelled(now)`).
3. Zapytania powtarzane w wielu miejscach przenieś do managerów, QuerySetów albo repozytoriów.
4. Wprowadź regułę, że zapis przechodzi przez serwis, i pilnuj jej testem architektury.

Popularny w społeczności Django „Django Styleguide” HackSoftu proponuje właśnie taki podział: `services` do zapisu, `selectors` do odczytu, cienkie widoki i modele z prostymi regułami.

## Mapowanie tabel w środku warstw

<a id="term-orm"></a>[Object-Relational Mapper](00%20Glossary%20Layered.md#orm) (ORM) mapuje tabele na obiekty. W architekturze warstwowej należy do warstwy dostępu do danych, ale w praktyce jego klasy przenikają wszystkie warstwy.

Są dwa główne wzorce ORM opisane przez Fowlera:

<a id="term-active-record"></a>[Active Record](00%20Glossary%20Layered.md#active-record): obiekt odpowiada wierszowi tabeli i sam się zapisuje (`appointment.save()`). Tak działają Django ORM, Rails ActiveRecord i Laravel Eloquent.

<a id="term-data-mapper"></a>[Data Mapper](00%20Glossary%20Layered.md#data-mapper): obiekty domeny nie wiedzą o bazie, a osobny mapper przenosi dane między nimi a tabelami. Tak działają SQLAlchemy (w trybie mapowania imperatywnego), Hibernate i Entity Framework w dużej mierze.

Gdy model ORM jest jednocześnie modelem biznesowym, co jest normą przy Active Record, pojawiają się konsekwencje:

- warstwa logiki zależy od ORM-a, więc testy reguł wymagają bazy albo skomplikowanych mocków,
- klasy biznesowe dziedziczą ograniczenia ORM-a: wymagane konstruktory, mutowalne pola, lazy loading relacji,
- schemat bazy i model biznesowy muszą mieć ten sam kształt, więc zmiana jednego wymusza zmianę drugiego,
- obiekty biznesowe mogą wykonać zapytanie w dowolnym momencie (`appointment.doctor.schedule`), co ukrywa koszt i prowadzi do problemu N+1 (rozdział 05),
- warstwa prezentacji dostaje obiekty, które potrafią zapisać się do bazy, więc granica między warstwami jest umowna.

Dla aplikacji z prostą logiką to akceptowalny kompromis, bo Active Record jest szybki w pisaniu i czytelny. Dla złożonej logiki zespoły oddzielają model biznesowy od modelu ORM, co opisuje tutorial [hexagonal](../Hexagonal/), albo przynajmniej trzymają reguły w metodach, które nie wykonują zapytań.

## Co zapamiętać

- MVC to wzorzec warstwy prezentacji, a nie architektura całej aplikacji. Django nazywa go MTV.
- Django nie ma warstwy serwisów, Spring ma ją w adnotacjach, a w ASP.NET MVC dodaje się ją konwencją.
- Gruby kontroler zamyka logikę w jednym punkcie wejścia. Gruby model jest mniejszym złem, ale rośnie i miesza reguły z ORM-em.
- Porządek przywraca się przez serwisy do przypadków użycia, proste reguły w modelu i zapytania w managerach lub repozytoriach.
- ORM należy do dostępu do danych, ale przy Active Record jego klasy są modelem biznesowym.
- Model ORM jako model biznesowy wiąże reguły z bazą, schemat z modelem i ukrywa koszt zapytań.

## Pytania sprawdzające

### 11. Jak architektura warstwowa wygląda w Django, Spring albo ASP.NET MVC? Które elementy frameworka należą do której warstwy?

<details>
<summary>Odpowiedź</summary>

W Django widoki, szablony, formularze i serializery to prezentacja, pola modeli, managery i QuerySety to dostęp do danych, metody modeli bywają logiką, a warstwy serwisów brak, więc zespoły dodają `services.py`. W Springu `@Controller` to prezentacja, `@Service` z `@Transactional` to serwisy, a `@Repository` i Spring Data to dostęp do danych. W ASP.NET MVC kontrolery i Razor to prezentacja, serwisy i repozytoria dodaje się konwencją, a `DbContext` bywa repozytorium i Unit of Work. MVC (w Django MTV) to wzorzec prezentacji, a nie całej architektury.

Zobacz: sekcja „Nazwy frameworków a warstwy”.

</details>

### 12. Czym są fat model i fat controller? Który z nich jest mniejszym złem i jak przywrócić porządek?

<details>
<summary>Odpowiedź</summary>

Fat controller to kontroler lub widok z logiką, zapytaniami i formatowaniem naraz. Fat model to klasa ORM z dziesiątkami metod biznesowych, zapytań i efektów ubocznych. Mniejszym złem jest gruby model, bo reguły są wspólne dla wszystkich punktów wejścia, ale klasa rośnie, wiąże logikę z ORM-em i ukrywa efekty uboczne. Porządek: logika z widoków do serwisów, przypadki użycia i efekty uboczne z modeli do serwisów, proste reguły jednego obiektu w modelu, powtarzane zapytania w managerach lub repozytoriach, a zapis tylko przez serwis pilnowany testem architektury.

Zobacz: sekcja „Gdzie trafia logika bez serwisów”.

</details>

### 13. Gdzie w architekturze warstwowej leży ORM i jakie konsekwencje ma to, że modele ORM są jednocześnie modelem biznesowym?

<details>
<summary>Odpowiedź</summary>

ORM należy do warstwy dostępu do danych, ale przy Active Record (Django, Rails) jego klasy są jednocześnie modelem biznesowym, a przy Data Mapper (SQLAlchemy imperatywnie, Hibernate) mogą być oddzielone. Konsekwencje połączenia: testy reguł wymagają bazy, klasy biznesowe dziedziczą ograniczenia ORM-a, schemat i model muszą mieć ten sam kształt, obiekty mogą wykonać zapytanie w dowolnym momencie (N+1), a prezentacja dostaje obiekty zdolne do zapisu. Dla prostej logiki to akceptowalny kompromis, a dla złożonej lepiej oddzielić model od ORM-a.

Zobacz: sekcja „Mapowanie tabel w środku warstw”.

</details>
