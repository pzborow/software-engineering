# Reguły zależności

Warstwy mają sens tylko wtedy, gdy przestrzega się kierunku zależności. Jeśli repozytorium zacznie wołać serwis, a logika biznesowa importować widoki, podział na katalogi zostanie, ale jego korzyści znikną. Ten rozdział opisuje reguły, które utrzymują warstwy w porządku, i narzędzia, które je pilnują.

```text
dozwolone:                             zakazane:

views ──► services                     repositories ──► services
services ──► domain                    domain ──► views
services ──► repositories              repositories ──► views
domain ──► (nic z warstw wyższych)     services ──► views
```

## Zależność tylko w dół

Podstawowa reguła architektury warstwowej: warstwa może zależeć tylko od warstw leżących niżej. Warstwa niższa nie może znać warstwy wyższej, nie importuje jej modułów i nie wie, kto ją wywołuje.

Dlaczego to takie ważne:

- warstwę niższą można użyć z wielu wyższych. Serwis rezerwacji obsłuży widok WWW, API, polecenie CLI i zadanie Celery, jeśli nie wie, który z nich go woła,
- zmiana warstwy wyższej nie psuje niższych. Przebudowa widoków nie wymaga dotykania logiki,
- warstwy niższe da się testować i rozumieć bez wyższych,
- zależności tworzą drzewo, a nie sieć, więc łatwo przewidzieć skutki zmian.

Najczęstsze naruszenie to warstwa niższa, która potrzebuje czegoś z wyższej:

```python
# services/appointments.py: źle, serwis zna HTTP
from django.http import HttpRequest, Http404

class AppointmentService:
    def book(self, request: HttpRequest) -> int:
        doctor_id = int(request.POST["doctor_id"])        # serwis parsuje żądanie
        if not Doctor.objects.filter(id=doctor_id).exists():
            raise Http404                                 # serwis zna kody HTTP
        ...


# dobrze: serwis przyjmuje dane domenowe, rzuca wyjątki domenowe
class AppointmentService:
    def book(self, patient_id: int, doctor_id: int, starts_at: datetime) -> int:
        doctor = self._doctors.get(doctor_id)             # rzuca DoctorNotFound
        ...
```

## Warstwy zamknięte i otwarte

Czy widok może zawołać repozytorium bezpośrednio, pomijając serwis? Odpowiedź zależy od przyjętego wariantu.

