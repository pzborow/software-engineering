# Testowanie

Skoro use case'y dostają porty przez konstruktor, w testach podstawiamy w ich miejsce fake'i, bez bazy i HTTP. W przykładzie „Rowerek" przetestujemy StartRental i FinishRental na fake'ach, sprawdzimy RentalRepository testami kontraktowymi na fake'u i SQL oraz endpoint z podmienionym use case'em.

```text
test use case  -> fake'i portów (in-memory)
test kontraktowy -> fake  ┐
                 -> SQL   ┴ ten sam zestaw
test endpointu -> adapter HTTP -> use case (podmieniony)
```

## Testy use case'ów bez infrastruktury

Use case przyjmuje [porty wyjściowe](00%20Glosariusz.md#port-wyjściowy-driven) w konstruktorze, więc test sam składa go z prostych zamienników. Wystarczy [fake](00%20Glosariusz.md#fake), czyli działająca implementacja portu trzymana w pamięci (dokładniej omówimy go w następnej sekcji). Nie potrzeba bazy, sesji ani bramki płatności.

```text
test -> StartRental -> InMemoryRentalRepository
        (rdzeń)        (słownik w pamięci)
```

Test `StartRental` wygląda tak:

```python
# tests/test_start_rental.py
def test_start_rental_makes_rental_active():
    rentals = InMemoryRentalRepository()
    start_rental = StartRental(rentals)

    rental = start_rental("u1", "b1")

    assert rentals.active_for_user("u1") == rental
```

Test sprawdza zachowanie widoczne przez port (`active_for_user`), a nie to, jakie zapytania poszły do bazy. Dlatego przetrwa zmianę ORM albo schematu. Ten sam schemat działa dla `FinishRental`: podajemy fake repozytorium i fake `PaymentGateway`, który zapamiętuje wywołania `charge`, a potem sprawdzamy zwrócone `Money` i zapisane opłaty.

### Konsekwencja

Testy rdzenia biegną w milisekundach i można ich pisać dużo, także dla przypadków brzegowych: blokady przy zaległej płatności czy darmowych 20 minut. To, czy adapter naprawdę mówi do SQL, sprawdzamy osobno, w testach adapterów.

## Fake a mock

Fake to prawdziwa, działająca implementacja portu, tylko prostsza: `InMemoryRentalRepository` zamiast SQL trzyma wypożyczenia w słowniku. Mock (np. `unittest.mock.Mock`) niczego nie implementuje, tylko nagrywa wywołania, a test sprawdza, czy nastąpiły tak, jak zaplanował.

Fake ma własny stan zgodny z umową portu: po `add` kolejne `active_for_user` faktycznie zwraca zapisane wypożyczenie. Test weryfikuje więc **wynik** widoczny przez port:

```python
def test_start_rental_with_fake():
    rentals = InMemoryRentalRepository()
    rental = StartRental(rentals)("u1", "b1")
    assert rentals.active_for_user("u1") == rental
```

Mock weryfikuje **interakcję**, czyli to, jak use case woła port:

```python
# poza kanonem: ten sam test z mockiem
def test_start_rental_with_mock():
    rentals = Mock(spec=RentalRepository)
    rental = StartRental(rentals)("u1", "b1")
    rentals.add.assert_called_once_with(rental)
```

Różnica wychodzi przy refaktoryzacji. Załóżmy, że `StartRental` zaczyna przed zapisem wołać `active_for_user`, by egzekwować limit jednego wypożyczenia. Test z fake'iem przechodzi bez zmian, bo zachowanie się nie zmieniło. Test z mockiem pada: `active_for_user` zwraca teraz domyślnie obiekt `Mock`, traktowany jak istniejące wypożyczenie, więc trzeba dopisać zaprogramowaną odpowiedź.

| | Fake | Mock |
|---|---|---|
| Asercje | na wyniku i stanie | na wywołaniach metod |
| Refaktoryzacja use case'u | test przechodzi | test wymaga poprawek |

Konsekwencja: fake trzeba napisać i utrzymać, a jego zgodność z prawdziwym adapterem pilnują [testy kontraktowe](00%20Glosariusz.md#test-kontraktowy). W zamian jeden fake obsługuje wiele testów i przetrwa zmianę sposobu, w jaki use case woła port.

## Kiedy fake, a kiedy mock

Domyślnie wybieraj fake'i, a `unittest.mock` zostaw na rzadkie przypadki, w których wywołanie samo jest wymaganiem. Fake pasuje tam, gdzie port ma zachowanie, które test może obserwować, czyli stan, zapytania po zapisie i błędy.

Mock wystarcza dla portu bez obserwowalnego skutku, gdy liczy się samo wywołanie. Przykład to wysłanie SMS-a, gdy nie ma czego odczytać. Ma też sens na granicy, której nie kontrolujesz i nie chcesz odtwarzać.

Nawet błędy nie wymagają mocka. Port wyjściowy `PaymentGateway` można zastąpić fake'iem, który zapamiętuje obciążenia i na żądanie zgłasza `PaymentDeclined` lub `PaymentUnavailable`:

```python
class FakePaymentGateway:
    def __init__(self, fail_with: Exception | None = None) -> None:
        self.charged: list[tuple[str, Money]] = []
        self._fail_with = fail_with

    def charge(self, user_id: str, amount: Money) -> None:
        if self._fail_with:
            raise self._fail_with
        self.charged.append((user_id, amount))
```

Test `FinishRental` asertuje wtedy `gateway.charged == [("u1", Money(...))]`, czyli skutek, a nie sposób wywołania. Ścieżkę błędu sprawdza `FakePaymentGateway(fail_with=PaymentDeclined())`.

| Sytuacja | Wybór |
|---|---|
| Port ze stanem (repozytorium) | fake |
| Symulacja błędów portu | fake z wstrzykniętym błędem |
| Port bez obserwowalnego skutku | mock lub fake nagrywający |
| Cudzy klient, którego nie odtworzysz | mock na granicy adaptera |

Konsekwencja: fake to kod do utrzymania i może rozjechać się z prawdziwym adapterem. Tę zgodność sprawdzają testy kontraktowe, więc im częściej używasz fake'a, tym ważniejsze się stają.

## Testowanie adaptera repozytorium SQL

Adapter wyjściowy testuj na prawdziwej technologii, przez jego port, bez mocków sesji. Jego zadaniem jest tłumaczenie między domeną a bazą, więc tylko prawdziwa baza sprawdzi mapowanie, zapytania i ograniczenia schematu. Mock `Session` sprawdziłby jedynie, że wywołano `add`, a nie że wiersz da się odczytać.

Test ma dwa końce: wchodzi obiektem domenowym przez metodę portu i asertuje wynik odczytany również przez port. Dzięki temu nie zależy od nazw tabel ani od sposobu mapowania w `_to_domain`.

```python
@pytest.fixture
def repo(engine):
    with Session(engine) as session:
        yield SqlAlchemyRentalRepository(session)
        session.rollback()

def test_active_rental_roundtrip(repo):
    repo.add(Rental(id="r1", bike_id="b1", user_id="u1"))
    assert repo.active_for_user("u1") == Rental("r1", "b1", "u1")
    assert repo.active_for_user("u2") is None
```

Baza powinna być tak podobna do produkcyjnej, jak to możliwe. SQLite w pamięci jest szybki, ale różni się typami, blokadami i składnią, więc testy kontraktowe warto uruchamiać także na tym samym silniku co produkcja, np. w kontenerze PostgreSQL. Schemat twórz z migracji albo z metadanych modelu, a izolację zapewnij transakcją wycofywaną po teście.

Konsekwencja: testy adaptera są wolniejsze od testów use case'ów, więc jest ich mało i dotyczą wyłącznie tego, co adapter robi: zapisu, odczytu, mapowania i tłumaczenia błędów bazy. Reguły biznesowe zostają w szybkich testach na fake'ach.

## Testy kontraktowe portów

Test kontraktowy portu to zestaw testów napisany raz przeciw samemu [portowi](00%20Glosariusz.md#port-repozytorium), który uruchamiasz na każdej jego implementacji: na fake'u i na prawdziwym adapterze. Przechodzi na obu albo fake kłamie.

Fake w pamięci to druga implementacja portu, więc może z czasem odejść od zachowania bazy. Wtedy testy use case'ów są zielone, a produkcja się psuje. Kontrakt spina obie implementacje jednym zestawem asercji, np. „po `add` metoda `active_for_user` zwraca ten sam obiekt".

W pytest zrób klasę bazową z testami i fixture'em `repo`, który podklasy nadpisują. Nazwa bez prefiksu `Test` sprawia, że pytest nie zbiera jej samodzielnie.

```python
# poza kanonem: klasy testowe
class RentalRepositoryContract:
    def test_roundtrip(self, repo):
        repo.add(Rental("r1", "b1", "u1"))
        assert repo.active_for_user("u1") == Rental("r1", "b1", "u1")

class TestInMemoryRentalRepository(RentalRepositoryContract):
    @pytest.fixture
    def repo(self):
        return InMemoryRentalRepository()

class TestSqlAlchemyRentalRepository(RentalRepositoryContract):
    ...  # fixture repo jak w teście adaptera SQL
```

```text
RentalRepositoryContract ──► TestInMemoryRentalRepository ──► InMemoryRentalRepository
                         └─► TestSqlAlchemyRentalRepository ──► SqlAlchemyRentalRepository
```

Alternatywą jest fixture z `params=["fake", "sql"]`. Klasy dają jednak czytelniejsze nazwy testów i pozwalają oznaczyć wariant SQL markerem, np. `integration`.

Konsekwencja: nowe zachowanie portu dopisujesz w jednym miejscu i od razu sprawdzasz je na obu implementacjach. Błąd wykryty tylko na SQL najpierw dodaj do kontraktu, a potem popraw fake'a.

## Testowanie endpointu HTTP

Endpoint to [adapter](00%20Glosariusz.md#adapter) wejściowy, więc jego test ma sprawdzić tylko tłumaczenie: czy poprawne JSON-em żądanie dociera do [przypadku użycia](00%20Glosariusz.md#przypadek-użycia) z właściwymi argumentami i czy wynik wraca jako oczekiwana odpowiedź. Reguły (limit wypożyczeń, blokada za zaległą płatność) sprawdziłeś już w testach use case'ów, więc tu użyj zaślepki.

Mechanizmem jest `app.dependency_overrides`. Podmieniasz dependency, które w composition root buduje use case, oraz `current_user`, więc nie potrzebujesz tokenu ani sesji. Przypadek użycia jest wywoływalny (`__call__`), więc zaślepką może być zwykła funkcja.

```python
# app/composition.py · nowe dependency
def get_start_rental(session: Session = Depends(get_session)) -> StartRental: ...

def test_start_rental_returns_created_rental():
    calls = []
    def use_case(user_id, bike_id):
        calls.append((user_id, bike_id))
        return Rental("r1", bike_id, user_id)

    app.dependency_overrides[get_start_rental] = lambda: use_case
    app.dependency_overrides[current_user] = lambda: AuthUser(...)  # u1
    res = TestClient(app).post("/rentals", json={"bike_id": "b1"})

    assert res.status_code == 200 and res.json()["id"] == "r1"
    assert calls == [("u1", "b1")]
```

Sprawdzasz tu trzy rzeczy: kształt odpowiedzi, przekazanie tożsamości z uwierzytelnienia (nie z ciała żądania) i mapowanie na status. Analogicznie zaślepka rzucająca błąd rdzenia pokazuje, jaki kod HTTP zwraca adapter.

Po teście czyść `dependency_overrides` w fixture'ze, żeby podmiany nie wyciekły do innych testów. Konsekwencja: test działa w milisekundach i łamie się tylko wtedy, gdy zmieni się kontrakt HTTP.

## Co zapamiętać

- Skoro use case zna tylko porty, jego testy jednostkowe składają go z fake'ów w pamięci i sprawdzają reguły biznesowe bez bazy, sieci i frameworka.
- Fake asertuje wynik i stan przez port, mock asertuje wywołania, dlatego testy z fake'iem przeżywają refaktoryzację, która łamie testy z mockiem.
- Wybieraj fake, gdy port ma zachowanie do zaobserwowania (stan, błędy), a mock tylko wtedy, gdy samo wywołanie jest wymaganiem.
- Adapter SQL testuj na prawdziwej bazie przez metody portu (zapis, odczyt, asercja na obiektach domenowych), a nie na mocku sesji.
- Kontrakt portu piszesz raz i uruchamiasz na fake'u oraz prawdziwym adapterze, by fake nie odszedł od zachowania produkcji.
- Endpoint testuj przez TestClient z podmienionymi przez dependency_overrides use case'em i uwierzytelnieniem, sprawdzając tylko tłumaczenie żądania i odpowiedzi.

## Pytania sprawdzające

### 29. Jak architektura heksagonalna ułatwia testy jednostkowe use case'ów?

<details>
<summary>Odpowiedź</summary>

Use case zależy tylko od portów zdefiniowanych w rdzeniu, więc w teście można podać mu dowolne implementacje tych portów, np. fake'i w pamięci. Test uruchamia scenariusz jak zwykłą funkcję Pythona: bez bazy, sieci, frameworka i migracji. Dzięki temu testy są szybkie, deterministyczne i sprawdzają reguły biznesowe, a nie konfigurację technologii.

Zobacz: [sekcja „Testy use case'ów bez infrastruktury”](#testy-use-caseów-bez-infrastruktury).

</details>

### 30. Czym jest fake (adapter in-memory) i czym różni się od mocka?

<details>
<summary>Odpowiedź</summary>

Fake to działająca, uproszczona implementacja portu, np. repozytorium trzymające dane w słowniku, z własnym stanem zgodnym z umową portu. Mock nie ma logiki: nagrywa wywołania i pozwala sprawdzić, że nastąpiły w oczekiwany sposób. Fake pozwala więc asertować wynik i stan, a mock interakcję z portem. Dlatego testy z fake'iem są odporniejsze na refaktoryzację use case'u, ale sam fake trzeba utrzymywać i weryfikować testami kontraktowymi.

Zobacz: [sekcja „Fake a mock”](#fake-a-mock).

</details>

### 31. Kiedy preferować fake'i zamiast unittest.mock?

<details>
<summary>Odpowiedź</summary>

Preferuj fake'i wszędzie tam, gdzie port ma zachowanie obserwowalne dla testu: stan, zapytania po zapisie albo błędy, które można wstrzyknąć. Wtedy test sprawdza skutek, a nie sposób wywołania portu, więc przeżywa refaktoryzację. Mock zostaw dla portów bez obserwowalnego skutku, gdy samo wywołanie jest wymaganiem, oraz dla cudzych klientów, których nie opłaca się odtwarzać. Za fake'i płacisz utrzymaniem kodu i potrzebą testów kontraktowych, które pilnują jego zgodności z prawdziwym adapterem.

Zobacz: [sekcja „Kiedy fake, a kiedy mock”](#kiedy-fake-a-kiedy-mock).

</details>

### 32. Jak testować adapter wyjściowy, np. repozytorium SQL?

<details>
<summary>Odpowiedź</summary>

Adapter wyjściowy, np. repozytorium SQL, testuje się na prawdziwej bazie, przez metody portu: zapisujesz obiekt domenowy i odczytujesz go z powrotem tym samym portem. Mock sesji niczego nie dowodzi, bo mapowanie, zapytania i ograniczenia schematu sprawdzi tylko realna baza, najlepiej ten sam silnik co produkcyjny. Każdy test dostaje izolację przez transakcję wycofywaną po teście. Takich testów jest mało, bo dotyczą tylko pracy adaptera, a reguły biznesowe sprawdzają szybkie testy na fake'ach.

Zobacz: [sekcja „Testowanie adaptera repozytorium SQL”](#testowanie-adaptera-repozytorium-sql).

</details>

### 33. Czym są testy kontraktowe portów i jak uruchomić ten sam zestaw na fake'u i prawdziwym adapterze w pytest?

<details>
<summary>Odpowiedź</summary>

Test kontraktowy portu to zestaw asercji napisany raz przeciw portowi i uruchamiany na każdej jego implementacji, czyli na fake'u i na prawdziwym adapterze. Gwarantuje, że fake zachowuje się jak baza, więc testy use case'ów nie kłamią. W pytest robi się to klasą bazową z testami i fixture'em `repo`, który nadpisują podklasy: jedna zwraca fake'a, druga adapter SQL. Nowe zachowanie dopisujesz w jednym miejscu i sprawdzasz na obu.

Zobacz: [sekcja „Testy kontraktowe portów”](#testy-kontraktowe-portów).

</details>

### 34. Jak przetestować adapter wejściowy, np. endpoint HTTP, bez realnej infrastruktury?

<details>
<summary>Odpowiedź</summary>

Adapter wejściowy testujesz przez klienta testowego frameworka (w FastAPI `TestClient`), w którym podmieniasz przypadek użycia i uwierzytelnienie na proste zaślepki. Nie potrzeba serwera, bazy ani sieci. Test sprawdza tylko zadanie adaptera: tłumaczenie żądania HTTP na wywołanie use case'u oraz wyniku na status i JSON. Reguły biznesowe mają własne testy w rdzeniu.

Zobacz: [sekcja „Testowanie endpointu HTTP”](#testowanie-endpointu-http).

</details>
