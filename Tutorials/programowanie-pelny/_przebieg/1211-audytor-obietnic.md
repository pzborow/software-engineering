# Krok 1211 · audytor_obietnic

Węzeł: `settle_promises` · dział: — · pytanie: — · próba: —

## Prompt

````text
Jesteś audytorem obietnic w tutorialu: Programowanie od podstaw. Wcześniej w tekście padła obietnica:
„pokażemy w ćwiczeniu praktycznym” (praktyczne użycie Git na własnym komputerze).
Czy ta sekcja ją spełnia? reference_id="ref-124", status spełniona | częściowo | brak, section_id="sec-10-od-pomyslu-do-dzialajacego-programu",
quote = dokładny cytat (5-15 słów) z sekcji, który ją spełnia, explanation krótko.

SEKCJA [sec-10-od-pomyslu-do-dzialajacego-programu] "Od pomysłu do działającego programu":
Od pomysłu do programu dochodzi się małymi krokami: opisujesz zadanie zwykłymi słowami, piszesz najmniejszy kawałek, który coś robi, sprawdzasz go i dopiero wtedy dokładasz następny. Cały program naraz zwykle nie działa, a szukanie błędu w stu liniach jest męczące.

```text
pomysł → opis krokowy → mały kawałek kodu → uruchomienie → sprawdzenie → commit
              ↑                                                            |
              └──────────────────── następny kawałek ←─────────────────────┘
```

Weźmy pomysł: „chcę wiedzieć, kto komu ile jest winien”. Opis krokowy to rozbicie zadania na kroki, z których każdy da się zrobić osobno: dla każdej osoby zsumuj to, co zapłaciła, odejmij jej równy udział i wypisz wynik. Z tego wychodzi jedna mała [[funkcja]]:

```python
def saldo_osoby(wydatki, kto, liczba_osob):
    # ile zapłacił kto minus jego równy udział
    ...
```

Funkcję sprawdzasz na danych, których wynik znasz z kartki. Dopiero gdy się zgadza, zapisujesz [[commit]] (zapisaną wersję kodu z opisem) i myślisz o kolejnym kawałku, np. wczytaniu wydatków z pliku.

Każdy krok jest na tyle mały, że wiesz, co miało się stać. Jeśli coś się nie zgadza, winna jest ostatnia zmiana, a poprzedni commit czeka jako działający punkt powrotu, jak w sekcji o zapisywaniu wersji kodu. Dzięki temu nie zgadujesz, gdzie szukać błędu.
````

## Odpowiedź

````json
{
  "reference_id": "ref-124",
  "status": "brak",
  "section_id": "sec-10-od-pomyslu-do-dzialajacego-programu",
  "explanation": "Sekcja wspomina commit tylko jako element cyklu pracy i definiuje go jednym zdaniem. Nie ma w niej ćwiczenia praktycznego z Git na własnym komputerze: brak poleceń (git init, add, commit) i kroków do wykonania. Odsyła też do innej sekcji o zapisywaniu wersji kodu."
}
````
