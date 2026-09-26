# Krok 0968 · znudzony_czytelnik

Węzeł: `review` · dział: 9 · pytanie: 50 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Czym różni się błąd składni od błędu logicznego?".

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
## Po co sprawdzać dane użytkownika
Program powinien sprawdzać dane od użytkownika, bo człowiek potrafi wpisać coś, czego kod się nie spodziewał, a wtedy program albo się zatrzyma, albo policzy coś błędnego.

Ta kontrola to [[walidacja-danych|walidacja]]: sprawdzenie, czy wpisana wartość nadaje się do dalszej pracy, zanim program jej użyje. Pamiętasz, że [[input|input]] zawsze zwraca tekst. Gdy ktoś na pytanie „Ile zapłacił?” wpisze `abc`, samo `float("abc")` przerwie program komunikatem o błędzie. A gdy wpisze `-5`, program nie zgłosi żadnego błędu i po cichu policzy złe saldo.

Dlatego sprawdzamy dane w miejscu, gdzie wchodzą do programu. Pokazuje to funkcja `sprawdz_kwote`, która odpowiada `True` albo `False`:

```python
def sprawdz_kwote(tekst):
    if not tekst.replace(".", "", 1).isdigit():
        return False
    return float(tekst) > 0

for tekst in ["45.5", "abc", "-5", "0", ""]:
    print(repr(tekst), sprawdz_kwote(tekst))
```

```text
'45.5' True
'abc' False
'-5' False
'0' False
'' False
```

Pierwsza linia sprawdza, czy tekst składa się z cyfr (z najwyżej jedną kropką). Druga dopiero wtedy zamienia go na liczbę i pyta, czy jest dodatnia.

Konsekwencja: zły wpis nie kończy programu, tylko dostaje komunikat i kolejną szansę. Program, który sprawdza dane, jest odporny na pomyłki, a Ty masz pewność, że reszta kodu dostaje wartości, na które jest przygotowana.

NOWA SEKCJA "Błąd składni a błąd logiczny":
Błąd składni łamie zasady zapisu, więc Python zatrzymuje się, zanim cokolwiek wykona. Błąd logiczny ma zapis poprawny, ale robi coś innego, niż zamierzałeś, więc program działa i po cichu podaje zły wynik.

[[blad-skladni|Błąd składni]] to naruszenie [[skladnia|składni]] języka, czyli reguł zapisu: brakujący dwukropek po `if`, niedomknięty cudzysłów, źle wcięta linia. Python czyta cały plik przed startem i takiego zapisu nie rozumie, więc nie wykona nawet linii przed błędem. Komunikat wskazuje linię i miejsce.

[[blad-logiczny|Błąd logiczny]] to pomyłka w pomyśle: zły wzór, zły dzielnik, zły warunek. Python nie ma jak jej zauważyć, bo każda instrukcja jest poprawna. Widzisz go tylko wtedy, gdy porównasz wynik z tym, czego się spodziewałeś.

| | Błąd składni | Błąd logiczny |
|---|---|---|
| Kiedy wychodzi | przed startem programu | w trakcie i po nim |
| Komunikat | jest, ze wskazaną linią | brak |
| Kto go znajduje | Python | Ty |

Trzy osoby dzielą wydatki 45.5, 20 i 12.5 zł:

```python
suma = 45.5 + 20 + 12.5
print("Na osobę:", suma / 2)
```

```text
Na osobę: 39.0
```

Program nie zgłasza żadnego problemu, a wynik jest zły: powinno być 26.0, bo osoby są trzy. Podobnie działał zły wpis `-5` z poprzedniej sekcji: brak komunikatu, zły wynik. Konsekwencja: błędy składni są uciążliwe, ale łatwe, bo Python je wskaże. Za błędy logiczne odpowiadasz Ty, dlatego wynik zawsze sprawdzaj z rachunkiem na kartce. Jak czytać komunikaty i szukać takich błędów, omówimy osobno, w dalszych sekcjach tego działu.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Błąd logiczny ma pełny przykład (kod i wynik), a błąd składni tylko wyliczankę w prozie. Nie widzę, jak wygląda zły zapis ani komunikat Pythona ze wskazaną linią. Twierdzenie, że Python nie wykona nawet linii przed błędem, jest nieprzekonujące bez pokazania. Wystarczy 2–3 linie, np. `print(\"start\")` i `if suma > 10` bez dwukropka, do tego wynik `text` z komunikatem, w którym nie ma wypisanego „start”. Żeby zmieścić się w limicie, można skrócić tabelę albo powtórzenie w pierwszym akapicie.",
      "target": "Błąd składni",
      "severity": "blokująca"
    }
  ]
}
````
