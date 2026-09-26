# Krok 0310 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 4 · pytanie: — · próba: 1

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 04: "Dane i zmienne". Pytania, na które odpowie:
- Czym jest dana w programie?
- Czym jest zmienna?
- Jak można porównać zmienną do pudełka z etykietą?
- Czym różni się liczba od tekstu w programie?
- Czym jest typ danych?
- Co to jest wartość logiczna prawda/fałsz?
- Do czego służy przypisanie wartości do zmiennej?

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
Każdy program musi gdzieś zapamiętać to, na czym pracuje: imię, kwotę, informację, czy coś już zrobiono. Ten dział pokazuje, jak w Pythonie przechowywać takie informacje i jak odróżniać ich rodzaje, np. liczbę od tekstu czy prawdę od fałszu. Po jego przeczytaniu utworzysz własne zmienne i sprawdzisz, co w nich leży. Do tej pory pisaliśmy instrukcje, które coś wypisywały lub wykonywały; teraz dostaną one dane, na których mogą pracować. W przykładzie „Wspólna Kasa” do rozlicz.py trafią imię, opis i kwota wydatku oraz informacja „czy zapłacono”, a w warsztacie w kasa.py wypiszemy je razem z typami.

DIAGRAM:
instrukcje (dział 03) + dane (dział 04) → program

kwota  ← 45.50   (liczba)
opis   ← "obiad" (tekst)
oplacone ← True  (prawda/fałsz)
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "diagram",
      "severity": "sugestia",
      "target": "kwota ← 45.50 (liczba) itd.",
      "detail": "Strzałka ← nie jest nigdzie wyjaśniona, a w pierwszej linii diagramu strzałka → znaczy coś innego (składanie w program). Dodaj krótki podpis, np. „nazwa ← wartość (wartość trafia pod nazwę)”, albo narysuj pudełka z etykietą: [kwota: 45.50]. Warto też oddzielić wizualnie dwie części albo dać im nagłówki, żeby nie wyglądały na jeden przepływ.",
      "source": "diagram"
    },
    {
      "kind": "diagram",
      "severity": "sugestia",
      "target": "instrukcje (dział 03) + dane (dział 04) → program",
      "detail": "Pierwsza linia mówi to samo co zdanie „Do tej pory pisaliśmy instrukcje… teraz dostaną dane” i niewiele dodaje. Można ją usunąć albo połączyć z drugą częścią, tak by diagram pokazywał dane wchodzące do instrukcji.",
      "source": "diagram"
    },
    {
      "kind": "język",
      "severity": "sugestia",
      "target": "True, 45.50",
      "detail": "Czytelnik spoza IT zobaczy w diagramie „True” i kropkę dziesiętną zamiast przecinka bez żadnego sygnału, że tak wygląda zapis w Pythonie. Dodaj podpis, np. „zapis w Pythonie”, żeby nie wyglądało to na błąd.",
      "source": "diagram"
    }
  ]
}
````
