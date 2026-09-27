# Model domeny wniosku

Kontrakty z działu 01 potrzebują teraz konkretnych danych, więc budujemy model Urzędu Zaginionych Poniedziałków: dataclassy Wniosek, Pieczatka, Zalacznik, Glos i [Decyzja](00%20Glosariusz.md#decyzję), zdarzenia z życia wniosku oraz wyjątek NiewaznaPieczatka. Dowiesz się, co decyduje o mutowalności obiektu, i poznasz [Factory Method](00%20Glosariusz.md#factory-method) oraz [Abstract Factory](00%20Glosariusz.md#abstract-factory), które tworzą wnioski i spójne rodziny parserów oraz walidatorów kalendarzy. Dziedziny splatają się tak, że domena dostarcza obiekty, wzorce kreacyjne mówią, jak je tworzyć, a pytest sprawdza ich zachowanie przez interfejs, a nie implementację.

```text
model (dataclassy): Wniosek, Pieczatka, Zalacznik, Glos, Decyzja
        ^
        | tworzy
fabryki:
  twórca (Factory Method) --tworzy--> konkretny wniosek
  Abstract Factory (dla jednego kalendarza) --tworzy--> parser + walidator
        |
        | sprawdza przez interfejs
        v
      pytest
```

**W tym dziale:**

- [Test przez interfejs, nie implementację](#test-przez-interfejs-nie-implementację)
- [Model wniosku jako dataclass](#model-wniosku-jako-dataclass)
- [Pieczątka z przyszłości](#pieczątka-z-przyszłości)
- [Załącznik z obcego kalendarza](#załącznik-z-obcego-kalendarza)
- [Zdarzenia w życiu wniosku](#zdarzenia-w-życiu-wniosku)
- [Głos i decyzja komisji](#głos-i-decyzja-komisji)
- [Factory Method dla wniosków](#factory-method-dla-wniosków)
- [Abstract Factory dla kalendarzy](#abstract-factory-dla-kalendarzy)

## Test przez interfejs, nie implementację

[Test zachowania](00%20Glosariusz.md#test-zachowania) wywołuje tylko publiczną metodę z kontraktu i sprawdza to, co widzi klient: wynik albo wyjątek. Nie zagląda do prywatnych pól, nie liczy wywołań pomocniczych i nie zna kolejności kroków w środku.

[Wiemy już, że atrapa podstawiona przez konstruktor pozwala odciąć zależność](01%20Interfejsy%20ABC%20i%20Protocol.md#lm-7). Teraz idziemy dalej: test zachowania to test, który przetrwa każdą poprawną przeróbkę wnętrza klasy. Kontrola z kalendarzem ma odpowiadać na pytanie „czy ta data to poniedziałek z kalendarza”, a jak to robi, jest jej sprawą.

Najpierw kontrprzykład:

<a id="lm-9"></a>

```python
# poza kanonem: test przywiązany do implementacji
def test_kontrola_trzyma_kalendarz():
    kontrola = KontrolaPoniedzialku(KalendarzStaly())
    assert isinstance(kontrola._kalendarz, KalendarzStaly)
```

Zmiana nazwy pola albo dodanie cache’u zepsuje ten test, choć zachowanie się nie zmieniło. Wersja przez interfejs:

```python
def test_data_spoza_kalendarza_nie_przechodzi():
    kontrola = KontrolaPoniedzialku(KalendarzStaly())
    assert kontrola.sprawdz(date(2024, 1, 2)) is False
```

Zasada wyboru jest prosta:

| Sprawdzasz | Metoda |
|---|---|
| wynik metody z kontraktu | zwykły `assert` |
| wyjątek zgłaszany przez kontrakt | `pytest.raises` |
| współpracę, będącą sednem zachowania | `assert_called_once_with` na mocku |

[Mock ze `spec` z poprzedniej sekcji](01%20Interfejsy%20ABC%20i%20Protocol.md#lm-8) jest więc wyjątkiem, nie regułą. Dobry test możesz też sparametryzować po implementacjach kontraktu (`@pytest.mark.parametrize`): jeśli przechodzi dla każdej, sprawdza kontrakt, a nie klasę.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-model-domeny-wniosku)_

## Model wniosku jako dataclass

Skoro projekt ma już testy, <a id="ref-2"></a>możemy wreszcie zbudować to, co [trzy wnioski z wcześniejszego przykładu](01%20Interfejsy%20ABC%20i%20Protocol.md#trzy-wnioski-o-poniedziałek) tylko opisywały: klasę wniosku. Modelujemy ją jako [dataclass](00%20Glosariusz.md#dataclass), czyli klasę, której `__init__`, `__repr__` i `__eq__` Python generuje z adnotacji pól. O mutowalności decyduje rola obiektu: <a id="lm-10"></a>byt z tożsamością, którego stan zmienia się w czasie, jest mutowalny, a wartość opisująca fakt jest zamrożona (`frozen=True`).

Wniosek jest bytem: ten sam numer przechodzi od „złożony” do „przyjęty”, więc `status` musi się dać zmienić. Pieczątka jest wartością: rok 2024 zawsze znaczy to samo, a próba przypisania czegokolwiek do jej pola kończy się `FrozenInstanceError`.

```python
@dataclass(frozen=True)
class Pieczatka:
    rok: int

@dataclass
class Wniosek:
    numer: int
    poniedzialek: date
    pieczatka: Pieczatka
    status: str = "zlozony"
```

Konsekwencje są praktyczne:

| | `Wniosek` (mutowalny) | `Pieczatka` (frozen) |
|---|---|---|
| zmiana pola | tak, `w.status = ...` | `FrozenInstanceError` |
| hash | brak (`__hash__` = `None`) | jest, nadaje się na klucz |
| współdzielenie | ryzykowne | bezpieczne |

Uwaga: <a id="lm-11"></a>`frozen` jest płytkie. Zamrożona klasa z polem `list` nadal pozwala tę listę zmieniać, więc w wartościach używaj krotek. Dzięki zamrożonym wartościom stary stan da się zachować obok nowego, co przyda się, gdy [decyzję trzeba będzie cofnąć](#ref-21).

_Wersje: Python 3.13 · [źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-model-domeny-wniosku)_

## Pieczątka z przyszłości

Pieczątkę z przyszłości reprezentuj tak samo jak każdą: `Pieczatka(rok=2031)` da się utworzyć, bo to poprawny fakt zapisany na papierze. Nieważność jest dopiero wynikiem porównania z bieżącym rokiem, więc sprawdza ją metoda, która zgłasza wyjątek domenowy `NiewaznaPieczatka`, czyli własną klasę błędu nazwaną językiem urzędu.

Konstruktor nie odrzuca takiej pieczątki celowo. Gdyby robił to `__post_init__`, model zależałby od zegara, a [wniosek z pieczątką z przyszłości (rok 2031 z przykładu o trzech wnioskach)](01%20Interfejsy%20ABC%20i%20Protocol.md#lm-2) nie dałby się nawet zbudować, żeby go odrzucić i pokazać w teście. [Zamrożoną wartość, czyli fakt bez tożsamości](#lm-10), zostawiamy więc czystą, a regułę wkładamy do metody.

<a id="lm-12"></a>Bieżący rok przekazujemy z zewnątrz, zamiast wołać `date.today()`. Test nie zależy wtedy od daty uruchomienia.

```python
class NiewaznaPieczatka(ValueError):
    def __init__(self, pieczatka: "Pieczatka", rok_biezacy: int):
        super().__init__(f"pieczątka {pieczatka.rok} z przyszłości (jest {rok_biezacy})")
        self.pieczatka = pieczatka

@dataclass(frozen=True)
class Pieczatka:
    rok: int

    def zweryfikuj(self, rok_biezacy: int) -> None:
        if self.rok > rok_biezacy:
            raise NiewaznaPieczatka(self, rok_biezacy)
```

Wyjątek dziedziczy po `ValueError`, bo wartość jest błędna, a nie zawiodło środowisko. Osobna klasa pozwala wywołującemu złapać dokładnie ten przypadek i odczytać `pieczatka` z wyjątku. Kontrola zwracająca tylko `True` albo `False` mówi wyłącznie „nie”, wyjątek mówi dlaczego.

W teście wystarczy `pytest.raises(NiewaznaPieczatka)` dla `Pieczatka(2031).zweryfikuj(2024)` oraz brak wyjątku dla `Pieczatka(2024)`.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-model-domeny-wniosku)_

## Załącznik z obcego kalendarza

Kalendarze załączników różnią się [formatem kalendarza](00%20Glosariusz.md#format-kalendarza), czyli umową, jak zapisać dzień jako tekst i od którego dnia liczyć tydzień. Są niezgodne, bo ten sam napis w różnych formatach oznacza różne daty, a nic w samym napisie nie zdradza, którą umowę przyjęto.

Trzy rzeczy bywają różne: kolejność składników daty (`2024-03-04`, `03/04/2024`, `04/03/2024`), pierwszy dzień tygodnia (poniedziałek w ISO, niedziela w części krajów) oraz epoka i numeracja lat. Urząd szuka poniedziałków, więc pomyłka o dzień tygodnia rozstrzyga o losie wniosku.

Dlatego załącznik musi nieść nazwę formatu obok treści. Jak każdy fakt, dataclass z `frozen=True` jest tu wartością: opisuje, co przyszło, i się nie zmienia ([por. byt kontra wartość](#lm-10)).

```python
from dataclasses import dataclass
from datetime import date, datetime
FORMATY = {"iso": "%Y-%m-%d", "us": "%m/%d/%Y", "eu": "%d/%m/%Y"}

@dataclass(frozen=True)
class Zalacznik:
    nazwa: str
    format: str
    data: str

    def jako_date(self) -> date:
        return datetime.strptime(self.data, FORMATY[self.format]).date()

print(Zalacznik("a.ics", "us", "03/04/2024").jako_date())
print(Zalacznik("b.ics", "eu", "03/04/2024").jako_date())
```

```text
2024-03-04
2024-04-03
```

<a id="lm-13"></a>Ten sam napis dał poniedziałek 4 marca albo środę 3 kwietnia. Bez pola `format` urząd zgadywałby po cichu i odrzucał dobre wnioski. Ujednolicenie takich obcych kalendarzy do wspólnego interfejsu [zrobi później Adapter](03%20Tworzenie%20wniosk%C3%B3w.md#ref-25), a [dobór parsera do formatu fabryki](#ref-26).

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-model-domeny-wniosku)_

## Zdarzenia w życiu wniosku

Życie wniosku to krótka lista faktów: został złożony, jego pieczątka została odrzucona, zapadła decyzja, decyzję cofnięto. Każdy z nich opisujemy jako [zdarzenie domenowe](00%20Glosariusz.md#zdarzenie-domenowe), czyli niezmienny zapis tego, co już się stało, nazwany w czasie przeszłym.

Zdarzenie jest wartością, a nie bytem. [Byt i wartość](00%20Glosariusz.md#byt-i-wartość) różnią się tak: byt ma tożsamość i zmienia się w czasie (wniosek zmienia status), a wartość porównuje się po zawartości i nigdy się nie zmienia (por. byt kontra wartość). Faktu nie da się „poprawić”, więc zdarzenie to `@dataclass(frozen=True)`. Niesie tylko dane potrzebne odbiorcy, żeby nie sięgał z powrotem do wniosku.

| Zdarzenie | Dane |
|---|---|
| `WniosekZlozony` | `numer`, `poniedzialek` |
| `PieczatkaOdrzucona` | `numer`, `rok`, `rok_biezacy` |
| `DecyzjaPodjeta` | `numer`, `przyznana`, `poprzedni_status` |
| `DecyzjaCofnieta` | `numer`, `przywrocony_status` |

Ważne jest pole `poprzedni_status`. Zdarzenie, które mówi tylko „przyznano”, nie pozwala wrócić do stanu sprzed decyzji, [a to trzeba będzie umieć zrobić](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#ref-31). Zapis starej wartości w momencie zmiany kosztuje jedno pole, a odtworzenie jej po fakcie bywa niemożliwe.

<a id="lm-14"></a>

```python
@dataclass(frozen=True)
class DecyzjaPodjeta:
    numer: int
    przyznana: bool
    poprzedni_status: str   # do cofnięcia

@dataclass(frozen=True)
class PieczatkaOdrzucona:
    numer: int
    rok: int
    rok_biezacy: int        # ten sam rok, który przekazano z zewnątrz
```

Zdarzenia nie mają metod ani logiki. Kto je wyśle i kto odbierze, rozstrzygną później [Observer i cofanie decyzji](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#ref-29), a samą decyzję z głosami zamodelujemy w następnej sekcji.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-model-domeny-wniosku)_

## Głos i decyzja komisji

[Głos](00%20Glosariusz.md#głos-komisji) to zamrożony dataclass z nazwiskiem członka i wynikiem, a decyzja to <a id="ref-21"></a>zamrożony dataclass, który trzyma wszystkie głosy oraz status wniosku sprzed rozstrzygnięcia. Dzięki temu wynik da się odtworzyć z głosów, a wniosek cofnąć.

Oba obiekty opisują fakt, więc [jak w przypadku zdarzeń są wartościami](#zdarzenia-w-życiu-wniosku), a nie bytami. Nikt nie „poprawia” oddanego głosu. Wniosek pozostaje zmiennym bytem, a decyzja jest o nim zapisem.

<a id="ref-30"></a>Głosy trzymamy w `tuple`, nie w `list`. [`frozen` jest płytkie](#lm-11), więc zamrożona decyzja z listą pozwalałaby po cichu zmienić wynik głosowania.

```python
@dataclass(frozen=True)
class Glos:
    czlonek: str
    za: bool

@dataclass(frozen=True)
class Decyzja:
    numer: int
    glosy: tuple[Glos, ...]
    poprzedni_status: str   # do cofnięcia

    @property
    def przyznana(self) -> bool:
        return sum(g.za for g in self.glosy) > len(self.glosy) / 2
```

Pole `przyznana` jest wyliczane, a nie zapisane, więc nie może być sprzeczne z głosami. Remis oznacza odrzucenie, bo przyznanie wymaga większości.

Do cofnięcia służy `poprzedni_status`, [ten sam zapis starej wartości co w `DecyzjaPodjeta`](#lm-14). Cofnięcie ustawia wnioskowi `decyzja.poprzedni_status` i tworzy `DecyzjaCofnieta` z tą wartością jako `przywrocony_status`. Samo wykonanie cofnięcia [opiszemy przy obiekcie polecenia](04%20Struktury%20wniosku.md#ref-35).

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#02-model-domeny-wniosku)_

## Factory Method dla wniosków

Wnioski, decyzje i zdarzenia już mamy, więc czas zająć się tym, kto tworzy obiekty urzędu i jak wybiera ich klasę. Factory Method to metoda, którą klasa bazowa woła, by dostać obiekt, a podklasa decyduje, jakiej klasy on będzie. Dzięki temu wspólny kod nie zna konkretnych klas.

Załóżmy, że urząd przyjmuje też wnioski pilne: `WniosekPilny`, podklasę `Wniosek` z dodatkowym polem `powod`. Klasa bazowa `Rejestr` ma stały przebieg: sprawdza pieczątkę i zwraca wniosek. Metodę tworzącą zostawia podklasom:

```python
class Rejestr(ABC):
    def zloz(self, numer, poniedzialek, pieczatka, rok_biezacy) -> Wniosek:
        pieczatka.zweryfikuj(rok_biezacy)
        return self.utworz_wniosek(numer, poniedzialek, pieczatka)

    @abstractmethod
    def utworz_wniosek(self, numer, poniedzialek, pieczatka) -> Wniosek: ...

class RejestrPilnych(Rejestr):
    def utworz_wniosek(self, numer, poniedzialek, pieczatka) -> Wniosek:
        return WniosekPilny(numer, poniedzialek, pieczatka)
```

Ten wzorzec ma sens, gdy wybór klasy idzie w parze z resztą zachowania, na przykład z własną weryfikacją w podklasie. Kiedy zmienia się tylko klasa, dziedziczenie po `Rejestr` to za dużo. Wystarczy [funkcja fabryczna](00%20Glosariusz.md#funkcja-fabryczna), czyli zwykła funkcja zwracająca obiekt, a klasę przekazujemy jej jako argument:

```python
def zloz(klasa: type[Wniosek], numer, poniedzialek, pieczatka, rok_biezacy):
    pieczatka.zweryfikuj(rok_biezacy)
    return klasa(numer, poniedzialek, pieczatka)

zloz(WniosekPilny, 7, poniedzialek, pieczatka, 2025)
```

Przebieg jest ten sam, zmienia się tylko klasa, więc `Rejestr` i jego podklasy są zbędne. [Zgodnie z regułą „zacznij od funkcji”](01%20Interfejsy%20ABC%20i%20Protocol.md#wzorzec-czy-zwykła-funkcja) sięgnij po Factory Method dopiero wtedy, gdy podklasa ma zmieniać także inne kroki.

| Sytuacja | Wybór |
|---|---|
| Wariant to tylko inna klasa | funkcja z argumentem `klasa` |
| Wspólny przebieg, wariant zmienia krok tworzenia i zachowanie | Factory Method |
| Trzeba tworzyć całą rodzinę obiektów naraz | [Abstract Factory (następna sekcja)](#ref-38) |

[Test pisz przez interfejs](#test-przez-interfejs-nie-implementację): `RejestrPilnych().zloz(...)` ma zwrócić `WniosekPilny`, a [pieczątka z przyszłości ma dać `NiewaznaPieczatka`](#pieczątka-z-przyszłości).

## Abstract Factory dla kalendarzy

Abstract Factory to obiekt z kilkoma metodami tworzącymi, z których każda zwraca inny element [rodziny produktów](00%20Glosariusz.md#rodzina-produktów), czyli zestawu obiektów zaprojektowanych do pracy razem. Klient dostaje jedną fabrykę i bierze z niej wszystkie elementy, więc nie pomiesza parsera jednego kalendarza z walidatorem drugiego.

[Przy załączniku z obcego kalendarza](#lm-13) (sekcja „Załącznik z obcego kalendarza”) widzieliśmy, że napis `data` znaczy coś tylko razem z `format`. Potrzebujemy więc dwóch produktów: `ParserDaty` zamienia napis na `date`, a `WalidatorDaty` mówi, czy napis jest poprawny w danym formacie. Oba są protokołami, a fabryka abstrakcyjna wymusza spójność strukturą: po jednej metodzie na produkt, po jednej podklasie na format.

```python
class FabrykaKalendarza(ABC):
    @abstractmethod
    def parser(self) -> ParserDaty: ...
    @abstractmethod
    def walidator(self) -> WalidatorDaty: ...
class FabrykaPolska(FabrykaKalendarza):  # "04.03.2024"
    def parser(self) -> ParserDaty: return ParserPolski()
    def walidator(self) -> WalidatorDaty: return WalidatorPolski()

class FabrykaIso(FabrykaKalendarza): ...  # tak samo: ParserIso, WalidatorIso

FABRYKI = {"iso": FabrykaIso(), "pl": FabrykaPolska()}

def fabryka_dla(zalacznik: Zalacznik) -> FabrykaKalendarza:
    return FABRYKI[zalacznik.format]
```

<a id="ref-26"></a>`fabryka_dla` to dobór fabryki do formatu: jedyne miejsce, które zna napisy `"iso"` i `"pl"`. Dalej kod pracuje na kontrakcie: `f = fabryka_dla(z)`, potem `f.walidator()` i `f.parser()`. Nowy format to nowa podklasa i wpis w słowniku, bez zmian u klientów.

Różnica względem poprzedniej sekcji: <a id="ref-38"></a>Factory Method tworzy jeden obiekt, a Abstract Factory całą rodzinę naraz. Kosztem jest sztywność, bo nowy rodzaj produktu, na przykład formater, wymaga nowej metody w każdej fabryce. Test pisz przez interfejs: dla każdej fabryki to, co przyjmie `walidator()`, musi dać się sparsować przez `parser()`.

> **Pułapka: Fabryki jako współdzielone singletony w słowniku.** `FABRYKI` tworzy po jednej instancji na format, a `fabryka_dla` zwraca tę samą za każdym razem. Fabryka zwraca produkty przez `parser()` i `walidator()`, więc jeśli produkty kiedyś trzymają stan (cache, konfiguracja), będzie on współdzielony między wszystkimi klientami i testami. Fabryka powinna być bezstanowa albo tworzyć nowe produkty przy każdym wywołaniu.

## Co zapamiętać

- Test wzorca powinien wołać tylko metody kontraktu i asertować wynik lub wyjątek, a nie prywatne pola czy kroki wewnętrzne.
- Byt ze zmiennym stanem (wniosek) to zwykły dataclass, a wartość (pieczątka) to dataclass z frozen=True, pamiętając, że zamrożenie jest płytkie.
- Pieczątka z przyszłości to poprawna wartość; nieważność wykrywa metoda z bieżącym rokiem z zewnątrz i zgłasza domenowy NiewaznaPieczatka (ValueError).
- Załącznik musi nieść nazwę formatu kalendarza obok daty, bo ten sam napis w różnych formatach oznacza różne dni.
- Zdarzenie domenowe to zamrożony dataclass z faktem w czasie przeszłym, a zapis poprzedniego stanu w momencie zmiany umożliwia późniejsze cofnięcie.
- Decyzja to niezmienna wartość z krotką głosów i polem poprzedni_status, z którego wynika, do jakiego stanu ją cofnąć.
- Gdy wariant to tylko inna klasa, użyj funkcji fabrycznej z argumentem klasy; Factory Method wybieraj, gdy podklasa zmienia też resztę przebiegu.
- Abstract Factory tworzy całą rodzinę pasujących obiektów przez jedną fabrykę na format, więc klient nie może pomieszać parsera z walidatorem z innego kalendarza.

## Pytania sprawdzające

### 9. Jak napisać test, który sprawdza zachowanie wzorca przez jego interfejs, a nie implementację?

<details>
<summary>Odpowiedź</summary>

Wywołuj tylko publiczne metody z kontraktu i asercje opieraj na tym, co widzi klient: wyniku albo zgłoszonym wyjątku. Nie sprawdzaj prywatnych pól ani wewnętrznych wywołań, bo refaktoryzacja poprawnego kodu zepsuje wtedy testy. Mocki z asercją wywołań zostaw dla współpracy, która sama jest zachowaniem. Test można sparametryzować po implementacjach kontraktu, by upewnić się, że sprawdza kontrakt, a nie klasę.

Zobacz: [sekcja „Test przez interfejs, nie implementację”](#test-przez-interfejs-nie-implementację).

</details>

### 10. Jak zamodelować wniosek o odzyskanie poniedziałku jako dataclass i co decyduje o jego mutowalności?

<details>
<summary>Odpowiedź</summary>

Wniosek modelujemy jako zwykły `@dataclass` z polami numer, poniedziałek, pieczątka i status. O mutowalności decyduje rola obiektu: wniosek ma tożsamość i zmienia stan w czasie, więc jest mutowalny, a pieczątka to wartość, więc dostaje `frozen=True`. Zamrożenie daje hash i bezpieczne współdzielenie, ale jest płytkie.

Zobacz: [sekcja „Model wniosku jako dataclass”](#model-wniosku-jako-dataclass).

</details>

### 11. Jak reprezentować pieczątkę z przyszłości i jaki wyjątek zgłosić, gdy jest nieważna?

<details>
<summary>Odpowiedź</summary>

Pieczątkę z przyszłości reprezentuj zwykłym zamrożonym `Pieczatka(rok=2031)`, bo to poprawny fakt, a nie błąd konstrukcji. Nieważność sprawdza osobna metoda porównująca rok z bieżącym rokiem przekazanym z zewnątrz. Gdy pieczątka jest nieważna, zgłasza wyjątek domenowy `NiewaznaPieczatka` dziedziczący po `ValueError`, który niesie pieczątkę i mówi, dlaczego odrzucono.

Zobacz: [sekcja „Pieczątka z przyszłości”](#pieczątka-z-przyszłości).

</details>

### 12. Czym różnią się formaty kalendarzy załączników i co je czyni niezgodnymi?

<details>
<summary>Odpowiedź</summary>

Formaty kalendarzy różnią się kolejnością składników daty, pierwszym dniem tygodnia oraz epoką i numeracją lat. Niezgodność bierze się stąd, że ten sam napis, np. 03/04/2024, w jednym formacie jest 4 marca, a w innym 3 kwietnia, i sam napis nie zdradza umowy. Dlatego model Zalacznik przechowuje nazwę formatu obok treści.

Zobacz: [sekcja „Załącznik z obcego kalendarza”](#załącznik-z-obcego-kalendarza).

</details>

### 13. Jakie zdarzenia zachodzą w życiu wniosku i jakie dane niesie każde z nich?

<details>
<summary>Odpowiedź</summary>

W życiu wniosku zachodzą cztery zdarzenia: złożenie, odrzucenie pieczątki, decyzja i jej cofnięcie. Każde to niezmienny dataclass (frozen=True) w czasie przeszłym, niosący tylko dane potrzebne odbiorcy. Kluczowe jest pole poprzedni_status w decyzji, bo bez niego nie da się jej później cofnąć.

Zobacz: [sekcja „Zdarzenia w życiu wniosku”](#zdarzenia-w-życiu-wniosku).

</details>

### 14. Jak zamodelować głos członka komisji i decyzję (przyznana/odrzucona) oraz jakie dane niesie, by dało się ją cofnąć?

<details>
<summary>Odpowiedź</summary>

Głos to zamrożony dataclass z członkiem komisji i wynikiem (za lub przeciw). Decyzja to zamrożony dataclass z numerem wniosku, krotką głosów i polem poprzedni_status, a przyznanie wylicza się z większości głosów. Zapisany status sprzed decyzji pozwala wniosek przywrócić, a krotka chroni wynik przed zmianą po fakcie.

Zobacz: [sekcja „Głos i decyzja komisji”](#głos-i-decyzja-komisji).

</details>

### 15. Jak Factory Method deleguje wybór klasy wniosku do podklasy i kiedy wystarczy zwykła funkcja fabryczna?

<details>
<summary>Odpowiedź</summary>

Factory Method to metoda tworząca w klasie bazowej, którą wołany przez stały przebieg kod deleguje do podklasy, więc to ona wybiera klasę wniosku. Gdy różni się tylko klasa, a przebieg jest ten sam, wystarcza funkcja fabryczna przyjmująca klasę jako argument. Wzorzec opłaca się, gdy wariant zmienia też inne kroki procedury.

Zobacz: [sekcja „Factory Method dla wniosków”](#factory-method-dla-wniosków).

</details>

### 16. Jak Abstract Factory zapewnia spójną rodzinę obiektów (parser, walidator) dla jednego kalendarza?

<details>
<summary>Odpowiedź</summary>

Abstract Factory ma po jednej metodzie tworzącej na każdy produkt rodziny (parser, walidator) i po jednej podklasie na format kalendarza. Klient bierze oba obiekty z tej samej fabryki, więc zawsze pasują do siebie. Dobór fabryki do formatu załącznika jest w jednym miejscu, a nowy format to nowa podklasa.

Zobacz: [sekcja „Abstract Factory dla kalendarzy”](#abstract-factory-dla-kalendarzy).

</details>
