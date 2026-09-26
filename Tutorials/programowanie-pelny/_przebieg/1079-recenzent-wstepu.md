# Krok 1079 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 10 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 10: "Programowanie w praktyce". Pytania, na które odpowie:
- Jakie są przykłady programów używanych na co dzień?
- Czym różni się strona internetowa od aplikacji mobilnej?
- Jak od pomysłu dojść do działającego programu?
- Jakie umiejętności poza kodowaniem przydają się programiście?
- Od czego zacząć samodzielną naukę programowania?
- Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?

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
Masz już wszystkie klocki: dane, decyzje, pętle, funkcje, pliki i sprawdzanie błędów. Ten dział pokazuje, jak z nich korzystać poza ćwiczeniami: gdzie programy spotykasz na co dzień, jak od pomysłu dojść do działającego narzędzia i od czego zacząć dalszą naukę. Ocenimy też gotową Wspólną Kasę i pomysły na jej rozwój, a w warsztacie dopiszesz do niej własną funkcję, np. kto komu ile jest winien, i zapiszesz ją jako kolejny commit. Dzięki temu zobaczysz, jak automatyzować drobne zadania z własnej pracy.

DIAGRAM:
pomysł → plan kroków → kod → test → commit → następny pomysł
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "wyjaśnienie",
      "severity": "blokująca",
      "target": "„zapiszesz ją jako kolejny commit”",
      "detail": "Czytelnik spoza IT może nie znać słowa „commit”. We wstępie nie ma wyjaśnienia ani odwołania do działu, w którym je poznał. Dodaj krótkie odwołanie („zapiszesz ją w historii zmian, jako kolejny commit, jak w dziale X”) albo zastąp to opisem.",
      "source": "wstęp"
    },
    {
      "kind": "odwołanie",
      "severity": "blokująca",
      "target": "„gotową Wspólną Kasę”",
      "detail": "Wspólna Kasa pojawia się bez wprowadzenia. Czytelnik nie wie, że to projekt z poprzednich działów. Dodaj, że to program budowany w poprzednich działach (np. do rozliczania wspólnych wydatków), i wskaż, który dział.",
      "source": "wstęp"
    },
    {
      "kind": "diagram",
      "severity": "blokująca",
      "target": "diagram: pomysł → … → commit → następny pomysł",
      "detail": "Diagram jest pojedynczą linią i nie ma zamknięcia pętli. Ostatnia strzałka „następny pomysł” wisi w powietrzu, bo nie wraca do początku. Etykiety „plan kroków” i „commit” nie są wyjaśnione. Nie wiadomo, co się dzieje, gdy test nie przejdzie. Przerysuj jako cykl ze strzałką powrotną z „test” do „kod” („nie działa – popraw”) i z „następny pomysł” do „pomysł”. Dodaj jedno zdanie we wstępie wprowadzające diagram, np. „tak wygląda droga od pomysłu do działającego programu”.",
      "source": "diagram"
    },
    {
      "kind": "pokrycie",
      "severity": "sugestia",
      "target": "cały wstęp",
      "detail": "Wstęp mówi o automatyzacji, pomysłach i dalszej nauce, ale prawie nie zapowiada różnicy między stroną a aplikacją mobilną ani umiejętności poza kodowaniem. Wystarczy jedna fraza, np. „i jakie inne umiejętności się przydadzą”.",
      "source": "wstęp"
    },
    {
      "kind": "konkret",
      "severity": "sugestia",
      "target": "„kto komu ile jest winien”",
      "detail": "Przykład jest dobry, ale zdanie „Dzięki temu zobaczysz, jak automatyzować drobne zadania z własnej pracy” jest skokiem. Dodaj łącznik: taki sam tok pracy da się zastosować do własnych zadań, np. zestawień w arkuszu.",
      "source": "wstęp"
    }
  ]
}
````
