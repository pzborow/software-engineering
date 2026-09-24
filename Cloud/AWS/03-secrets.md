# Secrets Manager & Parameter Store

**Opis**
Przestań hardcodować hasła. **Secrets Manager** = sejf na kredencjały, który potrafi się sam rotować. **Parameter Store** = plik konfiguracyjny w chmurze (hierarchia klucz/wartość).

**Kluczowe koncepty**
- **Secret** — wartości wrażliwe (hasła, API keys, tokens); Secrets Manager potrafi je **rotować** automatycznie.
- **Parameter** — klucz/wartość w hierarchii, np. `/app/prod/db_url`; zwykły tekst, lista albo SecureString (zaszyfrowany).
- **KMS** — oba szyfrują dane w spoczynku kluczami KMS.
- **Dostęp** — kontrola przez IAM + logi dostępu w CloudTrailu.

**Key points**
- Secrets Manager: kredencjały do DB, API keys, OAuth tokens; **auto-rotacja** (np. hasło do RDS zmienia się samo co 30 dni).
- Parameter Store: zwykłe stringi, listy, albo zaszyfrowane (SecureString); ścieżki hierarchiczne typu `/app/prod/db_url`.
- Oba szyfrują KMS-em i logują dostęp do CloudTraila.
- Zasada: rotujące kredencjały → Secrets Manager; konfig aplikacji / feature flags → Parameter Store (standardowe parametry są darmowe).

**Example (AWS CLI)**
```bash
# Secrets Manager — odczyt sekretu JSON (typowo: kredencjały do RDS)
aws secretsmanager get-secret-value --secret-id prod/db --query SecretString
# -> {"username": "admin", "password": "rotated-..."}

# utworzenie sekretu + włączenie auto-rotacji co 30 dni
aws secretsmanager create-secret \
  --name prod/db \
  --secret-string '{"username":"admin","password":"tmp","host":"mydb.abc123.rds.amazonaws.com"}' \
  --rotation-enabled --rotation-days 30

# zmiana wartości
aws secretsmanager put-secret-value --secret-id prod/db \
  --secret-string '{"username":"admin","password":"new-pass"}'
```

```bash
# Parameter Store — zwykła wartość konfiguracyjna
aws ssm get-parameter --name /app/feature_flags/new_ui --query Parameter.Value

# zapis: zwykły + zaszyfrowany (SecureString)
aws ssm put-parameter --name /app/prod/log_level --value info --type String
aws ssm put-parameter --name /app/prod/api_key --value sk-abc --type SecureString

# lista parametrów pod ścieżką (jak "katalog")
aws ssm describe-parameters --path /app/prod --recursive \
  --query 'Parameters[*].[Name,Type]'
```

**Pełny flow** — sekret + odczyt z aplikacji:
```bash
# 1. utwórz sekret z kredencjałami do bazy
aws secretsmanager create-secret --name prod/db \
  --secret-string '{"username":"admin","password":"tmp","host":"mydb.rds.amazonaws.com"}'

# 2. utwórz parametry konfiguracyjne (hierarchia)
aws ssm put-parameter --name /app/prod/log_level --value info --type String
aws ssm put-parameter --name /app/prod/timeout_ms --value 5000 --type String

# 3. odczyt z aplikacji (Python + boto3) — bez hardcodowania
```
```python
import boto3, json

sm = boto3.client("secretsmanager")
secret = json.loads(sm.get_secret_value(SecretId="prod/db")["SecretString"])
# -> {"username": "admin", "password": "tmp", "host": "mydb.rds.amazonaws.com"}

ssm = boto3.client("ssm")
log_level = ssm.get_parameter(Name="/app/prod/log_level")["Parameter"]["Value"]  # "info"
```
```bash
# 4. włącz auto-rotację (Secrets Manager sam zmieni hasło w RDS co 30 dni)
aws secretsmanager rotate-secret --secret-id prod/db --rotation-days 30

# 5. zweryfikuj — po rotacji hasło się zmieniło, a aplikacja nadal działa
aws secretsmanager get-secret-value --secret-id prod/db --query SecretString
```
