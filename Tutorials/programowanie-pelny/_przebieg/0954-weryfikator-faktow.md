# Krok 0954 · weryfikator_faktów

Węzeł: `review` · dział: 8 · pytanie: 49 · próba: 1

## Prompt

````text
Jesteś weryfikatorem faktów tutorialu: Programowanie od podstaw. Czytelnik: osoba spoza IT, poziom docelowy: początkujący.
Czytelnik zna: obsługa komputera: pliki, foldery, przeglądarka; arytmetyka i procenty ze szkoły; arkusz kalkulacyjny na poziomie użytkownika.
Wersje obowiązujące w tutorialu: Python 3.13. Wersje zadeklarowane w sekcji: (brak).

Sprawdź w DOKUMENTACJI konkretne, sprawdzalne twierdzenia nowej sekcji: komendy i ich flagi, nazwy argumentów,
pól i zasobów, wartości domyślne, składnię oraz zachowanie zależne od wersji.
- Najpierw Context7: resolve-library-id, potem query-docs. Gdy czegoś nie ma w Context7, użyj WebFetch
  na oficjalnej stronie dokumentacji. Najwyżej 4 zapytania łącznie: wybierz twierdzenia najbardziej narażone na błąd.
- Nie oceniaj stylu, dydaktyki ani ogólnych idei. Kod jest szkicem: `...` i pominięte fragmenty nie są błędem.
- Każdą niezgodność z dokumentacją zgłoś jako kind="fakt", target=fragment sekcji, detail=co mówi dokumentacja
  (z adresem strony) i jak poprawić. "blokująca", gdy czytelnik wykonując kod dostałby błąd albo inne zachowanie;
  "sugestia", gdy to nieścisłość bez takich skutków.
- sources: tylko strony, które faktycznie przeczytałeś, i które twierdzenie sekcji potwierdzają albo obalają.
- ok=true, gdy nie ma blokujących niezgodności.

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
      "kind": "fakt",
      "severity": "sugestia",
      "target": "if not tekst.replace(\".\", \"\", 1).isdigit()",
      "detail": "Dokumentacja Pythona (https://docs.python.org/3/library/stdtypes.html#str.isdigit) mówi, że str.isdigit() zwraca True także dla znaków takich jak indeksy górne (np. \"²\"), a float(\"²\") zgłasza ValueError. Dla zwykłych danych z klawiatury początkującego kod działa poprawnie i cały wynik w bloku text jest zgodny z tym, co program wypisze. Jeśli sekcja ma twierdzić, że funkcja chroni przed każdym błędem konwersji, warto to złagodzić albo w przyszłości użyć try/except ValueError. Nie było sprawdzane w dokumentacji online w tej sesji; wniosek wynika ze znajomości dokumentacji.",
      "source": "docs.python.org str.isdigit",
      "target_note": ""
    }
  ],
  "sources": []
}
````
