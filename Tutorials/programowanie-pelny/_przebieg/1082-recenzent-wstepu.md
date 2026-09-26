# Krok 1082 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 10 · pytanie: — · próba: 2

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
Znasz już wszystkie klocki, ale wciąż możesz nie wiedzieć, jak użyć ich poza ćwiczeniami. Ten dział pokazuje, gdzie programy spotykasz na co dzień i jak od pomysłu dojść do działającego narzędzia, a Ty dowiesz się, od czego zacząć dalszą naukę i jak zautomatyzować drobne zadania z własnej pracy. Ocenimy Wspólną Kasę, czyli program do rozliczania wspólnych wydatków, który budowałeś w poprzednich działach, i pomysły na jej rozwój. W warsztacie dopiszesz do niej własną funkcję, np. kto komu ile jest winien, i zapiszesz ją w historii zmian jako kolejny commit, tak jak w dziale 9. Tak wygląda droga od pomysłu do działającego programu.

DIAGRAM:
pomysł → plan kroków → kod → test → commit
  ↑                      ↑       │
  │                      └───────┘ nie działa – popraw
  └──────── następny pomysł ──────┘

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [wyjaśnienie] „zapiszesz ją jako kolejny commit”: Czytelnik spoza IT może nie znać słowa „commit”. We wstępie nie ma wyjaśnienia ani odwołania do działu, w którym je poznał. Dodaj krótkie odwołanie („zapiszesz ją w historii zmian, jako kolejny commit, jak w dziale X”) albo zastąp to opisem.
- [odwołanie] „gotową Wspólną Kasę”: Wspólna Kasa pojawia się bez wprowadzenia. Czytelnik nie wie, że to projekt z poprzednich działów. Dodaj, że to program budowany w poprzednich działach (np. do rozliczania wspólnych wydatków), i wskaż, który dział.
- [diagram] diagram: pomysł → … → commit → następny pomysł: Diagram jest pojedynczą linią i nie ma zamknięcia pętli. Ostatnia strzałka „następny pomysł” wisi w powietrzu, bo nie wraca do początku. Etykiety „plan kroków” i „commit” nie są wyjaśnione. Nie wiadomo, co się dzieje, gdy test nie przejdzie. Przerysuj jako cykl ze strzałką powrotną z „test” do „kod” („nie działa – popraw”) i z „następny pomysł” do „pomysł”. Dodaj jedno zdanie we wstępie wprowadzające diagram, np. „tak wygląda droga od pomysłu do działającego programu”.
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "diagram",
      "severity": "blokująca",
      "status": "niespełniona",
      "target": "diagram: pomysł → … → commit → następny pomysł",
      "source": "poprzednia recenzja",
      "detail": "Pętla „następny pomysł” nadal nie jest domknięta czytelnie. Dolna linia kończy się pod „test”, a nie pod „commit”, i nie ma strzałki w górę do „commit”. Wygląda to tak, jakby wychodziła z „test”, a nie z „commit”. Dolny róg jest też przesunięty o jedną kolumnę względem pionowej kreski „│” nad nim. Popraw: przedłuż dolną linię pod „commit”, dodaj tam „↑” lub „│” prowadzące do „commit” i oznacz kierunek powrotu do „pomysł” strzałką „↑” przy „pomysł”, którą już masz. Wyrównaj znaki w kolumnach. Najprościej dopisz „→ następny pomysł (wracamy na początek)” i narysuj go jako osobną pętlę wychodzącą z „commit”."
    }
  ]
}
````
