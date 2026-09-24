# Rozpoznanie terenu

Zanim cokolwiek się zmieni, trzeba wiedzieć, gdzie się jest. W nieznanym systemie bez dokumentacji i bez autorów najważniejsze pytania brzmią: co ten system robi, które miejsca są niebezpieczne, a które warto poprawić najpierw? Ten rozdział pokazuje, jak odpowiedzieć na nie w kilka dni, a nie w kilka miesięcy.

```text
pytanie                          źródło odpowiedzi
co robi system?                  ludzie, logi produkcyjne, UI, testy ręczne
jak jest zbudowany?              struktura katalogów, zależności, punkty wejścia
dlaczego tak wygląda?            historia gita, zgłoszenia, commity
gdzie jest ryzyko?               hotspoty, złożoność, sprzężenie zmian
jak działa konkretna funkcja?    scratch refactoring, szkic efektów, debugger
```

## Pierwsze dni

W nieznanym systemie nie zaczyna się od czytania kodu linia po linii. Zaczyna się od obrazu całości, a kod czyta się dopiero wtedy, gdy wiadomo, czego szukać.

Kolejność, która dobrze się sprawdza:

1. Uruchom system lokalnie i przejdź główne ścieżki jak użytkownik: złóż zamówienie, wygeneruj fakturę, anuluj. To, czego nie da się uruchomić, jest pierwszym zadaniem do naprawy.
2. Porozmawiaj z ludźmi: support wie, co najczęściej się psuje, księgowość wie, jakie faktury są błędne, a osoby, które pracowały z systemem, wiedzą, czego się bać.
3. Znajdź punkty wejścia: endpointy HTTP, zadania cron, konsumenci kolejek, polecenia CLI. Każdy z nich to początek ścieżki, którą da się prześledzić.
4. Narysuj zależności: moduły, bazy, usługi zewnętrzne. Wystarczy kartka albo prosty wykres z narzędzia (`pydeps` dla Pythona).
5. Przejrzyj logi i metryki produkcyjne: które endpointy są używane, które błędy się powtarzają, które funkcje nikt nie wywołuje od roku.
6. Zapisuj, co już wiadomo. Notatki z pierwszych dni są najcenniejszą dokumentacją, bo świeże spojrzenie szybko znika.

```bash
# punkty wejścia i struktura
grep -rn "@app.route\|@router\.\|path(" --include=*.py . | wc -l
grep -rn "def handle\|@celery.task\|@shared_task" --include=*.py .
pydeps shop --max-bacon 2 -o deps.svg

# martwy kod: funkcje, których nikt nie woła
vulture shop/ --min-confidence 80
```

## Archeologia w historii

