# Krok 1064 · znudzony_czytelnik

Węzeł: `review` · dział: 9 · pytanie: 55 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak szukać rozwiązań problemów programistycznych w internecie?".

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
## Po co zapisywać wersje kodu
Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast szukać własnych zmian z pamięci.

Robi to [[git|Git]], program do zapisywania historii plików. Zapis jednej wersji to [[commit|commit]]: zdjęcie wybranych plików z danej chwili, z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię, to [[repozytorium|repozytorium]]. W przykładowym programie do dzielenia wydatków, „Wspólnej Kasie”, będzie nim folder `wspolna_kasa`, w którym leżą pliki programu.

Wersje przydają się w trzech sytuacjach:

- Dopisujesz do „Wspólnej Kasy” nową funkcję, [[sec-09-czym-jest-testowanie-programu|testy]] przestają przechodzić, a Ty wracasz do wczorajszego commita zamiast szukać własnych zmian.
- Historia pokazuje, kiedy pojawił się błąd, co przy szukaniu przyczyny oszczędza sporo czasu.
- Każdy commit ma opis, więc po miesiącu wiesz, dlaczego kod wygląda tak, a nie inaczej.

Dobry moment na commit to chwila, gdy testy przechodzą. Wiele małych commitów jest lepsze niż jeden wielki.

Sam zapis wygląda tak:

```text
git init -b main
git add funkcje.py test_rozlicz.py
git commit -m "Funkcje i testy Wspolnej Kasy"
```

`init` zakłada repozytorium w bieżącym folderze, `add` wybiera pliki do zapisu, a `commit` zapisuje wersję. Git trzeba mieć zainstalowanym (sprawdzisz to poleceniem `git --version`, a instalator jest na stronie git-scm.com). Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym.

NOWA SEKCJA "Szukanie rozwiązań w internecie":
Wpisz w wyszukiwarkę to, co widzisz: ostatnią linię [[komunikat-o-bledzie|komunikatu o błędzie]] i nazwę języka. Prawie każdy błąd ktoś już miał i ktoś już opisał, jak go naprawić.

Ostatnia linia [[traceback|Tracebacku]] to ta, którą, jak w sekcji o czytaniu komunikatów, czytasz od dołu. Skopiuj ją, ale bez elementów tylko Twoich: ścieżek do plików i nazw własnych zmiennych, bo nikt inny ich nie ma.

```text
python TypeError: unsupported operand type(s) for /: 'str' and 'int'
```

Gdy nie ma komunikatu, a wynik jest zły, opisz problem słowami: co robisz i co się dzieje, np. „python input zwraca tekst zamiast liczby”.

Wyniki oceniaj po kolei:

| Źródło | Jak je traktować |
|---|---|
| [[dokumentacja|dokumentacja]] Pythona (oficjalny opis języka, docs.python.org) | najbardziej wiarygodna, ale sucha |
| pytania i odpowiedzi na forach, np. Stack Overflow | szukaj odpowiedzi z dużą liczbą głosów i sprawdź datę |
| poradniki i filmy | dobre na start, ale bywają przestarzałe |

Skopiowanego kodu nie wklejaj w ciemno. Przeczytaj, zrozum, co robi, i uruchom na małym przykładzie. Jeśli po kilku próbach nadal nic, zadaj własne pytanie: wklej pełny komunikat i najmniejszy kod, który błąd wywołuje.

Umiejętność szukania to zwykła część pracy programisty, nie oznaka słabości.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
