# RDS — Relational Database Service (i Aurora)

**Opis**
RDS to po prostu zwykły serwer Postgres/MySQL w chmurze. Łączysz się normalnym klientem — AWS zajmuje się serwerem, backupami, patchami i failoverem.

**Kluczowe koncepty**
- **DB instance** — wirtualny serwer z silnikiem bazy; łączysz się z nim jak z każdą inną bazą.
- **Engine** — który SQL: PostgreSQL, MySQL, Oracle, SQL Server.
- **Aurora** — własny silnik AWS (kompatybilny z MySQL/Postgres), zbudowany pod chmurę.
- **Multi-AZ** — standby replika w innej strefie dostępności; przy awarii ruch przełącza się sam.
- **Backup** — automatyczne backupy + snapshoty na żądanie.

**Key points**
- Silniki: MySQL, PostgreSQL, Oracle, SQL Server.
- **Aurora**: własny silnik AWS, kompatybilny z MySQL/Postgres, zbudowany pod chmurę (szybszy, więcej replik).
- **Multi-AZ**: standby replika w innej strefie — gdy baza padnie, ruch sam przełącza się na replikę.

**Example** — to zwykłe połączenie z bazą:
```bash
psql "host=mydb.abc123.us-east-1.rds.amazonaws.com dbname=app user=admin" \
  -c "SELECT 1"
```

```python
import psycopg2

conn = psycopg2.connect(host="mydb.abc123.us-east-1.rds.amazonaws.com",
                        user="admin", password="secret", dbname="app")
with conn.cursor() as cur:
    cur.execute("SELECT id, name FROM users LIMIT 5")
    for row in cur.fetchall():
        print(row)
```

Zarządzanie instancją:
```bash
aws rds describe-db-instances --db-instance-identifier mydb
aws rds stop-db-instance --db-instance-identifier mydb
aws rds start-db-instance --db-instance-identifier mydb

# zmiana rozmiaru (np. podwojenie)
aws rds modify-db-instance --db-instance-identifier mydb \
  --db-instance-class db.r6g.large --apply-immediately
```

Backup i restore:
```bash
# snapshot na żądanie
aws rds create-db-snapshot --db-instance-identifier mydb \
  --db-snapshot-identifier mydb-before-migration

# nowa instancja ze snapshotu
aws rds restore-db-instance-from-db-snapshot \
  --db-instance-identifier mydb-restore \
  --db-snapshot-identifier mydb-before-migration
```

**Pełny flow** — od zera do działającej bazy:
```bash
# 1. utwórz instancję (Postgres, najtańszy typ, w VPC)
aws rds create-db-instance \
  --db-instance-identifier mydb \
  --db-instance-class db.t3.micro \
  --engine postgres --allocated-storage 20 \
  --master-username admin --master-password 'Str0ng!Pass' \
  --db-name app \
  --vpc-security-group-ids sg-0abc \
  --availability-zone us-east-1a

# 2. poczekaj, aż stanie się available (może chwilę trwać)
aws rds wait db-instance-available --db-instance-identifier mydb

# 3. odczytaj endpoint (adres hosta)
aws rds describe-db-instances --db-instance-identifier mydb \
  --query 'DBInstances[0].Endpoint'
# -> {"Address": "mydb.abc123.us-east-1.rds.amazonaws.com", "Port": 5432}

# 4. połącz się i utwórz tabelę
psql "host=mydb.abc123.us-east-1.rds.amazonaws.com dbname=app user=admin" \
  -c "CREATE TABLE users (id serial primary key, name text);" \
  -c "INSERT INTO users (name) VALUES ('ada');"

# 5. odczytaj
psql "host=mydb.abc123.us-east-1.rds.amazonaws.com dbname=app user=admin" \
  -c "SELECT * FROM users;"
```
