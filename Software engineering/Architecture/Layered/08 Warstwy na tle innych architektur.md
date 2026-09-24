# Warstwy na tle innych architektur

Architektura warstwowa jest punktem odniesienia dla większości nowszych podejść. Hexagonal, onion i clean poprawiają jej kierunek zależności. Vertical slice kwestionuje sam podział na warstwy techniczne. <a id="term-modular-monolith"></a>[Modularny monolit](00%20Glossary%20Layered.md#modular-monolith) i DDD dzielą system w innym wymiarze, a warstwy mogą istnieć w środku każdego modułu. Ten rozdział porównuje te podejścia i pokazuje, co dokładnie każde z nich zmienia.

```text
podejście                 czym dzieli kod                   co zmienia względem warstw
layered                   poziomo, według rodzaju kodu      punkt odniesienia
hexagonal, onion, clean   poziomo, rdzeń i otoczenie        odwraca zależność logiki od danych
vertical slice            pionowo, według funkcji           rezygnuje z warstw technicznych
modularny monolit, DDD    pionowo, według obszarów biznesu  warstwy mogą żyć w każdym module
```

## Odwrócenie jednej strzałki

W architekturze warstwowej logika zależy od warstwy dostępu do danych. <a id="term-hexagonal-architecture"></a>[Architektura heksagonalna](00%20Glossary%20Layered.md#hexagonal-architecture), a także onion i clean, odwracają dokładnie tę jedną zależność: logika definiuje interfejs, którego potrzebuje (port, repozytorium), a warstwa danych go implementuje. To zastosowanie <a id="term-dependency-inversion"></a>[zasady odwrócenia zależności](00%20Glossary%20Layered.md#dependency-inversion) (Dependency Inversion Principle) do całej aplikacji.

```text
Layered:                                     Hexagonal / onion / clean:

prezentacja ──► logika ──► dostęp do danych   prezentacja ──► logika ◄── dostęp do danych
                                                                │
                                              logika definiuje interfejs AppointmentRepository,
                                              dostęp do danych go implementuje
```

```python
# layered: logika importuje konkretne repozytorium z warstwy niżej
from clinic.repositories import AppointmentRepository

class AppointmentService:
    def __init__(self):
        self._repo = AppointmentRepository()


# hexagonal: logika definiuje interfejs, implementacja jest na zewnątrz
class Appointments(Protocol):                    # w warstwie logiki
    def upcoming_count(self, patient_id: int) -> int: ...
    def add(self, appointment: Appointment) -> None: ...

class AppointmentService:
    def __init__(self, appointments: Appointments):
        self._appointments = appointments        # dowolna implementacja: SQL, pamięć, fake
```

Konsekwencje tej jednej zmiany:

| | Layered | Hexagonal / onion / clean |
|---|---|---|
| Kierunek zależności logiki | w stronę bazy | baza w stronę logiki |
| Test reguł | zwykle z bazą | z fake'iem w pamięci |
| Wymiana bazy lub ORM-a | dotyka logiki | tylko nowy adapter |
| Kto definiuje interfejs danych | warstwa danych | warstwa logiki |
| Typy ORM w logice | tak, zwykle | nie |
| Liczba elementów | mniej | więcej: interfejsy, adaptery, mapowanie |

Różnice między samymi hexagonal, onion i clean dotyczą nazw i szczegółowości: portów i adapterów, pierścieni, kręgów i boundaries. Mechanizm jest wspólny. Szczegóły są w tutorialach [hexagonal](../Hexagonal/), [onion](../Onion/) i [clean](../Clean/).

## Pionowe plasterki

<a id="term-vertical-slice"></a>[Vertical slice architecture](00%20Glossary%20Layered.md#vertical-slice) spopularyzował Jimmy Bogard, autor MediatR. Zamiast dzielić kod na warstwy techniczne, dzieli go na funkcje (feature), czyli pionowe plasterki. Każdy plasterek zawiera wszystko, czego potrzebuje jedna operacja: od obsługi żądania, przez logikę, po dostęp do danych.

```text
Warstwy techniczne:                    Pionowe plasterki:

views/                                 features/
├── appointments.py                    ├── book_appointment/
├── doctors.py                         │   ├── endpoint.py
services/                              │   ├── handler.py       logika i zapis
├── appointments.py                    │   └── validator.py
├── doctors.py                         ├── cancel_appointment/
repositories/                          │   ├── endpoint.py
├── appointments.py                    │   └── handler.py
└── doctors.py                         └── doctor_schedule/
                                           ├── endpoint.py
                                           └── query.py         czysty SQL, bez modelu
```

| | Warstwy techniczne | Vertical slice |
|---|---|---|
| Jednostka podziału | rodzaj kodu (widok, serwis, repozytorium) | funkcja biznesowa |
| Zmiana jednej funkcji | wiele katalogów | jeden katalog |
| Sprzężenie | wysokie w warstwie (wspólne serwisy), niskie między warstwami | niskie między plasterkami, wysokie w plasterku |
| Współdzielenie kodu | domyślne, przez wspólne serwisy i repozytoria | celowo ograniczone, duplikacja akceptowana |
| Swoboda techniczna | jedna konwencja dla wszystkiego | każdy plasterek może użyć innego podejścia: ORM, surowy SQL, transaction script, model domeny |
| Ryzyko | serwisy-giganty, sinkhole | duplikacja reguł między plasterkami |

Vertical slice dobrze pasuje do CQRS: każdy plasterek to jedna komenda albo jedno zapytanie. Zapytanie może użyć prostego SQL-a, a komenda bogatego modelu, bez narzucania obu tej samej warstwy. Reguły wspólne dla wielu plasterków przenosi się do modelu domeny współdzielonego przez nie, co łączy vertical slice z DDD.

## Warstwy w modułach

Modularny monolit to jedna wdrażana aplikacja podzielona na moduły według obszarów biznesowych, np. `appointments`, `billing`, `medical_records`. Moduły komunikują się przez publiczne API i nie sięgają do swoich tabel. W DDD takie moduły odpowiadają zwykle <a id="term-bounded-context"></a>[bounded contextom](00%20Glossary%20Layered.md#bounded-context), czyli granicom, w których obowiązuje jeden model i jeden język.

Architektura warstwowa i modularny monolit nie są alternatywami, tylko dzielą system w różnych wymiarach:

- podział na moduły jest pionowy, według obszarów biznesowych,
- podział na warstwy jest poziomy, według rodzaju kodu,
- warstwy mogą istnieć wewnątrz każdego modułu.

```text
clinic/
├── appointments/                  moduł (bounded context „Rejestracja”)
│   ├── api.py                     publiczne API modułu
│   ├── presentation/
│   ├── services/
│   ├── domain/
│   └── repositories/
├── billing/                       moduł (bounded context „Rozliczenia”)
│   ├── api.py
│   ├── services/                  prosty CRUD: dwie warstwy wystarczą
│   └── repositories/
└── medical_records/               moduł z architekturą heksagonalną
    ├── api.py
    ├── domain/
    ├── application/
    └── adapters/
```

Każdy moduł może mieć inną architekturę wewnętrzną, dopasowaną do złożoności. Rozliczenia z prostymi regułami mogą mieć dwie warstwy, rejestracja wizyt klasyczne trzy lub cztery, a dokumentacja medyczna z bogatymi regułami i wymogami audytu architekturę heksagonalną. To samo zalecenie pojawia się w DDD: pełna inwestycja w core domain, prostsze podejście w supporting i generic. Tutorial [ddd](../DDD/) opisuje to szczegółowo.

## Co zapamiętać

- Hexagonal, onion i clean odwracają jedną zależność: logika definiuje interfejs danych, a warstwa danych go implementuje.
- Ta zmiana umożliwia testy reguł bez bazy i wymianę technologii bez dotykania logiki, kosztem większej liczby elementów.
- Vertical slice dzieli kod według funkcji zamiast warstw. Zmiana funkcji dotyka jednego katalogu, a każdy plasterek może mieć inne podejście.
- Vertical slice dobrze łączy się z CQRS, a wspólne reguły trzyma się w modelu domeny.
- Modularny monolit dzieli system pionowo według obszarów biznesowych, a warstwy mogą istnieć w środku modułu.
- Każdy moduł lub bounded context może mieć inną architekturę, dopasowaną do złożoności.

## Pytania sprawdzające

### 23. Czym architektura warstwowa różni się od hexagonal, onion i clean? Którą jedną zależność te architektury odwracają?

<details>
<summary>Odpowiedź</summary>

Odwracają zależność logiki od warstwy dostępu do danych. W layered logika importuje konkretne repozytoria, a w hexagonal, onion i clean logika definiuje interfejs, którego potrzebuje, a warstwa danych go implementuje (Dependency Inversion Principle zastosowana do całej aplikacji). Skutki: reguły testuje się z fake'iem w pamięci, wymiana bazy lub ORM-a to nowy adapter, a typy ORM nie trafiają do logiki. Kosztem jest więcej interfejsów, adapterów i mapowania. Różnice między tymi trzema są głównie w nazwach i szczegółowości.

Zobacz: sekcja „Odwrócenie jednej strzałki”.

</details>

### 24. Czym jest vertical slice architecture i czym różni się od podziału na warstwy techniczne?

<details>
<summary>Odpowiedź</summary>

To podejście spopularyzowane przez Jimmy'ego Bogarda, w którym kod dzieli się według funkcji biznesowych: każdy plasterek zawiera obsługę żądania, logikę i dostęp do danych jednej operacji. W porównaniu z warstwami zmiana funkcji dotyka jednego katalogu zamiast wielu, sprzężenie jest niskie między plasterkami, a każdy może użyć innego podejścia (surowy SQL, transaction script, model domeny). Ryzykiem jest duplikacja reguł, więc wspólne reguły trzyma się we współdzielonym modelu domeny. Dobrze pasuje do CQRS: plasterek to jedna komenda albo jedno zapytanie.

Zobacz: sekcja „Pionowe plasterki”.

</details>

### 25. Jak architektura warstwowa ma się do modularnego monolitu i do DDD? Czy warstwy mogą istnieć wewnątrz modułu lub bounded contextu?

<details>
<summary>Odpowiedź</summary>

To różne wymiary podziału: modularny monolit dzieli system pionowo według obszarów biznesowych, które w DDD odpowiadają bounded contextom, a warstwy dzielą kod poziomo według rodzaju. Warstwy mogą i często powinny istnieć wewnątrz modułu. Każdy moduł może mieć inną architekturę: prosty moduł dwie warstwy, typowy trzy lub cztery, a moduł z bogatą logiką (core domain) architekturę heksagonalną. Moduły komunikują się przez publiczne API i nie sięgają do cudzych tabel.

Zobacz: sekcja „Warstwy w modułach”.

</details>
