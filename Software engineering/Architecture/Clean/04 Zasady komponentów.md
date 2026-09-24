# Zasady komponentów

Kręgi mówią, gdzie leży kod. Nie mówią, jak podzielić go na paczki, moduły i biblioteki, które da się rozwijać i wydawać osobno. Martin poświęca temu dwie części książki: trzy zasady spójności i trzy zasady powiązań. To materiał, który w pytaniach o Clean Architecture pojawia się często, a w Hexagonal i Onion w ogóle.

```text
Spójność (co razem):                  Powiązania (jak zależą):
REP  wydawaj razem to, co używasz      ADP  bez cykli w grafie zależności
CCP  grupuj to, co zmienia się razem   SDP  zależ od stabilniejszych
CRP  nie zmuszaj do zależności         SAP  stabilne powinny być abstrakcyjne
     od zbędnych rzeczy
```

## Jednostka wdrożenia

<a id="term-component"></a>[Komponent](00%20Glossary%20Clean.md#component) to najmniejsza jednostka, którą można wdrożyć albo wydać osobno. W Javie jest to plik `.jar`, w .NET `.dll`, w Ruby gem. W Pythonie odpowiednikiem jest paczka dystrybucyjna (wheel z własnym `pyproject.toml`) albo, w obrębie jednego repozytorium, pakiet najwyższego poziomu z wyraźnymi granicami.

```text
rooms-entities        wheel: rooms.entities
rooms-use-cases       wheel: rooms.use_cases       zależy od rooms-entities
rooms-adapters        wheel: rooms.interface_adapters
rooms-web             wheel: rooms.frameworks      zależy od wszystkich
```

Podział na komponenty to decyzja, które klasy trafią razem i jak komponenty będą od siebie zależeć. Odpowiadają na to dwie grupy zasad.

## Trzy zasady spójności

<a id="term-rep"></a>[REP](00%20Glossary%20Clean.md#rep) (Reuse/Release Equivalence Principle) mówi, że jednostka ponownego użycia jest jednostką wydania. Jeśli inne zespoły mają używać komponentu, musi on mieć numer wersji, historię zmian i proces wydawania. Klasy w komponencie powinny mieć wspólny temat, bo są wydawane razem.

<a id="term-ccp"></a>[CCP](00%20Glossary%20Clean.md#ccp) (Common Closure Principle) mówi, żeby grupować klasy, które zmieniają się z tych samych powodów i w tym samym czasie, a rozdzielać te, które zmieniają się z różnych powodów. To zasada pojedynczej odpowiedzialności (SRP) przeniesiona na poziom komponentów. Zmiana reguł anulowania powinna dotknąć jednego komponentu, a nie pięciu.

<a id="term-crp"></a>[CRP](00%20Glossary%20Clean.md#crp) (Common Reuse Principle) mówi, żeby nie zmuszać użytkowników komponentu do zależności od rzeczy, których nie używają. Jeśli moduł raportów potrzebuje tylko `TimeSlot`, a komponent zawiera też ciężki klient kalendarza Google, każda zmiana w kliencie wymusza ponowne wydanie i testy raportów. To zasada segregacji interfejsów (ISP) na poziomie komponentów.

Zasady się ścierają. Martin rysuje je jako <a id="term-tension-triangle"></a>[trójkąt napięć](00%20Glossary%20Clean.md#tension-triangle):

```text
                     REP
                (łatwo używać)
                   /     \
      za dużo     /       \    za dużo
      wydań      /         \   zmian w wielu
                /           \  komponentach
             CCP ─────────── CRP
     (łatwo zmieniać)   (mniej niepotrzebnych wydań)
                 za trudno używać
```

REP i CCP powiększają komponenty, a CRP je zmniejsza. Nie da się spełnić wszystkich naraz. We wczesnej fazie projektu ważniejsze jest CCP, bo kod szybko się zmienia i liczy się łatwość zmian. Gdy projekt dojrzewa i inni zaczynają go używać, rośnie znaczenie REP i CRP.

## Graf bez cykli

<a id="term-adp"></a>[ADP](00%20Glossary%20Clean.md#adp) (Acyclic Dependencies Principle) mówi, że graf zależności między komponentami nie może mieć cykli. Cykl sprawia, że komponenty w nim tworzą w praktyce jeden duży komponent: nie da się ich wydać, przetestować ani zbudować osobno.

```text
Cykl:
reservations ──► rooms                     rezerwacja sprawdza pojemność sali
rooms        ──► reservations              sala pyta o swoją zajętość

Po odwróceniu zależności:
reservations ──► rooms                     rezerwacja sprawdza pojemność sali
reservations ──► rooms.OccupancySource     implementuje interfejs zdefiniowany w rooms
rooms        ──► (nic z reservations)
```

Są dwa sposoby rozbicia cyklu:

1. Odwrócenie zależności: komponent `rooms` definiuje interfejs `OccupancySource`, którego potrzebuje, a `reservations` go implementuje. Strzałka z `rooms` do `reservations` zamienia się w strzałkę z `reservations` do `rooms`.
2. Nowy komponent: wspólną część obu komponentów (np. `TimeSlot`) wydziel do trzeciego komponentu, od którego zależą oba.

```python
# rooms/occupancy.py
class OccupancySource(Protocol):
    def busy_slots(self, room_id: str) -> list[TimeSlot]: ...


class RoomOccupancy:
    def __init__(self, source: OccupancySource):
        self._source = source

    def is_free(self, room_id: str, slot: TimeSlot) -> bool:
        return not any(slot.overlaps(s) for s in self._source.busy_slots(room_id))
```

W Pythonie cykle między pakietami często ujawniają się jako `ImportError` przy częściowo zainicjalizowanym module. `import-linter` z kontraktem `independence` albo `layers` wykrywa je, zanim trafią na produkcję.

## Zależności w stronę stabilności

<a id="term-sdp"></a>[SDP](00%20Glossary%20Clean.md#sdp) (Stable Dependencies Principle) mówi, że zależności powinny wskazywać w stronę komponentów stabilniejszych. Stabilny komponent to taki, który trudno zmienić, bo zależy od niego wiele innych.

Martin mierzy to metryką <a id="term-instability"></a>[niestabilności](00%20Glossary%20Clean.md#instability) `I`:

```text
Fan-in  = liczba klas spoza komponentu, które zależą od klas w komponencie
Fan-out = liczba klas spoza komponentu, od których zależą klasy w komponencie

I = Fan-out / (Fan-in + Fan-out)

I = 0  maksymalnie stabilny: wszyscy zależą od niego, on od nikogo
I = 1  maksymalnie niestabilny: nikt od niego nie zależy, on zależy od innych
```

SDP w liczbach: `I` komponentu powinno być większe od `I` komponentów, od których zależy. Dla systemu rezerwacji:

| Komponent | Fan-in | Fan-out | I |
|---|---:|---:|---:|
| `entities` | 9 | 0 | 0,00 |
| `use_cases` | 6 | 3 | 0,33 |
| `interface_adapters` | 2 | 6 | 0,75 |
| `frameworks` | 0 | 5 | 1,00 |

Niestabilność rośnie w stronę krawędzi. Clean Architecture z Dependency Rule automatycznie spełnia SDP: środek jest najbardziej stabilny, a zewnętrze najmniej.

## Stabilne znaczy abstrakcyjne

<a id="term-sap"></a>[SAP](00%20Glossary%20Clean.md#sap) (Stable Abstractions Principle) mówi, że komponent powinien być tak abstrakcyjny, jak jest stabilny. Stabilny komponent jest trudny do zmiany, więc żeby dało się go rozszerzać, powinien składać się z abstrakcji. Niestabilny komponent może być konkretny, bo łatwo go zmienić.

<a id="term-abstractness"></a>[Abstrakcyjność](00%20Glossary%20Clean.md#abstractness) `A` mierzy się tak:

```text
Na = liczba klas abstrakcyjnych i interfejsów w komponencie (w Pythonie: Protocol, ABC)
Nc = liczba wszystkich klas w komponencie

A = Na / Nc      A = 0 zupełnie konkretny, A = 1 zupełnie abstrakcyjny
```

SDP i SAP razem są wersją odwrócenia zależności na poziomie komponentów: zależności wskazują w stronę stabilności, a stabilność idzie w parze z abstrakcją. Zależności wskazują więc w stronę abstrakcji.

## Wykres A względem I

Na wykresie z osią `I` (niestabilność) i osią `A` (abstrakcyjność) Martin rysuje odcinek od (0, 1) do (1, 0). To <a id="term-main-sequence"></a>[ciąg główny](00%20Glossary%20Clean.md#main-sequence) (main sequence), na którym `A + I = 1`. Komponenty powinny leżeć na nim albo blisko niego.

```text
A (abstrakcyjność)
1 ┤╲                          ● strefa bezużyteczności (1, 1)
  │  ╲
  │    ╲   ciąg główny: A + I = 1
  │      ╲
  │        ╲
  │          ╲
0 ┤● strefa    ╲
  │  bólu (0, 0) ╲
  └─────────────────────────── I (niestabilność)
  0                          1
```

Odległość od ciągu głównego: `D = |A + I − 1|`. Wartość 0 jest idealna, wartość bliska 1 oznacza problem.

Punkt (0, 0) to <a id="term-zone-of-pain"></a>[strefa bólu](00%20Glossary%20Clean.md#zone-of-pain): komponent stabilny i konkretny. Wszyscy od niego zależą, a nie da się go rozszerzyć bez zmiany. Typowy przykład to schemat bazy danych używany bezpośrednio przez pół systemu. Wyjątkiem są rzeczy konkretne, ale nieulotne, na przykład biblioteka standardowa albo `datetime`. Ich nikt nie zmienia, więc nie bolą.

Punkt (1, 1) to <a id="term-zone-of-uselessness"></a>[strefa bezużyteczności](00%20Glossary%20Clean.md#zone-of-uselessness): komponent abstrakcyjny, od którego nikt nie zależy. Zwykle są to pozostałości po dawnych interfejsach, których nikt nie implementuje ani nie używa.

## Zasady w Pythonie

W Pythonie te zasady przekładają się na kilka praktyk:

- komponentem jest pakiet najwyższego poziomu (`rooms.entities`) albo osobna paczka instalowalna,
- ADP pilnuje `import-linter` z kontraktami `layers` i `independence`,
- Fan-in, Fan-out i `I` można policzyć z grafu importów, na przykład narzędziem `pydeps` albo prostym skryptem na module `ast`,
- `A` liczy się jako stosunek klas `Protocol` i `ABC` do wszystkich klas w pakiecie,
- CCP w praktyce oznacza pakiety według funkcji biznesowej (`reservations`, `rooms`, `billing`), a nie wyłącznie według warstwy technicznej.

```python
# prosty licznik abstrakcyjności pakietu
import ast
import pathlib


def abstractness(package_dir: str) -> float:
    total = abstract = 0
    for path in pathlib.Path(package_dir).rglob("*.py"):
        for node in ast.walk(ast.parse(path.read_text())):
            if isinstance(node, ast.ClassDef):
                total += 1
                bases = {getattr(b, "id", getattr(b, "attr", "")) for b in node.bases}
                abstract += bool(bases & {"Protocol", "ABC"})
    return abstract / total if total else 0.0
```

## SOLID na dwóch poziomach

Zasady komponentów są przeniesieniem SOLID o poziom wyżej, a Clean Architecture jest ich zastosowaniem do całej aplikacji:

| SOLID (klasy) | Odpowiednik dla komponentów | Rola w Clean Architecture |
|---|---|---|
| SRP: jeden powód zmiany | CCP | każdy krąg zmienia się z innego powodu |
| OCP: otwarte na rozszerzenie | SDP i SAP | kręgi wewnętrzne chronione przed zmianami zewnętrznych |
| LSP: podstawialność | wymienne implementacje | każdy gateway i presenter można podmienić |
| ISP: małe interfejsy | CRP | wąskie boundaries dla każdego przypadku użycia |
| DIP: zależność od abstrakcji | ADP (rozbijanie cykli), SAP | Dependency Rule i interfejsy definiowane w środku |

Martin pisze, że OCP jest jednym z głównych powodów istnienia architektury: system ma być łatwy do rozszerzenia bez dużych zmian w istniejącym kodzie. Kręgi i zasady komponentów to mechanizm, który to umożliwia.

## Co zapamiętać

- Komponent to jednostka wdrożenia: `.jar`, `.dll`, a w Pythonie paczka albo pakiet najwyższego poziomu.
- REP, CCP i CRP decydują, co trafia razem, i tworzą trójkąt napięć.
- ADP zabrania cykli, które rozbija się odwróceniem zależności albo nowym komponentem.
- SDP: zależności wskazują w stronę stabilności, mierzonej jako `I = Fan-out / (Fan-in + Fan-out)`.
- SAP: stabilne komponenty powinny być abstrakcyjne, `A = Na / Nc`.
- Komponenty powinny leżeć blisko ciągu głównego `A + I = 1`, z dala od strefy bólu i strefy bezużyteczności.
- Zasady komponentów to SOLID przeniesiony z klas na moduły.

## Pytania sprawdzające

### 21. Czym są zasady spójności komponentów REP, CCP i CRP i jak ze sobą konkurują?

<details>
<summary>Odpowiedź</summary>

REP: jednostka ponownego użycia jest jednostką wydania, więc komponent ma wersję i wspólny temat. CCP: grupuj to, co zmienia się z tych samych powodów i w tym samym czasie (SRP dla komponentów). CRP: nie zmuszaj użytkowników do zależności od rzeczy, których nie używają (ISP dla komponentów). REP i CCP powiększają komponenty, CRP je zmniejsza, co tworzy trójkąt napięć. We wczesnej fazie ważniejsze jest CCP, później REP i CRP.

Zobacz: sekcja „Trzy zasady spójności”.

</details>

### 22. Czym jest Acyclic Dependencies Principle i jak rozbić cykl zależności między komponentami?

<details>
<summary>Odpowiedź</summary>

ADP mówi, że graf zależności między komponentami nie może mieć cykli, bo komponenty w cyklu nie dają się wydać, zbudować ani przetestować osobno. Cykl rozbija się odwróceniem zależności, czyli interfejsem zdefiniowanym w komponencie, który go potrzebuje, i zaimplementowanym w drugim (np. `OccupancySource`), albo wydzieleniem wspólnej części do nowego komponentu, od którego zależą oba.

Zobacz: sekcja „Graf bez cykli”.

</details>

### 23. Czym jest Stable Dependencies Principle i jak mierzy się stabilność (I = Fan-out / (Fan-in + Fan-out))?

<details>
<summary>Odpowiedź</summary>

SDP mówi, że zależności powinny wskazywać w stronę komponentów stabilniejszych. Niestabilność `I = Fan-out / (Fan-in + Fan-out)`, gdzie Fan-in to liczba zewnętrznych klas zależnych od komponentu, a Fan-out to liczba zewnętrznych klas, od których komponent zależy. `I = 0` oznacza maksymalnie stabilny, `I = 1` maksymalnie niestabilny. `I` komponentu powinno być większe niż `I` komponentów, od których zależy. Clean Architecture spełnia to automatycznie, bo `I` rośnie od Entities do Frameworks.

Zobacz: sekcja „Zależności w stronę stabilności”.

</details>

### 24. Czym jest Stable Abstractions Principle i jak łączy się z SDP?

<details>
<summary>Odpowiedź</summary>

SAP mówi, że komponent powinien być tak abstrakcyjny, jak jest stabilny. Abstrakcyjność `A = Na / Nc` to stosunek klas abstrakcyjnych i interfejsów do wszystkich klas. Razem z SDP daje to odwrócenie zależności na poziomie komponentów: zależności wskazują w stronę stabilności, a stabilne komponenty są abstrakcyjne, więc zależności wskazują w stronę abstrakcji.

Zobacz: sekcja „Stabilne znaczy abstrakcyjne”.

</details>

### 25. Czym są „main sequence”, „strefa bólu” i „strefa bezużyteczności”?

<details>
<summary>Odpowiedź</summary>

Na wykresie `A` względem `I` ciąg główny to odcinek `A + I = 1`, na którym lub blisko którego powinny leżeć komponenty. Odległość od niego to `D = |A + I − 1|`. Strefa bólu (0, 0) to komponenty stabilne i konkretne, trudne do zmiany i rozszerzenia (np. schemat bazy używany wszędzie). Wyjątkiem są rzeczy nieulotne, jak biblioteka standardowa. Strefa bezużyteczności (1, 1) to komponenty abstrakcyjne, od których nikt nie zależy.

Zobacz: sekcja „Wykres A względem I”.

</details>

### 26. Jak zasady komponentów przekładają się na podział na pakiety i paczki w Pythonie?

<details>
<summary>Odpowiedź</summary>

Komponent to pakiet najwyższego poziomu albo osobna paczka instalowalna. Cykle (ADP) wykrywa `import-linter`. Fan-in, Fan-out i `I` liczy się z grafu importów (`pydeps` albo skrypt na `ast`), a `A` jako stosunek klas `Protocol` i `ABC` do wszystkich klas. CCP sugeruje grupowanie według funkcji biznesowej, a nie tylko według warstwy technicznej.

Zobacz: sekcja „Zasady w Pythonie”.

</details>

### 27. Jak SOLID na poziomie klas ma się do zasad komponentów i do samej Clean Architecture?

<details>
<summary>Odpowiedź</summary>

Zasady komponentów przenoszą SOLID o poziom wyżej: SRP odpowiada CCP, ISP odpowiada CRP, DIP odpowiada rozbijaniu cykli (ADP) i SAP, a OCP realizują SDP i SAP, które chronią stabilne komponenty. Clean Architecture stosuje to do całej aplikacji: Dependency Rule to DIP, wymienne gateway'e i presentery to LSP, wąskie boundaries to ISP. Martin wskazuje OCP jako jeden z głównych powodów istnienia architektury.

Zobacz: sekcja „SOLID na dwóch poziomach”.

</details>
