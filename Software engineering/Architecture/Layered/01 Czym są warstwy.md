# Czym są warstwy

<a id="term-layered-architecture"></a>[Architektura warstwowa](00%20Glossary%20Layered.md#layered-architecture) dzieli aplikację na poziome części, z których każda ma jedną rodzajową odpowiedzialność: wyświetlanie, logikę, dostęp do danych. Każda część korzysta tylko z części leżącej pod nią. To najstarszy i najpowszechniejszy sposób organizowania aplikacji biznesowych. Jest też punktem wyjścia dla architektur z tutoriali [hexagonal](../Hexagonal/), [onion](../Onion/) i [clean](../Clean/), które powstały, żeby naprawić jego słabości.

Najprostszy model działania wygląda tak:

```text
┌──────────────────────────────┐
│  prezentacja (HTTP, UI)      │
├──────────────────────────────┤
│  logika biznesowa            │
├──────────────────────────────┤
│  dostęp do danych            │
└──────────────┬───────────────┘
               ▼
          baza danych
    zależności wskazują w dół
```

Przykładem przewodnim tego tutorialu jest system rejestracji wizyt w przychodni: pacjenci umawiają wizyty, lekarze mają grafiki, a recepcja potwierdza i odwołuje terminy.

## Jedna odpowiedzialność na poziom

Każda <a id="term-layer"></a>[warstwa](00%20Glossary%20Layered.md#layer) grupuje kod o tym samym rodzaju odpowiedzialności. Pomysł wynika z zasady <a id="term-separation-of-concerns"></a>[separacji odpowiedzialności](00%20Glossary%20Layered.md#separation-of-concerns): kod, który formatuje HTML, nie powinien jednocześnie liczyć, czy lekarz ma wolny termin, i budować zapytań SQL.

Architektura warstwowa stała się standardem w latach 90. i 2000., gdy aplikacje biznesowe przechodziły od monolitów klient–serwer (formularze, które bezpośrednio pisały do bazy) do aplikacji webowych. Rozwiązywała konkretne problemy tamtych systemów:

- logika była rozsiana po formularzach, więc ta sama reguła miała kilka wersji,
- zmiana wyglądu ekranu wymagała dotykania kodu zapisującego dane,
- nie dało się dodać drugiego interfejsu, np. webowego obok desktopowego, bez kopiowania logiki,
- programiści nie wiedzieli, gdzie szukać kodu i gdzie dodawać nowy.

Warstwy dały prostą odpowiedź na pytanie „gdzie to umieścić?” i umożliwiły podział pracy: jedni pisali ekrany, inni logikę, jeszcze inni bazę.

## Warstwa logiczna i fizyczna

W języku angielskim są dwa słowa, które po polsku często tłumaczy się tak samo. Layer to warstwa logiczna, czyli podział kodu. <a id="term-tier"></a>[Tier](00%20Glossary%20Layered.md#tier) to warstwa fizyczna, czyli osobny proces, serwer albo maszyna, na której coś działa.

| | Layer (logiczna) | Tier (fizyczna) |
|---|---|---|
| Co dzieli | kod: pakiety, moduły, klasy | procesy, serwery, sieć |
| Komunikacja | wywołania funkcji w jednym procesie | przez sieć: HTTP, SQL, RPC |
| Przykład | `views`, `services`, `repositories` w jednej aplikacji Django | przeglądarka, serwer aplikacji, serwer bazy danych |

Klasyczne układy fizyczne:

```text
2-tier:   [klient z logiką i UI] ──SQL──► [baza danych]
3-tier:   [przeglądarka] ──HTTP──► [serwer aplikacji] ──SQL──► [baza danych]
N-tier:   [przeglądarka] ──► [CDN] ──► [API gateway] ──► [serwer aplikacji] ──► [cache] ──► [baza]
```

<a id="term-n-tier"></a>[N-tier](00%20Glossary%20Layered.md#n-tier) oznacza układ z dowolną liczbą fizycznych poziomów. W potocznym użyciu „N-tier” często oznacza też po prostu architekturę warstwową, co wprowadza zamieszanie. Aplikacja Django z trzema warstwami logicznymi, działająca w jednym kontenerze z osobną bazą, ma trzy layers i dwa tiers. Na rozmowie warto te pojęcia rozróżniać.

## Dlaczego tak popularna

Architektura warstwowa jest domyślnym wyborem wielu zespołów i frameworków. Ma realne zalety:

- jest prosta do wyjaśnienia: nowa osoba rozumie układ w kilka minut,
- frameworki (Django, Rails, Spring, ASP.NET MVC) prowadzą do niej domyślnie, więc zespół nie musi niczego projektować,
- daje jasną odpowiedź, gdzie umieścić nowy kod, przynajmniej na początku projektu,
- pozwala wymienić prezentację: to samo API może obsłużyć stronę WWW i aplikację mobilną,
- dobrze pasuje do aplikacji, w których większość pracy to przenoszenie danych między formularzem a bazą.

```python
# typowa aplikacja warstwowa: trzy pliki, trzy warstwy
# views.py        prezentacja: HTTP, formularze, szablony
# services.py     logika: reguły rezerwacji wizyt
# repositories.py dostęp do danych: zapytania ORM
```

Słabości architektury warstwowej ujawniają się dopiero wtedy, gdy logika biznesowa rośnie. Opisują je rozdziały 07 i 08. Do tego czasu warstwy bywają dokładnie tym, czego zespół potrzebuje.

## Co zapamiętać

- Architektura warstwowa dzieli aplikację na poziome warstwy o jednym rodzaju odpowiedzialności, a zależności wskazują w dół.
- Wynika z separacji odpowiedzialności i stała się standardem przy przejściu od aplikacji klient–serwer do webowych.
- Layer to podział logiczny kodu, tier to podział fizyczny na procesy i serwery.
- 2-tier, 3-tier i N-tier opisują układy fizyczne. Potocznie „N-tier” bywa synonimem architektury warstwowej.
- Zalety to prostota, wsparcie frameworków i jasne miejsce dla kodu. Słabości ujawniają się przy rosnącej logice.

## Pytania sprawdzające

### 1. Czym jest architektura warstwowa i jakie problemy miała rozwiązać, gdy stała się standardem w aplikacjach biznesowych?

<details>
<summary>Odpowiedź</summary>

To podział aplikacji na poziome warstwy (prezentacja, logika, dostęp do danych), z których każda ma jeden rodzaj odpowiedzialności i korzysta tylko z warstwy niższej. Wynika z separacji odpowiedzialności. Stała się standardem przy przejściu od aplikacji klient–serwer, w których logika była rozsiana po formularzach, zmiana ekranu dotykała zapisu danych, drugi interfejs wymagał kopiowania logiki, a nie było wiadomo, gdzie umieszczać kod.

Zobacz: początek rozdziału i sekcja „Jedna odpowiedzialność na poziom”.

</details>

### 2. Czym różni się warstwa logiczna (layer) od warstwy fizycznej (tier)? Czym są architektury 2-tier, 3-tier i N-tier?

<details>
<summary>Odpowiedź</summary>

Layer to logiczny podział kodu w jednym procesie (pakiety, moduły), komunikujący się wywołaniami funkcji. Tier to fizyczny podział na procesy, serwery i maszyny, komunikujące się przez sieć. 2-tier to klient z logiką i baza, 3-tier to przeglądarka, serwer aplikacji i baza, a N-tier to dowolna liczba fizycznych poziomów (CDN, gateway, cache). Potocznie „N-tier” bywa używane jako synonim architektury warstwowej. Aplikacja Django w jednym kontenerze z osobną bazą ma trzy layers i dwa tiers.

Zobacz: sekcja „Warstwa logiczna i fizyczna”.

</details>

### 3. Dlaczego architektura warstwowa jest domyślnym wyborem wielu zespołów i frameworków? Jakie ma realne zalety?

<details>
<summary>Odpowiedź</summary>

Jest prosta do wyjaśnienia, frameworki (Django, Rails, Spring, ASP.NET MVC) prowadzą do niej domyślnie, daje jasne miejsce dla nowego kodu, pozwala wymienić lub dodać warstwę prezentacji (web i mobile na tym samym API) i dobrze pasuje do aplikacji, w których większość pracy to przenoszenie danych między formularzem a bazą. Słabości pojawiają się dopiero, gdy logika biznesowa rośnie.

Zobacz: sekcja „Dlaczego tak popularna”.

</details>
