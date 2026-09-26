# Krok 1187 · audytor_pokrycia

Węzeł: `coverage` · dział: 2 · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem pokrycia tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.

Dla KAŻDEGO pytania oceń, czy treść sekcji działu naprawdę na nie odpowiada na poziomie: początkujący.
Samo użycie terminu nie jest odpowiedzią. Pytania o decyzje i kompromisy wymagają uzasadnienia albo ograniczeń.
status: covered | partial | uncovered. section_ids: id sekcji w nawiasach kwadratowych, które odpowiadają.
explanation: jedno-dwa zdania; dla partial/uncovered napisz konkretnie, czego brakuje.

PYTANIA:
- 7. Czym jest algorytm?
  odpowiedź: Algorytm to skończony ciąg jednoznacznych kroków, który z danych wejściowych prowadzi do wyniku. Jest pomysłem na rozwiązanie, a nie kodem: można go zapisać słowami, na schemacie albo w dowolnym języku programowania. Program jest jednym ze sposobów wykonania algorytmu.
  sekcje pisarza: sec-02-czym-jest-algorytm
- 8. Jak przepis kulinarny przypomina algorytm?
  odpowiedź: Przepis ma dane wejściowe (składniki), uporządkowane kroki i wynik (danie), tak jak algorytm. Różnica jest w precyzji: kucharz domyśli się, ile to „szczypta”, a komputer wymaga kroków i warunków zakończenia, które da się sprawdzić.
  sekcje pisarza: sec-02-przepis-jako-algorytm
- 9. Dlaczego kolejność kroków w algorytmie ma znaczenie?
  odpowiedź: Prawie każdy krok algorytmu korzysta z wyniku wcześniejszego, więc zamiana miejsc podsuwa krokowi dane, których jeszcze nie ma. Wynik jest wtedy błędny albo algorytm w ogóle nie działa. Kroki niezależne od siebie można zamieniać, ale zależne muszą stać w porządku wyznaczonym przez dane. Komputer wykonuje kroki dokładnie tak, jak je zapisano.
  sekcje pisarza: sec-02-kolejnosc-krokow-algorytmu
- 10. Czym jest schemat blokowy?
  odpowiedź: Schemat blokowy to rysunek algorytmu: kroki są w ramkach, a strzałki pokazują kolejność ich wykonywania. Owal oznacza początek lub koniec, prostokąt zwykły krok, romb pytanie z rozgałęzieniem „tak” i „nie”. Dzięki niemu widać rozgałęzienia, powroty i koniec algorytmu, zanim powstanie kod.
  sekcje pisarza: sec-02-czym-jest-schemat-blokowy
- 11. Jak podzielić duży problem na mniejsze części?
  odpowiedź: Dziel problem na części, z których każda ma własne dane wejściowe, jedno zadanie i wynik, który można sprawdzić osobno. Jeśli część jest nadal duża, dziel ją dalej, aż da się ją opisać jednym zdaniem. Kolejność części wynika z tego, która potrzebuje wyniku której.
  sekcje pisarza: sec-02-podzial-problemu-na-czesci
- 12. Co to znaczy, że algorytm jest poprawny?
  odpowiedź: Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, a nie tylko dla jednego przykładu. Trzeba więc najpierw opisać, jaki wynik jest właściwy, a potem sprawdzić algorytm także na przypadkach brzegowych, np. gdy kwota nie dzieli się równo.
  sekcje pisarza: sec-02-poprawny-algorytm

