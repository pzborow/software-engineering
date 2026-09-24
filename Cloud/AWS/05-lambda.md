# Lambda — Serverless Computing

**Opis**
Wgrywasz tylko *funkcję*. AWS uruchamia ją, gdy coś się wydarzy (request HTTP, nowy plik w S3, ...) i płacisz za milisekundy wykonania. Zero serwerów do zarządzowania, na zawsze.

**Kluczowe koncepty**
- **Function** — kod + runtime (Python, Node, ...); ma `handler`, który AWS wywołuje.
- **Trigger / event** — co ją odpala: HTTP (API Gateway), nowy plik w S3, timer, DynamoDB...
- **Concurrency** — ile kopii może działać równolegle; domyślnie skaluje się samo, można rezerwować.
- **Environment variables** — konfig bez kodu (albo link do Secrets Manager).

**Key points**
- **Event-driven**: mogą ją odpalić S3, DynamoDB, API Gateway, timer, albo zwykły HTTP.
- Wiele runtime'ów (Python, Node.js, Java, Go, ...) albo własny kontener.
- **Concurrency**: domyślnie skaluje się do tysięcy równoległych wywołań; można rezerwować/provisionować concurrency, by to kontrolować.
- Deploy: zip upload, obraz kontenera, albo **AWS SAM** (infrastruktur jako kod).

**Example** — sama funkcja to Python (sygnatura `handler` jest wymagana):
```python
import json

def handler(event, context):
    # event: to, co wysłał trigger (np. rekord z S3, ciało requestu)
    print("wchodzę do lambda", event)          # print trafia do CloudWatch Logs
    return {"statusCode": 200, "body": json.dumps({"ok": True})}
```

Deploy i test przez CLI:
```bash
zip function.zip handler.py
aws lambda create-function --function-name hello --runtime python3.12 \
  --zip-file fileb://function.zip --handler handler.handler

aws lambda invoke --function-name hello out.json
cat out.json   # -> {"statusCode": 200, "body": "{\"ok\": true}"}
```

Codzienne operacje:
```bash
# podgląd funkcji, logi ostatniego wywołania
aws lambda list-functions --query 'Functions[*].FunctionName'
aws logs get-log-events --log-group-name /aws/lambda/hello \
  --log-stream-name $(aws logs describe-log-streams --log-group-name /aws/lambda/hello \
    --query 'sort_by(logStreams, &lastEventTimestamp)[-1].logStreamName' --output text)

# zaktualizuj kod bez zmiany konfiguracji
aws lambda update-function-code --function-name hello --zip-file fileb://function.zip

# zmienna środowiskowa (np. nazwa bazy)
aws lambda update-function-configuration --function-name hello \
  --environment Variables={DB_HOST=mydb.rds.amazonaws.com}

# trigger: nowy plik w S3 odpala funkcję
aws lambda add-permission --function-name hello \
  --statement-id s3-trigger --action lambda:InvokeFunction --principal s3.amazonaws.com
aws s3api put-bucket-notification-configuration --bucket my-bucket \
  --notification-configuration '{"LambdaFunctionConfigurations":[
    {"Id":"to-lambda","LambdaFunctionArn":"arn:aws:lambda:...:function:hello","Events":["s3:ObjectCreated"]}]}'
```

**Pełny flow** — S3 → Lambda (co to znaczy "triggerowany przez S3"):

Kiedy wrzucisz plik do bucketa, S3 wysyła event `s3:ObjectCreated`. Jeśli bucket ma
powiadomienie skierowane do Twojej funkcji, Lambda jest wywoływana automatycznie —
bez żadnego kodu po stronie S3. `event` w `handler` zawiera dane o nowym pliku.

```python
# handler.py — funkcja, która "przetwarza" każdy nowy plik z S3
import json, boto3

s3 = boto3.client("s3")

def handler(event, context):
    # event["Records"][0] to informacja o nowym obiekcie
    bucket = event["Records"][0]["s3"]["Bucket"]["name"]
    key    = event["Records"][0]["s3"]["Object"]["key"]

    body = s3.get_object(Bucket=bucket, Key=key)["Body"].read().decode()
    print(f"przetwarzam {key}: {body!r}")   # tu Twoja logika

    # np. zapisz wynik do innego bucketa
    s3.put_object(Bucket="my-bucket", Key=f"processed/{key}", Body=body.upper())
    return {"ok": True, "key": key}
```

```bash
# 1. utwórz funkcję
zip function.zip handler.py
aws lambda create-function --function-name s3-processor --runtime python3.12 \
  --zip-file fileb://function.zip --handler handler.handler \
  --role arn:aws:iam::123456789012:role/lambda-role

# 2. daj S3 pozwolenie na wywołanie funkcji
aws lambda add-permission --function-name s3-processor \
  --statement-id s3-trigger --action lambda:InvokeFunction --principal s3.amazonaws.com

# 3. podłącz bucket do funkcji (event: nowy obiekt)
aws s3api put-bucket-notification-configuration --bucket my-bucket \
  --notification-configuration '{"LambdaFunctionConfigurations":[
    {"Id":"to-lambda",
     "LambdaFunctionArn":"arn:aws:lambda:us-east-1:123456789012:function:s3-processor",
     "Events":["s3:ObjectCreated"]}]}'

# 4. TEST — wrzuć plik i patrz, jak Lambda sama się uruchamia
aws s3 cp hello.txt s3://my-bucket/incoming/hello.txt
aws logs tail /aws/lambda/s3-processor --follow
# -> przetwarzam incoming/hello.txt: 'hello'
# -> ok: True, key: incoming/hello.txt
```
