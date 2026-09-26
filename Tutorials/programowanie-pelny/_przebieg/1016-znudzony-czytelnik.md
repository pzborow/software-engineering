# Krok 1016 · znudzony_czytelnik

Węzeł: `review` · dział: 9 · pytanie: 52 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym jest testowanie programu?".

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
## Jak czytać komunikat o błędzie
Czytaj komunikat od dołu: ostatnia linia mówi, co poszło nie tak, a linie nad nią pokazują, gdzie to się stało. Komunikat nie jest wyrokiem, tylko wskazówką.

Gdy program zatrzyma się w trakcie pracy, Python wypisuje [[traceback|Traceback]], czyli ślad wywołań: listę miejsc w kodzie, przez które przeszło wykonanie aż do błędu. Wszystko razem to [[komunikat-o-bledzie|komunikat o błędzie]], czyli tekst, w którym Python opisuje, co go zatrzymało i w którym miejscu. Dzielimy przez zero:

```python
# blad_pusta.py - Traceback: dzielenie przez zero
def na_osobe(suma, osoby):
    return suma / osoby

print("Start")
print(na_osobe(0, 0))
```

```text
Start
Traceback (most recent call last):
  File "/home/ania/wspolna_kasa/blad_pusta.py", line 6, in <module>
    print(na_osobe(0, 0))
          ~~~~~~~~^^^^^^
  File "/home/ania/wspolna_kasa/blad_pusta.py", line 3, in na_osobe
    return suma / osoby
           ~~~~~^~~~~~~
ZeroDivisionError: division by zero
```

(Ścieżka u Ciebie będzie inna, bo zależy od miejsca pliku.)

Ostatnia linia ma dwie części: nazwę błędu (`ZeroDivisionError`, dzielenie przez zero) i opis (`division by zero`). Wyżej stoją pary „plik, linia, funkcja” i przepisana linia kodu. Ostatnia para jest miejscem, w którym Python się potknął, a wyższe pokazują, kto tę funkcję wywołał. Znaki `^` i `~` wskazują fragment linii.

Inaczej niż przy błędzie składni ze „Startem”, który się nie pojawił, tu „Start” się wypisał, bo program ruszył i padł dopiero w środku.

Konsekwencja: nie bój się czerwonego tekstu. Przeczytaj ostatnią linię, znajdź w śladzie własny plik i numer linii, a zwykle już wiesz, gdzie szukać. Szukanie przyczyny krok po kroku omówimy przy debugowaniu.

NOWA SEKCJA "Czym jest testowanie programu":
[[testowanie|Testowanie]] to systematyczne sprawdzanie programu na wielu danych, dla których z góry znasz poprawny wynik. Zamiast raz spojrzeć na ekran i uznać, że „wygląda dobrze”, zapisujesz oczekiwania i pozwalasz komputerowi je porównać.

Najprostszy test to jedno sprawdzenie małej funkcji. W Pythonie służy do tego [[assert|assert]]: instrukcja, która nic nie robi, gdy warunek jest prawdziwy, a zatrzymuje program błędem `AssertionError`, gdy jest fałszywy.

```python
def na_osobe(suma, osoby):
    return suma / osoby

assert na_osobe(78, 3) == 26
assert na_osobe(0, 4) == 0
assert na_osobe(100, 4) == 25
print("Wszystkie testy przeszły")
```

```text
Wszystkie testy przeszły
```

Cisza po `assert` znaczy „zgadza się”. Gdyby ktoś zmienił dzielenie tak, że wynik byłby zły, jak przy błędzie z niewłaściwym dzielnikiem, pierwszy test zatrzymałby program i wskazał linię, w której oczekiwanie przestało być prawdą.

Dobre testy obejmują zwykłe dane i przypadki brzegowe, np. pustą listę wydatków. Kosztują chwilę, a po każdej zmianie kodu uruchamiasz je jednym poleceniem i wiesz, czy niczego nie zepsułeś.

Test nie dowodzi, że błędów nie ma, tylko że w sprawdzonych przypadkach ich nie ma. Gdy test się wywali, szukanie przyczyny omówimy przy debugowaniu.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "konkret",
      "severity": "sugestia",
      "target": "przypadki brzegowe, pusta lista wydatków",
      "detail": "Przypadek brzegowy jest tylko wspomniany, a przykład (lista wydatków) nie pasuje do funkcji na_osobe, która listy nie przyjmuje. Lepiej wskazać brzeg z kodu: na_osobe(0, 0) z poprzedniej sekcji kończy się ZeroDivisionError, więc test pokazałby ten brzeg. Jedno zdanie wystarczy.",
      "source": "Dobre testy obejmują zwykłe dane i przypadki brzegowe"
    },
    {
      "kind": "odwołanie",
      "severity": "sugestia",
      "target": "jak przy błędzie z niewłaściwym dzielnikiem",
      "detail": "Odwołanie do błędu, którego czytelnik nie widział (poprzednia sekcja pokazywała dzielenie przez zero). Należy je zastąpić konkretem, np. „gdyby ktoś zamienił / na *”, albo odnieść się do dzielenia przez zero.",
      "source": "Gdyby ktoś zmienił dzielenie tak, że wynik byłby zły"
    }
  ]
}
````
