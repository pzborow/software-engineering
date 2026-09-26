# Krok 1175 · znudzony_czytelnik

Węzeł: `review` · dział: 10 · pytanie: 61 · próba: 2

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak automatyzacja prostych zadań może pomóc w pracy osoby spoza IT?".

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
## Od czego zacząć naukę
Zacznij od jednego małego problemu, który naprawdę Cię dotyczy, i jednego języka, np. [[python|Pythona]]. Nie szukaj idealnego kursu ani najlepszego języka: liczy się to, żebyś pisał(a) kod co tydzień i uruchamiał(a) go u siebie.

Praktyczny początek wygląda tak:

```text
mały problem → opis krokowy → kilka linii kodu → uruchomienie → commit
```

To ta sama pętla, którą znasz z sekcji o budowie programu od pomysłu. Różnica jest tylko w tym, że teraz to Ty wybierasz pomysł. Dobry pierwszy problem jest mały, znany z życia i da się go sprawdzić na kartce: rozliczenie wydatków, lista zakupów, przeliczanie kwot z arkusza.

Nie kopiuj gotowców bez zrozumienia. Lepiej napisać własną, kulawą wersję niż wkleić cudzą. Gdy utkniesz, szukaj tak, jak w sekcji o rozwiązaniach w internecie: po ostatniej linii komunikatu.

Kolejne elementy dokładaj po jednym: dane, decyzje, pętle, funkcje, pliki, testy. Ten tutorial jest taką drogą, a Wspólna Kasa to jej przykład.

Warsztat poniżej to Twój pierwszy samodzielny krok: dopisujesz do Wspólnej Kasy jedną własną funkcję, która wypisuje, kto ile dopłaca albo dostaje, i zapisujesz ją jako [[commit]]. W kolejnej sekcji zobaczysz, jak taki kawałek kodu zaczyna pracować za Ciebie.

NOWA SEKCJA "Automatyzacja prostych zadań":
[[automatyzacja|Automatyzacja]] to zlecenie komputerowi powtarzalnej czynności, którą wcześniej robiłeś(-aś) ręcznie. Osoba spoza IT zyskuje na niej czas i pewność: komputer nie nudzi się, nie myli przy setnej pozycji i robi to samo za każdym razem.

Mechanizm znasz: to [[petla|pętla]] po danych i [[funkcja|funkcja]]. Zamiast przepisywać kwoty do kalkulatora, opisujesz kroki raz, a program wykonuje je dla dowolnej liczby pozycji. Tak wygląda to we Wspólnej Kasie:

```python
wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.0},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.0},
           {"kto": "Celina", "opis": "bilety", "kwota": 15.0}]
osoby = ["Ania", "Bartek", "Celina"]
suma = 0
for wydatek in wydatki:
    suma = suma + wydatek["kwota"]
print(f"Razem: {suma} zł")
print(f"Na osobę: {suma / len(osoby)} zł")
```

```text
Razem: 180.0 zł
Na osobę: 60.0 zł
```

Jutro lista ma 200 wydatków zamiast trzech, a kod zostaje ten sam. Ten sam mechanizm obsłuży arkusz z fakturami czy listę zamówień w Twojej pracy.

Nie automatyzuj wszystkiego. Opłaca się zadanie, które powtarzasz często, ma jasne reguły i da się sprawdzić na kartce. Zadanie robione raz w roku lub wymagające oceny człowieka zwykle lepiej zostawić sobie.

Konsekwencja jest praktyczna: zaczynasz od małego, nudnego zadania z własnej pracy i piszesz je tą samą pętlą nauki. Po [[commit|commicie]] masz gotowe narzędzie, do którego możesz wracać. W warsztacie zapisujesz w ten sposób swój `dlugi.py`.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Czytelnik zna arkusz, więc zapyta: po co pętla, skoro SUMA w arkuszu robi to samo? Jedno zdanie o tym, kiedy kod wygrywa z arkuszem (np. zadanie powtarzane co tydzień na nowych plikach, bez klikania), dałoby realną decyzję zamiast ogólnika o arkuszu z fakturami.",
      "severity": "sugestia",
      "target": "Ten sam mechanizm obsłuży arkusz z fakturami"
    },
    {
      "kind": "odwołanie",
      "detail": "`dlugi.py` pojawia się bez wyjaśnienia. Poprzednia sekcja mówiła o funkcji dopisanej do Wspólnej Kasy. Warto jednym słowem powiedzieć, że to plik z funkcją liczącą, kto ile dopłaca.",
      "severity": "sugestia",
      "target": "`dlugi.py`"
    }
  ]
}
````
