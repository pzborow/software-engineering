# Krok 0085 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 2 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 02: "Algorytmy i myślenie krokowe". Pytania, na które odpowie:
- Czym jest algorytm?
- Jak przepis kulinarny przypomina algorytm?
- Dlaczego kolejność kroków w algorytmie ma znaczenie?
- Czym jest schemat blokowy?
- Jak podzielić duży problem na mniejsze części?
- Co to znaczy, że algorytm jest poprawny?

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
W poprzednim dziale zobaczyłeś, że komputer wykonuje dokładnie to, co zapisano, więc zanim cokolwiek napiszesz, musisz wiedzieć, jakie kroki mają prowadzić do wyniku. Ten dział uczy, jak takie kroki wymyślić i zapisać: jako algorytm, jako schemat blokowy i jako zestaw mniejszych części. Po jego przeczytaniu rozpiszesz prosty problem krok po kroku, dopilnujesz kolejności działań i sprawdzisz, czy wynik jest poprawny. Posłuży nam do tego rozliczenie wspólnych wydatków „Wspólna Kasa”, które podzielimy na części, a te później staną się funkcjami.

DIAGRAM:
problem → algorytm (kroki) → schemat blokowy → mniejsze części → sprawdzenie poprawności
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "język",
      "severity": "sugestia",
      "target": "a te później staną się funkcjami",
      "detail": "Czytelnik spoza IT nie zna słowa „funkcje”, a wstęp go nie wyjaśnia. Lepiej napisać np. „a te później zamienimy w osobne fragmenty programu”. Można też po prostu skończyć na „podzielimy na części”.",
      "source": "wstęp"
    },
    {
      "kind": "diagram",
      "severity": "sugestia",
      "target": "strzałki w diagramie",
      "detail": "Strzałki nie mają opisu, a wygląda to na jednokierunkowy proces, w którym poprawność sprawdza się dopiero na końcu. Dodaj strzałkę powrotną od „sprawdzenia poprawności” do „kroków” z etykietą, np. „jeśli wynik zły – popraw kroki”. Wtedy nie powstanie błędne wrażenie, że wystarczy przejść listę raz. Możesz też dopisać pod diagramem jedno zdanie, że strzałka oznacza „następny etap pracy”.",
      "source": "diagram"
    },
    {
      "kind": "diagram",
      "severity": "sugestia",
      "target": "„algorytm (kroki)”",
      "detail": "Nawias jest niejasny: czy „kroki” to inna nazwa algorytmu, czy jego część? W diagramie nie widać też kolejności kroków, choć wstęp ją obiecuje. Zapisz np. „algorytm (kroki w kolejności)”.",
      "source": "diagram"
    }
  ]
}
````
