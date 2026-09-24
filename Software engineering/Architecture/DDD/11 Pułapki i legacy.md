# Pułapki i legacy

DDD rzadko zaczyna się od czystej kartki. Zwykle zespół ma działający system z latami historii, ograniczony dostęp do ekspertów i presję na nowe funkcje. Ten rozdział opisuje najczęstsze problemy we wdrażaniu DDD i sposób, w jaki Eric Evans proponuje wprowadzać je do starego systemu bez przepisywania go.

## Model bez zachowań

<a id="term-anemic-domain-model"></a>[Anemiczny model domeny](00%20Glossary%20DDD.md#anemic-domain-model) to określenie Martina Fowlera z 2003 roku. Oznacza model, w którym klasy domeny mają tylko dane (gettery i settery), a cała logika jest w serwisach. Wygląda jak model obiektowy, ale działa jak procedury operujące na strukturach danych.

```python
# anemiczny: RentalAgreement to worek na dane
class RentalAgreementService:
    def extend(self, agreement_id: str, new_end: datetime) -> None:
        a = self._repo.get(agreement_id)
        if a.returned_at is not None:
            raise ValueError("...")
        if len(a.extensions) >= 3:
            raise ValueError("...")
        a.extensions.append({"from": a.end, "to": new_end})
        a.end = new_end                       # każdy może ustawić dowolną datę
        self._repo.save(a)


# bogaty: umowa pilnuje własnych reguł
agreement.extend(new_end, availability)
```

Anemia jest problemem, bo reguły nie mają jednego domu. Ta sama walidacja pojawia się w kilku serwisach, każdy może zmienić stan z pominięciem reguł, a model nie mówi językiem domeny.

Czy anemiczny model jest zawsze błędem? Nie. W supporting i generic subdomains, gdzie logika jest prosta, właściwym wzorcem jest często <a id="term-transaction-script"></a>[transaction script](00%20Glossary%20DDD.md#transaction-script): procedura obsługująca jedno żądanie od początku do końca, na prostych strukturach danych. Jest czytelny, szybki do napisania i wystarczający, gdy nie ma niezmienników do pilnowania. Anemiczny model jest błędem tam, gdzie domena jest złożona, czyli przede wszystkim w core domain, a także tam, gdzie zespół udaje, że stosuje DDD, a w praktyce pisze transaction scripts ukryte za encjami i repozytoriami.

## Bez dostępu do ekspertów

DDD zakłada współpracę z ekspertami. Co zrobić, gdy ich nie ma albo biznes nie chce uczestniczyć w modelowaniu?

Najpierw warto sprawdzić, czy problem jest prawdziwy. Często eksperci istnieją, tylko nikt ich nie zaprosił albo spotkania były nudne i abstrakcyjne. Pomagają:

- krótkie, konkretne sesje o prawdziwych przypadkach zamiast długich spotkań wymagań,
- Event Storming albo Domain Storytelling zamiast dokumentów do przeczytania, bo są angażujące i szybko dają widoczny wynik,
- pokazanie ekspertowi działającego kodu i testów w jego języku, dzięki czemu widzi, że jego czas ma wpływ,
- rozmowa z osobami, które wykonują pracę (pracownicy oddziałów, likwidatorzy), a nie tylko z kierownikami.

Jeśli eksperci naprawdę są niedostępni, zespół może szukać innych źródeł wiedzy:

- użytkownicy systemu i zgłoszenia do supportu,
- dokumenty biznesowe: regulaminy, umowy, cenniki, procedury, przepisy,
- dane produkcyjne i logi, które pokazują, jak system jest używany, w tym obejścia stosowane przez użytkowników,
- istniejący kod legacy, traktowany ostrożnie, bo zawiera zarówno reguły, jak i błędy,
- osoby w zespole, które stają się ekspertami przez naukę domeny.

Brak dostępu do ekspertów to też sygnał strategiczny. Jeśli biznes nie chce inwestować czasu w obszar, to prawdopodobnie nie jest on dla niego core domain. Warto wtedy zapytać, czy pełne DDD jest tu uzasadnione, czy wystarczy prostsze podejście.

## DDD w istniejącym bałaganie

Evans w tekście „Getting Started with DDD When Surrounded by Legacy Systems” (2013) opisuje strategie wprowadzania DDD do Big Ball of Mud bez przepisywania systemu.

<a id="term-bubble-context"></a>[Bubble context](00%20Glossary%20DDD.md#bubble-context) to mały, nowy bounded context z czystym modelem, zbudowany dla jednej konkretnej funkcji i odizolowany od legacy przez ACL. Nie ma własnej bazy. Czyta i zapisuje dane legacy, tłumacząc je w warstwie ochronnej. Jest tani na start i pozwala zespołowi nauczyć się DDD na małym, realnym problemie.

```text
┌──────────── Big Ball of Mud ────────────┐
│  tabele POJAZDY, UMOWY, KLIENCI, ...    │
│  procedury składowane, raporty          │
└───────────────────┬─────────────────────┘
                    │ ACL (odczyt i zapis w obie strony)
            ┌───────▼─────────┐
            │ bubble: Pricing │  czysty model wyceny, testy, język ekspertów
            └─────────────────┘
```

<a id="term-autonomous-bubble"></a>[Autonomous bubble](00%20Glossary%20DDD.md#autonomous-bubble) to dojrzalsza wersja: kontekst ma własną bazę i własny model danych, a z legacy synchronizuje się asynchronicznie, zwykle przez ACL i zdarzenia lub okresowy import. Działa nawet wtedy, gdy legacy jest niedostępne. Jest droższy, ale daje prawdziwą niezależność i jest krokiem w stronę wydzielenia kontekstu na stałe.

Z czasem kolejne funkcje przechodzą do nowych kontekstów, a legacy się kurczy. To <a id="term-strangler-fig"></a>[strangler fig](00%20Glossary%20DDD.md#strangler-fig), wzorzec Martina Fowlera nazwany od figowca dusiciela, który obrasta stare drzewo, aż je zastąpi.

Kolejność kroków:

1. Wybierz jedną wartościową, często zmienianą funkcję z core domain. Wycena jest dobrym kandydatem, bo jej zmiana przynosi zyski, a obecny kod jest trudny do zmiany.
2. Zbuduj bubble context z czystym modelem i <a id="term-anti-corruption-layer"></a>[anti-corruption layer](00%20Glossary%20DDD.md#anti-corruption-layer) do legacy.
3. Przełącz wywołania tej funkcji na nowy kontekst. Legacy nadal istnieje, ale ta funkcja już go nie używa.
4. Gdy kontekst się sprawdzi, przekształć go w autonomous bubble z własnymi danymi.
5. Powtarzaj dla kolejnych funkcji, zaczynając od tych, które dają największą wartość.

Najważniejsza zasada: nowy kontekst nie może wpuścić do siebie modelu legacy. Każde pojęcie z legacy przechodzi przez ACL, inaczej bałagan rozleje się do nowego kodu.

## Najczęstsze błędy

| Błąd | Objaw | Skutek | Naprawa |
|---|---|---|---|
| wzorce bez języka | encje i repozytoria z nazwami technicznymi | model nie odpowiada biznesowi | knowledge crunching, słownik per kontekst |
| jeden model dla wszystkiego | `Customer` z sześćdziesięcioma polami | każda zmiana blokuje innych | bounded contexts |
| agregaty jako tabele | agregat na każdą tabelę, relacje obiektowe między nimi | konflikty, transakcje przez pół systemu | agregaty według niezmienników, referencje przez ID |
| nadmierna abstrakcja | interfejsy, fabryki i serwisy dla prostych rzeczy | powolny rozwój, trudny kod | pełne DDD tylko w core, prostota w supporting i generic |
| DDD wszędzie | pełny zestaw wzorców w CRUD-owym panelu | koszt bez korzyści | klasyfikacja subdomen |
| brak ekspertów | model wymyślony przez programistów | trafne technicznie, błędne biznesowo | warsztaty, inne źródła wiedzy, pytanie o strategię |
| granice według technologii | kontekst „baza”, kontekst „API”, serwis per encja | rozproszony monolit | granice według języka i procesu |
| przepisywanie od zera | projekt „nowy system” na dwa lata | ryzyko, brak wartości po drodze | bubble context, strangler fig |

Wspólny mianownik większości tych błędów to traktowanie DDD jako zestawu wzorców technicznych zamiast sposobu myślenia o domenie. Wzorce są ważne, ale bez języka, granic i świadomych decyzji strategicznych dają dużo kodu i mało korzyści.

## Co zapamiętać

- Anemiczny model to dane bez zachowań. Jest błędem w złożonej domenie, a w prostej wystarcza transaction script.
- Brak ekspertów często da się naprawić lepszą formą współpracy. Pomagają też inne źródła wiedzy i pytanie, czy to na pewno core domain.
- Bubble context to mały, czysty kontekst przy legacy, połączony z nim przez ACL i bez własnej bazy.
- Autonomous bubble ma własne dane i synchronizuje się z legacy asynchronicznie.
- Strangler fig stopniowo przenosi funkcje z legacy do nowych kontekstów, zaczynając od najwartościowszych.
- Model legacy nie może przeciekać do nowych kontekstów, a wszystko przechodzi przez ACL.
- Większość błędów wynika z traktowania DDD jako zestawu wzorców zamiast sposobu modelowania.

## Pytania sprawdzające

### 48. Czym jest anemiczny model domeny i czy zawsze jest błędem?

<details>
<summary>Odpowiedź</summary>

To termin Martina Fowlera na model, w którym klasy domeny mają tylko dane, a logika jest w serwisach. Reguły nie mają jednego domu, walidacja się powtarza, a stan można zmienić z pominięciem reguł. Nie zawsze jest błędem: w supporting i generic subdomains z prostą logiką właściwy bywa transaction script. Błędem jest w złożonej domenie, zwłaszcza w core, i tam, gdzie transaction scripts ukrywa się za encjami i repozytoriami, udając DDD.

Zobacz: sekcja „Model bez zachowań”.

</details>

### 49. Co zrobić, gdy nie ma dostępu do ekspertów domenowych albo biznes nie chce uczestniczyć w modelowaniu?

<details>
<summary>Odpowiedź</summary>

Najpierw sprawdzić, czy problem jest prawdziwy: krótkie sesje o konkretnych przypadkach, Event Storming lub Domain Storytelling zamiast dokumentów, pokazywanie działającego kodu w języku eksperta, rozmowy z osobami wykonującymi pracę. Gdy eksperci naprawdę są niedostępni: użytkownicy i zgłoszenia, dokumenty biznesowe i przepisy, dane i logi produkcyjne, ostrożnie kod legacy i członkowie zespołu, którzy uczą się domeny. Brak zaangażowania biznesu to też sygnał, że obszar może nie być core domain.

Zobacz: sekcja „Bez dostępu do ekspertów”.

</details>

### 50. Jak wprowadzać DDD do Big Ball of Mud (bubble context, autonomous bubble, ACL, strangler)?

<details>
<summary>Odpowiedź</summary>

Według Evansa (2013): zacząć od bubble context, czyli małego, czystego kontekstu dla jednej wartościowej funkcji z core, bez własnej bazy, z dostępem do legacy wyłącznie przez ACL. Przełączyć tę funkcję na nowy kontekst. Po sprawdzeniu przekształcić go w autonomous bubble z własnymi danymi, synchronizowany z legacy asynchronicznie. Powtarzać dla kolejnych funkcji według wartości, co jest strangler fig. Najważniejsze: model legacy nigdy nie przecieka do nowych kontekstów.

Zobacz: sekcja „DDD w istniejącym bałaganie”.

</details>

### 51. Jakie są najczęstsze błędy zespołów wdrażających DDD (wzorce bez języka, jeden model dla wszystkiego, agregaty jako tabele, nadmierna abstrakcja)?

<details>
<summary>Odpowiedź</summary>

Wzorce bez języka, czyli techniczne nazwy i model niezgodny z biznesem. Jeden model dla wszystkich działów, czyli przeładowane klasy i blokowanie się zespołów. Agregaty jako tabele z relacjami obiektowymi, czyli konflikty i transakcje przez pół systemu. Nadmierna abstrakcja i DDD wszędzie, także w CRUD-zie. Model wymyślony bez ekspertów. Granice według technologii zamiast języka i procesu. Przepisywanie od zera zamiast bubble context i strangler fig. Wspólna przyczyna to traktowanie DDD jako zestawu wzorców zamiast sposobu modelowania.

Zobacz: sekcja „Najczęstsze błędy”.

</details>
