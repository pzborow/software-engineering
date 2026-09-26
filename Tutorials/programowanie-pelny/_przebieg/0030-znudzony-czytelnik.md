# Krok 0030 · znudzony_czytelnik

Węzeł: `review` · dział: 1 · pytanie: 3 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Kim jest programista i czym się zajmuje?".

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
## Czym jest programowanie
[[programowanie|Programowanie]] to tworzenie programów: zamiana problemu na ciąg instrukcji, które komputer wykona bez twojego udziału. Samo pisanie jest tylko jednym z etapów, a największą część pracy zajmuje wymyślenie rozwiązania.

Zwykle wygląda to tak:

```text
problem --> kroki rozwiązania --> zapis dla komputera --> uruchomienie --> poprawki
                   ^                                                         |
                   +---------------------------------------------------------+
```

Wróćmy do czworga znajomych z wyjazdu. Najpierw trzeba dokładnie ustalić, co jest problemem: kto komu ile ma oddać, żeby każdy zapłacił tyle samo. Potem rozbijasz to na kroki, które wykonałbyś na kartce: zsumuj wydatki, podziel przez liczbę osób, porównaj z tym, co kto zapłacił. Dopiero taki opis zapisujesz w [[jezyk-programowania|języku programowania]], czyli w ściśle określonym języku, który komputer potrafi odczytać. Tym językiem zajmiemy się osobno.

Pierwsza wersja rzadko działa idealnie. Uruchamiasz program, patrzysz na wynik, znajdujesz pomyłkę i poprawiasz. Ta pętla poprawek to normalna część pracy, a nie dowód, że coś poszło nie tak.

Zyskujesz na tym jedną rzecz: raz opisane rozwiązanie działa przy każdym kolejnym wyjeździe, dla dowolnych kwot.

NOWA SEKCJA "Kim jest programista":
[[programista|Programista]] to osoba, która zamienia potrzebę na instrukcje: bierze problem opisany zwykłymi słowami i tworzy program, który go rozwiązuje. Pisanie kodu to tylko część tej pracy.

Weźmy czworo znajomych z wyjazdu, którzy męczą się z rozliczaniem wydatków w arkuszu. Ktoś musi ustalić, czego naprawdę potrzebują: czy program ma tylko wyliczyć, kto komu ile oddaje, czy też pamiętać kolejne wyjazdy. Potem opisuje rozwiązanie krok po kroku, zapisuje je w języku programowania, sprawdza na kilku przykładach i poprawia błędy.

```text
potrzeba --> ustalenie, co program ma robić --> kroki --> kod --> sprawdzanie --> poprawki
```

Programista sporo czasu spędza więc na rozmowie, myśleniu, czytaniu cudzego kodu i szukaniu przyczyn błędów. Rzadko zaczyna od pustej strony, często rozwija program, który już istnieje.

Nie trzeba być programistą z zawodu, żeby programować. Osoba spoza IT, która napisze mały program do własnych rozliczeń, wykonuje tę samą pracę, tylko na mniejszą skalę.

Na razie nie piszemy kodu. Ten problem z wydatkami będzie jednak przykładem, który będzie nam towarzyszył: program „Wspólna Kasa” zbudujemy razem, a ty przećwiczysz w tej roli.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "tempo",
      "severity": "sugestia",
      "target": "akapit z wyjazdem i diagram",
      "detail": "Poprzednia sekcja pokazała prawie ten sam przepływ (potrzeba, kroki, kod, uruchomienie, poprawki) na tym samym przykładzie z czworgiem znajomych. Nowego jest tu tylko ustalanie, czego ktoś naprawdę potrzebuje. Diagram można wyciąć albo zastąpić jednym zdaniem o tym, czym rola różni się od samego procesu.",
      "source": "sekcja",
      "status": "nowa"
    },
    {
      "kind": "konkret",
      "severity": "sugestia",
      "target": "Programista sporo czasu spędza na rozmowie, myśleniu, czytaniu cudzego kodu",
      "detail": "To lista ogólników. Jedno małe porównanie albo liczba by pomogły, na przykład: pisanie to ułamek dnia, a reszta to ustalanie i szukanie błędów. Można też dodać jedno pytanie, które programista zadałby znajomym.",
      "source": "sekcja",
      "status": "nowa"
    }
  ]
}
````
