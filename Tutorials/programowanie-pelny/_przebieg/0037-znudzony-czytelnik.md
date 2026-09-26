# Krok 0037 · znudzony_czytelnik

Węzeł: `review` · dział: 1 · pytanie: 3 · próba: 2

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
[[programista|Programista]] to osoba, która zamienia potrzebę na instrukcje: bierze problem opisany zwykłymi słowami i tworzy program, który go rozwiązuje. Pisanie [[kod|kodu]], czyli zapisanych w języku programowania instrukcji programu, to tylko część tej pracy.

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
      "detail": "Poprzednia sekcja już pokazała ten sam przykład (czworo znajomych) i niemal ten sam diagram: potrzeba, kroki, kod, uruchomienie, poprawki. Tu nowa jest tylko rola człowieka: rozmowa o potrzebach, czytanie cudzego kodu, szukanie błędów. Warto skrócić powtórkę etapów. Diagram można wyrzucić albo zastąpić jednym konkretnym zdaniem o tym, co programista robi w typowy dzień. Np. ustala ze znajomymi, czy kwoty mają być w złotych i groszach, i sprawdza, czy program dobrze liczy dla 3 osób i kwoty 100 zł.",
      "source": "nowa sekcja"
    }
  ]
}
````