OBIETNICE złożone wcześniej w tutorialu, które mogą być spełnione w tym dziale. Dla każdej podaj w promises:
status spełniona | częściowo | brak, section_id sekcji, która ją spełnia, quote = dokładny cytat (5-15 słów) z tej sekcji
i explanation (czego brakuje, gdy nie spełniona).
- ref-8: „Na razie nie piszemy kodu” (kod pojawi się w dalszych działach)
- ref-9: „języku, którego użyjemy w tym tutorialu” (Python jako język tutorialu)
- ref-10: „Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”” (Python i budowa programu „Wspólna Kasa” omówione później)
- ref-16: „Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach)
- ref-19: „Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”” (zapowiedź, że Wspólna Kasa wraca w kolejnych działach)
- ref-23: „Wrócimy do niego przy podziale problemu na części” (schemat blokowy jako narzędzie podziału problemu); ma ją spełnić pytanie 11
- ref-24: „przykład, który będzie nam towarzyszył” (Wspólna Kasa wraca w kolejnych działach)
- ref-25: „dostanie z niego kod dopiero później” (kod Wspólnej Kasy pojawi się w dalszych działach)
- ref-30: „przykład, który będzie nam towarzyszył w kolejnych działach” (Wspólna Kasa wraca w kolejnych działach)

SEKCJE DZIAŁU 02 "Algorytmy i myślenie krokowe":
[sec-02-czym-jest-algorytm] ## Czym jest algorytm
[[algorytm|Algorytm]] to skończony ciąg jednoznacznych kroków, który dla podanych danych prowadzi do wyniku. Nie jest jeszcze programem: to sam pomysł na rozwiązanie, który można zapisać zwykłymi słowami, na kartce albo w kodzie.

Dobry algorytm ma trzy cechy. Zaczyna od jasno określonych danych wejściowych. Każdy krok jest na tyle dokładny, że nie wymaga domyślania się: „Podziel sumę przez liczbę osób” jest jednoznaczne, a „rozlicz się jakoś sprawiedliwie” nie. Wreszcie po skończonej liczbie kroków algorytm się kończy i daje wynik.

Weźmy czworo znajomych na wyjeździe, którzy płacili na zmianę. Rozliczenie da się opisać tak:

```text
dane: lista wydatków (kto, ile) i liczba osób
1. Zsumuj wszystkie wydatki.
2. Podziel sumę przez liczbę osób: to udział jednej osoby.
3. Dla każdej osoby odejmij udział od tego, ile wydała.
4. Wynik dodatni: reszta jest jej winna. Ujemny: sama jest winna.
wynik: saldo każdej osoby
```

Na razie nie piszemy kodu: to celowo zwykły język. Ten sam algorytm można potem zapisać w Pythonie, w arkuszu kalkulacyjnym albo wykonać ręcznie. Właśnie dlatego warto go oddzielać od kodu.

Konsekwencja: zanim napiszesz program, upewnij się, że masz algorytm. Gdy kroki są jasne na papierze, zamiana ich na kod jest już głównie kwestią zapisu.

[sec-02-przepis-jako-algorytm] ## Przepis jako algorytm
Przepis kulinarny to [[algorytm|algorytm]] zapisany dla kucharza: ma dane wejściowe (składniki), uporządkowane kroki i wynik (gotowe danie). Różnica polega na tym, że człowiek wybaczy przepisowi niedokładność, a komputer nie.

Zestawmy oba zapisy:

| Przepis | Algorytm |
|---|---|
| składniki i ich ilości | dane wejściowe |
| kolejne kroki: „pokrój”, „wymieszaj” | jednoznaczne instrukcje |
| „piecz 40 minut w 180°C” | [[warunek-zakonczenia|warunek zakończenia]] |
| gotowe ciasto | wynik |

Warunek zakończenia to sprawdzalny test „czy już koniec?”. „Piecz 40 minut” albo „piecz, aż termometr pokaże 95°C w środku” da się zmierzyć. „Piecz, aż się zrumieni” już nie, bo każdy inaczej oceni rumieniec.

Tak samo jest z „dodaj szczyptę soli” czy „smaż chwilę”: kucharz zinterpretuje to po swojemu. W algorytmie musi stać coś takiego jak „Podziel sumę przez liczbę osób”, bez pola na domysły.

