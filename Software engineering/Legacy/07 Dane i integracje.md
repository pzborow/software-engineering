# Dane i integracje

Kod można cofnąć jednym wdrożeniem. Danych nie. Błędna migracja schematu, utracona kolumna albo źle przeniesione faktury to problemy, których nie naprawi rollback aplikacji. Do tego dane legacy mają zwykle więcej odbiorców, niż ktokolwiek pamięta: raporty, eksporty, skrypty księgowości, stary system magazynowy. Ten rozdział pokazuje, jak zmieniać dane i integracje w małych, odwracalnych krokach.

```text
problem                                          technika
zmiana kolumny, której używa działający kod      expand and contract
nieznani odbiorcy tabeli                         odkrywanie, widoki zgodności, monitorowanie użycia
nowy kod rozmawia ze starym systemem             anti-corruption layer
przeniesienie danych do nowego systemu           migracja, synchronizacja, podwójny zapis, uzgodnienie
```

## Zmiana schematu w kilku krokach

Zmiana schematu w jednym kroku („zmień nazwę kolumny `total` na `gross_amount`”) wymaga, żeby w tej samej chwili zmienił się kod wszystkich odbiorców. W systemie z kilkoma instancjami aplikacji, zadaniami w tle i raportami to niemożliwe. Przez kilka minut wdrożenia stara wersja kodu będzie czytać kolumnę, której już nie ma.

