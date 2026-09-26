# Krok 0972 · sprawdzacz_wyników

Węzeł: `review` · dział: 9 · pytanie: 50 · próba: 1

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

SEKCJA "Błąd składni a błąd logiczny":
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
  "ok": true,
  "needs": []
}
````
