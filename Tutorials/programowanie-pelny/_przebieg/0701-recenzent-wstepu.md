# Krok 0701 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 7 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 07: "Funkcje i porządek w kodzie". Pytania, na które odpowie:
- Czym jest funkcja?
- Po co dzielić program na funkcje?
- Czym są argumenty funkcji?
- Co to znaczy, że funkcja zwraca wynik?
- Dlaczego nazwy zmiennych i funkcji powinny być czytelne?
- Czym jest ponowne użycie kodu?

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
Gdy program rośnie, te same obliczenia zaczynają się powtarzać, a kod trudno przeczytać i poprawić. Ten dział pokazuje, jak zamknąć kawałek pracy w funkcji: nadać jej czytelną nazwę, przekazać dane i odebrać wynik. Po lekturze będziesz umieć dzielić program na małe, nazwane części i używać ich wielokrotnie, tak jak dzielisz problem na kroki (dział 02), a pętle i listy (dział 06) trzymasz w porządku. Na przykładzie „Wspólnej Kasy” rozbijemy rozliczenie na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby, a w warsztacie użyjemy suma(wydatki) i na_osobe(suma, osoby) dla dwóch różnych wyjazdów.

DIAGRAM:
wydatki ──► suma(wydatki) ──► suma
suma, osoby ──► na_osobe(suma, osoby) ──► kwota
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "diagram",
      "severity": "blokująca",
      "target": "Diagram: „suma, osoby ──► na_osobe(suma, osoby) ──► kwota”",
      "detail": "Diagram jest niespójny z wstępem i wprowadza w błąd. Dwie linie wyglądają na dwa osobne, niepowiązane przepływy; nie widać, że wynik pierwszej funkcji (suma) trafia do drugiej. Etykieta „kwota” nie pojawia się w tekście (wstęp mówi o udziale na osobę), a „osoby” nie ma skąd się wziąć. Pominięto też saldo_osoby, choć wstęp ją zapowiada. Przerysuj jako jeden ciąg: wydatki ──► suma(wydatki) ──► suma ──► na_osobe(suma, osoby) ──► udział na osobę, z dopiskiem, że osoby (liczba osób) wchodzi do na_osobe z boku (np. strzałka z góry). Użyj tych samych nazw co w tekście albo krótko opisz, co znaczą strzałki (dane wchodzą / wynik wychodzi)."
    },
    {
      "kind": "spójność",
      "severity": "blokująca",
      "target": "nazwy funkcji: suma_wydatkow, udzial_na_osobe, saldo_osoby vs suma(wydatki), na_osobe(suma, osoby)",
      "detail": "We wstępie te same funkcje występują pod dwoma różnymi zestawami nazw (suma_wydatkow/udzial_na_osobe vs suma/na_osobe), bez wyjaśnienia. Początkujący pomyśli, że to sześć różnych funkcji albo pomyłka. Ujednolić nazwy albo jedno zdanie: warsztat to uproszczona wersja przykładu. Diagram też używa krótkich nazw."
    },
    {
      "kind": "tempo",
      "severity": "sugestia",
      "target": "Wymienione nazwy funkcji i zapisy typu suma(wydatki), na_osobe(suma, osoby)",
      "detail": "Wstęp jest gęsty od zapisów kodu, a czytelnik nie zna jeszcze nawiasów w wywołaniu funkcji. Zostaw w tekście nazwy zapowiadające scenariusz (Wspólna Kasa, dwa wyjazdy), a zapisy kodu zostaw diagramowi lub sekcjom."
    },
    {
      "kind": "wyjaśnienie",
      "severity": "sugestia",
      "target": "„Wspólnej Kasy”",
      "detail": "Jeśli „Wspólna Kasa” nie była wprowadzona w poprzednich działach, dodaj pół zdania: kto z kim się rozlicza (np. wspólne wydatki na wyjeździe). Wtedy hasło „saldo osoby” będzie zrozumiałe."
    }
  ]
}
````
