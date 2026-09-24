# Indeksy i wyszukiwanie

## Opis

Indeksy pomagają odnajdywać dane bez przeglądania całych kolekcji. ArangoDB oferuje różne rodzaje indeksów oraz możliwości wyszukiwania tekstowego. Dobór powinien wynikać z rzeczywistych zapytań i wymagań jakościowych.

## Kluczowe koncepty

- **Indeks** — struktura przyspieszająca określone wyszukiwanie.
- **Indeks unikalny** — wspiera wymaganie niepowtarzalności wartości.
- **Indeks złożony** — obejmuje więcej niż jeden atrybut.
- **Wyszukiwanie pełnotekstowe** — odnajdywanie treści według słów i rankingu.
- **ArangoSearch** — mechanizm wyszukiwania i analizy tekstu.

## Key points

- Indeks przyspiesza jedne zapytania, ale ma koszt przechowywania i zmian.
- Nie każdy atrybut powinien mieć indeks.
- Indeks musi pasować do warunków i kolejności zapytań.
- Wyszukiwanie tekstowe różni się od prostego filtrowania wartości.
- Indeksy nie zastępują dobrego modelu danych.

## Example

Dla zapytań filtrujących po kilku atrybutach może być potrzebny indeks złożony. Dla wyszukiwania po treści opisowej właściwszy będzie mechanizm wyszukiwania tekstowego.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Zbieramy najczęstsze i najważniejsze zapytania.
2. Określamy warunki filtrowania, sortowania i wyszukiwania.
3. Dobieramy minimalny zestaw indeksów.
4. Sprawdzamy plan zapytania i jego koszt.
5. Mierzymy wpływ indeksu na odczyt i modyfikacje.
6. Usuwamy indeksy, które nie dają uzasadnionej wartości.

## Pytania

1. Do czego służy indeks?
2. Czy indeks zawsze przyspiesza cały system?
3. Czym jest indeks unikalny?
4. Czym jest indeks złożony?
5. Czym różni się wyszukiwanie tekstowe od filtra?
6. Czym jest ArangoSearch?
7. Czy każdy atrybut powinien mieć indeks?
8. Od czego zależy dobór indeksu?
9. Jaki koszt ma nadmiar indeksów?
10. Czy indeks zastępuje dobry model danych?

## Odpowiedzi

1. Przyspiesza określone sposoby odnajdywania danych.
2. Nie, może zwiększać koszt zapisu i zajmować miejsce.
3. Wspiera niepowtarzalność wartości.
4. Obejmuje kilka atrybutów.
5. Wyszukiwanie tekstowe analizuje treść, a filtr sprawdza warunek wartości.
6. Mechanizm wyszukiwania i analizy tekstu.
7. Nie, tylko te używane przez ważne zapytania.
8. Od wzorców zapytań i wymagań systemu.
9. Więcej miejsca i większy koszt zmian danych.
10. Nie, tylko wspiera właściwie zaprojektowany model.

[Powrót do spisu treści](README.md)
