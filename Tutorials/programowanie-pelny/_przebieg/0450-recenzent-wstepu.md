# Krok 0450 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 5 · pytanie: — · próba: 2

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
Dotąd program tylko przechowywał dane w zmiennych; w tym dziale nauczy się z nimi coś robić. Po jego przeczytaniu policzysz wynik z liczb, sklejisz z tekstów zdanie, porównasz dwie wartości i sprawisz, że program wybierze jedną z dróg, zamiast zawsze robić to samo. Wykorzystasz zmienne i typy z poprzedniego działu oraz rozgałęzienia ze schematów blokowych z działu 2. W przykładzie „Wspólna Kasa” program policzy udział jednej osoby i zdecyduje, czy ktoś jest winien pieniądze, czy ma dostać zwrot, a w warsztacie oceni, czy wydatek jest duży.

DIAGRAM:
1. Dane (zmienne):        kwota, liczba osób
          ↓
2. Działanie:            kwota podzielona przez liczbę osób
          ↓
3. Porównanie:           czy koszt jest większy niż limit?
          ↓
4. Decyzja:              jeśli tak → jedna droga
                         w przeciwnym razie → druga droga

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [diagram] diagram: „> ?” pod „porównanie” i „if / else” pod „decyzja”: Diagram używa skrótów, których czytelnik jeszcze nie zna: „if / else” (angielskie słowa, w tekście wstępu w ogóle nie padają) i „> ?”. Zastąp je opisami po polsku, spójnymi z pytaniami działu, np. „jeśli… to… / w przeciwnym razie”, a porównanie zapisz zrozumiale, np. „czy kwota jest większa niż…?”. Ukośnik w „kwota / osoby” może się kojarzyć z „albo”; lepiej użyć „kwota ÷ osoby” lub „kwota podzielona na osoby”.
- [diagram] diagram: układ etykiet pod strzałkami: Przykładowe wartości („kwota, osoby”, „kwota / osoby”, „> ?”, „if / else”) są ustawione w drugiej linii bez jasnego przypisania do etapów; w terminalu spacje łatwo się rozjadą i nie widać, która etykieta należy do którego pola. Narysuj pionowo albo w pudełkach, tak by każdy przykład był bezpośrednio pod swoim etapem. Dodaj też, co wynika z porównania (dwie ścieżki: tak/nie), bo dziś „decyzja” wisi bez wyniku.
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
