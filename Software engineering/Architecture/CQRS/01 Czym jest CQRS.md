# Czym jest CQRS

<a id="term-cqrs"></a>[Command Query Responsibility Segregation](00%20Glossary%20CQRS.md#cqrs) (CQRS) to wzorzec, w którym operacje zmieniające stan systemu i operacje odczytu mają osobne modele. Nazwę i opis spopularyzował Greg Young około 2010 roku. Wzorzec wyrósł z prostszej zasady opisanej przez Bertranda Meyera dwadzieścia lat wcześniej.

Najprostszy model działania wygląda tak:

```text
                 ┌──────────────┐
komenda ────────►│ model zapisu │──── zapis ────► magazyn zapisu
                 └──────────────┘                     │
                                                      │ synchronizacja
                 ┌──────────────┐                     ▼
zapytanie ──────►│ model odczytu│◄─── odczyt ──── magazyn odczytu
                 └──────────────┘
```

Przykładem przewodnim tego tutorialu jest system zgłoszeń serwisowych (helpdesk). Klienci otwierają zgłoszenia, agenci je przejmują i rozwiązują, a kierownik patrzy na statystyki czasu reakcji.

## Od zasady do wzorca

<a id="term-cqs"></a>[CQS](00%20Glossary%20CQRS.md#cqs) (Command Query Separation) to zasada Bertranda Meyera z książki „Object-Oriented Software Construction”. Każda metoda powinna być albo komendą, która zmienia stan i nic nie zwraca, albo zapytaniem, które zwraca wynik i nie zmienia stanu. Zadanie pytania nie powinno zmieniać odpowiedzi.

```python
class Ticket:
    def assign(self, agent_id: str) -> None:      # komenda: zmienia stan, nic nie zwraca
        self.assignee_id = agent_id

    def is_overdue(self, now: datetime) -> bool:  # zapytanie: zwraca wynik, nic nie zmienia
        return self.status == "open" and now > self.due_at
```

CQS dotyczy pojedynczych metod. CQRS przenosi ten podział na poziom architektury: nie dwie metody na jednym obiekcie, tylko dwa osobne modele. Po stronie zapisu jest <a id="term-write-model"></a>[model zapisu](00%20Glossary%20CQRS.md#write-model), który pilnuje reguł biznesowych. Po stronie odczytu jest <a id="term-read-model"></a>[model odczytu](00%20Glossary%20CQRS.md#read-model), przygotowany pod konkretne ekrany i zapytania. Greg Young opisywał CQRS jako „dwa obiekty tam, gdzie wcześniej był jeden”.

## Jeden model, dwa sprzeczne cele

W klasycznej aplikacji jeden model, na przykład klasa `Ticket` zmapowana przez ORM, obsługuje wszystko. Zapis potrzebuje od niego czegoś innego niż odczyt:

| Potrzeba | Zapis | Odczyt |
|---|---|---|
| Kształt danych | znormalizowany, bez duplikacji | zdenormalizowany, gotowy do wyświetlenia |
| Zachowanie | reguły, walidacja, niezmienniki | brak, tylko dane |
| Zakres | jeden agregat naraz | wiele encji, filtry, sortowanie, agregacje |
| Obciążenie | mniej operacji, każda ważna | dużo więcej operacji, często 10–100 razy |
| Skalowanie | trudne, wymaga spójności | łatwe, można replikować i cache'ować |

Jeden model musi być kompromisem. Encja `Ticket` dostaje pola potrzebne tylko do list (`customer_name`, `agent_name`), gettery używane tylko przez raporty i relacje ładowane leniwie, które na liście generują setki zapytań. Reguły biznesowe giną wśród kodu, który służy tylko do wyświetlania. Jednocześnie zapytania do raportu SLA wymagają pięciu JOIN-ów, bo model jest znormalizowany pod zapis.

CQRS zdejmuje ten kompromis. Model zapisu może być mały i skupiony na regułach. Model odczytu może mieć dowolny kształt, bo nie pilnuje żadnych niezmienników.

## Co CQRS wymaga, a czego nie

CQRS nie wymaga:

- osobnych baz danych,
- kolejki ani brokera wiadomości,
- mikroserwisów,
- <a id="term-event-sourcing"></a>[event sourcingu](00%20Glossary%20CQRS.md#event-sourcing), czyli zapisywania stanu jako ciągu zdarzeń.

Każdy z tych elementów bywa używany razem z CQRS, ale żaden nie jest jego częścią. Najprostsza implementacja to dwa rodzaje klas w jednej aplikacji i jednej bazie:

```python
# strona zapisu: agregat z regułami, zapis przez repozytorium
class ResolveTicketHandler:
    def __call__(self, cmd: ResolveTicket) -> None:
        ticket = self._tickets.get(cmd.ticket_id)
        ticket.resolve(cmd.resolution, self._clock.now())
        self._tickets.save(ticket)


# strona odczytu: surowy SQL, żadnych encji
class AgentQueueQuery:
    def __call__(self, agent_id: str) -> list[QueueItem]:
        rows = self._db.execute(text("""
            SELECT t.id, t.title, t.priority, c.name AS customer, t.due_at
            FROM tickets t JOIN customers c ON c.id = t.customer_id
            WHERE t.assignee_id = :a AND t.status = 'open'
            ORDER BY t.priority, t.due_at
        """), {"a": agent_id})
        return [QueueItem(*r) for r in rows]
```

Obie strony czytają tę samą tabelę `tickets`. Mimo to jest to już CQRS: model zapisu i model odczytu to różne klasy o różnym kształcie i różnych zależnościach.

## Poziomy wdrożenia

CQRS można wdrażać stopniowo. Każdy poziom daje więcej swobody i kosztuje więcej:

```text
poziom 1  osobne klasy        handler komendy i handler zapytania, jedna baza, te same tabele
poziom 2  osobne modele       strona odczytu ma własne widoki lub tabele, aktualizowane w tej samej transakcji
poziom 3  osobne magazyny     odczyt w innej bazie (np. Elasticsearch), aktualizowany asynchronicznie
poziom 4  zdarzenia jako źródło  event sourcing po stronie zapisu, read modele budowane ze zdarzeń
```

| Poziom | Co zyskujesz | Co płacisz |
|---|---|---|
| 1 | czysty model zapisu, szybkie zapytania SQL | prawie nic |
| 2 | read modele dopasowane do ekranów | utrzymanie projekcji, wolniejszy zapis |
| 3 | niezależne skalowanie i dobór technologii | spójność ostateczna, outbox, monitoring opóźnień |
| 4 | pełna historia, dowolne nowe read modele z przeszłości | event store, wersjonowanie zdarzeń, zmiana sposobu myślenia |

Większość systemów, którym CQRS pomaga, zatrzymuje się na poziomie 1 albo 2. Poziom 3 jest uzasadniony, gdy odczyt ma zupełnie inne wymagania, na przykład wyszukiwanie pełnotekstowe. Poziom 4 to osobna decyzja, opisana w rozdziale 07.

## Kiedy nie stosować

Greg Young i Udi Dahan wielokrotnie ostrzegali przed używaniem CQRS jako architektury całego systemu. CQRS stosuje się w konkretnym bounded contextcie, w którym zapis i odczyt naprawdę się rozjeżdżają, a nie wszędzie „dla porządku”.

Sygnały, że CQRS nie jest potrzebny:

- aplikacja jest prostym CRUD-em, a ekrany pokazują dane w tej samej postaci, w jakiej są zapisywane,
- nie ma istotnych reguł biznesowych po stronie zapisu,
- obciążenie odczytu i zapisu jest podobne i małe,
- zespół nie ma doświadczenia ze spójnością ostateczną, a biznes wymaga natychmiastowej spójności wszędzie.

Sygnały, że może pomóc:

- ten sam model obsługuje bogate reguły i kilkanaście różnych widoków,
- raporty i listy są wolne, bo model jest znormalizowany pod zapis,
- odczyt potrzebuje innej technologii niż zapis (wyszukiwanie, cache, analityka),
- odczytów jest dużo więcej niż zapisów i trzeba je skalować osobno.

## Co zapamiętać

- CQS Meyera dzieli metody na komendy i zapytania, CQRS Younga dzieli modele.
- Model zapisu pilnuje reguł, model odczytu ma kształt dopasowany do ekranów.
- Jeden model dla obu stron jest kompromisem, który nie służy dobrze żadnej z nich.
- CQRS nie wymaga osobnych baz, kolejki, mikroserwisów ani event sourcingu.
- Najprostsza wersja to osobne klasy komend i zapytań w jednej bazie.
- Wdrożenie ma poziomy, a każdy kolejny dokłada kosztów, na czele ze spójnością ostateczną.
- CQRS stosuje się w wybranych częściach systemu, nie wszędzie.

## Pytania sprawdzające

### 1. Czym różni się CQS (Bertrand Meyer) od CQRS (Greg Young)? Dlaczego CQRS to coś więcej niż „metody bez efektów ubocznych”?

<details>
<summary>Odpowiedź</summary>

CQS to zasada na poziomie metod: metoda albo zmienia stan i nic nie zwraca, albo zwraca wynik i nic nie zmienia. CQRS przenosi podział na poziom architektury: zapis i odczyt mają osobne modele o różnym kształcie, zależnościach, a czasem magazynach. Chodzi nie tylko o brak efektów ubocznych w zapytaniach, ale o to, że strona odczytu w ogóle nie używa modelu z regułami biznesowymi.

Zobacz: sekcja „Od zasady do wzorca”.

</details>

### 2. Jaki problem rozwiązuje CQRS? Dlaczego jeden model do zapisu i odczytu staje się kompromisem, który nie służy żadnej ze stron?

<details>
<summary>Odpowiedź</summary>

Zapis potrzebuje znormalizowanego modelu z regułami, działającego na jednym agregacie. Odczyt potrzebuje zdenormalizowanych danych z wielu encji, z filtrami i agregacjami, przy dużo większym obciążeniu. Jeden model dostaje wtedy pola i relacje potrzebne tylko do list, co zaciemnia reguły, a jednocześnie raporty wymagają wielu JOIN-ów, bo model jest znormalizowany pod zapis. CQRS pozwala zoptymalizować każdą stronę osobno.

Zobacz: sekcja „Jeden model, dwa sprzeczne cele”.

</details>

### 3. Czy CQRS wymaga osobnych baz danych, event sourcingu, kolejki albo mikroserwisów? Jak wygląda najprostsza możliwa implementacja?

<details>
<summary>Odpowiedź</summary>

Nie wymaga żadnego z nich. Wszystkie bywają łączone z CQRS, ale nie są jego częścią. Najprostsza implementacja to osobne klasy w jednej aplikacji i jednej bazie: handler komendy ładuje agregat, wywołuje regułę i zapisuje go przez repozytorium, a handler zapytania wykonuje bezpośredni SQL i zwraca płaskie DTO, bez encji.

Zobacz: sekcja „Co CQRS wymaga, a czego nie”.

</details>

### 4. Jakie są poziomy wdrożenia CQRS (osobne klasy, osobne modele, osobne magazyny) i jakie koszty dochodzą na każdym poziomie?

<details>
<summary>Odpowiedź</summary>

Poziom 1: osobne klasy komend i zapytań w jednej bazie, praktycznie bez kosztów. Poziom 2: własne widoki lub tabele odczytu aktualizowane w tej samej transakcji, czyli koszt utrzymania projekcji i wolniejszego zapisu. Poziom 3: osobny magazyn odczytu aktualizowany asynchronicznie, czyli spójność ostateczna, outbox i monitoring opóźnień. Poziom 4: event sourcing po stronie zapisu, czyli event store, wersjonowanie zdarzeń i inny sposób myślenia. Większość systemów zatrzymuje się na poziomie 1 lub 2.

Zobacz: sekcja „Poziomy wdrożenia”.

</details>

### 5. Kiedy CQRS jest złym wyborem? Dlaczego Greg Young i Udi Dahan ostrzegają przed stosowaniem go w całym systemie?

<details>
<summary>Odpowiedź</summary>

CQRS jest złym wyborem w prostym CRUD-zie, przy braku istotnych reguł zapisu, przy małym i podobnym obciążeniu obu stron oraz tam, gdzie biznes wymaga natychmiastowej spójności wszędzie, a zespół nie zna spójności ostatecznej. Young i Dahan ostrzegają, bo CQRS dokłada złożoności, która opłaca się tylko w bounded contextach, gdzie zapis i odczyt naprawdę się rozjeżdżają. Stosowany wszędzie mnoży koszty bez korzyści.

Zobacz: sekcja „Kiedy nie stosować”.

</details>
