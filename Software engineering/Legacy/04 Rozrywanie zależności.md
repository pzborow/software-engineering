# Rozrywanie zależności

Testy z rozdziału 03 zabezpieczają przepływ, ale są wolne, kruche i znają szczegóły modułów. Żeby napisać szybkie, precyzyjne testy i bezpiecznie dodawać nowe funkcje, trzeba sprawić, żeby kod dało się uruchomić w teście bez prawdziwej bazy, sieci i zegara. Feathers opisuje w tym celu kilkadziesiąt technik. Ten rozdział pokazuje najważniejsze z nich, każdą na przykładzie „przed i po”.

```text
problem                                   technika
kod sam tworzy zależność                  parametryzacja, wstrzyknięcie przez konstruktor lub parametr
nowa funkcja w kodzie bez testów          sprout method, sprout class
zachowanie przed lub po starym kodzie     wrap method, wrap class
globalny obiekt, singleton, statyk        akcesor z możliwością podmiany, przekazanie w parametrze
konkretna klasa zamiast abstrakcji        extract interface, subclass and override
```

## Miejsce, w którym można zmienić zachowanie

<a id="term-seam"></a>[Szew](00%20Glossary%20Legacy.md#seam) (seam) to według Feathersa miejsce, w którym można zmienić zachowanie programu bez edytowania kodu w tym miejscu. Każdy szew ma <a id="term-enabling-point"></a>[punkt włączenia](00%20Glossary%20Legacy.md#enabling-point) (enabling point), czyli miejsce, w którym decyduje się, które zachowanie zostanie użyte.

W Pythonie występują cztery rodzaje szwów:

| Rodzaj | Punkt włączenia | Przykład |
|---|---|---|
| obiektowy | przekazanie innego obiektu | `InvoiceGenerator(db=FakeDb())` |
| przez parametr | argument funkcji z wartością domyślną | `generate_invoice(1001, clock=lambda: FIXED)` |
| przez moduł | nazwa w przestrzeni modułu | `monkeypatch.setattr("billing.invoices.DB", test_db)` |
| przez konfigurację | ustawienia, zmienne środowiskowe | `KSEF_URL=http://localhost:9999` |

W oryginalnym `generate_invoice` jedynymi szwami są moduł i konfiguracja. Działają, ale ich punkt włączenia jest daleko od kodu i łatwo o nim zapomnieć. Celem rozrywania zależności jest dodanie szwów obiektowych i przez parametr, które są jawne i czytelne.

## Wstrzyknięcie bez przepisywania

Najprostszą techniką jest parametryzacja: zależność, którą kod tworzy albo pobiera sam, staje się parametrem z wartością domyślną równą dotychczasowemu zachowaniu. Istniejący kod wywołujący nie zmienia się wcale.

```python
# przed: zależności ukryte w środku funkcji
def generate_invoice(order_id):
    order = DB.query("SELECT * FROM orders WHERE id=%s", order_id)[0]
    ...
    if order["coupon"] == "BLACKFRIDAY" and datetime.datetime.now().month == 11:
        ...
    requests.post(settings.KSEF_URL, json={...})
    send_mail(customer["email"], ...)


# po: parametry z wartościami domyślnymi, wywołania bez zmian
def generate_invoice(order_id, db=None, now=None, post=None, mail=None):
    db = db or DB
    now = now or datetime.datetime.now
    post = post or requests.post
    mail = mail or send_mail

    order = db.query("SELECT * FROM orders WHERE id=%s", order_id)[0]
    ...
    if order["coupon"] == "BLACKFRIDAY" and now().month == 11:
        ...
    post(settings.KSEF_URL, json={...})
    mail(customer["email"], ...)
```

Wersja obiektowa to <a id="term-parameterize-constructor"></a>[parametryzacja konstruktora](00%20Glossary%20Legacy.md#parameterize-constructor): funkcja staje się klasą, a zależności przychodzą przez konstruktor, z domyślnymi wartościami dla starego kodu.

```python
class InvoiceGenerator:
    def __init__(self, db=None, clock=None, ksef=None, mailer=None):
        self._db = db or DB
        self._clock = clock or SystemClock()
        self._ksef = ksef or KsefClient(settings.KSEF_URL)
        self._mailer = mailer or SmtpMailer()

    def generate(self, order_id):
        ...


def generate_invoice(order_id):                     # stary punkt wejścia zostaje
    return InvoiceGenerator().generate(order_id)
```

Obie zmiany są mechaniczne i małe, więc można je zrobić, mając tylko testy end-to-end z rozdziału 03. Po nich test nie potrzebuje już `monkeypatch` ani `freezegun`:

```python
def test_generate_invoice_with_fakes():
    db = FakeDb.with_order(1001, items=[item("books", 100, 2)], customer=pl_consumer())
    ksef, mailer = FakeKsef(), FakeMailer()
    gen = InvoiceGenerator(db=db, clock=FixedClock("2026-03-15"), ksef=ksef, mailer=mailer)

    number = gen.generate(1001)

    assert number == "FV/2026/1"
    assert ksef.sent == [{"number": "FV/2026/1", "total": 210.0}]
    assert mailer.sent[0].to == "anna@example.com"
```

## Nowy kod obok starego

Biznes chce nowej funkcji: dopłaty 5 zł za płatność przy odbiorze. Najprościej dopisać `if` do 400-liniowej funkcji, ale wtedy nowy kod jest równie nietestowalny jak stary.

<a id="term-sprout-method"></a>[Sprout method](00%20Glossary%20Legacy.md#sprout-method) polega na napisaniu nowej logiki jako osobnej funkcji z testami i wywołaniu jej ze starego kodu jedną linią:

```python
# nowa, w pełni testowana funkcja
COD_FEE = Decimal("5.00")

def cash_on_delivery_fee(payment_method: str, total: Decimal) -> Decimal:
    if payment_method != "cod":
        return Decimal("0")
    if total >= Decimal("300"):
        return Decimal("0")                    # darmowe powyżej 300 zł
    return COD_FEE


def test_cod_fee_waived_above_300():
    assert cash_on_delivery_fee("cod", Decimal("300")) == Decimal("0")


# w starym kodzie: jedna nowa linia
def generate_invoice(order_id, db=None, now=None, post=None, mail=None):
    ...
    total = round(total, 2)
    total += float(cash_on_delivery_fee(order["payment_method"], Decimal(str(total))))   # nowe
    ...
```

<a id="term-sprout-class"></a>[Sprout class](00%20Glossary%20Legacy.md#sprout-class) to ta sama idea, gdy nowa logika jest większa albo gdy starej klasy nie da się nawet utworzyć w teście. Nową funkcję pisze się jako osobną klasę z testami, a stary kod tworzy ją i woła:

```python
class EuB2BVatRules:                              # nowe reguły VAT dla firm z UE, osobna klasa
    def __init__(self, vies: ViesClient):
        self._vies = vies

    def rate_for(self, customer: dict, category: str) -> Decimal:
        if customer["type"] == "B2B" and customer["country"] != "PL":
            if self._vies.is_valid(customer["vat_id"]):
                return Decimal("0")               # odwrotne obciążenie tylko z ważnym NIP UE
        return STANDARD_RATES[category]
```

Sprout nie poprawia starego kodu, ale zatrzymuje jego rozrost: każda nowa funkcja jest przetestowana i odseparowana. Wadą jest to, że stary kod na razie zostaje, a logika żyje w dwóch miejscach. Z czasem kolejne fragmenty wychodzą ze starej funkcji do nowych.

## Zachowanie przed lub po

Czasem nowe zachowanie ma nastąpić przed albo po starym, a nie w jego środku. Dział prawny chce, żeby każda wygenerowana faktura trafiała do dziennika audytu.

<a id="term-wrap-method"></a>[Wrap method](00%20Glossary%20Legacy.md#wrap-method) polega na zmianie nazwy starej funkcji i utworzeniu nowej o dotychczasowej nazwie, która woła starą i dodaje nowe zachowanie:

```python
# stara funkcja dostaje nową nazwę, jej treść się nie zmienia
def _generate_invoice_core(order_id, db=None, now=None, post=None, mail=None):
    ...                                           # 400 starych linii


# nowa funkcja o starej nazwie: wszyscy wywołujący dostają audyt automatycznie
def generate_invoice(order_id, audit=None, **deps):
    audit = audit or AuditLog()
    number = _generate_invoice_core(order_id, **deps)
    audit.record("invoice_generated", order_id=order_id, number=number)
    return number
```

<a id="term-wrap-class"></a>[Wrap class](00%20Glossary%20Legacy.md#wrap-class) to ta sama idea na poziomie klasy, czyli w praktyce wzorzec Decorator. KSeF czasem odpowiada błędem 503 i trzeba ponawiać wysyłkę. Zamiast zmieniać klienta KSeF, owija się go:

```python
class RetryingKsefClient:
    def __init__(self, inner, attempts: int = 3, sleep=time.sleep):
        self._inner = inner
        self._attempts = attempts
        self._sleep = sleep

    def send(self, invoice: dict) -> None:
        for attempt in range(1, self._attempts + 1):
            try:
                return self._inner.send(invoice)
            except KsefUnavailable:
                if attempt == self._attempts:
                    raise
                self._sleep(2 ** attempt)


ksef = RetryingKsefClient(KsefClient(settings.KSEF_URL))
```

Wrap dodaje zachowanie bez dotykania starego kodu i jest łatwy do przetestowania osobno. Działa tylko wtedy, gdy nowe zachowanie da się umieścić przed albo po starym, a nie w jego środku.

## Globalne obiekty i singletony

`DB` w kodzie fakturowania to globalny obiekt tworzony przy imporcie modułu. Kod legacy często ma ich więcej: `settings`, `cache`, `logger`, klientów HTTP tworzonych jako zmienne modułu, klasy z metodami statycznymi. W teście nie da się ich łatwo podmienić, a jeśli się da (`monkeypatch`), podmiana przecieka między testami, jeśli ktoś zapomni ją cofnąć.

Techniki, od najprostszej:

1. Przekazanie w parametrze, jak w sekcji o wstrzyknięciu. Globalny obiekt zostaje wartością domyślną, ale kod, który go używa, już od niego nie zależy.
2. Akcesor zamiast bezpośredniego dostępu (w terminologii Feathersa introduce static setter). Kod woła funkcję, a test może ustawić inną instancję:

```python
# shop/db.py
_db = None

def get_db():
    global _db
    if _db is None:
        _db = Database(settings.DATABASE_URL)
    return _db

def set_db_for_tests(db):                    # tylko dla testów, jawnie nazwane
    global _db
    _db = db
```

3. Zamiana wywołań statycznych i funkcji modułu na metody obiektu wstrzykiwanego przez konstruktor. `datetime.datetime.now()` staje się `self._clock.now()`, a `requests.post` metodą `self._http.post`.
4. Dla klas będących singletonami: konstruktor pozostaje prywatny w użyciu produkcyjnym, ale w teście tworzy się osobną instancję i przekazuje ją jawnie.

Kierunek jest zawsze ten sam: globalny stan przesuwa się z wnętrza logiki na brzegi aplikacji, gdzie jest składany raz, przy starcie.

## Abstrakcja wydzielona z konkretu

<a id="term-extract-interface"></a>[Extract interface](00%20Glossary%20Legacy.md#extract-interface) polega na opisaniu metod, których kod używa z konkretnej klasy, jako interfejsu, żeby w teście podstawić inną implementację. W Pythonie interfejsem jest `Protocol`, więc istniejąca klasa nie musi nic dziedziczyć:

```python
class InvoiceStore(Protocol):
    def next_number(self, year: int) -> str: ...
    def save(self, number: str, order_id: int, total: Decimal) -> None: ...


class SqlInvoiceStore:                     # istniejący kod SQL przeniesiony tutaj, bez zmian logiki
    ...


class InMemoryInvoiceStore:                # do testów
    def __init__(self):
        self.saved, self._seq = [], 0

    def next_number(self, year: int) -> str:
        self._seq += 1
        return f"FV/{year}/{self._seq}"

    def save(self, number, order_id, total):
        self.saved.append((number, order_id, total))
```

<a id="term-subclass-and-override"></a>[Subclass and override method](00%20Glossary%20Legacy.md#subclass-and-override) to technika na sytuację, gdy zależność jest wywoływana z metody klasy, a nie da się jej łatwo wstrzyknąć. Wydziela się problematyczne wywołanie do osobnej metody, a w teście tworzy się podklasę, która tę metodę nadpisuje:

```python
class LegacyInvoiceService:
    def generate(self, order_id):
        ...
        self._send_to_ksef(number, total)            # wydzielone wywołanie sieciowe
        ...

    def _send_to_ksef(self, number, total):
        requests.post(settings.KSEF_URL, json={"number": number, "total": total})


class TestableInvoiceService(LegacyInvoiceService):   # tylko w testach
    def __init__(self):
        self.ksef_calls = []

    def _send_to_ksef(self, number, total):
        self.ksef_calls.append((number, total))
```

To technika przejściowa. Pozwala szybko objąć klasę testami, ale test zależy od wewnętrznej struktury klasy. Docelowo zależność powinna przyjść przez konstruktor.

<a id="term-monkeypatching"></a>[Monkeypatching](00%20Glossary%20Legacy.md#monkeypatching), czyli podmiana atrybutu modułu lub klasy w czasie działania, to w Pythonie najłatwiejszy szew i zarazem pułapka.

| Kiedy wolno | Kiedy to pułapka |
|---|---|
| testy charakteryzujące przed rozerwaniem zależności | stały sposób testowania nowego kodu |
| zależność biblioteki, której nie kontrolujesz (np. `time.sleep`) | podmiana w złym miejscu: `patch("datetime.datetime.now")` zamiast tam, gdzie nazwa jest używana |
| jednorazowo, przez `monkeypatch` z automatycznym cofnięciem | podmiana globalna bez cofnięcia, przeciekająca między testami |
| krótki okres przejściowy z planem zastąpienia szwem | test, który podmienia pięć rzeczy, żeby przetestować jedną |

Test, który potrzebuje dużo monkeypatchingu, mówi, że kod ma za dużo ukrytych zależności. To sygnał, żeby wprowadzić prawdziwy szew, a nie powód, żeby dodać kolejną podmianę.

## Co zapamiętać

- Szew to miejsce, w którym można zmienić zachowanie bez edycji kodu, a punkt włączenia decyduje o wyborze. W Pythonie są szwy obiektowe, przez parametr, przez moduł i przez konfigurację.
- Parametryzacja z wartościami domyślnymi wstrzykuje zależności bez zmiany wywołujących.
- Sprout method i sprout class dodają nową logikę obok starej, w pełni przetestowaną.
- Wrap method i wrap class dodają zachowanie przed lub po starym kodzie bez jego zmiany.
- Globalne obiekty przesuwa się na brzegi: parametr, akcesor z podmianą, obiekt wstrzykiwany przez konstruktor.
- Extract interface (`Protocol`) i subclass and override dają szwy w konkretnych klasach. Drugie jest techniką przejściową.
- Monkeypatching jest dobry na start i dla bibliotek, ale jego nadmiar sygnalizuje brak prawdziwych szwów.

## Pytania sprawdzające

### 13. Czym jest szew (seam) według Feathersa i jakie są jego rodzaje (obiektowy, przez parametr, przez moduł, przez konfigurację)?

<details>
<summary>Odpowiedź</summary>

Szew to miejsce, w którym można zmienić zachowanie programu bez edytowania kodu w tym miejscu. Punkt włączenia to miejsce, w którym wybiera się zachowanie. W Pythonie są szwy obiektowe (przekazanie innego obiektu), przez parametr (argument z wartością domyślną), przez moduł (podmiana nazwy w przestrzeni modułu, `monkeypatch`) i przez konfigurację (ustawienia, zmienne środowiskowe). Legacy zwykle ma tylko szwy przez moduł i konfigurację, a celem jest dodanie jawnych szwów obiektowych i przez parametr.

Zobacz: sekcja „Miejsce, w którym można zmienić zachowanie”.

</details>

### 14. Jak wstrzyknąć zależność do kodu, który tworzy ją sam (parametryzacja konstruktora, parametr z wartością domyślną)?

<details>
<summary>Odpowiedź</summary>

Zależność staje się parametrem z wartością domyślną równą dotychczasowemu zachowaniu: `generate_invoice(order_id, db=None, now=None, ...)` z `db = db or DB`. Wywołujący nie zmieniają się wcale. W wersji obiektowej (parametryzacja konstruktora) funkcja staje się klasą, zależności przychodzą przez `__init__` z domyślnymi wartościami, a stary punkt wejścia zostaje jako cienka funkcja. Zmiany są mechaniczne, więc można je zrobić pod ochroną testów end-to-end, a potem pisać testy z fake'ami bez `monkeypatch`.

Zobacz: sekcja „Wstrzyknięcie bez przepisywania”.

</details>

### 15. Czym są sprout method i sprout class? Kiedy dodać nowy kod obok starego zamiast w środku?

<details>
<summary>Odpowiedź</summary>

Sprout method: nową logikę pisze się jako osobną, przetestowaną funkcję i wywołuje ze starego kodu jedną linią (np. `cash_on_delivery_fee`). Sprout class: to samo, gdy logika jest większa albo starej klasy nie da się utworzyć w teście (np. `EuB2BVatRules`). Stosuje się je przy każdej nowej funkcji w nietestowalnym kodzie, bo zatrzymują jego rozrost i dają pełne testy nowej logiki. Wadą jest to, że stary kod zostaje, a logika żyje w dwóch miejscach, dopóki kolejne fragmenty nie zostaną wydzielone.

Zobacz: sekcja „Nowy kod obok starego”.

</details>

### 16. Czym jest wrap method i wrap class? Jak dodać zachowanie przed lub po starym kodzie bez jego zmiany?

<details>
<summary>Odpowiedź</summary>

Wrap method: stara funkcja dostaje nową nazwę (np. `_generate_invoice_core`), a nowa funkcja o starej nazwie woła ją i dodaje zachowanie przed lub po (np. zapis do dziennika audytu). Wszyscy wywołujący dostają nowe zachowanie automatycznie. Wrap class to ta sama idea dla klasy, czyli wzorzec Decorator, np. `RetryingKsefClient` owijający klienta KSeF ponowieniami. Działa, gdy nowe zachowanie można umieścić przed lub po starym, a nie w jego środku.

Zobacz: sekcja „Zachowanie przed lub po”.

</details>

### 17. Jak radzić sobie z globalnymi zmiennymi, singletonami i metodami statycznymi, których nie da się podmienić w teście?

<details>
<summary>Odpowiedź</summary>

Przesuwać globalny stan z wnętrza logiki na brzegi aplikacji. Kolejne techniki: przekazanie w parametrze z globalnym obiektem jako wartością domyślną, akcesor zamiast bezpośredniego dostępu z jawnie nazwaną funkcją do podmiany w testach (introduce static setter), zamiana wywołań statycznych i funkcji modułu (`datetime.now()`, `requests.post`) na metody obiektu wstrzykiwanego przez konstruktor oraz tworzenie osobnych instancji singletonów w testach i przekazywanie ich jawnie. Monkeypatch globalnego obiektu bez cofnięcia przecieka między testami.

Zobacz: sekcja „Globalne obiekty i singletony”.

</details>

### 18. Czym jest extract interface i subclass and override? Kiedy wolno użyć monkeypatchingu w testach, a kiedy to pułapka?

<details>
<summary>Odpowiedź</summary>

Extract interface opisuje używane metody konkretnej klasy jako interfejs (w Pythonie `Protocol`), żeby w teście podstawić inną implementację (np. `InMemoryInvoiceStore`). Subclass and override wydziela problematyczne wywołanie do metody i nadpisuje ją w podklasie testowej. To technika przejściowa, bo test zależy od struktury klasy. Monkeypatching wolno stosować w testach charakteryzujących, dla bibliotek spoza naszej kontroli i jednorazowo z automatycznym cofnięciem. Pułapką jest jako stały sposób testowania, przy podmianie w złym miejscu, przy wycieku między testami i gdy test podmienia wiele rzeczy naraz, bo to sygnał braku prawdziwych szwów.

Zobacz: sekcja „Abstrakcja wydzielona z konkretu”.

</details>
