# Krok 0060 · znudzony_czytelnik

Węzeł: `review` · dział: 1 · pytanie: 5 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Dlaczego komputer potrzebuje precyzyjnych instrukcji?".

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
## Czym jest język programowania
[[jezyk-programowania|Język programowania]] to ściśle określony sposób zapisywania [[instrukcja|instrukcji]], który potrafi zrozumieć komputer. Ma własne słowa i reguły zapisu, ale jest o wiele prostszy i bardziej rygorystyczny niż język polski.

Komputer nie wyciąga wniosków z kontekstu. Zdanie „podziel rachunek po równo” człowiek zrozumie od razu, komputer nie. Język programowania wymusza zapis, który ma jedno znaczenie. Zbiór jego reguł nazywamy [[skladnia|składnią]]: mówi ona, jak wolno układać słowa i znaki, żeby powstało poprawne polecenie.

Oto jedna instrukcja w Pythonie, języku, którego użyjemy w tym tutorialu:

```python
print("Cześć, Wspólna Kasa!")
```

```text
Cześć, Wspólna Kasa!
```

Słowo `print` znaczy „wypisz”, a tekst w cudzysłowie to to, co ma się pojawić na ekranie. Gdybyś pominął jeden cudzysłów, komputer odmówiłby wykonania polecenia, bo zapis łamie reguły.

Języków jest bardzo wiele, a każdy ma inną składnię i inne zastosowania. Różnią się zapisem, ale robią to samo: pozwalają opisać kroki, które komputer wykona. Kto pozna zasady jednego, łatwiej nauczy się następnych.

Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”.

NOWA SEKCJA "Po co komputerowi precyzja":
Komputer potrzebuje precyzyjnych [[instrukcja|instrukcji]], bo nie rozumie intencji, tylko wykonuje dokładnie to, co zapisano. Człowiek dopowiada sobie brakujące szczegóły, komputer ich nie zna i niczego nie zgaduje.

Wróćmy do czworga znajomych na wyjeździe. Polecenie „podziel rachunek po równo” dla nich jest jasne. Dla komputera brakuje w nim niemal wszystkiego:

| Człowiek rozumie | Komputer musi dostać |
|---|---|
| „rachunek” | które wydatki dodać i skąd je wziąć |
| „po równo” | przez ile osób dzielimy |
| „podziel” | co zrobić, gdy kwota nie dzieli się na równe części |
| (nic) | gdzie i w jakiej formie pokazać wynik |

Dlatego opis dla komputera wygląda tak:

```text
1. Dodaj wszystkie wydatki.
2. Podziel sumę przez liczbę osób.
3. Wypisz wynik z dokładnością do grosza.
```

Każdy krok ma jedno znaczenie i nie zostawia miejsca na domysły. Komputer wykona go tysiące razy bez zmęczenia, ale też bez zdrowego rozsądku. Jeśli podasz złą liczbę osób, pomyli się z pełną pewnością siebie.

Konsekwencja jest praktyczna: precyzja to zadanie programisty. To on ustala, co dokładnie ma się stać, i dlatego w pracy nad programem tyle miejsca zajmuje sprawdzanie i poprawianie.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Sekcja opisuje kroki słowami, ale nie pokazuje, co się dzieje, gdy komputer dostanie niedokładną instrukcję. Krótki przykład z liczbami (np. 100 zł na 3 osoby = 33,333… i pytanie, ile wypisać) uczyniłby tezę o „braku domysłów” namacalną. Można zastąpić zdanie o „złej liczbie osób”.",
      "severity": "sugestia",
      "target": "Każdy krok ma jedno znaczenie i nie zostawia miejsca na domysły",
      "source": "Nowa sekcja"
    },
    {
      "kind": "tempo",
      "detail": "Sekcja w dużej mierze powtarza tezę z poprzedniej („komputer nie wyciąga wniosków z kontekstu”, „podziel rachunek po równo”). Nowością jest tabela i lista kroków, ale ostatni akapit o pracy programisty i sprawdzaniu wprowadza nowy wątek bez rozwinięcia.",
      "severity": "sugestia",
      "target": "Ostatni akapit",
      "source": "Nowa sekcja"
    }
  ]
}
````
