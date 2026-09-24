# Refaktoryzacja

Gdy kod ma testy i szwy, można go poprawiać. W kodzie legacy poprawianie musi być szczególnie zdyscyplinowane: małe kroki, wyraźne oddzielenie zmian struktury od zmian zachowania i świadomość, kiedy lepiej przestać. Ten rozdział pokazuje, jak refaktoryzować obliczanie VAT w `generate_invoice` i jak nie dać się wciągnąć w refaktoryzację bez końca.

```text
commit 1  refactor: wydziel calculate_total z generate_invoice
commit 2  refactor: wydziel vat_rate_for(category, customer)
commit 3  refactor: zamień łańcuch if na tabelę stawek
commit 4  refactor: nazwy z języka księgowości (is_reverse_charge, REDUCED_RATES)
commit 5  feat: stawka obniżona 5% dla nowej kategorii ebooks
```

## Struktura osobno, zachowanie osobno

<a id="term-refactoring"></a>[Refactoring](00%20Glossary%20Legacy.md#refactoring), czyli refaktoryzacja, to według Martina Fowlera zmiana wewnętrznej struktury kodu, która nie zmienia jego zewnętrznego zachowania. Wszystko, co zmienia wynik, nawet o grosz, jest zmianą zachowania, a nie refaktoryzacją.

Kent Beck opisał to metaforą <a id="term-two-hats"></a>[dwóch kapeluszy](00%20Glossary%20Legacy.md#two-hats). Programista nosi w danej chwili albo kapelusz „dodaję funkcję”, albo kapelusz „refaktoryzuję”, nigdy oba naraz. Zmienia je często, ale świadomie.

Dlaczego nie łączy się ich w jednym commicie:

- testy charakteryzujące z rozdziału 03 mają przy refaktoryzacji przechodzić bez zmian. Jeśli w tym samym commicie zmienia się zachowanie, test musi się zmienić, a wtedy nie wiadomo, czy zmiana wyniku jest zamierzona, czy przypadkowa,
- code review commitu, który jednocześnie przenosi 200 linii i zmienia jeden warunek, prawie zawsze przeoczy ten warunek,
- jeśli coś pójdzie źle na produkcji, commit z czystą refaktoryzacją da się bezpiecznie cofnąć, a zmiana funkcji zostaje. W połączonym commicie trzeba cofać wszystko,
- `git bisect` wskazuje commit, który zepsuł zachowanie. W czystej historii to zawsze commit „feat” albo „fix”, a nie przeniesienie kodu.

Praktyczna konwencja: prefiks w komunikacie (`refactor:`, `feat:`, `fix:`) i zasada, że commit `refactor:` nie zmienia żadnego testu poza przeniesieniem go razem z kodem.

## Małe kroki

W legacy refaktoryzuje się w krokach tak małych, że każdy można sprawdzić testami w kilka sekund i cofnąć bez żalu. Duży krok („przepiszę tę funkcję porządnie”) kończy się godzinami debugowania i często porzuceniem zmiany.

Przykład: obliczanie VAT w `generate_invoice`, w kolejnych krokach, każdy z uruchomieniem testów.

```python
# krok 0: stan wyjściowy, fragment pętli
for i in items:
    price = i["price"] * i["qty"]
    if i["category"] == "books":
        vat = 0.05
    elif i["category"] == "food" and customer["country"] == "PL":
        vat = 0.08
    else:
        vat = 0.23
    if customer["type"] == "B2B" and customer["country"] != "PL":
        vat = 0
    total += price * (1 + vat)


# krok 1: wydziel funkcję (Extract Function), treść przeniesiona bez zmian
def vat_rate_for(category, customer):
    if category == "books":
        vat = 0.05
    elif category == "food" and customer["country"] == "PL":
        vat = 0.08
    else:
        vat = 0.23
    if customer["type"] == "B2B" and customer["country"] != "PL":
        vat = 0
    return vat

for i in items:
    total += i["price"] * i["qty"] * (1 + vat_rate_for(i["category"], customer))


# krok 2: wczesny powrót dla odwrotnego obciążenia (kolejność warunków zachowana w skutkach)
def vat_rate_for(category, customer):
    if customer["type"] == "B2B" and customer["country"] != "PL":
        return 0
    if category == "books":
        return 0.05
    if category == "food" and customer["country"] == "PL":
        return 0.08
    return 0.23


# krok 3: nazwy z języka księgowości i tabela zamiast łańcucha warunków
REDUCED_RATES = {"books": 0.05}
REDUCED_RATES_DOMESTIC = {"food": 0.08}
STANDARD_RATE = 0.23

def is_reverse_charge(customer):
    return customer["type"] == "B2B" and customer["country"] != "PL"

def vat_rate_for(category, customer):
    if is_reverse_charge(customer):
        return 0
    if category in REDUCED_RATES:
        return REDUCED_RATES[category]
    if customer["country"] == "PL" and category in REDUCED_RATES_DOMESTIC:
        return REDUCED_RATES_DOMESTIC[category]
    return STANDARD_RATE
```

Po każdym kroku golden master z rozdziału 03 musi dać identyczny wynik. Krok 2 wymaga uwagi: kolejność warunków się zmieniła, ale skutek jest ten sam, bo odwrotne obciążenie i tak nadpisywało stawkę. Właśnie po to są testy.

Część refaktoryzacji jest bezpieczna nawet bez testów, jeśli wykonuje ją narzędzie, a nie człowiek. To <a id="term-automated-refactoring"></a>[refaktoryzacje automatyczne](00%20Glossary%20Legacy.md#automated-refactoring) w IDE: zmiana nazwy (Rename), wydzielenie zmiennej, metody i stałej (Extract Variable, Method, Constant), wstawienie w miejsce użycia (Inline), przeniesienie (Move), zmiana sygnatury (Change Signature). PyCharm, VS Code z Pylance albo Rope dla Pythona wykonują je z uwzględnieniem wszystkich użyć.

W Pythonie trzeba uważać bardziej niż w językach statycznie typowanych. Narzędzie nie zobaczy wywołań przez `getattr(obj, "generate_" + kind)`, nazw w szablonach, w konfiguracji, w SQL-u ani w innych repozytoriach. Po automatycznej zmianie nazwy warto przeszukać projekt tekstowo (`grep -rn "generate_invoice"`), także poza plikami `.py`.

## Zostaw trochę lepiej

<a id="term-boy-scout-rule"></a>[Zasada skauta](00%20Glossary%20Legacy.md#boy-scout-rule) (boy scout rule), spopularyzowana przez Roberta C. Martina, mówi: zostaw kod w trochę lepszym stanie, niż go zastałeś. W legacy to najtańszy sposób spłacania długu, bo poprawki dzieją się tam, gdzie i tak toczy się praca, czyli w hotspotach.

Problem polega na tym, że zasada skauta łatwo zamienia się w rozlewanie zakresu: zadanie „dodaj stawkę 5% dla e-booków” kończy się przepisaniem modułu fakturowania i tygodniowym opóźnieniem. Granice, które pomagają:

- poprawiaj tylko kod, którego dotyka zadanie, a nie sąsiednie moduły,
- poprawki przygotowujące, czyli takie, które ułatwiają zadanie, rób przed zmianą, jako osobne commity `refactor:`,
- poprawki porządkowe, czyli takie, które nie są potrzebne do zadania, ograniczaj do tego, co mieści się w kilkudziesięciu minutach,
- większe pomysły zapisuj jako osobne zadanie w backlogu, a nie realizuj w ramach bieżącego.

Kent Beck ujął podejście do poprawek przygotowujących w jednym zdaniu, które dobrze działa w legacy: „najpierw spraw, żeby zmiana była łatwa (to może być trudne), potem zrób łatwą zmianę”. Taka <a id="term-preparatory-refactoring"></a>[refaktoryzacja przygotowująca](00%20Glossary%20Legacy.md#preparatory-refactoring) jest najłatwiejsza do uzasadnienia, bo wprost przyspiesza zadanie, za które biznes płaci.

```text
zadanie: stawka 5% dla nowej kategorii e-booków

refactor: wydziel vat_rate_for         ← przygotowanie, 20 minut
refactor: tabela stawek obniżonych     ← przygotowanie, 15 minut
feat: e-booki ze stawką 5%             ← właściwa zmiana, jedna linia w tabeli i test
refactor: nazwy zmiennych w pętli      ← skaut, 5 minut
```

## Kiedy nie refaktoryzować

Refaktoryzacja kosztuje czas i niesie ryzyko. Czasem nie warto jej robić:

- kod nie będzie zmieniany. Brzydki, ale stabilny moduł, którego nikt nie dotyka od lat, nie generuje kosztów, a jego poprawa ich nie zmniejszy,
- kod wkrótce zniknie, bo jest zastępowany (rozdział 06) albo funkcja jest wycofywana. Czas lepiej poświęcić na nową wersję,
- nie ma żadnej siatki bezpieczeństwa i nie da się jej szybko zbudować, a kod jest krytyczny (np. rozliczenia z urzędem skarbowym). Najpierw testy, potem refaktoryzacja, a nie odwrotnie,
- tuż przed ważnym wydaniem lub w czasie zamrożenia zmian. Refaktoryzacja może poczekać tydzień,
- nie rozumiesz jeszcze domeny. Refaktoryzacja bez zrozumienia często utrwala złe pojęcia w nowej, ładniejszej formie. Lepiej zacząć od scratch refactoringu z rozdziału 02,
- refaktoryzacja nie ma celu. „Kod będzie ładniejszy” to za mało. „Dodawanie stawek VAT zajmie godzinę zamiast dnia” to cel.

## Co zapamiętać

- Refaktoryzacja zmienia strukturę bez zmiany zachowania. Wszystko, co zmienia wynik, jest zmianą zachowania.
- Dwa kapelusze: refaktoryzacja i zmiana funkcji w osobnych commitach, bo inaczej testy, review, rollback i `git bisect` tracą sens.
- W legacy refaktoryzuje się bardzo małymi krokami, z testami po każdym kroku.
- Refaktoryzacje automatyczne w IDE są bezpieczne nawet bez testów, ale w Pythonie nie widzą użyć dynamicznych, tekstowych i zewnętrznych.
- Zasada skauta działa w granicach zadania. Najpierw refaktoryzacja przygotowująca, potem łatwa zmiana, a większe pomysły do backlogu.
- Nie refaktoryzuje się kodu, który się nie zmienia, zaraz zniknie, jest krytyczny bez testów, a także bez zrozumienia domeny i bez celu.

## Pytania sprawdzające

### 19. Czym różni się refaktoryzacja od zmiany zachowania i dlaczego nie łączy się ich w jednym commicie?

<details>
<summary>Odpowiedź</summary>

Refaktoryzacja (Fowler) zmienia strukturę bez zmiany zewnętrznego zachowania, a wszystko, co zmienia wynik, jest zmianą zachowania. Według metafory dwóch kapeluszy Kenta Becka nosi się naraz tylko jeden. Nie łączy się ich, bo testy charakteryzujące przestają odróżniać zmianę zamierzoną od przypadkowej, code review przeocza zmianę ukrytą w przeniesionym kodzie, nie da się cofnąć samej refaktoryzacji, a `git bisect` wskazuje wymieszane commity. Konwencja: prefiksy `refactor:`, `feat:`, `fix:`, a commit refaktoryzacyjny nie zmienia testów.

Zobacz: sekcja „Struktura osobno, zachowanie osobno”.

</details>

### 20. Jak refaktoryzować w bardzo małych krokach i jakie refaktoryzacje są bezpieczne nawet bez testów (automatyczne w IDE)?

<details>
<summary>Odpowiedź</summary>

Kroki powinny być tak małe, żeby każdy dało się sprawdzić testami w kilka sekund i cofnąć, np. wydzielenie funkcji bez zmian treści, potem wczesne powroty, potem nazwy i tabela zamiast warunków, z golden masterem po każdym kroku. Bez testów bezpieczne są refaktoryzacje wykonywane przez narzędzie: Rename, Extract Variable, Method, Constant, Inline, Move i Change Signature w PyCharm, Pylance lub Rope. W Pythonie narzędzie nie widzi wywołań dynamicznych (`getattr`), nazw w szablonach, konfiguracji, SQL-u i innych repozytoriach, więc po zmianie trzeba przeszukać projekt tekstowo.

Zobacz: sekcja „Małe kroki”.

</details>

### 21. Czym jest zasada skauta i jak stosować ją bez rozlewania zakresu zadania?

<details>
<summary>Odpowiedź</summary>

To zasada spopularyzowana przez Roberta C. Martina: zostaw kod trochę lepszym, niż go zastałeś. W legacy spłaca dług tam, gdzie toczy się praca. Żeby nie rozlewać zakresu: poprawiaj tylko kod dotykany przez zadanie, poprawki ułatwiające zadanie rób przed zmianą jako osobne commity (refaktoryzacja przygotowująca, czyli najpierw łatwa zmiana, potem ta łatwa zmiana), porządki ograniczaj do kilkudziesięciu minut, a większe pomysły zapisuj w backlogu.

Zobacz: sekcja „Zostaw trochę lepiej”.

</details>

### 22. Kiedy nie należy refaktoryzować legacy?

<details>
<summary>Odpowiedź</summary>

Gdy kod nie będzie zmieniany, bo stabilny i nietykany kod nie generuje kosztów. Gdy kod wkrótce zniknie przez zastąpienie lub wycofanie funkcji. Gdy kod jest krytyczny, a nie ma i nie da się szybko zbudować siatki bezpieczeństwa (najpierw testy). Tuż przed wydaniem lub w zamrożeniu zmian. Gdy nie rozumie się domeny, bo refaktoryzacja utrwala złe pojęcia (lepszy jest scratch refactoring). Gdy refaktoryzacja nie ma mierzalnego celu.

Zobacz: sekcja „Kiedy nie refaktoryzować”.

</details>
