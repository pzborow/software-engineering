# Krok 0191 · weryfikator_odwołań

Węzeł: `review` · dział: 3 · pytanie: 13 · próba: 1

## Prompt

````text
Jesteś weryfikatorem odwołań w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.

Znajdź w nowej sekcji WSZYSTKIE odwołania, także te, których autor nie zadeklarował:
- nawiązania do czegoś wcześniejszego („jak widzieliśmy”, „ten błąd z napiwkiem”, „wspomniany wcześniej”),
- obietnice czegoś późniejszego („powiemy osobno”, „wrócimy do tego”, „w dziale o pętlach”).
Zwykłe użycie pojęcia (np. „programu”, „listy”) NIE jest odwołaniem; nawiązanie odsyła do konkretnego miejsca albo zdarzenia,
a obietnica zapowiada, że temat wróci.

Dla każdego podaj w references: direction, phrase (dokładny fragment zdania z sekcji), about, target i quote:
- wstecz: target = id punktu zaczepienia (lm-N), a gdy żaden nie pasuje: id sekcji z listy niżej albo "glosariusz:<id>";
  quote puste (cytat punktu zaczepienia jest znany).
- w przód: target = numer późniejszego pytania, jeśli któreś wyraźnie to omówi, inaczej puste; quote puste.
- poza tutorialem: target i quote puste.
Wolno nawiązywać tylko do punktów i sekcji z list (ten i poprzedni dział) albo do haseł glosariusza. Nawiązanie, którego cel
nie istnieje albo mówi co innego, zgłoś jako potrzebę kind="odwołanie", severity="blokująca", detail = jak poprawić
(wyjaśnić na miejscu albo usunąć). Obietnicę, która odwołuje się do „pytań”, numerów albo list wewnętrznych,
zgłoś jako blokującą: czytelnik ich nie zna, zdanie ma mówić o temacie.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

ZADEKLAROWANE PRZEZ AUTORA:
- w przód: „jak to działa, pokażemy przy uruchamianiu programu” → 15 (uruchamianie programu i program czytający kod)
- w przód: „przykład, który będzie nam towarzyszył” → - (Wspólna Kasa wraca w kolejnych działach)
- wstecz: „Ten sam [[algorytm|algorytm]], który wcześniej opisywaliśmy słowami” → sec-02-czym-jest-algorytm (algorytm opisany w dziale o algorytmach)

HASŁA GLOSARIUSZA (id: termin):
- program-komputerowy: program komputerowy
- instrukcja: instrukcja
- programista: programista
- programowanie: programowanie
- jezyk-programowania: język programowania
- kod: kod
- skladnia: składnia
- aplikacja: aplikacja
- algorytm: algorytm
- warunek-zakonczenia: warunek zakończenia
- schemat-blokowy: schemat blokowy
- funkcja: funkcja
- specyfikacja-wyniku: specyfikacja wyniku
- przypadek-brzegowy: przypadek brzegowy

PÓŹNIEJSZE PYTANIA:
- 14. Do czego służy edytor kodu?
- 15. Co to znaczy uruchomić program?
- 16. Czym jest kompilator lub interpreter?
- 17. Co to jest błąd w programie?
- 18. Do czego służą komentarze w kodzie?
- 19. Czym jest dana w programie?
- 20. Czym jest zmienna?
- 21. Jak można porównać zmienną do pudełka z etykietą?
- 22. Czym różni się liczba od tekstu w programie?
- 23. Czym jest typ danych?
- 24. Co to jest wartość logiczna prawda/fałsz?
- 25. Do czego służy przypisanie wartości do zmiennej?
- 26. Jakie podstawowe działania matematyczne może wykonać program?
- 27. Jak program łączy ze sobą teksty?
- 28. Jak program porównuje dwie wartości?
- 29. Czym jest instrukcja warunkowa „jeśli… to…”?
- 30. Do czego służy część „w przeciwnym razie”?
- 31. Do czego służą operatory „i” oraz „lub”?
- 32. Czym jest pętla?
- 33. Kiedy warto użyć pętli zamiast pisać to samo wiele razy?
- 34. Czym jest pętla nieskończona i dlaczego jest problemem?
- 35. Czym jest lista danych?
- 36. Jak odczytać konkretny element listy?
- 37. Jak przejść przez wszystkie elementy listy?
- 38. Czym jest funkcja?
- 39. Po co dzielić program na funkcje?
- 40. Czym są argumenty funkcji?
- 41. Co to znaczy, że funkcja zwraca wynik?
- 42. Dlaczego nazwy zmiennych i funkcji powinny być czytelne?
- 43. Czym jest ponowne użycie kodu?
- 44. Czym są dane wejściowe programu?
- 45. Czym są dane wyjściowe programu?
- 46. Jak program może zapytać użytkownika o informację?
- 47. Czym jest plik i jak program może z niego korzystać?
- 48. Czym jest interfejs użytkownika?
- 49. Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?
- 50. Czym różni się błąd składni od błędu logicznego?
- 51. Jak przeczytać komunikat o błędzie?
- 52. Czym jest testowanie programu?
- 53. Czym jest debugowanie?
- 54. Dlaczego warto zapisywać kolejne wersje kodu?
- 55. Jak szukać rozwiązań problemów programistycznych w internecie?
- 56. Jakie są przykłady programów używanych na co dzień?
- 57. Czym różni się strona internetowa od aplikacji mobilnej?
- 58. Jak od pomysłu dojść do działającego programu?
- 59. Jakie umiejętności poza kodowaniem przydają się programiście?
- 60. Od czego zacząć samodzielną naukę programowania?
- 61. Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

