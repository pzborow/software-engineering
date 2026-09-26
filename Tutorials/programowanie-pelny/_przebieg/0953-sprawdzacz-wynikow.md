# Krok 0953 · sprawdzacz_wyników

Węzeł: `review` · dział: 8 · pytanie: 49 · próba: 1

## Prompt

````text
Jesteś sprawdzaczem wyników w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.

Dla każdego bloku kodu, który da się uruchomić samodzielnie (ma wszystkie dane, nie zawiera `...`) i coś wypisuje:
1. Czy bezpośrednio pod nim jest blok ```text z wynikiem? Brak: kind="wynik", severity="blokująca",
   detail = dokładny wynik, który trzeba dopisać.
2. Wykonaj kod w myślach krok po kroku (wartości, obliczenia, zaokrąglenia, formatowanie, kolejność linii)
   i porównaj z podanym wynikiem znak w znak. Niezgodność: kind="wynik", severity="blokująca",
   detail = co się nie zgadza i poprawny wynik.
Szkice (z `...`, bez danych) i bloki bez wypisywania pomiń. ok=true, gdy wszystko się zgadza.

Każdej potrzebie nadaj severity:
- "blokująca": bez poprawki czytelnik nie zrozumie odpowiedzi albo wyniesie błędne przekonanie. Zawsze blokujące są:
  kluczowe pojęcie sekcji bez hasła w glosariuszu i bez definicji w tekście; teza, która jest sednem odpowiedzi
  na pytanie, podana bez żadnego przykładu (kodu, scenariusza albo diagramu); błąd merytoryczny.
- "sugestia": tekst jest zrozumiały, a zmiana tylko by go poprawiła (dodatkowy przykład, zgrabniejsze sformułowanie,
  drobne powtórzenie, detal w kodzie).
Jeśli nie ma nic blokującego, ok=true (sugestie mogą zostać).

SEKCJA "Po co sprawdzać dane użytkownika":
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
      "kind": "wyjaśnienie",
      "detail": "W kodzie jest `repr(tekst)`, a czytelnik spoza IT nie wie, czemu wynik ma apostrofy. Wystarczy jedno zdanie, np. że `repr` pokazuje tekst w apostrofach, dzięki czemu widać także pusty wpis `''`.",
      "severity": "sugestia",
      "target": "repr"
    },
    {
      "kind": "przykład",
      "detail": "Zdanie o złym wpisie, który dostaje komunikat i kolejną szansę, nie ma pokrycia w kodzie. Można dodać krótką pętlę z `input` i `sprawdz_kwote`, która ponawia pytanie.",
      "severity": "sugestia",
      "target": "Konsekwencja"
    }
  ]
}
````
