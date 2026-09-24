# CloudWatch

**Opis**
Dasboard + alarm przeciwpożarowy Twojego konta AWS: liczby (metryki), logi i alerty, które odpalają się, gdy coś przekroczy próg.

**Kluczowe koncepty**
- **Metric** — liczba w czasie: CPU, requesty, latency; każdy serwis AWS je emituje.
- **Log group / stream** — struktura logów: grupa = np. funkcja Lambda, stream = jedno uruchomienie.
- **Alarm** — warunek ("CPU > 80% przez 5 min") + akcja (powiadomienie, scale up).
- **Dashboard** — zbiorcze widoki metryk.

**Key points**
- **Metryki**: CPU, pamięć, liczba requestów, latency — każdy serwis AWS je emituje.
- **Logi**: pliki logów z Lambda, EC2, ECS itd.
- **Alerty**: np. "CPU > 80% przez 5 minut" → powiadomienie na Slack / scale up / restart.

**Example (AWS CLI)**
```bash
# własna metryka (np. licznik requestów w swojej aplikacji)
aws cloudwatch put-metric-data --namespace my-app \
  --metric-data MetricName=requests,Value=1

# odczyt metryki
aws cloudwatch get-metric-statistics --namespace my-app --metric-name requests \
  --start-time 2026-09-15T00:00:00Z --end-time 2026-09-15T23:59:59Z \
  --period 3600 --statistics Average

# CPU instancji EC2 (metryki wbudowane — nie trzeba nic zgłaszać)
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization \
  --dimensions Name=InstanceId,Value=i-0abc123 \
  --start-time 2026-09-15T00:00:00Z --period 3600 --statistics Average
```

Logi:
```bash
# logi z Lambda
aws logs get-log-events --log-group-name /aws/lambda/hello \
  --log-stream-name 2026-09-15

# wyszukaj błędy we wszystkich logach grupy (jak grep)
aws logs filter-log-events --log-group-name /aws/lambda/hello \
  --filter-pattern "ERROR" --query 'events[*].message'
```

Alarmy:
```bash
# alarm: CPU > 80% przez 5 minut -> powiadomienie na e-mail
aws cloudwatch put-metric-alarm \
  --alarm-name "high-cpu" \
  --namespace AWS/EC2 --metric-name CPUUtilization \
  --dimensions Name=InstanceId,Value=i-0abc123 \
  --threshold 80 --comparison-operator GreaterThanThreshold \
  --evaluation-periods 1 --period 300 \
  --alarm-actions arn:aws:sns:us-east-1:123456789012:ops-alerts
```

**Pełny flow** — metryka → alarm → powiadomienie na e-mail:
```bash
# 1. zgłoś własną metrykę (np. licznik błędów w aplikacji)
aws cloudwatch put-metric-data --namespace my-app \
  --metric-data MetricName=errors,Value=1

# 2. utwórz topic SNS (kanał powiadomień)
aws sns create-topic --name ops-alerts
# -> {"TopicArn": "arn:aws:sns:us-east-1:123456789012:ops-alerts"}

# 3. zasubskrybuj e-mail
aws sns subscribe --topic-arn arn:aws:sns:us-east-1:123456789012:ops-alerts \
  --protocol email --notification-endpoint you@example.com
# (potwierdź subskrypcję w mailu)

# 4. utwórz alarm: > 5 błędów na minutę -> powiadom
aws cloudwatch put-metric-alarm \
  --alarm-name "too-many-errors" \
  --namespace my-app --metric-name errors \
  --threshold 5 --comparison-operator GreaterThanThreshold \
  --evaluation-periods 1 --period 60 \
  --alarm-actions arn:aws:sns:us-east-1:123456789012:ops-alerts

# 5. zweryfikuj stan alarmu
aws cloudwatch describe-alarms --alarm-names too-many-errors \
  --query 'MetricAlarms[*].[AlarmName,State.Value]'
# -> ["too-many-errors", "OK"]
```
