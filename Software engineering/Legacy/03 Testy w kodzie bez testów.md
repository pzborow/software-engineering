# Testy w kodzie bez testów

Zmiana kodu bez testów to zgadywanie. Problem w tym, że kod legacy zwykle nie jest napisany tak, żeby dało się go testować. Funkcja `generate_invoice` łączy się z bazą, woła KSeF, wysyła e-mail i zależy od bieżącej daty. Ten rozdział pokazuje, jak mimo to objąć ją testami, zanim cokolwiek się w niej zmieni.

```text
zwykły test:            „kod powinien robić X”       specyfikacja, pisana przed kodem
test charakteryzujący:  „kod teraz robi X”           fotografia, pisana po kodzie

cel: siatka bezpieczeństwa, która krzyknie, gdy zmiana przypadkiem zmieni zachowanie
```

## Fotografia zachowania

<a id="term-characterization-test"></a>[Test charakteryzujący](00%20Glossary%20Legacy.md#characterization-test) to pojęcie Feathersa: test, który opisuje, co kod robi teraz, a nie co powinien robić. Nie weryfikuje poprawności, tylko zamraża obecne zachowanie, żeby każda zmiana była widoczna.

Procedura pisania jest odwrotna niż w zwykłym teście:

1. Wywołaj kod z konkretnymi danymi.
2. Wpisz w asercji wartość, o której wiesz, że jest zła, np. `0`.
3. Uruchom test i odczytaj z komunikatu błędu, co kod faktycznie zwrócił.
4. Wpisz tę wartość do asercji. Test przechodzi i opisuje obecne zachowanie.
5. Powtarzaj dla kolejnych przypadków, zwłaszcza tych, które wyglądają dziwnie.

```python
def test_books_have_5_percent_vat():
    total = invoice_total_for(items=[item("books", price=100, qty=1)], customer=pl_consumer())
    assert total == 0                 # celowo źle
# AssertionError: assert 105.0 == 0   ← kod liczy 105.0


def test_books_have_5_percent_vat():
    total = invoice_total_for(items=[item("books", price=100, qty=1)], customer=pl_consumer())
    assert total == 105.0             # zachowanie zamrożone
```

Test charakteryzujący różni się od zwykłego testu jednostkowego:

| | Zwykły test | Test charakteryzujący |
|---|---|---|
| Źródło oczekiwanej wartości | specyfikacja, wymagania | obecny wynik kodu |
| Pisany | przed kodem albo razem z nim | po kodzie |
| Nieudany test oznacza | błąd w kodzie | zmianę zachowania, niekoniecznie błąd |
| Cel | potwierdzić poprawność | wykryć każdą zmianę |
| Nazwa | opisuje wymaganie | opisuje zaobserwowane zachowanie |

## Nagranie całego wyniku

Gdy funkcja jest duża, a przypadków dużo, pisanie asercji ręcznie jest za wolne. <a id="term-golden-master"></a>[Golden master](00%20Glossary%20Legacy.md#golden-master) polega na tym, żeby uruchomić kod dla wielu kombinacji danych, zapisać cały wynik do pliku i od tej pory porównywać każde uruchomienie z tym zapisem.

```python
# tests/test_invoice_golden_master.py
import itertools
import json
from pathlib import Path

CATEGORIES = ["books", "food", "electronics"]
COUNTRIES = ["PL", "DE", "US"]
TYPES = ["B2C", "B2B"]
COUPONS = [None, "BLACKFRIDAY"]
MONTHS = [3, 11]

MASTER = Path(__file__).parent / "golden" / "invoice_totals.json"


def run_all_cases() -> dict:
    results = {}
    for cat, country, ctype, coupon, month in itertools.product(CATEGORIES, COUNTRIES, TYPES, COUPONS, MONTHS):
        key = f"{cat}|{country}|{ctype}|{coupon}|{month}"
        results[key] = invoice_total_for(
            items=[item(cat, price=100, qty=2)],
            customer=customer(country=country, type=ctype),
            coupon=coupon,
            today=f"2026-{month:02d}-15",
        )
    return results


def test_invoice_totals_match_golden_master():
    actual = run_all_cases()
    if not MASTER.exists():                                   # pierwsze uruchomienie: nagranie
        MASTER.parent.mkdir(exist_ok=True)
        MASTER.write_text(json.dumps(actual, indent=2, sort_keys=True))
    expected = json.loads(MASTER.read_text())
    assert actual == expected
```

72 kombinacje (3 × 3 × 2 × 2 × 2) dają siatkę bezpieczeństwa w kilka minut pracy. Plik `invoice_totals.json` trafia do repozytorium, a każda zmiana w nim jest widoczna w code review.

<a id="term-approval-testing"></a>[Approval testing](00%20Glossary%20Legacy.md#approval-testing) to uogólnienie tej techniki z narzędziami do zatwierdzania zmian. Biblioteka `approvaltests` (dostępna w Pythonie, Javie, .NET i innych językach) zapisuje wynik jako plik `.received`, porównuje z `.approved` i przy różnicy otwiera narzędzie diff. Programista świadomie akceptuje nowy wynik albo poprawia kod.

```python
from approvaltests import verify


def test_invoice_pdf_text():
    pdf_text = render_pdf_text(sample_invoice())
    verify(pdf_text)            # porównuje z test_invoice_pdf_text.approved.txt
```

Approval testing dobrze sprawdza się dla dużych, strukturalnych wyników: PDF-ów, e-maili, raportów, odpowiedzi JSON, eksportów CSV. Pułapką są dane zmienne: daty, numery, UUID. Trzeba je ustalić w teście albo zamaskować przed porównaniem (`scrubber` w `approvaltests`).

## Gdy test ujawni błąd

Test charakteryzujący zamraża zachowanie, także błędne. W przykładzie golden master pokazuje, że kupon `BLACKFRIDAY` daje rabat w każdym listopadzie, a nie tylko w 2019 roku, jak ustalono w rozdziale 02. Co z tym zrobić?

Zasada: nie poprawiaj błędu w tym samym kroku, w którym piszesz testy charakteryzujące. Powody:

- klienci lub inne systemy mogą polegać na obecnym zachowaniu, nawet błędnym. Raport marketingu może zakładać, że rabat co roku działa,
- poprawka to zmiana zachowania, która wymaga decyzji biznesowej, a test charakteryzujący to czynność techniczna,
- połączenie obu rzeczy sprawia, że w code review nie widać, co jest refaktoryzacją, a co zmianą.

Postępowanie:

```python
def test_blackfriday_coupon_applies_every_november__suspected_bug_INV_231():
    # Zachowanie zamrożone. Zgłoszone jako INV-231: kupon miał działać tylko w 2019.
    total = invoice_total_for(items=[item("electronics", 100, 1)], customer=pl_consumer(),
                              coupon="BLACKFRIDAY", today="2026-11-15")
    assert total == 110.7
```

1. Zamroź obecne zachowanie testem z nazwą, która mówi, że to podejrzany błąd, i numerem zgłoszenia.
2. Zgłoś problem właścicielowi biznesowemu z konkretnym przykładem.
3. Po decyzji popraw kod w osobnej zmianie i zaktualizuj test, tym razem jako zwykły test wymagania.

Wyjątek stanowią błędy oczywiście szkodliwe, np. wyciek danych albo faktura z ujemną kwotą. Te poprawia się od razu, ale też jako osobną, jawną zmianę.

## Czas, losowość, sieć i globalny stan

Kod legacy rzadko jest deterministyczny. `generate_invoice` zależy od czterech rzeczy, które zmieniają się między uruchomieniami: daty, sekwencji w bazie, KSeF i serwera pocztowego. Zanim da się rozerwać te zależności (rozdział 04), można je przejąć w testach narzędziami, które nie wymagają zmian w kodzie.

| Źródło niedeterminizmu | Narzędzie w Pythonie | Jak działa |
|---|---|---|
| bieżąca data i czas | `freezegun`, `time-machine` | podmienia `datetime.now()` globalnie |
| losowość | `random.seed(...)`, `faker` z seedem | powtarzalne wartości |
| HTTP | `responses`, `respx`, `vcrpy` | przechwytuje żądania, zwraca przygotowane odpowiedzi, nagrywa i odtwarza |
| e-mail | `pytest` z `monkeypatch`, `django.core.mail.outbox` | zbiera wysłane wiadomości zamiast ich wysyłania |
| globalne połączenie z bazą | baza testowa w kontenerze, `monkeypatch` obiektu `DB` | ten sam kod, inna baza |
| zmienne środowiskowe, ustawienia | `monkeypatch.setenv`, `monkeypatch.setattr(settings, ...)` | wartości na czas testu |

```python
import responses
from freezegun import freeze_time


@freeze_time("2026-03-15 10:00:00")
@responses.activate
def test_generate_invoice_end_to_end(test_db, monkeypatch):
    monkeypatch.setattr("billing.invoices.DB", test_db)             # globalna baza podmieniona
    sent = []
    monkeypatch.setattr("billing.invoices.send_mail", lambda *a: sent.append(a))
    responses.post(settings.KSEF_URL, json={"status": "accepted"})
    test_db.load_fixture("order_1001_books_pl.sql")

    number = generate_invoice(1001)

    assert number == "FV/2026/1"
    assert test_db.query("SELECT total FROM invoices WHERE number=%s", number)[0]["total"] == 210.0
    assert responses.calls[0].request.body == b'{"number": "FV/2026/1", "total": 210.0}'
    assert sent[0][0] == "anna@example.com"
```

Taki test jest brzydki: zna nazwy modułów, podmienia globalne obiekty i ustawia pół świata. W kodzie legacy to normalne na początku. Jego zadaniem jest dać bezpieczeństwo do rozrywania zależności, a po rozdziale 04 zostanie zastąpiony prostszymi testami.

## Od którego poziomu zacząć

Kolejność w kodzie legacy jest odwrotna niż przy pisaniu nowego kodu. Nowy kod zaczyna się od testów jednostkowych, a legacy od testów wysokiego poziomu, bo tylko one dają się napisać bez zmian w kodzie.

```text
krok 1  testy end-to-end i golden master     siatka bezpieczeństwa na całym przepływie, bez zmian w kodzie
krok 2  rozrywanie zależności                 szwy, wstrzykiwanie, wydzielanie (rozdział 04)
krok 3  testy jednostkowe wydzielonych części reguły VAT, rabaty, numeracja, szybkie i precyzyjne
krok 4  odchudzanie testów end-to-end         zostają tylko najważniejsze ścieżki
```

| Poziom | Zalety w legacy | Wady |
|---|---|---|
| end-to-end, golden master | działa bez zmian w kodzie, łapie zmiany w całym przepływie | wolne, kruche, słaba diagnostyka |
| integracyjne z bazą | wierne, testują SQL i transakcje | wymagają bazy i danych testowych |
| jednostkowe | szybkie, precyzyjne | możliwe dopiero po rozerwaniu zależności |

Nie trzeba pokrywać testami całego systemu. Testy pisze się dla kodu, który zamierza się zmienić, zaczynając od hotspotów z rozdziału 02. Pokrycie rośnie tam, gdzie toczy się praca, a nie równomiernie.

## Co zapamiętać

- Test charakteryzujący opisuje, co kod robi teraz, a nie co powinien robić. Oczekiwaną wartość odczytuje się z komunikatu nieudanego testu.
- Golden master nagrywa wynik dla wielu kombinacji danych i porównuje z nim każde uruchomienie. Approval testing dodaje do tego zatwierdzanie zmian.
- Błąd odkryty testem charakteryzującym zamraża się z opisem i numerem zgłoszenia, a poprawia osobno, po decyzji biznesowej.
- Czas, losowość, sieć i globalny stan przejmuje się w testach narzędziami (`freezegun`, `responses`, `monkeypatch`), zanim da się je wstrzyknąć.
- W legacy zaczyna się od testów wysokiego poziomu, a jednostkowe dochodzą po rozerwaniu zależności.
- Testy pisze się tam, gdzie kod będzie zmieniany, zaczynając od hotspotów.

## Pytania sprawdzające

### 8. Czym jest test charakteryzujący i czym różni się od zwykłego testu jednostkowego?

<details>
<summary>Odpowiedź</summary>

To test (pojęcie Feathersa), który opisuje obecne zachowanie kodu zamiast wymaganego. Pisze się go po kodzie: wywołujesz kod, wpisujesz celowo złą wartość w asercji, odczytujesz faktyczny wynik z komunikatu błędu i wpisujesz go do testu. Zwykły test sprawdza zgodność ze specyfikacją, a nieudany oznacza błąd. Test charakteryzujący wykrywa każdą zmianę zachowania, niekoniecznie błąd, i służy jako siatka bezpieczeństwa przed zmianami.

Zobacz: sekcja „Fotografia zachowania”.

</details>

### 9. Czym są approval testing i golden master? Jak zamrozić zachowanie funkcji, której nikt nie rozumie?

<details>
<summary>Odpowiedź</summary>

Golden master to uruchomienie kodu dla wielu kombinacji danych (np. `itertools.product`), zapisanie całego wyniku do pliku w repozytorium i porównywanie z nim każdego kolejnego uruchomienia. Approval testing uogólnia to z narzędziami: biblioteka `approvaltests` zapisuje wynik jako `.received`, porównuje z `.approved` i przy różnicy pokazuje diff do świadomej akceptacji. Obie techniki zamrażają zachowanie bez rozumienia kodu. Zmienne dane (daty, UUID) trzeba ustalić lub zamaskować.

Zobacz: sekcja „Nagranie całego wyniku”.

</details>

### 10. Co zrobić, gdy test charakteryzujący ujawni zachowanie, które wygląda na błąd? Poprawiać od razu czy zostawić?

<details>
<summary>Odpowiedź</summary>

Nie poprawiać w tym samym kroku. Klienci lub inne systemy mogą polegać na obecnym zachowaniu, poprawka to zmiana zachowania wymagająca decyzji biznesowej, a połączenie z testami zaciemnia code review. Należy zamrozić zachowanie testem z nazwą wskazującą podejrzany błąd i numerem zgłoszenia, zgłosić problem z konkretnym przykładem, a po decyzji poprawić w osobnej zmianie i zamienić test na zwykły test wymagania. Wyjątkiem są błędy oczywiście szkodliwe, ale też jako osobna zmiana.

Zobacz: sekcja „Gdy test ujawni błąd”.

</details>

### 11. Jak testować kod zależny od czasu, losowości, sieci i globalnego stanu?

<details>
<summary>Odpowiedź</summary>

Przed rozerwaniem zależności przejmuje się je narzędziami bez zmian w kodzie: `freezegun` lub `time-machine` dla daty, stały seed dla losowości, `responses`, `respx` lub `vcrpy` dla HTTP, `monkeypatch` albo skrzynka testowa dla e-maili, baza testowa w kontenerze i podmiana globalnego obiektu połączenia, `monkeypatch` dla ustawień i zmiennych środowiskowych. Takie testy są brzydkie i znają szczegóły modułów, ale dają bezpieczeństwo do rozrywania zależności. Potem zastępuje się je prostszymi.

Zobacz: sekcja „Czas, losowość, sieć i globalny stan”.

</details>

### 12. Jak dobrać poziom testów dla legacy (jednostkowe, integracyjne, end-to-end) i od którego zacząć?

<details>
<summary>Odpowiedź</summary>

Odwrotnie niż przy nowym kodzie: najpierw testy end-to-end i golden master, bo dają się napisać bez zmian w kodzie i tworzą siatkę bezpieczeństwa. Potem rozrywanie zależności. Następnie szybkie testy jednostkowe wydzielonych części (reguły VAT, rabaty). Na końcu odchudzenie testów end-to-end do najważniejszych ścieżek. Testy pisze się tam, gdzie kod będzie zmieniany, zaczynając od hotspotów, a nie równomiernie w całym systemie.

Zobacz: sekcja „Od którego poziomu zacząć”.

</details>
