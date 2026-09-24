# Onion na tle innych architektur

Na rozmowie o Onion prawie zawsze pada pytanie o porównanie: z Hexagonal, z Clean, z klasycznymi warstwami. Dobrze znać różnice, ale jeszcze ważniejsze jest zrozumienie, co te podejścia łączy, a co naprawdę je dzieli.

```text
2005  Hexagonal (Cockburn)    granica: porty i adaptery
2008  Onion (Palermo)         koncentryczne warstwy z nazwanym wnętrzem
2012  Clean (Martin)          kręgi i jawna reguła zależności
────  N-tier                  warstwy ułożone w stos, zależności w dół
```

## Granica zamiast pierścieni

<a id="term-hexagonal-architecture"></a>[Architektura heksagonalna](00%20Glossary%20Onion.md#hexagonal-architecture) Alistaira Cockburna powstała trzy lata przed Onion. Dzieli świat na wnętrze aplikacji i zewnętrze, a granicę opisuje przez <a id="term-port"></a>[porty](00%20Glossary%20Onion.md#port), czyli interfejsy należące do wnętrza, oraz <a id="term-adapter"></a>[adaptery](00%20Glossary%20Onion.md#adapter), czyli implementacje na zewnątrz.

Mechanizm jest identyczny jak w cebuli: interfejs repozytorium w rdzeniu i implementacja SQL na zewnątrz to w języku hexagonal port wyjściowy i adapter. Różnica leży w tym, co każdy wzorzec opisuje dokładnie:

| | Hexagonal | Onion |
|---|---|---|
| Główna metafora | wnętrze, zewnętrze i porty na granicy | koncentryczne pierścienie |
| Wnętrze | nie narzuca podziału | Domain Model, Domain Services, Application Services |
| Granica | szczegółowo: strony driving i driven, porty wejściowe i wyjściowe | ogólnie: interfejsy w warstwach wewnętrznych |
| Zewnętrze | adaptery wejściowe i wyjściowe | UI, infrastruktura i testy w jednym pierścieniu |

Hexagonal mówi dużo o granicy i mało o środku. Onion mówi dużo o środku i mniej o granicy. Palermo sam zaznaczał, że Onion dzieli z hexagonal główne założenie: wyprowadzić infrastrukturę na zewnątrz i nie wiązać z nią rdzenia.

## Kręgi Roberta Martina

<a id="term-clean-architecture"></a>[Clean Architecture](00%20Glossary%20Onion.md#clean-architecture) Roberta C. Martina z 2012 roku rysuje cztery kręgi. Martin przedstawił ją jako syntezę hexagonal, onion i kilku podobnych podejść.

```text
Onion                        Clean
─────                        ─────
Domain Model                 Entities
Domain Services              Entities (reguły ogólne dla przedsiębiorstwa)
Application Services         Use Cases (Interactors)
UI / infrastruktura / testy  Interface Adapters + Frameworks & Drivers
```

Różnice są drobne, ale warto je znać:

- Clean dzieli zewnętrze na dwa kręgi: Interface Adapters (kontrolery, presentery, gateway'e) i Frameworks & Drivers (baza, web framework). Onion ma tu jeden pierścień.
- Clean wprowadza nazwy dla przepływu przez granicę: Input Boundary, Output Boundary, Presenter. Use case nie zwraca wyniku, tylko przekazuje go do presentera.
- Onion rozdziela Domain Model i Domain Services, a Clean łączy je w Entities.
- Clean formułuje regułę zależności jako „The Dependency Rule”, czyli tę samą zasadę, którą Palermo opisał wcześniej.

## Warstwy, ale nie stos

Klasyczna <a id="term-layered-architecture"></a>[architektura warstwowa](00%20Glossary%20Onion.md#layered-architecture) (N-tier) też ma warstwy, więc łatwo ją pomylić z cebulą. Różnica jest w kierunku zależności i w tym, co leży na dole.

```text
N-tier                              Onion

Prezentacja                         UI · Infrastruktura · Testy
    ↓                                        ↓
Logika biznesowa                    Application Services
    ↓                                        ↓
Dostęp do danych  ← fundament       Domain Services  (interfejsy repozytoriów)
    ↓                                        ↓
Baza danych                         Domain Model     ← fundament
```

| | N-tier | Onion |
|---|---|---|
| Fundament | dostęp do danych i baza | model domeny |
| Interfejs repozytorium | w warstwie danych | w rdzeniu |
| Logika zależy od bazy | tak | nie |
| Test logiki bez bazy | trudny | naturalny |
| Infrastruktura | warstwa pośrodku stosu | pierścień zewnętrzny obok UI |

Kluczowe zdanie: w N-tier infrastruktura jest pod logiką, w Onion obok UI. Ta jedna zmiana, czyli przeniesienie interfejsów do rdzenia, odwraca zależność między logiką a bazą.

## Zapis przez domenę, odczyt obok

<a id="term-cqrs"></a>[CQRS](00%20Glossary%20Onion.md#cqrs) (Command Query Responsibility Segregation) rozdziela operacje zmieniające stan od operacji odczytu. W cebuli oznacza to dwie ścieżki przez pierścienie.

Komendy, na przykład „wypożycz książkę”, przechodzą przez wszystkie warstwy, bo w Domain Model i Domain Services są reguły do pilnowania. Zapytania, na przykład „pokaż moje wypożyczenia z karami”, nie muszą. Ładowanie agregatów tylko po to, żeby zbudować tabelkę, jest kosztowne i niczego nie chroni.

Zapytanie zwraca <a id="term-read-model"></a>[model odczytu](00%20Glossary%20Onion.md#read-model): płaskie DTO przygotowane pod ekran. Interfejs odczytu leży w warstwie Application Services, a jego implementacja w pierścieniu zewnętrznym może użyć surowego SQL-a:

```python
# application/queries.py
class MemberLoansQuery(Protocol):
    def for_member(self, member_id: str) -> list[LoanSummary]: ...


# infrastructure/sql_queries.py
class SqlMemberLoansQuery:
    def for_member(self, member_id: str) -> list[LoanSummary]:
        rows = self._conn.execute(text("""
            SELECT l.id, b.title, l.borrowed_on + 30 AS due_date,
                   GREATEST(CURRENT_DATE - (l.borrowed_on + 30), 0) * 0.50 AS fine
            FROM loans l JOIN books b ON b.id = l.book_id
            WHERE l.member_id = :m AND l.returned_on IS NULL
        """), {"m": member_id})
        return [LoanSummary(*row) for row in rows]
```

```text
komenda:   API ──► Application Services ──► Domain Services ──► Domain Model ──► repozytorium
zapytanie: API ──► interfejs zapytania ──────────────────────────────────────► SQL / widok
```

Reguła zależności nadal obowiązuje: API zna interfejs z rdzenia, a nie SQL. Pomijane są tylko warstwy domenowe. Uwaga na koszt: w zapytaniu powtórzyły się reguły „30 dni” i „0,50 zł za dzień”. To świadomy kompromis na rzecz wydajności, który powinien być opisany testem porównującym wynik zapytania z `FineCalculator`.

## Co zapamiętać

- Onion, Hexagonal i Clean opierają się na tej samej regule: zależności do środka, interfejsy w rdzeniu.
- Hexagonal szczegółowo opisuje granicę (porty, adaptery), Onion szczegółowo opisuje wnętrze.
- Clean dzieli zewnętrze na dwa kręgi i nazywa elementy przepływu: boundary, interactor, presenter.
- N-tier stawia bazę na dole stosu, Onion stawia na dole model domeny.
- Przeniesienie interfejsów repozytoriów do rdzenia odwraca zależność logiki od bazy.
- W CQRS komendy przechodzą przez domenę, zapytania mogą ją pominąć przez interfejs odczytu.

## Pytania sprawdzające

### 22. Czym Onion różni się od Hexagonal Architecture? Co je łączy?

<details>
<summary>Odpowiedź</summary>

Łączy je mechanizm: rdzeń niezależny od technologii, interfejsy w rdzeniu, implementacje na zewnątrz, zależności do środka. Interfejs repozytorium w Onion to port wyjściowy w hexagonal, a implementacja SQL to adapter. Różnią się akcentem. Hexagonal szczegółowo opisuje granicę (strony driving i driven, porty wejściowe i wyjściowe) i nie dzieli wnętrza. Onion dzieli wnętrze na Domain Model, Domain Services i Application Services, a całe zewnętrze traktuje jako jeden pierścień.

Zobacz: sekcja „Granica zamiast pierścieni”.

</details>

### 23. Czym Onion różni się od Clean Architecture? Jak odpowiadają sobie ich warstwy?

<details>
<summary>Odpowiedź</summary>

Domain Model i Domain Services odpowiadają Entities, Application Services odpowiadają Use Cases (Interactors), a pierścień zewnętrzny odpowiada dwóm kręgom: Interface Adapters i Frameworks & Drivers. Clean dodatkowo nazywa elementy przepływu przez granicę (Input i Output Boundary, Presenter), a jej use case przekazuje wynik do presentera zamiast go zwracać. Reguła zależności jest ta sama. Clean jest późniejszą syntezą Onion i hexagonal.

Zobacz: sekcja „Kręgi Roberta Martina”.

</details>

### 24. Czym Onion różni się od klasycznego N-tier, skoro oba mają warstwy?

<details>
<summary>Odpowiedź</summary>

Kierunkiem zależności i tym, co jest fundamentem. W N-tier zależności płyną w dół do warstwy danych, interfejsy repozytoriów leżą w warstwie danych, a logika zależy od bazy. W Onion fundamentem jest model domeny, interfejsy repozytoriów leżą w rdzeniu, a infrastruktura jest w pierścieniu zewnętrznym obok UI. Dzięki temu logikę da się testować bez bazy.

Zobacz: sekcja „Warstwy, ale nie stos”.

</details>

### 25. Jak Onion łączy się z CQRS? Czy strona odczytu musi przechodzić przez wszystkie warstwy?

<details>
<summary>Odpowiedź</summary>

Nie musi. Komendy przechodzą przez wszystkie warstwy, bo w domenie są reguły do pilnowania. Zapytania korzystają z interfejsu odczytu zdefiniowanego w rdzeniu (np. `MemberLoansQuery`), którego implementacja w infrastrukturze zwraca płaski model odczytu, np. z surowego SQL-a. Reguła zależności obowiązuje dalej, pomijane są tylko warstwy domenowe. Kosztem może być powtórzenie reguł w zapytaniu, które warto pokryć testem.

Zobacz: sekcja „Zapis przez domenę, odczyt obok”.

</details>
