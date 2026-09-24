# Czym jest Hexagonal

<a id="term-hexagonal-architecture"></a>[Architektura heksagonalna](00%20Glossary%20Hexagonal.md#hexagonal-architecture) to sposób organizowania aplikacji, w którym logika biznesowa jest odizolowana od technologii: bazy danych, frameworka HTTP, kolejki czy zewnętrznych API. Wzorzec opisał Alistair Cockburn w 2005 roku pod nazwą Ports and Adapters. Obie nazwy oznaczają to samo.

Najprostszy model działania wygląda tak:

```text
świat zewnętrzny (HTTP, CLI, testy)
        ↓
     port wejściowy
        ↓
  rdzeń aplikacji (reguły biznesowe)
        ↓
     port wyjściowy
        ↓
świat zewnętrzny (baza, e-mail, płatności)
```

## Środek i zewnętrze

Aplikacja dzieli się na dwie strefy. W środku jest <a id="term-application-core"></a>[rdzeń aplikacji](00%20Glossary%20Hexagonal.md#application-core), czyli kod, który wie, jak złożyć zamówienie, policzyć rabat albo odrzucić płatność. Na zewnątrz jest wszystko, co da się wymienić bez zmiany reguł biznesowych: framework webowy, ORM, broker wiadomości, dostawca e-maili.

W rdzeniu żyje <a id="term-domain"></a>[domena](00%20Glossary%20Hexagonal.md#domain), czyli model pojęć biznesowych: zamówienie, pozycja zamówienia, kwota. Na zewnątrz leży <a id="term-infrastructure"></a>[infrastruktura](00%20Glossary%20Hexagonal.md#infrastructure), czyli kod techniczny, który łączy aplikację z konkretnymi narzędziami.

```text
┌───────────────────── infrastruktura ─────────────────────┐
│                                                          │
│   HTTP ──┐                                  ┌── Postgres │
│          │      ┌────── rdzeń ──────┐       │            │
│   CLI ───┼────► │ domena + use case │ ◄─────┼── SMTP     │
│          │      └───────────────────┘       │            │
│   testy ─┘                                  └── Stripe   │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

## Jak rdzeń rozmawia ze światem

Rdzeń nie rozmawia z technologią bezpośrednio. Komunikuje się przez <a id="term-port"></a>[porty](00%20Glossary%20Hexagonal.md#port), czyli interfejsy opisujące, czego rdzeń potrzebuje albo co oferuje. Konkretną technologię podłącza <a id="term-adapter"></a>[adapter](00%20Glossary%20Hexagonal.md#adapter), czyli klasa implementująca port albo wywołująca go.

Dla przykładu rdzeń mówi: „potrzebuję zapisać zamówienie”. Nie mówi: „wykonaj INSERT w Postgresie”. Port nazywa potrzebę, adapter ją realizuje.

```python
from typing import Protocol


class OrderRepository(Protocol):          # port, należy do rdzenia
    def save(self, order: "Order") -> None: ...


class PostgresOrderRepository:            # adapter, należy do infrastruktury
    def __init__(self, session):
        self._session = session

    def save(self, order: "Order") -> None:
        self._session.add(OrderRow.from_domain(order))
```

## Dlaczego heksagon

Kształt sześciokąta nie ma znaczenia technicznego. Cockburn narysował heksagon, żeby odejść od obrazka „góra–dół” znanego z warstw i pokazać, że aplikacja ma wiele równorzędnych stron. Z każdej strony może być podłączony inny aktor: użytkownik, test, baza, inny system. Liczba boków jest dowolna.

## Problem, który rozwiązuje

Klasyczna <a id="term-layered-architecture"></a>[architektura warstwowa](00%20Glossary%20Hexagonal.md#layered-architecture) układa kod w stos: na górze prezentacja, pod nią logika, na dole dostęp do danych. Zależności płyną w dół, więc logika biznesowa importuje warstwę danych.

```text
Warstwowo:                      Heksagonalnie:

controller                      controller ──► rdzeń
    ↓                                          ▲
service                         repozytorium ──┘
    ↓                           (implementuje port rdzenia)
repository (ORM)
```

Po lewej logika zależy od ORM. Zmiana bazy, test bez bazy albo przeniesienie reguł do innego procesu wymaga dotykania kodu biznesowego. Po prawej to repozytorium zależy od rdzenia. Rdzeń nie wie, czy zamówienie trafia do Postgresa, pliku czy listy w pamięci.

## Kierunek zależności

Najważniejsza zasada ma nazwę <a id="term-dependency-rule"></a>[reguła zależności](00%20Glossary%20Hexagonal.md#dependency-rule): zależności w kodzie wskazują zawsze do środka. Adapter importuje rdzeń, rdzeń nigdy nie importuje adaptera.

Łatwo to sprawdzić: w plikach domeny i scenariuszy aplikacji nie powinno być importów `sqlalchemy`, `fastapi`, `requests`, `boto3` ani modułów z katalogu `adapters`. Jeśli takie importy są, granica już przecieka.

```python
# domain/order.py: dobrze
from dataclasses import dataclass
from decimal import Decimal

# domain/order.py: źle, domena zna ORM
from sqlalchemy.orm import Mapped
```

## Korzyści i koszty

Architektura heksagonalna daje konkretne korzyści:

- reguły biznesowe da się testować w milisekundach, bez bazy i sieci,
- technologię można wymienić, wymieniając jeden adapter,
- tę samą logikę można wywołać z HTTP, CLI, kolejki i testu,
- decyzje infrastrukturalne można odłożyć, zaczynając od adapterów w pamięci.

Ma też koszty:

- więcej plików, interfejsów i mapowania między modelami,
- pośredniość utrudnia nawigację po kodzie osobom nowym w projekcie,
- łatwo zbudować „ceremonię” bez realnej logiki do ochrony.

## Kiedy nie warto

Hexagonal opłaca się, gdy jest co chronić, czyli gdy aplikacja ma nietrywialne reguły biznesowe i będzie rozwijana latami. Nie opłaca się w prostym CRUD-zie, gdzie cała logika to „zapisz formularz w tabeli”, w skrypcie jednorazowym ani w prototypie, który ma sprawdzić pomysł w tydzień.

Dobrym testem jest pytanie: co zostałoby w rdzeniu, gdyby usunąć framework i bazę? Jeśli prawie nic, dodatkowe warstwy niczego nie izolują.

## Co zapamiętać

- Hexagonal i Ports and Adapters to ta sama architektura Alistaira Cockburna.
- Rdzeń zawiera domenę i scenariusze aplikacji, infrastruktura zawiera technologię.
- Port to interfejs na granicy rdzenia, adapter to jego konkretna realizacja.
- Kształt heksagonu symbolizuje wiele równorzędnych stron, a nie sześć elementów.
- Reguła zależności: kod zależy zawsze do środka, nigdy na zewnątrz.
- Zyskujesz testowalność i wymienialność kosztem większej liczby elementów.
- Prosty CRUD i prototyp zwykle nie potrzebują hexagonal.

## Pytania sprawdzające

### 1. Czym jest architektura heksagonalna (Ports & Adapters) i kto ją zaproponował?

<details>
<summary>Odpowiedź</summary>

To sposób organizowania aplikacji, w którym logika biznesowa (rdzeń) jest odizolowana od technologii. Rdzeń komunikuje się ze światem przez porty, czyli interfejsy, a konkretne technologie podłącza się przez adaptery. Wzorzec opisał Alistair Cockburn w 2005 roku. Nazwy „hexagonal” i „Ports and Adapters” oznaczają to samo.

Zobacz: początek rozdziału i sekcja „Jak rdzeń rozmawia ze światem”.

</details>

### 2. Jaki problem rozwiązuje? Co było nie tak z klasyczną architekturą warstwową?

<details>
<summary>Odpowiedź</summary>

W architekturze warstwowej zależności płyną w dół: logika biznesowa importuje warstwę dostępu do danych, a często także ORM. Przez to zmiana bazy, test bez bazy albo wywołanie logiki z innego miejsca wymaga zmian w kodzie biznesowym. Hexagonal odwraca tę zależność: repozytorium zależy od rdzenia, a nie odwrotnie.

Zobacz: sekcja „Problem, który rozwiązuje”.

</details>

### 3. Dlaczego akurat „heksagon”? Czy liczba boków ma znaczenie?

<details>
<summary>Odpowiedź</summary>

Nie ma znaczenia. Cockburn narysował sześciokąt, żeby odejść od pionowego obrazka warstw i pokazać, że aplikacja ma wiele równorzędnych stron, do których podłącza się różnych aktorów: użytkownika, test, bazę, inny system.

Zobacz: sekcja „Dlaczego heksagon”.

</details>

### 4. Co znaczy, że aplikacja jest „w środku”, a świat zewnętrzny „na zewnątrz”?

<details>
<summary>Odpowiedź</summary>

W środku jest rdzeń: domena, czyli model pojęć biznesowych, oraz scenariusze aplikacji. Na zewnątrz jest wszystko, co da się wymienić bez zmiany reguł biznesowych: framework webowy, ORM, baza, broker, dostawca e-maili. Środek nie wie, jakie konkretne technologie są na zewnątrz.

Zobacz: sekcja „Środek i zewnętrze”.

</details>

### 5. Jaka jest zasada kierunku zależności w tej architekturze?

<details>
<summary>Odpowiedź</summary>

Reguła zależności: zależności w kodzie wskazują zawsze do środka. Adapter importuje rdzeń, rdzeń nigdy nie importuje adaptera ani biblioteki technicznej. W praktyce w plikach domeny nie powinno być importów typu `sqlalchemy`, `fastapi` czy `requests`.

Zobacz: sekcja „Kierunek zależności”.

</details>

### 6. Jakie są główne korzyści, a jakie koszty wprowadzenia hexagonal?

<details>
<summary>Odpowiedź</summary>

Korzyści: szybkie testy reguł bez infrastruktury, wymiana technologii przez wymianę adaptera, wywoływanie tej samej logiki z HTTP, CLI, kolejki i testów, odkładanie decyzji infrastrukturalnych. Koszty: więcej plików, interfejsów i mapowania, więcej pośredniości w nawigacji po kodzie i ryzyko ceremonii bez realnej logiki do ochrony.

Zobacz: sekcja „Korzyści i koszty”.

</details>

### 7. Kiedy nie warto stosować architektury heksagonalnej?

<details>
<summary>Odpowiedź</summary>

Gdy nie ma czego chronić: w prostym CRUD-zie, w skrypcie jednorazowym, w krótkim prototypie. Test praktyczny: co zostałoby w rdzeniu po usunięciu frameworka i bazy? Jeśli prawie nic, dodatkowe warstwy niczego nie izolują.

Zobacz: sekcja „Kiedy nie warto”.

</details>
