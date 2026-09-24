# Bezpieczeństwo

## Opis

Bezpieczeństwo ArangoDB obejmuje ochronę dostępu do instancji, baz, kolekcji i danych oraz zabezpieczenie komunikacji. Uprawnienia powinny odpowiadać rzeczywistym rolom i potrzebom, a nie być szersze dla wygody.

## Kluczowe koncepty

- **Uwierzytelnianie** — potwierdzenie tożsamości użytkownika lub aplikacji.
- **Autoryzacja** — określenie dozwolonych operacji.
- **Role i uprawnienia** — zakres dostępu do zasobów.
- **Szyfrowanie** — ochrona danych podczas przesyłania lub przechowywania.
- **Audyt** — rejestrowanie istotnych działań.

## Key points

- Dostęp należy ograniczać zgodnie z zasadą najmniejszych uprawnień.
- Konto administracyjne nie powinno być domyślnym kontem aplikacji.
- Sekrety nie powinny być przechowywane w kodzie.
- Bezpieczeństwo obejmuje także backupy i logi.
- Uprawnienia trzeba regularnie przeglądać.

## Example

Aplikacja może mieć dostęp tylko do określonej bazy i kolekcji, bez prawa do zarządzania całą instancją.

## Dodatkowe wyjaśnienie

W praktyce ważne jest to, że ArangoDB nie wybiera modelu za projektanta. Decyzja zależy od tego, jak dane są odczytywane, jak powiązane są relacje i czy potrzebne są zapytania grafowe, dokumentowe czy tekstowe. To, co naprawdę ma znaczenie, to zgodność modelu z prawdziwymi potrzebami systemu oraz umiejętność utrzymania spójności danych bez nadmiernej komplikacji.

## Pełny flow

1. Identyfikujemy użytkowników, aplikacje i zasoby.
2. Definiujemy wymagane operacje.
3. Nadajemy minimalne uprawnienia.
4. Chronimy komunikację i sekrety.
5. Rejestrujemy istotne działania.
6. Regularnie weryfikujemy dostęp i reagujemy na incydenty.

## Pytania

1. Co obejmuje bezpieczeństwo ArangoDB?
2. Czym różni się uwierzytelnianie od autoryzacji?
3. Co oznacza najmniejsze uprawnienie?
4. Dlaczego aplikacja nie powinna używać konta administracyjnego?
5. Co należy chronić poza danymi?
6. Czym jest audyt?
7. Gdzie nie powinny trafić sekrety?
8. Dlaczego trzeba przeglądać uprawnienia?
9. Co należy określić przed nadaniem dostępu?
10. Jaki jest cel bezpiecznej konfiguracji?

## Odpowiedzi

1. Dostęp, uprawnienia, komunikację, sekrety, backupy i audyt.
2. Pierwsze potwierdza tożsamość, drugie określa dozwolone działania.
3. Dostęp tylko do zasobów koniecznych do pracy.
4. Bo daje zbyt szeroki dostęp i zwiększa skutki błędu.
5. Komunikację, backupy, logi i konfigurację.
6. Rejestrowanie istotnych działań do analizy.
7. W kodzie i publicznie dostępnej konfiguracji.
8. Role i potrzeby zmieniają się w czasie.
9. Tożsamości, zasoby i potrzebne operacje.
10. Ograniczenie ryzyka nieuprawnionego dostępu.

[Powrót do spisu treści](README.md)
