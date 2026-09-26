# Krok 1197 · audytor_obietnic

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem obietnic w tutorialu: Programowanie od podstaw. Wcześniej w tekście padła obietnica:
„Na razie nie piszemy kodu” (zapowiedź, że kod pojawi się w dalszych działach).
Czy ta sekcja ją spełnia? reference_id="ref-16", status spełniona | częściowo | brak, section_id="sec-03-czym-jest-kod-zrodlowy",
quote = dokładny cytat (5-15 słów) z sekcji, który ją spełnia, explanation krótko.

SEKCJA [sec-03-czym-jest-kod-zrodlowy] "Czym jest kod źródłowy":
[[kod-zrodlowy|Kod źródłowy]] to tekst programu zapisany w [[jezyk-programowania|języku programowania]], który czyta i pisze człowiek. To „źródło”, z którego komputer dopiero dostaje coś do wykonania.

Fizycznie kod źródłowy jest zwykłym plikiem tekstowym, tak jak notatka czy lista zakupów. Różnica polega na treści: każda linia to [[instrukcja|instrukcja]] zapisana według ścisłych reguł [[skladnia|składni]]. Ten sam [[algorytm|algorytm]], który wcześniej opisywaliśmy słowami i schematem, tu dostaje zapis, którego nie da się zrozumieć na dwa sposoby.

Kod źródłowy zapisujemy w pliku o rozszerzeniu zależnym od języka. Pliki Pythona kończą się na `.py`. Taki plik będzie miał nasz przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Zaczyna się od pliku `rozlicz.py`:

```python
# rozlicz.py
print("Wspólna Kasa")
print(300 / 3)
```

```text
Wspólna Kasa
100.0
```

Plik sam niczego nie robi. Dopiero osobny program czyta go i wykonuje linia po linii, a jak to działa, pokażemy przy uruchamianiu programu.

Konsekwencja: kod źródłowy możesz otworzyć, przeczytać i poprawić w każdym edytorze tekstu. Dlatego to on jest tym, co programista naprawdę tworzy i zmienia.
````

## Odpowiedź

````json
{
  "reference_id": "ref-16",
  "status": "spełniona",
  "section_id": "sec-03-czym-jest-kod-zrodlowy",
  "quote": "Zaczyna się od pliku `rozlicz.py`:",
  "explanation": "Sekcja pokazuje pierwszy prawdziwy kod tutorialu, czyli plik rozlicz.py z dwiema liniami print i jego wynik. Tym samym kończy etap „nie piszemy kodu”. Zapowiedź, że kod pojawi się dalej, została zrealizowana."
}
````
