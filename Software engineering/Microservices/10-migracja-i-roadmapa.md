# Migracja i roadmapa

Migracja do mikroserwisów powinna być stopniowa. Najgorszy wariant to wielkie przepisanie systemu, które przez wiele miesięcy nie dostarcza wartości, a na końcu próbuje zastąpić wszystko naraz.

<a id="term-strangler-fig-pattern"></a>[Strangler fig pattern](00-glosariusz.md#strangler-fig-pattern) polega na stopniowym przejmowaniu fragmentów odpowiedzialności starego systemu przez nowe elementy. Nowy kod otacza stary system i przejmuje kolejne przepływy, aż stary fragment można usunąć.

Pierwszym krokiem migracji jest zwykle uporządkowanie monolitu. Trzeba znaleźć moduły, właścicieli danych, przepływy biznesowe i zależności. Jeśli nie umiemy wskazać granic w kodzie i domenie, nie umiemy ich też bezpiecznie przenieść do sieci.

Drugim krokiem jest wybranie fragmentu o rozsądnym ryzyku. Nie powinien to być najbardziej krytyczny proces w firmie, ale też nie powinien to być fragment bez znaczenia. Dobry kandydat ma jasną odpowiedzialność, mierzalną wartość i ograniczoną liczbę zależności.

Trzecim krokiem jest zbudowanie operacyjnych fundamentów: pipeline, logi, metryki, tracing, alerty, obsługa sekretów, rollback i testy kontraktowe. Bez tego każda nowa usługa zwiększa dług operacyjny.

Migracja kończy się dopiero wtedy, gdy stary fragment można usunąć albo wyraźnie ograniczyć. Samo dodanie nowej usługi obok starego systemu nie jest sukcesem, jeśli zespół musi utrzymywać oba modele na zawsze.

## Kolejność działania

1. Uporządkuj monolit i nazwij moduły.
2. Wskaż bounded context i właścicieli danych.
3. Wybierz pierwszy fragment do wydzielenia.
4. Zbuduj kontrakt i sposób synchronizacji danych.
5. Dodaj obserwowalność i automatyzację wdrożeń.
6. Przenieś ruch stopniowo.
7. Usuń lub ogranicz stary kod.

## Co zapamiętać

- Migracja jest procesem biznesowo-technicznym, nie tylko refaktoryzacją.
- Najpierw stabilizuj granice, potem wydzielaj usługi.
- Każda wydzielona usługa musi mieć właściciela, observability i pipeline.