<a id="term-expand-contract"></a>[Expand and contract](00%20Glossary%20Legacy.md#expand-contract) (inaczej parallel change) dzieli zmianę na fazy, z których każda jest zgodna z poprzednią i następną wersją kodu:

```text
faza 1  expand     dodaj nową strukturę obok starej          stary kod działa bez zmian
faza 2  migrate    zapisuj do obu, uzupełnij stare dane      stary i nowy kod działają równocześnie
faza 3  switch     czytaj z nowej struktury                  stara struktura nadal aktualizowana
faza 4  contract   przestań pisać do starej, usuń ją         dopiero gdy nikt jej nie czyta
```

Przykład: kwota faktury była zapisywana jako `total FLOAT` brutto. Nowy wymóg KSeF to osobno netto, VAT i brutto w typie dokładnym.

```sql
-- faza 1: expand (wdrożenie 1)
ALTER TABLE invoices ADD COLUMN net_amount NUMERIC(12,2);
ALTER TABLE invoices ADD COLUMN vat_amount NUMERIC(12,2);
ALTER TABLE invoices ADD COLUMN gross_amount NUMERIC(12,2);
```

```python
# faza 2: kod zapisuje do starej i nowych kolumn (wdrożenie 2)
db.execute(
    "INSERT INTO invoices (number, order_id, total, net_amount, vat_amount, gross_amount) "
    "VALUES (%s, %s, %s, %s, %s, %s)",
    number, order_id, float(gross), net, vat, gross,
)
```

```sql
-- faza 2: uzupełnienie historii w paczkach, żeby nie blokować tabeli (zadanie w tle)
UPDATE invoices SET gross_amount = ROUND(total::numeric, 2)
WHERE id IN (SELECT id FROM invoices WHERE gross_amount IS NULL ORDER BY id LIMIT 5000);
```

Takie uzupełnienie istniejących wierszy nazywa się <a id="term-backfill"></a>[backfill](00%20Glossary%20Legacy.md#backfill). Robi się je w paczkach, bo jedno `UPDATE` na milionach wierszy zablokuje tabelę i zapełni log transakcji. Wartości `net_amount` i `vat_amount` dla starych faktur trzeba wyliczyć z pozycji zamówień, bo nie da się ich odtworzyć z samej kwoty brutto.

```python
# faza 3: odczyt z nowych kolumn, zapis nadal do obu (wdrożenie 3)
row = db.query("SELECT number, gross_amount FROM invoices WHERE id=%s", invoice_id)[0]
```

```sql
-- faza 4: contract, gdy nikt nie czyta kolumny total (wdrożenie 4, po tygodniach)
ALTER TABLE invoices DROP COLUMN total;
```

Każda faza jest osobnym wdrożeniem i każdą można cofnąć bez utraty danych, aż do fazy 4. Dlatego faza 4 następuje dopiero po sprawdzeniu, że starej kolumny nikt nie używa.

## Nieznani odbiorcy danych

Tabela `invoices` istnieje od 2014 roku. Czyta ją aplikacja, ale też nocny eksport do systemu księgowego, raport w Metabase, skrypt działu finansów uruchamiany raz na kwartał i stary system magazynowy, który ma bezpośrednie połączenie z bazą. Nikt nie ma pełnej listy. Usunięcie kolumny `total` w fazie 4 zepsuje coś, o czym zespół dowie się z opóźnieniem, często w najgorszym możliwym momencie, np. przy zamknięciu kwartału.

Jak znaleźć ukrytych odbiorców:

- statystyki zapytań w bazie: `pg_stat_statements` w PostgreSQL pokazuje, jakie zapytania są wykonywane i jak często,
- log zapytań z nazwą aplikacji: każde połączenie ustawia `application_name`, więc widać, kto czyta,
- osobni użytkownicy bazy dla każdego odbiorcy zamiast jednego wspólnego konta, dzięki czemu log pokazuje, kto co robi,
- przeszukanie innych repozytoriów, harmonogramów zadań, konfiguracji narzędzi BI i arkuszy z połączeniami ODBC,
- zapytanie do ludzi: finanse, analitycy, administratorzy.

```sql
-- kto czyta kolumnę total w ostatnim czasie
SELECT calls, query
FROM pg_stat_statements
WHERE query ILIKE '%invoices%' AND query ILIKE '%total%'
ORDER BY calls DESC;
```

Gdy odbiorców nie da się zmienić od razu, stosuje się <a id="term-compatibility-view"></a>[widok zgodności](00%20Glossary%20Legacy.md#compatibility-view): tabela zmienia strukturę, a stara struktura zostaje udostępniona jako widok o tej samej nazwie, z którego korzystają dotychczasowi odbiorcy.

```sql
ALTER TABLE invoices RENAME TO invoices_v2;
CREATE VIEW invoices AS
SELECT id, number, order_id, gross_amount::float AS total, created_at
FROM invoices_v2;
```

Ostatnim krokiem jest ostrożne wyłączenie. Zamiast od razu usuwać kolumnę, można ją najpierw przemianować (`total_deprecated`) albo odebrać uprawnienia i obserwować błędy przez tydzień. Jeśli nikt się nie zgłosi, usuwa się ją naprawdę. Takie podejście nazywa się czasem scream test: wyłącz coś i sprawdź, kto krzyknie.

## Ochrona przed starym modelem

Nowy moduł fakturowania musi pobierać dane klientów ze starego systemu CRM, w którym klient to tabela `KLIENCI` z kolumnami `TYP_KL` („F” lub „O”), `KRAJ_KOD` (numery krajów z wewnętrznego słownika) i `NIP_UE` (czasem z prefiksem kraju, czasem bez). Jeśli nowy kod zacznie operować tymi pojęciami, stanie się tak samo trudny jak stary.

<a id="term-anti-corruption-layer"></a>[Anti-corruption layer](00%20Glossary%20Legacy.md#anti-corruption-layer) (ACL) to warstwa tłumacząca, która stoi między nowym kodem a starym systemem. Nowy kod zna tylko własny model. ACL wie, jak przetłumaczyć stare pojęcia na nowe i z powrotem.

```python
# nowy model: jasne pojęcia, typy, walidacja
@dataclass(frozen=True)
class Customer:
    id: str
    kind: CustomerKind                     # CONSUMER albo BUSINESS
    country: str                           # ISO 3166, np. "PL", "DE"
    eu_vat_id: str | None                  # zawsze z prefiksem kraju


# ACL: jedyne miejsce, które zna stary CRM
class LegacyCrmCustomers:
    KIND = {"O": CustomerKind.CONSUMER, "F": CustomerKind.BUSINESS}

    def __init__(self, crm_db, country_codes: dict[int, str]):
        self._db = crm_db
        self._countries = country_codes     # słownik z tabeli SLOW_KRAJE, wczytany raz

    def get(self, customer_id: str) -> Customer:
        row = self._db.query("SELECT * FROM KLIENCI WHERE ID_KL = %s", customer_id)[0]
        country = self._countries[row["KRAJ_KOD"]]
        return Customer(
            id=str(row["ID_KL"]),
            kind=self.KIND[row["TYP_KL"]],
            country=country,
            eu_vat_id=self._normalize_vat_id(row["NIP_UE"], country),
        )

    @staticmethod
    def _normalize_vat_id(raw: str | None, country: str) -> str | None:
        if not raw:
            return None
        raw = raw.replace("-", "").replace(" ", "").upper()
        return raw if raw[:2].isalpha() else country + raw
```

Zasady:

- ACL jest jedynym miejscem, które zna stare nazwy, kody i formaty. Nigdzie indziej w nowym kodzie nie ma `TYP_KL` ani `KRAJ_KOD`,
- ACL tłumaczy także dziwactwa danych: brakujące wartości, niespójne formaty, magiczne kody. Każde takie tłumaczenie ma test,
- ACL działa w obie strony, jeśli nowy kod coś zapisuje do starego systemu,
- gdy stary system zostanie wymieniony, zmienia się tylko ACL, a nowy moduł pozostaje bez zmian.

ACL jest zwykle największym i najbrzydszym fragmentem nowego kodu, bo zbiera całą złożoność starego świata. To dobrze, bo ta złożoność jest w jednym miejscu, z testami, a nie rozlana po nowym systemie.

## Przeniesienie danych

Gdy nowy moduł fakturowania przejmuje funkcje starego (rozdział 06), trzeba przenieść dane: historię faktur, numerację, dane klientów. Są trzy podejścia, zwykle łączone.

Migracja jednorazowa: skrypt kopiuje dane ze starego systemu do nowego w oknie serwisowym. Jest prosta, ale wymaga przestoju albo zamrożenia zmian i daje jedną szansę na poprawny wynik.

Synchronizacja ciągła: stary system pozostaje źródłem prawdy, a zmiany są na bieżąco przenoszone do nowego przez zdarzenia, change data capture (np. Debezium czytający log bazy) albo okresowy import. Nowy system może działać równolegle przez tygodnie.

<a id="term-dual-write"></a>[Podwójny zapis](00%20Glossary%20Legacy.md#dual-write) (dual write): aplikacja zapisuje każdą zmianę do obu systemów. Wygląda najprościej, ale jest najbardziej ryzykowny. Bez wspólnej transakcji zapis do jednego systemu może się udać, a do drugiego nie, i dane się rozjeżdżają. Jeśli już go stosować, to z mechanizmem, który wykrywa i naprawia rozbieżności, albo z zapisem do tabeli pośredniej w tej samej transakcji (outbox) i asynchronicznym przeniesieniem.

```text
typowa kolejność przy przejmowaniu fakturowania

1. migracja jednorazowa historii (faktury sprzed 2026)            stary system nadal źródłem prawdy
2. synchronizacja ciągła nowych faktur stary → nowy (CDC)          nowy system tylko czyta
3. parallel run: nowy liczy faktury, porównanie ze starym          rozdział 06
4. przełączenie: nowy system źródłem prawdy, synchronizacja nowy → stary, dla starych raportów
5. wyłączenie synchronizacji i starego systemu
```

Niezależnie od podejścia potrzebne jest <a id="term-data-reconciliation"></a>[uzgodnienie danych](00%20Glossary%20Legacy.md#data-reconciliation) (reconciliation): regularne porównanie danych w obu systemach, które wykrywa rozbieżności. Porównuje się liczby rekordów, sumy kontrolne i próbki szczegółowe.

```python
def reconcile_invoices(day: date, old_db, new_db) -> list[str]:
    problems = []
    old = {r["number"]: Decimal(str(r["total"])) for r in old_db.query(
        "SELECT number, total FROM invoices WHERE created_at::date = %s", day)}
    new = {r["number"]: r["gross_amount"] for r in new_db.query(
        "SELECT number, gross_amount FROM invoices WHERE issued_on = %s", day)}

    for number in old.keys() - new.keys():
        problems.append(f"brak w nowym: {number}")
    for number in new.keys() - old.keys():
        problems.append(f"nadmiarowa w nowym: {number}")
    for number in old.keys() & new.keys():
        if abs(old[number] - new[number]) > Decimal("0.01"):
            problems.append(f"różnica kwoty {number}: {old[number]} vs {new[number]}")
    if sum(old.values()) != sum(new.values()):
        problems.append(f"suma dnia: {sum(old.values())} vs {sum(new.values())}")
    return problems
```

Uzgodnienie uruchamia się codziennie przez cały okres przejściowy, a jego wynik trafia do alertów. Przełączenie źródła prawdy następuje dopiero po okresie bez rozbieżności, obejmującym także nietypowe dni: koniec miesiąca, korekty, zwroty.

## Co zapamiętać

- Danych nie da się cofnąć jak kodu, więc zmienia się je w małych, odwracalnych krokach.
- Expand and contract dzieli zmianę schematu na fazy zgodne z sąsiednimi wersjami kodu: dodaj, zapisuj do obu i uzupełnij, przełącz odczyt, usuń.
- Backfill wykonuje się w paczkach, żeby nie blokować tabel.
- Ukrytych odbiorców danych szuka się w statystykach zapytań, logach, innych repozytoriach i u ludzi. Widok zgodności i scream test chronią przed zepsuciem ich pracy.
- Anti-corruption layer tłumaczy stary model na nowy i jest jedynym miejscem, które zna stare pojęcia.
- Dane przenosi się migracją jednorazową, synchronizacją ciągłą albo podwójnym zapisem. Ten ostatni jest najbardziej ryzykowny.
- Uzgodnienie danych codziennie porównuje oba systemy i warunkuje przełączenie źródła prawdy.

## Pytania sprawdzające

### 28. Jak bezpiecznie zmieniać schemat bazy w działającym systemie (expand and contract, migracje w kilku krokach)?

<details>
<summary>Odpowiedź</summary>

Przez expand and contract (parallel change). Najpierw expand, czyli dodanie nowej struktury obok starej. Potem zapis do obu i backfill starych danych w paczkach. Następnie przełączenie odczytu na nową strukturę. Na końcu contract, czyli usunięcie starej struktury, dopiero gdy nikt jej nie czyta. Każda faza jest osobnym wdrożeniem zgodnym z poprzednią i następną wersją kodu, więc do fazy końcowej wszystko można cofnąć bez utraty danych. Zmiana w jednym kroku psuje instancje i zadania działające na starej wersji podczas wdrożenia.

Zobacz: sekcja „Zmiana schematu w kilku krokach”.

</details>

### 29. Jak zmienić strukturę danych, z której korzysta kilka systemów lub raportów, o których nikt nie pamięta?

<details>
<summary>Odpowiedź</summary>

Najpierw znaleźć odbiorców: statystyki zapytań (`pg_stat_statements`), `application_name` i osobni użytkownicy bazy per odbiorca, przeszukanie repozytoriów, harmonogramów i narzędzi BI oraz rozmowy z finansami i analitykami. Gdy odbiorców nie da się od razu zmienić, stosuje się widok zgodności: stara struktura dostępna jako widok o tej samej nazwie. Usuwa się ostrożnie: najpierw zmiana nazwy lub odebranie uprawnień i obserwacja (scream test), a dopiero potem faktyczne usunięcie.

Zobacz: sekcja „Nieznani odbiorcy danych”.

</details>

### 30. Czym jest anti-corruption layer i jak chroni nowy kod przed pojęciami i danymi starego systemu?

<details>
<summary>Odpowiedź</summary>

To warstwa tłumacząca między nowym kodem a starym systemem. Nowy kod zna tylko własny model (np. `Customer` z `CustomerKind` i krajem ISO), a ACL zamienia stare pojęcia, kody i formaty (`TYP_KL`, `KRAJ_KOD`, niespójny `NIP_UE`) na nowe i z powrotem. Jest jedynym miejscem znającym stary świat, tłumaczy też dziwactwa danych z testem dla każdego, a przy wymianie starego systemu zmienia się tylko ACL. Zbiera złożoność w jednym, przetestowanym miejscu zamiast rozlewać ją po nowym kodzie.

Zobacz: sekcja „Ochrona przed starym modelem”.

</details>

### 31. Jak przenieść dane ze starego systemu do nowego (migracja jednorazowa, synchronizacja, podwójny zapis) i jak zweryfikować poprawność?

<details>
<summary>Odpowiedź</summary>

Migracja jednorazowa jest prosta, ale wymaga okna serwisowego i daje jedną szansę. Synchronizacja ciągła (zdarzenia, CDC, okresowy import) pozwala działać równolegle, a stary system pozostaje źródłem prawdy. Podwójny zapis jest najbardziej ryzykowny, bo bez wspólnej transakcji dane się rozjeżdżają, więc tylko z wykrywaniem rozbieżności albo przez outbox. Zwykle łączy się je: migracja historii, synchronizacja, parallel run, przełączenie źródła prawdy, wyłączenie. Poprawność weryfikuje codzienne uzgodnienie danych (liczby, sumy, próbki) z alertami, a przełączenie następuje po okresie bez rozbieżności, także w nietypowe dni.

Zobacz: sekcja „Przeniesienie danych”.

</details>
