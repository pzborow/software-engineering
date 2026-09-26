# Wersje i źródła

## Wersje obowiązujące

- **Python 3.13**: Składnia przykładów (zmienne, pętle, funkcje, input, pliki) i komunikaty o błędach pochodzą z Pythona 3.x.

## Wersje w przykładach

| Narzędzie lub standard | Wersja | Od czego zależy | Gdzie |
|---|---|---|---|
| Git | 2.x | Opcja -b main w git init wymaga Gita 2.28 lub nowszego. | [09 › Zapisuj wersje kodu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#zapisuj-wersje-kodu) |
| Python | 3.13 | Przykład z print działa w tej wersji. | [01 › Poznaj język programowania](01%20Wejd%C5%BA%20w%20%C5%9Bwiat%20programowania.md#poznaj-język-programowania), [03 › Rozpoznaj błąd w programie](03%20Napisz%20i%20uruchom%20kod.md#rozpoznaj-błąd-w-programie), [05 › Wykonuj działania matematyczne](05%20Podejmuj%20decyzje%20w%20programie.md#wykonuj-działania-matematyczne), [05 › Połącz kilka tekstów](05%20Podejmuj%20decyzje%20w%20programie.md#połącz-kilka-tekstów), [05 › Zapisz warunek z if](05%20Podejmuj%20decyzje%20w%20programie.md#zapisz-warunek-z-if), [07 › Przekaż funkcji argumenty](07%20Uporz%C4%85dkuj%20kod%20funkcjami.md#przekaż-funkcji-argumenty), [09 › Rozróżnij dwa rodzaje błędów](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#rozróżnij-dwa-rodzaje-błędów), [09 › Czytaj komunikat o błędzie](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#czytaj-komunikat-o-błędzie) |

## Źródła

Weryfikator faktów sprawdził w dokumentacji sekcje: 44; źródła ma sekcji: 20.

### 01. Wejdź w świat programowania

- [Poznaj język programowania](01%20Wejd%C5%BA%20w%20%C5%9Bwiat%20programowania.md#poznaj-język-programowania): [Python 3.13 tutorial: An Informal Introduction to Python (strings, print)](https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/introduction.rst). print() wypisuje tekst w cudzysłowie na ekran (bez cudzysłowów), a literał tekstowy zapisuje się w cudzysłowach; kod print("Cześć, Wspólna Kasa!") jest poprawny w Pythonie 3.13.
- [Poznaj język programowania](01%20Wejd%C5%BA%20w%20%C5%9Bwiat%20programowania.md#poznaj-język-programowania): [Python 3.13 docs: What's New in 3.10 (improved SyntaxError messages)](https://github.com/python/cpython/blob/v3.13.9/Doc/whatsnew/3.10.rst). Niedomknięte ograniczniki, w tym literały tekstowe, kończą się SyntaxError, więc brak jednego cudzysłowu uniemożliwia wykonanie polecenia.

### 03. Napisz i uruchom kod

- [Uruchom swój program](03%20Napisz%20i%20uruchom%20kod.md#uruchom-swój-program): [Python 3.13 tutorial: An Informal Introduction (comments)](https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/introduction.rst). Komentarz zaczyna się od # i jest ignorowany przez interpreter, więc w kasa.py wykonuje się tylko print.
- [Uruchom swój program](03%20Napisz%20i%20uruchom%20kod.md#uruchom-swój-program): [Python 3.13 tutorial: Modules (running a script)](https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/modules.rst). Skrypt uruchamia się poleceniem `python nazwa.py` w powłoce; `python kasa.py` jest poprawną formą.
- [Opisuj kod komentarzami](03%20Napisz%20i%20uruchom%20kod.md#opisuj-kod-komentarzami): [Lexical analysis — Python 3.13 documentation](https://docs.python.org/3.13/reference/lexical_analysis.html). Komentarz zaczyna się od # (poza literałem napisowym), kończy z końcem linii, jest ignorowany przez składnię i może stać za instrukcją w tej samej linii.

### 04. Zapamiętaj dane w zmiennych

- [Rozróżnij liczbę i tekst](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#rozróżnij-liczbę-i-tekst): [CPython 3.13 tokenizer tests: float literals](https://github.com/python/cpython/blob/v3.13.9/Lib/test/tokenizedata/tokenize_tests.txt). Ułamek dziesiętny zapisuje się z kropką (np. `x = 3.14`), więc `kwota = 45.5` jest poprawnym literałem float.
- [Sprawdź typ danych](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#sprawdź-typ-danych): [Python 3.13 typing docs (przykład z type(a) dla int)](https://github.com/python/cpython/blob/v3.13.9/Doc/library/typing.rst). type() zwraca typ wartości (type(3) to int); nazwy int oraz typ obiektu zgadzają się z tabelą sekcji.
- [Sprawdź typ danych](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#sprawdź-typ-danych): [Python 3.13 built-in functions (type())](https://github.com/python/cpython/blob/v3.13.9/Doc/library/functions.rst). type(obiekt) jest wbudowaną funkcją zwracającą typ obiektu; w Pythonie 3 typy wbudowane są klasami, więc wynik ma postać <class 'str'>.
- [Użyj prawdy i fałszu](04%20Zapami%C4%99taj%20dane%20w%20zmiennych.md#użyj-prawdy-i-fałszu): [Built-in Types — Boolean Type (Python 3.13)](https://docs.python.org/3.13/library/stdtypes.html). bool ma dwie stałe True i False, zapisywane wielką literą; type(zaplacono) wypisuje <class 'bool'>; kod z sekcji daje podany wynik.

### 05. Podejmuj decyzje w programie

- [Wykonuj działania matematyczne](05%20Podejmuj%20decyzje%20w%20programie.md#wykonuj-działania-matematyczne): [Python 3.13: Expressions (arytmetyka, priorytety operatorów)](https://docs.python.org/3.13/reference/expressions.html). Potwierdza operatory + - * / // % **, wynik float z `/`, dzielenie z zaokrągleniem w dół dla `//`, resztę dla `%`, kolejność działań, sklejanie (`+`) i powtarzanie (`*`) tekstu oraz to, że pozostałe działania wymagają liczb (TypeError).
- [Wykonuj działania matematyczne](05%20Podejmuj%20decyzje%20w%20programie.md#wykonuj-działania-matematyczne): [Python 3.13 Tutorial: Floating-Point Arithmetic](https://docs.python.org/3.13/tutorial/floatingpoint.html). Potwierdza, że ułamki są trzymane jako przybliżenia binarne, co tłumaczy końcówkę `...336` w wyniku `100 / 3`.
- [Połącz kilka tekstów](05%20Podejmuj%20decyzje%20w%20programie.md#połącz-kilka-tekstów): [CPython 3.13 docs: Doc/library/stdtypes.rst (f-strings)](https://github.com/python/cpython/blob/v3.13.9/Doc/library/stdtypes.rst). F-string wstawia wartości nietekstowe (np. liczby) przez domyślne str(), więc `f"{imie} zapłaciła {kwota} zł"` działa z liczbą.
- [Połącz kilka tekstów](05%20Podejmuj%20decyzje%20w%20programie.md#połącz-kilka-tekstów): [CPython 3.13 docs: Doc/whatsnew/3.2.rst (str() dla float)](https://github.com/python/cpython/blob/v3.13.9/Doc/whatsnew/3.2.rst). str() liczby zmiennoprzecinkowej daje jej zapis tekstowy, więc str(45.5) daje "45.5".
- [Porównaj dwie wartości](05%20Podejmuj%20decyzje%20w%20programie.md#porównaj-dwie-wartości): [Python 3.13 Language Reference: Expressions – Comparisons](https://docs.python.org/3.13/reference/expressions.html#comparisons). Sześć operatorów porównania (==, !=, <, >, <=, >=) zwraca True albo False. Obiekty nie muszą być tego samego typu. Porównanie == tekstu z liczbą daje False, bez błędu. Dlatego wyniki w bloku text (True, False, False, True, False, False) są poprawne.
- [Zapisz warunek z if](05%20Podejmuj%20decyzje%20w%20programie.md#zapisz-warunek-z-if): [Compound statements — Python 3.13 documentation](https://docs.python.org/3.13/reference/compound_stmts.html). Składnia `if warunek:` z dwukropkiem i blokiem wciętych linii (suite); dokumentacja wymaga spójnego wcięcia, a nie dokładnie czterech spacji.

### 06. Powtarzaj i zbieraj dane

- [Unikaj pętli nieskończonej](06%20Powtarzaj%20i%20zbieraj%20dane.md#unikaj-pętli-nieskończonej): [Compound statements (while)](https://docs.python.org/3.13/reference/compound_stmts.html). Pętla while powtarza ciało, dopóki warunek jest prawdziwy. Kod `while True:` jest poprawny.
- [Unikaj pętli nieskończonej](06%20Powtarzaj%20i%20zbieraj%20dane.md#unikaj-pętli-nieskończonej): [Built-in Exceptions (KeyboardInterrupt)](https://docs.python.org/3.13/library/exceptions.html). KeyboardInterrupt jest zgłaszany, gdy użytkownik naciśnie klawisz przerwania, zwykle Control-C.
- [Unikaj pętli nieskończonej](06%20Powtarzaj%20i%20zbieraj%20dane.md#unikaj-pętli-nieskończonej): [time — Time access and conversions](https://docs.python.org/3.13/library/time.html). time.sleep(1) zawiesza wykonanie na 1 sekundę. Wywołanie w tym przykładzie jest poprawne.
- [Zbierz dane w liście](06%20Powtarzaj%20i%20zbieraj%20dane.md#zbierz-dane-w-liście): [An Informal Introduction to Python (3.13) – Lists](https://docs.python.org/3.13/tutorial/introduction.html). Lista zapisana w nawiasach kwadratowych z wartościami rozdzielonymi przecinkami, len() zwraca liczbę elementów, wypisanie listy tekstów pokazuje apostrofy (['Ania', 'Bartek', 'Celina']), pusta lista to [].
- [Wybierz element z listy](06%20Powtarzaj%20i%20zbieraj%20dane.md#wybierz-element-z-listy): [An Informal Introduction to Python (3.13)](https://docs.python.org/3.13/tutorial/introduction.html). Indeksowanie od zera, indeksy ujemne liczone od końca (-1 ostatni, -2 przedostatni) i IndexError dla indeksu spoza zakresu; przykład kodu daje wskazane wyniki.
- [Przejdź przez całą listę](06%20Powtarzaj%20i%20zbieraj%20dane.md#przejdź-przez-całą-listę): [Python 3.13 tutorial: More Control Flow Tools (for statements)](https://github.com/python/cpython/blob/v3.13.9/Doc/tutorial/controlflow.rst). Pętla `for` iteruje po elementach sekwencji (np. listy) w kolejności ich występowania, a przykład `for w in words:` odpowiada składni `for imie in osoby:`.
- [Przejdź przez całą listę](06%20Powtarzaj%20i%20zbieraj%20dane.md#przejdź-przez-całą-listę): [Python 3.13 language reference: Compound statements (for)](https://github.com/python/cpython/blob/v3.13.9/Doc/reference/compound_stmts.rst). Zmienna pętli jest przy każdej iteracji nadpisywana kolejnym elementem, więc `imie` dostaje po kolei każdy element.

### 08. Porozmawiaj z użytkownikiem

- [Przyjmij dane z zewnątrz](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#przyjmij-dane-z-zewnątrz): [Built-in Functions: input() (Python 3.13)](https://docs.python.org/3.13/library/functions.html#input). input("Kto zapłacił? ") jest poprawnym wywołaniem: argument prompt jest wypisywany na standardowe wyjście, a funkcja zwraca tekst (str), więc szkic z zapytaj_o_wydatek() jest zgodny z dokumentacją.
- [Zapytaj użytkownika o dane](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapytaj-użytkownika-o-dane): [Built-in Functions — Python 3.13 documentation](https://docs.python.org/3.13/library/functions.html). input(prompt) wypisuje pytanie bez końcowego newline, czeka na linię i zwraca ją jako str (bez znaku nowej linii); float("45.5") daje 45.5, a float("abc") zgłasza ValueError, co potwierdza twierdzenie o błędzie przerywającym program.
- [Zapisz dane w pliku](08%20Porozmawiaj%20z%20u%C5%BCytkownikiem.md#zapisz-dane-w-pliku): [Built-in Functions — open() (Python 3.13)](https://docs.python.org/3.13/library/functions.html). Tryby 'r' (czytanie, plik musi istnieć), 'w' (zapis z obcięciem starej treści), 'a' (dopisywanie na końcu) oraz parametr encoding w trybie tekstowym; przykład z open(..., encoding='utf-8') działa.

### 09. Oswój błędy w kodzie

- [Rozróżnij dwa rodzaje błędów](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#rozróżnij-dwa-rodzaje-błędów): [Errors and Exceptions — Python 3.13](https://docs.python.org/3.13/tutorial/errors.html). Format komunikatu SyntaxError (plik, linia, karetka, typ i komunikat) oraz to, że błędy składni wykrywane są przy parsowaniu, przed wykonaniem; potwierdza też, że błąd bywa wskazany za miejscem do poprawy.
- [Czytaj komunikat o błędzie](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#czytaj-komunikat-o-błędzie): [Errors and Exceptions (Python 3.13 Tutorial)](https://docs.python.org/3.13/tutorial/errors.html). Format śladu (Traceback (most recent call last), File ..., in <module>, znaki ~ i ^ pod linią kodu) oraz ostatnia linia w postaci ZeroDivisionError: division by zero, czyli nazwa błędu i opis.
- [Czytaj komunikat o błędzie](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#czytaj-komunikat-o-błędzie): [What's New In Python 3.13](https://docs.python.org/3.13/whatsnew/3.13.html). Znaczniki ~ i ^ pochodzą z Pythona 3.11 (PEP 657) i w 3.13 nie zmieniono ich działania, więc występują w przykładzie. Wersja 3.13 domyślnie koloruje ślad w terminalu, co nie przeczy zdaniu o czerwonym tekście.
- [Zapisuj wersje kodu](09%20Osw%C3%B3j%20b%C5%82%C4%99dy%20w%20kodzie.md#zapisuj-wersje-kodu): [git-init Documentation](https://git-scm.com/docs/git-init). Opcja `-b <branch-name>` / `--initial-branch` istnieje i ustawia nazwę początkowej gałęzi; domyślnie `master`, konfigurowalne przez init.defaultBranch. Wpis „git init” bez argumentu działa w bieżącym folderze (składnia z opcjonalnym <directory>).
