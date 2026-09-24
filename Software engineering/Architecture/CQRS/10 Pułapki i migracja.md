# Pułapki i migracja

CQRS ma prostą ideę i dużo miejsc, w których można się pomylić. Większość problemów w projektach CQRS nie wynika z trudnej techniki, tylko z decyzji: gdzie wzorzec zastosować, jak podzielić odpowiedzialności i jak szybko przejść do wersji z osobnymi magazynami. Ten rozdział zbiera najczęstsze błędy i pokazuje, jak wprowadzać CQRS do istniejącego systemu bez przepisywania go.

## Najczęstsze błędy

Pierwszy błąd to CQRS wszędzie. Zespół wprowadza komendy, zdarzenia, projekcje i osobne bazy w każdym module, także w CRUD-owym słowniku kategorii. Każda zmiana wymaga wtedy modyfikacji komendy, handlera, zdarzenia, projekcji i modelu odczytu, a na końcu użytkownik i tak widzi te same dane, które wpisał. CQRS stosuje się w kontekstach, w których zapis i odczyt naprawdę się różnią (rozdział 01).

Drugi błąd to <a id="term-crud-command"></a>[komendy CRUD](00%20Glossary%20CQRS.md#crud-command): `CreateTicket`, `UpdateTicket`, `DeleteTicket` z pełnym zestawem pól. Komenda `UpdateTicket` nie mówi, co się stało, więc handler nie wie, które reguły sprawdzić, a zdarzenie `TicketUpdated` zmusza każdą projekcję do porównywania pól, żeby zgadnąć intencję. Komendy powinny wyrażać zadania biznesowe, a interfejs powinien być zbudowany jako <a id="term-task-based-ui"></a>[task-based UI](00%20Glossary%20CQRS.md#task-based-ui) (rozdział 02).

```python
# komenda CRUD: intencja ukryta
UpdateTicket(ticket_id="T-1", status="resolved", assignee_id="A-7", priority="high", note="...")

# komendy zadaniowe: intencja jawna
ResolveTicket(ticket_id="T-1", resolution="replaced")
EscalateTicket(ticket_id="T-1", new_priority="high", reason="klient VIP")
```

Trzeci błąd to logika biznesowa w projekcjach. Projekcja zaczyna decydować: „jeśli zgłoszenie jest otwarte dłużej niż 4 godziny, oznacz je jako przeterminowane i wyślij e-mail”. Reguła działa tylko w tej projekcji, nie ma jej w modelu zapisu, a przy replayu e-maile wyjdą ponownie. Decyzje należą do strony zapisu albo do process managera, a projekcja tylko przekłada fakty na dane. Efekty uboczne, takie jak e-mail, obsługują osobni, idempotentni konsumenci zdarzeń, których nie uruchamia się przy replayu.

Czwarty błąd to ignorowanie opóźnień. Na środowisku deweloperskim projekcja działa w kilka milisekund i nikt nie zauważa spójności ostatecznej. Na produkcji, pod obciążeniem albo po awarii, opóźnienie rośnie do minut, a UI pokazuje stare dane zaraz po zapisie. Opóźnienie trzeba zaprojektować od początku: read-your-writes, optymistyczny UI, cele i alerty (rozdział 05).

| Błąd | Objaw | Naprawa |
|---|---|---|
| CQRS wszędzie | każda zmiana dotyka pięciu plików, brak korzyści | CQRS tylko w wybranych kontekstach |
| komendy CRUD | `UpdateX` z wszystkimi polami, projekcje zgadują intencję | komendy zadaniowe, task-based UI |
| logika w projekcjach | reguły poza modelem zapisu, efekty uboczne przy replayu | decyzje w agregacie lub process managerze |
| ignorowanie opóźnień | „zapisałem, a nie widzę” | read-your-writes, UX, metryki opóźnienia |
| krytyczne decyzje na modelu odczytu | przekroczone limity, podwójne rezerwacje | reguły krytyczne na danych zapisu |
| współdzielony model odczytu między zespołami | zmiana projekcji psuje innym ekrany | model odczytu należy do jednego odbiorcy |
| od razu poziom 4 (event sourcing i osobne bazy) | miesiące budowy infrastruktury przed pierwszą funkcją | wdrażanie poziomami |

## Wprowadzanie do istniejącego systemu

Istniejący system helpdesk działa na jednym modelu ORM. Lista zgłoszeń agenta jest wolna, raport SLA spowalnia bazę, a klasa `Ticket` ma 60 pól i 40 metod. Przepisanie całości od nowa to ryzyko bez gwarancji sukcesu. Bezpieczniej jest przechodzić poziomami z rozdziału 01, według wzorca <a id="term-strangler-fig"></a>[strangler fig](00%20Glossary%20CQRS.md#strangler-fig): nowa struktura stopniowo przejmuje funkcje starej.

```text
krok 1  osobne zapytania        wolne ekrany dostają własne handlery zapytań z SQL, bez ORM
krok 2  komendy zadaniowe       najczęściej zmieniane operacje dostają komendy i handlery
krok 3  modele odczytu          najwolniejsze ekrany dostają tabele zdenormalizowane, projekcja synchroniczna
krok 4  zdarzenia i outbox      zapis emituje zdarzenia do outboxa, pierwsze projekcje asynchroniczne
krok 5  osobne magazyny         wyszukiwarka do Elasticsearch, raporty do hurtowni
krok 6  (opcjonalnie) ES        event sourcing tylko tam, gdzie historia jest wartością biznesową
```

Każdy krok jest osobnym wdrożeniem, daje zauważalny efekt i można się na nim zatrzymać. Wiele systemów osiąga cel po kroku 3.

Krok 1 nie wymaga żadnej infrastruktury. Wystarczy wydzielić zapytania z modelu ORM:

```python
# przed: lista budowana z modelu ORM, 1 + N zapytań
tickets = session.query(Ticket).filter_by(assignee_id=agent_id, status="open").all()
return [{"title": t.title, "customer": t.customer.name, "messages": len(t.messages)} for t in tickets]

# po: handler zapytania, jedno zapytanie SQL, bez ORM
class AgentQueueQuery:
    def __call__(self, agent_id: str) -> list[QueueItem]:
        return [QueueItem(*r) for r in self._db.execute(text("""
            SELECT t.id, t.title, c.name, t.priority, t.sla_deadline, count(m.id)
            FROM tickets t JOIN customers c ON c.id = t.customer_id
            LEFT JOIN messages m ON m.ticket_id = t.id
            WHERE t.assignee_id = :a AND t.status = 'open'
            GROUP BY t.id, c.name
        """), {"a": agent_id})]
```

W kroku 3 tabela zdenormalizowana powstaje obok starych tabel. Wypełnia się ją jednorazowym zapytaniem z istniejących danych, a potem aktualizuje przez projekcję synchroniczną w tej samej transakcji co zapis. Stary kod ekranu przełącza się na nowy handler zapytania, a po okresie porównywania wyników stare zapytanie się usuwa.

W kroku 4 najważniejsze jest wprowadzenie outboxa, zanim pojawi się pierwsza projekcja asynchroniczna albo pierwszy konsument w innym serwisie. Publikowanie zdarzeń bezpośrednio z handlera, „tymczasowo, bez outboxa”, prowadzi do dual write, który na produkcji objawi się dopiero po pierwszej awarii (rozdział 06).

Na każdym kroku zasada jest ta sama: najpierw mierzalny problem (wolna lista, obciążona baza, potrzeba wyszukiwania), potem najmniejszy krok CQRS, który go rozwiązuje.

## Co zapamiętać

- CQRS stosuje się w wybranych kontekstach, a nie w całym systemie.
- Komendy wyrażają zadania biznesowe. Komendy CRUD ukrywają intencję przed handlerem i projekcjami.
- Projekcje nie podejmują decyzji i nie wywołują efektów ubocznych, które powtórzyłyby się przy replayu.
- Opóźnienie projekcji trzeba zaprojektować od początku, bo na produkcji zawsze się pojawi.
- Migracja idzie poziomami: osobne zapytania, komendy zadaniowe, modele odczytu, zdarzenia z outboxem, osobne magazyny, event sourcing.
- Każdy krok rozwiązuje zmierzony problem i może być ostatnim.

## Pytania sprawdzające

### 44. Jakie są najczęstsze błędy przy wdrażaniu CQRS (CQRS wszędzie, logika biznesowa w projekcjach, komendy jako CRUD, ignorowanie opóźnień)?

<details>
<summary>Odpowiedź</summary>

CQRS wszędzie: narzut plików i infrastruktury bez korzyści w modułach CRUD. Komendy CRUD (`UpdateTicket` z wszystkimi polami): intencja ukryta przed handlerem i projekcjami. Rozwiązaniem są komendy zadaniowe i task-based UI. Logika w projekcjach: reguły poza modelem zapisu i efekty uboczne powtarzane przy replayu. Decyzje należą do agregatu lub process managera. Ignorowanie opóźnień: problemy widoczne dopiero na produkcji. Inne błędy to krytyczne decyzje na modelu odczytu, współdzielenie modeli odczytu między zespołami i startowanie od razu z event sourcingiem i osobnymi bazami.

Zobacz: sekcja „Najczęstsze błędy”.

</details>

### 45. Jak stopniowo wprowadzić CQRS do istniejącego systemu (najpierw osobne modele odczytu, potem osobny magazyn, na końcu zdarzenia)?

<details>
<summary>Odpowiedź</summary>

Poziomami, według wzorca strangler fig. Najpierw osobne handlery zapytań z SQL dla wolnych ekranów, bez infrastruktury. Potem komendy zadaniowe dla najczęściej zmienianych operacji. Dalej tabele zdenormalizowane z projekcją synchroniczną, wypełnione jednorazowo z istniejących danych i porównywane ze starym zapytaniem. Następnie zdarzenia z outboxem (zanim pojawi się pierwszy konsument asynchroniczny), osobne magazyny dla wyszukiwania i raportów, a event sourcing tylko tam, gdzie historia ma wartość biznesową. Każdy krok odpowiada na zmierzony problem i może być ostatnim.

Zobacz: sekcja „Wprowadzanie do istniejącego systemu”.

</details>