PUNKTY ZACZEPIENIA (ten i poprzedni dział):
- [lm-8] algorytm rozliczenia w czterech krokach (dział 02): „Podziel sumę przez liczbę osób: to udział jednej osoby.”
- [lm-9] przepis dla kogoś, kto nie gotował (dział 02): „wyobraź sobie przepis dla kogoś, kto nigdy nie gotował”
- [lm-10] mierzalny warunek pieczenia (dział 02): „„Piecz 40 minut” albo „piecz, aż termometr pokaże 95°C w środku” da się zmierzyć.”
- [lm-11] odejmowanie przed policzeniem udziału (dział 02): „Źle:     udział jeszcze nieznany (0 zł) --> Ala: 60 - 0 = +60 zł”
- [lm-12] schemat rozliczenia z rombem (dział 02): „< Wpłaciła więcej niż udział? > --tak--> [ Ma zwrot ] --+”
- [lm-13] drzewo podziału rozliczenia (dział 02): „Rozlicz wyjazd”
- [lm-14] brakujący grosz (dział 02): „Dla 100 zł na troje po zsumowaniu udziałów brakuje grosza.”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-02-czym-jest-algorytm] Czym jest algorytm (dział 02): Algorytm to skończony ciąg jednoznacznych kroków od danych do wyniku, niezależny od tego, w jakim języku zostanie zapisany.
- [sec-02-przepis-jako-algorytm] Przepis jako algorytm (dział 02): Przepis to algorytm dla człowieka: składniki, kroki i wynik, tylko że algorytm musi być zapisany bez pola na domysły, ze sprawdzalnym warunkiem końca.
- [sec-02-kolejnosc-krokow-algorytmu] Kolejność kroków algorytmu (dział 02): Krok, który potrzebuje wyniku innego kroku, musi stać po nim, a komputer nigdy nie poprawi kolejności za Ciebie.
- [sec-02-czym-jest-schemat-blokowy] Czym jest schemat blokowy (dział 02): Schemat blokowy rysuje algorytm jako ramki połączone strzałkami, dzięki czemu rozgałęzienia, powroty i koniec widać, zanim powstanie kod.
- [sec-02-podzial-problemu-na-czesci] Podział problemu na części (dział 02): Dziel problem na części z jasnym wejściem i wynikiem, aż każdą da się opisać jednym zdaniem i sprawdzić osobno.
- [sec-02-poprawny-algorytm] Poprawny algorytm (dział 02): Algorytm jest poprawny, gdy dla każdych dozwolonych danych kończy pracę i daje wynik zgodny ze specyfikacją, także w przypadkach brzegowych.

NOWA SEKCJA "Czym jest kod źródłowy":
[[kod-zrodlowy|Kod źródłowy]] to tekst programu zapisany w [[jezyk-programowania|języku programowania]], który czyta i pisze człowiek. To „źródło”, z którego komputer dopiero dostaje coś do wykonania.

Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to [[instrukcja|instrukcja]] zapisana według ścisłych reguł [[skladnia|składni]]. Ten sam [[algorytm|algorytm]], który wcześniej opisywaliśmy słowami i schematem, tu dostaje zapis, którego nie da się zrozumieć na dwa sposoby.

Kod źródłowy zapisujemy w pliku o rozszerzeniu zależnym od języka. Pliki Pythona kończą się na `.py`. Taki plik będzie miał nasz przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Zaczyna się od pliku `rozlicz.py`:

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

```text
Wspólna Kasa
100.0
```

Plik sam niczego nie robi. Dopiero osobny program czyta go i wykonuje linia po linii, a jak to działa, pokażemy przy uruchamianiu programu.

Konsekwencja: kod źródłowy możesz otworzyć, przeczytać i poprawić w każdym edytorze tekstu. Dlatego to on jest tym, co programista naprawdę tworzy i zmienia.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "wstecz",
      "phrase": "Ten sam algorytm, który wcześniej opisywaliśmy słowami i schematem",
      "about": "algorytm rozliczenia opisany wcześniej słowami i schematem blokowym",
      "target": "lm-8",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "jak to działa, pokażemy przy uruchamianiu programu",
      "about": "czytanie i wykonywanie pliku z kodem przez osobny program",
      "target": "15",
      "quote": ""
    },
    {
      "direction": "w przód",
      "phrase": "nasz przykład, który będzie nam towarzyszył",
      "about": "Wspólna Kasa jako przykład wracający w kolejnych działach",
      "target": "",
      "quote": ""
    }
  ],
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "Kod w przykładzie liczy tylko 300 / 3, a nie cały algorytm rozliczenia z czterech kroków, więc „ten sam algorytm” trochę przesadza. Lepiej napisać, że to pierwszy krok algorytmu (podział sumy przez liczbę osób) zapisany w Pythonie.",
      "kind_": "",
      "severity": "sugestia",
      "target": "Ten sam algorytm, który wcześniej opisywaliśmy"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Czytelnik spoza IT nie wie, co robi print ani skąd wynik 100.0 (kropka, „.0”). Jedno zdanie pod kodem by to wyjaśniło: print wyświetla tekst lub wynik na ekranie, a 300 / 3 to dzielenie.",
      "severity": "sugestia",
      "target": "print(300 / 3)"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "„Rozszerzenie pliku” (.py) nie jest wyjaśnione. Wystarczy dopisać, że to końcówka nazwy po kropce, po której widać rodzaj pliku.",
      "severity": "sugestia",
      "target": "rozszerzeniu zależnym od języka"
    }
  ]
}
````
