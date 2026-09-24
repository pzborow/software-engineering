# Granice serwisów i domena

<a id="term-granica-serwisu"></a>[Granica serwisu](00-glosariusz.md#granica-serwisu) określa, za co usługa odpowiada i czego nie powinna robić. Dobra granica zmniejsza liczbę wspólnych zmian. Zła granica sprawia, że każda funkcja wymaga dotykania wielu usług.

Najlepsze granice zwykle wynikają z języka biznesu. Jeśli zespół biznesowy mówi osobno o zamówieniach, płatnościach, katalogu i dostawie, to są to kandydaci na oddzielne obszary. Nie oznacza to automatycznie osobnych usług, ale oznacza oddzielne odpowiedzialności.

<a id="term-bounded-context"></a>[Bounded context](00-glosariusz.md#bounded-context) pomaga zrozumieć, że to samo słowo może znaczyć co innego w różnych częściach systemu. „Klient” w płatnościach może oznaczać płatnika, a w marketingu odbiorcę kampanii. Próba wymuszenia jednego modelu dla całej firmy często prowadzi do sztucznego, przeciążonego obiektu.

Granica serwisu powinna obejmować reguły, dane i decyzje. Jeśli `Orders` przechowuje zamówienia, ale `Payments` decyduje o ich statusie, odpowiedzialność jest rozmyta. Usługi mogą współpracować, ale decyzja powinna mieć jednego właściciela.

Nie każda granica musi od razu stać się procesem lub repozytorium. Najpierw można utrzymać ją jako moduł w modularnym monolicie. Gdy granica okaże się stabilna i potrzebuje niezależnego wdrażania, łatwiej ją wydzielić.

## Sygnały dobrej granicy

- zmiany biznesowe zwykle mieszczą się w jednej usłudze,
- dane mają jasnego właściciela,
- model pojęć jest spójny w obrębie usługi,
- API pokazuje intencje biznesowe, a nie tabele,
- usługa może być testowana i wdrażana niezależnie.

## Sygnały złej granicy

- każda zmiana wymaga równoległych PR-ów w wielu usługach,
- usługi współdzielą bazę danych,
- jedna usługa musi znać szczegóły wewnętrzne drugiej,
- pojawia się wiele synchronicznych wywołań w jednym przepływie,
- model biznesowy jest sztucznie podzielony według warstw technicznych.

## Co zapamiętać

- Granice usług są decyzją domenową, nie tylko techniczną.
- Bounded context chroni przed wymuszaniem jednego modelu dla całej organizacji.
- Najpierw stabilizuj granice, dopiero potem rozdzielaj procesy.
