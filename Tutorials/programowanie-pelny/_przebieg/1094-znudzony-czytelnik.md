# Krok 1094 · znudzony_czytelnik

Węzeł: `review` · dział: 10 · pytanie: 56 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jakie są przykłady programów używanych na co dzień?".

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
## Szukanie rozwiązań w internecie
Wpisz w wyszukiwarkę to, co widzisz: ostatnią linię [[komunikat-o-bledzie|komunikatu o błędzie]] i nazwę języka. Prawie każdy błąd ktoś już miał i ktoś już opisał, jak go naprawić.

Ostatnia linia [[traceback|Tracebacku]] to ta, którą, jak w sekcji o czytaniu komunikatów, czytasz od dołu. Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych, bo nikt inny ich nie ma.

```text
python TypeError: unsupported operand type(s) for /: 'str' and 'int'
```

Gdy nie ma komunikatu, a wynik jest zły, opisz problem słowami: co robisz i co się dzieje, np. „python input zwraca tekst zamiast liczby”.

Wyniki oceniaj po kolei:

| Źródło | Jak je traktować |
|---|---|
| dokumentacja Pythona, czyli oficjalny opis języka i jego funkcji (docs.python.org) | najbardziej wiarygodna, ale sucha |
| pytania i odpowiedzi na forach, np. Stack Overflow | szukaj odpowiedzi z dużą liczbą głosów i sprawdź datę |
| poradniki i filmy | dobre na start, ale bywają przestarzałe |

Skopiowanego kodu nie wklejaj w ciemno. Przeczytaj, zrozum, co robi, i uruchom na małym przykładzie. Jeśli po kilku próbach nadal nic, zadaj własne pytanie: wklej pełny komunikat i najmniejszy kod, który błąd wywołuje.

Umiejętność szukania to zwykła część pracy programisty, nie oznaka słabości.

NOWA SEKCJA "Programy używane na co dzień":
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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Teza, że pod spodem są zmienne, if, pętle i funkcje, jest podana ogólnie. Przydałby się krótki kod (kilka linii Pythona) pokazujący np. alarm: porównanie godziny z zegarem przez if, żeby czytelnik zobaczył ten sam schemat w małym programie.",
      "severity": "sugestia",
      "target": "Pod spodem są te same klocki",
      "source": "akapit po tabeli"
    },
    {
      "kind": "tempo",
      "detail": "Sekcja w dużej części powtarza schemat wejście–przetwarzanie–wyjście, który czytelnik zna z własnych skryptów, a nowe pojęcia (aplikacja, interfejs) są wprowadzone jednym zdaniem. Ostatnie zdanie o automatyzacji pracy pojawia się nagle bez przykładu.",
      "severity": "sugestia",
      "target": "Konsekwencja: ... zautomatyzować",
      "source": "ostatni akapit"
    }
  ]
}
````
