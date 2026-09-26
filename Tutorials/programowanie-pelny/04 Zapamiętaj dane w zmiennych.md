# Zapamiętaj dane w zmiennych

Każdy program musi gdzieś zapamiętać to, na czym pracuje: imię, kwotę, informację, czy coś już zrobiono. Ten dział pokazuje, jak w Pythonie przechowywać takie informacje i jak odróżniać ich rodzaje, np. liczbę od tekstu czy prawdę od fałszu. Po jego przeczytaniu utworzysz własne zmienne i sprawdzisz, co w nich leży. Do tej pory pisaliśmy instrukcje, które coś wypisywały lub wykonywały; teraz dostaną one dane, na których mogą pracować. W przykładzie „Wspólna Kasa” do rozlicz.py trafią imię, opis i kwota wydatku oraz informacja „czy zapłacono”, a w warsztacie w kasa.py wypiszemy je razem z typami.

```text
instrukcje (dział 03) + dane (dział 04) → program

kwota  ← 45.50   (liczba)
opis   ← "obiad" (tekst)
oplacone ← True  (prawda/fałsz)
```

**W tym dziale:**

- [Zobacz, czym jest dana](#zobacz-czym-jest-dana)
- [Nazwij swoją pierwszą zmienną](#nazwij-swoją-pierwszą-zmienną)
- [Wyobraź sobie pudełko z etykietą](#wyobraź-sobie-pudełko-z-etykietą)
- [Rozróżnij liczbę i tekst](#rozróżnij-liczbę-i-tekst)
- [Sprawdź typ danych](#sprawdź-typ-danych)
- [Użyj prawdy i fałszu](#użyj-prawdy-i-fałszu)
- [Przypisz wartość zmiennej](#przypisz-wartość-zmiennej)

**Warsztat, punkt startowy:** pliki z końca działu 03: `kasa.py` ([treść](99%20Warsztat.md#po-dziale-03)).

## Zobacz, czym jest dana

[Dana](00%20Glosariusz.md#dana) to każda informacja, na której pracuje program: imię, kwota, data, odpowiedź „tak” lub „nie”. Program bez danych nie miałby czego liczyć ani wypisać.

W arkuszu kalkulacyjnym danymi są wartości w komórkach: nazwisko w jednej, kwota w drugiej. W programie jest podobnie, tylko że dane zapisujesz wprost w kodzie albo dostajesz z zewnątrz.

```python
# poza kanonem
print("Ania")       # tekst: imię
print(45.5)         # liczba: kwota
print(True)         # prawda albo fałsz: czy zapłacono
print(45.5 + 10)    # z liczbą można liczyć
```

```text
Ania
45.5
True
55.5
```

Każda z tych trzech wartości to jedna dana, ale każda jest innego rodzaju. Rodzaj danej decyduje o tym, co program może z nią zrobić. Do liczby 45.5 da się dodać 10 albo ją podzielić. <a id="lm-24"></a>Imienia „Ania” nie da się podzielić przez 2, bo to nie ma sensu; można je co najwyżej wypisać, porównać z innym albo połączyć z innym tekstem. Prawda lub fałsz odpowiada na pytanie tak/nie.

Dane trzeba też gdzieś przechowywać, żeby użyć ich więcej niż raz. Do tego służy [zmienna](00%20Glosariusz.md#zmienna), którą poznasz w następnej sekcji. To, jak Python nazywa poszczególne rodzaje danych, [wyjaśnimy przy typach danych](#ref-45).

> **Z przymrużeniem oka:** Program bez danych to kucharz bez produktów: piec rozgrzany, fartuch wyprasowany, a obiadu i tak nie będzie.

## Nazwij swoją pierwszą zmienną

Zmienna to <a id="ref-44"></a>nazwane miejsce w pamięci programu, w którym leży jedna dana. Dzięki nazwie możesz tę daną wielokrotnie odczytać, użyć w obliczeniach albo zastąpić inną.

[Pamiętasz, że dane trzeba gdzieś przechowywać](#zobacz-czym-jest-dana), żeby użyć ich więcej niż raz. Właśnie do tego służy zmienna. Zamiast wpisywać `45.5` w kilku miejscach, nadajesz kwocie nazwę i posługujesz się nią. To trochę jak komórka w arkuszu, którą nazwałeś „kwota”, a potem odwołujesz się do niej po nazwie.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(imie, kwota, zaplacono)
kwota = 60
print(kwota + 10)
```

```text
Ania 45.5 True
70
```

Znak `=` nie oznacza tu „równa się” jak w matematyce. Znaczy: „zapisz to, co po prawej, pod nazwą po lewej”. [Dokładniej opiszemy to przy przypisaniu](#ref-47).

[Wartość zmiennej](00%20Glosariusz.md#wartość-zmiennej) może się zmieniać w trakcie działania programu, stąd nazwa: <a id="lm-25"></a>po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce. Nazwa zostaje ta sama. W „Wspólnej Kasie” takie zmienne w `rozlicz.py` opisują pojedynczy wydatek: kto zapłacił, ile i czy już się rozliczył.

> **Wtręt:** Marta wpisała kwotę za zakupy, `45.5`, bezpośrednio w pięciu liniach programu. Potem okazało się, że paragon opiewał na `54.5`, więc poprawiła ją w czterech miejscach i przeoczyła piąte. Komputer nie zgłosił błędu, tylko wykonał wszystko dokładnie: cztery obliczenia zgodne z paragonem i jedno nie. Gdyby kwota siedziała w zmiennej `kwota`, wystarczyłaby jedna poprawka.

> **Pułapka: Zmiana wartości zmienia też typ.** Po `kwota = 60` zmienna z liczby dziesiętnej (`45.5`) staje się liczbą całkowitą. Program nie zgłasza błędu, więc dalsze wyniki mogą wyglądać inaczej, niż się spodziewasz (np. `70` zamiast `70.0`).

## Wyobraź sobie pudełko z etykietą

Zmienną można porównać do pudełka z etykietą: etykieta to nazwa, a w środku leży jedna dana, czyli wartość zmiennej (to, co aktualnie jest w pudełku). Program szuka pudełka po etykiecie i zagląda do środka.

```text
etykieta: kwota      etykieta: imie
┌──────────┐         ┌──────────┐
│   45.5   │         │  "Ania"  │
└──────────┘         └──────────┘
```

Porównanie tłumaczy trzy rzeczy. Pudełko mieści jedną wartość naraz, więc nowa wartość wypiera starą, jak w przypadku zmiany kwoty z poprzedniej sekcji. Etykieta zostaje, zmienia się tylko zawartość. Wreszcie każde pudełko żyje własnym życiem: kopia wartości do drugiego pudełka nie łączy ich na stałe.

```python
# poza kanonem
kwota_stara = 45.5
kwota = kwota_stara
kwota = 60
print(kwota_stara, kwota)
```

```text
45.5 60
```

Zmiana `kwota` nie ruszyła `kwota_stara`, bo do drugiego pudełka trafiła kopia wartości.

Obraz jest uproszczony: pod spodem Python działa nieco inaczej, ale na tym etapie to nie ma znaczenia. Ważna konsekwencja: etykieta ma być czytelna. W „Wspólnej Kasie” pudełko `kwota` jest zrozumiałe, a `x` zmusza do zgadywania, co w środku.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dodajemy trzy zmienne i wypisujemy ich zawartość.

```diff
 print("Wspólna Kasa")
+nazwa_wyjazdu = "Mazury"
+kwota_wydatku = 45.5
+czy_oplacone = True
+print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
```

<details>
<summary>Cały plik <code>kasa.py</code> po zmianie</summary>

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
nazwa_wyjazdu = "Mazury"
kwota_wydatku = 45.5
czy_oplacone = True
print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
```

</details>

**Krok 2. Uruchom.** Uruchamiamy skrypt.

```bash
python kasa.py
```

Wynik:

```text
Wspólna Kasa
Mazury 45.5 True
```

> **Z życia wzięte:** W skrypcie do przetwarzania zamówień, który dostałem w spadku, kluczowe wartości siedziały w zmiennych `x`, `x2` i `tmp`. Musiałem zmienić próg, od którego zamówienie trafia do ręcznej weryfikacji, i przez pół dnia ustalałem, która z nich go przechowuje. Dopiero prześledzenie każdego użycia pokazało, że to `x2`, a `tmp` trzyma coś zupełnie innego. Zmieniłem nazwy na `prog_weryfikacji` i `liczba_zamowien`, a kolejna zmiana progu zajęła kilka minut. Od tamtej pory nazywam zmienne tak, żeby etykieta mówiła, co leży w środku.

**Ilustracja:** _Nowa wartość wypiera starą, ale kopia w drugim pudełku zostaje._

Tekst alternatywny: Osoba wkłada koralową kartkę do jednego z dwóch pudełek z etykietami; stara żółta kartka wypada z pudełka, a w drugim pudełku nadal leży jej kopia.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Jasny pokój z drewnianą półką. Na półce stoją obok siebie dwa kartonowe pudełka z doczepionymi papierowymi etykietami (puste kartki, bez tekstu). Uśmiechnięta osoba o prostych kształtach wkłada do pierwszego pudełka nową koralową kartkę, a stara musztardowa kartka wypada z niego i leży obok. Drugie pudełko stoi spokojnie i widać w nim wystającą musztardową kartkę, identyczną jak ta, która wypadła: to kopia, której zmiana w pierwszym pudełku nie dotknęła.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/04-wyobraź-sobie-pudełko-z-etykietą-1.png`

</details>

## Rozróżnij liczbę i tekst

Liczba to wartość, na której program liczy. Tekst to ciąg znaków, który program przechowuje, wypisuje, porównuje i skleja. Zapis decyduje o tym, z czym mamy do czynienia: `45.5` bez cudzysłowu to liczba, a <a id="lm-27"></a>`"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5.

| Zapis | Co to jest | Można dzielić? |
|---|---|---|
| `45.5` | liczba | tak |
| `"45.5"` | tekst | nie |
| `"Ania"` | tekst | nie |

W programie ułamek dziesiętny zapisujemy z kropką, nie z przecinkiem, [tak jak `kwota = 45.5` w „Wspólnej Kasie”](#nazwij-swoją-pierwszą-zmienną).

```python
kwota = 45.5
imie = "Ania"
print(kwota / 2)
print(imie)
```

```text
22.75
Ania
```

Liczbę można podzielić, tekstu nie. To ta sama myśl co [imię „Ania” nie do podzielenia przez 2](#lm-24). Python zatrzyma się z komunikatem `TypeError`. 

Uwaga na plus: przy liczbach dodaje, a przy tekstach skleja je w jeden. [Tym zajmiemy się osobno.](05%20Podejmuj%20decyzje%20w%20programie.md#ref-52)

Konsekwencja: kwotę zapisaną w cudzysłowie program potraktuje jak napis, nie jak pieniądze. Nazwę tej cechy danych, czyli typ, omówimy w następnej sekcji.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Dopisujemy dzielenie tekstu przez 2, żeby zobaczyć błąd.

```diff
 print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
+print(nazwa_wyjazdu / 2)
```

<details>
<summary>Cały plik <code>kasa.py</code> po zmianie</summary>

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
nazwa_wyjazdu = "Mazury"
kwota_wydatku = 45.5
czy_oplacone = True
print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
print(nazwa_wyjazdu / 2)
```

</details>

**Krok 2. Uruchom.** Python wykonuje linie po kolei i zatrzymuje się na dzieleniu tekstu.

```bash
python kasa.py
```

Zobaczysz błąd (celowy, poprawimy go):

```text
Wspólna Kasa
Mazury 45.5 True
Traceback (most recent call last):
  File "/home/ania/wspolna_kasa/kasa.py", line 7, in <module>
    print(nazwa_wyjazdu / 2)
          ~~~~~~~~~~~~~~^~~
TypeError: unsupported operand type(s) for /: 'str' and 'int'
```

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-zapamiętaj-dane-w-zmiennych)_

> **Wtręt:** Marta wpisała kwotę jako `"45.5"`, bo w arkuszu tak oznaczała tekstowe komórki, i kazała programowi podzielić ją przez 2. Zamiast `22.75` dostała czerwony `TypeError`. Tym razem nie cofnęła rąk: sprawdziła zapis, zauważyła cudzysłów, usunęła go i wynik się pojawił. Dla programu `"45.5"` to były cztery znaki, a nie pieniądze.

## Sprawdź typ danych

<a id="ref-53"></a>[Typ danych](00%20Glosariusz.md#typ-danych) to rodzaj wartości, który mówi Pythonowi, czym ta wartość jest i jakie działania są na niej dozwolone. [Wcześniej pisaliśmy po prostu „rodzaj danych”](#zobacz-czym-jest-dana), teraz mamy na to fachową nazwę.

Typ ma każda wartość, także ta ukryta w zmiennej. Python rozpoznaje go po zapisie: cudzysłów oznacza tekst, cyfry z kropką ułamek, a `True` lub `False` prawdę albo fałsz. Dlatego `"45.5"` to [tylko cztery znaki: 4, 5, kropka, 5](#lm-27), a nie pieniądze. Typ sprawdzisz funkcją `type()`.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(type(imie))
print(type(kwota))
print(type(zaplacono))
```

```text
<class 'str'>
<class 'float'>
<class 'bool'>
```

Słowo `class` na razie pomiń, ważna jest nazwa po nim. <a id="ref-45"></a>Oto podstawowe typy Pythona:

| Nazwa w Pythonie | Co to jest | Przykład |
|---|---|---|
| `str` | tekst | `"Ania"` |
| `int` | liczba całkowita | `3` |
| `float` | liczba z ułamkiem | `45.5` |
| `bool` | prawda lub fałsz | `True` |

Typ decyduje o tym, co program może zrobić z wartością. Dlatego [imienia nie podzielisz przez 2](#lm-24), a kwotę tak. Typem `bool` zajmiemy się osobno, w kolejnej sekcji.

Konsekwencja: gdy program zachowuje się dziwnie, jedno z pierwszych pytań brzmi „jakiego typu jest ta wartość?”.

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Zamiast dzielenia tekstu przez 2 sprawdzamy typy zmiennych.

```diff
 print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
-print(nazwa_wyjazdu / 2)
+print(type(nazwa_wyjazdu))
+print(type(kwota_wydatku))
+print(type(czy_oplacone))
```

<details>
<summary>Cały plik <code>kasa.py</code> po zmianie</summary>

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
nazwa_wyjazdu = "Mazury"
kwota_wydatku = 45.5
czy_oplacone = True
print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
print(type(nazwa_wyjazdu))
print(type(kwota_wydatku))
print(type(czy_oplacone))
```

</details>

**Krok 2. Uruchom.** Uruchamiamy poprawiony skrypt.

```bash
python kasa.py
```

Wynik:

```text
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>
```

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-zapamiętaj-dane-w-zmiennych)_

<details>
<summary>Na marginesie: Rakieta, która pomyliła typy liczb</summary>

W 1996 roku pierwsza rakieta Ariane 5 rozpadła się po niespełna 40 sekundach lotu. Komisja badająca wypadek wskazała, że oprogramowanie zamieniało liczbę z ułamkiem, zapisaną na 64 bitach, na liczbę całkowitą zapisaną na 16 bitach. Wartość była za duża, by się w niej zmieścić, więc obliczenia zakończyły się błędem. Typ danych to zatem nie tylko szkolna etykietka: bywa, że o wszystkim decyduje to, w jakim „pojemniku” trzymamy liczbę.

Źródło: [Ariane flight V88 (Wikipedia)](https://en.wikipedia.org/wiki/Ariane_flight_V88)

</details>

## Użyj prawdy i fałszu

[Wartość logiczna](00%20Glosariusz.md#wartość-logiczna) to dana, która <a id="ref-58"></a>ma tylko dwie możliwe wartości: prawda albo fałsz. W Pythonie zapisujesz je jako `True` i `False`, a ich typ to `bool`.

Pasuje do każdej odpowiedzi „tak albo nie”: czy wydatek jest zapłacony, czy kwota jest większa od zera. Nie ma nic pomiędzy. W arkuszu to odpowiednik pola wyboru: zaznaczone albo nie.

Zapisuje się je z wielkiej litery i bez cudzysłowu. [Ta sama zasada, co przy `"45.5"`](#lm-27): `True` to wartość logiczna, a `"True"` w cudzysłowie to tylko tekst z czterech liter.

```python
zaplacono = True
print(zaplacono)
zaplacono = False
print(zaplacono)
print(type(zaplacono))
```

```text
True
False
<class 'bool'>
```

[Zmienną logiczną podmieniasz jak każdą inną: po drugim przypisaniu `True` znika](#lm-25), a jej miejsce zajmuje `False`.

Konsekwencja: taka wartość służy programowi do podejmowania decyzji. Na podstawie `zaplacono` program będzie mógł wybrać, czy przypomnieć o długu. [Jak to zapisać, pokażemy przy instrukcji warunkowej](05%20Podejmuj%20decyzje%20w%20programie.md#ref-61).

> **Warsztat: zrób u siebie**

**Krok 1. Zmień plik `kasa.py`.** Podmieniamy wartość logiczną na False i wypisujemy ją.

```diff
 print(type(czy_oplacone))
+czy_oplacone = False
+print(czy_oplacone)
```

<details>
<summary>Cały plik <code>kasa.py</code> po zmianie</summary>

```python
# kasa.py - pierwszy skrypt Wspólnej Kasy
print("Wspólna Kasa")
nazwa_wyjazdu = "Mazury"
kwota_wydatku = 45.5
czy_oplacone = True
print(nazwa_wyjazdu, kwota_wydatku, czy_oplacone)
print(type(nazwa_wyjazdu))
print(type(kwota_wydatku))
print(type(czy_oplacone))
czy_oplacone = False
print(czy_oplacone)
```

</details>

**Krok 2. Uruchom.**

```bash
python kasa.py
```

Wynik:

```text
Wspólna Kasa
Mazury 45.5 True
<class 'str'>
<class 'float'>
<class 'bool'>
False
```

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#04-zapamiętaj-dane-w-zmiennych)_

> **Z przymrużeniem oka:** Zapytany, czy współlokator zwrócił pieniądze, program odpowiada `True` albo `False`. Odpowiedź „no, prawie oddał” nie należy do typu `bool`, choć w prawdziwych rozliczeniach zdarza się najczęściej.

## Przypisz wartość zmiennej

[Przypisanie](00%20Glosariusz.md#przypisanie) to instrukcja, która zapisuje wartość pod nazwą zmiennej. Dzięki niej program zapamiętuje daną i może do niej wrócić w dalszej części kodu.

<a id="ref-47"></a>Zapisujesz je znakiem `=`. Po lewej stoi nazwa, po prawej wartość: `kwota = 45.5`. To nie jest równanie ze szkoły, tylko polecenie: „weź to, co po prawej, i połóż pod nazwą po lewej”. Jeśli zmienna jeszcze nie istniała, Python ją tworzy. Jeśli istniała, podmienia jej wartość, [tak jak przy pudełku z etykietą](#wyobraź-sobie-pudełko-z-etykietą).

Przypisanie działa od prawej do lewej i tylko w chwili wykonania. Gdy po prawej stronie stoi inna zmienna, Python kopiuje jej aktualną wartość. Późniejsza zmiana oryginału nie rusza kopii.

```python
kwota = 45.5
kwota_stara = kwota
kwota = 60
print(kwota)
print(kwota_stara)
```

```text
60
45.5
```

Linia `kwota_stara = kwota` skopiowała 45.5 w chwili wykonania. Dopiero potem `kwota = 60` zmieniła tylko `kwota`.

Konsekwencja: kolejność linii ma znaczenie. Program czyta kod od góry, więc wartość zmiennej zależy od tego, które przypisanie wykonało się ostatnie.

> **Z życia wzięte:** W skrypcie do wystawiania ofert na górze pliku napisałem `cena_brutto = cena * 1.23`, a niżej, po pobraniu aktualnego cennika, podmieniałem `cena`. W ofertach lądowały jednak stare kwoty brutto. Założyłem bez sprawdzenia, że `cena_brutto` sama się przeliczy, tymczasem przypisanie wykonało się raz, w chwili, gdy `cena` miała jeszcze starą wartość. Przeniosłem obliczenie pod aktualizację ceny. Od tamtej pory czytam takie linie jako jednorazowe polecenie, a nie stałą zależność.

## Co zapamiętać

- Dana to informacja, na której pracuje program, a jej rodzaj (tekst, liczba, prawda/fałsz) określa, co można z nią zrobić.
- Zmienna to nazwa, pod którą program przechowuje daną, żeby móc jej użyć wielokrotnie i w razie potrzeby zmienić.
- Zmienna to pudełko z etykietą: nazwa zostaje, w środku jest jedna wartość, którą można podmienić, a kopie są niezależne.
- Cudzysłów zmienia rodzaj danych: 45.5 to liczba, którą można dzielić, a "45.5" to tekst, którego dzielić się nie da.
- Typ danych to rodzaj wartości (str, int, float, bool), który decyduje o tym, jakie działania są na niej możliwe.
- Wartość logiczna (`bool`) to `True` albo `False`, zapisywane z wielkiej litery i bez cudzysłowu, a program używa jej do podejmowania decyzji.
- Przypisanie `=` to polecenie zapisania wartości z prawej strony pod nazwą z lewej, a o wartości zmiennej decyduje ostatnie wykonane przypisanie.

## Pytania sprawdzające

### 19. Czym jest dana w programie?

<details>
<summary>Odpowiedź</summary>

Dana to pojedyncza informacja, na której pracuje program, na przykład imię, kwota albo odpowiedź „tak/nie”. Program przyjmuje dane, przetwarza je i wypisuje wynik. Rodzaj danej decyduje o tym, jakie działania mają sens: liczby można dodawać i dzielić, a imion nie.

Zobacz: [sekcja „Zobacz, czym jest dana”](#zobacz-czym-jest-dana).

</details>

### 20. Czym jest zmienna?

<details>
<summary>Odpowiedź</summary>

Zmienna to nazwane miejsce w pamięci programu, w którym leży jedna dana. Dzięki nazwie można tę daną odczytać, użyć w obliczeniach albo zastąpić inną. Wartość zmiennej może się zmieniać w trakcie działania programu, a nazwa zostaje ta sama.

Zobacz: [sekcja „Nazwij swoją pierwszą zmienną”](#nazwij-swoją-pierwszą-zmienną).

</details>

### 21. Jak można porównać zmienną do pudełka z etykietą?

<details>
<summary>Odpowiedź</summary>

Zmienna przypomina pudełko z etykietą: etykieta to nazwa, a w środku leży jedna wartość. Po nazwie program znajduje pudełko i odczytuje zawartość. Nową wartość można włożyć, wtedy stara znika, a etykieta zostaje. Skopiowanie wartości do drugiego pudełka nie łączy ich na stałe.

Zobacz: [sekcja „Wyobraź sobie pudełko z etykietą”](#wyobraź-sobie-pudełko-z-etykietą).

</details>

### 22. Czym różni się liczba od tekstu w programie?

<details>
<summary>Odpowiedź</summary>

Liczba to wartość, na której program wykonuje obliczenia, a tekst to ciąg znaków, który program przechowuje, wypisuje i skleja. O rodzaju decyduje zapis: 45.5 bez cudzysłowu to liczba, a "45.5" w cudzysłowie to tekst. Liczbę można podzielić, a tekstu nie, więc pomylenie ich kończy się błędem albo złym wynikiem.

Zobacz: [sekcja „Rozróżnij liczbę i tekst”](#rozróżnij-liczbę-i-tekst).

</details>

### 23. Czym jest typ danych?

<details>
<summary>Odpowiedź</summary>

Typ danych to rodzaj wartości, który określa, czym ona jest i co można z nią zrobić. Podstawowe typy Pythona to tekst (str), liczba całkowita (int), liczba z ułamkiem (float) i prawda/fałsz (bool). Typ wartości sprawdzisz funkcją type().

Zobacz: [sekcja „Sprawdź typ danych”](#sprawdź-typ-danych).

</details>

### 24. Co to jest wartość logiczna prawda/fałsz?

<details>
<summary>Odpowiedź</summary>

Wartość logiczna to dana, która może mieć tylko dwie wartości: prawda (`True`) albo fałsz (`False`). Służy do zapisania odpowiedzi „tak albo nie”, np. czy wydatek został zapłacony. Jej typ w Pythonie nazywa się `bool`.

Zobacz: [sekcja „Użyj prawdy i fałszu”](#użyj-prawdy-i-fałszu).

</details>

### 25. Do czego służy przypisanie wartości do zmiennej?

<details>
<summary>Odpowiedź</summary>

Przypisanie zapisuje wartość pod nazwą zmiennej, dzięki czemu program może ją zapamiętać i użyć później. Zapisuje się je znakiem `=`: po lewej nazwa, po prawej wartość. Jeśli zmienna już istniała, jej stara wartość zostaje zastąpiona nową. Przy przypisaniu innej zmiennej kopiowana jest jej aktualna wartość, więc późniejsza zmiana oryginału nie wpływa na kopię.

Zobacz: [sekcja „Przypisz wartość zmiennej”](#przypisz-wartość-zmiennej).

</details>
