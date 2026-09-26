# Krok 0049 · weryfikator_odwołań

Węzeł: `review` · dział: 1 · pytanie: 4 · próba: 1

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
- w przód: „Pythonem zajmiemy się osobno” → - (Python jako język tutorialu, omówiony później)

HASŁA GLOSARIUSZA (id: termin):
- program-komputerowy: program komputerowy
- instrukcja: instrukcja
- programista: programista
- programowanie: programowanie
- jezyk-programowania: język programowania
- kod: kod

PÓŹNIEJSZE PYTANIA:
- 5. Dlaczego komputer potrzebuje precyzyjnych instrukcji?
- 6. Czym różni się program od aplikacji?
- 7. Czym jest algorytm?
- 8. Jak przepis kulinarny przypomina algorytm?
- 9. Dlaczego kolejność kroków w algorytmie ma znaczenie?
- 10. Czym jest schemat blokowy?
- 11. Jak podzielić duży problem na mniejsze części?
- 12. Co to znaczy, że algorytm jest poprawny?
- 13. Czym jest kod źródłowy?
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
- [lm-1] schemat programu (dział 01): „dane na wejściu  -->  program (instrukcje)  -->  wynik na wyjściu”
- [lm-2] czworo znajomych na wyjeździe (dział 01): „Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg.”
- [lm-3] pętla poprawek (dział 01): „Uruchamiasz program, patrzysz na wynik, znajdujesz pomyłkę i poprawiasz.”
- [lm-4] ścieżka od potrzeby do poprawek (dział 01): „potrzeba --> ustalenie, co program ma robić --> kroki --> kod --> sprawdzanie --> poprawki”

SEKCJE Z TEGO I POPRZEDNIEGO DZIAŁU (tytuł: wniosek):
- [sec-01-czym-jest-program-komputerowy] Czym jest program komputerowy (dział 01): Program to ciąg instrukcji, które komputer wykonuje po kolei, aby z danych wejściowych uzyskać wynik.
- [sec-01-czym-jest-programowanie] Czym jest programowanie (dział 01): Programowanie to zamiana problemu na dokładne kroki dla komputera oraz sprawdzanie i poprawianie ich, aż wynik będzie poprawny.
- [sec-01-kim-jest-programista] Kim jest programista (dział 01): Programista zamienia potrzebę na działający program, a pisanie kodu to tylko jeden z etapów tej pracy.

NOWA SEKCJA "Czym jest język programowania":
[[jezyk-programowania|Język programowania]] to ściśle określony sposób zapisywania [[instrukcja|instrukcji]], który potrafi zrozumieć komputer. Ma własne słowa i reguły zapisu, ale jest o wiele prostszy i bardziej rygorystyczny niż język polski.

Komputer nie wyciąga wniosków z kontekstu. Zdanie „podziel rachunek po równo” człowiek zrozumie od razu, komputer nie. Język programowania wymusza zapis, który ma jedno znaczenie. Zbiór jego reguł nazywamy [[skladnia|składnią]]: mówi ona, jak wolno układać słowa i znaki, żeby powstało poprawne polecenie.

Oto jedna instrukcja w Pythonie, języku, którego użyjemy w tym tutorialu:

```python
print("Cześć, Wspólna Kasa!")
```

```text
Cześć, Wspólna Kasa!
```

Słowo `print` znaczy „wypisz”, a tekst w cudzysłowie to to, co ma się pojawić na ekranie. Gdybyś pominął jeden cudzysłów, komputer odmówiłby wykonania polecenia, bo zapis łamie reguły.

Języków jest bardzo wiele, a każdy ma inną składnię i inne zastosowania. Różnią się zapisem, ale robią to samo: pozwalają opisać kroki, które komputer wykona. Kto pozna zasady jednego, łatwiej nauczy się następnych.

Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”.
````

## Odpowiedź

````json
{
  "ok": true,
  "references": [
    {
      "direction": "w przód",
      "phrase": "języku, którego użyjemy w tym tutorialu",
      "about": "Python jako język tutorialu"
    },
    {
      "direction": "w przód",
      "phrase": "Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”",
      "about": "Python i budowa programu „Wspólna Kasa” omówione później",
      "target": ""
    }
  ],
  "needs": [
    {
      "kind": "wyjaśnienie",
      "detail": "„Wspólna Kasa” pojawia się bez wyjaśnienia (w przykładzie i w ostatnim zdaniu). Warto jednym zdaniem przypomnieć, że to program do rozliczania wydatków znajomych z wyjazdu, żeby czytelnik wiedział, co to jest.",
      "target": "Wspólna Kasa",
      "severity": "sugestia"
    }
  ]
}
````
