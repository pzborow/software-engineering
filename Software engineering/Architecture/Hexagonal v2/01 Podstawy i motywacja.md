# Podstawy i motywacja

Architektura heksagonalna (Ports & Adapters) to sposób organizacji kodu, w którym część z logiką biznesową, czyli regułami działania aplikacji, nie zależy od frameworka, bazy danych ani protokołu komunikacji. Rozwiązuje problem kodu, w którym te reguły splatają się ze szczegółami technicznymi, przez co trudno je testować bez uruchamiania całej infrastruktury i trudno wymienić jej dowolny element. Logika biznesowa sama określa, jakich interfejsów (abstrakcyjnych punktów styku) potrzebuje do komunikacji z otoczeniem, a bazy danych, frameworki i protokoły są do nich dopasowywane.

## Problem: logika uwięziona w infrastrukturze

Architektura heksagonalna rozwiązuje problem sprzężenia [logiki domenowej](00%20Glosariusz.md#logika-domenowa) (reguł biznesowych, które czynią system wartym budowy) z technologią, przez którą system się z otoczeniem komunikuje. Gdy reguły żyją w widoku HTTP, modelu ORM i wywołaniu SDK bramki płatności, nie da się ich zmienić, przetestować ani użyć ponownie bez ciągnięcia całej reszty.

W „Rowerku” tak wygląda pierwsza, naturalna wersja wypożyczania:

```python
# poza kanonem
@router.post("/rentals")
def start_rental(bike_id: int, user_id: int, db: Session = Depends(get_db)):
    user = db.query(UserModel).get(user_id)
    if db.query(RentalModel).filter_by(user_id=user_id, finished=False).count():
        raise HTTPException(409, "Limit jednego wypożyczenia")
    if user.overdue_payment:
        raise HTTPException(402, "Zaległa płatność")
    ...
    stripe.PaymentIntent.create(customer=user.stripe_id, amount=...)
    db.add(RentalModel(bike_id=bike_id, user_id=user_id)); db.commit()
```

Limit wypożyczeń, blokada za zaległość i cennik są tu wymieszane z `HTTPException`, zapytaniami SQLAlchemy i Stripe. Test reguły wymaga bazy i mocka `stripe`, a zmiana bramki lub dodanie konsumenta zdarzeń z zamków oznacza kopiowanie reguł. Zmiana technologii przestaje być lokalna.

Rozwiązanie: reguły trafiają do środka, a wszystko, co zewnętrzne, łączy się z nimi przez wąskie [porty](00%20Glosariusz.md#port) (interfejsy zdefiniowane przez rdzeń), implementowane przez [adaptery](00%20Glosariusz.md#adapter) (kod tłumaczący konkretną technologię na te interfejsy).

```text
FastAPI ──► [ Rental, Bike, User, PricingPolicy ] ◄── SQLAlchemy
Stripe  ──►        (rdzeń, bez importów        ◄── kolejka IoT
                    frameworków)
```

Konsekwencja: rdzeń da się testować bez infrastruktury, a technologie wymieniać bez zmiany reguł.

## Wnętrze i zewnętrze heksagonu

Wewnątrz heksagonu leży wszystko, co wyraża reguły biznesowe i nie wie, jak system komunikuje się ze światem: [encje](00%20Glosariusz.md#encja), [obiekty wartości](00%20Glosariusz.md#obiekt-wartości) i [przypadki użycia](00%20Glosariusz.md#przypadek-użycia). Na zewnątrz jest cała technologia: HTTP, baza SQL, bramka płatności, SMS, kolejka z zamków IoT.

Encja to obiekt z tożsamością, którego stan zmienia się w czasie (`Rental`, `Bike`, `User`). Obiekt wartości nie ma tożsamości i jest niezmienny, jak `PricingPolicy` z darmowymi 20 minutami. Przypadek użycia to jeden scenariusz aplikacji, np. `StartRental`, który składa te elementy w całość: sprawdza limit wypożyczeń, blokadę za zaległość i zapisuje wynik.

Rdzeń nie importuje FastAPI, SQLAlchemy ani Stripe. Gdy potrzebuje bazy lub płatności, deklaruje port, np. `RentalRepository`, czyli interfejs w swoim własnym języku. Implementuje go adapter leżący na zewnątrz.

```text
core/                      # wewnątrz: zero importów infrastruktury
  entities.py              # Rental, Bike, User
  pricing.py               # PricingPolicy
  ports.py                 # RentalRepository
  use_cases.py             # StartRental
adapters/                  # na zewnątrz: FastAPI, SQLAlchemy, Stripe...
```

Granicę wyznacza więc pytanie: czy ten kod zmieni się, gdy zmienią się reguły „Rowerka”, czy gdy zmieni się technologia? Reguły trafiają do rdzenia, technologia do adapterów. Konsekwencja: `StartRental` da się uruchomić w teście bez bazy, serwera i Stripe.

## Sześciokąt to tylko metafora

Sześć boków sześciokąta nic nie liczy. Autor wzorca potrzebował kształtu z wieloma bokami, by pokazać, że rdzeń ma wiele równorzędnych punktów styku ze światem, a nie jedno „wejście” u góry i jedno „wyjście” na dole, jak w rysunku warstw.

Rdzeń to logika domenowa i przypadki użycia, czyli kod niezależny od technologii, który komunikuje się ze światem wyłącznie przez porty. Liczba portów wynika z rozmów, które rdzeń prowadzi ze światem, a nie z geometrii. Port to granica ze względu na **cel rozmowy** (zapis wypożyczeń, pobranie opłaty, powiadomienie), a nie ze względu na technologię.

Ta sama zasada działa po stronie adapterów: jeden port może mieć wiele adapterów (`RentalRepository` z SQL-em i z pamięcią w testach), a jeden adapter może obsługiwać kilka portów.

### Ile portów w „Rowerku”

| Rozmowa | Kierunek | Przykład |
|---|---|---|
| Uruchomienie scenariusza | wchodzi do rdzenia | `StartRental` wywołany z HTTP |
| Zapis i odczyt wypożyczeń | rdzeń wywołuje świat | `RentalRepository` |
| Pobranie opłaty | rdzeń wywołuje świat | bramka płatności |
| Powiadomienie użytkownika | rdzeń wywołuje świat | SMS lub e-mail |
| Zdarzenia z zamków | wchodzi do rdzenia | konsument kolejki |

Pięć, dwanaście, cztery: liczba jest wtórna. Nowa integracja dokłada port, a nie „siódmy bok”.

Konsekwencja: nie projektuj pod liczbę. Zapytaj „o czym rdzeń rozmawia ze światem i po co?”, a granice portów wyznaczą się same.

## Kierunek zależności: do rdzenia

Zależności biegną od infrastruktury do rdzenia, nigdy odwrotnie. Rdzeń nie importuje SQLAlchemy, FastAPI ani klienta Stripe, natomiast adaptery importują encje i porty rdzenia.

To zastosowanie [zasady odwrócenia zależności](00%20Glosariusz.md#zasada-odwrócenia-zależności): moduły wysokiego poziomu (reguły biznesowe) nie zależą od modułów niskiego poziomu (technologia), oba zależą od abstrakcji, a tę abstrakcję, czyli port, posiada rdzeń. W sprzężonym kodzie „Rowerka” widok importował model ORM, a ten klienta Stripe. Teraz `StartRental` zna tylko `RentalRepository`, a implementacja podpina się od zewnątrz.

```text
przepływ wywołania:   router → StartRental → RentalRepository ⇢ SQL
zależności w kodzie:  router → core ← SqlAlchemyRentalRepository
```

Wywołania nadal idą „w głąb”, do bazy, ale importy wskazują w stronę rdzenia. Adapter wygląda tak:

```python
# infra/sqlalchemy_rentals.py · adapter
from core.entities import Rental  # import wskazuje do rdzenia

class SqlAlchemyRentalRepository:
    def __init__(self, session: Session) -> None: ...
    def add(self, rental: Rental) -> None: ...
    def active_for_user(self, user_id: str) -> Rental | None: ...
```

Dzięki `Protocol` adapter nie musi nawet dziedziczyć po porcie: wystarczy zgodna sygnatura.

Konsekwencja: w pakiecie `core` żaden import nie prowadzi do `infra`. Da się to sprawdzić automatycznie, a rdzeń uruchomić w teście bez bazy i sieci.

## Heksagon a architektura warstwowa

Architektura warstwowa układa kod w stos (prezentacja → logika → dane), w którym każda warstwa zależy od tej pod nią. Heksagonalna zamiast stosu daje [rdzeń](00%20Glosariusz.md#rdzeń) otoczony adapterami, a zależności kieruje do środka. Różnica leży w kierunku zależności i w tym, kto posiada abstrakcję.

Rdzeń (zwany też heksagonem, czyli wnętrzem sześciokąta) to wszystko, co zmienia się wraz z regułami biznesowymi: logika domenowa, encje, przypadki użycia i porty. Adaptery leżą na zewnątrz.

W klasycznym stosie warstwa logiki importuje warstwę danych, czyli w praktyce model ORM i jego sesję. Logika „Rowerka” (limit jednego wypożyczenia, blokada przy zaległej płatności) zna wtedy SQLAlchemy, więc zależy od szczegółu technicznego. Warstwy bywają też „przeciekowe”: widok sięga prosto do bazy, bo nic tego nie zabrania.

W heksagonie logika nie leży nad bazą, tylko obok niej, jako jeden z końców portu. `RentalRepository` należy do rdzenia, a `SqlAlchemyRentalRepository` go implementuje.

| Cecha | Warstwowa | Heksagonalna |
|---|---|---|
| Zależności | z góry na dół | do rdzenia |
| Logika zna | warstwę danych (ORM) | tylko własne porty |
| Baza i UI | „dół” i „góra” stosu | równorzędne adaptery |
| Test logiki | zwykle z bazą | na fake'ach, bez infrastruktury |

```text
warstwowa:        widok → logika → dane (ORM) → SQL
heksagonalna:     router → core ← SqlAlchemyRentalRepository
```

Konsekwencja: warstw można nadal używać wewnątrz rdzenia czy adaptera. Zmienia się to, że baza przestaje być fundamentem, a staje się wymienną implementacją.

## Co zapamiętać

- Architektura heksagonalna oddziela reguły biznesowe od technologii, by można je było testować i zmieniać niezależnie od infrastruktury.
- Do rdzenia należy to, co zmienia się wraz z regułami biznesowymi (encje, obiekty wartości, przypadki użycia, porty), a do adapterów to, co zmienia się wraz z technologią.
- Liczbę portów wyznaczają rozmowy rdzenia ze światem, a nie sześć boków rysunku.
- Importy zawsze wskazują do rdzenia: to rdzeń definiuje porty, a adaptery je implementują, nigdy odwrotnie.
- Warstwowa stawia bazę u podstawy stosu, od której zależy logika; heksagonalna stawia rdzeń w środku, a wszystko inne jest wymiennym adapterem.

## Pytania sprawdzające

### 1. Jaki główny problem projektowy rozwiązuje architektura heksagonalna?

<details>
<summary>Odpowiedź</summary>

Architektura heksagonalna rozwiązuje problem sprzężenia reguł biznesowych z technologią: widokami HTTP, ORM-em, bramkami płatności czy kolejkami. Gdy reguły są z nimi splecione, nie da się ich testować ani zmieniać bez całej infrastruktury. Wyodrębnia więc rdzeń domenowy, który komunikuje się ze światem przez porty implementowane przez adaptery. Dzięki temu technologie stają się wymienne, a reguły zostają stabilne.

Zobacz: [sekcja „Problem: logika uwięziona w infrastrukturze”](#problem-logika-uwięziona-w-infrastrukturze).

</details>

### 2. Co znajduje się wewnątrz „heksagonu”, a co na zewnątrz?

<details>
<summary>Odpowiedź</summary>

Wewnątrz heksagonu są encje, obiekty wartości i przypadki użycia, czyli reguły biznesowe wraz z portami, które rdzeń sam definiuje. Na zewnątrz leży cała technologia: framework webowy, baza danych, bramka płatności, powiadomienia i kolejki, obsługiwane przez adaptery. Rdzeń nie importuje niczego z infrastruktury, więc granicę wyznacza pytanie, czy kod zmienia się wraz z regułami biznesowymi, czy z technologią.

Zobacz: [sekcja „Wnętrze i zewnętrze heksagonu”](#wnętrze-i-zewnętrze-heksagonu).

</details>

### 3. Dlaczego sześciokąt jest tylko metaforą i nie oznacza sześciu portów?

<details>
<summary>Odpowiedź</summary>

Sześciokąt to tylko rysunek: wybrano kształt z wieloma bokami, by pokazać, że rdzeń ma wiele równorzędnych punktów styku ze światem, a nie jedno wejście i jedno wyjście. Liczba portów wynika z rozmów, jakie rdzeń, czyli logika domenowa i przypadki użycia, prowadzi ze światem (zapis danych, płatności, powiadomienia), a nie z liczby boków. Port wyznacza cel rozmowy, nie technologia, więc może ich być cztery albo dwanaście.

Zobacz: [sekcja „Sześciokąt to tylko metafora”](#sześciokąt-to-tylko-metafora).

</details>

### 4. Jaki kierunek powinny mieć zależności między rdzeniem a infrastrukturą?

<details>
<summary>Odpowiedź</summary>

Zależności źródłowe powinny wskazywać do wnętrza: infrastruktura importuje rdzeń, a rdzeń nie importuje infrastruktury. Rdzeń definiuje porty w swoim własnym języku, a adaptery je implementują, więc to technologia dostosowuje się do reguł biznesowych. Dzięki temu wymiana bazy, bramki płatności czy frameworka nie wymaga zmian w logice domenowej.

Zobacz: [sekcja „Kierunek zależności: do rdzenia”](#kierunek-zależności-do-rdzenia).

</details>

### 5. Czym architektura heksagonalna różni się od klasycznej architektury warstwowej?

<details>
<summary>Odpowiedź</summary>

W architekturze warstwowej zależności biegną z góry na dół, więc logika zależy od warstwy danych, zwykle od ORM. W heksagonalnej zależności kierowane są do rdzenia, który zawiera logikę domenową, przypadki użycia i porty. To rdzeń posiada abstrakcje (porty), a baza i UI są równorzędnymi adapterami. Dzięki temu logikę można testować i zmieniać bez infrastruktury.

Zobacz: [sekcja „Heksagon a architektura warstwowa”](#heksagon-a-architektura-warstwowa).

</details>