Ten sam przepis mogą wykonać różne osoby w różnych kuchniach i wyjdzie to samo danie. Tak samo algorytm da się wykonać w Pythonie, w arkuszu albo na kartce.

Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”. Jej przepis to [[lm-8|cztery kroki rozliczenia, które już znasz]]: składniki to wydatki i liczba osób, a „danie” to saldo każdego.

Konsekwencja: pisząc algorytm, wyobraź sobie przepis dla kogoś, kto nigdy nie gotował. Jeśli taka osoba wykona go bez pytań, kroki są dość dokładne.

[sec-02-kolejnosc-krokow-algorytmu] ## Kolejność kroków algorytmu
Kolejność ma znaczenie, bo prawie każdy krok korzysta z wyniku poprzedniego. Zamiana miejsc sprawia, że krok dostaje dane, których jeszcze nie ma, i [[algorytm|algorytm]] daje zły wynik albo wcale nie działa.

Weźmy cztery kroki rozliczenia we „Wspólnej Kasie”. Ala wydała 60 zł, Bartek 40 zł, Czarek 20 zł. Najpierw sumujemy: 120 zł. Potem dzielimy przez trzy osoby: udział wynosi 40 zł. Na końcu odejmujemy udział od wpłaty każdego.

Teraz zamieńmy kroki: odejmujemy udział, zanim go policzyliśmy.

```text
# poza kanonem
Dobrze:  suma 120 zł --> udział 40 zł --> Ala: 60 - 40 = +20 zł
Źle:     udział jeszcze nieznany (0 zł) --> Ala: 60 - 0 = +60 zł
```

Krok „odejmij udział” nie miał czego odjąć. Zależność między krokami to właśnie taka sytuacja: jeden krok potrzebuje wyniku innego, więc musi stać po nim.

Nie każda para kroków jest tak związana. Policzenie osób i zsumowanie wydatków są niezależne, więc możesz zrobić je w dowolnej kolejności. Oba muszą jednak być gotowe przed dzieleniem.

Konsekwencja: pisząc algorytm, przy każdym kroku zapytaj, skąd bierze dane. Jeśli z wyniku innego kroku, ten krok stoi za nim. Komputer wykona kroki dokładnie w zapisanej kolejności i niczego sam nie przestawi.

[sec-02-czym-jest-schemat-blokowy] ## Czym jest schemat blokowy
[[schemat-blokowy|Schemat blokowy]] to rysunek [[algorytm|algorytmu]]: każdy krok jest w ramce, a strzałki pokazują, w jakiej kolejności je wykonać. Działa jak mapa, po której palcem przejdziesz od początku do końca.

Używa kilku umownych kształtów. Owal oznacza początek albo koniec, prostokąt to zwykły krok, a romb to pytanie, po którym droga rozwidla się na „tak” i „nie”. Krok wykonujesz, gdy dojdziesz do niego strzałką, a nie dlatego, że stoi niżej na kartce.

Oto rozliczenie „Wspólnej Kasy” z trzema osobami, narysowane znakami tekstowymi:

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

Rysunek ma dwie zalety. Rozgałęzienia i powroty widać od razu, a w opisie słownym łatwo je przeoczyć. Poza tym pokazuje, gdzie algorytm się kończy, czyli sprawdzalny [[warunek-zakonczenia|warunek zakończenia]].

Konsekwencja: schemat pozwala sprawdzić algorytm na kartce, zanim powstanie [[kod|kod]]. Wrócimy do niego przy podziale problemu na części, a „Wspólna Kasa”, przykład, który będzie nam towarzyszył, dostanie z niego kod dopiero później.

[sec-02-podzial-problemu-na-czesci] ## Podział problemu na części
Duży problem dzielisz tak, by każda część miała własne dane wejściowe, jedno zadanie i wynik, który da się sprawdzić osobno. Zaczynasz od całego zadania, a potem pytasz: z jakich mniejszych kroków się składa?

