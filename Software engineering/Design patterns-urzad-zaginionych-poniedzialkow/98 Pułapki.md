# Pułapki

Nieoczywiste zachowania kodu z przykładów, które prowadzą do błędów w produkcji albo w testach. Łowca pułapek sprawdza tylko sekcje z kodem i nie wypisuje niczego na siłę.

Sekcje z kodem: 46 · sprawdzone: 46 · pułapki tematu: 19 · poboczne: 3

## Pułapki tematu

Ilustrują zagadnienia, których dotyczy tutorial. Te same uwagi są w ramkach pod sekcjami.

### 01. Interfejsy ABC i Protocol

- **Podwójna dyspozycja / Visitor:** **Nowy typ elementu bez metody w Kontroler.** Każdy nowy typ elementu wymaga równoległej metody `dla_...` w `Kontroler` i we wszystkich kontrolerach. Brak jej wychodzi dopiero w runtime jako `AttributeError` przy `przyjmij`, a nie przy definicji klasy. Wspólny interfejs (ABC z `@abstractmethod`) przenosi błąd na instancjonowanie.
  Dotyczy: `def przyjmij(self, k): return k.dla_zalacznika(self)` · [sekcja „Idea podwójnej dyspozycji”](01%20Interfejsy%20ABC%20i%20Protocol.md#idea-podwójnej-dyspozycji)

- **wzorzec behawioralny: lista kontroli zamiast jednej metody:** **all() przerywa listę kontroli na pierwszej odmowie.** `all(k.sprawdz(wniosek) for k in kontrole)` jest leniwe: po pierwszym `False` kolejne kontrole w ogóle się nie wykonują. Kolejność ma więc znaczenie, a kontrola z efektem ubocznym (audyt, zbieranie powodów odmowy) lub kosztowna zależność może nie zostać uruchomiona. Gdy potrzeba pełnego raportu, trzeba najpierw zebrać wyniki wszystkich kontroli do listy.
  Dotyczy: `ok = all(k.sprawdz(wniosek) for k in kontrole)` · [sekcja „Trzy rodziny wzorców”](01%20Interfejsy%20ABC%20i%20Protocol.md#trzy-rodziny-wzorców)

- **Podwójna dyspozycja w Visitorze:** **Podklasa po cichu odwiedzana jako klasa bazowa.** `WniosekPilny` dziedziczy `przyjmij`, więc każdy wizytator dostaje go w `odwiedz_wniosek` jako zwykły `Wniosek`. Żaden błąd ani ostrzeżenie nie pojawia się, a logika dla pilnych wniosków po cichu nie działa. Trzeba nadpisać `przyjmij` w każdej podklasie, której wizytatorzy mają rozróżniać, i dodać `odwiedz_wniosek_pilny` do kontraktu.
  Dotyczy: `w.odwiedz_wniosek(self)` · [sekcja „Koszt podwójnej dyspozycji”](01%20Interfejsy%20ABC%20i%20Protocol.md#koszt-podwójnej-dyspozycji)

### 02. Model domeny wniosku

- **Abstract Factory, rodzina produktów:** **Fabryki jako współdzielone singletony w słowniku.** `FABRYKI` tworzy po jednej instancji na format, a `fabryka_dla` zwraca tę samą za każdym razem. Fabryka zwraca produkty przez `parser()` i `walidator()`, więc jeśli produkty kiedyś trzymają stan (cache, konfiguracja), będzie on współdzielony między wszystkimi klientami i testami. Fabryka powinna być bezstanowa albo tworzyć nowe produkty przy każdym wywołaniu.
  Dotyczy: `FABRYKI = {"iso": FabrykaIso(), "pl": FabrykaPolska()}` · [sekcja „Abstract Factory dla kalendarzy”](02%20Model%20domeny%20wniosku.md#abstract-factory-dla-kalendarzy)

### 03. Tworzenie wniosków

- **Builder:** **Builder wielokrotnego użytku przecieka stan.** `_pola` i `_powod` żyją w instancji, a `build()` ich nie zeruje. Ponowne użycie tego samego budowniczego dla kolejnego wniosku odziedziczy `pilny` i stare pola, więc powstanie `WniosekPilny` zamiast `Wniosek`. Twórz nowego budowniczego na każdy wniosek albo czyść stan w `build()`.
  Dotyczy: `self._pola["pieczatka"].zweryfikuj(rok_biezacy)` · [sekcja „Builder składa wniosek”](03%20Tworzenie%20wniosk%C3%B3w.md#builder-składa-wniosek)

- **Decorator: opakowania są przezroczyste dla klienta, ale nie dla introspekcji typu:** **Dziennik przy zagnieżdżeniu loguje nazwę opakowania.** `type(self._wewnetrzna).__name__` zwraca klasę bezpośrednio opakowanego obiektu. Gdy dziennik stoi wokół licznika wokół `KontrolaPoniedzialku`, wpis brzmi np. `KontrolaZLicznikiem: True`, a nie nazwa właściwej kontroli. Ten sam problem dotyczy `isinstance` i `type()` na opakowanej kontroli. Rozwiązanie: dekorator wystawia nazwę (np. `nazwa` przekazywaną w dół łańcucha) albo loguje się jawną etykietę.
  Dotyczy: `self._dziennik.append(f"{type(self._wewnetrzna).__name__}: {wynik}")` · [sekcja „Decorator obiektowy kontra funkcyjny”](03%20Tworzenie%20wniosk%C3%B3w.md#decorator-obiektowy-kontra-funkcyjny)

### 04. Struktury wniosku

- **Fasada koordynująca podsystem:** **Fasada trzyma stan i zdarzenie ginie.** `zdecyduj` zmienia status wniosku w słowniku `_wnioski` (stan w pamięci fasady) i tworzy `DecyzjaPodjeta` tylko lokalnie, przekazując je do `Powiadomienie`. Jeśli `o_decyzji` rzuci wyjątek po zmianie statusu, wniosek ma już nowy status, a klient nie dostaje wyniku ani zdarzenia. Zdarzenie z `poprzedni_status` nie jest nigdzie zachowane, więc obiecane cofnięcie nie ma na czym działać. Kolejność: najpierw powiadomienie albo trwały zapis zdarzenia w spójnej operacji.
  Dotyczy: `self._powiadomienie.o_decyzji(zdarzenie, adresat)` · [sekcja „Fasada jako okienko urzędu”](04%20Struktury%20wniosku.md#fasada-jako-okienko-urzędu)

- **Proxy leniwy (leniwa inicjalizacja):** **Wyścig przy leniwym tworzeniu weryfikatora.** Sprawdzenie `self._prawdziwy is None` i przypisanie nie są atomowe. Przy współbieżnych pierwszych wywołaniach (wątki) powstaje kilka weryfikatorów, a licznik `utworzone` przestaje być równy 1. Zabezpiecz tworzenie blokadą albo utwórz weryfikator przed udostępnieniem zastępnika.
  Dotyczy: `if self._prawdziwy is None: self._prawdziwy = self._utworz()` · [sekcja „Proxy jako strażnik weryfikatora”](04%20Struktury%20wniosku.md#proxy-jako-strażnik-weryfikatora)

- **Command: dane do cofnięcia zapisane poza poleceniem:** **Undo przywraca stan z głosowania, nie sprzed execute.** `undo` wpisuje `self.wynik.poprzedni_status`, zapisany w chwili głosowania, a nie status z momentu `execute`. Jeśli między głosowaniem a `execute` status `Wniosek` się zmienił (np. wykonano inne polecenie na tym samym wniosku), cofnięcie przywróci nieaktualną wartość i złamie odwrotną kolejność stosu. Stan do cofnięcia należy zapisywać w `execute`, z bieżącego `self.cel.status`.
  Dotyczy: `self.cel.status = self.wynik.poprzedni_status` · [sekcja „Command i cofanie decyzji”](04%20Struktury%20wniosku.md#command-i-cofanie-decyzji)

### 05. Przepływ komisji

- **Mediator jako właściciel reguły współpracy (zliczanie i moment decyzji):** **Mediator zlicza głosy, nie członków.** `zglos` porównuje tylko `len(self._glosy)` z `_liczba`, więc ten sam `CzlonekKomisji` może zagłosować dwa razy i zamknąć głosowanie za nieobecnych. Każdy głos po osiągnięciu progu też zwraca kolejną `Decyzja`, bo warunek to `<`, a nie stan zamknięcia. Ponieważ członkowie nie znają siebie nawzajem, jedyną barierą jest mediator: trzeba w nim śledzić, kto już głosował, i pamiętać o zamknięciu głosowania.
  Dotyczy: `if len(self._glosy) < self._liczba: return None` · [sekcja „Mediator w środku komisji”](05%20Przep%C5%82yw%20komisji.md#mediator-w-środku-komisji)

- **Memento: zakres zapisywanego stanu:** **Migawka z vars(self) kopiuje też współpracowników.** `copy.deepcopy(vars(self))` obejmuje każde pole wniosku, także referencje do obiektów zewnętrznych, np. obserwatorów, mediatora czy dziennika. `przywroc` podmienia je wtedy na kopie, więc wniosek przestaje powiadamiać oryginalne obiekty, a zapis do dziennika trafia do duplikatu. Zapisuj tylko jawnie wybrane pola stanu albo wyłącz zależności z migawki.
  Dotyczy: `vars(self).update(copy.deepcopy(migawka._stan))` · [sekcja „Memento jako migawka wniosku”](05%20Przep%C5%82yw%20komisji.md#memento-jako-migawka-wniosku)

- **Observer: uchwyt wypisania i sprzątanie martwych subskrypcji:** **Uchwyt wypisania rzuca ValueError przy ponownym użyciu.** `lambda: self._refy.remove(ref)` rzuci `ValueError`, jeśli `ref` już usunięto: przy drugim wywołaniu uchwytu albo gdy `publikuj` sprzątnęło wcześniej martwą referencję. Obie metody sprzątania (uchwyt i odśmiecacz) się na siebie nakładają, więc uchwyt powinien być idempotentny, np. sprawdzać `if ref in self._refy`.
  Dotyczy: `return lambda: self._refy.remove(ref)` · [sekcja „Observer i subskrybenci zdarzeń”](05%20Przep%C5%82yw%20komisji.md#observer-i-subskrybenci-zdarzeń)

- **State:** **Status jako napis rozjeżdża się ze stanem.** Stan istnieje tylko chwilowo: `STANY[wniosek.status]()` tworzy obiekt, a do `Wniosek` wraca sam napis `.nazwa`. Jeśli `decyduj` rzuci wyjątek po utworzeniu `Decyzji`, decyzja z `poprzedni_status` już powstała, a status się nie zmienił. Kolejność operacji nie jest atomowa, więc powstaje decyzja bez przejścia. Najpierw wywołaj `decyduj`, potem twórz `Decyzję`.
  Dotyczy: `wniosek.status = STANY[wniosek.status]().decyduj(decyzja.przyznana).nazwa` · [sekcja „State zamiast ifów po statusie”](05%20Przep%C5%82yw%20komisji.md#state-zamiast-ifów-po-statusie)

- **Strategy jako klasa ze stanem:** **Strategia ze stanem współdzielona między komisje.** Instancja `Kwalifikowana` trzyma `wyniki` i ta sama `kw` użyta w kilku głosowaniach lub komisjach miesza historię. Lista rośnie bez końca i jest niebezpieczna przy współbieżnym użyciu. Twórz instancję na komisję albo resetuj stan.
  Dotyczy: `self.ulamek, self.wyniki = ulamek, []` · [sekcja „Strategia jako funkcja albo klasa”](05%20Przep%C5%82yw%20komisji.md#strategia-jako-funkcja-albo-klasa)

- **hak w Template Method:** **Hak bez return po cichu blokuje głosowanie.** Baza sprawdza wynik `kontrola` przez `if not self.kontrola(wniosek)`. Podklasa, która nadpisze hak i zapomni o `return` na którejś ścieżce, zwraca `None`, więc szablon traktuje to jak odmowę. `rozpatrz` zwraca wtedy stary `wniosek.status`, nie zgłasza błędu i nie odróżnia „odrzucono kontrolę” od „jeszcze nie rozpatrzono”. Pilnuj tego testem każdej ścieżki nadpisanego haka albo wymuś `bool` zwracany z haka.
  Dotyczy: `if not self.kontrola(wniosek): return wniosek.status` · [sekcja „Template Method i szablon rozpatrzenia”](05%20Przep%C5%82yw%20komisji.md#template-method-i-szablon-rozpatrzenia)

- **Visitor ze stanem:** **Wizytator liczy stan, którego nie da się użyć ponownie.** `RaportStatusow` trzyma `liczniki` w instancji, więc drugie `teczka.przyjmij(raport)` dolicza do starych wyników zamiast zacząć od zera. Dla każdego przejścia twórz nowego wizytatora albo dodaj reset.
  Dotyczy: `self.liczniki = Counter()` · [sekcja „Visitor i raporty po teczkach”](05%20Przep%C5%82yw%20komisji.md#visitor-i-raporty-po-teczkach)

- **Observer w sekwencji składanej przez fasadę (granica wycofania zmian):** **Wyjątek obserwatora po zmianie statusu bez cofnięcia.** `publikuj` jest poza blokiem `try`, więc gdy któryś obserwator rzuci wyjątek, `wniosek.status` zostaje już zmieniony, a `migawka` nie jest przywrócona. Wywołujący widzi błąd, choć decyzja zapadła, a część obserwatorów mogła nie dostać `DecyzjaPodjeta`. Trzeba objąć publikację tą samą granicą błędu albo odizolować wyjątki obserwatorów w `Publikator`.
  Dotyczy: `publikator.publikuj(DecyzjaPodjeta(wniosek.numer, przyznana, decyzja.poprzedni_status))` · [sekcja „Od kontroli do decyzji”](05%20Przep%C5%82yw%20komisji.md#od-kontroli-do-decyzji)

### 06. System Urzędu Zaginionych Poniedziałków

- **Observer: zakres subskrypcji:** **Subskrypcja bez filtra słyszy cudze wnioski.** Lambda podpięta do wspólnego `Publikator` dostaje każde `DecyzjaPodjeta` i `DecyzjaCofnieta`, także z innych wniosków. `adresat` dostanie powiadomienia o cudzych sprawach, dopóki nie wywoła `wypisz`. Filtruj po `numer` w lambdzie albo twórz publikatora per sprawa.
  Dotyczy: `wypisz = pub.subskrybuj(lambda z: powiadomienie.o_decyzji(z, adresat))` · [sekcja „Decyzja z powiadomieniami i cofaniem”](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#decyzja-z-powiadomieniami-i-cofaniem)

- **State jako Enum ze słownikiem przejść:** **Słownik przejść rzuca KeyError na stanie końcowym.** `PRZEJSCIA[(Status(wniosek.status), decyzja.przyznana)]` zna tylko przejścia z `ZLOZONY`. Decyzja dla wniosku już `PRZYZNANY` albo `ODRZUCONY` kończy się `KeyError`, a nie czytelnym odrzuceniem. Klasy State egzekwują dozwolone przejścia we własnych metodach. Przy słowniku trzeba użyć `.get` i jawnie obsłużyć brak przejścia.
  Dotyczy: `nowy = PRZEJSCIA[(Status(wniosek.status), decyzja.przyznana)]` · [sekcja „Trzy wzorce i ich prostsze idiomy”](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md#trzy-wzorce-i-ich-prostsze-idiomy)

## Pułapki poboczne (Python i narzędzia przykładów)

Wynikają z narzędzi użytych do pokazania przykładów, a nie z tematu. Nie ma ich w tekście, żeby nie rozpraszały czytania.

### 01. Interfejsy ABC i Protocol

- **Protocol i typowanie strukturalne:** **Protocol bez @runtime_checkable nie działa z isinstance.** `Kalendarz` to zwykły Protocol, więc `isinstance(obj, Kalendarz)` rzuci `TypeError`, a zgodność sprawdza tylko type checker. Z `@runtime_checkable` isinstance sprawdza jedynie obecność metod, nie ich sygnatury (np. `rok: int` czy typ zwracany), więc obcy obiekt o innej sygnaturze przejdzie test i wybuchnie dopiero przy wywołaniu.
  Dotyczy: `class Kalendarz(Protocol):` · [sekcja „ABC czy Protocol”](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol)

- **Protocol vs ABC, moment wykrycia błędu:** **Brak dziedziczenia = brak błędu w runtime.** `KalendarzObcy` z literówką w nazwie metody albo złą sygnaturą utworzy się bez błędu. Niezgodność wykryje tylko mypy, a bez niego w produkcji zobaczymy `AttributeError` przy użyciu. Inaczej niż `Kontrola` z `@abstractmethod`, która zawodzi już w konstruktorze. Trzeba uruchamiać type checker w CI.
  Dotyczy: `class KalendarzObcy: # nie dziedziczy po Kalendarz` · [sekcja „ABC czy Protocol”](01%20Interfejsy%20ABC%20i%20Protocol.md#abc-czy-protocol)

- **atrapa zależności zgodna z kontraktem interfejsu (Protocol/ABC):** **spec nie sprawdza sygnatury metod kontraktu.** `Mock(spec=Kalendarz)` pilnuje tylko nazw atrybutów. Wywołanie `poniedzialki` z błędną liczbą lub nazwą argumentów przejdzie, a test zazieleni się mimo niezgodności z kontraktem. Użyj `create_autospec(Kalendarz, instance=True)`, który wymusza też sygnatury.
  Dotyczy: `kalendarz = Mock(spec=Kalendarz)` · [sekcja „Atrapa z podglądem wywołań”](01%20Interfejsy%20ABC%20i%20Protocol.md#atrapa-z-podglądem-wywołań)
