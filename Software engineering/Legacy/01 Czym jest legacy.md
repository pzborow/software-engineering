# Czym jest legacy

Prawie każdy programista pracuje z kodem, którego nie napisał, którego nikt do końca nie rozumie i którego boi się zmieniać. Ten tutorial pokazuje, jak z takim kodem pracować bezpiecznie: jak go zrozumieć, jak objąć testami, jak rozrywać zależności, refaktoryzować, przeprowadzać duże zmiany i rozmawiać o nim z biznesem.

Przykładem przewodnim jest moduł fakturowania w sklepie internetowym, napisany w 2014 roku i od tamtej pory łatany przez kolejne zespoły:

```python
# billing/invoices.py (oryginał ma 400 linii, tu skrót)
import datetime

import requests

from shop import settings
from shop.db import DB                      # globalne połączenie z bazą
from shop.mail import send_mail
from shop.pdf import render_pdf


def generate_invoice(order_id):
    order = DB.query("SELECT * FROM orders WHERE id=%s", order_id)[0]
    items = DB.query("SELECT * FROM order_items WHERE order_id=%s", order_id)
    customer = DB.query("SELECT * FROM customers WHERE id=%s", order["customer_id"])[0]

    total = 0
    for i in items:
        price = i["price"] * i["qty"]
        if i["category"] == "books":
            vat = 0.05
        elif i["category"] == "food" and customer["country"] == "PL":
            vat = 0.08
        else:
            vat = 0.23
        if customer["type"] == "B2B" and customer["country"] != "PL":
            vat = 0                          # odwrotne obciążenie
        total += price * (1 + vat)

    if order["coupon"] == "BLACKFRIDAY" and datetime.datetime.now().month == 11:
        total = total * 0.9
    total = round(total, 2)

    number = "FV/%s/%s" % (datetime.datetime.now().year, DB.next_seq("invoice"))
    DB.execute("INSERT INTO invoices (number, order_id, total) VALUES (%s, %s, %s)",
               number, order_id, total)
    requests.post(settings.KSEF_URL, json={"number": number, "total": total})
    send_mail(customer["email"], "Faktura " + number, render_pdf(number, order, items, customer))
    return number
```

Funkcja łączy odczyt z bazy, reguły VAT, rabaty, numerację, zapis, wysyłkę do KSeF i e-mail. Zależy od globalnego połączenia z bazą, od aktualnej daty i od dwóch usług sieciowych. Nie ma testów. Każdy kolejny rozdział robi z nią coś nowego.

## Kod bez testów

