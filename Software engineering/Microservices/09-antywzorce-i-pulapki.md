# Antywzorce i pułapki

<a id="term-rozproszony-monolit"></a>[Rozproszony monolit](00-glosariusz.md#rozproszony-monolit) to system, który wygląda jak mikroserwisy, ale zachowuje się jak jeden monolit. Usługi muszą być wdrażane razem, znają swoje szczegóły, współdzielą bazę albo wymagają zsynchronizowanych zmian.

Najczęstszą pułapką jest podział techniczny zamiast domenowego. Serwisy typu `UserAPI`, `UserBusinessLogic` i `UserStorage` zwykle tylko przenoszą warstwy aplikacji do sieci. To zwiększa opóźnienia i awaryjność bez poprawy autonomii.

Drugą pułapką jest wspólna baza danych. Na początku ułatwia pracę, ale usuwa granice odpowiedzialności. Gdy wiele usług pisze do tych samych tabel, żadna naprawdę nie jest właścicielem danych.

Trzecią pułapką jest zbyt drobny podział. Jeśli przepływ użytkownika wymaga kilkunastu synchronicznych wywołań, system będzie wolny, trudny w debugowaniu i podatny na częściowe awarie.

Kolejną pułapką jest brak wersjonowania kontraktów. Jeśli dostawca zmienia API bez planu migracji, konsumenci zaczynają bać się aktualizacji. To prowadzi do zamrożenia architektury.

Mikroserwisy mogą też zwiększyć koszt poznawczy. Zamiast jednego repozytorium i jednego procesu trzeba rozumieć wiele usług, pipeline'ów, dashboardów, alertów i zależności.

## Typowe sygnały ostrzegawcze

- każda zmiana wymaga wielu repozytoriów,
- usługi mają wspólną bazę,
- brak właścicieli usług,
- błędy diagnozuje się ręcznie przez wiele logów bez correlation ID,
- wdrożenia są rzadkie i stresujące,
- zespoły mówią o endpointach, ale nie o domenie.

## Co zapamiętać

- Mikroserwisy bez autonomii są tylko droższym monolitem.
- Współdzielona baza to silny sygnał złej granicy.
- Zbyt małe usługi potrafią zwiększyć sprzężenie zamiast je zmniejszyć.
