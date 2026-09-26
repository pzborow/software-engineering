# Krok 0185 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 3 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 03: "Kod i jego uruchamianie". Pytania, na które odpowie:
- Czym jest kod źródłowy?
- Do czego służy edytor kodu?
- Co to znaczy uruchomić program?
- Czym jest kompilator lub interpreter?
- Co to jest błąd w programie?
- Do czego służą komentarze w kodzie?

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
Do tej pory układałeś algorytmy na papierze i w głowie, a teraz zapiszesz pierwszy prawdziwy kod i sprawdzisz, że komputer go wykona. Po tym dziale będziesz wiedzieć, czym jest kod źródłowy, do czego służy edytor, jak uruchomić program i co robi interpreter. Nauczysz się też rozpoznawać błąd i opisywać kod komentarzami. Zaczniemy plik kasa.py dla „Wspólnej Kasy” i celowo go zepsujemy, żeby zobaczyć pierwszy komunikat o błędzie.

DIAGRAM:
algorytm (dział 02) → kod w pliku → interpreter → wynik lub błąd
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "severity": "sugestia",
      "target": "„Wspólnej Kasy” i plik kasa.py",
      "detail": "Czytelnik może nie pamiętać, czym jest „Wspólna Kasa” z poprzednich działów. Warto dodać pół zdania przypominającego, np. że to przykład, który rozwijamy od początku tutoriala. Nazwa pliku kasa.py z rozszerzeniem .py jest niewyjaśniona, ale to zapowiedź, więc nie blokuje.",
      "source": "wstęp"
    },
    {
      "kind": "diagram",
      "severity": "sugestia",
      "target": "diagram: „kod w pliku → interpreter”",
      "detail": "Diagram jest zrozumiały i zgodny z tematem działu. Strzałki oznaczają kolejne etapy, a kierunek jest oczywisty. Można go ulepszyć przez etykiety przy strzałkach, np. „zapisujesz w edytorze” i „uruchamiasz”. Wtedy widać, że edytor też jest w tym procesie. Obecnie edytor, o którym mówi wstęp, na diagramie nie występuje.",
      "source": "diagram"
    },
    {
      "kind": "spójność",
      "severity": "sugestia",
      "target": "„Po tym dziale będziesz wiedzieć … Nauczysz się też …”",
      "detail": "Dwa zdania z zapowiedzią umiejętności brzmią jak wyliczenie. Można je połączyć w jedno i zapowiedzieć działanie zamiast wiedzy, np. „napiszesz, uruchomisz i naprawisz krótki program”. To tylko poprawa stylu.",
      "source": "wstęp"
    }
  ]
}
````
