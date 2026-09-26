# Krok 1209 · audytor_obietnic

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem obietnic w tutorialu: Programowanie od podstaw. Wcześniej w tekście padła obietnica:
„Usuwamy ją w warsztacie poniżej.” (zapowiedź poprawienia błędnej ostatniej linii w warsztacie).
Czy ta sekcja ją spełnia? reference_id="ref-102", status spełniona | częściowo | brak, section_id="sec-09-czym-jest-debugowanie",
quote = dokładny cytat (5-15 słów) z sekcji, który ją spełnia, explanation krótko.

SEKCJA [sec-09-czym-jest-debugowanie] "Czym jest debugowanie":
[[debugowanie|Debugowanie]] to szukanie przyczyny błędu i jej usuwanie. Nie polega na zgadywaniu, tylko na sprawdzaniu, co program faktycznie robi w kolejnych krokach.

Metoda jest prosta. Najpierw odtwarzasz błąd na jednych, konkretnych danych. Potem zawężasz miejsce: przed podejrzanym krokiem wypisujesz wartości i porównujesz je z tym, czego oczekujesz. Pierwsze miejsce, w którym wartość jest inna niż powinna, wskazuje przyczynę. Na końcu poprawiasz jedną rzecz i uruchamiasz ponownie.

Weźmy [[blad-logiczny|błąd logiczny]] z wynikiem 39.0 zamiast 26.0. Podejrzewamy dwa dane wejściowe dzielenia, więc je wypisujemy:

```python
def na_osobe(suma, osoby):
    return suma / osoby

suma = 78.0
liczba_osob = 2
print("DEBUG suma:", suma)
print("DEBUG liczba_osob:", liczba_osob)
print(na_osobe(suma, liczba_osob))
```

```text
DEBUG suma: 78.0
DEBUG liczba_osob: 2
39.0
```

Suma się zgadza, a liczba osób nie: mają być trzy. Funkcja jest w porządku, błąd siedzi w danych, które jej podajemy. Bez wypisania szukalibyśmy pewnie w dzieleniu.

Gdy test z poprzedniej sekcji zgłosi błąd, zaczynasz tak samo: odtwarzasz przypadek, który go wywołał, i patrzysz na wartości. Po naprawie usuń linie z `DEBUG`, żeby nie zaśmiecały wyniku.
````

## Odpowiedź

````json
{
  "reference_id": "ref-102",
  "status": "brak",
  "section_id": "sec-09-czym-jest-debugowanie",
  "explanation": "Sekcja nie zawiera warsztatu ani poprawienia błędnej ostatniej linii w warsztacie. Pokazuje tylko diagnozę na przykładzie (błędna liczba osób) i radę, by po naprawie usunąć linie DEBUG. Obietnica pozostaje niespełniona i musi być zrealizowana w warsztacie."
}
````
