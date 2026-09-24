# Czym jest Onion

<a id="term-onion-architecture"></a>[Architektura cebulowa](00%20Glossary%20Onion.md#onion-architecture) (Onion Architecture) to sposób organizowania aplikacji w koncentryczne warstwy, w których logika biznesowa jest w środku, a technologia na zewnątrz. Opisał ją Jeffrey Palermo w serii artykułów z 2008 roku. Wzorzec powstał w świecie .NET, ale działa w każdym języku, także w Pythonie.

Najprostszy model działania wygląda tak:

```text
┌──────────────────────────────────────────────┐
│  UI · infrastruktura · testy                 │
│  ┌────────────────────────────────────────┐  │
│  │  Application Services                  │  │
│  │  ┌──────────────────────────────────┐  │  │
│  │  │  Domain Services                 │  │  │
│  │  │  ┌────────────────────────────┐  │  │  │
│  │  │  │  Domain Model              │  │  │  │
│  │  │  └────────────────────────────┘  │  │  │
│  │  └──────────────────────────────────┘  │  │
│  └────────────────────────────────────────┘  │
└──────────────────────────────────────────────┘
        zależności wskazują zawsze do środka
```

## Środek cebuli

Centrum aplikacji to <a id="term-domain-model"></a>[model domeny](00%20Glossary%20Onion.md#domain-model): obiekty opisujące pojęcia i reguły biznesowe. W przykładzie przewodnim tego tutorialu jest to wypożyczalnia książek: `Book`, `Member`, `Loan`, reguła „członek może mieć najwyżej trzy wypożyczenia”.

Warstwy wewnętrzne razem tworzą <a id="term-application-core"></a>[rdzeń aplikacji](00%20Glossary%20Onion.md#application-core). Rdzeń nie wie, czy dane leżą w PostgreSQL, czy przychodzą przez HTTP, czy przez kolejkę. Wszystko, co wie o technologii, leży w najbardziej zewnętrznym pierścieniu, czyli w <a id="term-infrastructure"></a>[infrastrukturze](00%20Glossary%20Onion.md#infrastructure).

```python
# środek cebuli: czysty Python, zero importów technicznych
from dataclasses import dataclass, field


@dataclass
class Member:
    id: str
    name: str
    active_loans: list[str] = field(default_factory=list)

    def can_borrow(self) -> bool:
        return len(self.active_loans) < 3
```

## Problem, który rozwiązuje

Palermo zaczyna od krytyki klasycznej <a id="term-layered-architecture"></a>[architektury warstwowej](00%20Glossary%20Onion.md#layered-architecture), w której UI zależy od logiki, a logika od dostępu do danych. W takim układzie baza danych jest fundamentem, na którym stoi cała aplikacja.

```text
Warstwowo (N-tier):            Onion:

UI                             UI    infrastruktura
 ↓                              ↘    ↙
logika biznesowa               Application Services
 ↓                                   ↓
dostęp do danych                Domain Services
 ↓                                   ↓
baza danych                     Domain Model
```

Po lewej logika biznesowa importuje warstwę danych, więc zmiana ORM-a, test bez bazy albo przeniesienie reguł do innego procesu wymaga dotykania kodu biznesowego. Po prawej to infrastruktura zależy od rdzenia. Baza danych przestaje być fundamentem i staje się szczegółem na obrzeżu.

## Kierunek zależności

Najważniejsza zasada ma nazwę <a id="term-dependency-rule"></a>[reguła zależności](00%20Glossary%20Onion.md#dependency-rule): kod może zależeć tylko od warstw położonych bliżej środka. Warstwa wewnętrzna nigdy nie importuje warstwy zewnętrznej.

Palermo sformułował cztery zasady:

1. Aplikacja jest zbudowana wokół niezależnego modelu obiektowego.
2. Warstwy wewnętrzne definiują interfejsy, warstwy zewnętrzne je implementują.
3. Zależności wskazują do środka.
4. Cały rdzeń aplikacji da się skompilować i uruchomić bez infrastruktury.

Czwarta zasada jest najlepszym testem praktycznym. Jeśli rdzeń da się zaimportować i przetestować w czystym interpreterze, bez bazy i frameworka, cebula jest zbudowana poprawnie.

```python
# domain/member.py: dobrze
from dataclasses import dataclass

# domain/member.py: źle, środek zna bazę
from sqlalchemy.orm import Mapped
```

## Korzyści i koszty

Onion daje korzyści:

- reguły biznesowe da się testować bez bazy, sieci i frameworka,
- infrastrukturę można wymienić bez zmiany modelu domeny,
- warstwy mają nazwane odpowiedzialności, więc łatwo zdecydować, gdzie umieścić nowy kod,
- model domeny jest chroniony przed szczegółami technicznymi.

Ma też koszty:

- więcej warstw, projektów i interfejsów niż w prostym układzie,
- mapowanie danych między modelem domeny a bazą i UI,
- ryzyko mnożenia warstw, które niczego nie robią poza przekazywaniem wywołań dalej.

## Kiedy nie warto

Onion opłaca się, gdy model domeny jest bogaty i będzie żył długo. Nie opłaca się w prostym CRUD-zie, gdzie cała logika to zapis formularza w tabeli, w krótkim prototypie ani w skrypcie. Jeśli warstwa Domain Model zawierałaby same pola bez zachowań, cztery pierścienie są ceremonią bez treści.

Dobre pytanie kontrolne: co zostanie w środku cebuli, gdy usunę bazę i framework? Jeśli prawie nic, lepiej wybrać prostszy układ.

## Co zapamiętać

- Onion Architecture opisał Jeffrey Palermo w 2008 roku.
- W środku jest model domeny, na zewnątrz UI, infrastruktura i testy.
- Baza danych nie jest fundamentem, tylko szczegółem na obrzeżu.
- Kod może zależeć wyłącznie od warstw bliższych środka.
- Warstwy wewnętrzne definiują interfejsy, zewnętrzne je implementują.
- Rdzeń musi dać się uruchomić bez infrastruktury.
- Prosty CRUD i prototyp zwykle nie potrzebują cebuli.

## Pytania sprawdzające

### 1. Czym jest architektura cebulowa (Onion Architecture) i kto ją zaproponował?

<details>
<summary>Odpowiedź</summary>

To architektura, w której aplikacja jest zbudowana z koncentrycznych warstw: w środku model domeny, wokół niego serwisy domenowe i aplikacyjne, a na zewnątrz UI, infrastruktura i testy. Zależności wskazują zawsze do środka. Zaproponował ją Jeffrey Palermo w 2008 roku.

Zobacz: początek rozdziału i sekcja „Środek cebuli”.

</details>

### 2. Jaki problem klasycznej architektury warstwowej rozwiązuje Onion?

<details>
<summary>Odpowiedź</summary>

W architekturze warstwowej (N-tier) zależności płyną w dół: UI → logika → dostęp do danych, więc logika biznesowa zależy od bazy i ORM-a. Baza jest fundamentem aplikacji, a zmiana technologii albo test bez bazy wymaga dotykania logiki. Onion odwraca ten układ: model domeny jest w środku, a infrastruktura zależy od rdzenia.

Zobacz: sekcja „Problem, który rozwiązuje”.

</details>

### 3. Co symbolizuje metafora cebuli? Co jest w środku, a co na zewnątrz?

<details>
<summary>Odpowiedź</summary>

Cebula to warstwy nałożone jedna na drugą wokół wspólnego środka. W środku jest model domeny, dalej Domain Services i Application Services, a w zewnętrznym pierścieniu UI, infrastruktura i testy. Im bliżej środka, tym stabilniejszy i bardziej biznesowy kod. Im dalej, tym więcej technologii i szczegółów, które można wymienić.

Zobacz: diagram na początku rozdziału i sekcja „Środek cebuli”.

</details>

### 4. Jaka jest główna zasada kierunku zależności w Onion?

<details>
<summary>Odpowiedź</summary>

Kod może zależeć tylko od warstw położonych bliżej środka. Warstwa wewnętrzna nigdy nie importuje zewnętrznej. Wynikają z tego pozostałe zasady Palermo: warstwy wewnętrzne definiują interfejsy, zewnętrzne je implementują, a rdzeń da się skompilować i uruchomić bez infrastruktury.

Zobacz: sekcja „Kierunek zależności”.

</details>

### 5. Kiedy Onion Architecture jest przerostem formy nad treścią?

<details>
<summary>Odpowiedź</summary>

Gdy model domeny jest ubogi: w prostym CRUD-zie, krótkim prototypie albo skrypcie. Jeśli warstwa Domain Model zawierałaby same pola bez zachowań, cztery warstwy są ceremonią. Pytanie kontrolne: co zostanie w środku po usunięciu bazy i frameworka?

Zobacz: sekcja „Kiedy nie warto”.

</details>
