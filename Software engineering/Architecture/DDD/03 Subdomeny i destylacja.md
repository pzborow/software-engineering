# Subdomeny i destylacja

Nie każda część systemu jest równie ważna. Wypożyczalnia zarabia na trafnej wycenie i dobrym wykorzystaniu floty, a nie na formularzu logowania. DDD każe to nazwać wprost i rozłożyć wysiłek zespołu zgodnie z tym, co daje firmie przewagę. Ten rozdział pokazuje, jak podzielić domenę na części, jak rozpoznać tę najważniejszą i jak ją chronić.

```text
                    domena: wynajem samochodów
┌──────────────────────────────┬──────────────────────────┬─────────────────────────┐
│ core                         │ supporting               │ generic                 │
│ dynamiczna wycena            │ zarządzanie flotą        │ płatności               │
│ planowanie wykorzystania     │ obsługa szkód            │ tożsamość i logowanie   │
│ floty                        │ program lojalnościowy    │ fakturowanie, e-maile   │
└──────────────────────────────┴──────────────────────────┴─────────────────────────┘
```

## Trzy rodzaje subdomen

Domenę dzieli się na mniejsze obszary. Każda <a id="term-subdomain"></a>[subdomena](00%20Glossary%20DDD.md#subdomain) to obszar działalności biznesu z własnymi problemami i ekspertami i należy do jednej z trzech kategorii.

<a id="term-core-domain"></a>[Core domain](00%20Glossary%20DDD.md#core-domain) to obszar, w którym firma wyróżnia się na tle konkurencji. Jest złożony, zmienia się często i nie da się go kupić, bo wtedy przestałby wyróżniać. W wypożyczalni jest to dynamiczna wycena (cena zależna od popytu, sezonu, obłożenia oddziału, historii klienta) i planowanie wykorzystania floty (gdzie przesunąć auta, kiedy je serwisować, kiedy sprzedać).

<a id="term-supporting-subdomain"></a>[Supporting subdomain](00%20Glossary%20DDD.md#supporting-subdomain) jest potrzebna do działania biznesu i specyficzna dla firmy, ale nie daje przewagi. Zwykle jest stosunkowo prosta. W wypożyczalni: ewidencja floty, obsługa szkód, program lojalnościowy.

<a id="term-generic-subdomain"></a>[Generic subdomain](00%20Glossary%20DDD.md#generic-subdomain) to problem rozwiązany wiele razy, taki sam w każdej firmie. Bywa złożony, ale nie wyróżnia. W wypożyczalni: płatności, logowanie i tożsamość, fakturowanie, wysyłka e-maili i SMS-ów.

| | Core | Supporting | Generic |
|---|---|---|---|
| Przewaga konkurencyjna | tak | nie | nie |
| Złożoność | wysoka | niska lub średnia | różna, często wysoka |
| Zmienność | częste zmiany | rzadkie | rzadkie |
| Specyficzna dla firmy | tak | tak | nie |
| Przykład w wypożyczalni | wycena, planowanie floty | szkody, flota | płatności, logowanie |

Ta sama funkcja może być różnie klasyfikowana w różnych firmach. Dla wypożyczalni płatności są generic. Dla firmy fintech, która na nich zarabia, są core. Klasyfikacja wynika ze strategii biznesu, a nie z natury problemu.

## Jak znaleźć rdzeń

Core domain nie wynika z architektury systemu, tylko z odpowiedzi na pytania biznesowe:

- Dlaczego klienci wybierają nas, a nie konkurencję?
- Co byśmy stracili, gdyby konkurent skopiował ten obszar?
- Na czym zarabiamy albo oszczędzamy więcej niż inni?
- Które reguły zmieniają się najczęściej, bo eksperymentujemy?
- Gdzie zarząd chce inwestować w najbliższych latach?

Odpowiedzi muszą dać ludzie odpowiedzialni za strategię, a nie zespół techniczny. Programiści często mylą core domain z najtrudniejszą technicznie częścią systemu. Integracja z systemem księgowym może być najbardziej skomplikowana w kodzie, a mimo to generic.

Klasyfikacja zmienia się w czasie. Wypożyczalnia może zdecydować, że program lojalnościowy stanie się głównym wyróżnikiem, i wtedy przesunie się on z supporting do core. Dlatego mapę subdomen warto przeglądać przy każdej większej zmianie strategii.

## Gdzie kierować wysiłek

Podział na subdomeny przekłada się na konkretne decyzje:

| Decyzja | Core | Supporting | Generic |
|---|---|---|---|
| Build vs buy | zawsze budować samodzielnie | budować prosto albo zlecić | kupić, SaaS, open source |
| Zespół | najlepsi ludzie, stały zespół | zespół mniej doświadczony, outsourcing | integracja przez niewielki zespół |
| Podejście | pełne DDD, bogaty model, eksperymenty | prosta architektura, transaction script, CRUD | adapter do gotowego rozwiązania |
| Jakość kodu | najwyższa, testy, refaktoryzacja modelu | wystarczająca | minimalna warstwa integracji |
| Czas ekspertów | dużo, stała współpraca | okazjonalnie | prawie wcale |

```python
# generic: płatności przez gotowe API, cienki adapter
class StripePayments:
    def charge_deposit(self, customer_id: str, amount: Money) -> PaymentRef: ...


# supporting: ewidencja floty jako prosty CRUD, bez agregatów i zdarzeń
class VehicleRegistry:
    def register(self, vin: str, model: str, branch_id: str) -> None: ...


# core: bogaty model wyceny, reguły, value objects, testy z ekspertem
class DynamicPricing:
    def quote(self, request: QuoteRequest, demand: DemandForecast) -> Quote: ...
```

Najczęstszy błąd to równomierne rozłożenie wysiłku: zespół buduje własny system płatności z pełnym DDD, a wycenę implementuje jako tabelę stawek w arkuszu. Drugi błąd to kupienie gotowego rozwiązania dla core domain. Jeśli wycena pochodzi z pudełkowego systemu, konkurent może kupić ten sam system.

## Problem i rozwiązanie

Subdomena opisuje <a id="term-problem-space"></a>[przestrzeń problemu](00%20Glossary%20DDD.md#problem-space): jaki obszar biznesu istnieje, niezależnie od oprogramowania. <a id="term-bounded-context"></a>[Bounded context](00%20Glossary%20DDD.md#bounded-context) należy do <a id="term-solution-space"></a>[przestrzeni rozwiązania](00%20Glossary%20DDD.md#solution-space): to granica, w której obowiązuje jeden model i jeden język w oprogramowaniu. Rozdział 04 opisuje konteksty szczegółowo.

Idealnie jedna subdomena odpowiada jednemu kontekstowi, ale nie jest to wymóg:

| Relacja | Przykład | Kiedy sensowna |
|---|---|---|
| 1 subdomena : 1 kontekst | wycena w kontekście `Pricing` | domyślny, najprostszy przypadek |
| 1 subdomena : wiele kontekstów | szkody podzielone na `ClaimsIntake` i `ClaimsSettlement` | subdomena duża, różne języki w jej częściach |
| wiele subdomen : 1 kontekst | flota i serwis w jednym kontekście `FleetOps` | subdomeny małe, jeden zespół, wspólny język |
| subdomena rozlana po kontekstach | reguły wyceny w rezerwacjach, rozliczeniach i ofertach | objaw problemu, do naprawy |

Ostatni przypadek jest częsty w systemach bez świadomego projektowania strategicznego: reguły core domain są rozrzucone po wielu modułach, więc nikt nie może ich spójnie zmienić.

## Wydobywanie rdzenia

W dużym systemie core domain ginie wśród kodu pomocniczego. Evans nazywa proces jej wyodrębniania <a id="term-distillation"></a>[destylacją](00%20Glossary%20DDD.md#distillation): tak jak destylacja oddziela esencję od reszty, tak tutaj oddziela się rdzeń od mechanizmów pomocniczych. Techniki destylacji:

- <a id="term-domain-vision-statement"></a>[domain vision statement](00%20Glossary%20DDD.md#domain-vision-statement): krótki opis (strona tekstu), czym jest core domain i jaką wartość daje. Dla wypożyczalni: „Wyceniamy każdy najem tak, żeby maksymalizować przychód z floty przy zachowaniu przewidywalnej ceny dla stałych klientów”. Pomaga ustalić, co jest w rdzeniu, a co nie,
- highlighted core: dokument lub oznaczenie w kodzie wskazujące, które moduły i klasy tworzą rdzeń, żeby nowe osoby wiedziały, gdzie jest to, co najważniejsze,
- cohesive mechanisms: wydzielenie złożonych, ale ogólnych mechanizmów (np. solver optymalizacji, silnik reguł) do osobnych modułów z czytelnym interfejsem, żeby rdzeń opisywał „co”, a nie „jak”,
- <a id="term-segregated-core"></a>[segregated core](00%20Glossary%20DDD.md#segregated-core): przeniesienie elementów rdzenia do osobnego modułu i usunięcie z niego wszystkiego, co pomocnicze, nawet kosztem pewnej duplikacji,
- abstract core: wyodrębnienie najważniejszych abstrakcji rdzenia do osobnego modułu, gdy rdzeń jest tak duży, że nawet po segregacji trudno go ogarnąć.

```text
przed destylacją                      po destylacji
pricing/                              pricing_core/          ← segregated core
├── models.py        (200 klas)       ├── quote.py            Quote, PriceComponent
├── utils.py                          ├── rules.py            PricingRule, DemandRule, LoyaltyRule
├── optimizer.py                      └── policy.py           PricingPolicy
├── reports.py                        pricing_mechanisms/     ← cohesive mechanisms
└── integrations.py                   └── demand_forecast.py  model prognozy, osobny interfejs
                                      pricing_support/
                                      └── reports.py, integrations.py
```

Destylacja jest inwestycją w czytelność i szybkość zmian w rdzeniu. Robi się ją stopniowo, zaczynając od domain vision statement, który nic nie kosztuje, a porządkuje dyskusje.

## Co zapamiętać

- Subdomeny dzielą się na core (przewaga), supporting (potrzebne, specyficzne, proste) i generic (rozwiązane wszędzie tak samo).
- Klasyfikacja wynika ze strategii biznesu, a nie z trudności technicznej, i zmienia się w czasie.
- Core buduje się samodzielnie z najlepszym zespołem i pełnym DDD. Generic kupuje się i integruje cienkim adapterem.
- Subdomena to przestrzeń problemu, a bounded context to przestrzeń rozwiązania. Relacja 1:1 jest idealna, ale nie obowiązkowa.
- Reguły rdzenia rozlane po wielu kontekstach to problem do naprawy.
- Destylacja wydobywa rdzeń: domain vision statement, highlighted core, cohesive mechanisms, segregated core, abstract core.

## Pytania sprawdzające

### 9. Czym różnią się core domain, supporting subdomain i generic subdomain? Podaj przykłady dla konkretnego biznesu.

<details>
<summary>Odpowiedź</summary>

Core domain daje przewagę konkurencyjną, jest złożona, zmienna i specyficzna dla firmy. W wypożyczalni to dynamiczna wycena i planowanie wykorzystania floty. Supporting subdomain jest potrzebna i specyficzna, ale nie wyróżnia i zwykle jest prosta: ewidencja floty, obsługa szkód, program lojalnościowy. Generic subdomain to problem rozwiązany wszędzie tak samo: płatności, logowanie, fakturowanie, e-maile. Ta sama funkcja może mieć inną kategorię w innej firmie, np. płatności są core w fintechu.

Zobacz: sekcja „Trzy rodzaje subdomen”.

</details>

### 10. Jak zidentyfikować core domain i dlaczego to decyzja biznesowa, a nie techniczna?

<details>
<summary>Odpowiedź</summary>

Przez pytania: dlaczego klienci wybierają nas, co stracimy, jeśli konkurent to skopiuje, na czym zarabiamy więcej niż inni, gdzie eksperymentujemy, gdzie chce inwestować zarząd. To decyzja biznesowa, bo wynika ze strategii firmy, a programiści często mylą core z tym, co najtrudniejsze technicznie (np. integracja z księgowością jest trudna, ale generic). Klasyfikację przegląda się przy zmianach strategii.

Zobacz: sekcja „Jak znaleźć rdzeń”.

</details>

### 11. Jak podział na subdomeny wpływa na decyzje build vs buy, dobór zespołu i jakość kodu w każdej z nich?

<details>
<summary>Odpowiedź</summary>

Core: zawsze budować samodzielnie, najlepszy stały zespół, pełne DDD, najwyższa jakość, stała współpraca z ekspertami. Supporting: budować prosto (CRUD, transaction script) albo zlecić, zespół mniej doświadczony lub outsourcing, jakość wystarczająca. Generic: kupić (SaaS, open source) i zintegrować cienkim adapterem. Błędy to równy podział wysiłku (własny system płatności, a wycena w arkuszu) oraz kupowanie gotowca dla core domain.

Zobacz: sekcja „Gdzie kierować wysiłek”.

</details>

### 12. Czym różni się subdomena (przestrzeń problemu) od bounded contextu (przestrzeń rozwiązania)? Czy muszą się pokrywać 1:1?

<details>
<summary>Odpowiedź</summary>

Subdomena to obszar biznesu istniejący niezależnie od oprogramowania, a bounded context to granica w oprogramowaniu, w której obowiązuje jeden model i język. Relacja 1:1 jest idealna, ale nie obowiązkowa. Dużą subdomenę można podzielić na kilka kontekstów, a kilka małych subdomen jednego zespołu może dzielić jeden kontekst. Problemem jest subdomena rozlana po wielu kontekstach, np. reguły wyceny w rezerwacjach, rozliczeniach i ofertach.

Zobacz: sekcja „Problem i rozwiązanie”.

</details>

### 13. Czym jest destylacja domeny (domain vision statement, highlighted core, segregated core) i po co się ją robi?

<details>
<summary>Odpowiedź</summary>

To wyodrębnianie core domain z kodu pomocniczego, żeby była czytelna i łatwa do zmiany. Domain vision statement to krótki opis wartości rdzenia. Highlighted core wskazuje, które moduły tworzą rdzeń. Cohesive mechanisms wydzielają ogólne mechanizmy (solver, silnik reguł). Segregated core przenosi rdzeń do osobnego modułu bez elementów pomocniczych. Abstract core wyodrębnia najważniejsze abstrakcje. Robi się ją stopniowo, zaczynając od taniego vision statement.

Zobacz: sekcja „Wydobywanie rdzenia”.

</details>
