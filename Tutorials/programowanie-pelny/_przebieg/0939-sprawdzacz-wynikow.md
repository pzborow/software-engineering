# Krok 0939 · sprawdzacz_wyników

Węzeł: `review` · dział: 8 · pytanie: 48 · próba: 1

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

SEKCJA "Czym jest interfejs użytkownika":
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
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
