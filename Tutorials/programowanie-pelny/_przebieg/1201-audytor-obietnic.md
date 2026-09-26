# Krok 1201 · audytor_obietnic

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem obietnic w tutorialu: Programowanie od podstaw. Wcześniej w tekście padła obietnica:
„U siebie zobaczysz to za chwilę” (błąd TypeError we własnym pliku czytelnika).
Czy ta sekcja ją spełnia? reference_id="ref-51", status spełniona | częściowo | brak, section_id="sec-09-jak-czytac-komunikat-o-bledzie",
quote = dokładny cytat (5-15 słów) z sekcji, który ją spełnia, explanation krótko.

SEKCJA [sec-09-jak-czytac-komunikat-o-bledzie] "Jak czytać komunikat o błędzie":
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
````

## Odpowiedź

````json
{
  "reference_id": "ref-51",
  "status": "brak",
  "section_id": "sec-09-jak-czytac-komunikat-o-bledzie",
  "explanation": "Sekcja pokazuje tylko przykład ZeroDivisionError z cudzą ścieżką (/home/ania/...). Nie ma w niej TypeError ani prośby, by czytelnik wywołał błąd we własnym pliku i go zobaczył. Uwaga „Ścieżka u Ciebie będzie inna” dotyczy ścieżki, a nie takiego ćwiczenia."
}
````
