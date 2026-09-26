# Krok 1111 · znudzony_czytelnik

Węzeł: `review` · dział: 10 · pytanie: 57 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym różni się strona internetowa od aplikacji mobilnej?".

Zgłoś potrzeby (najwyżej 3, zero też jest dobrą odpowiedzią), wybierając kind:
- "przykład": teza jest abstrakcyjna i brakuje krótkiego kodu lub scenariusza,
- "konkret": ogólniki zamiast decyzji, liczby, nazwy klasy albo porównania,
- "skrócenie": powtórzenia, lanie wody, przykład dłuższy niż potrzeba,
- "diagram": przepływ łatwiej zrozumieć z rysunku tekstowego,
- "tempo": za dużo nowych pojęć naraz albo sekcja nie wnosi nic nowego względem poprzedniej.
Sekcja ma limit 250 słów prozy i jeden, najwyżej dwa krótkie bloki kodu.
Nie proś o coś, co się w tym nie zmieści, i nie żądaj jednocześnie dodania i skrócenia.
Kod może być tylko w językach: python, text.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

POPRZEDNIA SEKCJA:
## Programy używane na co dzień
Na co dzień używasz dziesiątek programów, choć rzadko o tym myślisz: komunikatora, mapy, banku w telefonie, arkusza kalkulacyjnego, przeglądarki. Każdy z nich to [[program-komputerowy|program]] albo [[aplikacja|aplikacja]], czyli program z oprawą dla użytkownika, i działa według tego samego schematu, który znasz z własnych skryptów.

Zawsze są [[dane-wejsciowe|dane wejściowe]], jakieś przetwarzanie i [[dane-wyjsciowe|dane wyjściowe]]:

| Program | Wejście | Co robi | Wyjście |
|---|---|---|---|
| Nawigacja | cel podróży, Twoja pozycja | wybiera najkrótszą trasę | trasa na mapie |
| Bank w telefonie | kwota i numer konta | sprawdza saldo, księguje przelew | potwierdzenie |
| Arkusz kalkulacyjny | liczby w komórkach | liczy wzory | sumy i wykresy |
| Wyszukiwarka | wpisane słowa | szuka i układa wyniki | lista stron |
| Alarm w telefonie | ustawiona godzina | porównuje ją z zegarem | dzwonek |

Pod spodem są te same klocki, które już budowałeś: zmienne, decyzje (`if`), pętle po listach, funkcje i pliki. Nawigacja też przegląda listę dróg i wybiera jedną, a bank też sprawdza dane od użytkownika, zanim cokolwiek zaksięguje.

Różni je skala i [[interfejs-uzytkownika|interfejs]]: przyciski i mapy zamiast pytań w terminalu. Program do dzielenia wspólnych wydatków między osoby, który budujesz w warsztacie (nazywamy go „Wspólna Kasa”), należy do tej samej rodziny: bierze wydatki, liczy i wypisuje, kto ile zapłacił. Jest po prostu mały. Czym różni się strona internetowa od aplikacji mobilnej, wyjaśnimy w następnej sekcji.

Konsekwencja: skoro gotowe programy to złożone proste kroki, da się je zrozumieć, a proste zadania z Twojej pracy da się zautomatyzować własnym małym programem.

NOWA SEKCJA "Strona internetowa a aplikacja mobilna":
Strona internetowa działa w [[przegladarka|przeglądarce]] (programie do otwierania stron, np. Chrome czy Firefox) i otwierasz ją przez adres, a aplikacja mobilna to program zainstalowany w telefonie, pobrany ze sklepu. Obie są [[aplikacja|aplikacjami]] w sensie oprawy dla użytkownika, ale trafiają do niego inaczej.

Strona leży na cudzym komputerze, czyli [[serwer|serwerze]] (komputerze w internecie, który przechowuje stronę i odpowiada na zapytania). Przeglądarka pobiera ją za każdym razem, więc nic nie instalujesz, a autor może ją poprawić dla wszystkich naraz. Ta sama strona działa na komputerze, tablecie i telefonie.

Aplikacja mobilna jest zainstalowana na urządzeniu. Ma łatwiejszy dostęp do aparatu, powiadomień czy czujników i często działa bez internetu. Za to wymaga pobrania, aktualizacji i osobnej wersji dla każdego systemu, np. Androida i iOS.

| Cecha | Strona internetowa | Aplikacja mobilna |
|---|---|---|
| Uruchomienie | adres w przeglądarce | ikona na telefonie |
| Instalacja | brak | ze sklepu |
| Aktualizacja | automatyczna, u autora | pobierasz nową wersję |
| Dostęp do aparatu i czujników | ograniczony | szeroki |
| Bez internetu | zwykle nie działa | często działa |

Pod spodem obie robią to samo, co każdy program: dane wejściowe, przetwarzanie, dane wyjściowe. We „Wspólnej Kasie” wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.

Konsekwencja: rachunki możesz kiedyś udostępnić jako stronę, którą znajomi otworzą przez link, albo jako aplikację w telefonie. Na razie masz wersję w terminalu, a jej funkcje liczące przydałyby się w obu wariantach.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "tempo",
      "detail": "Akapit „Pod spodem obie robią to samo…” powtarza schemat wejście–przetwarzanie–wyjście z poprzedniej sekcji. Wystarczy jedno zdanie o tym, że „Wspólna Kasa” może stać się stroną albo aplikacją. Zaoszczędzone słowa można przeznaczyć na konkretny przykład różnicy, np. że strona banku otworzy się na każdym telefonie bez instalacji, a aplikacja banku wyśle powiadomienie o przelewie.",
      "severity": "sugestia",
      "target": "akapit „Pod spodem obie robią to samo”",
      "source": "nowa sekcja"
    }
  ]
}
````
