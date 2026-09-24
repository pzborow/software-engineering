# Czym jest Clean

<a id="term-clean-architecture"></a>[Clean Architecture](00%20Glossary%20Clean.md#clean-architecture) to sposób organizowania aplikacji w koncentryczne kręgi, w którym reguły biznesowe są w środku, a bazy danych, frameworki i interfejs użytkownika na zewnątrz. Robert C. Martin opisał ją w artykule na blogu w 2012 roku, a rozwinął w książce „Clean Architecture” z 2017 roku.

Najprostszy model działania wygląda tak:

```text
┌──────────────────────────────────────────────────────────┐
│  Frameworks & Drivers   (web, baza, UI, urządzenia)      │
│  ┌────────────────────────────────────────────────────┐  │
│  │  Interface Adapters  (kontrolery, presentery)      │  │
│  │  ┌──────────────────────────────────────────────┐  │  │
│  │  │  Use Cases  (reguły aplikacji)               │  │  │
│  │  │  ┌────────────────────────────────────────┐  │  │  │
│  │  │  │  Entities  (reguły przedsiębiorstwa)   │  │  │  │
│  │  │  └────────────────────────────────────────┘  │  │  │
│  │  └──────────────────────────────────────────────┘  │  │
│  └────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────┘
          zależności w kodzie wskazują do środka
```

Przykładem przewodnim tego tutorialu jest system rezerwacji sal konferencyjnych: `Room`, `Reservation`, reguła „rezerwacje tej samej sali nie mogą się nakładać”.

## Po co w ogóle architektura

Martin zaczyna od celu: architektura ma zminimalizować wysiłek potrzebny do zbudowania i utrzymania systemu. Dobra architektura sprawia, że koszt zmiany nie rośnie z każdym wydaniem.

Drugi cel to utrzymywanie otwartych opcji. Decyzje o bazie danych, frameworku webowym czy sposobie wdrożenia można odłożyć na później, bo reguły biznesowe od nich nie zależą. Im później taka decyzja, tym więcej wiadomo, kiedy się ją podejmuje. Zespół może zacząć od repozytorium w pamięci, a PostgreSQL wybrać, gdy znane są już realne wymagania.

## Co jest ważne, a co wymienne

Martin dzieli kod na dwie kategorie. <a id="term-policy"></a>[Polityka](00%20Glossary%20Clean.md#policy) (policy) to reguły i procedury biznesowe, czyli to, dla czego system w ogóle istnieje. W rezerwacji sal polityką jest zakaz nakładania się rezerwacji i zasada, że rezerwację można anulować najpóźniej 24 godziny wcześniej.

<a id="term-detail"></a>[Szczegół](00%20Glossary%20Clean.md#detail) (detail) to wszystko, co jest potrzebne, żeby ludzie, programy i dane mogły komunikować się z polityką: baza danych, serwer WWW, framework, protokół, format JSON. Szczegóły są ważne, ale polityka nie powinna o nich wiedzieć.

```python
# polityka: czysty Python, zero importów technicznych
from dataclasses import dataclass
from datetime import datetime


@dataclass(frozen=True)
class TimeSlot:
    start: datetime
    end: datetime

    def overlaps(self, other: "TimeSlot") -> bool:
        return self.start < other.end and other.start < self.end
```

Książka ma osobne rozdziały „The Database Is a Detail”, „The Web Is a Detail” i „Frameworks Are Details”. Nie chodzi w nich o to, że baza jest nieważna. Chodzi o to, że struktura danych biznesowych i reguły ich przetwarzania nie powinny zależeć od tego, jak dane są przechowywane ani skąd przychodzi żądanie.

Z tym podziałem wiąże się pojęcie poziomu. Im dalej kod jest od wejścia i wyjścia systemu, tym wyższy jest jego poziom. Reguła nakładania się rezerwacji jest wysokopoziomowa. Parsowanie JSON-a z żądania HTTP jest niskopoziomowe. Kod wysokiego poziomu nie powinien zależeć od kodu niskiego poziomu.

## Jedna reguła ponad wszystkie

Najważniejsza zasada ma nazwę <a id="term-dependency-rule"></a>[Dependency Rule](00%20Glossary%20Clean.md#dependency-rule): zależności w kodzie źródłowym mogą wskazywać wyłącznie do środka. Nic w kręgu wewnętrznym nie może znać nazwy niczego z kręgu zewnętrznego: klasy, funkcji, zmiennej ani formatu danych.

```python
# entities/reservation.py: dobrze
from dataclasses import dataclass
from datetime import datetime

# entities/reservation.py: źle, reguły znają framework i ORM
from django.db import models
from sqlalchemy.orm import Mapped
```

Reguła dotyczy także formatów danych. Jeśli zewnętrzny krąg używa wiersza z bazy albo słownika z JSON-a, ta struktura nie może wejść do środka. Do środka trafiają tylko proste struktury zdefiniowane przez krąg wewnętrzny.

Martin pokazuje, że wszystkie podobne architektury (Hexagonal, Onion, DCI, BCE) mają wspólne cechy wynikające z tej reguły:

- niezależność od frameworków, które są narzędziami, a nie klatką,
- testowalność reguł biznesowych bez UI, bazy i serwera,
- niezależność od UI, który można wymienić bez zmiany reguł,
- niezależność od bazy danych,
- niezależność od jakichkolwiek zewnętrznych systemów.

## Korzyści i koszty

Clean Architecture daje:

- reguły biznesowe testowane w milisekundach,
- możliwość odłożenia decyzji technicznych,
- wymianę bazy, frameworka albo UI bez dotykania polityki,
- jasne miejsce dla każdego rodzaju kodu.

Kosztuje:

- więcej interfejsów i struktur danych, bo każda granica wymaga własnych typów,
- mapowanie danych przy każdym przekroczeniu granicy,
- więcej pośredniości, przez co nowym osobom trudniej śledzić przepływ,
- ryzyko przesady, gdy każdy use case dostaje pełen zestaw interfejsów i modeli.

## Kiedy nie warto

Martin sam pisze, że pełne granice są drogie i że architekt musi zdecydować, gdzie ich potrzeba. Prosty CRUD, panel administracyjny nad tabelą, prototyp albo skrypt nie mają polityki, którą trzeba chronić. W takich przypadkach cztery kręgi to ceremonia.

Pytanie kontrolne jest takie samo jak przy innych architekturach: co zostanie w Entities i Use Cases po usunięciu bazy i frameworka? Jeśli prawie nic, lepiej wybrać prostszy układ albo wprowadzić tylko częściowe granice, opisane w rozdziale 05.

## Co zapamiętać

- Clean Architecture opisał Robert C. Martin w 2012 roku i rozwinął w książce z 2017 roku.
- Cel architektury: niski koszt zmian i otwarte opcje co do szczegółów technicznych.
- Polityka to reguły biznesowe, szczegóły to baza, web, framework i formaty.
- Dependency Rule: zależności w kodzie wskazują wyłącznie do środka, także w przypadku formatów danych.
- Kod wysokiego poziomu (daleko od wejścia i wyjścia) nie zależy od kodu niskiego poziomu.
- Pełne granice są drogie i nie każdy system ich potrzebuje.

## Pytania sprawdzające

### 1. Czym jest Clean Architecture i kto ją zaproponował?

<details>
<summary>Odpowiedź</summary>

To architektura złożona z koncentrycznych kręgów: Entities, Use Cases, Interface Adapters oraz Frameworks & Drivers. Reguły biznesowe są w środku, a technologia na zewnątrz, i obowiązuje zasada, że zależności w kodzie wskazują do środka. Zaproponował ją Robert C. Martin (Uncle Bob) w artykule z 2012 roku i rozwinął w książce z 2017 roku.

Zobacz: początek rozdziału.

</details>

### 2. Jakie cele architektury stawia Robert C. Martin? Co znaczy, że architektura ma „utrzymywać otwarte opcje”?

<details>
<summary>Odpowiedź</summary>

Celem jest zminimalizowanie wysiłku potrzebnego do zbudowania i utrzymania systemu, tak żeby koszt zmian nie rósł z czasem. Utrzymywanie otwartych opcji oznacza, że decyzje o szczegółach (baza, framework, sposób wdrożenia) można odłożyć, bo reguły biznesowe od nich nie zależą. Im później taka decyzja, tym więcej wiadomo o realnych wymaganiach.

Zobacz: sekcja „Po co w ogóle architektura”.

</details>

### 3. Co oznacza stwierdzenie, że baza danych, UI i framework to „szczegóły”?

<details>
<summary>Odpowiedź</summary>

Że są mechanizmami komunikacji z polityką, a nie jej częścią. Są ważne technicznie, ale reguły biznesowe nie mogą od nich zależeć. Struktura danych biznesowych i reguły ich przetwarzania są niezależne od sposobu przechowywania i dostarczania danych. Dlatego bazę, framework czy UI można wymienić bez zmiany polityki.

Zobacz: sekcja „Co jest ważne, a co wymienne”.

</details>

### 4. Na czym polega The Dependency Rule i dlaczego jest najważniejszą zasadą tej architektury?

<details>
<summary>Odpowiedź</summary>

Zależności w kodzie źródłowym mogą wskazywać tylko do środka. Nic w kręgu wewnętrznym nie może znać nazwy niczego z kręgu zewnętrznego: klasy, funkcji, zmiennej ani formatu danych. Jest najważniejsza, bo wynikają z niej wszystkie korzyści: niezależność od frameworków, UI, bazy i usług zewnętrznych oraz testowalność reguł.

Zobacz: sekcja „Jedna reguła ponad wszystkie”.

</details>

### 5. Czym różni się polityka (policy) od szczegółu (detail) i jak to się ma do „poziomu” kodu?

<details>
<summary>Odpowiedź</summary>

Polityka to reguły biznesowe, np. zakaz nakładania się rezerwacji. Szczegół to mechanizm, np. baza, HTTP czy JSON. Poziom kodu to jego odległość od wejścia i wyjścia systemu: im dalej, tym wyższy poziom. Polityka jest wysokopoziomowa, parsowanie żądania niskopoziomowe, a kod wysokiego poziomu nie może zależeć od kodu niskiego poziomu.

Zobacz: sekcja „Co jest ważne, a co wymienne”.

</details>

### 6. Kiedy Clean Architecture jest przesadą i jakie są jej koszty?

<details>
<summary>Odpowiedź</summary>

Jest przesadą w prostym CRUD-zie, panelu administracyjnym nad tabelą, prototypie czy skrypcie, czyli tam, gdzie nie ma polityki do ochrony. Koszty to więcej interfejsów i struktur danych, mapowanie przy każdej granicy, więcej pośredniości i ryzyko przesady. Martin zaleca świadomie wybierać, gdzie potrzebne są pełne granice, a gdzie wystarczą częściowe.

Zobacz: sekcje „Korzyści i koszty” i „Kiedy nie warto”.

</details>
