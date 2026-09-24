# Strona odczytu

Strona odczytu nie pilnuje reguł i nie zmienia stanu. Jej jedynym zadaniem jest szybko i tanio dostarczyć dane w dokładnie takim kształcie, jakiego potrzebuje ekran albo klient API. Zwalnia to z wielu ograniczeń, ale wymaga innego sposobu projektowania niż strona zapisu.

```text
ekran „Moja kolejka” (agent)        ──► agent_queue           (tabela zdenormalizowana)
ekran „Moje zgłoszenia” (klient)    ──► customer_tickets      (tabela zdenormalizowana)
panel SLA (kierownik)               ──► sla_daily_stats       (agregaty per dzień i priorytet)
wyszukiwarka zgłoszeń               ──► indeks Elasticsearch  (pełny tekst)
```

## Model pod pytanie, nie pod domenę

Każde <a id="term-query"></a>[zapytanie](00%20Glossary%20CQRS.md#query) po stronie odczytu zwraca dane dla konkretnego odbiorcy. Model odczytu projektuje się od końca: zaczyna się od ekranu albo odpowiedzi API, a dopiero potem ustala się, jak przechowywać dane.

Ekran „Moja kolejka” agenta pokazuje tytuł zgłoszenia, nazwę klienta, priorytet, czas do przekroczenia SLA i liczbę wiadomości. Model odczytu zawiera dokładnie te pola:

```sql
CREATE TABLE agent_queue (
    ticket_id        uuid PRIMARY KEY,
    agent_id         uuid NOT NULL,
    title            text NOT NULL,
    customer_name    text NOT NULL,
    priority         text NOT NULL,
    priority_rank    smallint NOT NULL,       -- do sortowania bez CASE
    sla_deadline     timestamptz NOT NULL,
    message_count    int NOT NULL DEFAULT 0,
    last_activity_at timestamptz NOT NULL
);
CREATE INDEX agent_queue_by_agent ON agent_queue (agent_id, priority_rank, sla_deadline);
```

Nazwa klienta jest skopiowana, choć „w domenie” należy do klienta. Priorytet jest zapisany dwa razy, jako tekst i jako liczba do sortowania. Takie powielanie to <a id="term-denormalization"></a>[denormalizacja](00%20Glossary%20CQRS.md#denormalization). Po stronie zapisu byłaby błędem, bo utrudnia pilnowanie spójności. Po stronie odczytu jest celem, bo zamienia zapytanie z pięcioma JOIN-ami na odczyt jednej tabeli po indeksie.

<a id="term-query-handler"></a>[Handler zapytania](00%20Glossary%20CQRS.md#query-handler) jest wtedy trywialny:

```python
@dataclass(frozen=True)
class QueueItem:
    ticket_id: str
    title: str
    customer_name: str
    priority: str
    sla_deadline: datetime
    message_count: int


class AgentQueueQuery:
    def __call__(self, agent_id: str, limit: int = 50) -> list[QueueItem]:
        rows = self._db.execute(text("""
            SELECT ticket_id, title, customer_name, priority, sla_deadline, message_count
            FROM agent_queue WHERE agent_id = :a
            ORDER BY priority_rank, sla_deadline LIMIT :n
        """), {"a": agent_id, "n": limit})
        return [QueueItem(*r) for r in rows]
```

Handler zapytania nie ładuje agregatów, nie używa repozytorium z regułami i nie ma walidacji biznesowej. Sprawdza tylko uprawnienia, czyli czy wywołujący może zobaczyć te dane.

## Ile modeli odczytu

Nie ma reguły „jeden model na ekran” ani „jeden model na agregat”. Decyzję podejmuje się na podstawie trzech pytań:

- Czy ekrany potrzebują tych samych pól i tego samego sortowania? Jeśli tak, mogą dzielić model.
- Czy mają różnych odbiorców z różnymi uprawnieniami? Klient nie powinien widzieć notatek wewnętrznych, więc `customer_tickets` to osobny model, nawet jeśli pola się pokrywają.
- Czy mają różne wymagania wydajnościowe lub technologiczne? Wyszukiwanie pełnotekstowe potrzebuje innego magazynu niż lista po indeksie.

| Model | Odbiorcy | Wspólny z | Dlaczego osobny |
|---|---|---|---|
| `agent_queue` | agenci | lista „Nieprzypisane” (filtr `agent_id IS NULL`) | inne sortowanie niż u klienta |
| `customer_tickets` | klienci | brak | inne uprawnienia, brak notatek wewnętrznych |
| `sla_daily_stats` | kierownicy | brak | agregaty zamiast wierszy |
| `tickets_search` | wszyscy | brak | wyszukiwanie pełnotekstowe |

Każdy model trzeba utrzymywać, więc warto zaczynać od kilku modeli i dzielić je, gdy pojawi się konkretny powód. Model odczytu jest tani do zmiany: można go usunąć i odbudować, bo źródłem prawdy jest strona zapisu.

## Wybór magazynu

Model odczytu może żyć w tej samej bazie co strona zapisu albo w zupełnie innej. Najprostszą formą odczytu z własnym kształtem jest <a id="term-materialized-view"></a>[widok zmaterializowany](00%20Glossary%20CQRS.md#materialized-view): wynik zapytania zapisany fizycznie i odświeżany na żądanie. Wybór magazynu zależy od rodzaju zapytań:

| Magazyn | Dobry do | Uwagi |
|---|---|---|
| Widok SQL | prosty start, dane zawsze aktualne | liczony przy każdym odczycie, nie rozwiązuje problemu wydajności |
| Widok zmaterializowany | raporty odświeżane okresowo | w PostgreSQL `REFRESH MATERIALIZED VIEW`, dane nieaktualne między odświeżeniami |
| Tabela zdenormalizowana | listy, kolejki, szczegóły | aktualizowana przez projekcję, najbardziej elastyczna |
| Elasticsearch, OpenSearch | wyszukiwanie pełnotekstowe, filtry fasetowe | osobny system, zawsze asynchroniczny |
| Redis | liczniki, rankingi, dane „na żywo” | ograniczona trwałość i zapytania |
| Baza dokumentowa | szczegóły obiektu jako jeden dokument | jeden odczyt zamiast wielu JOIN-ów |
| Hurtownia (BigQuery, ClickHouse) | analityka, raporty historyczne | duże opóźnienie, tanie zapytania analityczne |

Tabela zdenormalizowana w tej samej bazie PostgreSQL to rozsądny domyślny wybór. Umożliwia aktualizację w tej samej transakcji co zapis i nie wprowadza nowej technologii. Osobny magazyn warto dodać dopiero wtedy, gdy baza relacyjna nie radzi sobie z danym rodzajem zapytań.

## Czytanie tabel zapisu

Najprostszy wariant CQRS, opisany w rozdziale 01, czyta bezpośrednio z tabel strony zapisu. To uprawniony skrót, ale ma konsekwencje:

- zmiana schematu tabel zapisu psuje zapytania odczytu, więc obie strony nie są od siebie niezależne,
- zapytania odczytu konkurują o te same zasoby co zapis, więc ciężki raport spowalnia komendy,
- zapytania z wieloma JOIN-ami wracają, a z nimi problemy wydajności,
- uprawnienia trzeba sprawdzać przy każdym zapytaniu, bo tabela zawiera wszystkie dane.

Skrót jest dobry na początek i dla prostych ekranów. Gdy zmiany schematu zapisu zaczynają wymagać poprawiania kilkunastu zapytań, albo raporty spowalniają zapis, czas przejść na własne modele odczytu. Pośrednim krokiem są widoki SQL, które odcinają zapytania od fizycznego schematu tabel.

Odwrotny kierunek jest zakazany: strona zapisu nie powinna podejmować decyzji na podstawie modeli odczytu, jeśli reguła musi być pewna. Rozdział 02 opisuje to przy walidacji.

## Dane z wielu źródeł

Ekran szczegółów zgłoszenia pokazuje dane zgłoszenia, profil klienta z CRM i stan zamówienia części z magazynu. Każde z tych źródeł to osobny <a id="term-bounded-context"></a>[bounded context](00%20Glossary%20CQRS.md#bounded-context), czyli część systemu z własnym modelem i często własnym zespołem.

Są dwa sposoby złożenia takich danych.

<a id="term-api-composition"></a>[Kompozycja API](00%20Glossary%20CQRS.md#api-composition) polega na tym, że handler zapytania albo warstwa BFF woła kilka źródeł i skleja wynik w czasie odczytu:

```python
class TicketDetailsQuery:
    async def __call__(self, ticket_id: str) -> TicketDetails:
        ticket = await self._tickets.details(ticket_id)
        customer, parts = await asyncio.gather(
            self._crm.customer_summary(ticket.customer_id),
            self._warehouse.parts_for_ticket(ticket_id),
        )
        return TicketDetails(ticket, customer, parts)
```

Drugi sposób to model odczytu, który subskrybuje zdarzenia z kilku kontekstów (`TicketOpened`, `CustomerRenamed`, `PartShipped`) i utrzymuje gotową, połączoną kopię.

| | Kompozycja API | Model zasilany zdarzeniami |
|---|---|---|
| Aktualność | zawsze bieżące dane | spójność ostateczna |
| Wydajność | suma opóźnień źródeł, wiele wywołań | jeden odczyt |
| Dostępność | awaria jednego źródła psuje ekran | działa, gdy źródła leżą |
| Koszt | prosty kod | projekcja, subskrypcje, odbudowa |
| Sprzężenie | zna API wszystkich źródeł | zna zdarzenia wszystkich źródeł |

Kompozycja API wystarcza dla ekranów szczegółów pojedynczego obiektu. Model zasilany zdarzeniami jest potrzebny, gdy trzeba filtrować lub sortować po danych z wielu kontekstów naraz, na przykład „zgłoszenia klientów VIP, czekające na części”.

## Co zapamiętać

- Model odczytu projektuje się od ekranu lub odpowiedzi API, a nie od struktury domeny.
- Denormalizacja jest po stronie odczytu celem, bo zamienia wiele JOIN-ów na odczyt jednej tabeli.
- Handler zapytania nie ładuje agregatów i sprawdza tylko uprawnienia.
- Liczba modeli zależy od pól, sortowania, uprawnień i wymagań technicznych. Warto zaczynać od kilku.
- Domyślny magazyn to tabela zdenormalizowana w tej samej bazie, a inne dodaje się z konkretnego powodu.
- Czytanie tabel zapisu to uprawniony skrót, który z czasem wiąże obie strony.
- Dane z wielu kontekstów łączy się kompozycją API albo modelem zasilanym zdarzeniami.

## Pytania sprawdzające

### 12. Czym jest read model i dlaczego projektuje się go pod ekran lub zapytanie, a nie pod strukturę domeny?

<details>
<summary>Odpowiedź</summary>

To struktura danych przygotowana dla konkretnego odbiorcy: ekranu, raportu albo endpointu API. Nie pilnuje reguł, więc może mieć dowolny kształt: skopiowane pola, pola pomocnicze do sortowania, dane z kilku agregatów. Projektuje się go od ekranu, bo celem jest odczyt jednej tabeli po indeksie zamiast wielu JOIN-ów. Denormalizacja jest tu zaletą, a nie błędem.

Zobacz: sekcja „Model pod pytanie, nie pod domenę”.

</details>

### 13. Jak zdecydować, ile read modeli potrzeba? Kiedy jeden model obsługuje kilka ekranów, a kiedy trzeba je rozdzielić?

<details>
<summary>Odpowiedź</summary>

Jeden model może obsługiwać kilka ekranów, jeśli potrzebują tych samych pól i sortowania. Rozdziela się je, gdy mają różnych odbiorców z różnymi uprawnieniami (klient nie widzi notatek wewnętrznych), różne kształty (agregaty zamiast wierszy) albo różne wymagania techniczne (wyszukiwanie pełnotekstowe). Warto zaczynać od kilku modeli i dzielić je z konkretnego powodu. Model odczytu jest tani do zmiany, bo można go odbudować.

Zobacz: sekcja „Ile modeli odczytu”.

</details>

### 14. Jak dobrać magazyn dla read modelu (widok SQL, tabela zdenormalizowana, Elasticsearch, Redis, dokumentowa baza)?

<details>
<summary>Odpowiedź</summary>

Według rodzaju zapytań. Widok SQL to prosty start bez zysku wydajności. Widok zmaterializowany nadaje się do raportów odświeżanych okresowo. Tabela zdenormalizowana to listy i kolejki. Elasticsearch służy do pełnego tekstu i faset, Redis do liczników i rankingów, baza dokumentowa do szczegółów jako jednego dokumentu, a hurtownia do analityki. Domyślnym wyborem jest tabela zdenormalizowana w tej samej bazie. Nową technologię dodaje się, gdy relacyjna baza nie radzi sobie z danym typem zapytań.

Zobacz: sekcja „Wybór magazynu”.

</details>

### 15. Czy strona odczytu może czytać bezpośrednio z tabel strony zapisu? Jakie są konsekwencje takiego skrótu?

<details>
<summary>Odpowiedź</summary>

Może, to uprawniony skrót na początek. Konsekwencje: zmiany schematu zapisu psują zapytania odczytu, ciężkie raporty konkurują z komendami o zasoby, wracają JOIN-y i problemy wydajności, a uprawnienia trzeba sprawdzać przy każdym zapytaniu. Pośrednim krokiem są widoki SQL odcinające zapytania od schematu. Odwrotny kierunek, czyli krytyczne decyzje zapisu oparte na modelu odczytu, jest zakazany.

Zobacz: sekcja „Czytanie tabel zapisu”.

</details>

### 16. Jak obsłużyć zapytania, które łączą dane z wielu agregatów albo bounded contextów?

<details>
<summary>Odpowiedź</summary>

Kompozycją API: handler zapytania lub BFF woła kilka źródeł (często równolegle) i skleja wynik. Dane są zawsze aktualne, ale opóźnienia się sumują, a awaria źródła psuje ekran. Albo modelem odczytu zasilanym zdarzeniami z kilku kontekstów: jeden szybki odczyt, odporność na awarie źródeł, ale spójność ostateczna i koszt projekcji. Kompozycja wystarcza do szczegółów pojedynczego obiektu, a model zdarzeniowy jest potrzebny do filtrowania i sortowania po danych z wielu kontekstów.

Zobacz: sekcja „Dane z wielu źródeł”.

</details>
