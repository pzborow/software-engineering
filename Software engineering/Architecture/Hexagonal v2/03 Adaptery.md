# Adaptery

Porty opisują rozmowy rdzenia ze światem, ale same nic nie robią – ruch zaczyna się dopiero w adapterach. W tym dziale dodajemy do „Rowerka" rentals_router, SqlAlchemyRentalRepository (z mapowaniem RentalRow na Rental) i StripePaymentGateway, tłumaczący wyjątki na błędy rdzenia.

```text
rentals_router --> [port wejściowy] RDZEŃ [port wyjściowy] <-- SqlAlchemyRentalRepository
                                                     <-- StripePaymentGateway
```

## Czym jest adapter

[Adapter](00%20Glosariusz.md#adapter) to kod poza rdzeniem, który spełnia [port](00%20Glosariusz.md#port) i tłumaczy jego język domeny na konkretną technologię (albo odwrotnie). Port mówi, czego potrzebuje rdzeń, a adapter wie, jak to zrobić przy pomocy SQLAlchemy, Stripe czy FastAPI.

Rola względem portu jest zawsze ta sama: adapter go **implementuje** albo **wywołuje**. Adapter wyjściowy (`SqlAlchemyRentalRepository`, `StripePaymentGateway`) implementuje [port wyjściowy](00%20Glosariusz.md#port-wyjściowy-driven), więc rdzeń woła go przez interfejs. Adapter wejściowy (`rentals_router`) wywołuje [port wejściowy](00%20Glosariusz.md#port-wejściowy-driving), czyli przypadek użycia, na żądanie ze świata zewnętrznego.

```python
class StripePaymentGateway:
    def charge(self, user_id: str, amount: Money) -> None:
        try:
            stripe.PaymentIntent.create(...)  # język dostawcy
        except stripe.CardError as e:
            raise ...  # błąd rdzenia
```

Adapter wykonuje trzy czynności: przyjmuje typy domeny, tłumaczy je na typy technologii i przekłada wynik oraz wyjątki z powrotem na język rdzenia. Nie podejmuje decyzji biznesowych, bo te należą do rdzenia.

```text
HTTP --> rentals_router --> StartRental --> RentalRepository <-- SqlAlchemyRentalRepository --> SQL
        (adapter wejściowy)   (rdzeń)          (port)             (adapter wyjściowy)
```

Konsekwencja: technologię wymieniasz, pisząc nowy adapter tego samego portu, a rdzeń pozostaje bez zmian. Wszystko, co zna ORM, SDK lub framework, mieszka w adapterach.

## Adaptery wejściowe w Pythonie

Adapterem wejściowym jest każdy kod, który odbiera zdarzenie ze świata i zamienia je na wywołanie portu wejściowego, czyli [przypadku użycia](00%20Glosariusz.md#przypadek-użycia). W backendzie Pythona najczęściej jest to endpoint HTTP, ale równie dobrze komenda CLI, konsument kolejki albo zadanie cykliczne.

| Adapter wejściowy | Wyzwalacz | Przykład w „Rowerku" |
|---|---|---|
| Router HTTP (FastAPI, Flask, Django view) | żądanie HTTP | `rentals_router` wywołuje `StartRental` |
| Komenda CLI (Click, Typer, `manage.py`) | polecenie w terminalu | ręczne naliczenie zaległych opłat |
| Konsument kolejki (Celery, Kafka, RabbitMQ) | wiadomość | `LockEventConsumer` z zamków IoT |
| Zadanie cykliczne (cron, APScheduler) | zegar | codzienne sprawdzanie zaległych płatności |
| Handler webhooka | wywołanie zwrotne dostawcy | potwierdzenie płatności od bramki |

Wszystkie robią to samo: parsują dane wejściowe (JSON, argumenty, bajty wiadomości), budują argumenty przypadku użycia, wywołują go i przekładają wynik lub błąd rdzenia na język protokołu, np. na kod HTTP albo kod wyjścia procesu.

```python
@router.post("/rentals")
def start_rental(body: StartRentalRequest,
                 use_case: StartRental = Depends(...)) -> RentalResponse:
    rental = use_case(body.user_id, body.bike_id)
    return RentalResponse(id=rental.id, bike_id=rental.bike_id)
```

Konsekwencja: ten sam `StartRental` obsłuży żądanie HTTP, polecenie CLI i wiadomość z kolejki bez zmiany ani jednej linii rdzenia. Dodanie nowego kanału wejścia to dopisanie nowego adaptera.

## Adaptery wyjściowe w Pythonie

Adapterem wyjściowym jest każdy kod, który implementuje port wyjściowy i przekłada wywołanie rdzenia na rozmowę z konkretną technologią. W backendzie Pythona to najczęściej repozytorium na bazie SQL, klient bramki płatności, nadawca powiadomień, klient HTTP cudzego API, zegar lub publikator wiadomości.

| Adapter wyjściowy | Technologia | Przykład w „Rowerku" |
|---|---|---|
| Repozytorium | SQLAlchemy, Django ORM, surowy SQL | `SqlAlchemyRentalRepository` |
| Bramka płatności | Stripe SDK, klient HTTP | `StripePaymentGateway` |
| Powiadomienia | SMTP, dostawca SMS | wysyłka potwierdzenia wypożyczenia |
| Publikator wiadomości | Kafka, RabbitMQ, SQS | komenda do zamka IoT |
| Cache i magazyn plików | Redis, S3 | zapis raportów |
| Zegar, generator identyfikatorów | `datetime`, `uuid` | czas rozpoczęcia jazdy |

Mechanizm jest zawsze ten sam: adapter przyjmuje typy domeny, wywołuje bibliotekę i zwraca typy domeny. Szczegóły, takie jak sesja, klucz API czy adres serwera, dostaje w konstruktorze i nie wyciekają one do rdzenia.

```python
class StripePaymentGateway:
    def __init__(self, client: stripe.StripeClient) -> None: ...

    def charge(self, user_id: str, amount: Money) -> None:
        self._client.payment_intents.create(
            params={"amount": int(amount.amount * 100),
                    "currency": amount.currency, ...})
```

Adapter zna centy i obiekty Stripe, a rdzeń zna tylko `Money`. Dlatego `StripePaymentGateway` spełnia `PaymentGateway` bez dziedziczenia, a wymiana dostawcy sprowadza się do napisania kolejnej klasy.

Konsekwencja: każdy adapter wyjściowy da się zastąpić fake'iem, czyli uproszczoną, ale działającą implementacją portu (np. przechowującą dane w pamięci), a nie mockiem sprawdzającym wywołania. Dzięki temu przypadki użycia testujesz bez bazy i sieci.

## Zakres adaptera wejściowego

Adapter wejściowy tłumaczy świat zewnętrzny na wywołanie portu wejściowego i z powrotem. Jego praca kończy się na granicy protokołu: to, co ma sens tylko w HTTP, zostaje w routerze, a to, co ma sens w domenie, trafia do rdzenia.

| Adapter wejściowy robi | Adapter wejściowy nie robi |
|---|---|
| parsuje i waliduje kształt danych (JSON, nagłówki, bajty) | sprawdza reguł, np. limitu jednego aktywnego wypożyczenia |
| uwierzytelnia wywołującego i przekazuje jego tożsamość | liczy cen ani kar |
| wywołuje jeden przypadek użycia | woła repozytorium czy bramkę płatności bezpośrednio |
| mapuje wynik na odpowiedź (kod HTTP, DTO, kod wyjścia) | zwraca encji z rdzenia jako gotowego JSON-a |
| zamienia błędy rdzenia na błędy protokołu | składa kilku przypadków użycia w proces biznesowy |

Dobry handler jest cienki: kilka linii, bez gałęzi o znaczeniu domenowym. Tożsamość pochodzi z uwierzytelnienia, nie z ciała żądania, bo klient mógłby podać cudzy identyfikator.

```python
@router.post("/rentals")
def start_rental(body: StartRentalRequest,
                 user: AuthUser = Depends(current_user),
                 use_case: StartRental = Depends(...)) -> RentalResponse:
    rental = use_case(user.id, body.bike_id)
    return RentalResponse(id=rental.id, bike_id=rental.bike_id)
```

Router nie wie, jak sprawdzić blokadę przy zaległej płatności. Zna tylko `StartRentalRequest`, `AuthUser`, `RentalResponse` i kody HTTP.

Test cienkości: jeśli ta sama reguła musiałaby się pojawić drugi raz w `LockEventConsumer` albo w CLI, to należy do przypadku użycia. Konsekwencja: każdy nowy kanał wejścia dopisuje tylko tłumaczenie, a reguły zostają w jednym miejscu, gdzie testujesz je bez serwera HTTP.

## Mapowanie modeli zewnętrznych

Adapter mapuje modele zewnętrzne na obiekty domenowe, bo tylko wtedy [rdzeń](00%20Glosariusz.md#rdzeń) nie dowiaduje się, że istnieje ORM, JSON czy SDK dostawcy. Model zewnętrzny jest kształtowany przez technologię, więc jego zmiana (nowa kolumna, zmiana wersji API) nie może przenosić się na reguły biznesowe.

### Co się dzieje bez mapowania

Gdyby `active_for_user` zwracało `RentalRow`, rdzeń dostałby obiekt ORM. Jest to [model trwałości](00%20Glosariusz.md#model-trwałości), czyli klasa opisująca, jak dane leżą w bazie, a nie czym jest wypożyczenie w domenie. Taki obiekt niesie sesję, leniwe ładowanie i zmiany śledzone przez ORM. Przypadek użycia zaczyna działać na cudzym stanie, a test bez bazy przestaje być możliwy.

Drugi problem to kierunek zmian. Kolumna `user_fk` zmienia nazwę i psuje logikę, która nie miała z nią nic wspólnego.

### Mapowanie na granicy

Adapter zna oba kształty i tłumaczy między nimi w obu kierunkach. Reszta systemu widzi tylko `Rental`.

```python
class SqlAlchemyRentalRepository(RentalRepository):
    def active_for_user(self, user_id: str) -> Rental | None:
        row = self._session.scalars(...).first()
        return None if row is None else self._to_domain(row)

    @staticmethod
    def _to_domain(row: RentalRow) -> Rental:
        return Rental(id=str(row.id), bike_id=row.bike_ref, user_id=row.user_fk)
```

Ta sama zasada dotyczy DTO: `StripePaymentGateway` przyjmuje `Money` i sam składa żądanie w formacie Stripe, np. kwotę w groszach.

### Konsekwencja

Koszt to dodatkowy kod i kopiowanie pól. W zamian schemat bazy, wersję API dostawcy i kształt JSON-a zmieniasz wyłącznie w adapterze, a `Rental` pozostaje zwykłą dataclass, którą testujesz bez infrastruktury.

## Tłumaczenie wyjątków w adapterze

Adapter łapie wyjątki biblioteki i rzuca w ich miejsce [błędy rdzenia](00%20Glosariusz.md#błąd-rdzenia), czyli wyjątki zdefiniowane w rdzeniu obok portu i nazwane według znaczenia dla domeny. Rdzeń nie może łapać `stripe.CardError`, bo musiałby zaimportować SDK, a to odwróciłoby kierunek zależności.

### Błędy należą do portu

Błędy są częścią kontraktu portu, tak jak sygnatury metod. Dlatego leżą w `core/ports.py`, a nazywają to, co rdzeń może z nimi zrobić: uznać płatność za odrzuconą albo spróbować później. Płatność przy zakończeniu wypożyczenia wywołuje `FinishRental`, któremu wstrzykujemy `PaymentGateway`.

```python
# core/ports.py
class PaymentDeclined(Exception): ...
class PaymentUnavailable(Exception): ...

# infra/stripe_gateway.py
def charge(self, user_id: str, amount: Money) -> None:
    try:
        stripe.PaymentIntent.create(...)
    except stripe.CardError as exc:
        raise PaymentDeclined(user_id) from exc
    except (stripe.APIConnectionError, stripe.RateLimitError) as exc:
        raise PaymentUnavailable() from exc
```

### Zasady tłumaczenia

- Grupuj według reakcji rdzenia, nie według klas biblioteki: odmowa (nie ponawiaj) i awaria przejściowa (można ponowić) to dwa różne błędy.
- Zawsze `from exc`: ślad stosu dostawcy zostaje w logach, choć rdzeń go nie widzi.
- Nie łap `Exception`. Nierozpoznany wyjątek to zwykle bug i ma się głośno wydostać.
- Nie kopiuj komunikatów dostawcy do błędu rdzenia; zostają w przyczynie.

### Konsekwencja

`FinishRental` i testy na fake'ach operują na `PaymentDeclined`, więc fake bramki po prostu go rzuca. Zamiana Stripe na innego dostawcę wymaga nowej tabeli tłumaczeń w adapterze, nie zmian w rdzeniu. Adapter wejściowy mapuje potem błędy rdzenia na kody odpowiedzi, np. 402 albo 503.

## Co zapamiętać

- Adapter implementuje port wyjściowy albo wywołuje port wejściowy i tłumaczy między językiem domeny a językiem technologii, nie zawierając reguł biznesowych.
- Router HTTP, CLI, konsument kolejki, zadanie cykliczne i webhook to adaptery wejściowe wywołujące te same przypadki użycia, a nowy kanał wejścia nie zmienia rdzenia.
- Adapter wyjściowy to klasa, która przyjmuje i zwraca typy domeny, chowa bibliotekę za portem i dzięki temu daje się zastąpić fake'iem lub innym dostawcą.
- Adapter wejściowy tłumaczy protokół na wywołanie jednego przypadku użycia i z powrotem, z tożsamością z uwierzytelnienia, a reguły biznesowe zostawia rdzeniowi.
- Adapter jest jedynym miejscem, które zna model zewnętrzny i tłumaczy go na obiekty domenowe, więc zmiany technologii nie przenikają do rdzenia.
- Adapter tłumaczy wyjątki technologii na błędy należące do portu w rdzeniu, pogrupowane według reakcji rdzenia, z zachowaniem przyczyny przez `from exc`.

## Pytania sprawdzające

### 11. Czym jest adapter i jaką pełni rolę względem portu?

<details>
<summary>Odpowiedź</summary>

Adapter to kod poza rdzeniem, który łączy port z konkretną technologią. Adapter wyjściowy implementuje port wyjściowy i tłumaczy wywołania rdzenia na język bazy, bramki czy kolejki. Adapter wejściowy przyjmuje żądanie ze świata (np. HTTP) i wywołuje port wejściowy, czyli przypadek użycia. Dzięki temu technologię wymienia się przez nowy adapter, bez zmian w rdzeniu.

Zobacz: [sekcja „Czym jest adapter”](#czym-jest-adapter).

</details>

### 12. Podaj przykłady adapterów wejściowych w backendzie Pythona.

<details>
<summary>Odpowiedź</summary>

Adaptery wejściowe to kod, który odbiera bodziec ze świata i wywołuje przypadek użycia rdzenia. Typowe przykłady w Pythonie to routery HTTP (FastAPI, Flask, Django), komendy CLI, konsumenci kolejek (Celery, Kafka, RabbitMQ), zadania cykliczne oraz handlery webhooków. Każdy parsuje dane wejściowe, wywołuje ten sam przypadek użycia i tłumaczy wynik na język swojego protokołu.

Zobacz: [sekcja „Adaptery wejściowe w Pythonie”](#adaptery-wejściowe-w-pythonie).

</details>

### 13. Podaj przykłady adapterów wyjściowych w backendzie Pythona.

<details>
<summary>Odpowiedź</summary>

Adapterami wyjściowymi są repozytoria na SQL (SQLAlchemy, Django ORM), klienci bramek płatności, nadawcy e-maili i SMS, publikatory wiadomości (Kafka, RabbitMQ), cache i magazyny plików oraz zegar czy generator identyfikatorów. Każdy przyjmuje typy domeny, woła bibliotekę i zwraca typy domeny, a szczegóły konfiguracji dostaje w konstruktorze. Dzięki temu można go podmienić na fake'a lub innego dostawcę bez zmian w rdzeniu.

Zobacz: [sekcja „Adaptery wyjściowe w Pythonie”](#adaptery-wyjściowe-w-pythonie).

</details>

### 14. Za co odpowiada adapter wejściowy, a czego nie powinien robić?

<details>
<summary>Odpowiedź</summary>

Adapter wejściowy odpowiada za tłumaczenie żądania z konkretnego protokołu (HTTP, CLI, kolejka) na wywołanie przypadku użycia oraz wyniku lub błędu z powrotem na odpowiedź protokołu. Obejmuje to parsowanie i walidację kształtu danych oraz uwierzytelnienie, którego tożsamość przekazuje do rdzenia. Nie powinien zawierać reguł biznesowych, obliczeń, bezpośrednich wywołań portów wyjściowych ani składania procesów z wielu przypadków użycia. Test: reguła, którą musiałbyś powielić w innym kanale wejścia, należy do rdzenia.

Zobacz: [sekcja „Zakres adaptera wejściowego”](#zakres-adaptera-wejściowego).

</details>

### 15. Dlaczego adapter powinien mapować modele zewnętrzne (ORM, DTO) na obiekty domenowe?

<details>
<summary>Odpowiedź</summary>

Adapter mapuje modele zewnętrzne (wiersze ORM, DTO dostawców) na obiekty domenowe, aby rdzeń nie zależał od kształtu wymuszonego przez technologię. Dzięki temu zmiana schematu bazy, wersji API czy biblioteki dotyka tylko adaptera, a nie reguł biznesowych. Rdzeń dostaje zwykłe obiekty bez sesji, leniwego ładowania i śledzenia zmian, więc testuje się go bez infrastruktury. Kosztem jest dodatkowy kod mapujący, ale to on chroni granicę.

Zobacz: [sekcja „Mapowanie modeli zewnętrznych”](#mapowanie-modeli-zewnętrznych).

</details>

### 16. Jak adapter powinien tłumaczyć wyjątki technologii na wyjątki zrozumiałe dla rdzenia?

<details>
<summary>Odpowiedź</summary>

Adapter łapie konkretne wyjątki biblioteki i rzuca w ich miejsce błędy zdefiniowane w rdzeniu, razem z portem, nazwane według znaczenia dla domeny. Błędy grupuje się według reakcji rdzenia (odmowa kontra awaria przejściowa), a nie według klas dostawcy. Oryginał zostaje jako przyczyna (`from exc`), a nierozpoznanych wyjątków się nie łapie. Dzięki temu rdzeń nie importuje SDK, a zmiana dostawcy dotyka tylko adaptera.

Zobacz: [sekcja „Tłumaczenie wyjątków w adapterze”](#tłumaczenie-wyjątków-w-adapterze).

</details>
