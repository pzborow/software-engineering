# Krok 0447 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 5 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 05: "Operacje i decyzje". Pytania, na które odpowie:
- Jakie podstawowe działania matematyczne może wykonać program?
- Jak program łączy ze sobą teksty?
- Jak program porównuje dwie wartości?
- Czym jest instrukcja warunkowa „jeśli… to…”?
- Do czego służy część „w przeciwnym razie”?
- Do czego służą operatory „i” oraz „lub”?

Autor pisał według zasad: Napisz 3-6 zdań, najwyżej 150 słów: po co jest ten dział (jaki problem czytelnika rozwiązuje), co czytelnik będzie umiał po jego przeczytaniu i jak dział łączy się z poprzednimi. Nie wyliczaj sekcji, spis sekcji dołączamy pod wstępem. Definicje i przykłady należą do sekcji, wstęp tylko zapowiada. Możesz dodać mały diagram tekstowy.
Nie żądaj niczego, czego te zasady zabraniają (dłuższego tekstu, definicji, przykładów, terminów w pierwszym dziale).

Sprawdź wstęp i diagram oczami tego czytelnika:
- Czy wstęp mówi, po co jest ten dział, co czytelnik będzie po nim umiał i jak dział łączy się z poprzednimi?
- Czy diagram jest zrozumiały bez dodatkowych wyjaśnień: każda strzałka i etykieta ma jasne znaczenie, nic nie wisi
  w powietrzu, kierunek przepływu jest oczywisty? Czy zgadza się z tym, czego dotyczy dział, i nie wprowadza w błąd?
- Diagram, który nic nie wnosi albo myli, zgłoś do usunięcia albo przerysowania.
Problemy zgłoś jako potrzeby (kind: diagram, konkret, wyjaśnienie albo tempo; target: fragment; detail: jak poprawić).

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

WSTĘP:
Dotąd program tylko przechowywał dane w zmiennych; w tym dziale nauczy się z nimi coś robić. Po jego przeczytaniu policzysz wynik z liczb, sklejisz z tekstów zdanie, porównasz dwie wartości i sprawisz, że program wybierze jedną z dróg, zamiast zawsze robić to samo. Wykorzystasz zmienne i typy z poprzedniego działu oraz rozgałęzienia ze schematów blokowych z działu 2. W przykładzie „Wspólna Kasa” program policzy koszt na osobę i zdecyduje, czy ktoś jest winien pieniądze, czy ma dostać zwrot, a w warsztacie oceni, czy wydatek jest duży.

DIAGRAM:
dane (zmienne) → działania → porównanie → decyzja
 kwota, osoby     kwota / osoby   > ?      if / else
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "diagram",
      "severity": "blokująca",
      "target": "diagram: „> ?” pod „porównanie” i „if / else” pod „decyzja”",
      "detail": "Diagram używa skrótów, których czytelnik jeszcze nie zna: „if / else” (angielskie słowa, w tekście wstępu w ogóle nie padają) i „> ?”. Zastąp je opisami po polsku, spójnymi z pytaniami działu, np. „jeśli… to… / w przeciwnym razie”, a porównanie zapisz zrozumiale, np. „czy kwota jest większa niż…?”. Ukośnik w „kwota / osoby” może się kojarzyć z „albo”; lepiej użyć „kwota ÷ osoby” lub „kwota podzielona na osoby”."
    },
    {
      "kind": "diagram",
      "severity": "blokująca",
      "target": "diagram: układ etykiet pod strzałkami",
      "detail": "Przykładowe wartości („kwota, osoby”, „kwota / osoby”, „> ?”, „if / else”) są ustawione w drugiej linii bez jasnego przypisania do etapów; w terminalu spacje łatwo się rozjadą i nie widać, która etykieta należy do którego pola. Narysuj pionowo albo w pudełkach, tak by każdy przykład był bezpośrednio pod swoim etapem. Dodaj też, co wynika z porównania (dwie ścieżki: tak/nie), bo dziś „decyzja” wisi bez wyniku."
    },
    {
      "kind": "konkret",
      "severity": "sugestia",
      "target": "„zdecyduje, czy ktoś jest winien pieniądze, czy ma dostać zwrot”",
      "detail": "Przykład „Wspólna Kasa” pojawia się bez zarysu sytuacji (kto komu płaci). Jedno krótkie zdanie o tym, czym jest ta kasa (np. wspólny wyjazd, wydatki dzielone na osoby), pomoże czytelnikowi wyobrazić sobie scenariusz. Uwaga: „zwrot” i „jest winien” to dwa wyniki, a w diagramie jest jedno porównanie „>” – upewnij się, że zgadza się to z przykładem."
    },
    {
      "kind": "wyjaśnienie",
      "severity": "sugestia",
      "target": "„rozgałęzienia ze schematów blokowych z działu 2”",
      "detail": "Wstęp nie mówi, jak to nawiązanie się przyda (np. „decyzja w programie to ten sam romb ze schematu, tylko zapisany kodem”). Jedno takie zdanie wzmocni związek z poprzednimi działami."
    },
    {
      "kind": "tempo",
      "severity": "sugestia",
      "target": "ostatnie zdanie („w warsztacie oceni, czy wydatek jest duży”)",
      "detail": "Zdanie jest długie, a pojęcie „warsztat” nie zostało wprowadzone; zapis „oceni, czy wydatek jest duży” nie mówi, względem czego. Rozważ skrócenie lub doprecyzowanie („w warsztacie sam napiszesz program sprawdzający, czy wydatek przekracza ustalony próg”)."
    }
  ]
}
````
