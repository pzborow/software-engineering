# Wdrażanie, testowanie i bezpieczeństwo

Mikroserwisy mają sens tylko wtedy, gdy można je bezpiecznie i często wdrażać. Jeśli każda zmiana wymaga ręcznego procesu, wspólnego okna wdrożeniowego i koordynacji wielu zespołów, autonomia pozostaje teorią.

<a id="term-deployment-pipeline"></a>[Deployment pipeline](00-glosariusz.md#deployment-pipeline) powinien automatyzować build, testy, publikację artefaktu i wdrożenie. Każda usługa powinna mieć powtarzalny sposób przejścia od commita do środowiska.

<a id="term-canary-release"></a>[Canary release](00-glosariusz.md#canary-release) zmniejsza ryzyko, bo nowa wersja obsługuje najpierw małą część ruchu. <a id="term-blue-green-deployment"></a>[Blue-green deployment](00-glosariusz.md#blue-green-deployment) pozwala przełączyć ruch między starą i nową wersją środowiska. Oba podejścia wymagają metryk i szybkiego wycofania.

Testowanie mikroserwisów nie może opierać się wyłącznie na wielu wielkich testach przez cały system. Takie testy są wolne, kruche i trudne w diagnozie. Potrzebne są testy jednostkowe, integracyjne, <a id="term-contract-test"></a>[contract testy](00-glosariusz.md#contract-test) i mała liczba krytycznych <a id="term-test-end-to-end"></a>[testów end-to-end](00-glosariusz.md#test-end-to-end).

Contract test jest szczególnie ważny, bo sprawdza relację między konsumentem i dostawcą usługi. Dzięki niemu dostawca wie, czy zmiana API nie łamie realnych oczekiwań odbiorcy.

Bezpieczeństwo nie może polegać tylko na zaufanej sieci wewnętrznej. Każda usługa powinna rozumieć tożsamość, autoryzację i zakres dostępu do własnych zasobów. Sekrety powinny być zarządzane poza kodem i rotowane.

## Przykład

Zmiana pola w `Payments API` powinna przejść testy dostawcy i testy kontraktowe konsumentów. Dopiero potem można wdrożyć canary i obserwować błędy, czas odpowiedzi oraz metryki biznesowe.

## Co zapamiętać

- Niezależne wdrożenia wymagają automatyzacji.
- Contract testy chronią przed przypadkowym złamaniem współpracy.
- E2E jest potrzebne, ale nie powinno być jedyną linią obrony.
- Bezpieczeństwo jest odpowiedzialnością każdej usługi.
