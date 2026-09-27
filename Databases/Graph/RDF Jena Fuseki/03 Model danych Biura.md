# Model danych Biura

Znasz już trójki, literały, [grafy nazwane](00%20Glosariusz.md#graf-nazwany) i [słownik](00%20Glosariusz.md#słownik) bpc, ale brakuje Ci gotowego modelu, do którego można załadować dane. Ten dział go buduje: zdefiniujesz klasy i własności Biura Paradoksów Czasowych, przygotujesz dane CSV z celowymi sprzecznościami i napiszesz funkcję iri_for, która zamienia klucze na stabilne IRI i bezpiecznie znosi puste lub błędne wartości. Po lekturze opiszesz każdą kolumnę CSV jako [wiersz mapowania](00%20Glosariusz.md#wiersz-mapowania) na trójki, tak by sześć analiz Biura z działu 01 (m.in. sprzeczne wizyty i łańcuch spotkań) miało na czym pracować. Dziedziny łączą się tu tak: model określa, co ma powstać, CSV dostarcza surowe wiersze, a Python przekłada jedno na drugie.

```text
model (klasy, własności) -- określa predykaty i typy --> mapowanie kolumn
CSV (wiersze) -- klucze --> iri_for -- IRI zasobów --> mapowanie kolumn
mapowanie kolumn -- tworzy --> trójki w grafach
```

**W tym dziale:**

- [Klasy i własności Biura](#klasy-i-własności-biura)
- [Wizyta jako węzeł, nie trójka](#wizyta-jako-węzeł-nie-trójka)
- [Słowniki, przestrzenie i grafy modelu](#słowniki-przestrzenie-i-grafy-modelu)
- [Wiersze CSV dla sześciu analiz](#wiersze-csv-dla-sześciu-analiz)
- [Klucze jako IRI i połączenia](#klucze-jako-iri-i-połączenia)
- [Wiersz mapowania kolumn wizyty](#wiersz-mapowania-kolumn-wizyty)
- [Znaki specjalne w kluczach IRI](#znaki-specjalne-w-kluczach-iri)
- [Pusta komórka i zła data](#pusta-komórka-i-zła-data)

## Klasy i własności Biura

Biuro ma sześć płaskich klas i tylko tyle własności, ile czytają analizy. Klasy i własności leżą w `bpc:`, a instancje w `ex:`, zgodnie z [rozdziałem z sekcji [Słownik bpc a IRI instancji]](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#słownik-bpc-a-iri-instancji).

Epokę opisujemy przedziałem z [OWL-Time](00%20Glosariusz.md#owl-time): to gotowy słownik W3C do opisu czasu, a `time:Interval` to przedział z początkiem i końcem.

| Klasa | Własności | Wskazują na |
|---|---|---|
| `bpc:Podroznik` | `bpc:odwiedzil` | wizyta |
| `bpc:Wizyta` | `bpc:epoka`, `bpc:linia`, `bpc:od`, `bpc:do` | epoka, linia czasu, daty `xsd:date` |
| `bpc:Epoka` | `rdfs:label`, granice z OWL-Time | nazwa, przedział |
| `bpc:Artefakt` | `bpc:powstal` | data powstania, `xsd:date` |
| `bpc:Spotkanie` | `bpc:uczestnik`, `bpc:naWizycie` | podróżnik, wizyta |
| `bpc:Raport` | `bpc:opisuje` | wizyta |

Każda własność ma powód. Artefakt ma datę powstania, bo <a id="lm-10"></a>analiza „artefakt przed powstaniem” porównuje ją z datą wizyty. Spotkanie wskazuje wizytę, bo analiza szukająca spotkań bez wizyty potrzebuje tej krawędzi.

```turtle
bpc:Artefakt a rdfs:Class .
bpc:Spotkanie a rdfs:Class .
bpc:powstal a rdf:Property ;
  rdfs:domain bpc:Artefakt ;
  rdfs:range  xsd:date .
bpc:naWizycie a rdf:Property ;
  rdfs:domain bpc:Spotkanie ;
  rdfs:range  bpc:Wizyta .
# bpc:Epoka, bpc:Raport, bpc:uczestnik, bpc:opisuje analogicznie
...
```

[Domain i range niczego nie odrzucają](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#typy-etykiety-domain-i-range), więc złą datę wychwyci dopiero walidacja. To, kiedy wizyta, spotkanie i raport powinny być osobnymi węzłami, a kiedy pojedynczymi trójkami, rozstrzygniemy osobno.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-model-danych-biura)_

## Wizyta jako węzeł, nie trójka

Zasób zamiast pojedynczej trójki wybierasz wtedy, gdy zdarzenie ma własne cechy (daty, epokę, linię) albo gdy inne rzeczy muszą się do niego odwoływać. Taki węzeł to [węzeł zdarzenia](00%20Glosariusz.md#węzeł-zdarzenia): zasób z własnym IRI, który zbiera wszystkie fakty o jednym zdarzeniu.

Zapis `ex:p1 bpc:odwiedzil ex:epoka_rzym` to jedna trójka. Nie ma w niej miejsca na daty ani linię, a przecież `bpc:od` i `bpc:do` muszą mieć podmiot. Tym podmiotem jest wizyta. Tak samo w [relacji wielostronnej](00%20Glosariusz.md#relacja-wielostronna) (spotkanie ma kilku uczestników i wizytę) nie da się zmieścić wszystkiego w jednej trójce.

Węzeł jest potrzebny, gdy spełniony jest którykolwiek z warunków:

| Warunek | Przykład w Biurze |
|---|---|
| Zdarzenie ma własne atrybuty | wizyta: `bpc:epoka`, `bpc:linia`, `bpc:od`, `bpc:do` |
| Inne zasoby się do niego odwołują | `bpc:naWizycie`, `bpc:opisuje` |
| Uczestniczy więcej niż jeden zasób | spotkanie z `bpc:uczestnik` |
| Trzeba je policzyć lub porównać | analiza nakładających się wizyt |

<a id="ref-29"></a>Pojedyncza trójka wystarcza dla stałej cechy bez własnych atrybutów, np. `ex:artefakt1 bpc:powstal "0100-01-01"^^xsd:date`.

Zysk: raport wskazuje konkretną wizytę, a [analiza zestawia jej daty z datą artefaktu](#lm-10). Koszt: więcej trójek i jeden IRI do wygenerowania na wiersz. Wizyta z CSV ma klucz `id`, więc IRI jest gotowy.

```turtle
ex:w1 a bpc:Wizyta ;
  bpc:epoka ex:epoka_rzym ;
  bpc:linia ex:linia_a ;
  bpc:od "0050-03-01"^^xsd:date .
ex:p1 bpc:odwiedzil ex:w1 .
```

## Słowniki, przestrzenie i grafy modelu

Spójny model składa się z trzech decyzji: skąd pochodzą terminy, gdzie leżą IRI i w którym grafie ląduje która trójka. Każda decyzja dotyczy innej warstwy i ma jedno miejsce.

| Warstwa | Wybór w Biurze | Uzasadnienie |
|---|---|---|
| Słownik | własny `bpc:` (klasy i własności), OWL-Time dla epok, PROV-O dla pochodzenia | gotowy termin bierzemy tylko tam, gdzie analiza lub konwerter go używa |
| Przestrzeń nazw | `bpc:` dla schematu, `ex:` dla instancji | schemat i dane nie mieszają się w jednej przestrzeni |
| Graf | jeden graf nazwany na linię czasu, osobny graf provenance | linię niesie nazwa grafu, a metadane konwersji nie zanieczyszczają danych o wizytach |

PROV-O to standardowy słownik W3C do opisu pochodzenia danych: kto, jaką aktywnością i z czego coś wytworzył. Stąd nazwa grafu `ex:provenance`, czyli grafu z metadanymi konwersji. [Pełne URI jego terminów podaliśmy w sekcji o PROV-O](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#pełne-uri-terminów-prov-o).

Wspólne fakty, czyli definicje klas i własności oraz epoki takie jak `ex:epoka_rzym`, zostają w grafie domyślnym. To graf [datasetu](00%20Glosariusz.md#dataset) bez nazwy: trafiają do niego trójki bez wskazanego grafu, a w [TriG](00%20Glosariusz.md#trig) zapisuje się go poza blokami z nazwą. Nie należy do żadnej linii, więc każda linia może się do niego odwoływać. Wizyty, spotkania i raporty trafiają do grafu swojej linii, a opis konwersji CSV do `ex:provenance`. [Kolumny CSV przypiszemy do własności w tabeli mapowania](#ref-33).

Konsekwencja: cały model mieści się w jednym datasecie `biuro` i jednym pliku TriG. Kolejne kroki, czyli IRI, mapowanie i konwerter, wypełniają szkielet z trzema miejscami.

```turtle
# graf domyślny: słownik bpc: i epoki wspólne
bpc:Wizyta a rdfs:Class .
ex:epoka_rzym a time:Interval ; ...
ex:linia_a { ex:w1 a bpc:Wizyta ; bpc:linia ex:linia_a ; ... }
ex:linia_b { ex:w2 a bpc:Wizyta ; bpc:linia ex:linia_b ; ... }
ex:provenance { ... }
```

## Wiersze CSV dla sześciu analiz

Model już stoi, więc teraz potrzebujemy danych, które da się przez niego przepuścić. Każda z sześciu analiz ma wynik tylko wtedy, gdy w plikach leży wiersz celowo zepsuty w jeden określony sposób. Zapisujemy sześć plików w `dane/`: `podroznicy.csv`, `epoki.csv`, `wizyty.csv`, `artefakty.csv`, `spotkania.csv` i `raporty.csv`.

| Analiza | Wiersze, które ją uruchamiają |
|---|---|
| sprzeczne wizyty | `p1` jest w `w1` (linia A) i `w2` (linia B) w nakładających się dniach |
| łańcuch spotkań | `s1`, `s2`, `s3` łączą `p1`→`p2`→`p3`→`p4` |
| artefakt przed powstaniem | `a1` ma `powstal` 0150-01-01, a jego wizyta `w1` kończy się w 0100 |
| braki | `w6` bez daty `do`, `s4` bez wizyty |
| porównanie linii | `w4` (A) i `w5` (B) opisują to samo, `w1`–`w3` tylko jedną linię |
| rozbieżny raport | `r1` opisuje `w1` z końcem 0100-03-20, a `wizyty.csv` ma 0100-03-10 |

Wizyta `w1` służy dwóm analizom, ale każda czyta z niej co innego: [artefakt porównuje datę powstania `a1` z jej datami](#lm-10), raport porównuje koniec z `r1`. Klucze to zwykłe napisy bez prefiksów, IRI zbudujemy z nich w konwerterze. Pusta komórka `do` w `w6` i pusta `wizyta` w `s4` są zamierzone: brak to inny przypadek niż błąd.

```text
id,podroznik,epoka,linia,od,do
w1,p1,rzym,linia_a,0100-03-01,0100-03-10
w2,p1,rzym,linia_b,0100-03-05,0100-03-12
w6,p4,rzym,linia_b,0100-06-01,
```

Daty są w formacie ISO, więc [później dostaną typ `xsd:date`](#ref-37).

## Klucze jako IRI i połączenia

[Klucze z CSV mamy już w plikach](#wiersze-csv-dla-sześciu-analiz), więc czas zamienić je w adresy. <a id="ref-36"></a>Klucz główny wiersza staje się końcówką [IRI](00%20Glosariusz.md#iri) zasobu w przestrzeni `ex:`, a klucz obcy to komórka, z której budujesz IRI innego wiersza i wpisujesz je jako drugi koniec trójki.

Wiersz `w1,p1,rzym,...` z `wizyty.csv` daje zasób `ex:w1`. Kolumna `epoka` zawiera klucz obcy `rzym`. Budujemy z niego dokładnie to IRI, które powstałoby z `id` w `epoki.csv`, i <a id="lm-13"></a>dostajemy trójkę `ex:w1 bpc:epoka ex:epoka_rzym`: klucz obcy jest tu obiektem.

Kierunek zależy od wybranej własności. Kolumna `podroznik` wskazuje zasób klasy `bpc:Podroznik` i daje `ex:p1 bpc:odwiedzil ex:w1`: klucz obcy jest podmiotem, a obiektem klucz główny wiersza. <a id="lm-14"></a>Połączenie działa w obu przypadkach, bo oba wiersze dają identyczny adres. [Zapis tego w tabeli mapowania pokażemy w następnym kroku](#ref-40). IRI z kluczy budujemy tak, jak zapowiadaliśmy przy plikach CSV:

```python
EX = "http://example.org/id/"

def iri_for(key, kind=""):
    return EX + (f"{kind}_{key}" if kind else key)

row = {"id": "w1", "podroznik": "p1", "epoka": "rzym"}
w = iri_for(row["id"])
print(f"<{w}> bpc:epoka <{iri_for(row['epoka'], 'epoka')}> .")
print(f"<{iri_for(row['podroznik'])}> bpc:odwiedzil <{w}> .")
```

```text
<http://example.org/id/w1> bpc:epoka <http://example.org/id/epoka_rzym> .
<http://example.org/id/p1> bpc:odwiedzil <http://example.org/id/w1> .
```

Klucze `p1` i `w1` są unikalne, więc bez przedrostka. Klucz `rzym` mógłby zderzyć się z innym zasobem, dlatego epoka dostaje `epoka_`, zgodnie z `ex:epoka_rzym`.

### Dlaczego nie z etykiety

Etykieta, np. imię z kolumny `imie`, jest atrybutem: może się zmienić, powtórzyć u dwóch podróżników albo zawierać spacje i polskie znaki. IRI z niej zmieniłoby się przy poprawce literówki, a trójki wskazujące na stary adres straciłyby cel. Klucz jest stały, więc etykietę zapisujemy osobno jako `rdfs:label`. Klucze ze spacją i znakami spoza ASCII [omówimy przy kodowaniu IRI](#znaki-specjalne-w-kluczach-iri).

> **Pułapka: Brak referencji: IRI bez węzła docelowego.** Trójka `ex:w1 bpc:epoka ex:epoka_rzym` powstaje z samej komórki, a RDF nie ma kluczy obcych. Literówka w kolumnie `epoka` (np. `rzm`) daje poprawną trójkę wskazującą na zasób bez żadnych własności. Fuseki tego nie zgłosi, a zapytania po cichu gubią wiersz. Trzeba to wyłapać osobnym zapytaniem kontrolnym albo walidacją (SHACL).

## Wiersz mapowania kolumn wizyty

Wiersz mapowania mówi, co powstaje z jednej kolumny CSV, i ma sześć pól: subject, predicate, object, typ RDF, słownik i uzasadnienie. [Tabela mapowania](00%20Glosariusz.md#tabela-mapowania) to lista takich wierszy dla jednego pliku. Tak dotrzymujemy obietnicy: <a id="ref-33"></a>kolumny przypisujemy do własności, a daty dostają typ `xsd:date`.

Słownik to zestaw klas i własności pod wspólnym prefiksem; `bpc:` jest własnym słownikiem projektu. Pole „słownik” wskazuje, skąd pochodzi orzeczenie.

<a id="ref-40"></a>Dla `wizyty.csv` (`id,podroznik,epoka,linia,od,do`) tabela wygląda tak:

<a id="ref-37"></a>

```python
# {kolumna}: (subject, predicate, object, typ RDF, słownik, uzasadnienie)
mapping = {
  "id":        ("ex:{id}", "rdf:type", "bpc:Wizyta", "IRI", "bpc", "wizyta to węzeł z atrybutami"),
  "podroznik": ("ex:{podroznik}", "bpc:odwiedzil", "ex:{id}", "IRI", "bpc", "klucz obcy; podmiot to bpc:Podroznik"),
  "epoka":     ("ex:{id}", "bpc:epoka", "ex:epoka_{epoka}", "IRI", "bpc", "klucz obcy jako obiekt"),
  "linia":     ("ex:{id}", "bpc:linia", "{linia}", "xsd:string", "bpc", "tekst; graf wybiera ta sama komórka"),
  "od":        ("ex:{id}", "bpc:od", "{od}", "xsd:date", "bpc", "analizy porównują daty"),
  "do":        ("ex:{id}", "bpc:do", "{do}", "xsd:date", "bpc", "koniec wizyty, ta sama zasada"),
}
```

Pola `subject` i `object` to szablony: `{id}` podmieni wartość komórki, a IRI zbuduje `iri_for`. <a id="lm-15"></a>Kolumna `id` daje dwie rzeczy naraz: adres wizyty i jej klasę `bpc:Wizyta`. Kolumna `podroznik` zawiera klucz podróżnika, więc szablon `ex:{podroznik}` wskazuje zasób klasy `bpc:Podroznik`.

Uzasadnienie nie jest ozdobą. <a id="lm-16"></a>Gdy za miesiąc ktoś zapyta, czemu `linia` to napis, a nie zasób, odpowiedź stoi w tabeli. Daty muszą być `xsd:date`, bo [inaczej porównanie w analizie zadziała na napisach](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#lm-5).

Co zrobić z pustą komórką albo błędną datą, [opiszemy przy obsłudze braków](#ref-44). <a id="ref-34"></a>[Jeden wiersz przeprowadzimy przez całą tabelę w kolejnym kroku](04%20Konwersja%20CSV%20do%20TriG.md#ref-45).

> **Pułapka: Literał bez jawnego typu to xsd:string.** Szablon `{od}` jest tylko tekstem; jeśli generator zapisze go jako zwykły literał (`"2020-01-01"`) bez `^^xsd:date`, w RDF to `xsd:string`. Porównania i `FILTER` po dacie nie zadziałają jak na datach, a literały o różnych typach nie są sobie równe. Typ z kolumny „typ RDF” musi trafić do serializacji.

## Znaki specjalne w kluczach IRI

[Konwerter będzie budował z kluczy adresy](#klucze-jako-iri-i-połączenia), więc `iri_for` musi poradzić sobie z kluczem, którego nie da się wpisać do IRI wprost: spacją, `/`, `#` albo polskimi literami. Klucz kodujemy jako [kodowanie procentowe](00%20Glosariusz.md#kodowanie-procentowe): każdy bajt spoza bezpiecznego zestawu zapisujemy jako `%` i dwie cyfry szesnastkowe, po zamianie tekstu na UTF-8. Do tego dochodzi normalizacja Unicode do postaci NFC, bo „Ż" można zapisać jednym znakiem albo literą Z z osobną kropką, a to byłyby dwa różne adresy.

```python
from urllib.parse import quote
from unicodedata import normalize

EX = "http://example.org/id/"

def iri_for(key, kind=""):
    local = quote(normalize("NFC", key.strip()), safe="")
    return EX + (f"{kind}_{local}" if kind else local)

print(iri_for("p 1"))
print(iri_for("Żaneta"))
print(iri_for("rzym", "epoka"))
```

```text
http://example.org/id/p%201
http://example.org/id/%C5%BBaneta
http://example.org/id/epoka_rzym
```

Argument `safe=""` jest ważny: domyślnie `quote` zostawia `/`, więc klucz `a/b` udawałby ścieżkę. Zwykłe klucze, jak `p1`, zostają bez zmian, więc dotychczasowe adresy się nie zmieniają.

### Skąd stabilność

Adres zależy wyłącznie od zawartości komórki: przycięcia spacji, NFC i deterministycznego kodowania. Nie wchodzi w niego numer wiersza, losowy identyfikator ani czas. Ten sam klucz da ten sam adres w każdym przebiegu i w każdym pliku, więc [klucz obcy nadal trafia w klucz główny](#lm-14). [Dopiero to pozwoli porównywać wyniki dwóch przebiegów](04%20Konwersja%20CSV%20do%20TriG.md#ref-49).

_Wersje: Python 3.12 · [źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-model-danych-biura)_

## Pusta komórka i zła data

<a id="ref-44"></a>Pustą komórkę traktujemy jako brak: nie powstaje żadna trójka. Niepoprawną datę traktujemy jako błąd: wiersz jest odrzucany z komunikatem. Żadnej z nich nie zamieniamy na napis.

Dwa błędy, które tak omijamy, wyglądają podobnie, ale mają różne przyczyny. Pythonowe `None` wstawione do szablonu `{od}` daje napis `None`, więc powstaje `"None"^^xsd:date`. Pusty napis daje `""^^xsd:date`. Oba są niepoprawne leksykalnie: [literał](00%20Glosariusz.md#literał) z [typem danych](00%20Glosariusz.md#typ-danych) `xsd:date` musi mieć treść w formacie daty, a typowany literał i zwykły napis to dwie różne rzeczy ([zob. data kontra napis](02%20Podstawy%20RDF%2C%20RDFS%20i%20s%C5%82ownik%C3%B3w.md#lm-5)). Ten sam problem ma `2024-02-30`, bo takiego dnia nie ma.

Dlatego jedna funkcja decyduje o wszystkim, zanim cokolwiek trafi do trójki:

```python
from datetime import date

def date_literal(cell):
    cell = cell.strip()
    if not cell:
        return None
    return f'"{date.fromisoformat(cell).isoformat()}"^^xsd:date'

for cell in ["0027-01-01", "", "2024-02-30"]:
    try:
        print(repr(date_literal(cell)))
    except ValueError as e:
        print("błąd:", e)
```

```text
'"0027-01-01"^^xsd:date'
None
błąd: day is out of range for month
```

Wywołujący robi z wynikiem trzy rzeczy. <a id="lm-19"></a>`None` oznacza pominięcie trójki, bo brak w CSV zostaje brakiem w RDF. Literał trafia do grafu. Wyjątek `ValueError` odrzuca wiersz i dopisuje go do listy błędów, do której wrócimy przy sprawdzaniu wynikowego grafu. [To rozdzielenie brak/błąd znasz już z wierszy CSV dla analiz](#wiersze-csv-dla-sześciu-analiz).

Tak samo działa pusty klucz obcy: bez komórki nie wołamy `iri_for`, więc nie ma połączenia.

_Wersje: Python 3.12 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#03-model-danych-biura)_

## Co zapamiętać

- Model Biura to sześć płaskich klas w bpc: i wyłącznie własności potrzebne analizom; domain i range opisują, ale nie walidują.
- Rób z wizyty, spotkania i raportu osobny węzeł, gdy zdarzenie ma własne atrybuty lub inne zasoby muszą się do niego odwoływać; stałą cechę zapisz jedną trójką.
- Model Biura to własny słownik bpc: z OWL-Time i PROV-O, instancje w ex:, wspólne fakty w grafie domyślnym, wizyty w grafach linii i metadane w grafie provenance.
- Sześć analiz ma wynik dopiero wtedy, gdy w CSV leży po jednym celowo zepsutym wierszu na każdą, a brak (pusta komórka) to osobny przypadek niż błąd.
- Klucz główny daje IRI zasobu, klucz obcy to to samo IRI zbudowane z komórki innego wiersza, a etykiety zapisuj osobno jako rdfs:label, bo IRI musi być stałe.
- Wiersz mapowania zapisuje dla kolumny subject, predicate, object, typ RDF, słownik i uzasadnienie, a daty dostają w nim typ xsd:date.
- Buduj IRI z klucza funkcją deterministyczną (strip, NFC, quote z safe=""), a nie z numeru wiersza czy losowego id, wtedy adresy są takie same w każdym przebiegu.
- Pusta komórka daje brak trójki, a niepoprawna data odrzucenie wiersza; nigdy literał "None" ani pusty czy zły literał z typem xsd:date.

## Pytania sprawdzające

### 13. Jakie klasy i własności Biura zdefiniujesz dla podróżnika, wizyty, epoki, artefaktu, spotkania i raportu?

<details>
<summary>Odpowiedź</summary>

Biuro ma sześć płaskich klas: bpc:Podroznik, bpc:Wizyta, bpc:Epoka, bpc:Artefakt, bpc:Spotkanie i bpc:Raport. Własności to tylko te, które czytają analizy: odwiedzil, epoka, linia, od, do, powstal, uczestnik, naWizycie i opisuje. Epoka dostaje przedział z OWL-Time, a domain i range służą jako opis, nie walidacja.

Zobacz: [sekcja „Klasy i własności Biura”](#klasy-i-własności-biura).

</details>

### 14. Kiedy wizyta lub raport mają być osobnym zasobem zamiast pojedynczej trójki i co daje taki węzeł?

<details>
<summary>Odpowiedź</summary>

Wizyta, spotkanie lub raport mają być osobnym zasobem, gdy mają własne atrybuty (daty, epoka, linia), gdy inne zasoby się do nich odwołują albo gdy uczestniczy w nich więcej niż jeden zasób. Węzeł z własnym IRI daje podmiot dla tych faktów i cel dla krawędzi, np. raportu opisującego wizytę. Pojedyncza trójka wystarcza dla stałej cechy bez własnych atrybutów.

Zobacz: [sekcja „Wizyta jako węzeł, nie trójka”](#wizyta-jako-węzeł-nie-trójka).

</details>

### 15. Jak z wybranych słowników, własnego namespace i podziału na grafy złożysz spójny model Biura?

<details>
<summary>Odpowiedź</summary>

Model składa się z trzech decyzji. Terminy bierzesz z własnego słownika bpc:, OWL-Time dla epok i PROV-O dla pochodzenia. Klasy i własności trzymasz w bpc:, a instancje w ex:. Wspólne fakty zostają w grafie domyślnym, wizyty trafiają do grafów linii czasu, a metadane konwersji do osobnego grafu provenance.

Zobacz: [sekcja „Słowniki, przestrzenie i grafy modelu”](#słowniki-przestrzenie-i-grafy-modelu).

</details>

### 16. Jakie wiersze w CSV muszą się znaleźć (sprzeczne wizyty, łańcuch spotkań, artefakt przed powstaniem, braki, rozbieżny raport), by sześć analiz miało wynik?

<details>
<summary>Odpowiedź</summary>

Każdej analizie odpowiada konkretny wiersz: nakładające się wizyty tego samego podróżnika w dwóch liniach, spotkania łączące czterech podróżników, artefakt z datą powstania późniejszą niż wizyta, pusta data końca i spotkanie bez wizyty, wizyty powtórzone w obu liniach oraz raport z inną datą końca niż wizyta. Dane leżą w sześciu plikach CSV, a klucze są zwykłymi napisami.

Zobacz: [sekcja „Wiersze CSV dla sześciu analiz”](#wiersze-csv-dla-sześciu-analiz).

</details>

### 17. Jak klucz główny zamieniasz na IRI zasobu, a klucz obcy na połączenie, i dlaczego nie z etykiety?

<details>
<summary>Odpowiedź</summary>

Klucz główny wiersza staje się końcówką IRI zasobu w przestrzeni ex:, a klucz obcy jest zamieniany tą samą funkcją na IRI drugiego zasobu i wpisywany jako drugi koniec trójki (obiekt lub podmiot, zależnie od własności). Oba wiersze dają identyczny adres, więc połączenie działa. Etykieta się nie nadaje, bo zmienia się, powtarza i zawiera znaki specjalne, a IRI musi być stałe.

Zobacz: [sekcja „Klucze jako IRI i połączenia”](#klucze-jako-iri-i-połączenia).

</details>

### 18. Jak dla kolumn wizyty zapisać wiersz mapowania: subject, predicate, object, typ RDF, słownik i uzasadnienie?

<details>
<summary>Odpowiedź</summary>

Dla każdej kolumny wizyty zapisujesz wiersz z sześcioma polami: subject i object jako szablony z kluczami, predicate z własnością, typ RDF (IRI, xsd:string lub xsd:date), słownik oraz krótkie uzasadnienie. Kolumna id daje adres i klasę wizyty, klucze obce dają połączenia, a od i do dostają typ xsd:date. Uzasadnienie zostaje w tabeli, by decyzję dało się później odtworzyć.

Zobacz: [sekcja „Wiersz mapowania kolumn wizyty”](#wiersz-mapowania-kolumn-wizyty).

</details>

### 19. Jak zakodujesz w IRI klucz ze spacją lub znakami spoza ASCII i co zapewnia stabilność identyfikatorów między przebiegami?

<details>
<summary>Odpowiedź</summary>

Klucz kodujesz procentowo (UTF-8, `urllib.parse.quote` z `safe=""`), po przycięciu spacji i normalizacji do NFC; spacja staje się `%20`, a „Ż" `%C5%BB`. Stabilność zapewnia to, że adres jest czystą funkcją treści klucza: bez numeru wiersza, losowości i czasu. Ten sam klucz daje więc ten sam IRI w każdym przebiegu i w każdej tabeli.

Zobacz: [sekcja „Znaki specjalne w kluczach IRI”](#znaki-specjalne-w-kluczach-iri).

</details>

### 20. Jak obsłużysz pustą komórkę i niepoprawną datę, by nie powstał literał "None" ani zły typ?

<details>
<summary>Odpowiedź</summary>

Pusta komórka oznacza brak, więc nie tworzymy trójki. Niepoprawna data jest błędem, więc odrzucamy wiersz z komunikatem. Jedna funkcja zwraca None, literał z xsd:date albo rzuca ValueError, dzięki czemu nie powstaje ani "None"^^xsd:date, ani ""^^xsd:date, ani literał z datą, której nie ma.

Zobacz: [sekcja „Pusta komórka i zła data”](#pusta-komórka-i-zła-data).

</details>
