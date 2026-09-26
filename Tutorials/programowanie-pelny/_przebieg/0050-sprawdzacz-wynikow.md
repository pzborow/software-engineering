# Krok 0050 · sprawdzacz_wyników

Węzeł: `review` · dział: 1 · pytanie: 4 · próba: 1

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

SEKCJA "Czym jest język programowania":
[[jezyk-programowania|Język programowania]] to ściśle określony sposób zapisywania [[instrukcja|instrukcji]], który potrafi zrozumieć komputer. Ma własne słowa i reguły zapisu, ale jest o wiele prostszy i bardziej rygorystyczny niż język polski.

Komputer nie wyciąga wniosków z kontekstu. Zdanie „podziel rachunek po równo” człowiek zrozumie od razu, komputer nie. Język programowania wymusza zapis, który ma jedno znaczenie. Zbiór jego reguł nazywamy [[skladnia|składnią]]: mówi ona, jak wolno układać słowa i znaki, żeby powstało poprawne polecenie.

Oto jedna instrukcja w Pythonie, języku, którego użyjemy w tym tutorialu:

```python
print("Cześć, Wspólna Kasa!")
```

```text
Cześć, Wspólna Kasa!
```

Słowo `print` znaczy „wypisz”, a tekst w cudzysłowie to to, co ma się pojawić na ekranie. Gdybyś pominął jeden cudzysłów, komputer odmówiłby wykonania polecenia, bo zapis łamie reguły.

Języków jest bardzo wiele, a każdy ma inną składnię i inne zastosowania. Różnią się zapisem, ale robią to samo: pozwalają opisać kroki, które komputer wykona. Kto pozna zasady jednego, łatwiej nauczy się następnych.

Pythonem zajmiemy się osobno, gdy przejdziemy do pisania „Wspólnej Kasy”.
````

## Odpowiedź

````json
{
  "ok": true,
  "needs": []
}
````
