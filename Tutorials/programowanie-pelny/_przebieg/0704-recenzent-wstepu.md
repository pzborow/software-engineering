# Krok 0704 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 7 · pytanie: — · próba: 2

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
Gdy program rośnie, te same obliczenia zaczynają się powtarzać, a kod trudno przeczytać i poprawić. Ten dział pokazuje, jak zamknąć kawałek pracy w funkcji: nadać jej czytelną nazwę, przekazać dane i odebrać wynik. Po lekturze podzielisz program na małe, nazwane części i użyjesz ich wielokrotnie, tak jak w dziale 02 dzieliłeś problem na kroki, a pętle i listy z działu 06 zostaną w porządku. W przykładzie „Wspólnej Kasy” rozbijemy rozliczenie na funkcje suma_wydatkow, udzial_na_osobe i saldo_osoby. W warsztacie zbudujemy uproszczoną wersję: suma(wydatki) i na_osobe(suma, osoby), użyte dla dwóch różnych wyjazdów.

DIAGRAM:
                          osoby
                            │
                            ▼
wydatki ──► suma(wydatki) ──► suma ──► na_osobe(suma, osoby) ──► udział na osobę

Strzałka w funkcję: dane wchodzą. Strzałka z funkcji: wynik wychodzi.

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [diagram] Diagram: „suma, osoby ──► na_osobe(suma, osoby) ──► kwota”: Diagram jest niespójny z wstępem i wprowadza w błąd. Dwie linie wyglądają na dwa osobne, niepowiązane przepływy; nie widać, że wynik pierwszej funkcji (suma) trafia do drugiej. Etykieta „kwota” nie pojawia się w tekście (wstęp mówi o udziale na osobę), a „osoby” nie ma skąd się wziąć. Pominięto też saldo_osoby, choć wstęp ją zapowiada. Przerysuj jako jeden ciąg: wydatki ──► suma(wydatki) ──► suma ──► na_osobe(suma, osoby) ──► udział na osobę, z dopiskiem, że osoby (liczba osób) wchodzi do na_osobe z boku (np. strzałka z góry). Użyj tych samych nazw co w tekście albo krótko opisz, co znaczą strzałki (dane wchodzą / wynik wychodzi).
- [spójność] nazwy funkcji: suma_wydatkow, udzial_na_osobe, saldo_osoby vs suma(wydatki), na_osobe(suma, osoby): We wstępie te same funkcje występują pod dwoma różnymi zestawami nazw (suma_wydatkow/udzial_na_osobe vs suma/na_osobe), bez wyjaśnienia. Początkujący pomyśli, że to sześć różnych funkcji albo pomyłka. Ujednolić nazwy albo jedno zdanie: warsztat to uproszczona wersja przykładu. Diagram też używa krótkich nazw.
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
      "detail": "Strzałka z góry („osoby” i ▼) jest przesunięta w lewo. Wypada nad połączeniem suma(wydatki) ──► suma, a nie nad na_osobe(suma, osoby). Czytelnik może uznać, że liczba osób wchodzi do funkcji suma albo do samej strzałki. Przesuń „osoby” i ▼ tak, żeby stały dokładnie nad na_osobe(...), np. nad literami „na_osobe”. Reszta diagramu jest już spójna: jeden ciąg, te same nazwy co w warsztacie i legenda strzałek. Nazwy funkcji też są wyjaśnione, bo warsztat to „uproszczona wersja”.",
      "kind_note": "",
      "severity": "blokująca",
      "status": "niespełniona",
      "target": "diagram: strzałka „osoby” do na_osobe",
      "source": "diagram"
    }
  ]
}
````
