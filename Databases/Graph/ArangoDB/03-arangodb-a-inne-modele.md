# ArangoDB a inne modele baz danych

## Opis

ArangoDB łączy cechy bazy dokumentowej, grafowej i narzędzi wyszukiwania. Nie oznacza to, że zastępuje każdą bazę w każdym zastosowaniu. Różnica polega na tym, że kilka sposobów modelowania jest dostępnych w jednej platformie.

## Kluczowe koncepty

- **Model dokumentowy** — dane jako niezależne dokumenty JSON.
- **Model grafowy** — dane jako wierzchołki i relacje.
- **Model relacyjny** — dane organizowane w tabelach i relacjach opartych na kluczach.
- **Wyszukiwanie** — odnajdywanie danych według tekstu, filtrów i rankingu.
- **Baza wielomodelowa** — platforma obsługująca więcej niż jeden model.

## Key points

- Dokumenty dobrze pasują do obiektów o zmiennej strukturze.
- Graf dobrze pasuje do wielopoziomowych relacji.
- Model relacyjny pozostaje naturalny dla wielu procesów tabelarycznych.
- ArangoDB ogranicza potrzebę łączenia kilku silników, ale nie usuwa kompromisów.
- Porównanie powinno dotyczyć potrzeb, a nie popularności technologii.

## Example

Ten sam zestaw danych można traktować jako dokumenty do prostego odczytu, jako graf do analizy relacji oraz jako źródło wyszukiwania tekstowego. Wybór sposobu zależy od konkretnego pytania.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Opisujemy dane bez przywiązania do technologii.
2. Rozpoznajemy operacje dokumentowe, relacyjne, grafowe i wyszukiwawcze.
3. Wybieramy model dominujący oraz modele pomocnicze.
4. Oceniamy, czy jedna platforma upraszcza rozwiązanie.
5. Sprawdzamy wydajność, spójność i kompetencje zespołu.
6. Dokumentujemy powody wyboru.

## Pytania

1. Jakie modele łączy ArangoDB?
2. Do czego pasuje model dokumentowy?
3. Do czego pasuje model grafowy?
4. Czy ArangoDB jest klasyczną bazą relacyjną?
5. Co oznacza baza wielomodelowa?
6. Jaka jest korzyść z jednego silnika?
7. Czy jeden silnik usuwa wszystkie kompromisy?
8. Od czego zależy wybór modelu?
9. Czy model relacyjny jest zawsze gorszy?
10. Po co dokumentować powód wyboru?

## Odpowiedzi

1. Dokumentowy, grafowy i wyszukiwawczy.
2. Do obiektów o elastycznej strukturze.
3. Do danych, których znaczenie wynika z relacji.
4. Nie, jest bazą wielomodelową z innym sposobem organizacji danych.
5. Obsługę kilku modeli w jednej platformie.
6. Mniej rozdzielonych technologii do utrzymania.
7. Nie, nadal trzeba świadomie wybrać model i kompromisy.
8. Od danych, zapytań i wymagań systemu.
9. Nie, może być najlepszy dla określonego problemu.
10. Aby decyzja była zrozumiała i możliwa do ponownej oceny.

[Powrót do spisu treści](README.md)
