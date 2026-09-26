# Sekrety i konfiguracja

Wiele incydentów bezpieczeństwa nie wymaga żadnej podatności w kodzie. Wystarczy klucz API w publicznym repozytorium, `DEBUG = True` na produkcji albo token w logach. Błędy konfiguracji są jedną z najwyżej notowanych kategorii na liście OWASP Top 10. Ten rozdział opisuje, gdzie trzymać sekrety, co zrobić, gdy wyciekną, i które ustawienia Django decydują o bezpieczeństwie produkcji.

```text
sekrety sklepu                          gdzie powinny być          gdzie często trafiają
SECRET_KEY, klucz JWT                   menedżer sekretów, env     settings.py w repozytorium
hasło do bazy                           menedżer sekretów          docker-compose.yml, README
klucz API operatora płatności           menedżer sekretów          logi żądań, Slack
sekret webhooków                        menedżer sekretów          test w repozytorium
klucze szyfrowania pól (Fernet)         KMS, menedżer sekretów     ta sama zmienna co reszta
```

## Sekrety poza kodem

<a id="term-secret"></a>[Sekret](00%20Glossary%20Security.md#secret) to każda wartość, której ujawnienie daje dostęp do systemu albo danych: hasła, klucze API, klucze podpisu i szyfrowania, tokeny. Zasada jest prosta: sekrety nie trafiają do repozytorium, nawet prywatnego. Repozytorium jest kopiowane na laptopy, do CI, do narzędzi zewnętrznych i trzyma historię na zawsze.

Kolejne poziomy dojrzałości:

| Sposób | Jak | Zalety | Ryzyka |
|---|---|---|---|
| sekret w kodzie | `SECRET_KEY = "abc…"` w `settings.py` | brak | każdy z dostępem do repozytorium ma sekret, historia na zawsze |
| plik `.env` | `django-environ` czyta plik niewersjonowany | proste, rozdzielone środowiska | plik kopiowany ręcznie, łatwo go zacommitować |
| zmienne środowiskowe | ustawiane przez platformę (Kubernetes, Heroku, systemd) | standard 12-factor | widoczne w `/proc`, `docker inspect`, raportach błędów, procesach potomnych |
| menedżer sekretów | Vault, AWS Secrets Manager, GCP Secret Manager, Azure Key Vault | audyt dostępu, rotacja, uprawnienia per usługa | zależność od usługi, koszt konfiguracji |
| KMS dla kluczy szyfrowania | klucz nigdy nie opuszcza usługi, aplikacja prosi o szyfrowanie | klucz nie wycieknie z aplikacji | opóźnienie, koszt wywołań |

W Django typowy układ to `django-environ` i zmienne środowiskowe, które na produkcji wypełnia menedżer sekretów (np. External Secrets Operator w Kubernetes albo integracja platformy):

```python
# settings/base.py
import environ

env = environ.Env()
environ.Env.read_env(BASE_DIR / ".env")        # tylko lokalnie, plik w .gitignore

SECRET_KEY = env("DJANGO_SECRET_KEY")          # bez wartości domyślnej: brak zmiennej = błąd startu
DEBUG = env.bool("DJANGO_DEBUG", default=False)
DATABASES = {"default": env.db("DATABASE_URL")}
PAYMENT_API_KEY = env("PAYMENT_API_KEY")
```

Zasada „fail closed” ma tu znaczenie. Wartość domyślna `DEBUG` to `False`, a `SECRET_KEY` nie ma wartości domyślnej. Brak zmiennej na produkcji kończy się błędem startu, a nie cichym uruchomieniem z niebezpiecznymi ustawieniami. Do repozytorium trafia `.env.example` z nazwami zmiennych i fikcyjnymi wartościami.

Zasada najmniejszych uprawnień dotyczy też sekretów. Każda usługa ma własne dane dostępowe z minimalnym zakresem: konto bazy aplikacji bez prawa do zmian schematu (migracje osobnym kontem), klucz do S3 tylko do jednego bucketu, token CI tylko do jednego repozytorium.

Sekrety przeciekają też poza repozytorium:

- do logów, np. przez logowanie całego żądania z nagłówkiem `Authorization` albo całego wyjątku z parametrami,
- na stronę błędu Django. Przy `DEBUG = True` pokazuje ona ustawienia. Filtr `SafeExceptionReporterFilter` ukrywa ustawienia, których nazwy zawierają m.in. `KEY`, `SECRET`, `PASS`, `TOKEN` i `SIGNATURE`, ale nie te nazwane inaczej, np. `STRIPE_SK`,
- do systemów zgłaszania błędów (Sentry), jeśli nie skonfiguruje się oczyszczania danych,
- do zrzutów ekranu, czatów i dokumentacji.

## Gdy sekret wycieknie

Wyciek sekretu trzeba traktować jak jego przejęcie, nawet jeśli repozytorium było publiczne tylko przez kilka minut. Boty skanują GitHuba w poszukiwaniu kluczy w ciągu sekund od publikacji.

Kolejność działań jest ważna:

1. Unieważnij albo zrotuj sekret u źródła: nowy klucz API u operatora płatności, nowe hasło bazy, nowy `SECRET_KEY` (rozdział 06). To pierwszy krok, a nie usuwanie z historii gita.
2. Wdróż nowy sekret i upewnij się, że stary przestał działać.
3. Sprawdź, czy stary sekret był użyty: logi dostawcy API, logi dostępu do bazy, CloudTrail w AWS, nietypowe działania.
4. Oceń skutki i, jeśli dotyczy to danych osobowych, uruchom proces zgłoszenia naruszenia (rozdział 10).
5. Usuń sekret z historii repozytorium (`git filter-repo`, BFG), jeśli ma to sens. Pamiętaj jednak, że istniejące klony, forki i cache nadal go mają, więc nie zastępuje to kroku 1.
6. Ustal, jak sekret trafił do repozytorium, i dodaj zabezpieczenie, żeby to się nie powtórzyło.

Zapobieganie działa na kilku poziomach:

- <a id="term-secret-scanning"></a>[skanowanie sekretów](00%20Glossary%20Security.md#secret-scanning): GitHub secret scanning i push protection blokują wypchnięcie commitu z rozpoznanym kluczem. Lokalnie robi to pre-commit z `gitleaks` albo `detect-secrets`,
- `.gitignore` z `.env`, `*.pem`, `*.key` i plikami lokalnych ustawień od pierwszego commita,
- filtry w konfiguracji logowania i Sentry, usuwające nagłówki `Authorization`, `Cookie` i pola z hasłami,
- krótko żyjące dane dostępowe tam, gdzie to możliwe (role IAM zamiast stałych kluczy, OIDC z CI do chmury zamiast kluczy w sekretach pipeline'u), bo taki sekret wygasa sam.

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.24.0
    hooks:
      - id: gitleaks
```

## Ustawienia produkcyjne

Kilka ustawień Django decyduje o bezpieczeństwie całej aplikacji. Większość z nich sprawdza `python manage.py check --deploy`.

<a id="term-debug-mode"></a>[Tryb debug](00%20Glossary%20Security.md#debug-mode) (`DEBUG = True`) to najpoważniejszy błąd konfiguracji Django. Strona błędu pokazuje ślad stosu z fragmentami kodu, zmienne lokalne (w tym dane użytkowników), ustawienia (część jest ukryta, jak opisano wyżej), listę adresów URL projektu i szczegóły zapytań SQL. Dodatkowo Django w trybie debug zapisuje wszystkie zapytania SQL w pamięci.

<a id="term-allowed-hosts"></a>[`ALLOWED_HOSTS`](00%20Glossary%20Security.md#allowed-hosts) to lista nazw domen, dla których Django obsłuży żądanie. Chroni przed atakami przez nagłówek `Host`. Django używa go do budowania pełnych adresów w linkach resetu hasła, przekierowaniach i e-mailach. Bez tej listy napastnik może wysłać żądanie z `Host: evil.example` i sprawić, że aplikacja wygeneruje prawdziwy e-mail z linkiem do jego domeny (rozdział 04). Przy `DEBUG = False` i pustej liście Django odrzuca wszystkie żądania.

Lista kontrolna ustawień produkcyjnych:

```python
# settings/production.py
DEBUG = False
ALLOWED_HOSTS = ["shop.example", "api.shop.example"]
CSRF_TRUSTED_ORIGINS = ["https://shop.example", "https://admin.shop.example"]   # ze schematem

SECURE_SSL_REDIRECT = True
SECURE_PROXY_SSL_HEADER = ("HTTP_X_FORWARDED_PROTO", "https")   # tylko gdy proxy ustawia i nadpisuje ten nagłówek
SECURE_HSTS_SECONDS = 60 * 60 * 24 * 365
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True

ADMIN_URL = env("DJANGO_ADMIN_URL")                      # nie /admin/
REST_FRAMEWORK = {
    "DEFAULT_PERMISSION_CLASSES": ["rest_framework.permissions.IsAuthenticated"],
    "DEFAULT_RENDERER_CLASSES": ["rest_framework.renderers.JSONRenderer"],   # bez browsable API
}
LOGGING = {...}                                          # błędy do monitoringu, bez danych wrażliwych
```

| Ustawienie | Ryzyko przy złej wartości |
|---|---|
| `DEBUG = True` | wyciek kodu, danych i konfiguracji na stronie błędu |
| `ALLOWED_HOSTS = ["*"]` | zatrucie linków resetu hasła i przekierowań przez nagłówek `Host` |
| `SECURE_PROXY_SSL_HEADER` bez proxy, które go nadpisuje | klient może udawać HTTPS, co wyłącza przekierowania i flagi |
| `SESSION_COOKIE_SECURE = False` | ciasteczko sesji wysłane przez HTTP może zostać podsłuchane |
| `CSRF_TRUSTED_ORIGINS` za szerokie | obejście ochrony CSRF z dodanych domen |
| admin pod `/admin/` bez ograniczeń | zgadywanie haseł pracowników, znana ścieżka |
| DRF browsable API i `AllowAny` | ujawnienie struktury API, dostęp bez logowania |
| wspólne konto bazy z prawem do DDL | błąd lub SQL injection może usunąć tabele |

Ustawienia dzieli się na moduły per środowisko (`base.py`, `local.py`, `production.py`), a `check --deploy --fail-level WARNING` z ustawieniami produkcyjnymi uruchamia się w CI. Dzięki temu regresja w konfiguracji zatrzymuje wdrożenie, zanim trafi na produkcję.

## Co zapamiętać

- Sekrety nie trafiają do repozytorium. Kolejne poziomy to `.env` lokalnie, zmienne środowiskowe na produkcji, menedżer sekretów i KMS dla kluczy szyfrowania.
- `SECRET_KEY` bez wartości domyślnej i `DEBUG` domyślnie `False`, czyli fail closed. Każda usługa ma własne dane dostępowe z minimalnym zakresem.
- Sekrety przeciekają przez logi, stronę błędu, Sentry i czaty. Filtr Django ukrywa tylko ustawienia o rozpoznawalnych nazwach.
- Po wycieku najpierw unieważnienie i rotacja, potem sprawdzenie użycia, a dopiero na końcu czyszczenie historii. Zapobiegają temu skanowanie sekretów, pre-commit, `.gitignore` i krótko żyjące dane dostępowe.
- `DEBUG = False`, konkretne `ALLOWED_HOSTS`, ciasteczka `Secure`, HSTS, ostrożne `SECURE_PROXY_SSL_HEADER`, ukryty admin i restrykcyjne domyślne uprawnienia DRF.
- `check --deploy` w CI z ustawieniami produkcyjnymi zatrzymuje regresje konfiguracji.

## Pytania sprawdzające

### 32. Jak trzymać sekrety poza repozytorium (zmienne środowiskowe, `django-environ`, vault, menedżery sekretów w chmurze)?

<details>
<summary>Odpowiedź</summary>

Sekrety (hasła, klucze API, klucze podpisu i szyfrowania, tokeny) nie trafiają do repozytorium, nawet prywatnego. Lokalnie służy do tego `.env` w `.gitignore` czytany przez `django-environ`, z `.env.example` w repozytorium. Na produkcji zmienne środowiskowe wypełnia menedżer sekretów (Vault, AWS Secrets Manager, GCP Secret Manager, Azure Key Vault) z audytem i rotacją, a klucze szyfrowania trzyma się w KMS. Obowiązuje fail closed: `SECRET_KEY` bez wartości domyślnej, `DEBUG` domyślnie `False`. Każda usługa dostaje własne, minimalne dane dostępowe. Trzeba też uważać na wycieki przez logi, stronę błędu i Sentry.

Zobacz: sekcja „Sekrety poza kodem”.

</details>

### 33. Co zrobić, gdy sekret trafił do repozytorium albo do logów?

<details>
<summary>Odpowiedź</summary>

Traktować go jak przejęty, bo boty skanują repozytoria w sekundy. Kolejność: unieważnić lub zrotować u źródła i wdrożyć nowy sekret, sprawdzić, czy stary był użyty (logi dostawcy, bazy, CloudTrail), ocenić skutki i ewentualnie zgłosić naruszenie, na końcu usunąć z historii (`git filter-repo`, BFG), co nie zastępuje rotacji, bo klony i cache zostają. Potem zapobieganie: GitHub secret scanning i push protection, pre-commit z `gitleaks` lub `detect-secrets`, `.gitignore`, filtry w logach i Sentry, krótko żyjące dane dostępowe (role IAM, OIDC z CI).

Zobacz: sekcja „Gdy sekret wycieknie”.

</details>

### 34. Jakie ustawienia Django są krytyczne na produkcji (`DEBUG`, `ALLOWED_HOSTS`, `SECURE_*`, `CSRF_TRUSTED_ORIGINS`, admin pod domyślnym adresem)?

<details>
<summary>Odpowiedź</summary>

`DEBUG = False`, bo strona błędu ujawnia kod, zmienne, ustawienia i SQL. Konkretne `ALLOWED_HOSTS`, bo nagłówek `Host` buduje linki resetu hasła. `SECURE_SSL_REDIRECT`, HSTS, `SESSION_COOKIE_SECURE` i `CSRF_COOKIE_SECURE`. `SECURE_PROXY_SSL_HEADER` tylko za proxy nadpisującym nagłówek. Wąskie `CSRF_TRUSTED_ORIGINS` ze schematem. Admin pod niestandardowym adresem i ograniczony siecią. W DRF domyślnie `IsAuthenticated` i bez browsable API. Osobne konto bazy bez DDL. Ustawienia per środowisko i `check --deploy` w CI.

Zobacz: sekcja „Ustawienia produkcyjne”.

</details>
