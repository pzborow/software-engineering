# Kiedy stosować, a kiedy nie

Mikroserwisy warto stosować, gdy problemem organizacji jest skala niezależnej pracy. Jeśli kilka zespołów musi równolegle rozwijać różne obszary, a jedna aplikacja blokuje wydania, mikroserwisy mogą pomóc.

Drugim dobrym powodem są różne wymagania operacyjne. Jeśli wyszukiwanie wymaga innego skalowania niż płatności, a raportowanie ma inny profil obciążenia niż proces zamówień, oddzielne usługi mogą ułatwić zarządzanie zasobami i ryzykiem.

Mikroserwisy nie są dobrym wyborem, gdy domena jest nieznana. Wtedy granice będą się często zmieniały, a koszt zmian w systemie rozproszonym będzie wysoki. Lepiej zacząć od modularnego monolitu i wydzielać dopiero stabilniejsze obszary.

Nie warto stosować mikroserwisów, jeśli głównym problemem jest słaba jakość kodu. Rozbicie słabego projektu na wiele usług zwykle zwiększa liczbę miejsc, w których ten sam bałagan trzeba utrzymać.

Mikroserwisy wymagają dojrzałości operacyjnej. Zespół potrzebuje automatyzacji wdrożeń, monitoringu, logowania, obsługi incydentów, testów kontraktowych i umiejętności pracy ze spójnością ostateczną. Bez tego system będzie trudniejszy niż monolit.

## Decyzja praktyczna

Jeśli system może być utrzymany jako modularny monolit przez jeden lub dwa zespoły, zwykle warto tak zacząć. Jeśli moduły mają już stabilne granice, różne tempo zmian i osobnych właścicieli, można stopniowo wydzielać usługi.

## Co zapamiętać

- Mikroserwisy rozwiązują problemy niezależności i skali organizacyjnej.
- Nie rozwiązują automatycznie problemów jakości kodu.
- Domena musi być wystarczająco rozumiana, żeby wyznaczyć granice.
- Brak observability i CI/CD to mocny argument przeciw mikroserwisom.
