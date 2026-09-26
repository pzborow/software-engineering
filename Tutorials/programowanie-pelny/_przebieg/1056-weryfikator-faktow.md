# Krok 1056 · weryfikator_faktów

Węzeł: `review` · dział: 9 · pytanie: 54 · próba: 2

## Prompt

````text
Jesteś weryfikatorem faktów tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Wersje obowiązujące w tutorialu: Python 3.13. Wersje zadeklarowane w sekcji: Git 2.x.

Sprawdź w DOKUMENTACJI konkretne, sprawdzalne twierdzenia nowej sekcji: komendy i ich flagi, nazwy argumentów,
pól i zasobów, wartości domyślne, składnię oraz zachowanie zależne od wersji.
- Najpierw Context7: resolve-library-id, potem query-docs. Gdy czegoś nie ma w Context7, użyj WebFetch
  na oficjalnej stronie dokumentacji. Najwyżej 4 zapytania łącznie: wybierz twierdzenia najbardziej narażone na błąd.
- Nie oceniaj stylu, dydaktyki ani ogólnych idei. Kod jest szkicem: `...` i pominięte fragmenty nie są błędem.
- Każdą niezgodność z dokumentacją zgłoś jako kind="fakt", target=fragment sekcji, detail=co mówi dokumentacja
  (z adresem strony) i jak poprawić. "blokująca", gdy czytelnik wykonując kod dostałby błąd albo inne zachowanie;
  "sugestia", gdy to nieścisłość bez takich skutków.
- sources: tylko strony, które faktycznie przeczytałeś, i które twierdzenie sekcji potwierdzają albo obalają.
- ok=true, gdy nie ma blokujących niezgodności.

NOWA SEKCJA "Po co zapisywać wersje kodu":
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
  "ok": true,
  "needs": [
    {
      "kind": "fakt",
      "severity": "sugestia",
      "target": "git init -b main",
      "detail": "Dokumentacja git-init (https://git-scm.com/docs/git-init) potwierdza opcję `-b <branch-name>` / `--initial-branch=<branch-name>`. Opcja pojawiła się w Git 2.28 (ta informacja pochodzi z mojej wiedzy, strona ze Context7 jej nie podaje). Sekcja deklaruje tylko „Git 2.x”, więc na starszym Gicie 2.x (do 2.27) `git init -b main` zwróci błąd nieznanej opcji. Popraw deklarację wersji na „Git 2.28 lub nowszy” albo dopisz w tekście, że polecenie wymaga nowszego Gita.",
      "source": "https://git-scm.com/docs/git-init",
      "status": "nowa",
      "target_note": ""
    }
  ],
  "sources": [
    {
      "title": "git-init Documentation",
      "url": "https://git-scm.com/docs/git-init",
      "supports": "Opcja `-b <branch-name>` / `--initial-branch` istnieje i ustawia nazwę początkowej gałęzi; domyślnie `master`, konfigurowalne przez init.defaultBranch. Wpis „git init” bez argumentu działa w bieżącym folderze (składnia z opcjonalnym <directory>)."
    }
  ]
}
````
