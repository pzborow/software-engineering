# Myśl krok po kroku

W poprzednim dziale zobaczyłeś, że komputer wykonuje dokładnie to, co zapisano, więc zanim cokolwiek napiszesz, musisz wiedzieć, jakie kroki mają prowadzić do wyniku. Ten dział uczy, jak takie kroki wymyślić i zapisać: jako [algorytm](00%20Glosariusz.md#algorytm), jako [schemat blokowy](00%20Glosariusz.md#schemat-blokowy) i jako zestaw mniejszych części. Po jego przeczytaniu rozpiszesz prosty problem krok po kroku, dopilnujesz kolejności działań i sprawdzisz, czy wynik jest poprawny. Posłuży nam do tego rozliczenie wspólnych wydatków „Wspólna Kasa”, które podzielimy na części, a te później staną się funkcjami.

```text
problem → algorytm (kroki) → schemat blokowy → mniejsze części → sprawdzenie poprawności
```

**W tym dziale:**

- [Zdefiniuj algorytm](#zdefiniuj-algorytm)
- [Porównaj przepis z algorytmem](#porównaj-przepis-z-algorytmem)
- [Pilnuj kolejności kroków](#pilnuj-kolejności-kroków)
- [Narysuj schemat blokowy](#narysuj-schemat-blokowy)
- [Rozłóż problem na części](#rozłóż-problem-na-części)
- [Sprawdź poprawność algorytmu](#sprawdź-poprawność-algorytmu)

## Zdefiniuj algorytm

Algorytm to skończony ciąg jednoznacznych kroków, który dla podanych danych prowadzi do wyniku. Nie jest jeszcze programem: to sam pomysł na rozwiązanie, który można zapisać zwykłymi słowami, na kartce albo w kodzie.

Dobry algorytm ma trzy cechy. Zaczyna od jasno określonych danych wejściowych. Każdy krok jest na tyle dokładny, że nie wymaga domyślania się: „Podziel sumę przez liczbę osób” jest jednoznaczne, a „rozlicz się jakoś sprawiedliwie” nie. Wreszcie po skończonej liczbie kroków algorytm się kończy i daje wynik.

Weźmy [czworo znajomych na wyjeździe, którzy płacili na zmianę](01%20Wejd%C5%BA%20w%20%C5%9Bwiat%20programowania.md#lm-2). Rozliczenie da się opisać tak:

<a id="lm-8"></a>

```text
dane: lista wydatków (kto, ile) i liczba osób
1. Zsumuj wszystkie wydatki.
2. Podziel sumę przez liczbę osób: to udział jednej osoby.
3. Dla każdej osoby odejmij udział od tego, ile wydała.
4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna.
wynik: saldo każdej osoby
```

<a id="ref-8"></a>Na razie nie piszemy [kodu](00%20Glosariusz.md#kod): to celowo zwykły język. <a id="ref-9"></a>Ten sam algorytm można potem zapisać w Pythonie, w arkuszu kalkulacyjnym albo wykonać ręcznie. Właśnie dlatego warto go oddzielać od kodu.

Konsekwencja: zanim napiszesz program, upewnij się, że masz algorytm. Gdy kroki są jasne na papierze, zamiana ich na kod jest już głównie kwestią zapisu.

<details>
<summary>Na marginesie: Skąd wzięło się słowo „algorytm”</summary>

Słowo „algorytm” pochodzi od zlatynizowanego imienia Muhammada ibn Musy al-Chwarizmiego, uczonego z Bagdadu z IX wieku. Jego traktat o rachunkach zapisywanych cyframi indyjskimi przetłumaczono na łacinę, a średniowieczni Europejczycy zaczęli nazywać takie metody rachowania od jego imienia. Inne jego dzieło, w którego tytule występuje słowo „al-dżabr”, dało z kolei nazwę algebrze.

Źródło: [Al-Khwarizmi – Wikipedia](https://en.wikipedia.org/wiki/Al-Khwarizmi)

</details>

## Porównaj przepis z algorytmem

Przepis kulinarny to algorytm zapisany dla kucharza: ma dane wejściowe (składniki), uporządkowane kroki i wynik (gotowe danie). Różnica polega na tym, że człowiek wybaczy przepisowi niedokładność, a komputer nie.

Zestawmy oba zapisy:

| Przepis | Algorytm |
|---|---|
| składniki i ich ilości | dane wejściowe |
| kolejne kroki: „pokrój”, „wymieszaj” | jednoznaczne instrukcje |
| „piecz 40 minut w 180°C” | [warunek zakończenia](00%20Glosariusz.md#warunek-zakończenia) |
| gotowe ciasto | wynik |

Warunek zakończenia to sprawdzalny test „czy już koniec?”. „Piecz 40 minut” albo „piecz, aż termometr pokaże 95°C w środku” da się zmierzyć. „Piecz, aż się zrumieni” już nie, bo każdy inaczej oceni rumieniec.

Tak samo jest z „dodaj szczyptę soli” czy „smaż chwilę”: kucharz zinterpretuje to po swojemu. W algorytmie musi stać coś takiego jak „Podziel sumę przez liczbę osób”, bez pola na domysły.

Ten sam przepis mogą wykonać różne osoby w różnych kuchniach i wyjdzie to samo danie. Tak samo algorytm da się wykonać w Pythonie, w arkuszu albo na kartce.

Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”. Jej przepis to [cztery kroki rozliczenia, które już znasz](#lm-8): składniki to wydatki i liczba osób, a „danie” to saldo każdego.

Konsekwencja: pisząc algorytm, wyobraź sobie przepis dla kogoś, kto nigdy nie gotował. Jeśli taka osoba wykona go bez pytań, kroki są dość dokładne.

**Ilustracja:** _Jeśli ktoś, kto nigdy nie gotował, wykona przepis bez pytań, kroki są dość dokładne._

Tekst alternatywny: Początkujący kucharz w fartuchu mierzy termometrem temperaturę ciasta w piekarniku, a przyjaciółka z kartką przepisu pokazuje uniesiony kciuk. Na blacie stoją odmierzone składniki i minutnik.

<details>
<summary>Prompt do generatora obrazów</summary>

```text
Jasna kuchnia. Początkujący kucharz w fartuchu stoi przy piekarniku z otwartymi drzwiczkami i ostrożnie wbija cienki termometr w złocisty placek na blasze. Na blacie obok stoją odmierzone miseczki ze składnikami, ustawione równo w rzędzie, oraz kuchenny minutnik. Za jego plecami uśmiechnięta przyjaciółka zagląda mu przez ramię z kartką przepisu w dłoni i unosi kciuk do góry. Nad piekarnikiem nie ma żadnych napisów, cała scena jest spokojna i uporządkowana.

Styl: Ciepła ilustracja w stylu szkicu kredką i akwareli na kremowym papierze, miękka kontur, przyjazne postacie o prostych kształtach, ograniczona paleta: granat, miętowa zieleń, musztardowy żółty i koral. Bez tekstu na obrazkach.
```

Plik obrazu: `ilustracje/02-porównaj-przepis-z-algorytmem-1.png`

</details>

## Pilnuj kolejności kroków

Kolejność ma znaczenie, bo prawie każdy krok korzysta z wyniku poprzedniego. Zamiana miejsc sprawia, że krok dostaje dane, których jeszcze nie ma, i algorytm daje zły wynik albo wcale nie działa.

Weźmy [cztery kroki rozliczenia](#lm-8) we „Wspólnej Kasie”. Ala wydała 60 zł, Bartek 40 zł, Czarek 20 zł. Najpierw sumujemy: 120 zł. Potem dzielimy przez trzy osoby: udział wynosi 40 zł. Na końcu odejmujemy udział od wpłaty każdego.

Teraz zamieńmy kroki: odejmujemy udział, zanim go policzyliśmy.

```text
# poza kanonem
Dobrze:  suma 120 zł --> udział 40 zł --> Ala: 60 - 40 = +20 zł
Źle:     udział jeszcze nieznany (0 zł) --> Ala: 60 - 0 = +60 zł
```

Krok „odejmij udział” nie miał czego odjąć. Zależność między krokami to właśnie taka sytuacja: jeden krok potrzebuje wyniku innego, więc musi stać po nim.

Nie każda para kroków jest tak związana. Policzenie osób i zsumowanie wydatków są niezależne, więc możesz zrobić je w dowolnej kolejności. Oba muszą jednak być gotowe przed dzieleniem.

Konsekwencja: pisząc algorytm, przy każdym kroku zapytaj, skąd bierze dane. Jeśli z wyniku innego kroku, ten krok stoi za nim. Komputer wykona kroki dokładnie w zapisanej kolejności i niczego sam nie przestawi.

> **Wtręt:** Marta zapisała kroki w takiej kolejności: „odejmij udział od wpłaty”, a dopiero potem „policz udział”. Komputer wykonał je dokładnie tak i uznał, że udział wynosi 0 zł, więc każdy współlokator dostał zwrot całej swojej wpłaty. Wszyscy byli zachwyceni do chwili, gdy Marta zauważyła, że czynsz nadal nie jest zapłacony. Wystarczyło przestawić dwa kroki.

> **Z życia wzięte:** W skrypcie automatyzującym raporty krok „spakuj plik do archiwum” stał przed krokiem „wygeneruj plik”. Skrypt nie zgłaszał błędu, bo w katalogu leżał jeszcze raport z poprzedniego dnia i to jego pakował. Przez kilka dni odbiorcy dostawali nieaktualne dane, a nikt niczego nie podejrzewał. Znalazłem przyczynę dopiero po porównaniu dat w archiwum. Od tamtej pory przy każdym kroku sprawdzam, skąd bierze dane, i ustawiam go dopiero za krokiem, który je tworzy.

## Narysuj schemat blokowy

Schemat blokowy to rysunek algorytmu: każdy krok jest w ramce, a strzałki pokazują, w jakiej kolejności je wykonać. Działa jak mapa, po której palcem przejdziesz od początku do końca.

Używa kilku umownych kształtów. Owal oznacza początek albo koniec, prostokąt to zwykły krok, a romb to pytanie, po którym droga rozwidla się na „tak” i „nie”. Krok wykonujesz, gdy dojdziesz do niego strzałką, a nie dlatego, że stoi niżej na kartce.

Oto [rozliczenie „Wspólnej Kasy” z trzema osobami](#lm-8), narysowane znakami tekstowymi:

```text
( Start )
    v
[ Zsumuj wydatki, podziel przez liczbę osób = udział ]
    v
[ Weź kolejną osobę ]
    v
< Wpłaciła więcej niż udział? > --tak--> [ Ma zwrot ] --+
    |nie                                                |
    v                                                   |
[ Ma dopłacić ] ----------------------------------------+
    v
< Są jeszcze osoby? > --tak--> (wróć do „Weź kolejną osobę”)
    |nie
    v
( Koniec )
```

Rysunek ma dwie zalety. Rozgałęzienia i powroty widać od razu, a w opisie słownym łatwo je przeoczyć. Poza tym pokazuje, gdzie algorytm się kończy, czyli sprawdzalny warunek zakończenia.

Konsekwencja: schemat pozwala sprawdzić algorytm na kartce, zanim powstanie kod. Wrócimy do niego przy podziale problemu na części, a „Wspólna Kasa”, przykład, który będzie nam towarzyszył, dostanie z niego kod dopiero później.

> **Z przymrużeniem oka:** Schemat blokowy bez strzałki „nie” wychodzącej z ostatniego rombu przypomina rondo bez zjazdów: wszystko jest poprawnie narysowane, tylko nikt stamtąd nie wyjedzie.

## Rozłóż problem na części

Duży problem dzielisz tak, by każda część miała własne dane wejściowe, jedno zadanie i wynik, który da się sprawdzić osobno. Zaczynasz od całego zadania, a potem pytasz: z jakich mniejszych kroków się składa?

Weźmy „rozlicz wyjazd”. To za dużo naraz, więc rozbijamy to na trzy części. Wracamy tu do [schematu blokowego z poprzedniej sekcji](#narysuj-schemat-blokowy): kroki w jego ramkach to gotowe kandydatki na części.

```text
Rozlicz wyjazd
  |-- 1. Zsumuj wydatki          (wydatki -> suma)
  |-- 2. Policz udział osoby     (suma, liczba osób -> udział)
  `-- 3. Porównaj wpłatę z udziałem
                                 (wpłata, udział -> saldo)
```

Każda część ma jasne wejście i wynik. Część 3 potrzebuje wyniku części 2, a ta wyniku części 1, więc kolejność wynika z tych zależności, [tak jak w sekcji o kolejności kroków](#pilnuj-kolejności-kroków).

Jeśli część nadal jest zbyt duża, dziel ją dalej, aż każdą da się opisać jednym zdaniem. Dobra część daje się też przetestować samodzielnie: znasz jej dane i wiesz, jaki wynik ma wyjść.

Konsekwencja: w programie takie części zamienimy w osobne [funkcje](00%20Glosariusz.md#funkcja), czyli nazwane fragmenty kodu do wielokrotnego użycia. Ich nazwy, np. `suma_wydatkow`, <a id="ref-10"></a>poznasz później, gdy zaczniemy pisać „Wspólną Kasę”, przykład, który będzie nam towarzyszył w kolejnych działach.

> **Wtręt:** Marta wpisała jedną instrukcję: „rozlicz wyjazd”. Kiedy wynik się nie zgadzał, nie umiała powiedzieć, czy zawiodła suma, udział, czy porównanie z wpłatą, bo wszystko siedziało w jednym kawałku. Dopiero podział na trzy części, każda z własnym wynikiem do sprawdzenia, pozwolił jej zajrzeć do sumy i zauważyć, że jeden rachunek został policzony dwa razy.

## Sprawdź poprawność algorytmu

Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny z tym, czego od niego wymagamy. Nie wystarczy, że zadziałał raz na jednym przykładzie.

Najpierw trzeba więc ustalić, co znaczy „zgodny”. To [specyfikacja wyniku](00%20Glosariusz.md#specyfikacja-wyniku): krótki opis, jaki wynik ma wyjść z jakich danych. Dla rozliczenia może brzmieć tak: suma wszystkich sald wynosi 0 zł, a nikomu nie znika ani nie przybywa grosza. Bez takiego opisu nie ma czego sprawdzać.

Potem sprawdzasz dwie rzeczy: czy algorytm zawsze dochodzi do warunku zakończenia i czy wynik spełnia specyfikację. Ważne są zwłaszcza [przypadki brzegowe](00%20Glosariusz.md#przypadek-brzegowy), czyli dane na skraju dozwolonego zakresu: jedna osoba, brak wydatków, kwota, która nie dzieli się równo.

Ten ostatni przypadek łatwo przeoczyć. W kodzie kwoty liczymy w groszach, a znak `//` dzieli i odrzuca resztę: `10000 // 3` daje `3333`, nie `3333,33`.

```python
# poza kanonem: udział w groszach, dzielenie całkowite
def udzial(suma_gr, osoby):
    return suma_gr // osoby

print(udzial(12000, 4) * 4)
print(udzial(10000, 3) * 3)
```

```text
12000
9999
```

Dla 120 zł na czworo wszystko się zgadza. Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza. Dlatego [w naszej liście kroków jest zdanie „Resztę groszy dopisz pierwszej osobie.”](01%20Wejd%C5%BA%20w%20%C5%9Bwiat%20programowania.md#lm-6): bez niego algorytm byłby niepoprawny, choć pierwszy przykład by przeszedł.

Konsekwencja: poprawność sprawdzasz na wielu danych, w tym celowo niewygodnych. [Do systematycznego sprawdzania wrócimy przy testowaniu programu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#ref-32).

## Co zapamiętać

- Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
- Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
- Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.
- Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, dzięki czemu rozgałęzienia, powroty i koniec widać, zanim powstanie kod.
- Dziel problem na części z jasnym wejściem i wynikiem, aż każdą da się opisać jednym zdaniem i sprawdzić osobno.
- Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, także w przypadkach brzegowych.

## Pytania sprawdzające

### 7. Czym jest algorytm?

<details>
<summary>Odpowiedź</summary>

Algorytm to skończony ciąg jednoznacznych kroków, który z danych wejściowych prowadzi do wyniku. Jest pomysłem na rozwiązanie, a nie kodem: można go zapisać słowami, na schemacie albo w dowolnym języku programowania. Program jest jednym ze sposobów wykonania algorytmu.

Zobacz: [sekcja „Zdefiniuj algorytm”](#zdefiniuj-algorytm).

</details>

### 8. Jak przepis kulinarny przypomina algorytm?

<details>
<summary>Odpowiedź</summary>

Przepis ma dane wejściowe (składniki), uporządkowane kroki i wynik (danie), tak jak algorytm. Różnica jest w precyzji: kucharz domyśli się, ile to „szczypta”, a komputer wymaga kroków i warunków zakończenia, które da się sprawdzić.

Zobacz: [sekcja „Porównaj przepis z algorytmem”](#porównaj-przepis-z-algorytmem).

</details>

### 9. Dlaczego kolejność kroków w algorytmie ma znaczenie?

<details>
<summary>Odpowiedź</summary>

Prawie każdy krok algorytmu korzysta z wyniku wcześniejszego, więc zamiana miejsc podsuwa krokowi dane, których jeszcze nie ma. Wynik jest wtedy błędny albo algorytm w ogóle nie działa. Kroki niezależne od siebie można zamieniać, ale zależne muszą stać w porządku wyznaczonym przez dane. Komputer wykonuje kroki dokładnie tak, jak je zapisano.

Zobacz: [sekcja „Pilnuj kolejności kroków”](#pilnuj-kolejności-kroków).

</details>

### 10. Czym jest schemat blokowy?

<details>
<summary>Odpowiedź</summary>

Schemat blokowy to rysunek algorytmu: kroki są w ramkach, a strzałki pokazują kolejność ich wykonywania. Owal oznacza początek lub koniec, prostokąt zwykły krok, romb pytanie z rozgałęzieniem „tak” i „nie”. Dzięki niemu widać rozgałęzienia, powroty i koniec algorytmu, zanim powstanie kod.

Zobacz: [sekcja „Narysuj schemat blokowy”](#narysuj-schemat-blokowy).

</details>

### 11. Jak podzielić duży problem na mniejsze części?

<details>
<summary>Odpowiedź</summary>

Dziel problem na części, z których każda ma własne dane wejściowe, jedno zadanie i wynik, który można sprawdzić osobno. Jeśli część jest nadal duża, dziel ją dalej, aż da się ją opisać jednym zdaniem. Kolejność części wynika z tego, która potrzebuje wyniku której.

Zobacz: [sekcja „Rozłóż problem na części”](#rozłóż-problem-na-części).

</details>

### 12. Co to znaczy, że algorytm jest poprawny?

<details>
<summary>Odpowiedź</summary>

Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, a nie tylko dla jednego przykładu. Trzeba więc najpierw opisać, jaki wynik jest właściwy, a potem sprawdzić algorytm także na przypadkach brzegowych, np. gdy kwota nie dzieli się równo.

Zobacz: [sekcja „Sprawdź poprawność algorytmu”](#sprawdź-poprawność-algorytmu).

</details>
