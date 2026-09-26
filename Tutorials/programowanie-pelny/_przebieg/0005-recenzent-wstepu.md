# Krok 0005 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 1 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 01: "Czym jest programowanie". Pytania, na które odpowie:
- Czym jest program komputerowy?
- Czym jest programowanie?
- Kim jest programista i czym się zajmuje?
- Czym jest język programowania?
- Dlaczego komputer potrzebuje precyzyjnych instrukcji?
- Czym różni się program od aplikacji?

Autor pisał według zasad: To pierwszy akapit całego tutorialu: 3-5 zdań, najwyżej 120 słów. Opisz, czym jest Programowanie od podstaw i jaki problem rozwiązuje, a w ostatnim zdaniu powiedz, co czytelnik będzie umiał po tym dziale. Używaj WYŁĄCZNIE ogólnych pojęć, które czytelnik zna; żadnych terminów specjalistycznych tej dziedziny (poza jej nazwą). Nie dodawaj new_terms. Nie wyliczaj sekcji, spis sekcji dołączamy pod wstępem. Definicje i przykłady należą do sekcji, wstęp tylko zapowiada.
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
Programowanie od podstaw to kurs dla osób, które codziennie korzystają z komputera, ale nigdy nie zastanawiały się, skąd bierze się to, co robi on na ekranie. Rozwiązuje prosty problem: bez zrozumienia, jak powstają programy, komputer pozostaje tajemniczą skrzynką, której można tylko ufać albo się bać. Zaczniemy od najważniejszego pytania, czyli czym właściwie jest programowanie i dlaczego wymaga tak dużej dokładności. Po tym dziale będziesz umieć własnymi słowami wyjaśnić, czym jest program, czym zajmuje się programista i dlaczego komputer działa tylko według precyzyjnych instrukcji.

DIAGRAM:
(brak)
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "tempo",
      "severity": "sugestia",
      "target": "Rozwiązuje prosty problem: bez zrozumienia... ufać albo się bać",
      "detail": "Można złagodzić metaforę „tajemniczej skrzynki” i dodać, że kurs prowadzi krok po kroku od zera. To tylko drobne ulepszenie, wstęp jest zrozumiały i mieści się w limitach."
    }
  ]
}
````
