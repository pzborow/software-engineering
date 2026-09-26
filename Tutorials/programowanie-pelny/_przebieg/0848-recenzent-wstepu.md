# Krok 0848 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 8 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 08: "Współpraca programu z użytkownikiem". Pytania, na które odpowie:
- Czym są dane wejściowe programu?
- Czym są dane wyjściowe programu?
- Jak program może zapytać użytkownika o informację?
- Czym jest plik i jak program może z niego korzystać?
- Czym jest interfejs użytkownika?
- Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?

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
Dotąd Twoje programy liczyły na danych wpisanych na sztywno w kodzie, a prawdziwy program musi umieć rozmawiać z człowiekiem. W tym dziale nauczysz się przyjmować dane od użytkownika, pokazywać mu wyniki, zapisywać je w pliku i wczytywać z powrotem oraz odrzucać błędnie wpisane wartości. Wykorzystasz przy tym zmienne, decyzje, pętle i funkcje z poprzednich działów. W przykładzie „Wspólna Kasa” program wczyta wydatki z pliku, zapyta o nowy wydatek i sprawdzi kwotę, a w warsztacie zbudujesz to krok po kroku, łącznie z ponownym pytaniem po wpisaniu tekstu zamiast liczby.

DIAGRAM:
użytkownik --wpisuje--> [ program ] --pokazuje--> użytkownik
                        ^    |
                    wczytuje zapisuje
                        |    v
                        [ plik ]
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "diagram",
      "severity": "sugestia",
      "target": "strzałki wczytuje/zapisuje",
      "detail": "Etykiety stoją obok dwóch pionowych strzałek i trzeba się domyślać, która należy do której. Lepiej narysować dwie oddzielne strzałki z etykietami przy nich, np. 'program --zapisuje--> [ plik ]' oraz '[ plik ] --wczytuje--> program'. Wtedy kierunek przepływu jest oczywisty.",
      "source": "diagram"
    },
    {
      "kind": "diagram",
      "severity": "sugestia",
      "target": "etykiety wpisuje/pokazuje",
      "detail": "Strzałki nie mówią, co przepływa. Dopisz 'wpisuje dane' i 'pokazuje wyniki'. To ułatwi później powiązanie diagramu z pojęciami dane wejściowe i wyjściowe, a czytelnik bez tego nie zauważy, że użytkownik po obu stronach to ta sama osoba.",
      "source": "diagram"
    }
  ]
}
````
