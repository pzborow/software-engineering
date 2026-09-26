# Wstrzykiwanie zależności i kompozycja

Porty i adaptery już istnieją, ale ktoś musi je połączyć w działającą aplikację. Ten dział pokazuje, jak wstrzykiwać zależności i gdzie zebrać całe okablowanie w composition root, razem z cyklem życia sesji SQL. W „Rowerku” zrobimy to ręcznie, potem przez FastAPI Depends, a na końcu opcjonalnie kontenerem DI.

```text
composition root
  |-- tworzy adapter (SQL, HTTP...) --> implementuje port
  '-- wstrzykuje adapter do use case'u przez konstruktor
FastAPI Depends --> use case --> port <-- adapter (sesja: otwórz/zamknij)
```

## DI a porty i adaptery

[Wstrzykiwanie zależności](00%20Glosariusz.md#wstrzykiwanie-zależności) to mechanizm, dzięki któremu rdzeń dostaje konkretny adapter, choć zna tylko port. [Odwrócenie zależności](00%20Glosariusz.md#zasada-odwrócenia-zależności) mówi, *kto od kogo zależy*; wstrzykiwanie rozwiązuje *skąd się bierze obiekt* w czasie działania. Bez niego port byłby tylko deklaracją bez implementacji.

Mechanizm: use case deklaruje w konstruktorze zależność typu portu, a ktoś spoza rdzenia podaje adapter. `FinishRental` prosi o `RentalRepository` i `PaymentGateway`, więc nie importuje niczego z `infra/`. Ten "ktoś" to [composition root](00%20Glosariusz.md#composition-root), czyli jedno miejsce na brzegu aplikacji, które tworzy adaptery i łączy je z use case'ami.

```python
# composition root, np. app/main.py
session = Session(engine)
finish_rental = FinishRental(
    rentals=SqlAlchemyRentalRepository(session),
    payments=StripePaymentGateway(),
)
```

Kierunek importów jest tu kluczowy:

```text
app/main.py ──► infra/*  ──► core/ports.py
     └────────────────────► core/use_cases.py ──► core/ports.py
```

Composition root zna wszystko, adaptery znają rdzeń, a rdzeń nie zna nikogo. Podmiana adaptera to zmiana jednej linii w okablowaniu, a w testach wstrzykujesz [fake'a](00%20Glosariusz.md#fake).

### Konsekwencja

Port bez wstrzykiwania jest martwy, a wstrzykiwanie bez portu daje tylko luźno typowane zależności. Dopiero razem dają wymienność adapterów bez dotykania rdzenia.

## Composition root: gdzie go umieścić

Composition root to jedyne miejsce w aplikacji, które zna zarówno rdzeń, jak i adaptery, i na starcie składa z nich graf obiektów. Umieść go jak najbliżej punktu wejścia procesu, poza pakietami `core/` i `infra/`, np. w osobnym pakiecie `app/`.

Skoro musi importować wszystko, nie może leżeć w rdzeniu ani w żadnym adapterze. Gdyby `core/` importował `infra/`, odwróciłbyś kierunek zależności. Gdyby robił to adapter, ukryłbyś okablowanie w kodzie technologii.

```text
app/
  composition.py   # build_*: tworzy adaptery i use case'y
  main.py          # punkt wejścia HTTP: FastAPI, routery
  worker.py        # punkt wejścia konsumenta zamków
```

Każdy proces ma własny punkt wejścia, a wspólne okablowanie wyciągasz do jednej funkcji:

```python
# app/composition.py
def build_finish_rental(session: Session) -> FinishRental:
    return FinishRental(
        rentals=SqlAlchemyRentalRepository(session),
        payments=StripePaymentGateway(),
    )
```

Composition root tylko tworzy i łączy obiekty, bez reguł biznesowych i bez logiki warunkowej poza wyborem adaptera (np. z konfiguracji). Wywołuj go raz przy starcie albo raz na żądanie, gdy zależność ma krótszy cykl życia, jak sesja SQL.

### Konsekwencja

Cała wiedza o tym, co z czym jest połączone, mieści się w jednym katalogu. Router i `LockEventConsumer` dostają gotowe use case'y, a testy budują własny graf z fake'ów, nie dotykając `app/`.

## Wstrzykiwanie przez konstruktor

Klasa deklaruje zależności jako parametry `__init__`, zapisuje je w polach i nigdy sama ich nie tworzy. Wywołujący, czyli composition root albo test, przekazuje gotowe obiekty. Do tego wystarczy Python, bez żadnego frameworka.

Mechanizm ma trzy reguły. Typy parametrów to porty z rdzenia (`RentalRepository`, `PaymentGateway`), nigdy klasy z `infra/`. Zależności są wymagane, bez wartości domyślnych w rodzaju `payments=StripePaymentGateway()`, bo taki default po cichu wciąga adapter do rdzenia. Konstruktor tylko przypisuje pola, bez I/O i logiki, więc obiekt jest gotowy do użycia zaraz po utworzeniu.

```python
# core/use_cases.py
class FinishRental:
    def __init__(self, rentals: RentalRepository, payments: PaymentGateway) -> None:
        self._rentals = rentals
        self._payments = payments
```

Ręczne okablowanie działa od liści do korzeni: najpierw adaptery bez zależności, potem te, które ich potrzebują, na końcu use case'y. Robi to `build_finish_rental` z poprzedniej sekcji. Kolejność wymusza sama sygnatura konstruktora, a brakujący argument kończy się `TypeError` przy starcie, nie w środku żądania.

Nazwane argumenty w wywołaniu konstruktora czynią okablowanie czytelnym, a type checker sprawdza, czy adapter pasuje do portu.

### Konsekwencja

Testy podają fake'i tym samym konstruktorem, bez patchowania importów. Cena to ręczne pisanie funkcji `build_*`, co przy kilkunastu use case'ach jest nadal tanie i jawne.

## FastAPI Depends w okablowaniu

`Depends` to wbudowane w FastAPI wstrzykiwanie zależności: framework wywołuje wskazaną funkcję, a jej wynik podstawia jako argument handlera. Sam graf providerów jest więc częścią okablowania, nie logiki.

### Gdzie Depends pomaga

Provider to cienka funkcja w `app/composition.py`, która deleguje do ręcznego buildera. Router deklaruje tylko, czego chce.

```python
# app/composition.py
def get_finish_rental(session: Session = Depends(get_session)) -> FinishRental:
    return build_finish_rental(session)

# infra/rentals_router.py
@router.post("/rentals/{rental_id}/finish")
def finish(rental_id: str, use_case: FinishRental = Depends(get_finish_rental)) -> ...: ...
```

Zyskujesz jedną rzecz: framework zarządza zakresem żądania, a testy HTTP podmieniają providera przez `app.dependency_overrides`. Logika składania obiektów nadal siedzi w `build_finish_rental`, więc da się ją użyć poza FastAPI, np. w `LockEventConsumer`.

### Gdzie zaczyna szkodzić

```python
# poza kanonem
class FinishRental:
    def __init__(self, rentals: RentalRepository = Depends(get_rentals)) -> None: ...
```

Import `fastapi` w `core/` łamie kierunek zależności. Gorzej, że `Depends(...)` działa tylko wewnątrz wywołań rozwiązywanych przez FastAPI. Wywołany z testu, konsumenta kolejki lub CLI, use case dostaje w polu obiekt `Depends`, nie repozytorium, i błąd wychodzi dopiero przy użyciu.

Reguła: `Depends` wolno stosować w adapterach i w `app/`, nigdy w `core/`. Rdzeń dalej przyjmuje zależności przez konstruktor.

## Kontener DI czy ręczne okablowanie

Domyślnie okablowuj ręcznie. Kontener DI warto dołożyć dopiero wtedy, gdy ręczny composition root zaczyna być kosztem: graf ma dziesiątki obiektów, wiele punktów wejścia go powtarza, a różne zależności żyją w różnych zakresach. [Kontener DI](00%20Glosariusz.md#kontener-di) to biblioteka, która sama buduje graf obiektów na podstawie zarejestrowanych typów i zakresów życia.

### Co kontener daje, a czego nie

Kontener automatyzuje to, co w `app/composition.py` robią funkcje w rodzaju `build_finish_rental`: dopasowuje parametry konstruktorów do zarejestrowanych implementacji portów. Zyskujesz mniej powtarzalnego kodu, jedno miejsce z rejestracją i deklaratywne zakresy (singleton, na żądanie). Płacisz tym, że graf staje się niejawny: brakującą rejestrację widać dopiero przy starcie lub w runtime, a nie w czytelnym wywołaniu konstruktora.

| Sytuacja | Wybór |
|---|---|
| kilka use case'ów, jeden–dwa punkty wejścia | ręcznie |
| kilkadziesiąt use case'ów, HTTP + konsument + CLI + zadania | kontener |
| tylko zakres żądania w HTTP | `Depends` |
| zależności o różnych zakresach życia w wielu procesach | kontener |

### Jak się nie pomylić

Kontener należy wyłącznie do composition root. Rdzeń nie może go importować ani wołać, bo zamienia się to w ukryty service locator.

```python
# poza kanonem
container.register(RentalRepository, SqlAlchemyRentalRepository)
container.register(PaymentGateway, StripePaymentGateway)
finish = container.resolve(FinishRental)
```

Jeśli po wprowadzeniu kontenera `FinishRental` nadal da się zbudować ręcznie w teście, granica jest zachowana.

## Cykl życia sesji przy wstrzykiwaniu

Zasobem zarządza ten, kto go tworzy: composition root otwiera sesję na początku zakresu (np. żądania HTTP), wstrzykuje ją do adaptera i zamyka po zakończeniu zakresu. Rdzeń i use case nigdy nie wołają `open`, `commit` ani `close` na sesji.

### Zakres życia w FastAPI

W FastAPI naturalnym narzędziem jest zależność z `yield`. Kod przed `yield` otwiera zasób, a kod po nim (w `finally`) go zwalnia, także przy wyjątku.

```python
# app/composition.py
def get_session() -> Iterator[Session]:
    session = SessionLocal()
    try:
        yield session
    finally:
        session.close()

def get_finish_rental(session: Session = Depends(get_session)) -> FinishRental:
    ...
```

Jedno żądanie dostaje jedną sesję. `Depends` cache'uje wynik w obrębie żądania, więc wszystkie adaptery zbudowane w tym żądaniu dzielą tę samą sesję.

### Poza HTTP

Konsument wiadomości z zamków i zadania cykliczne nie mają `Depends`. Tam zakres to jedna wiadomość lub jedno zadanie, a ręczny composition root otwiera go przez `with`: `with SessionLocal() as session:` i `build_finish_rental(session)`.

### Konsekwencja

Sesja nie może trafić do obiektu o dłuższym życiu, np. singletona zbudowanego przy starcie. Singletonami mogą być tylko obiekty bezstanowe, takie jak `StripePaymentGateway` i `PricingPolicy`. Granicę transakcji (kto woła `commit`) rozstrzyga dopiero Unit of Work, o którym mowa w dalszej części tutorialu.

## Co zapamiętać

- Porty mówią, czego rdzeń potrzebuje, adaptery to spełniają, a wstrzykiwanie zależności z composition root łączy je bez importowania infrastruktury przez rdzeń.
- Composition root leży poza rdzeniem i adapterami, przy punkcie wejścia procesu, i tylko tworzy oraz łączy obiekty.
- Wstrzykiwanie przez konstruktor to wymagane parametry typowane portami, zapisane w polach, a instancje składa z zewnątrz composition root lub test.
- Depends jest dobrym klejem w adapterze HTTP i composition root, ale w rdzeniu wiąże use case z FastAPI i psuje jego użycie poza HTTP.
- Zaczynaj od ręcznego okablowania, a kontener DI dołóż dopiero przy rozrośniętym grafie i wielu zakresach życia, trzymając go wyłącznie w composition root.
- Sesję otwiera i zamyka composition root w zakresie żądania lub wiadomości, a rdzeń i długo żyjące obiekty jej nie dotykają.

## Pytania sprawdzające

### 23. Jak wstrzykiwanie zależności wiąże się z portami i adapterami?

<details>
<summary>Odpowiedź</summary>

Port deklaruje, czego rdzeń potrzebuje, adapter to dostarcza, a wstrzykiwanie zależności jest mechanizmem, który łączy je w czasie działania. Use case przyjmuje w konstruktorze abstrakcje portów, a composition root na brzegu aplikacji tworzy konkretne adaptery i podaje je z zewnątrz. Dzięki temu rdzeń nigdy nie importuje infrastruktury, a adapter można podmienić, np. na fake'a w testach, bez zmiany use case'u.

Zobacz: [sekcja „DI a porty i adaptery”](#di-a-porty-i-adaptery).

</details>

### 24. Czym jest composition root i gdzie go umieścić w aplikacji w Pythonie?

<details>
<summary>Odpowiedź</summary>

Composition root to jedno miejsce, które na brzegu aplikacji tworzy adaptery i łączy je z use case'ami. W Pythonie umieszczasz go w osobnym pakiecie, np. `app/`, obok punktów wejścia procesu, poza `core/` i `infra/`. Musi znać wszystko, więc rdzeń ani adaptery nie mogą go zawierać, a sam nie zawiera reguł biznesowych.

Zobacz: [sekcja „Composition root: gdzie go umieścić”](#composition-root-gdzie-go-umieścić).

</details>

### 25. Jak wstrzykiwać zależności przez konstruktor bez użycia frameworka DI?

<details>
<summary>Odpowiedź</summary>

Klasa przyjmuje zależności jako parametry `__init__`, typowane portami z rdzenia, i tylko zapisuje je w polach. Instancje tworzy wywołujący, czyli composition root albo test, od adapterów-liści do use case'ów, więc framework DI nie jest potrzebny. Zależności są wymagane i bez domyślnych adapterów, co utrzymuje rdzeń wolnym od infrastruktury i pozwala podstawić fake'i w testach.

Zobacz: [sekcja „Wstrzykiwanie przez konstruktor”](#wstrzykiwanie-przez-konstruktor).

</details>

### 26. Jak FastAPI Depends pomaga wiązać adaptery i jakie ryzyko niesie jego użycie w rdzeniu?

<details>
<summary>Odpowiedź</summary>

Depends to mechanizm FastAPI, który przy każdym żądaniu rozwiązuje graf funkcji dostarczających zależności. Nadaje się do okablowania adapterów, bo działa po stronie adaptera wejściowego i tuż przy composition root: funkcja providera wywołuje ręczny builder i oddaje gotowy use case. Ryzyko pojawia się, gdy Depends trafia do rdzenia: use case zależy wtedy od frameworka webowego, przestaje być zwykłą klasą i traci testowalność bez FastAPI.

Zobacz: [sekcja „FastAPI Depends w okablowaniu”](#fastapi-depends-w-okablowaniu).

</details>

### 27. Kiedy warto użyć kontenera DI zamiast ręcznego okablowania?

<details>
<summary>Odpowiedź</summary>

Kontener DI warto wprowadzić, gdy ręczne okablowanie staje się uciążliwe: graf ma dziesiątki obiektów, jest powtarzany w wielu punktach wejścia (HTTP, konsument, CLI) albo zależności mają różne zakresy życia. W małym lub średnim systemie wystarczy ręczny composition root, bo jest jawny i błędy widać od razu. Kontener musi zostać w composition root, a rdzeń nadal przyjmuje zależności przez konstruktor i nie wie o kontenerze.

Zobacz: [sekcja „Kontener DI czy ręczne okablowanie”](#kontener-di-czy-ręczne-okablowanie).

</details>

### 28. Jak zarządzać cyklem życia zasobów, takich jak sesja bazy danych, przy wstrzykiwaniu?

<details>
<summary>Odpowiedź</summary>

Zasobem zarządza ten, kto go tworzy, czyli composition root: otwiera sesję na początku zakresu (żądanie, wiadomość, zadanie), wstrzykuje ją do adapterów i zamyka na końcu, także przy błędzie. W FastAPI służy do tego zależność z `yield` i `finally`, a poza HTTP blok `with`. Rdzeń nie zna sesji ani jej zamykania, a obiekty o dłuższym życiu, jak singletony, nie mogą jej przechowywać.

Zobacz: [sekcja „Cykl życia sesji przy wstrzykiwaniu”](#cykl-życia-sesji-przy-wstrzykiwaniu).

</details>
