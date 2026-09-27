# Wzorce projektowe GoF w Pythonie: kreacyjne, strukturalne i behawioralne

Wzorce projektowe GoF w Pythonie to sprawdzone sposoby układania klas i obiektów, dzięki którym kod rośnie bez przepisywania go od nowa przy każdej zmianie wymagań. Dzielą się na kreacyjne (jak powstają obiekty), strukturalne (jak się łączą) i behawioralne (jak współpracują i dzielą obowiązki). W tym dziale dziedziny łączą się tak: projektowanie obiektowe pokazujemy na przykładach z urzędu rozpatrującego wnioski o zaginiony poniedziałek, a każde rozwiązanie sprawdzamy testami w pytest. Po tym dziale ustalisz, jakie metody ma udostępniać dana część kodu, by inne mogły z niej korzystać bez znajomości jej wnętrza, uzasadnisz wybór między klasą bazową wymuszającą implementację a samym opisem wymaganych metod i uruchomisz pierwszy test, w którym sztuczny obiekt zastępuje prawdziwy składnik.

## Dla kogo

- Perspektywa: programista Python (backend), poziom: zaawansowany.
- Zakładamy, że znasz: Python: klasy, funkcje, moduły, wyjątki, kolekcje, dekoratory, typowanie.
- Przykłady kodu: python.

## Czego się nauczysz

Działy: 6 · pytania: 44. Na końcu każdego działu są „Co zapamiętać” i pytania sprawdzające z ukrytymi odpowiedziami.

1. [Interfejsy ABC i Protocol](01%20Interfejsy%20ABC%20i%20Protocol.md): sekcje: 10, pytania: 8
2. [Model domeny wniosku](02%20Model%20domeny%20wniosku.md): sekcje: 8, pytania: 8
3. [Tworzenie wniosków](03%20Tworzenie%20wniosk%C3%B3w.md): sekcje: 8, pytania: 8
4. [Struktury wniosku](04%20Struktury%20wniosku.md): sekcje: 8, pytania: 8
5. [Przepływ komisji](05%20Przep%C5%82yw%20komisji.md): sekcje: 8, pytania: 8
6. [System Urzędu Zaginionych Poniedziałków](06%20System%20Urz%C4%99du%20Zaginionych%20Poniedzia%C5%82k%C3%B3w.md): sekcje: 4, pytania: 4

## Przykład przewodni

**Urząd Zaginionych Poniedziałków.** Pakiet Pythona `urzad` obsługujący wnioski o odzyskanie zaginionego poniedziałku: pieczątki (także z przyszłości), załączniki z obcych kalendarzy, teczki, kontrole, głosowanie komisji, decyzje z powiadomieniami i cofaniem. [Stan i plan przyrostów](99%20Przyk%C5%82ad%20przewodni.md).

## Wersje

Przykłady opierają się na: Python 3.13, pytest 8.x. Szczegóły i źródła: [Wersje i źródła](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md).

## Pomocnicze strony

- [Ściągawka](96%20%C5%9Aci%C4%85gawka.md): najważniejsze rzeczy na jednej stronie.
- [Glosariusz](00%20Glosariusz.md): krótkie definicje pojęć z linkami do miejsc użycia.
- [Pułapki](98%20Pu%C5%82apki.md): nieoczywiste zachowania z przykładów.
- [Wersje i źródła](97%20Wersje%20i%20%C5%BAr%C3%B3d%C5%82a.md): od czego zależą przykłady i gdzie to potwierdzono.
- [Przykład przewodni](99%20Przyk%C5%82ad%20przewodni.md): cały wątek w jednym miejscu.
- [Raport pokrycia](raport-pokrycia.md): jak powstał tutorial i co zostało do redakcji.
