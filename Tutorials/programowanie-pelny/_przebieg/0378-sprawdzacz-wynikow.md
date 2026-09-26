# Krok 0378 · sprawdzacz_wyników

Węzeł: `review` · dział: 4 · pytanie: 22 · próba: 1

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

SEKCJA "Liczba a tekst":
Liczba to wartość, na której program liczy. Tekst to ciąg znaków, który program tylko przechowuje, wypisuje i porównuje. Zapis decyduje o tym, z czym mamy do czynienia: `45.5` bez cudzysłowu to liczba, a `"45.5"` w cudzysłowie to tekst, czyli cztery znaki: 4, 5, kropka, 5.

| Zapis | Co to jest | Można dzielić? |
|---|---|---|
| `45.5` | liczba | tak |
| `"45.5"` | tekst | nie |
| `"Ania"` | tekst | nie |

W programie ułamek dziesiętny zapisujemy z kropką, nie z przecinkiem, tak jak `kwota = 45.5` w „Wspólnej Kasie”.

```python
kwota = 45.5
imie = "Ania"
print(kwota / 2)
print(imie)
```

```text
22.75
Ania
```

Liczbę można dzielić, mnożyć i dodawać. Tekstu nie: to ta sama myśl co [[imienia nie da się podzielić|imię „Ania” nie do podzielenia przez 2]]. Python zatrzyma się z komunikatem `TypeError`. U siebie zobaczysz to za chwilę w `kasa.py`.

Konsekwencja: kwotę zapisaną w cudzysłowie program potraktuje jak napis, nie jak pieniądze. Nazwę tej cechy danych, czyli typ, omówimy w następnej sekcji.
````

## Odpowiedź

````json
{
  "ok": false,
  "needs": [
    {
      "kind": "fakt",
      "severity": "blokująca",
      "target": "Liczbę można dzielić, mnożyć i dodawać. Tekstu nie",
      "detail": "Zdanie sugeruje, że tekstu nie da się dodawać ani mnożyć, a w Pythonie się da: \"Ania\" + \"Kasia\" skleja teksty, a \"Ha\" * 3 daje \"HaHaHa\". Trzeba zawęzić twierdzenie do dzielenia albo do liczenia na wartościach, np. „Liczbę można dzielić. Tekstu nie: \"Ania\" / 2 kończy się błędem TypeError”. Ta sama nieścisłość jest w zdaniu „program tylko przechowuje, wypisuje i porównuje”, bo tekst można też sklejać. Sugerowana poprawka: dopisać „i skleja”, albo pominąć dodawanie.",
      "source": "sekcja Liczba a tekst"
    },
    {
      "kind": "odwołanie",
      "severity": "sugestia",
      "target": "[[imienia nie da się podzielić|imię „Ania” nie do podzielenia przez 2]]",
      "detail": "Zdanie „to ta sama myśl co …” jest niezgrabne, a etykieta odwołania jest po polsku nieprawidłowa („nie do podzielenia przez 2”). Lepiej: „tak jak imienia „Ania” nie da się podzielić przez 2”.",
      "source": "sekcja Liczba a tekst"
    },
    {
      "kind": "przykład",
      "severity": "sugestia",
      "target": "Tekstu nie [można dzielić]",
      "detail": "Teza, że tekstu nie da się dzielić, nie ma tu własnego przykładu kodu z błędem. Tekst odsyła do późniejszego kasa.py. Warto dać jedną linię, np. print(\"Ania\" / 2), i wskazać, że kończy się TypeError.",
      "source": "sekcja Liczba a tekst"
    }
  ]
}
````
