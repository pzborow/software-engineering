# Krok 1044 · znudzony_czytelnik

Węzeł: `review` · dział: 9 · pytanie: 54 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Dlaczego warto zapisywać kolejne wersje kodu?".

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
## Czym jest debugowanie
[[debugowanie|Debugowanie]] to szukanie przyczyny błędu i jej usuwanie. Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach.

Metoda jest prosta. Najpierw odtwarzasz błąd na jednych, konkretnych danych. Potem zawężasz miejsce: przed podejrzanym krokiem wypisujesz wartości i porównujesz je z tym, czego oczekujesz. Pierwsze miejsce, w którym wartość jest inna niż powinna, wskazuje przyczynę. Na końcu poprawiasz jedną rzecz i uruchamiasz ponownie.

Weźmy [[blad-logiczny|błąd logiczny]] z wynikiem 39.0 zamiast 26.0. Podejrzewamy dwa dane wejściowe dzielenia, więc je wypisujemy:

```python
def na_osobe(suma, osoby):
    return suma / osoby

suma = 78.0
liczba_osob = 2
print("DEBUG suma:", suma)
print("DEBUG liczba_osob:", liczba_osob)
print(na_osobe(suma, liczba_osob))
```

```text
DEBUG suma: 78.0
DEBUG liczba_osob: 2
39.0
```

Suma się zgadza, a liczba osób nie: mają być trzy. Funkcja jest w porządku, błąd siedzi w danych, które jej podajemy. Bez wypisania szukalibyśmy pewnie w dzieleniu.

Gdy test z poprzedniej sekcji zgłosi błąd, zaczynasz tak samo: odtwarzasz przypadek, który go wywołał, i patrzysz na wartości. Po naprawie usuń linie z `DEBUG`, żeby nie zaśmiecały wyniku.

NOWA SEKCJA "Po co zapisywać wersje kodu":
Zapisujesz kolejne wersje, żeby zawsze móc wrócić do stanu, który działał. Poprawka, która psuje program, przestaje być problemem: cofasz ją, zamiast pamiętać, co dokładnie zmieniłeś.

Robi to [[git|Git]], program do zapisywania historii plików. Zapis jednej wersji to [[commit|commit]]: migawka wybranych plików z krótkim opisem, co i po co się zmieniło. Miejsce, w którym Git trzyma całą historię projektu, to [[repozytorium|repozytorium]]. Dla „Wspólnej Kasy” będzie to `wspolna_kasa`.

Wersje przydają się w trzech sytuacjach:

- Po nieudanej zmianie wracasz do ostatniej działającej wersji.
- Historia pokazuje, kiedy pojawił się błąd, co przy szukaniu przyczyny oszczędza sporo czasu.
- Możesz śmiało eksperymentować, bo stara wersja i tak jest bezpieczna.

Dobry moment na commit to chwila, gdy testy przechodzą. Opis pisz tak, żeby po miesiącu dało się z niego coś zrozumieć. Wiele małych commitów jest lepsze niż jeden wielki.

Sam zapis wygląda tak:

```text
git init -b main
git add funkcje.py test_kasa.py
git commit -m "Funkcje Wspolnej Kasy i testy"
```

`init` zakłada repozytorium, `add` wybiera pliki do zapisu, a `commit` zapisuje wersję. Wybór plików przez `add` sprawia, że do historii trafia tylko to, co chcesz. Wykonasz to u siebie w warsztacie.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Sedno odpowiedzi to trzy ogólne punkty (wrócić do działającej wersji, znaleźć, kiedy pojawił się błąd, eksperymentować). Żaden nie ma konkretnego scenariusza, a kod pokazuje tylko, jak zapisać wersję, nie po co. Wystarczy jedno zdanie o „Wspólnej Kasie”. Na przykład: dopisujesz nową funkcję, testy przestają przechodzić, a wracasz do wczorajszego commita zamiast szukać własnych zmian. Można nim zastąpić jeden z punktów, na przykład trzeci, który tylko powtarza pierwszy.",
      "target": "lista trzech sytuacji",
      "severity": "blokująca",
      "source": "Wersje przydają się w trzech sytuacjach",
      "status": "nowa"
    }
  ]
}
````
