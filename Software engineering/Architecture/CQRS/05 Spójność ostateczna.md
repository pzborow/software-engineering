# Spójność ostateczna

Gdy projekcje działają asynchronicznie, model odczytu przez chwilę pokazuje stary stan. Agent przejmuje zgłoszenie, odświeża kolejkę i nie widzi go na liście. Technicznie wszystko działa poprawnie, ale użytkownik widzi błąd. Ten rozdział opisuje, skąd bierze się opóźnienie, jak je mierzyć i jak projektować system tak, żeby użytkownik go nie odczuł.

```text
t=0 ms     komenda AssignTicket zapisana, commit
t=5 ms     odpowiedź 200 OK do przeglądarki
t=20 ms    przeglądarka pyta o kolejkę agenta          ← stary stan
t=150 ms   relay publikuje zdarzenie z outboxa
t=300 ms   projekcja aktualizuje agent_queue
t=320 ms   kolejne zapytanie o kolejkę                  ← nowy stan
```

## Skąd opóźnienie

<a id="term-eventual-consistency"></a>[Eventual consistency](00%20Glossary%20CQRS.md#eventual-consistency) (spójność ostateczna) oznacza, że po zakończeniu zapisów wszystkie modele odczytu w końcu pokażą ten sam, aktualny stan, ale nie od razu. Gwarancja dotyczy tego, że odczyt dogoni zapis, a nie tego, kiedy to nastąpi.

Czas między commitem po stronie zapisu a widocznością zmiany w modelu odczytu to <a id="term-projection-lag"></a>[opóźnienie projekcji](00%20Glossary%20CQRS.md#projection-lag). Składa się z kilku części:

| Etap | Typowy czas | Od czego zależy |
|---|---|---|
| odczyt outboxa przez relay albo CDC | 10–500 ms | interwał odpytywania, obciążenie bazy |
| publikacja i dostarczenie przez broker | 1–50 ms | broker, sieć, batching |
| kolejka przed projekcją | 0 ms – minuty | tempo przetwarzania wobec tempa zdarzeń |
| przetworzenie i zapis modelu | 1–100 ms | złożoność projekcji, magazyn |
| refresh indeksu (Elasticsearch) | do 1 s | `refresh_interval` |

W normalnych warunkach opóźnienie wynosi setki milisekund. Po awarii projekcji, przy replayu albo przy nagłym wzroście ruchu może urosnąć do minut. System trzeba projektować na oba scenariusze.

## Własny zapis widoczny od razu

Najbardziej widoczny problem to brak <a id="term-read-your-writes"></a>[read-your-writes](00%20Glossary%20CQRS.md#read-your-writes): użytkownik nie widzi skutku własnej akcji. Inni użytkownicy zwykle nie zauważają opóźnienia rzędu sekundy, ale autor zmiany zauważa je od razu. Są cztery sposoby, żeby temu zapobiec.

Pierwszy sposób to <a id="term-consistency-token"></a>[token spójności](00%20Glossary%20CQRS.md#consistency-token). Komenda zwraca wersję agregatu albo pozycję w strumieniu. Klient przekazuje ją w zapytaniu, a handler zapytania czeka, aż projekcja do niej dotrze:

```python
class AgentQueueQuery:
    def __call__(self, agent_id: str, min_position: int | None = None) -> list[QueueItem]:
        if min_position is not None:
            self._wait_for(min_position, timeout=timedelta(seconds=2))
        return self._read(agent_id)

    def _wait_for(self, position: int, timeout: timedelta) -> None:
        deadline = time.monotonic() + timeout.total_seconds()
        while self._checkpoint("agent_queue") < position:
            if time.monotonic() > deadline:
                raise ReadModelBehind(position)       # API zwraca 503 z Retry-After albo stare dane z flagą
            time.sleep(0.05)
```

```text
POST /tickets/42/assignment          → 200 {"position": 18453}
GET  /agents/7/queue?min_position=18453
```

Drugi sposób to odczyt ze strony zapisu zaraz po zmianie. Ekran szczegółów zgłoszenia, na który użytkownik wraca po edycji, pobiera dane przez repozytorium zapisu, a nie przez model odczytu. Działa to dla pojedynczych obiektów, ale nie dla list i wyszukiwania.

Trzeci sposób to projekcja synchroniczna dla modeli, które autor zmiany ogląda od razu. Opisuje ją rozdział 04.

Czwarty sposób to aktualizacja po stronie klienta, opisana w następnej sekcji.

| Sposób | Dobry dla | Koszt |
|---|---|---|
| token spójności | listy, kolejki, wszystkie modele | czekanie w zapytaniu, obsługa timeoutu |
| odczyt ze strony zapisu | szczegóły jednego obiektu | część ruchu odczytu wraca na stronę zapisu |
| projekcja synchroniczna | kluczowe modele w tej samej bazie | wolniejszy zapis |
| aktualizacja w kliencie | interaktywne UI | logika po stronie frontendu |

## Interfejs, który nie czeka

Wiele problemów z opóźnieniem rozwiązuje się w UI, bez zmian w backendzie.

<a id="term-optimistic-ui"></a>[Optymistyczny UI](00%20Glossary%20CQRS.md#optimistic-ui) zakłada, że komenda się powiedzie, i od razu pokazuje jej skutek. Po kliknięciu „Przejmij” zgłoszenie pojawia się w kolejce agenta, zanim serwer potwierdzi. Jeśli komenda zostanie odrzucona, UI cofa zmianę i pokazuje komunikat. Działa to dobrze, gdy odrzucenia są rzadkie, a skutek komendy łatwo przewidzieć.

Inne wzorce:

- komunikat o przetwarzaniu: „Zgłoszenie zostało przekazane. Lista odświeży się za chwilę”, uczciwy i tani,
- przekierowanie na widok potwierdzenia zamiast listy, bo potwierdzenie można zbudować z danych komendy,
- powiadomienia push przez WebSocket albo SSE: projekcja po aktualizacji modelu wysyła zdarzenie „kolejka agenta 7 zmieniona”, a UI odświeża dane,
- task-based UI: interfejs oferuje akcje zamiast formularzy edycji, dzięki czemu skutek każdej akcji jest przewidywalny.

Połączenie optymistycznego UI z pushem daje dobre wrażenie natychmiastowości: zmiana pojawia się od razu, a push potwierdza albo koryguje ją po faktycznej aktualizacji modelu.

## Pomiar i akceptowalny poziom

Opóźnienia nie da się zarządzać, jeśli się go nie mierzy. Podstawową miarą jest różnica między czasem zapisu zdarzenia a czasem jego przetworzenia przez projekcję, liczona per projekcja:

```python
def handle_with_metrics(self, stored: StoredEvent) -> None:
    self._projection.handle(stored.payload)
    lag = (datetime.now(UTC) - stored.recorded_at).total_seconds()
    PROJECTION_LAG.labels(projection="agent_queue").observe(lag)
    PROJECTION_POSITION.labels(projection="agent_queue").set(stored.position)
```

Drugą miarą jest liczba nieprzetworzonych zdarzeń, czyli różnica między ostatnią pozycją w strumieniu a checkpointem projekcji. Jeśli rośnie, projekcja nie nadąża.

Akceptowalne opóźnienie to decyzja biznesowa, a nie techniczna. Właściciel produktu powinien odpowiedzieć na pytania:

- Jak długo agent może nie widzieć nowego zgłoszenia w kolejce? Może 5 sekund.
- Jak długo raport SLA może być nieaktualny? Może 15 minut.
- Co się stanie, jeśli wyszukiwarka pokaże zamknięte zgłoszenie jako otwarte? Nic groźnego.

Odpowiedzi stają się celami (np. „p99 opóźnienia `agent_queue` poniżej 2 s”) i progami alertów. Bez nich każda dyskusja o opóźnieniu zaczyna się od „wydaje mi się, że jest wolno”.

## Kiedy ostatecznie to za mało

Niektórych decyzji nie wolno podejmować na nieaktualnych danych. Wymagają one <a id="term-strong-consistency"></a>[silnej spójności](00%20Glossary%20CQRS.md#strong-consistency), czyli gwarancji, że odczyt widzi wszystkie zakończone zapisy.

Przykłady:

- saldo konta przed wypłatą,
- dostępność ostatniego miejsca albo ostatniej sztuki towaru,
- uprawnienia użytkownika po ich odebraniu,
- limit, którego przekroczenie ma skutki prawne lub finansowe.

W takich przypadkach decyzję podejmuje strona zapisu na podstawie własnych danych, w transakcji. Model odczytu może nadal służyć do wyświetlania („zostało 3 miejsca”), ale sama rezerwacja sprawdza dostępność w agregacie. To ta sama zasada, co przy walidacji w rozdziale 02: reguła krytyczna nie opiera się na modelu odczytu.

Połączenie wygląda tak: lista i wyszukiwanie korzystają ze spójności ostatecznej, szczegóły po edycji z odczytu ze strony zapisu albo z tokenu spójności, a decyzje krytyczne z danych zapisu w transakcji. Nie trzeba wybierać jednego modelu spójności dla całego systemu.

## Co zapamiętać

- Spójność ostateczna gwarantuje, że odczyt dogoni zapis, ale nie mówi kiedy.
- Opóźnienie projekcji składa się z relaya, brokera, kolejki, przetwarzania i refreshu. Normalnie są to setki milisekund, po awarii nawet minuty.
- Read-your-writes zapewnia token spójności, odczyt ze strony zapisu, projekcja synchroniczna albo aktualizacja w kliencie.
- Optymistyczny UI, komunikaty i push przez WebSocket ukrywają opóźnienie przed użytkownikiem.
- Opóźnienie mierzy się per projekcja, a akceptowalny poziom ustala biznes.
- Decyzje krytyczne wymagają silnej spójności i podejmuje je strona zapisu w transakcji.

## Pytania sprawdzające

### 23. Czym jest spójność ostateczna w CQRS i skąd bierze się opóźnienie między zapisem a odczytem?

<details>
<summary>Odpowiedź</summary>

To gwarancja, że po zakończeniu zapisów modele odczytu w końcu pokażą aktualny stan, ale nie od razu. Opóźnienie projekcji składa się z odczytu outboxa przez relay albo CDC, dostarczenia przez broker, czasu oczekiwania w kolejce, przetworzenia przez projekcję i ewentualnego refreshu indeksu. Normalnie są to setki milisekund, ale po awarii, przy replayu lub skoku ruchu nawet minuty.

Zobacz: sekcja „Skąd opóźnienie”.

</details>

### 24. Jak zapewnić read-your-writes dla użytkownika, który właśnie coś zapisał (wersja w odpowiedzi, czekanie na projekcję, odczyt ze strony zapisu)?

<details>
<summary>Odpowiedź</summary>

Token spójności: komenda zwraca wersję lub pozycję, a zapytanie z `min_position` czeka, aż checkpoint projekcji ją osiągnie, z timeoutem i obsługą przekroczenia. Odczyt ze strony zapisu dla szczegółów pojedynczego obiektu tuż po zmianie. Projekcja synchroniczna dla kluczowych modeli w tej samej bazie. Aktualizacja po stronie klienta (optymistyczny UI). Wybór zależy od rodzaju ekranu.

Zobacz: sekcja „Własny zapis widoczny od razu”.

</details>

### 25. Jak projektować UX przy opóźnionym odczycie (optymistyczny UI, komunikat „przetwarzanie”, push przez WebSocket)?

<details>
<summary>Odpowiedź</summary>

Optymistyczny UI od razu pokazuje przewidywany skutek komendy i cofa go przy odrzuceniu, co działa, gdy odrzucenia są rzadkie. Dostępne są też: uczciwy komunikat o przetwarzaniu, widok potwierdzenia zbudowany z danych komendy zamiast listy, push przez WebSocket lub SSE po aktualizacji modelu oraz task-based UI z przewidywalnymi akcjami. Połączenie optymistycznego UI z pushem daje wrażenie natychmiastowości.

Zobacz: sekcja „Interfejs, który nie czeka”.

</details>

### 26. Jak zmierzyć i ustalić akceptowalne opóźnienie projekcji? Kto w firmie powinien o tym zdecydować?

<details>
<summary>Odpowiedź</summary>

Mierzy się je per projekcja jako różnicę między czasem zapisu zdarzenia a czasem jego przetworzenia (histogram, p99) oraz jako liczbę nieprzetworzonych zdarzeń (ostatnia pozycja minus checkpoint). Akceptowalny poziom to decyzja biznesowa właściciela produktu, podejmowana osobno dla każdego modelu (np. kolejka 5 s, raport 15 min). Odpowiedzi stają się celami i progami alertów.

Zobacz: sekcja „Pomiar i akceptowalny poziom”.

</details>

### 27. Kiedy spójność ostateczna jest nie do przyjęcia i jak wtedy łączyć CQRS z odczytem silnie spójnym?

<details>
<summary>Odpowiedź</summary>

Gdy decyzja na nieaktualnych danych ma poważne skutki: saldo przed wypłatą, ostatnie miejsce, odebrane uprawnienia, limity prawne lub finansowe. Taką decyzję podejmuje strona zapisu na własnych danych w transakcji, a model odczytu służy tylko do wyświetlania. W jednym systemie można łączyć poziomy: listy ze spójnością ostateczną, szczegóły po edycji przez token lub odczyt ze strony zapisu, decyzje krytyczne z silną spójnością.

Zobacz: sekcja „Kiedy ostatecznie to za mało”.

</details>
