# Krok 0949 · znudzony_czytelnik

Węzeł: `review` · dział: 8 · pytanie: 49 · próba: 1

## Prompt

````text
Jesteś znudzonym, ale ambitnym czytelnikiem. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Czytasz tutorial liniowo. Oceń TYLKO nową sekcję, która odpowiada na pytanie: "Dlaczego program powinien sprawdzać dane wpisane przez użytkownika?".

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
## Czym jest interfejs użytkownika
[[interfejs-uzytkownika|Interfejs użytkownika]] to część programu, przez którą człowiek się z nim komunikuje: to, co program wyświetla, oraz sposób, w jaki przyjmuje od człowieka dane i polecenia. Użytkownik nie widzi kodu, widzi tylko interfejs.

Interfejs bywa różny. W [[interfejs-tekstowy|interfejsie tekstowym]], czyli takim, który działa w [[terminal|terminalu]] na samych napisach, program zadaje pytania, a Ty odpisujesz z klawiatury. W interfejsie graficznym są okna i przyciski. Nasza „Wspólna Kasa” zostaje przy wersji tekstowej, bo wystarczą do niej dwie znane już rzeczy: [[input|input]] do pytań i [[print|print]] do wyników.

Interfejs ma dwie strony: **wejście** (pytania, odpowiedzi) i **wyjście** (wyniki, komunikaty). To dokładnie [[dane-wejsciowe|dane wejściowe]] i [[dane-wyjsciowe|dane wyjściowe]], tylko widziane oczami człowieka. Stąd wniosek z wcześniejszych sekcji: suchy wynik nic nie mówi komuś, kto nie zna kodu, więc trzeba go opisać.

```python
def wypisz_podsumowanie(wydatki):
    print("=== Wspólna Kasa ===")
    for wydatek in wydatki:
        print(f"{wydatek['kto']}: {wydatek['kwota']} zł")

wydatki = [{"kto": "Ania", "opis": "zakupy", "kwota": 120.5},
           {"kto": "Bartek", "opis": "paliwo", "kwota": 45.5}]
wypisz_podsumowanie(wydatki)
```

```text
=== Wspólna Kasa ===
Ania: 120.5 zł
Bartek: 45.5 zł
```

Konsekwencja: pytanie w rodzaju „Ile zapłacił? ” i czytelne podsumowanie to nie ozdoby, tylko część działania programu. Interfejs trzeba więc projektować, a człowiek po drugiej stronie potrafi wpisać coś nieoczekiwanego.

NOWA SEKCJA "Po co sprawdzać dane użytkownika":
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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": [
    {
      "kind": "przykład",
      "detail": "Końcowe zdanie obiecuje, że zły wpis dostaje komunikat i kolejną szansę, ale kod tego nie pokazuje. Pokazuje tylko True/False. Wystarczy zastąpić pętlę testową krótką pętlą while z input(), która pyta ponownie po złym wpisie. Można też dopisać, że pętlę poznamy w następnej sekcji.",
      "severity": "sugestia",
      "source": "Konsekwencja: zły wpis nie kończy programu, tylko dostaje komunikat i kolejną szansę.",
      "target": "zakończenie sekcji"
    }
  ]
}
````