Kod mówi, co robi. Historia zmian mówi, dlaczego. <a id="term-code-archaeology"></a>[Archeologia kodu](00%20Glossary%20Legacy.md#code-archaeology) to odtwarzanie kontekstu decyzji z historii repozytorium, zgłoszeń i dokumentów.

Najbardziej przydatne polecenia gita:

```bash
# kto i kiedy zmienił tę linię, z pominięciem zmian formatowania
git blame -w -C -C -M billing/invoices.py -L 30,40

# historia jednej funkcji
git log -L :generate_invoice:billing/invoices.py

# kiedy pojawił się ten warunek (wyszukiwanie w treści zmian)
git log -S "BLACKFRIDAY" --oneline

# commity, których komunikat wspomina odwrotne obciążenie
git log --grep="odwrotn" -i --oneline

# kto najwięcej pracował nad modułem i kogo pytać
git shortlog -sn -- billing/

# pliki zmieniane w tym samym commicie co invoices.py
git log --format="" --name-only -- billing/invoices.py | sort | uniq -c | sort -rn | head
```

`git log -S "BLACKFRIDAY"` może pokazać, że warunek dodano w listopadzie 2019 roku w commicie „hotfix promocja”, a numer zgłoszenia w komunikacie prowadzi do rozmowy z działem marketingu. Wtedy wiadomo, że kupon miał działać tylko w tamtym roku, a warunek `month == 11` jest błędem, który od lat daje rabat co listopad.

Historia bywa jedynym źródłem wiedzy o regułach biznesowych. Warto czytać ją przed każdą zmianą w niezrozumiałym miejscu.

## Gdzie inwestować wysiłek

Nie cały kod legacy jest problemem. Kod, który od pięciu lat się nie zmienia i działa, może pozostać brzydki. Problemem jest kod, który jest jednocześnie złożony i często zmieniany, bo tam każda zmiana jest droga i ryzykowna.

<a id="term-hotspot"></a>[Hotspot](00%20Glossary%20Legacy.md#hotspot) w rozumieniu Adama Tornhilla z książki „Your Code as a Crime Scene” to plik albo funkcja o wysokiej częstotliwości zmian i wysokiej złożoności jednocześnie. Częstotliwość zmian bierze się z historii gita. Złożoność można mierzyć liczbą linii albo <a id="term-cyclomatic-complexity"></a>[złożonością cyklomatyczną](00%20Glossary%20Legacy.md#cyclomatic-complexity), czyli liczbą niezależnych ścieżek przez kod, rosnącą z każdym `if`, pętlą i `and`/`or`.

```python
# hotspots.py: częstotliwość zmian z gita razy złożoność z radona
import subprocess
from collections import Counter

from radon.complexity import cc_visit


def change_counts(since: str = "12 months ago") -> Counter:
    log = subprocess.run(
        ["git", "log", f"--since={since}", "--format=", "--name-only", "--", "*.py"],
        capture_output=True, text=True, check=True,
    ).stdout
    return Counter(line for line in log.splitlines() if line)


def complexity(path: str) -> int:
    with open(path) as f:
        return sum(block.complexity for block in cc_visit(f.read()))


changes = change_counts()
ranking = sorted(
    ((changes[p] * complexity(p), changes[p], complexity(p), p) for p in changes),
    reverse=True,
)
for score, n, cc, path in ranking[:10]:
    print(f"{score:6}  zmian={n:3}  złożoność={cc:4}  {path}")
```

```text
 score  zmian  złożoność  plik
  4180     38        110  billing/invoices.py
  1512     27         56  orders/checkout.py
   420     35         12  shop/settings.py
   380      2        190  reports/legacy_export.py
```

`billing/invoices.py` to hotspot: zmieniany co półtora tygodnia i bardzo złożony. `reports/legacy_export.py` jest bardziej złożony, ale zmieniany dwa razy w roku, więc jego poprawa może poczekać. `settings.py` zmienia się często, ale jest prosty.

Drugą przydatną miarą jest <a id="term-change-coupling"></a>[sprzężenie zmian](00%20Glossary%20Legacy.md#change-coupling) (change coupling): pliki, które zmieniają się razem w tych samych commitach, choć w kodzie nie widać między nimi zależności. Jeśli `invoices.py` i `reports/vat_summary.sql` zmieniają się razem w 80 procentach commitów, to reguły VAT są zduplikowane w dwóch miejscach. Takiej zależności nie pokaże żadne narzędzie do analizy importów.

## Zrozumieć jedną funkcję

Gdy wiadomo już, którą funkcję trzeba zmienić, trzeba ją zrozumieć. W funkcji na 400 linii czytanie od góry do dołu szybko przestaje działać. Pomagają trzy techniki.

<a id="term-scratch-refactoring"></a>[Scratch refactoring](00%20Glossary%20Legacy.md#scratch-refactoring) to technika Feathersa: robisz gałąź i refaktoryzujesz bez ograniczeń, bez testów i bez dbania o poprawność. Wydzielasz metody, zmieniasz nazwy, przestawiasz kod, żeby zrozumieć, co robi. Potem wyrzucasz całą gałąź. Zostaje zrozumienie i pomysł, jak kod powinien wyglądać.

```python
# gałąź scratch/invoices: wydzielanie tylko po to, żeby zrozumieć
def generate_invoice(order_id):
    order, items, customer = load_order_data(order_id)       # linie 12–40
    total = calculate_total(items, customer)                 # linie 41–180: VAT, 6 wyjątków
    total = apply_coupons(total, order)                      # linie 181–230: kupony zależne od daty
    number = next_invoice_number()                           # linie 231–260: numeracja per rok
    save_invoice(number, order_id, total)                    # linie 261–290
    notify_ksef(number, total)                               # linie 291–350: retry, 3 formaty
    send_invoice_email(customer, number, order, items)       # linie 351–400
    return number
```

<a id="term-effect-sketch"></a>[Szkic efektów](00%20Glossary%20Legacy.md#effect-sketch) (effect sketch) to kolejna technika Feathersa: rysujesz, które zmienne i funkcje wpływają na które. Dzięki temu widać, co może się zepsuć przy zmianie danego miejsca.

```text
customer["country"] ──┐
customer["type"] ─────┼──► vat ──► total ──► round ──► INSERT invoices
i["category"] ────────┘                  │                   │
order["coupon"] ──┐                      │                   └──► KSeF
datetime.now() ───┴──────► rabat ────────┘                   └──► e-mail z PDF
datetime.now().year ─────────────────────────► number ──┘
```

Ze szkicu wynika, że zmiana obliczania VAT wpływa na zapis, KSeF i PDF, a `datetime.now()` wpływa w dwóch miejscach: na rabat i na numer faktury.

Trzecia technika to obserwacja w działaniu: debugger z punktami przerwania na rozgałęzieniach, tymczasowe logowanie wartości pośrednich na środowisku testowym, a w ostateczności na produkcji z flagą. Logowanie pokazuje, które gałęzie `if` są w ogóle używane. Często okazuje się, że połowa warunków obsługuje przypadki, które nie zdarzyły się od lat.

## Co zapamiętać

- Nieznany system poznaje się od uruchomienia, rozmów, punktów wejścia, zależności i logów, a nie od czytania kodu linia po linii.
- Archeologia kodu z `git blame`, `git log -L`, `git log -S` i `git shortlog` odtwarza, dlaczego kod wygląda tak, a nie inaczej.
- Hotspot to kod często zmieniany i złożony jednocześnie. Tam inwestuje się najpierw. Kod złożony, ale niezmieniany, może poczekać.
- Sprzężenie zmian pokazuje ukryte zależności między plikami zmienianymi razem.
- Scratch refactoring to refaktoryzacja do wyrzucenia, która służy tylko zrozumieniu.
- Szkic efektów pokazuje, na co wpływa zmiana, a obserwacja w działaniu pokazuje, które gałęzie są naprawdę używane.

## Pytania sprawdzające

### 4. Od czego zacząć pracę w nieznanym systemie bez dokumentacji i bez autorów w zespole?

<details>
<summary>Odpowiedź</summary>

Od obrazu całości, a nie od czytania kodu. Uruchom system lokalnie i przejdź główne ścieżki. Porozmawiaj z supportem, użytkownikami i osobami, które znają system. Znajdź punkty wejścia: endpointy, cron, kolejki, CLI. Narysuj zależności między modułami i usługami. Przejrzyj logi i metryki, żeby zobaczyć, co jest używane i co się psuje. Zapisuj wnioski od pierwszego dnia. Kod czyta się, gdy wiadomo, czego szukać.

Zobacz: sekcja „Pierwsze dni”.

</details>

### 5. Jak używać historii gita (`log`, `blame`, `log -S`, `shortlog`) do archeologii kodu i zrozumienia, dlaczego coś jest napisane w dany sposób?

<details>
<summary>Odpowiedź</summary>

`git blame -w -C -C -M` pokazuje autora i commit każdej linii, z pominięciem zmian formatowania i przeniesień. `git log -L :funkcja:plik` pokazuje historię jednej funkcji. `git log -S "tekst"` znajduje commit, w którym pojawił się dany fragment, a `--grep` przeszukuje komunikaty. `git shortlog -sn -- katalog` pokazuje, kogo pytać. Pliki zmieniane razem ujawniają ukryte zależności. Komunikaty i numery zgłoszeń prowadzą do kontekstu biznesowego decyzji.

Zobacz: sekcja „Archeologia w historii”.

</details>

### 6. Czym jest analiza hotspotów (częstotliwość zmian razy złożoność) i jak pomaga wybrać, gdzie inwestować wysiłek?

<details>
<summary>Odpowiedź</summary>

To technika Adama Tornhilla: hotspot to plik lub funkcja jednocześnie często zmieniana (z historii gita) i złożona (liczba linii lub złożoność cyklomatyczna). Iloczyn tych miar wskazuje miejsca, gdzie każda zmiana jest droga i ryzykowna, więc poprawa przynosi największy zwrot. Kod złożony, ale rzadko zmieniany może poczekać. Uzupełnieniem jest sprzężenie zmian: pliki zmieniane razem, co ujawnia zduplikowane reguły i ukryte zależności.

Zobacz: sekcja „Gdzie inwestować wysiłek”.

</details>

### 7. Jak szybko zrozumieć przepływ w dużej funkcji lub module (scratch refactoring, szkicowanie efektów, logowanie, debugger)?

<details>
<summary>Odpowiedź</summary>

Scratch refactoring (Feathers): na osobnej gałęzi refaktoryzujesz bez ograniczeń tylko po to, żeby zrozumieć, a potem gałąź wyrzucasz. Szkic efektów: rysujesz, które zmienne i funkcje wpływają na które, więc widać zasięg zmiany. Obserwacja w działaniu: debugger na rozgałęzieniach i tymczasowe logowanie wartości pośrednich pokazują, które gałęzie są naprawdę używane. Często połowa warunków obsługuje przypadki, które dawno się nie zdarzają.

Zobacz: sekcja „Zrozumieć jedną funkcję”.

</details>
