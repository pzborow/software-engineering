# Krok 0016 · weryfikator_dodatków

Węzeł: `layers` · dział: 1 · pytanie: 1 · próba: —

## Prompt

````text
Jesteś weryfikatorem dodatków w tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT.
Sprawdź każdy dodatek (dygresję, żart, pomysł na ilustrację) do sekcji poniżej:
1. Logika: czy puenta, porównanie albo scena mają sens i są wewnętrznie spójne (np. żart mówi o literówce,
   a w jego przykładzie żadnej literówki nie ma, to błąd).
2. Zgodność z sekcją: czy dodatek naprawdę dotyczy tego, co sekcja mówi, i nie przeczy jej.
3. Fakty: daty, nazwiska, historie. Odrzuć, jeśli fakt jest błędny albo nie masz pewności, że jest prawdziwy.
4. Ton: bez żartów z ludzi i grup.
5. Rejestr: dodatek, który powtarza temat, puentę albo motyw wcześniejszego wpisu z zakazem powtórzeń, jest błędny;
   nawiązanie do wcześniejszego wpisu jest dobre tylko wtedy, gdy zgadza się z pierwowzorem.
6. Źródła: dodatek oznaczony [źródło wymagane] musi mieć źródło, które faktycznie otworzysz (WebFetch) i które
   potwierdza jego twierdzenia. Potwierdzone źródło podaj w source (title, url, supports). Bez potwierdzenia: ok=false.
Dla każdego podaj index, ok i przy ok=false jednozdaniowe problem.


DODATKI:
0. [wtręty] Marta prosi komputer o „sprawiedliwy” podział: Marta napisała w pierwszej wersji programu: „podziel koszty sprawiedliwie”. Komputer nie zgadł, co ona ma na myśli: nie wiedział, czy sprawiedliwie to po równo, czy według tego, kto ile zjadł. Dopiero gdy zamieniła to na jednoznaczne kroki (zsumuj wydatki, podziel przez liczbę osób, odejmij to, co kto już zapłacił), dostała wynik.
1. [dygresje] [źródło wymagane] Pierwszy program powstał przed komputerami: W 1843 roku Ada Lovelace opublikowała notatki do opisu Maszyny Analitycznej Charlesa Babbage'a. Zawierały one rozpisany krok po kroku sposób obliczania liczb Bernoulliego, uznawany przez wielu za pierwszy opublikowany program komputerowy. Maszyna nigdy nie została zbudowana, więc ten program nie mógł być wtedy uruchomiony. (źródło autora: Ada Lovelace – Britannica, https://www.britannica.com/biography/Ada-Lovelace)

SEKCJA "Czym jest program komputerowy":
[[program-komputerowy|Program komputerowy]] to zapisany z góry ciąg poleceń, które komputer wykonuje krok po kroku, żeby zamienić dane na wynik. Komputer sam nic nie wie ani nie zgaduje: robi dokładnie to, co mu zapisano.

Pojedyncze polecenie to [[instrukcja|instrukcja]], czyli jeden mały, jednoznaczny krok, np. „dodaj dwie liczby” albo „wypisz tekst na ekranie”. Program to wiele takich instrukcji ułożonych w określonej kolejności. Kalkulator, przeglądarka i gra działają tak samo, tylko mają instrukcji bardzo dużo.

Prosty schemat każdego programu wygląda tak:

```text
dane na wejściu  -->  program (instrukcje)  -->  wynik na wyjściu
```

Weźmy przykład, który będzie nam towarzyszył: „Wspólna Kasa”. Na wyjeździe czworo znajomych płaci na zmianę za jedzenie, paliwo i nocleg. Na koniec trzeba ustalić, kto komu ile jest winien. W arkuszu robisz to ręcznie: wpisujesz kwoty, sumujesz, dzielisz, odejmujesz, a przy każdym nowym wyjeździe zaczynasz od nowa.

Program „Wspólna Kasa” zrobi to za ciebie. Na wejściu dostanie listę wydatków (kto zapłacił i ile), a na wyjściu poda rozliczenie. Napisze go [[programista|programista]], czyli osoba, która zamienia potrzebę na instrukcje zrozumiałe dla komputera. Na razie nie piszemy kodu; ważne, że raz zapisane instrukcje można uruchamiać bez końca.
````

## Odpowiedź

````json
{
  "verdicts": [
    {
      "index": 0,
      "ok": true,
      "problem": ""
    },
    {
      "index": 1,
      "ok": true,
      "problem": "",
      "source": {
        "title": "Ada Lovelace – Wikipedia",
        "url": "https://en.wikipedia.org/wiki/Ada_Lovelace",
        "supports": "Notatki opublikowane we wrześniu 1843, Note G z metodą liczenia liczb Bernoulliego, często nazywana pierwszym opublikowanym programem; maszyna nigdy nie została ukończona, więc program nie został przetestowany."
      }
    }
  ]
}
````