Potocznie „legacy” oznacza stary kod. Michael Feathers w książce „Working Effectively with Legacy Code” (2004) proponuje inną definicję: <a id="term-legacy-code"></a>[kod legacy](00%20Glossary%20Legacy.md#legacy-code) to kod bez testów.

Ta definicja jest bardziej użyteczna niż wiek kodu z kilku powodów:

- opisuje problem, a nie datę. Kod napisany w zeszłym tygodniu bez testów ma te same wady co kod sprzed dziesięciu lat: nie da się go zmienić z pewnością, że nic się nie zepsuło,
- wskazuje rozwiązanie. Skoro problemem jest brak testów, pierwszym krokiem jest ich dodanie,
- nie ocenia autorów. Stary kod z dobrymi testami nie jest legacy w tym sensie. Można go spokojnie zmieniać,
- tłumaczy, dlaczego zespoły boją się zmian. Bez testów jedynym zabezpieczeniem jest ostrożność, a ta prowadzi do „edytuj i módl się” (edit and pray), czyli zmiany z nadzieją, że nic się nie zepsuje.

Feathers przeciwstawia temu podejście „zabezpiecz i zmień” (cover and modify): najpierw obejmij kod testami, które wykryją niechciane zmiany zachowania, potem zmieniaj. Większość technik z tego tutorialu służy temu, żeby to było możliwe w kodzie, który do testowania się nie nadaje.

W praktyce na legacy składa się więcej niż brak testów: brak dokumentacji, autorzy, którzy odeszli, przestarzałe biblioteki, nieznane reguły biznesowe. Brak testów jest jednak tym elementem, który sprawia, że wszystkie pozostałe są niebezpieczne.

## Pożyczka od przyszłości

<a id="term-technical-debt"></a>[Dług techniczny](00%20Glossary%20Legacy.md#technical-debt) to metafora Warda Cunninghama z 1992 roku. Szybkie rozwiązanie dzisiaj jest jak pożyczka: daje korzyść od razu, ale każda późniejsza zmiana w tym miejscu kosztuje więcej, czyli dług rośnie o „odsetki”. Spłata polega na poprawieniu kodu.

Martin Fowler podzielił dług na cztery rodzaje w <a id="term-debt-quadrant"></a>[kwadrancie długu technicznego](00%20Glossary%20Legacy.md#debt-quadrant):

| | Rozważny | Lekkomyślny |
|---|---|---|
| **Świadomy** | „Musimy wydać przed targami. Zapłacimy później.” | „Nie mamy czasu na projektowanie.” |
| **Nieświadomy** | „Teraz wiemy, jak to powinno wyglądać.” | „Co to jest warstwa?” |

- świadomy i rozważny: zespół wie, że skraca drogę, i ma plan spłaty. To uprawniona decyzja biznesowa,
- świadomy i lekkomyślny: zespół wie, że robi źle, i nie ma planu. Dług rośnie bez kontroli,
- nieświadomy i lekkomyślny: zespół nie zna lepszych praktyk. Tu pomaga nauka, a nie sam czas,
- nieświadomy i rozważny: zespół zrobił najlepiej, jak umiał, a lepsze rozwiązanie zrozumiał dopiero później. Ten rodzaj jest nieunikniony, bo wiedza o domenie rośnie w trakcie projektu.

Rozmowa z biznesem o długu działa lepiej, gdy mówi się o skutkach, a nie o jakości kodu:

| Zamiast | Powiedz |
|---|---|
| „Kod fakturowania jest brzydki.” | „Każda zmiana stawki VAT zajmuje nam tydzień zamiast dnia.” |
| „Musimy zrefaktoryzować moduł.” | „W ostatnim kwartale trzy błędy w fakturach wymagały korekt u klientów B2B.” |
| „Brakuje testów.” | „Nie możemy bezpiecznie wprowadzić nowego kuponu przed Black Friday.” |

Biznes rozumie koszt opóźnienia, ryzyko błędów i koszt obsługi incydentów. Dług techniczny jest przyczyną, a te skutki są argumentem.

## Dlaczego dobry kod się psuje

Kod staje się legacy, nawet jeśli pisali go dobrzy programiści. Meir Lehman w latach 70. i 80. sformułował prawa ewolucji oprogramowania. Dwa z nich są tu kluczowe: system, który jest używany, musi się ciągle zmieniać, inaczej staje się coraz mniej użyteczny, a jego złożoność rośnie, jeśli nikt nie pracuje nad jej zmniejszaniem. To zjawisko nazywa się <a id="term-software-rot"></a>[erozją oprogramowania](00%20Glossary%20Legacy.md#software-rot) (software rot).

Przyczyny, które nie wymagają złych programistów:

- zmieniające się wymagania. `generate_invoice` była dobrą funkcją dla sklepu, który sprzedawał tylko w Polsce. Potem doszły książki z obniżonym VAT, klienci B2B z UE, kupony i KSeF. Każda zmiana była rozsądna, a razem dały funkcję na 400 linii,
- presja czasu. Poprawka przed terminem trafia tam, gdzie najszybciej, a nie tam, gdzie powinna,
- rotacja ludzi. Autorzy odchodzą, a z nimi wiedza o tym, dlaczego kod wygląda tak, a nie inaczej,
- starzejące się otoczenie. Biblioteki, frameworki i wersje języka się zmieniają, a kod stoi w miejscu,
- rosnąca wiedza. To, co było najlepszym zrozumieniem domeny w 2014 roku, dziś jest nieaktualne,
- efekt wybitego okna. Gdy kod jest już nieuporządkowany, kolejna niedbała zmiana wydaje się nie robić różnicy.

Legacy nie jest więc wynikiem porażki, tylko naturalnym stanem kodu, który długo żyje i zarabia. Kod, który nie staje się legacy, to zwykle kod, którego nikt nie używa.

## Co zapamiętać

- Według Feathersa kod legacy to kod bez testów. Ta definicja wskazuje problem i jego rozwiązanie.
- „Edytuj i módl się” zamienia się w „zabezpiecz i zmień”: najpierw testy, potem zmiany.
- Dług techniczny to pożyczka od przyszłości, której odsetki płaci się przy każdej zmianie.
- Kwadrant Fowlera dzieli dług na świadomy lub nieświadomy oraz rozważny lub lekkomyślny. Nieświadomy rozważny jest nieunikniony.
- Z biznesem rozmawia się o skutkach długu: czasie zmian, błędach i ryzyku, a nie o jakości kodu.
- Kod staje się legacy przez zmiany wymagań, presję czasu, rotację ludzi i rosnącą wiedzę, a nie tylko przez złych programistów.

## Pytania sprawdzające

### 1. Czym jest kod legacy według Michaela Feathersa i dlaczego definicja „kod bez testów” jest bardziej użyteczna niż „stary kod”?

<details>
<summary>Odpowiedź</summary>

Według Feathersa kod legacy to kod bez testów. Definicja opisuje problem, a nie datę: świeży kod bez testów ma te same wady co stary, bo nie da się go zmieniać z pewnością. Wskazuje też rozwiązanie (dodać testy), nie ocenia autorów i tłumaczy strach przed zmianami. Zamiast „edytuj i módl się” proponuje „zabezpiecz i zmień”: najpierw testy wykrywające zmiany zachowania, potem modyfikacja.

Zobacz: sekcja „Kod bez testów”.

</details>

### 2. Czym jest dług techniczny, jakie ma rodzaje (świadomy i nieświadomy, rozważny i lekkomyślny) i jak rozmawiać o nim z biznesem?

<details>
<summary>Odpowiedź</summary>

To metafora Warda Cunninghama: szybkie rozwiązanie dziś jest pożyczką, której odsetki płaci się przy każdej późniejszej zmianie. Kwadrant Fowlera wyróżnia dług świadomy i rozważny (świadoma decyzja z planem spłaty), świadomy i lekkomyślny (bez planu), nieświadomy i lekkomyślny (brak wiedzy) oraz nieświadomy i rozważny (lepsze rozwiązanie widać dopiero później, co jest nieuniknione). Z biznesem rozmawia się o skutkach: czasie zmian, liczbie błędów, ryzyku i koszcie opóźnienia, a nie o jakości kodu.

Zobacz: sekcja „Pożyczka od przyszłości”.

</details>

### 3. Dlaczego kod staje się legacy, nawet jeśli pisali go dobrzy programiści?

<details>
<summary>Odpowiedź</summary>

Bo zgodnie z prawami Lehmana używany system musi się zmieniać, a jego złożoność rośnie, jeśli nikt jej nie zmniejsza. Przyczyny to zmieniające się wymagania, gdzie każda rozsądna zmiana dokłada złożoności, presja czasu, rotacja ludzi i utrata wiedzy, starzejące się biblioteki, rosnące zrozumienie domeny oraz efekt wybitego okna. Legacy to naturalny stan kodu, który długo żyje i zarabia, a nie dowód porażki.

Zobacz: sekcja „Dlaczego dobry kod się psuje”.

</details>