Weźmy „rozlicz wyjazd”. To za dużo naraz, więc rozbijamy to na trzy części. Wracamy tu do [[schemat-blokowy|schematu blokowego]] z poprzedniej sekcji: kroki w jego ramkach to gotowe kandydatki na części.

```text
Rozlicz wyjazd
  |-- 1. Zsumuj wydatki          (wydatki -> suma)
  |-- 2. Policz udział osoby     (suma, liczba osób -> udział)
  `-- 3. Porównaj wpłatę z udziałem
                                 (wpłata, udział -> saldo)
```

Każda część ma jasne wejście i wynik. Część 3 potrzebuje wyniku części 2, a ta wyniku części 1, więc kolejność wynika z tych zależności, tak jak w sekcji o kolejności kroków.

Jeśli część nadal jest zbyt duża, dziel ją dalej, aż każdą da się opisać jednym zdaniem. Dobra część daje się też przetestować samodzielnie: znasz jej dane i wiesz, jaki wynik ma wyjść.

Konsekwencja: w programie takie części zamienimy w osobne [[funkcja|funkcje]], czyli nazwane fragmenty kodu do wielokrotnego użycia. Ich nazwy, np. `suma_wydatkow`, poznasz później, gdy zaczniemy pisać „Wspólną Kasę”, przykład, który będzie nam towarzyszył w kolejnych działach.

[sec-02-poprawny-algorytm] ## Poprawny algorytm
[[algorytm|Algorytm]] jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny z tym, czego od niego wymagamy. Nie wystarczy, że zadziałał raz na jednym przykładzie.

Najpierw trzeba więc ustalić, co znaczy „zgodny”. To [[specyfikacja-wyniku|specyfikacja wyniku]]: krótki opis, jaki wynik ma wyjść z jakich danych. Dla rozliczenia może brzmieć tak: suma wszystkich sald wynosi 0 zł, a nikomu nie znika ani nie przybywa grosza. Bez takiego opisu nie ma czego sprawdzać.

Potem sprawdzasz dwie rzeczy: czy algorytm zawsze dochodzi do [[warunek-zakonczenia|warunku zakończenia]] i czy wynik spełnia specyfikację. Ważne są zwłaszcza [[przypadek-brzegowy|przypadki brzegowe]], czyli dane na skraju dozwolonego zakresu: jedna osoba, brak wydatków, kwota, która nie dzieli się równo.

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

Dla 120 zł na czworo wszystko się zgadza. Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza. Dlatego w naszej liście kroków jest zdanie „Resztę groszy dopisz pierwszej osobie.”: bez niego algorytm byłby niepoprawny, choć pierwszy przykład by przeszedł.

Konsekwencja: poprawność sprawdzasz na wielu danych, w tym celowo niewygodnych. Do systematycznego sprawdzania wrócimy przy testowaniu programu.
````

## Odpowiedź

````json
{
  "items": [
    {
      "question_id": 7,
      "status": "covered",
      "section_ids": [
        "sec-02-czym-jest-algorytm"
      ],
      "explanation": "Definicja: skończony ciąg jednoznacznych kroków od danych do wyniku, odróżniony od kodu (słowa, kartka, kod), z przykładem rozliczenia."
    },
    {
      "question_id": 8,
      "status": "covered",
      "section_ids": [
        "sec-02-przepis-jako-algorytm"
      ],
      "explanation": "Tabela mapuje składniki, kroki, warunek zakończenia i wynik; różnica w precyzji pokazana na „szczypcie” i „aż się zrumieni” vs. sprawdzalny test."
    },
    {
      "question_id": 9,
      "status": "covered",
      "section_ids": [
        "sec-02-kolejnosc-krokow-algorytmu"
      ],
      "explanation": "Wyjaśnia zależność danych między krokami, pokazuje błędny wynik po zamianie, kroki niezależne można zamieniać, komputer nie przestawia sam."
    },
    {
      "question_id": 10,
      "status": "covered",
      "section_ids": [
        "sec-02-czym-jest-schemat-blokowy"
      ],
      "explanation": "Podano kształty (owal, prostokąt, romb), strzałki, przykład tekstowy i korzyść: widać rozgałęzienia, powroty i koniec przed kodem."
    },
    {
      "question_id": 11,
      "status": "covered",
      "section_ids": [
        "sec-02-podzial-problemu-na-czesci"
      ],
      "explanation": "Kryteria części (wejście, jedno zadanie, wynik do sprawdzenia), dalszy podział do opisu jednym zdaniem i kolejność z zależności, z przykładem."
    },
    {
      "question_id": 12,
      "status": "covered",
      "section_ids": [
        "sec-02-poprawny-algorytm"
      ],
      "explanation": "Poprawność dla wszystkich dozwolonych danych, specyfikacja wyniku, przypadki brzegowe i przykład 100 zł na troje z resztą groszy."
    }
  ],
  "promises": [
    {
      "reference_id": "ref-8",
      "status": "spełniona",
      "section_id": "sec-02-czym-jest-algorytm",
      "quote": "Na razie nie piszemy kodu: to celowo zwykły język.",
      "explanation": "Dział pisze algorytm zwykłym językiem i zapowiada zapis w Pythonie później."
    },
    {
      "reference_id": "ref-9",
      "status": "spełniona",
      "section_id": "sec-02-czym-jest-algorytm",
      "quote": "Ten sam algorytm można potem zapisać w Pythonie",
      "explanation": "Python pojawia się jako język zapisu; kod w Pythonie jest też w sekcji o poprawności."
    },
    {
      "reference_id": "ref-10",
      "status": "spełniona",
      "section_id": "sec-02-podzial-problemu-na-czesci",
      "quote": "poznasz później, gdy zaczniemy pisać „Wspólną Kasę”",
      "explanation": "Zapowiedź, że Python i budowa Wspólnej Kasy przyjdą później."
    },
    {
      "reference_id": "ref-16",
      "status": "spełniona",
      "section_id": "sec-02-czym-jest-algorytm",
      "quote": "Na razie nie piszemy kodu: to celowo zwykły język.",
      "explanation": "Kod odłożony na później, zgodnie z zapowiedzią."
    },
    {
      "reference_id": "ref-19",
      "status": "spełniona",
      "section_id": "sec-02-przepis-jako-algorytm",
      "quote": "Przykładem, który będzie nam towarzyszył, jest „Wspólna Kasa”.",
      "explanation": "Wspólna Kasa wraca w tym dziale jako przykład w wielu sekcjach."
    },
    {
      "reference_id": "ref-23",
      "status": "spełniona",
      "section_id": "sec-02-podzial-problemu-na-czesci",
      "quote": "Wracamy tu do [[schemat-blokowy|schematu blokowego]] z poprzedniej sekcji: kroki w jego ramkach to gotowe kandydatki na części.",
      "explanation": "Sekcja o podziale problemu wraca do schematu blokowego jako źródła części."
    },
    {
      "reference_id": "ref-24",
      "status": "spełniona",
      "section_id": "sec-02-czym-jest-schemat-blokowy",
      "quote": "„Wspólna Kasa”, przykład, który będzie nam towarzyszył",
      "explanation": "Wspólna Kasa jest użyta i zapowiedziana jako towarzysząca dalej."
    },
    {
      "reference_id": "ref-25",
      "status": "spełniona",
      "section_id": "sec-02-czym-jest-schemat-blokowy",
      "quote": "dostanie z niego kod dopiero później",
      "explanation": "Zapowiedź kodu Wspólnej Kasy w dalszych działach."
    },
    {
      "reference_id": "ref-30",
      "status": "spełniona",
      "section_id": "sec-02-podzial-problemu-na-czesci",
      "quote": "przykład, który będzie nam towarzyszył w kolejnych działach",
      "explanation": "Zapowiedź powrotu Wspólnej Kasy w kolejnych działach."
    }
  ]
}
````
