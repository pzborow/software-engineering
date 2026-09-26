# Krok 0576 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 6 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 06: "Powtarzanie i kolekcje". Pytania, na które odpowie:
- Czym jest pętla?
- Kiedy warto użyć pętli zamiast pisać to samo wiele razy?
- Czym jest pętla nieskończona i dlaczego jest problemem?
- Czym jest lista danych?
- Jak odczytać konkretny element listy?
- Jak przejść przez wszystkie elementy listy?

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
Dotąd każdą wartość trzymałeś w osobnej zmiennej i każdą czynność zapisywałeś osobno, a przy dziesięciu wydatkach to szybko zamienia się w żmudne kopiowanie. W tym dziale nauczysz się zbierać dane na liście i powtarzać instrukcje w pętli, więc jednym zapisem obsłużysz i trzy, i trzysta pozycji. Wykorzystasz zmienne z działu 04 oraz warunki z działu 05, a we „Wspólnej Kasie” lista wydatków i pętla `for` zsumują kwoty i policzą saldo każdej osoby. Zobaczysz też, jak wygląda pętla, która się nie kończy, i jak ją zatrzymać.

DIAGRAM:
wydatki: [40, 25, 60]
            |
   for każdy wydatek:
            |
   suma = suma + wydatek  --> 125
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "diagram",
      "detail": "Diagram jest niejasny dla laika: nie widać, że pętla wykonuje się wielokrotnie (jeden przebieg na każdy wydatek), a wynik 125 pojawia się dopiero po wszystkich krokach. Strzałka '--> 125' przy jednej linii sugeruje, że wynik daje pojedyncze wykonanie. Zmienna 'suma' nie ma wartości początkowej (0). Przerysuj: pokaż start suma = 0, kolejne przebiegi (40 -> suma 40, 25 -> suma 65, 60 -> suma 125) i strzałkę powrotną z 'suma = suma + wydatek' do 'for każdy wydatek', albo diagram usuń.",
      "target": "diagram",
      "severity": "blokująca"
    },
    {
      "kind": "wyjaśnienie",
      "detail": "Diagram używa zapisów (`for`, nawiasy kwadratowe, 'suma = suma + wydatek') bez wyjaśnienia; czytelnik nie wie, że '=' to przypisanie, a nie równość. Wstęp nie zapowiada, że diagram to ilustracja sumowania. Dodaj jedno zdanie wprowadzające pod diagramem lub podpis, np. 'Pętla bierze po kolei każdy wydatek z listy i dodaje go do sumy'.",
      "target": "diagram i jego związek ze wstępem",
      "severity": "sugestia"
    },
    {
      "kind": "konkret",
      "detail": "'Wspólna Kasa' pojawia się bez wprowadzenia; jeśli to projekt przewijający się przez tutorial, wystarczy krótkie dopowiedzenie (np. 'nasza aplikacja do rozliczania wydatków'), by czytelnik nie zastanawiał się, co to.",
      "target": "„Wspólnej Kasie”",
      "severity": "sugestia"
    }
  ]
}
````
