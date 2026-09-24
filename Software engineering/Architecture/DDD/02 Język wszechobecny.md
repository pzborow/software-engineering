# Język wszechobecny

Model domeny nie powstaje w głowie architekta. Powstaje w rozmowach z ludźmi, którzy znają biznes, i żyje we wspólnym słowniku używanym przez wszystkich: w spotkaniach, w historyjkach użytkownika, w testach i w kodzie. Ten rozdział opisuje, jak ten słownik budować, pilnować i poprawiać.

```text
ekspert: „Klient może przedłużyć najem, jeśli auto nie jest zarezerwowane na kolejny termin.”
                                      │
                                      ▼
kod:     agreement.extend(new_return_date, fleet_schedule)
test:    test_extension_refused_when_car_reserved_for_next_period()
UI:      przycisk „Przedłuż najem”
```

## Jeden język dla wszystkich

<a id="term-ubiquitous-language"></a>[Ubiquitous language](00%20Glossary%20DDD.md#ubiquitous-language) (język wszechobecny) to wspólny, precyzyjny słownik zespołu i biznesu, używany wszędzie: w rozmowach, dokumentach, testach i kodzie. „Wszechobecny” nie oznacza „w całej firmie”, tylko „wszędzie w obrębie jednego modelu”. Rozdział 04 pokazuje, dlaczego każdy kontekst ma własny język.

Język musi być widoczny w kodzie, bo kod jest jedynym artefaktem, który na pewno odpowiada działaniu systemu. Dokumentacja się starzeje, a kod nie może kłamać. Jeśli w kodzie jest `BookingRecord.setStatus(3)`, a biznes mówi „potwierdzenie rezerwacji”, każda rozmowa wymaga tłumaczenia, a każde tłumaczenie to miejsce na błąd.

```python
# kod bez języka: programista musi pamiętać, co znaczy status 3
booking.status = 3
booking.amount = calc(booking, 0.85)
repo.update(booking)

# kod w języku domeny
reservation.confirm(deposit=Money("300.00", "PLN"))
quote = pricing.quote(vehicle_class, rental_period, loyalty_tier=GOLD)
```

Konsekwencje dla kodu:

- nazwy klas, metod, zdarzeń i wyjątków pochodzą z języka ekspertów, a nie z żargonu technicznego (`RentalAgreement`, a nie `ContractEntity`),
- metody wyrażają operacje biznesowe (`extend`, `close_with_damage`), a nie operacje na danych (`update`, `set_status`),
- zmiana słowa w rozmowie, np. z „kaucja” na „depozyt”, oznacza zmianę w kodzie. Jeśli zespół tego nie robi, język zaczyna się rozjeżdżać,
- testy akceptacyjne mogą być czytane przez ekspertów, bo używają ich słów.

## Wydobywanie wiedzy od ekspertów

<a id="term-domain-expert"></a>[Ekspert domenowy](00%20Glossary%20DDD.md#domain-expert) to osoba, która zna dziedzinę z praktyki: kierownik oddziału wypożyczalni, likwidator szkód, analityk cenowy. Nie musi znać się na oprogramowaniu i nie powinien projektować systemu. Jego rola to wyjaśniać, jak działa biznes, i weryfikować model.

Evans nazywa proces wspólnego budowania modelu <a id="term-knowledge-crunching"></a>[knowledge crunching](00%20Glossary%20DDD.md#knowledge-crunching). To iteracyjne „przeżuwanie” wiedzy: zespół słucha, zadaje pytania, proponuje model, sprawdza go na przykładach i poprawia. W praktyce wygląda to tak:

1. Rozmowa o konkretnych przypadkach, a nie o ogólnikach. „Opowiedz o ostatniej reklamacji szkody” działa lepiej niż „jak działają reklamacje”.
2. Szkic modelu na tablicy: pojęcia, relacje, reguły.
3. Sprawdzenie modelu na przykładach, zwłaszcza brzegowych. „Co, jeśli klient odda auto w innym oddziale? A jeśli w niedzielę? A jeśli z pełnym bakiem, choć płacił za pusty?”
4. Uwaga na zdziwienia i zawahania eksperta: „to zależy”, „zazwyczaj”, „oprócz przypadków, kiedy...”. Tam kryją się ukryte pojęcia.
5. Kod jako eksperyment: prototyp modelu z testami, który pokazuje ekspertowi, co zespół zrozumiał.
6. Powrót do rozmowy z nowymi pytaniami.

```python
# test jako pytanie do eksperta: czy to prawda?
def test_one_way_rental_adds_relocation_fee():
    agreement = rental_agreement(pickup="Warszawa", planned_return="Warszawa")
    settlement = agreement.close(returned_at="Kraków", fuel=FULL, mileage=412)
    assert settlement.fees == [RelocationFee(branch_from="Warszawa", branch_to="Kraków")]
```

Knowledge crunching nie kończy się po analizie wymagań. Trwa przez całe życie systemu, bo biznes się zmienia, a zespół rozumie go coraz lepiej.

## Jedno słowo, wiele znaczeń

W wypożyczalni słowo „klient” znaczy co innego w różnych działach:

| Dział | „Klient” oznacza | Co go interesuje |
|---|---|---|
| Rezerwacje | osoba, która rezerwuje auto | termin, klasa auta, oddział |
| Wydanie auta | kierowca z prawem jazdy | ważność prawa jazdy, wiek, kaucja |
| Rozliczenia | płatnik, często firma | NIP, adres do faktury, termin płatności |
| Marketing | kontakt, lead | zgody, historia kampanii, segment |
| Szkody | sprawca albo poszkodowany | polisa, protokół, udział w winie |

Próba stworzenia jednej klasy `Customer` z polami dla wszystkich działów prowadzi do obiektu z sześćdziesięcioma polami, z których każdy dział używa kilku, a reguły jednego działu przeszkadzają innym. To sygnał, że te działy mówią różnymi językami i potrzebują różnych modeli.

Rozwiązanie DDD jest dwuetapowe:

- w obrębie jednego modelu słowo ma jedno, precyzyjne znaczenie. Jeśli „klient” w rezerwacjach okazuje się dwoma pojęciami, zespół je rozdziela (`Booker` i `Driver`) albo doprecyzowuje,
- różne znaczenia tego samego słowa żyją w różnych bounded contextach, każdy z własnym modelem i językiem. Między nimi zachodzi jawne tłumaczenie (rozdziały 04 i 05).

Pomocne jest prowadzenie słownika pojęć per kontekst, najlepiej w repozytorium obok kodu. Słownik zawiera definicję, przykłady, słowa zakazane lub mylące i powiązania z innymi pojęciami.

## Gdy model przestaje pasować

Model rozjeżdża się z biznesem powoli i niezauważenie. Sygnały ostrzegawcze:

- programiści w rozmowie z ekspertem tłumaczą swoje nazwy: „u nas to się nazywa `BookingRecord`, ale chodzi o rezerwację”,
- ekspert używa słowa, którego nie ma w kodzie („przedłużenie”, „odbiór jednokierunkowy”), a reguła jest ukryta w `if`-ach,
- nowe wymagania wymagają obejść: flag, warunków specjalnych, pól `type` z wartościami „inne”,
- ta sama reguła jest zaimplementowana w kilku miejscach, bo nie ma dla niej pojęcia w modelu,
- nazwy techniczne (`Manager`, `Helper`, `Processor`, `Data`) zastępują pojęcia biznesowe.

Evans opisuje odpowiedź na to jako <a id="term-deeper-insight"></a>[refaktoryzację w stronę głębszego wglądu](00%20Glossary%20DDD.md#deeper-insight) (refactoring toward deeper insight). Nie chodzi o refaktoryzację techniczną (wydzielanie metod), tylko o zmianę modelu, gdy zespół lepiej zrozumie domenę. Często zaczyna się od odkrycia ukrytego pojęcia:

```python
# przed: reguła ukryta w warunkach
def calculate_price(reservation):
    price = base_rate(reservation.vehicle_class) * reservation.days
    if reservation.pickup_branch != reservation.return_branch:
        price += 250
    if reservation.customer.age < 25:
        price *= 1.2
    if reservation.days >= 7:
        price *= 0.9
    return price


# po: ukryte pojęcie „składnik ceny” stało się jawną częścią modelu
@dataclass(frozen=True)
class PriceComponent:
    name: str               # „opłata za zwrot w innym oddziale”, „dopłata dla młodego kierowcy”
    amount: Money


def quote(reservation, rules: list[PricingRule]) -> Quote:
    components = [c for rule in rules if (c := rule.apply(reservation))]
    return Quote(components)             # klient i ekspert widzą, z czego składa się cena
```

Przełom w modelu zdarza się rzadko, ale zmienia sposób rozmowy o systemie. W przykładzie ekspert od cen zaczyna mówić o „regułach cenowych” i „składnikach ceny”. Nowe reguły dodaje się bez zmiany istniejącego kodu, a klient dostaje przejrzystą wycenę. Taka refaktoryzacja jest możliwa tylko wtedy, gdy kod jest pokryty testami i zespół ma czas na zmiany modelu, a nie tylko na nowe funkcje.

## Co zapamiętać

- Ubiquitous language to wspólny słownik zespołu i biznesu, używany wszędzie w obrębie jednego modelu, także w kodzie.
- Nazwy klas, metod, zdarzeń i testów pochodzą z języka ekspertów, a zmiana słowa w rozmowie oznacza zmianę w kodzie.
- Knowledge crunching to iteracyjne budowanie modelu na konkretnych przykładach, trwające przez całe życie systemu.
- Ekspert domenowy wyjaśnia i weryfikuje, ale nie projektuje systemu.
- To samo słowo w różnych działach oznacza różne pojęcia, które należą do różnych kontekstów.
- Rozjazd modelu z biznesem widać po tłumaczeniach, obejściach i nazwach technicznych.
- Refaktoryzacja w stronę głębszego wglądu zmienia model, często przez odkrycie ukrytego pojęcia.

## Pytania sprawdzające

### 5. Czym jest ubiquitous language i dlaczego musi być widoczny w kodzie, a nie tylko w dokumentacji?

<details>
<summary>Odpowiedź</summary>

To wspólny, precyzyjny słownik zespołu i biznesu, używany w rozmowach, dokumentach, testach i kodzie w obrębie jednego modelu. Musi być w kodzie, bo kod jest jedynym artefaktem, który na pewno odpowiada działaniu systemu, a dokumentacja się starzeje. Nazwy spoza języka wymuszają ciągłe tłumaczenie, a każde tłumaczenie jest źródłem błędów. W praktyce: nazwy z języka ekspertów, metody jako operacje biznesowe, zmiana słowa w rozmowie oznacza zmianę w kodzie.

Zobacz: sekcja „Jeden język dla wszystkich”.

</details>

### 6. Czym jest knowledge crunching i jak wygląda praca z ekspertem domenowym w praktyce?

<details>
<summary>Odpowiedź</summary>

To iteracyjny proces wspólnego budowania modelu z ekspertem. Zespół rozmawia o konkretnych przypadkach, szkicuje model, sprawdza go na przykładach brzegowych, wyłapuje zawahania eksperta („to zależy”, „zazwyczaj”), w których kryją się ukryte pojęcia, a kod i testy traktuje jako eksperyment do weryfikacji z ekspertem. Ekspert wyjaśnia i weryfikuje, ale nie projektuje systemu. Proces trwa przez całe życie systemu.

Zobacz: sekcja „Wydobywanie wiedzy od ekspertów”.

</details>

### 7. Co zrobić, gdy to samo słowo znaczy co innego w różnych działach firmy (np. „klient”, „zamówienie”, „produkt”)?

<details>
<summary>Odpowiedź</summary>

Nie budować jednej klasy dla wszystkich znaczeń, bo powstaje przeładowany obiekt, w którym reguły działów sobie przeszkadzają. W obrębie jednego modelu słowo musi mieć jedno znaczenie, więc jeśli kryje dwa pojęcia, należy je rozdzielić (np. `Booker` i `Driver`). Różne znaczenia żyją w różnych bounded contextach z własnymi modelami i jawnym tłumaczeniem między nimi. Pomaga słownik pojęć per kontekst trzymany przy kodzie.

Zobacz: sekcja „Jedno słowo, wiele znaczeń”.

</details>

### 8. Jak rozpoznać, że model rozjechał się z językiem biznesu, i jak go przywrócić (refaktoryzacja w stronę głębszego wglądu)?

<details>
<summary>Odpowiedź</summary>

Sygnały: tłumaczenie nazw w rozmowie z ekspertem, słowa eksperta nieobecne w kodzie, obejścia przez flagi i pola „inne”, ta sama reguła w wielu miejscach, nazwy techniczne typu `Manager` czy `Helper`. Naprawą jest refaktoryzacja w stronę głębszego wglądu: zmiana modelu po lepszym zrozumieniu domeny, często przez uczynienie ukrytego pojęcia jawnym (np. składnik ceny i reguła cenowa zamiast zagnieżdżonych `if`-ów). Wymaga testów i czasu na zmiany modelu.

Zobacz: sekcja „Gdy model przestaje pasować”.

</details>
