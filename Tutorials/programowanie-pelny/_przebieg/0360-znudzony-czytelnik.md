# Krok 0360 · znudzony_czytelnik

Węzeł: `review` · dział: 4 · pytanie: 21 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Jak można porównać zmienną do pudełka z etykietą?".

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
## Czym jest zmienna
[[zmienna|Zmienna]] to nazwane miejsce w pamięci programu, w którym leży jedna [[dana|dana]]. Dzięki nazwie możesz tę daną wielokrotnie odczytać, użyć w obliczeniach albo zastąpić inną.

Pamiętasz, że dane trzeba gdzieś przechowywać, żeby użyć ich więcej niż raz. Właśnie do tego służy zmienna. Zamiast wpisywać `45.5` w kilku miejscach, nadajesz kwocie nazwę i posługujesz się nią. To trochę jak komórka w arkuszu, którą nazwałeś „kwota”, a potem odwołujesz się do niej po nazwie.

```python
imie = "Ania"
kwota = 45.5
zaplacono = True
print(imie, kwota, zaplacono)
kwota = 60
print(kwota + 10)
```

```text
Ania 45.5 True
70
```

Znak `=` nie oznacza tu „równa się” jak w matematyce. Znaczy: „zapisz to, co po prawej, pod nazwą po lewej”. Dokładniej opiszemy to przy przypisaniu.

Wartość zmiennej może się zmieniać w trakcie działania programu, stąd nazwa: po `kwota = 60` stara kwota znika, a nowa zajmuje jej miejsce. Nazwa zostaje ta sama. W „Wspólnej Kasie” takie zmienne w `rozlicz.py` opisują pojedynczy wydatek: kto zapłacił, ile i czy już się rozliczył.

NOWA SEKCJA "Zmienna jako pudełko z etykietą":
[[zmienna|Zmienną]] można porównać do pudełka z etykietą: etykieta to nazwa, a w środku leży jedna [[dana|dana]], czyli [[wartosc-zmiennej|wartość zmiennej]] (to, co aktualnie jest w pudełku). Program szuka pudełka po etykiecie i zagląda do środka.

```text
etykieta: kwota      etykieta: imie
┌──────────┐         ┌──────────┐
│   45.5   │         │  "Ania"  │
└──────────┘         └──────────┘
```

Porównanie tłumaczy trzy rzeczy. Pudełko mieści jedną wartość naraz, więc nowa wartość wypiera starą, jak w przypadku zmiany kwoty z poprzedniej sekcji. Etykieta zostaje, zmienia się tylko zawartość. Wreszcie każde pudełko żyje własnym życiem: kopia wartości do drugiego pudełka nie łączy ich na stałe.

```python
# poza kanonem
kwota_stara = 45.5
kwota = kwota_stara
kwota = 60
print(kwota_stara, kwota)
```

```text
45.5 60
```

Zmiana `kwota` nie ruszyła `kwota_stara`, bo do drugiego pudełka trafiła kopia wartości.

Obraz jest uproszczony: pod spodem Python działa nieco inaczej, ale na tym etapie to nie ma znaczenia. Ważna konsekwencja: etykieta ma być czytelna. W „Wspólnej Kasie” pudełko `kwota` jest zrozumiałe, a `x` zmusza do zgadywania, co w środku.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "tempo",
      "severity": "sugestia",
      "target": "akapit „Porównanie tłumaczy trzy rzeczy”",
      "detail": "Nadpisywanie wartości i stała nazwa były już w poprzedniej sekcji („stara kwota znika, a nowa zajmuje jej miejsce”). Nowe jest głównie to, że kopia jest niezależna. Warto skrócić powtórkę i położyć nacisk na kopiowanie.",
      "source": "poprzednia sekcja"
    },
    {
      "kind": "konkret",
      "severity": "sugestia",
      "target": "zdanie „Obraz jest uproszczony… Ważna konsekwencja”",
      "detail": "„Pod spodem Python działa nieco inaczej” jest ogólnikiem. Wniosek o czytelnej etykiecie nie wynika z porównania z pudełkiem. Można go połączyć z jednym konkretnym przykładem, np. `kwota` kontra `x`, albo pominąć.",
      "source": ""
    }
  ]
}
````
