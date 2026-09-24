# Czym są mikroserwisy

<a id="term-mikroserwis"></a>[Mikroserwis](00-glosariusz.md#mikroserwis) to samodzielna usługa realizująca konkretną zdolność biznesową. Nie chodzi o to, żeby każdy serwis miał mało linii kodu. Chodzi o to, żeby miał jasną odpowiedzialność, własny cykl zmian i ograniczoną liczbę powodów, dla których musi zmieniać się razem z resztą systemu.

Mikroserwisy są sposobem organizacji systemu wokół <a id="term-domena"></a>[domeny](00-glosariusz.md#domena), a nie tylko sposobem uruchamiania wielu procesów. Jeżeli usługi są wydzielone według warstw technicznych, ale każda zmiana biznesowa wymaga dotykania wszystkich naraz, to nie osiągamy najważniejszej korzyści.

Najważniejszą obietnicą mikroserwisów jest <a id="term-autonomia"></a>[autonomia](00-glosariusz.md#autonomia). Zespół powinien móc zmienić i wdrożyć usługę bez proszenia wielu innych zespołów o równoczesne wydanie. Ta autonomia jest jednak kupowana kosztem komunikacji sieciowej, obserwowalności, operacji i trudniejszego modelu danych.

Mikroserwis powinien ukrywać swoje decyzje wewnętrzne. Inne usługi powinny znać jego kontrakt, ale nie powinny znać tabel, szczegółów implementacji ani wewnętrznego modelu. Jeśli inni muszą wiedzieć, jak usługa przechowuje stan, granica jest nieszczelna.

Dobry mikroserwis nie jest izolowaną wyspą. Współpracuje z innymi usługami przez jawne API, zdarzenia albo wiadomości, ale robi to w taki sposób, aby awaria lub zmiana jednej części nie paraliżowała całego systemu.

## Przykład

W sklepie internetowym `Orders` może odpowiadać za przyjmowanie i status zamówień, `Payments` za płatności, a `Catalog` za informacje o produktach. Każda z tych usług ma inne reguły biznesowe, inne tempo zmian i inne dane, więc mogą być kandydatami na osobne serwisy.

Zły podział to `OrderController`, `OrderService` i `OrderRepository` jako trzy oddzielne usługi. To jest podział warstwowy, a nie biznesowy. Zwiększa koszty sieci, ale nie daje autonomii.

## Co zapamiętać

- Mikroserwis to granica odpowiedzialności biznesowej, nie „mała aplikacja”.
- Autonomia jest główną korzyścią, ale też głównym wymaganiem.
- Mikroserwisy mają sens dopiero wtedy, gdy organizacja potrafi utrzymać wiele niezależnych usług.
- Najpierw pytaj o granice domeny, potem o technologię.
