# Pułapki i decyzje

Cebulę łatwo narysować i równie łatwo zbudować tylko z nazwy. Projekty `Domain`, `Application` i `Infrastructure` istnieją, a mimo to reguły leżą w złych miejscach, model domeny nie ma zachowań, a każda zmiana przechodzi przez pięć plików. Ten rozdział opisuje najczęstsze problemy i decyzje, które trzeba podjąć świadomie.

## Pusty środek cebuli

<a id="term-anemic-domain-model"></a>[Anemiczny model domeny](00%20Glossary%20Onion.md#anemic-domain-model) to Domain Model złożony z klas z samymi polami, w którym cała logika siedzi w Application Services. Pierścienie istnieją, ale środek niczego nie chroni.

```python
# anemiczny: Book to worek na dane
@dataclass
class Book:
    id: str
    title: str
    available: bool


class BorrowBookService:
    def borrow(self, member_id: str, book_id: str) -> str:
        book = self._books.get(book_id)
        if not book.available:                         # reguła w serwisie aplikacyjnym
            raise LoanError("...")
        if len(self._loans.active_for(member_id)) >= 3: # reguła w serwisie aplikacyjnym
            raise LoanError("...")
        book.available = False                         # każdy może to ustawić
        ...
```

Dlaczego to częste akurat w Onion? Są trzy przyczyny:

- nazwa „Application Services” zachęca, żeby wszystko, co „robi coś w aplikacji”, trafiało tam,
- zespoły przenoszą nawyk z N-tier, gdzie encja była odbiciem tabeli, a logika mieszkała w serwisie,
- Domain Model generuje się z bazy albo pisze pod ORM, więc od początku jest strukturą danych.

Naprawa polega na przenoszeniu reguł do obiektów, których dotyczą: `Book.lend()` zamiast `book.available = False`, `LoanPolicy.can_borrow()` zamiast `len(...) >= 3` w serwisie. Sygnał, że się udało: Application Service czyta się jak lista kroków, bez `if`-ów biznesowych.

## ORM w środku cebuli

Najczęstszy przeciek technologii do rdzenia to klasy domeny, które są jednocześnie encjami ORM:

```python
# źle: Domain Model zna SQLAlchemy
class Book(Base):
    __tablename__ = "books"
    id: Mapped[str] = mapped_column(primary_key=True)
    title: Mapped[str]
    available: Mapped[bool] = mapped_column(default=True)
```

Skutki są realne. Lazy loading odpala zapytania z wnętrza metod domeny. ORM wymusza pusty konstruktor albo mutowalne pola. Zmiana nazwy kolumny zmienia domenę. Testy domeny potrzebują zainstalowanego SQLAlchemy.

Są dwa wyjścia. Pierwsze to mapowanie imperatywne: klasa domeny zostaje czystym `dataclass`, a mapowanie na tabelę jest zdefiniowane w infrastrukturze.

```python
# infrastructure/orm.py
from sqlalchemy.orm import registry

mapper_registry = registry()
mapper_registry.map_imperatively(Book, books_table)
```

Drugie to osobny <a id="term-persistence-model"></a>[model persystencji](00%20Glossary%20Onion.md#persistence-model): klasa `BookRow` odwzorowuje tabelę, a repozytorium tłumaczy ją na `Book` i z powrotem.

| | Mapowanie imperatywne | Osobny model persystencji |
|---|---|---|
| Ilość kodu | mała | mapper dla każdego agregatu |
| Czystość domeny | dobra, ale ORM nadal wpływa na zachowanie (lazy loading, tożsamość sesji) | pełna |
| Zmiana schematu | czasem dotyka domeny | tylko infrastruktura |
| Kiedy | proste klasy, schemat zbliżony do modelu | bogata domena, schemat inny niż model |

W .NET odpowiednikiem mapowania imperatywnego jest konfiguracja Entity Framework przez `IEntityTypeConfiguration` w projekcie Infrastructure zamiast atrybutów na klasach domeny.

## Warstwy, które niczego nie robią

<a id="term-pass-through-layer"></a>[Warstwa przelotowa](00%20Glossary%20Onion.md#pass-through-layer) to warstwa, która tylko przekazuje wywołanie dalej. Typowy przykład to Application Service, który woła jedną metodę repozytorium, i Domain Service, który woła jedną metodę encji:

```python
class BookService:                       # Application Services
    def get(self, book_id):
        return self._domain_service.get(book_id)


class BookDomainService:                 # Domain Services
    def get(self, book_id):
        return self._repo.get(book_id)
```

Towarzyszy jej <a id="term-interface-explosion"></a>[eksplozja interfejsów](00%20Glossary%20Onion.md#interface-explosion): `IBookService`, `IBookDomainService`, `IBookRepository` i trzy DTO dla jednego odczytu. Dodanie pola wymaga zmiany w ośmiu plikach.

Kilka zasad ogranicza ceremonię:

- Domain Services twórz tylko wtedy, gdy jest reguła obejmująca wiele obiektów. Warstwa może być pusta.
- Interfejs twórz dla rzeczy zewnętrznych i zmiennych, takich jak baza, zegar i zewnętrzne API, a nie dla każdego serwisu.
- Proste odczyty prowadź ścieżką zapytań z rozdziału 06, bez przechodzenia przez domenę.
- Proste moduły mogą mieć mniej pierścieni. Część CRUD-owa systemu nie musi być cebulą.

Pytanie kontrolne dla każdej warstwy i abstrakcji: jaką decyzję tu podejmujemy? Jeśli żadną, warstwa jest zbędna.

## Puchnące serwisy aplikacyjne

<a id="term-fat-application-service"></a>[Gruby serwis aplikacyjny](00%20Glossary%20Onion.md#fat-application-service) to Application Service, który rośnie do setek linii, bo każda nowa reguła trafia do niego jako kolejny `if`. Objawy są charakterystyczne:

- metody serwisu mają więcej `if`-ów niż wywołań repozytoriów,
- ta sama reguła jest skopiowana w dwóch serwisach, na przykład `BorrowBookService` i `ExtendLoanService`,
- test serwisu wymaga dziesięciu fake'ów, bo serwis robi wszystko,
- nazwa serwisu to rzeczownik (`LoanService`), a nie scenariusz.

Naprawa idzie w trzech kierunkach:

1. Reguły dotyczące jednego obiektu przenieś do Domain Model (`Loan.extend()` pilnuje limitu przedłużeń).
2. Reguły dotyczące wielu obiektów przenieś do Domain Services (`LoanPolicy`).
3. Podziel serwis per scenariusz: `BorrowBook`, `ReturnBook`, `ExtendLoan` zamiast jednego `LoanService` z dwudziestoma metodami.

```python
# po refaktoryzacji: serwis to lista kroków
class ExtendLoan:
    def __call__(self, loan_id: str) -> None:
        with self._uow as uow:
            loan = uow.loans.get(loan_id)
            loan.extend(self._clock.today())       # reguła w domenie
            uow.commit()
```

## Migracja z N-tier

Przepisywanie systemu od zera rzadko się udaje. Bezpieczniej przejść na Onion stopniowo, wzorcem <a id="term-strangler-fig"></a>[strangler fig](00%20Glossary%20Onion.md#strangler-fig): nowa struktura otacza stary kod i przejmuje jego funkcje, aż stary kod można usunąć.

Przed pierwszą zmianą warto zamrozić obecne zachowanie <a id="term-characterization-test"></a>[testami charakteryzującymi](00%20Glossary%20Onion.md#characterization-test). Takie testy opisują to, co system robi dziś, łącznie z dziwactwami, a nie to, co powinien robić.

```text
krok 1  testy charakteryzujące    zamroź zachowanie przez API
krok 2  projekt Domain            pusty, bez referencji, wymuszony kompilatorem lub import-linterem
krok 3  interfejsy repozytoriów   przenieś je z warstwy danych do rdzenia
krok 4  odwróć zależność          stara warstwa danych implementuje nowe interfejsy
krok 5  jeden scenariusz          przenieś reguły z serwisu do Domain Model i Domain Services
krok 6  powtarzaj                 scenariusz po scenariuszu, najpierw te najczęściej zmieniane
```

Krok 4 jest najważniejszy. Odwrócenie zależności nie wymaga przepisywania logiki. Wystarczy, że istniejąca klasa dostępu do danych zacznie implementować interfejs z rdzenia, a serwis zacznie zależeć od interfejsu zamiast od klasy.

Gdy nowy rdzeń musi korzystać ze starego modelu danych o innych pojęciach, stosuje się <a id="term-anti-corruption-layer"></a>[anti-corruption layer](00%20Glossary%20Onion.md#anti-corruption-layer): implementację w pierścieniu zewnętrznym, która tłumaczy stare pojęcia na język nowej domeny. W przykładzie `Member` ma dodatkowo pole `blocked`:

```python
class LegacyMemberRepository:                  # implementuje MemberRepository
    def get(self, member_id: str) -> Member:
        row = self._db.fetch_one("SELECT * FROM CZYTELNICY WHERE NR_KARTY = %s", member_id)
        return Member(
            id=row["NR_KARTY"],
            name=f'{row["IMIE"]} {row["NAZWISKO"]}',
            blocked=row["STATUS"] in ("Z", "B"),
        )
```

Nowa domena zna `blocked`, a nie `STATUS in ("Z", "B")`.

## Co zapamiętać

- Anemiczny Domain Model to pierścienie bez treści. Reguły powinny mieszkać w obiektach, których dotyczą.
- ORM w środku cebuli usuwa się mapowaniem imperatywnym albo osobnym modelem persystencji.
- Warstwa, która niczego nie decyduje, jest zbędna. Proste moduły mogą mieć mniej pierścieni.
- Gruby serwis aplikacyjny dzieli się według scenariuszy, a jego reguły przenosi do domeny.
- Migracja z N-tier zaczyna się od testów charakteryzujących i przeniesienia interfejsów repozytoriów do rdzenia.
- Anti-corruption layer tłumaczy stary model danych na język nowej domeny.

## Pytania sprawdzające

### 26. Dlaczego w źle wdrożonej Onion często powstaje anemiczny model domeny?

<details>
<summary>Odpowiedź</summary>

Bo nazwa „Application Services” zachęca, żeby tam trafiało wszystko, bo zespoły przenoszą nawyk z N-tier (encja jako odbicie tabeli, logika w serwisie) i bo model domeny bywa generowany z bazy albo pisany pod ORM. Skutek: pierścienie istnieją, ale środek nie chroni reguł i każdy może ustawić dowolny stan. Naprawa to przeniesienie reguł do obiektów domeny (`Book.lend()`) i serwisów domenowych (`LoanPolicy`), aż Application Service stanie się listą kroków.

Zobacz: sekcja „Pusty środek cebuli”.

</details>

### 27. Co zrobić, gdy encje ORM „przeciekają” do Domain Model (adnotacje, lazy loading)?

<details>
<summary>Odpowiedź</summary>

Oddzielić mapowanie od klas domeny. Pierwsza opcja to mapowanie imperatywne (SQLAlchemy `map_imperatively`, w EF Core `IEntityTypeConfiguration` w Infrastructure), dzięki któremu klasy domeny zostają czyste, choć ORM nadal wpływa na zachowanie. Druga opcja to osobny model persystencji (`BookRow`) i mapper w repozytorium, co daje pełną izolację kosztem większej ilości kodu. Pierwsza pasuje do prostych klas, druga do bogatej domeny i schematu różnego od modelu.

Zobacz: sekcja „ORM w środku cebuli”.

</details>

### 28. Jak uniknąć nadmiaru warstw i interfejsów, gdy logika jest prosta?

<details>
<summary>Odpowiedź</summary>

Nie tworzyć warstw przelotowych, które tylko przekazują wywołanie. Domain Services pojawiają się tylko przy regułach obejmujących wiele obiektów. Interfejsy powstają dla rzeczy zewnętrznych i zmiennych, a nie dla każdego serwisu. Proste odczyty idą ścieżką zapytań, a moduły CRUD mogą mieć mniej pierścieni. Pytanie kontrolne: jaką decyzję podejmuje ta warstwa? Jeśli żadną, jest zbędna.

Zobacz: sekcja „Warstwy, które niczego nie robią”.

</details>

### 29. Co zrobić, gdy Application Services puchną i zaczynają zawierać logikę biznesową?

<details>
<summary>Odpowiedź</summary>

Rozpoznać objawy: więcej `if`-ów niż wywołań repozytoriów, skopiowane reguły, wiele fake'ów w teście, nazwa-rzeczownik typu `LoanService`. Naprawić w trzech krokach: reguły jednego obiektu przenieść do Domain Model (`Loan.extend()`), reguły wielu obiektów do Domain Services (`LoanPolicy`), a serwis podzielić per scenariusz (`BorrowBook`, `ReturnBook`, `ExtendLoan`).

Zobacz: sekcja „Puchnące serwisy aplikacyjne”.

</details>

### 30. Jak stopniowo przejść z architektury N-tier na Onion w istniejącym projekcie?

<details>
<summary>Odpowiedź</summary>

Stopniowo, wzorcem strangler fig. Najpierw testy charakteryzujące zamrażają obecne zachowanie. Potem powstaje pusty projekt Domain z wymuszoną izolacją, a interfejsy repozytoriów przenosi się z warstwy danych do rdzenia. Istniejąca warstwa danych zaczyna je implementować, co odwraca zależność bez przepisywania logiki. Dalej reguły z serwisów przenosi się do domeny scenariusz po scenariuszu. Kontakt ze starym modelem danych odbywa się przez anti-corruption layer, który tłumaczy stare pojęcia na nowe.

Zobacz: sekcja „Migracja z N-tier”.

</details>