W <a id="term-strict-layering"></a>[ścisłym warstwowaniu](00%20Glossary%20Layered.md#strict-layering) każda warstwa korzysta tylko z warstwy bezpośrednio pod nią. Widok woła serwis, serwis woła logikę i repozytoria, a pominięcie warstwy jest zabronione.

W <a id="term-relaxed-layering"></a>[luźnym warstwowaniu](00%20Glossary%20Layered.md#relaxed-layering) warstwa może korzystać z dowolnej niższej warstwy. Widok może pobrać listę lekarzy bezpośrednio z repozytorium, bez przechodzenia przez serwis.

Mark Richards w książce „Software Architecture Patterns” proponuje określać to per warstwa. <a id="term-closed-layer"></a>[Warstwa zamknięta](00%20Glossary%20Layered.md#closed-layer) musi być przejściem dla każdego żądania. <a id="term-open-layer"></a>[Warstwa otwarta](00%20Glossary%20Layered.md#open-layer) może być pominięta. Typowy układ: warstwa serwisów zamknięta dla operacji zapisu, ale otwarta dla prostych odczytów.

| | Ścisłe (warstwy zamknięte) | Luźne (warstwy otwarte) |
|---|---|---|
| Izolacja | pełna, zmiana warstwy dotyka tylko sąsiada | słabsza, wyższe warstwy znają wiele niższych |
| Kod przelotowy | dużo, serwisy tylko przekazują wywołania | mało |
| Przewidywalność | wysoka, jedna droga dla każdego żądania | niższa, różne ścieżki dla podobnych operacji |
| Ryzyko | ceremonia i sinkhole anti-pattern (rozdział 07) | logika rozlana po widokach, pominięte reguły |

Kiedy pominięcie warstwy jest akceptowalne:

- proste odczyty bez reguł: lista specjalizacji, słownik oddziałów, grafik do wyświetlenia,
- raporty i eksporty, które czytają dane bez decyzji.

Kiedy nie jest akceptowalne:

- każda operacja zapisu, bo pominie reguły biznesowe i granicę transakcji,
- odczyty, które wymagają uprawnień albo filtrowania według reguł (pacjent widzi tylko swoje wizyty).

Najbezpieczniejsza umowa: zapis zawsze przez serwis, odczyt może iść na skróty, jeśli nie ma w nim reguł. Taka umowa jest w praktyce zalążkiem CQRS, opisanym w tutorialu [cqrs](../CQRS/).

## Cykle i automatyczne pilnowanie

<a id="term-dependency-cycle"></a>[Cykl zależności](00%20Glossary%20Layered.md#dependency-cycle) powstaje, gdy warstwa niższa zaczyna zależeć od wyższej. Typowe przypadki w aplikacji warstwowej:

- repozytorium woła serwis, np. `AppointmentRepository.save()` wysyła powiadomienie przez `NotificationService`,
- model ORM importuje serwis w metodzie `save()` albo w sygnale,
- serwis A woła serwis B, który woła serwis A. To cykl w obrębie jednej warstwy, ale z tymi samymi skutkami,
- warstwa logiki importuje formularz albo serializer, żeby „użyć tej samej walidacji”.

W Pythonie cykle często ujawniają się jako `ImportError` przy częściowo zainicjalizowanym module. Wtedy ktoś „naprawia” je importem wewnątrz funkcji, co ukrywa problem zamiast go usunąć.

Jak rozbić cykl:

1. Przenieś wspólny kod niżej. Jeśli repozytorium i serwis potrzebują tej samej funkcji, należy ona do warstwy niższej od obu.
2. Odwróć kierunek przez zdarzenie albo callback. Repozytorium nie woła serwisu powiadomień. Serwis po zapisie publikuje zdarzenie albo sam wywołuje powiadomienie.
3. Wydziel interfejs w warstwie niższej, który implementuje warstwa wyższa. To odwrócenie zależności, czyli zalążek architektury heksagonalnej.

Reguły zależności pilnuje się automatycznie. W Pythonie służy do tego `import-linter`, który jest <a id="term-architecture-test"></a>[testem architektury](00%20Glossary%20Layered.md#architecture-test) uruchamianym w CI:

```toml
# pyproject.toml
[tool.importlinter]
root_package = "clinic"

[[tool.importlinter.contracts]]
name = "Warstwy przychodni"
type = "layers"
layers = [
    "clinic.presentation",
    "clinic.services",
    "clinic.domain",
    "clinic.repositories",
]

[[tool.importlinter.contracts]]
name = "Logika nie zna Django HTTP"
type = "forbidden"
source_modules = ["clinic.domain", "clinic.services"]
forbidden_modules = ["django.http", "django.shortcuts", "rest_framework"]
```

Kontrakt `layers` domyślnie pozwala warstwie korzystać z każdej niższej, czyli realizuje luźne warstwowanie. Pomijanie warstw można dodatkowo zablokować kontraktem `forbidden`. W Javie tę samą rolę pełni ArchUnit (`layeredArchitecture().whereLayer(...).mayOnlyBeAccessedByLayers(...)`), a w .NET NetArchTest.

W kontrakcie `clinic.domain` leży nad `clinic.repositories`, czyli logika zależy od repozytoriów. To klasyczny układ warstwowy. Rozdział 08 pokazuje, co się zmienia, gdy tę jedną zależność odwrócić.

## Co zapamiętać

- Warstwa zależy tylko od warstw niższych. Niższa nie zna wyższej, dzięki czemu obsłuży wiele wywołujących.
- Ścisłe warstwowanie zakazuje pomijania warstw, a luźne pozwala korzystać z dowolnej niższej.
- Richards opisuje warstwy zamknięte i otwarte. Rozsądna umowa: zapis zawsze przez serwis, proste odczyty mogą iść na skróty.
- Cykle powstają, gdy warstwa niższa woła wyższą. Rozbija się je przeniesieniem kodu niżej, zdarzeniem albo interfejsem.
- `import-linter`, ArchUnit i NetArchTest zamieniają reguły warstw w test w CI.

## Pytania sprawdzające

### 8. Jaki jest kierunek zależności między warstwami i dlaczego warstwa niższa nie może znać wyższej?

<details>
<summary>Odpowiedź</summary>

Zależności wskazują w dół: warstwa może używać tylko warstw niższych. Niższa nie importuje wyższej i nie wie, kto ją woła. Dzięki temu warstwa niższa obsłuży wielu wywołujących (web, API, CLI, zadania w tle), zmiana warstwy wyższej jej nie psuje, można ją testować i rozumieć osobno, a zależności tworzą drzewo zamiast sieci. Typowe naruszenie to serwis przyjmujący `HttpRequest` albo rzucający `Http404`.

Zobacz: sekcja „Zależność tylko w dół”.

</details>

### 9. Czym różni się ścisłe warstwowanie (strict) od luźnego (relaxed)? Kiedy warstwa może pominąć warstwę pośrednią?

<details>
<summary>Odpowiedź</summary>

Ścisłe warstwowanie pozwala korzystać tylko z warstwy bezpośrednio niżej: pełna izolacja i jedna droga dla żądania, ale dużo kodu przelotowego. Luźne pozwala korzystać z każdej niższej warstwy: mniej ceremonii, ale słabsza izolacja i ryzyko rozlania logiki. Richards opisuje warstwy zamknięte (obowiązkowe) i otwarte (do pominięcia). Pominięcie jest akceptowalne dla prostych odczytów bez reguł i raportów, a nieakceptowalne dla zapisów i odczytów z uprawnieniami. Bezpieczna umowa: zapis zawsze przez serwis.

Zobacz: sekcja „Warstwy zamknięte i otwarte”.

</details>

### 10. Jak wykryć i usunąć cykle zależności między warstwami (np. repozytorium wołające serwis) i jak pilnować granic automatycznie?

<details>
<summary>Odpowiedź</summary>

Cykle powstają, gdy warstwa niższa woła wyższą: repozytorium wysyła powiadomienia przez serwis, model ORM importuje serwis w `save()`, serwisy wołają się nawzajem, logika importuje formularze. W Pythonie ujawniają się jako `ImportError`, często maskowany importem w funkcji. Usuwa się je, przenosząc wspólny kod niżej, odwracając kierunek przez zdarzenie lub callback albo wydzielając interfejs w warstwie niższej. Granic pilnuje automatycznie `import-linter` (kontrakty `layers` i `forbidden`), ArchUnit lub NetArchTest w CI.

Zobacz: sekcja „Cykle i automatyczne pilnowanie”.

</details>
