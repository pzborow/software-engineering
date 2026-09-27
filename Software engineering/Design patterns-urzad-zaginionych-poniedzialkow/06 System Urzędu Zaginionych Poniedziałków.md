# System Urzędu Zaginionych Poniedziałków

W Urzędzie Zaginionych Poniedziałków wzorce z działów 02–05 (kreacyjne, strukturalne i behawioralne) działały dotąd osobno, a ten dział składa je razem: [Command](00%20Glosariusz.md#command), [Memento](00%20Glosariusz.md#memento) i [Observer](00%20Glosariusz.md#observer) dają decyzję, która wysyła powiadomienia i da się cofnąć bez rozjazdu stanu. Jeden test end-to-end przez fasadę urzędu, czyli Okienko, przeprowadzi wniosek od złożenia do cofnięcia, a na koniec prześledzisz przepływ wszystkich 23 wzorców i ocenisz, które zastąpić prostszym idiomem Pythona. Wzorce behawioralne dostarczają tu klocków, a projektowanie obiektowe pyta, czy dany klocek jest naprawdę potrzebny. Po lekturze umiesz złożyć taki przepływ i uzasadnić, co w nim uprościć.

```text
Przepływ jednej decyzji:

Okienko -> polecenie (Command).execute
             (1) Memento zapisuje stan wniosku
             (2) zmiana decyzji
             (3) Observer powiadamia subskrybentów

Okienko -> polecenie (Command).undo
             (1) Memento przywraca stan
             (2) Observer powiadamia o cofnięciu
```

**W tym dziale:**

- [Decyzja z powiadomieniami i cofaniem](#decyzja-z-powiadomieniami-i-cofaniem)
- [Trzy wzorce i ich prostsze idiomy](#trzy-wzorce-i-ich-prostsze-idiomy)
- [Test end-to-end przez Okienko](#test-end-to-end-przez-okienko)
- [Wszystkie wzorce w jednym przepływie](#wszystkie-wzorce-w-jednym-przepływie)

## Decyzja z powiadomieniami i cofaniem

<a id="ref-96"></a>Połącz je tak: `poprowadz` zmienia [stan](00%20Glosariusz.md#state) i publikuje zdarzenie, obserwator zamienia zdarzenie na powiadomienie, a <a id="ref-84"></a>polecenie trzyma migawkę i przy `undo` przywraca ją oraz publikuje zdarzenie cofnięcia. <a id="ref-87"></a>Każdy wzorzec zostaje przy swojej roli, a łączy je Publikator.

### Powiadomienie jako obserwator

`Powiadomienie` z kanałem subskrybujemy na `Publikator` przez lambdę, która dopisuje adresata. `Publikator` nic nie wie o kanałach. Skoro <a id="ref-29"></a>publikuje dwa typy zdarzeń, `o_decyzji` przyjmuje teraz `DecyzjaPodjeta | DecyzjaCofnieta` i rozróżnia je przez `match`. [Uchwyt wypisania z `subskrybuj`](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń) zwalnia subskrypcję po zakończeniu sprawy.

### Polecenie z migawką

<a id="ref-81"></a>Polecenie przy cofnięciu przywraca cały zapisany stan wniosku, a nie tylko status. Cofnięcie to kolejne [zdarzenie domenowe](00%20Glosariusz.md#zdarzenie-domenowe), `DecyzjaCofnieta`, publikowane dopiero po udanym przywróceniu.

```python
# DecyzjaCofnieta is the immutable domain event defined earlier.

class Powiadomienie:
    def o_decyzji(self, zdarzenie, adresat: str) -> None:
        match zdarzenie:
            case DecyzjaPodjeta(numer=n, przyznana=p):
                tresc = f"Wniosek {n}: {'przyznany' if p else 'odrzucony'}"
            case DecyzjaCofnieta(numer=n, przywrocony_status=s):
                tresc = f"Wniosek {n}: decyzja cofnięta, status {s}"
        self.kanal.wyslij(adresat, tresc)

wypisz = pub.subskrybuj(lambda z: powiadomienie.o_decyzji(z, adresat))
decyzja, migawka = poprowadz(wniosek, glosy, kontrola, regula, pub)
polecenie = CofalnaDecyzja(wniosek, decyzja, migawka, pub)
polecenie.undo()
```

<a id="ref-76"></a>[`CofalnaDecyzja` to podklasa `PoleceniaDecyzji`](00%20Glosariusz.md#command): <a id="ref-31"></a>`undo` woła `wniosek.przywroc(migawka)`, potem `publikator.publikuj(DecyzjaCofnieta(...))`.

```text
poprowadz -> publikuj(DecyzjaPodjeta) -> o_decyzji -> Kanal
undo -> przywroc(migawka) -> publikuj(DecyzjaCofnieta) -> o_decyzji -> Kanal
```

Zdarzenie jest ostatnim krokiem po sukcesie, więc <a id="lm-48"></a>powiadomienia nigdy nie mówią o zmianie, której nie było. Cena: `match` w powiadomieniu rośnie z każdym nowym zdarzeniem.

_[źródła: 1](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-system-urzędu-zaginionych-poniedziałków)_

> **Pułapka: Subskrypcja bez filtra słyszy cudze wnioski.** Lambda podpięta do wspólnego `Publikator` dostaje każde `DecyzjaPodjeta` i `DecyzjaCofnieta`, także z innych wniosków. `adresat` dostanie powiadomienia o cudzych sprawach, dopóki nie wywoła `wypisz`. Filtruj po `numer` w lambdzie albo twórz publikatora per sprawa.

## Trzy wzorce i ich prostsze idiomy

Kod urzędu jest już cofalny i powiadamia, więc czas ocenić, co w nim kosztuje więcej, niż daje. Trzy wzorce mają w Pythonie tańsze odpowiedniki: Observer zastępuje lista funkcji, State zastępuje `Enum` ze słownikiem przejść, a Command zastępuje domknięcie z funkcją odwrotną.

| Wzorzec | Prostszy idiom | Wzorzec nadal lepszy, gdy |
|---|---|---|
| Observer (`Publikator`) | lista funkcji wywoływanych w pętli | potrzebujesz uchwytu wypisania, bezpiecznej kopii listy albo słabych referencji |
| State (`Zlozony`, `Przyznany`, `Odrzucony`) | `Status` i słownik przejść | stany mają własne zachowanie, a nie tylko graf przejść |
| Command (`CofalnaDecyzja`) | domknięcie `cofnij` | polecenie ma stan, historię na stosie albo kilka operacji |

```python
# poza kanonem: szkic idiomów zamiast klas
PRZEJSCIA: dict[tuple[Status, bool], Status] = {
    (Status.ZLOZONY, True): Status.PRZYZNANY,
    (Status.ZLOZONY, False): Status.ODRZUCONY,
}
nowy = PRZEJSCIA[(Status(wniosek.status), decyzja.przyznana)]

_sluchacze: list[Callable] = []
for f in _sluchacze:
    f(zdarzenie)

cofnij = lambda: wniosek.przywroc(migawka)
```

Trzy stany różnią się tylko tym, dokąd prowadzą, więc słownik wystarcza. Klasy `Stan` zaczną się opłacać, gdy `Przyznany` dostanie własne reguły, np. inną kontrolę.

Pętla po samej liście nie pozwala bezpiecznie wypisać się w trakcie powiadamiania. Dlatego w `Publikator` [kopia listy w pętli jest celowa](05%20Przep%C5%82yw%20komisji.md#lm-40). `CofalnaDecyzja` wygrywa z domknięciem, bo [po przywróceniu publikuje `DecyzjaCofnieta`](#decyzja-z-powiadomieniami-i-cofaniem) i da się ją odłożyć na stos.

Zacznij od idiomu, a wzorzec dodaj, gdy pojawi się stan, historia albo zachowanie, którego idiom nie udźwignie.

> **Pułapka: Słownik przejść rzuca KeyError na stanie końcowym.** `PRZEJSCIA[(Status(wniosek.status), decyzja.przyznana)]` zna tylko przejścia z `ZLOZONY`. Decyzja dla wniosku już `PRZYZNANY` albo `ODRZUCONY` kończy się `KeyError`, a nie czytelnym odrzuceniem. Klasy State egzekwują dozwolone przejścia we własnych metodach. Przy słowniku trzeba użyć `.get` i jawnie obsłużyć brak przejścia.

## Test end-to-end przez Okienko

Jeden test przez `Okienko` przeprowadza wniosek przez cały cykl: `zloz`, `zdecyduj`, potem cofnięcie. Asercje dotyczą tylko tego, co widać z zewnątrz fasady: statusu w teczce i wiadomości w kanale.

Do tej pory `Okienko` umiało złożyć i rozstrzygnąć wniosek, ale cofnięcie wymagało sięgania do `CofalnaDecyzja` z zewnątrz. Test przez fasadę nie może znać poleceń ani migawek, więc dodajemy `cofnij(numer, adresat)`. `Okienko` trzyma stos wykonanych poleceń i zdejmuje z niego ostatnie, [a reguły dalej siedzą w klasach domenowych](05%20Przep%C5%82yw%20komisji.md#lm-47).

Status odczytujemy [wizytatorem](00%20Glosariusz.md#visitor) `RaportStatusow` po `okienko.teczka`. Dzięki temu test nie zagląda do pól wniosku. Atrapą jest tylko kanał, który zapisuje wysłane wiadomości:

```python
def test_od_zlozenia_do_cofniecia():
    kanal = KanalTestowy()  # wyslij() dopisuje (adresat, tresc) do listy
    okienko = Okienko(Konfiguracja(rok_biezacy=2024), Powiadomienie(kanal))
    numer = okienko.zloz(DANE[0])
    assert okienko.zdecyduj(numer, GLOSY_ZA, "anna") is True
    assert statusy(okienko) == {"przyznany": 1}
    okienko.cofnij(numer, "anna")
    assert statusy(okienko) == {"zlozony": 1}
    assert [a for a, _ in kanal.wyslane] == ["anna", "anna"]
    ...
```

Pomocnik `statusy` przepuszcza teczkę przez `RaportStatusow` i zwraca `dict(raport.liczniki)`. Dwie wiadomości to `DecyzjaPodjeta` i `DecyzjaCofnieta`. Zgadza się to z zasadą, że [powiadomienia nigdy nie mówią o zmianie, której nie było](#lm-48) (opisaliśmy ją w sekcji o decyzji z powiadomieniami i cofaniem).

Ten jeden test sprawdza kolejność kroków, a nie każdą regułę osobno. Reguły komisji, kontrole i przejścia stanów można sprawdzać bezpośrednio na ich klasach domenowych, bez fasady. Tutaj wystarczy dopisać drugi przypadek z odrzuconą pieczątką, bo wyjątek ma przejść przez fasadę bez połknięcia.

Tak zbudowany test zadziała nawet [po zamianie `Stan` na `Enum` ze słownikiem](05%20Przep%C5%82yw%20komisji.md#lm-41). Nie zna wtedy żadnej klasy wewnętrznej, więc taka wymiana go nie zepsuje.

## Wszystkie wzorce w jednym przepływie

Wszystkie 23 wzorce spotykają się na jednej ścieżce: `Okienko` przyjmuje wniosek, komisja go rozstrzyga, a polecenie cofa decyzję. Nie każdy zasłużył na klasę: część zostawiłbym jako funkcję, `Enum` albo zwykłą pętlę.

```text
zloz:     [[fasada|Okienko]] → Singleton (rok) → Abstract Factory + Adapter (kalendarz)
          → Builder → Factory Method / Prototype (wniosek)
          → Flyweight + Proxy (pieczątka) → Decorator + Chain (kontrole) → Composite (teczka)
zdecyduj: Mediator (komisja) → Interpreter / Strategy / Template Method (reguła)
          → State (status) → Memento (migawka) → Command → Observer → Bridge (kanał)
cofnij:   Command.undo → Memento.przywroc → Observer → Bridge
raporty:  Visitor + Iterator po teczce
```

Kreacyjne (5) budują wniosek z konfiguracji, strukturalne (7) łączą go z obcym kalendarzem, pulą pieczątek i teczką, a behawioralne (11) prowadzą decyzję. Wspólny mianownik to [kompozycja](00%20Glosariusz.md#kompozycja) i kontrakty: fasada zna kolejność, klasy domenowe znają reguły. Dlatego [migawka przy błędzie](05%20Przep%C5%82yw%20komisji.md#lm-46) i [zdarzenie po sukcesie](#lm-48) działają bez wiedzy o sobie nawzajem, a decyzję, [którą trzeba było umieć cofnąć](#decyzja-z-powiadomieniami-i-cofaniem), cofa ta sama migawka.

### Co zastąpić prostszym idiomem

| Wzorzec | Idiom | Kiedy |
|---|---|---|
| Singleton | `@cache` na funkcji | [zawsze (już tak jest)](00%20Glosariusz.md#singleton) |
| Iterator | generator z `yield from` | zawsze |
| Strategy, Template Method | funkcja | zmienia się jeden krok |
| State | `Enum` + słownik przejść | stany różnią się tylko grafem |
| Chain | lista funkcji | ogniwa bez stanu |
| Prototype | `dataclasses.replace` | mało pól |
| Abstract Factory | słownik format → funkcje | dwa produkty |
| Visitor | `match` po typie | stabilny zbiór typów |

Przykład dla łańcucha: [`OgniwoNumeru` i `OgniwoStatusu` nie mają stanu](00%20Glosariusz.md#łańcuch-odpowiedzialności), więc cała klasa `Ogniwo` sprowadza się do listy:

```python
# poza kanonem
KONTROLE = [lambda w: w.numer > 0, lambda w: w.status == "zlozony"]

def przejdzie(wniosek) -> bool:
    return all(k(wniosek) for k in KONTROLE)
```

Zostawiam Fasadę, Adapter, Composite, Proxy, Command z Memento i Observera: rozwiązują problemy, których idiom nie ma, czyli obcy kod, cofanie i wypisywanie subskrybentów.

_[źródła: 2](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md#06-system-urzędu-zaginionych-poniedziałków)_

## Co zapamiętać

- Zdarzenie publikuj po udanej zmianie lub przywróceniu migawki, a Publikator niech będzie jedynym łącznikiem między poleceniem a powiadomieniami.
- Zacznij od idiomu (lista funkcji, Enum ze słownikiem, domknięcie) i sięgaj po wzorzec, gdy pojawi się wypisywanie, zachowanie stanów albo historia poleceń.
- Test end-to-end przez fasadę sprawdza kolejność kroków i to, co widać z zewnątrz (status w teczce, wiadomości w kanale), a nie wnętrze podsystemu.
- Użyj wzorca tam, gdzie idiom nie rozwiąże obcego kodu, cofania ani wypisywania subskrybentów; resztę zastąp funkcją, Enumem, generatorem lub match.

## Pytania sprawdzające

### 41. Jak połączyć Command, Memento i Observer, by decyzja wysyłała powiadomienia i dała się cofnąć?

<details>
<summary>Odpowiedź</summary>

`poprowadz` zmienia stan i publikuje `DecyzjaPodjeta` przez `Publikator`, a powiadomienie subskrybuje go jako obserwator. Polecenie trzyma migawkę i decyzję, a `undo` przywraca stan wniosku i publikuje `DecyzjaCofnieta`. Zdarzenia idą dopiero po sukcesie, więc powiadomienia nie opisują zmian, których nie było.

Zobacz: [sekcja „Decyzja z powiadomieniami i cofaniem”](#decyzja-z-powiadomieniami-i-cofaniem).

</details>

### 42. Dla trzech wzorców podaj prostszy idiom Pythona i warunek, gdy wzorzec nadal jest lepszy.

<details>
<summary>Odpowiedź</summary>

Observer zastąp listą funkcji wywoływanych w pętli, State enumem ze słownikiem przejść, a Command domknięciem z funkcją odwrotną. Wzorzec wraca, gdy potrzebujesz uchwytu wypisania i bezpiecznego powiadamiania (Observer), własnego zachowania stanów (State) albo historii i kilku operacji w poleceniu (Command).

Zobacz: [sekcja „Trzy wzorce i ich prostsze idiomy”](#trzy-wzorce-i-ich-prostsze-idiomy).

</details>

### 43. Jak przez fasadę przeprowadzić wniosek od złożenia do decyzji i cofnięcia w jednym teście end-to-end?

<details>
<summary>Odpowiedź</summary>

Test end-to-end woła tylko metody fasady `Okienko`: `zloz`, `zdecyduj` i nowe `cofnij`. Status sprawdza wizytatorem po teczce, a powiadomienia przez atrapę kanału. Nie zna poleceń, migawek ani stanów, więc przetrwa refaktoryzację wnętrza. Szczegóły reguł testuje się osobno na klasach domenowych.

Zobacz: [sekcja „Test end-to-end przez Okienko”](#test-end-to-end-przez-okienko).

</details>

### 44. Jak 23 wzorce trzech rodzin współpracują w przepływie od wniosku do cofnięcia decyzji i które zastąpiłbyś prostszym idiomem?

<details>
<summary>Odpowiedź</summary>

Wzorce współpracują w jednej kolejności: fasada Okienko składa wniosek z konfiguracji, fabryk, Buildera, puli i proxy pieczątek, kontroli i teczki, a potem komisja, reguła, State, Memento, Command i Observer prowadzą decyzję i jej cofnięcie. Prostszym idiomem zastąpiłbym Singleton, Iterator, Strategy, Template Method, State, Chain, Prototype, Abstract Factory i Visitor. Zostawiłbym Fasadę, Adapter, Composite, Proxy, Command z Memento oraz Observera.

Zobacz: [sekcja „Wszystkie wzorce w jednym przepływie”](#wszystkie-wzorce-w-jednym-przepływie).

</details>
