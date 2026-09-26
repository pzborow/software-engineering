# Krok 0964 · recenzent_wstępu

Węzeł: `open_chapter` · dział: 9 · pytanie: — · próba: 2

## Prompt

````text
Jesteś recenzentem wstępu działu w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Dział 09: "Błędy i dobre praktyki". Pytania, na które odpowie:
- Czym różni się błąd składni od błędu logicznego?
- Jak przeczytać komunikat o błędzie?
- Czym jest testowanie programu?
- Czym jest debugowanie?
- Dlaczego warto zapisywać kolejne wersje kodu?
- Jak szukać rozwiązań problemów programistycznych w internecie?

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
Każdy program prędzej czy później się myli, a do tej pory wiedziałeś tylko, że coś poszło nie tak. Ten dział uczy, jak spokojnie znaleźć przyczynę: przeczytać komunikat błędu, sprawdzić program testami, prześledzić go krok po kroku i zapisać poprawioną wersję, żeby nic nie przepadło. Wracamy do funkcji z działu 7 i danych od użytkownika z działu 8, bo w nich najłatwiej o pomyłkę. Na przykładzie „Wspólnej Kasy" naprawimy błąd psujący rozliczenie, a w warsztacie sami go wywołamy, zbadamy i zapiszemy poprawkę w Git.

DIAGRAM:
uruchomienie → komunikat lub zły wynik
   → szukanie przyczyny (debugowanie)
   → poprawka
   → test
        ├─ test nie przechodzi → wracamy do szukania przyczyny
        └─ test przechodzi → zapis wersji (Git)

TO JEST PONOWNA RECENZJA POPRAWIONEJ WERSJI. Autor dostał te uwagi:
- [diagram] diagram: Diagram jest mylący: strzałka powrotna z „zapisu wersji” wraca do „błędu” bez etykiety, więc nie wiadomo, co znaczy (po zapisie pojawia się nowy błąd? cykl trwa w nieskończoność?). Test stoi po komunikacie, choć testy służą do wykrywania błędów, a komunikat pojawia się przy uruchomieniu; kolejność jest niejasna. Przerysuj: np. „uruchomienie → komunikat lub zły wynik → szukanie przyczyny (debugowanie) → poprawka → test → zapis wersji”, a strzałkę powrotną opisz („test nadal nie przechodzi → wracamy do szukania przyczyny”) i poprowadź z testu, nie z zapisu. Albo usuń diagram.
Dla każdej z nich sprawdź, czy nowa wersja ją spełnia. Niespełnioną zgłoś ponownie z status="niespełniona"
i tym samym target. Spełnionych nie zgłaszaj. Nowe problemy (status="nowa") zgłaszaj WYŁĄCZNIE, gdy są blokujące:
to nie jest okazja do kolejnej rundy ulepszeń.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
