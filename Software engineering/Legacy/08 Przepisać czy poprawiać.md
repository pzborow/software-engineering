# Przepisać czy poprawiać

Każdy zespół pracujący z legacy w końcu mówi: „łatwiej byłoby napisać to od nowa”. Czasem to prawda, ale znacznie częściej przepisanie trwa dłużej, kosztuje więcej i daje gorszy wynik, niż zakładano. Ten rozdział wyjaśnia, dlaczego duże przepisania tak często zawodzą, kiedy mimo to są uzasadnione i jak przedstawić biznesowi decyzję o pracy nad legacy.

```text
przepisanie od zera                       stopniowa poprawa
───────────────────────────────────────   ───────────────────────────────────────
miesiące bez nowej wartości               wartość po każdym kroku
dwa systemy do utrzymania                 jeden system, zmieniany w miejscu
ryzyko skumulowane na koniec              ryzyko rozłożone na małe zmiany
nowe błędy w miejsce starych              stare błędy znane i opisane testami
decyzja nieodwracalna po roku             można przerwać w każdej chwili
```

## Dlaczego przepisania zawodzą

<a id="term-big-rewrite"></a>[Big rewrite](00%20Glossary%20Legacy.md#big-rewrite) to zastąpienie istniejącego systemu nowym, pisanym od zera, z przełączeniem w jednym momencie. Joel Spolsky w eseju „Things You Should Never Do” (2000) nazwał to najgorszym strategicznym błędem, jaki może popełnić firma programistyczna, na przykładzie Netscape, który przepisywał przeglądarkę przez trzy lata, tracąc w tym czasie rynek.

Powody porażek są powtarzalne:

- stary kod zawiera wiedzę, której nikt nie spisał. Każdy dziwny warunek w `generate_invoice` to kiedyś zgłoszony błąd albo wymaganie klienta. Nowy system popełnia te same błędy na nowo,
- ruchomy cel: w czasie przepisywania stary system musi być rozwijany, bo biznes nie czeka. Nowy system goni zmiany, które ciągle się pojawiają,
- <a id="term-feature-parity"></a>[parytet funkcji](00%20Glossary%20Legacy.md#feature-parity) okazuje się dużo większy, niż zakładano. Lista „co robi stary system” ciągle rośnie, bo ujawniają się funkcje, o których nikt nie pamiętał,
- brak wartości przez długi czas: przez miesiące zespół pracuje, a użytkownicy nie widzą zmian, więc cierpliwość biznesu się kończy,
- ryzyko skumulowane w jednym przełączeniu, które odbywa się przy największej niewiedzy o tym, co może pójść źle,
- dwa systemy do utrzymania przez cały okres przepisywania, a często dłużej, bo stary nie znika.

Fred Brooks w „The Mythical Man-Month” (1975) opisał jeszcze jedno zjawisko: <a id="term-second-system-effect"></a>[efekt drugiego systemu](00%20Glossary%20Legacy.md#second-system-effect). Zespół, który projektuje następcę systemu, z którego był niezadowolony, próbuje umieścić w nim wszystkie odłożone pomysły, uogólnienia i „porządne rozwiązania”. Drugi system staje się przeprojektowany, większy i bardziej skomplikowany niż potrzeba. W przepisywaniu legacy objawia się to frameworkiem do reguł podatkowych zamiast funkcji liczącej VAT i mikroserwisami zamiast jednego modułu.

Warto też pamiętać o <a id="term-chestertons-fence"></a>[płocie Chestertona](00%20Glossary%20Legacy.md#chestertons-fence), zasadzie G.K. Chestertona: nie usuwaj płotu, dopóki nie wiesz, dlaczego go postawiono. Warunek `if customer["type"] == "B2B" and customer["country"] != "PL": vat = 0` wygląda na hack, a jest wymogiem prawa podatkowego. Przepisanie „od czystej kartki” usuwa wszystkie płoty naraz.

## Kiedy przepisanie ma sens

Przepisanie bywa uzasadnione, ale rzadziej, niż się wydaje. Sygnały, które przemawiają za nim:

- technologia jest martwa i nie da się jej utrzymać: język lub platforma bez wsparcia, brak łatek bezpieczeństwa, brak ludzi na rynku, np. aplikacja w Visual Basic 6, system na Pythonie 2 z zależnościami, których nie da się zaktualizować,
- system jest mały i dobrze zrozumiany, więc przepisanie trwa tygodnie, a nie lata,
- zmieniły się fundamentalne założenia: system dla jednego klienta ma obsłużyć tysiące, model danych nie pasuje do nowego biznesu, a stopniowa zmiana dotknęłaby każdej linii,
- koszt utrzymania jest mierzalnie wyższy niż koszt budowy, a stopniowa poprawa była próbowana i nie działa,
- system da się przepisać fragmentami z punktem przechwycenia, czyli w praktyce strangler fig zamiast big bang.

Ostatni punkt jest kluczowy. Nawet gdy przepisanie jest uzasadnione, rzadko powinno być jednorazowym przełączeniem. Przepisanie moduł po module, z nowym kodem przejmującym kolejne funkcje i z parallel run dla każdego modułu, łączy zalety nowego kodu z bezpieczeństwem stopniowej zmiany.

| Pytanie | Poprawiać | Przepisać (stopniowo) |
|---|---|---|
| Czy technologia jest wspierana? | tak | nie |
| Czy system jest duży i słabo zrozumiany? | tak | nie |
| Czy architektura pasuje do przyszłych potrzeb? | w większości tak | fundamentalnie nie |
| Czy stopniowa poprawa była próbowana? | nie albo z sukcesem | tak, bez efektu |
| Czy da się przepisać fragmentami? | nie dotyczy | tak |

## Rozmowa z biznesem

Praca nad legacy konkuruje o czas z nowymi funkcjami. Żeby ją dostać, trzeba mówić językiem biznesu: pieniądze, czas, ryzyko. „Kod jest brzydki” nie jest argumentem.

Najpierw trzeba zebrać dane:

- czas realizacji zmian w obszarze legacy w porównaniu z innymi obszarami, np. zmiana stawki VAT trwa 8 dni, a podobna zmiana w module wysyłek 1 dzień,
- liczba i koszt incydentów: błędne faktury, korekty, reklamacje klientów B2B, godziny supportu,
- ryzyko: brak aktualizacji bezpieczeństwa, wiedza skupiona w jednej osobie, zbliżające się zmiany prawa (np. obowiązkowy KSeF), których stary kod nie udźwignie,
- utracone możliwości: funkcje, których nie da się zrobić albo które odkłada się z powodu legacy.

Potem przedstawia się propozycję jako inwestycję, a nie koszt. Dobrze działa pojęcie <a id="term-cost-of-delay"></a>[kosztu opóźnienia](00%20Glossary%20Legacy.md#cost-of-delay) (cost of delay), czyli tego, ile firma traci za każdy tydzień, w którym problem nie jest rozwiązany.

```text
Propozycja: 6 tygodni pracy nad modułem fakturowania (2 osoby)

Stan obecny                                  Po zmianie
zmiana reguły VAT: 8 dni                     zmiana reguły VAT: 1 dzień
błędne faktury: 12 miesięcznie, ~40 h korekt  błędne faktury: 1–2 miesięcznie (testy regresji)
KSeF: wdrożenie w starym kodzie ~3 miesiące   KSeF: wdrożenie ~3 tygodnie w nowym module

Koszt: 12 osobotygodni.
Zwrot: ~40 h korekt miesięcznie, szybsze zmiany cennika, zdążenie z KSeF przed terminem ustawowym.
Ryzyko braku działań: kary za brak KSeF, rosnący czas każdej zmiany.
```

Dobre praktyki takiej rozmowy:

- małe kroki z widocznymi efektami zamiast jednej dużej prośby o „kwartał na refaktoryzację”,
- łączenie pracy nad legacy z konkretną potrzebą biznesu, np. „żeby wdrożyć KSeF, musimy najpierw wydzielić obliczanie kwot”,
- mierzenie efektu po zmianie i raportowanie go, co buduje zaufanie przy kolejnych prośbach,
- uczciwość co do niepewności: podawanie przedziałów zamiast jednej liczby i zaznaczanie, czego jeszcze nie wiadomo.

## Co zapamiętać

- Big rewrite zawodzi przez utraconą wiedzę w starym kodzie, ruchomy cel, niedoszacowany parytet funkcji, brak wartości po drodze i ryzyko skumulowane na koniec.
- Efekt drugiego systemu (Brooks) sprawia, że następca jest przeprojektowany.
- Płot Chestertona: nie usuwaj warunku, dopóki nie wiesz, dlaczego istnieje.
- Przepisanie ma sens przy martwej technologii, małym i zrozumiałym systemie, zmienionych fundamentach i nieudanej stopniowej poprawie, a i tak najlepiej fragmentami.
- Z biznesem rozmawia się danymi: czas zmian, koszt incydentów, ryzyko, utracone możliwości, koszt opóźnienia.
- Pracę nad legacy przedstawia się jako inwestycję w małych krokach, powiązaną z konkretną potrzebą biznesu i mierzoną po wykonaniu.

## Pytania sprawdzające

### 32. Dlaczego duże przepisania (big rewrite) tak często się nie udają? Czym jest efekt drugiego systemu?

<details>
<summary>Odpowiedź</summary>

Bo stary kod zawiera niespisaną wiedzę (poprawki błędów, wymagania klientów, przepisy), którą nowy system traci. Stary system trzeba dalej rozwijać, więc cel się przesuwa. Parytet funkcji okazuje się większy, niż zakładano. Przez miesiące nie ma wartości dla użytkowników. Ryzyko kumuluje się w jednym przełączeniu, a przez cały czas trzeba utrzymywać dwa systemy (Spolsky, przypadek Netscape). Efekt drugiego systemu (Brooks, „The Mythical Man-Month”) to skłonność do przeprojektowania następcy: odłożone pomysły i uogólnienia sprawiają, że jest większy i bardziej złożony niż potrzeba. Płot Chestertona przypomina, żeby nie usuwać niezrozumianych warunków.

Zobacz: sekcja „Dlaczego przepisania zawodzą”.

</details>

### 33. Kiedy przepisanie od nowa jest jednak uzasadnione?

<details>
<summary>Odpowiedź</summary>

Gdy technologia jest martwa (brak wsparcia, łatek, ludzi na rynku), system jest mały i dobrze zrozumiany, fundamentalne założenia się zmieniły (skala, model danych), koszt utrzymania jest mierzalnie wyższy od kosztu budowy, a stopniowa poprawa była próbowana bez efektu. Nawet wtedy najlepiej przepisywać fragmentami, z punktem przechwycenia, strangler fig i parallel run dla każdego modułu, zamiast jednorazowego przełączenia.

Zobacz: sekcja „Kiedy przepisanie ma sens”.

</details>

### 34. Jak przedstawić biznesowi koszt i wartość pracy nad legacy, żeby dostać na nią czas?

<details>
<summary>Odpowiedź</summary>

Językiem pieniędzy, czasu i ryzyka, na podstawie danych: czas zmian w obszarze legacy wobec innych obszarów, liczba i koszt incydentów, ryzyka (bezpieczeństwo, wiedza w jednej osobie, zmiany prawa jak KSeF) i utracone możliwości. Propozycję przedstawia się jako inwestycję z kosztem, zwrotem i kosztem opóźnienia. W praktyce: małe kroki z widocznymi efektami zamiast kwartału na refaktoryzację, powiązanie z konkretną potrzebą biznesu, mierzenie i raportowanie efektów oraz uczciwe przedziały niepewności.

Zobacz: sekcja „Rozmowa z biznesem”.

</details>
