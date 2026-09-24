# AWS Services for Developers — Spis treści

Każda usługa w osobnym pliku, w stałym układzie: **Opis** → **Kluczowe koncepty** → **Key points** → **Example** (krótkie komendy) → **Pełny flow** (krok po kroku od zera do działającego rezultatu). Shell/CLI tam, gdzie pasuje, Python tam, gdzie to naturalne.

| # | Usługa | Plik | Jedno zdanie |
|---|--------|------|--------------|
| 1 | S3 | [01-s3.md](01-s3.md) | Nieskończony chmurny dysk: buckety z obiektami, po nazwie. |
| 2 | RDS / Aurora | [02-rds.md](02-rds.md) | Zwykły Postgres/MySQL w chmurze, AWS prowadzi serwer. |
| 3 | Secrets & Parameters | [03-secrets.md](03-secrets.md) | Sejf na hasła (rotacja) + chmurny plik konfiguracyjny. |
| 4 | EC2 | [04-ec2.md](04-ec2.md) | Wynajem wirtualnego serwera z pełnym rootem. |
| 5 | Lambda | [05-lambda.md](05-lambda.md) | Uruchamiasz tylko funkcję, płacisz za ms, zero serwerów. |
| 6 | CloudWatch | [06-cloudwatch.md](06-cloudwatch.md) | Metryki, logi i alerty dla całego konta. |
| 7 | ECS / EKS | [07-containers.md](07-containers.md) | Kontenery na skalę: prosty ECS albo Kubernetes (EKS). |
| 8 | AMI | [08-ami.md](08-ami.md) | Zamrożony obraz serwera — identyczna instancja w sekundy. |
| 9 | CodeBuild / CodePipeline | [09-cicd.md](09-cicd.md) | CI: build + testy, i taśma: source → build → deploy. |
