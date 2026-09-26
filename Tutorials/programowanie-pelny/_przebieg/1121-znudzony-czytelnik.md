# Krok 1121 · znudzony_czytelnik

Węzeł: `review` · dział: 10 · pytanie: 58 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak od pomysłu dojść do działającego programu?".

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
## Strona internetowa a aplikacja mobilna
Strona internetowa działa w [[przegladarka|przeglądarce]] (programie do otwierania stron, np. Chrome czy Firefox) i otwierasz ją przez adres, a aplikacja mobilna to program zainstalowany w telefonie, pobrany ze sklepu. Obie są [[aplikacja|aplikacjami]] w sensie oprawy dla użytkownika, ale trafiają do niego inaczej.

Strona leży na cudzym komputerze, czyli [[serwer|serwerze]] (komputerze w internecie, który przechowuje stronę i odpowiada na zapytania). Przeglądarka pobiera ją za każdym razem, więc nic nie instalujesz, a autor może ją poprawić dla wszystkich naraz. Ta sama strona działa na komputerze, tablecie i telefonie.

Aplikacja mobilna jest zainstalowana na urządzeniu. Ma łatwiejszy dostęp do aparatu, powiadomień czy czujników i często działa bez internetu. Za to wymaga pobrania, aktualizacji i osobnej wersji dla każdego systemu, np. Androida i iOS.

| Cecha | Strona internetowa | Aplikacja mobilna |
|---|---|---|
| Uruchomienie | adres w przeglądarce | ikona na telefonie |
| Instalacja | brak | ze sklepu |
| Aktualizacja | automatyczna, u autora | pobierasz nową wersję |
| Dostęp do aparatu i czujników | ograniczony | szeroki |
| Bez internetu | zwykle nie działa | często działa |

Pod spodem obie robią to samo, co każdy program: dane wejściowe, przetwarzanie, dane wyjściowe. We „Wspólnej Kasie” wejściem są kwoty wpisane przez znajomych, przetwarzaniem podział rachunku, a wyjściem wynik na ekranie strony albo aplikacji. Zmienia się tylko miejsce uruchomienia i sposób dostarczenia.

Konsekwencja: rachunki możesz kiedyś udostępnić jako stronę, którą znajomi otworzą przez link, albo jako aplikację w telefonie. Na razie masz wersję w terminalu, a jej funkcje liczące przydałyby się w obu wariantach.

NOWA SEKCJA "Od pomysłu do działającego programu":
Od pomysłu do programu dochodzi się małymi krokami: opisujesz zadanie zwykłymi słowami, piszesz najmniejszy kawałek, który coś robi, sprawdzasz go i dopiero wtedy dokładasz następny. Cały program naraz zwykle nie działa, a szukanie błędu w stu liniach jest męczące.

```text
pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit
              ↑                                                            |
              └──────────────────── następny kawałek ←─────────────────────┘
```

Weźmy pomysł: „chcę wiedzieć, kto komu ile jest winien”. Opis krokowy (jak przy podziale problemu na części) brzmi: dla każdej osoby zsumuj to, co zapłaciła, odejmij jej równy udział i wypisz wynik. Z tego wychodzi jedna mała [[funkcja]]:

```python
def saldo_osoby(wydatki, osoba, liczba_osob):
    # ile osoba zapłaciła minus jej równy udział
    ...
```

Funkcję sprawdzasz na danych, których wynik znasz z kartki. Dopiero gdy się zgadza, zapisujesz [[commit]] (zapisaną wersję kodu z opisem) i myślisz o kolejnym kawałku, np. wczytaniu wydatków z pliku.

Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, o którym była mowa przy [[sec-09-po-co-zapisywac-wersje-kodu|zapisywaniu wersji kodu]]. Za chwilę zrobisz to u siebie, w warsztacie.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "detail": "Przykład funkcji ma tylko `...` i brak przykładowych danych. Czytelnik nie widzi, jak „sprawdzasz na danych z kartki”. Można w komentarzu dodać np. wydatki: Ania 60, Bartek 0, Celina 30 → saldo Ani +20 (3 osoby, udział 30), bez wydłużania sekcji.",
      "severity": "sugestia",
      "target": "saldo_osoby / sprawdzenie na danych z kartki"
    }
  ]
}
````
