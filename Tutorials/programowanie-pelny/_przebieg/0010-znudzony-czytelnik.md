# Krok 0010 · znudzony_czytelnik

Węzeł: `review` · dział: 1 · pytanie: 1 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym jest program komputerowy?".

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

NOWA SEKCJA "Czym jest program komputerowy":
[[program-komputerowy|Program komputerowy]] to zapisany z góry ciąg poleceń, które komputer wykonuje krok po kroku, żeby zamienić dane na wynik. Komputer sam nic nie wie ani nie zgaduje: robi dokładnie to, co mu zapisano.

Pojedyncze polecenie to [[instrukcja|instrukcja]], czyli jeden mały, jednoznaczny krok, np. „dodaj dwie liczby” albo „wypisz tekst na ekranie”. Program to wiele takich instrukcji ułożonych w określonej kolejności. Kalkulator, przeglądarka i gra działają tak samo, tylko mają instrukcji bardzo dużo.

Prosty schemat każdego programu wygląda tak:

```text
dane na wejściu  -->  program (instrukcje)  -->  wynik na wyjściu
```

Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

Program „Wspólna Kasa” zrobi to za ciebie. Na wejściu dostanie listę wydatków (kto zapłacił i ile), a na wyjściu poda rozliczenie. Napisze go [[programista|programista]], czyli osoba, która zamienia potrzebę na instrukcje zrozumiałe dla komputera. Na razie nie piszemy kodu; ważne, że raz zapisane instrukcje można uruchamiać bez końca.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Wejście i wyjście „Wspólnej Kasy” opisano ogólnie („lista wydatków”, „rozliczenie”). Jedna linijka z liczbami (np. Ania zapłaciła 120 zł za paliwo, a wynik: Bartek oddaje Ani 30 zł) zilustrowałaby schemat wejście → program → wyjście. Zmieściłoby się w limicie po skróceniu jednego zdania.",
      "kind_note": "",
      "severity": "sugestia",
      "target": "akapit o „Wspólnej Kasie”",
      "source": "",
      "status": "nowa"
    }
  ]
}
````
