# Krok 0887 · znudzony_czytelnik

Węzeł: `review` · dział: 8 · pytanie: 46 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak program może zapytać użytkownika o informację?".

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
## Dane wyjściowe programu
[[dane-wyjsciowe|Dane wyjściowe]] to wszystko, co program oddaje na zewnątrz: wynik obliczeń, komunikat, zapisany plik. To druga strona [[dane-wejsciowe|danych wejściowych]]: wejście wpuszcza informacje do programu, wyjście je z niego wypuszcza.

Bez wyjścia program mógłby liczyć, ale nikt by o tym nie wiedział. Wynik zamknięty w zmiennej znika, gdy program się kończy.

Wyjście ma kilka adresatów:

| Dokąd trafia wynik | Przykład we „Wspólnej Kasie” |
|---|---|
| ekran | komunikat „Na osobę wychodzi 26.0” |
| plik | zapisane rozliczenie wyjazdu |
| inny program | dane przekazane do aplikacji banku |

Na razie znasz tylko pierwszą drogę: `print` pokazuje wartość w terminalu. Robiłeś to już w funkcji `wypisz_na_osobe`, o której mówiliśmy przy zwracaniu wyniku (przypomnienie: `print` tylko pokazuje tekst, niczego nie zwraca).

```python
def wypisz_na_osobe(suma, osoby):
    print(suma / osoby)

wypisz_na_osobe(78, 3)
```

```text
26.0
```

Konsekwencja: o tym, co program wypisze, decydujesz Ty. Suchy wynik „26.0” nic nie mówi komuś, kto nie zna kodu, więc dobre wyjście ma opis i jednostkę. Do plików wrócimy osobno, a wygląd całej rozmowy z użytkownikiem opiszemy przy interfejsie.

NOWA SEKCJA "Pytanie użytkownika o informację":
Program pyta użytkownika funkcją [[input|input]]: wypisuje pytanie, czeka, aż ktoś wpisze odpowiedź i naciśnie Enter, a potem oddaje tę odpowiedź jako wartość. To najprostszy sposób, by [[dane-wejsciowe|dane wejściowe]] przyszły od człowieka.

Tekst w nawiasach to pytanie, które zobaczy użytkownik. Wynik `input` przypisujesz do zmiennej, jak każdą [[wartosc-zwracana|wartość zwracaną]]. Program stoi w miejscu, dopóki odpowiedź nie nadejdzie. To pierwsze z pytań do użytkownika, jakie dobudowujemy do „Wspólnej Kasy”:

```python
def zapytaj_o_wydatek():
    kto = input("Kto zapłacił? ")
    kwota = input("Ile zapłacił? ")
    kwota = float(kwota)
    ...
```

Pułapka: `input` zawsze zwraca tekst, nawet gdy ktoś wpisze `45.5`. Dla Pythona to wciąż „45.5” w cudzysłowie, czyli tekst, którego nie da się dzielić ani dodawać do liczb (skończyłoby się to błędem `TypeError`). Dlatego `float()` zamienia tekst na liczbę.

Spacja na końcu pytania jest celowa: oddziela pytanie od tego, co wpisze użytkownik.

Konsekwencja: kod zostaje ten sam, a odpowiedzi zmieniają się przy każdym uruchomieniu. Ale `float("abc")` przerwie program błędem. Jak się przed tym bronić, pokażemy, gdy zajmiemy się sprawdzaniem danych wpisanych przez użytkownika.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Kod pokazuje tylko pytania, ale nie widać, jak wygląda rozmowa w terminalu. Krótki blok text z przebiegiem (pytanie, wpisana odpowiedź) uświadomiłby, że program czeka i co widzi użytkownik. Można go zmieścić kosztem kropek '...' w kodzie.",
      "severity": "sugestia",
      "target": "zapytaj_o_wydatek",
      "source": "blok kodu"
    },
    {
      "kind": "konkret",
      "detail": "Kod kończy się na '...' i nie pokazuje, co funkcja robi z odpowiedziami (np. return kto, kwota). Czytelnik nie widzi, jak dane 'przychodzą' do programu.",
      "severity": "sugestia",
      "target": "zapytaj_o_wydatek"
    }
  ]
}
````
