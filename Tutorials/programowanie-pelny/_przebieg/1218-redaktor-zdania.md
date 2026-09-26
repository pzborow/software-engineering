# Krok 1218 · redaktor_zdania

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś redaktorem tutorialu: Programowanie od podstaw. W sekcji padła obietnica, której tutorial nie spełnił:
fraza „pokażemy w ćwiczeniu praktycznym” (praktyczne użycie Git na własnym komputerze).

Podaj w old całe zdanie z tą obietnicą, dokładnie jak w tekście, a w new to samo zdanie bez obietnicy (zachowaj resztę sensu).
Jeśli zdanie jest samą zapowiedzią, new zostaw puste.

SEKCJA "Po co zapisywać wersje kodu":
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
````

## Odpowiedź

````json
{
  "old": "Git trzeba mieć zainstalowanym (sprawdzisz to poleceniem `git --version`, a instalator jest na stronie git-scm.com). Jak to zrobić krok po kroku na swoim komputerze, pokażemy w ćwiczeniu praktycznym.",
  "new": "Git trzeba mieć zainstalowanym (sprawdzisz to poleceniem `git --version`, a instalator jest na stronie git-scm.com)."
}
````
