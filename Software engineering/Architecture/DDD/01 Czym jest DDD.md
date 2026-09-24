# Czym jest DDD

<a id="term-ddd"></a>[Domain-Driven Design](00%20Glossary%20DDD.md#ddd) (DDD) to podejście do tworzenia oprogramowania dla złożonych dziedzin biznesowych. Zakłada, że najważniejszą częścią systemu jest model dziedziny, który zespół buduje razem z ludźmi znającymi biznes, a kod ma ten model wiernie odzwierciedlać. Podejście opisał Eric Evans w książce „Domain-Driven Design: Tackling Complexity in the Heart of Software” z 2003 roku, zwanej „Blue Book”.

Najprostszy model działania wygląda tak:

```text
eksperci biznesowi ◄──── rozmowa, warsztaty, przykłady ────► zespół
                 \                                        /
                  └──────► wspólny język i model ◄───────┘
                                    │
                                    ▼
                          kod, który mówi tym językiem
                                    │
                                    ▼
                    nowa wiedza z produkcji i rozmów ──► poprawiony model
```

Przykładem przewodnim tego tutorialu jest wypożyczalnia samochodów: rezerwacje, flota, dynamiczna wycena, umowy najmu, rozliczenia, szkody.

## Problem, z którym przyszedł Evans

Evans obserwował projekty, w których technologia była w porządku, a system i tak nie spełniał oczekiwań. Przyczyną nie były frameworki ani bazy, tylko to, że programiści nie rozumieli biznesu, a model w kodzie nie odpowiadał temu, jak biznes naprawdę działa. Każda nowa reguła wymagała obejść, a rozmowy z ekspertami przypominały tłumaczenie między dwoma językami.

Punktem wyjścia Evansa jest <a id="term-domain"></a>[domena](00%20Glossary%20DDD.md#domain), czyli obszar działalności, którym zajmuje się system: wynajem samochodów, ubezpieczenia, logistyka. Złożoność systemu wynika głównie z domeny, a nie z techniki. Tę złożoność trzeba zrozumieć i odwzorować, a nie ukryć pod warstwami frameworka.

Odpowiedzią jest <a id="term-domain-model"></a>[model domeny](00%20Glossary%20DDD.md#domain-model): uproszczona, celowa reprezentacja wiedzy o domenie. Model nie jest diagramem ani schematem bazy. Jest zbiorem pojęć, reguł i relacji, który pozwala rozwiązywać konkretne problemy biznesu. Ten sam model żyje w rozmowach, w dokumentacji i w kodzie.

## Modelowanie, a nie wzorce

Książka Evansa ma dwie części, które różnią się poziomem. <a id="term-strategic-design"></a>[Projektowanie strategiczne](00%20Glossary%20DDD.md#strategic-design) dotyczy całego systemu i organizacji. <a id="term-tactical-design"></a>[Projektowanie taktyczne](00%20Glossary%20DDD.md#tactical-design) dotyczy budowy modelu w kodzie w obrębie jednego kontekstu.

| Część | O czym | Przykładowe pojęcia |
|---|---|---|
| strategiczna | jak podzielić duży system i organizację, gdzie inwestować wysiłek | subdomeny, bounded context, mapa kontekstów, język wszechobecny |
| taktyczna | jak zbudować model w kodzie w obrębie jednego kontekstu | encja, value object, agregat, repozytorium, zdarzenie domenowe |

Wiele osób poznaje DDD od strony taktycznej, bo wzorce łatwo pokazać w kodzie. Evans podkreślał jednak, że najważniejsza jest część strategiczna i sam proces modelowania z ekspertami. Wzorce taktyczne to narzędzia, które pomagają wyrazić model w kodzie. Bez modelu nie mają czego wyrażać.

Dobrze pokazuje to prosty test: czy ekspert biznesowy, patrząc na nazwy klas i metod, rozpozna swój świat? `RentalAgreement.extend(new_return_date)` przejdzie ten test. `RentalManager.processUpdate(dto)` nie przejdzie, nawet jeśli pod spodem są encje i repozytoria zgodne z podręcznikiem.

## Wzorce bez strategii

<a id="term-ddd-lite"></a>[DDD lite](00%20Glossary%20DDD.md#ddd-lite) to określenie, które spopularyzował Vaughn Vernon. Oznacza stosowanie wyłącznie wzorców taktycznych: projekt ma encje, repozytoria, agregaty i value objects, ale nie ma wspólnego języka z biznesem, podziału na konteksty ani świadomego wyboru, gdzie inwestować.

Dlaczego to zwykle zawodzi:

- bez granic kontekstów powstaje jeden ogromny model, w którym „klient” musi obsłużyć rezerwacje, rozliczenia i marketing naraz,
- bez języka wszechobecnego nazwy w kodzie wymyślają programiści, a model rozjeżdża się z biznesem,
- bez podziału na subdomeny zespół wkłada tyle samo wysiłku w rejestrację użytkowników co w wycenę, która daje firmie przewagę,
- wzorce zaczynają być celem samym w sobie: agregaty powstają z tabel, repozytoria z DAO, a ilość kodu rośnie bez korzyści.

DDD lite nie jest bezwartościowe. Dobre value objects i agregaty poprawiają jakość kodu. Nie rozwiązują jednak problemu, dla którego DDD powstało.

## Kiedy się nie opłaca

DDD wymaga czasu ekspertów, warsztatów, iteracji modelu i zespołu, który chce rozumieć biznes. To inwestycja, która zwraca się tylko w określonych warunkach.

| Czynnik | DDD się opłaca | DDD się nie opłaca |
|---|---|---|
| Złożoność domeny | dużo reguł, wyjątków, zależności | CRUD, formularze, raporty |
| Przewaga konkurencyjna | system jest źródłem przewagi | system to wsparcie, standardowy proces |
| Dostęp do ekspertów | eksperci dostępni i zaangażowani | brak kontaktu z biznesem |
| Horyzont | system rozwijany latami | prototyp, jednorazowa kampania |
| Zespół | chce i umie rozmawiać z biznesem | nastawiony wyłącznie na technikę |
| Zmienność | reguły biznesowe często się zmieniają | wymagania stabilne i dobrze opisane |

Nawet w firmie, w której DDD się opłaca, nie stosuje się go wszędzie. Panel administracyjny, rejestracja użytkowników czy integracja z bramką płatności nie potrzebują bogatego modelu. Rozdział 03 pokazuje, jak zdecydować, które części systemu zasługują na pełne DDD.

## Co zapamiętać

- DDD opisał Eric Evans w 2003 roku jako odpowiedź na złożoność domeny, a nie techniki.
- Centrum jest model domeny budowany z ekspertami i odzwierciedlony w kodzie.
- Projektowanie strategiczne dzieli system i decyduje, gdzie inwestować. Projektowanie taktyczne buduje model w kodzie.
- Wzorce taktyczne to narzędzia wyrażania modelu, a nie cel.
- DDD lite, czyli same wzorce bez strategii i języka, zwykle nie rozwiązuje problemu, dla którego powstało DDD.
- DDD opłaca się przy złożonej, zmiennej domenie, która daje przewagę, z dostępem do ekspertów i długim horyzontem.

## Pytania sprawdzające

### 1. Czym jest Domain-Driven Design i jaki problem próbował rozwiązać Eric Evans w „Blue Book” z 2003 roku?

<details>
<summary>Odpowiedź</summary>

To podejście do tworzenia oprogramowania dla złożonych dziedzin, w którym centrum jest model domeny budowany wspólnie z ekspertami biznesowymi i wiernie odzwierciedlony w kodzie. Evans odpowiadał na projekty, które zawodziły nie przez technologię, tylko przez to, że programiści nie rozumieli biznesu, a model w kodzie nie odpowiadał rzeczywistości. Każda nowa reguła wymagała obejść, a komunikacja z ekspertami przypominała tłumaczenie.

Zobacz: początek rozdziału i sekcja „Problem, z którym przyszedł Evans”.

</details>

### 2. Dlaczego DDD to przede wszystkim sposób modelowania i współpracy z biznesem, a nie zestaw wzorców (encja, repozytorium, agregat)?

<details>
<summary>Odpowiedź</summary>

Bo wzorce taktyczne służą tylko do wyrażenia modelu w kodzie, a model powstaje w rozmowach z ekspertami i w decyzjach strategicznych: podziale na konteksty, języku, wyborze obszarów do inwestycji. Evans uważał część strategiczną za najważniejszą. Test praktyczny: czy ekspert rozpozna swój świat w nazwach klas i metod. Kod pełen podręcznikowych wzorców, ale z nazwami typu `RentalManager.processUpdate`, tego testu nie przejdzie.

Zobacz: sekcja „Modelowanie, a nie wzorce”.

</details>

### 3. Czym jest „DDD lite” i dlaczego stosowanie samych wzorców taktycznych bez części strategicznej zwykle zawodzi?

<details>
<summary>Odpowiedź</summary>

To termin Vaughna Vernona na stosowanie wyłącznie wzorców taktycznych, bez języka wszechobecnego, bounded contextów i świadomego wyboru subdomen. Zawodzi, bo powstaje jeden ogromny model z przeładowanymi pojęciami, nazwy wymyślają programiści, a wysiłek rozkłada się równo zamiast trafiać do core domain. Wzorce stają się celem: agregaty z tabel, repozytoria z DAO, więcej kodu bez korzyści. Same wzorce poprawiają jakość kodu, ale nie rozwiązują problemu złożoności domeny.

Zobacz: sekcja „Wzorce bez strategii”.

</details>

### 4. Kiedy DDD się nie opłaca? Jakie cechy projektu, domeny i zespołu przemawiają przeciwko niemu?

<details>
<summary>Odpowiedź</summary>

Gdy domena jest prosta (CRUD, formularze, raporty), system nie daje przewagi konkurencyjnej, nie ma dostępu do ekspertów, horyzont jest krótki (prototyp, kampania), zespół nie chce rozmawiać z biznesem albo wymagania są stabilne i dobrze opisane. Nawet tam, gdzie DDD się opłaca, stosuje się je tylko w wybranych częściach systemu, a nie w panelu administracyjnym czy integracji z bramką płatności.

Zobacz: sekcja „Kiedy się nie opłaca”.

</details>
