# Kontenery — ECS & EKS

**Opis**
Uruchamiasz kontenery Docker na skalę. **ECS** = prostszy, własny orkiestrator AWS. **EKS** = zarządzany Kubernetes — używasz zwykłego `kubectl`, AWS prowadzi control plane.

**Kluczowe koncepty**
- **Cluster** — pula, w której działają kontenery; w ECS to pula tasków, w EKS to Kubernetes.
- **Task / Task definition** (ECS) — co i jak uruchomić: obraz, CPU, RAM, porty.
- **Pod / Deployment** (EKS) — standardowe abstrakcje Kubernetes.
- **Fargate** — tryb serverless: AWS daje kontenerowi infrastrukturę, Ty nie widzisz serwerów.

**Key points**
- **ECS + Fargate**: kontenery bez żadnych serwerów (jak Lambda, ale dla kontenerów).
- **ECS na EC2**: zarządzasz instancjami sam — więcej kontroli, więcej roboty.
- **EKS**: kompatybilny z Kubernetes; świetny, jeśli już masz K8s aplikacje albo chcesz ekosystem.
- Oba integrują się z IAM, CloudTrailem i load balancerami od razu.

**Example (CLI)**
```bash
# ECS — cluster + task definition + start (Fargate)
aws ecs create-cluster --cluster-name prod

aws ecs register-task-definition --family api \
  --requires-compatibilities FARGATE --network-mode awsvpc \
  --cpu 256 --memory 512 \
  --containerDefinitions '[{"name":"api","image":"myrepo/api:3","essential":true,
    "portMappings":[{"containerPort":8080}]}]'

aws ecs run-task --cluster prod --task api:1 --launch-type FARGATE \
  --network-configuration "awsvpcConfiguration={subnets=[subnet-0abc],
    securityGroups=[sg-0abc],assignPublicIp=ENABLED}"

# co działa?
aws ecs list-tasks --cluster prod
aws ecs describe-tasks --cluster prod --tasks <task-arn>
```

```bash
# EKS — to po prostu Kubernetes
aws eks create-cluster --name prod --role-arn arn:aws:iam::123456789012:role/eks \
  --resources-vpc-config subnetIds=subnet-0abc

aws eks update-kubeconfig --name prod
kubectl get pods
kubectl apply -f deployment.yaml
kubectl logs deploy/api            # logi
kubectl rollout status deploy/api  # czy deploy się udał
```

**Pełny flow** — ECS: od obrazu do działającego taska:
```bash
# 1. utwórz repository ECR (gdzie leży obraz)
aws ecr create-repository --repository-name api
# -> arn:aws:ecr:us-east-1:123456789012:repository/api

# 2. zaloguj docker i wypchnij obraz
aws ecr get-login-password --region us-east-1 | \
  docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com
docker build -t api:3 .
docker tag api:3 123456789012.dkr.ecr.us-east-1.amazonaws.com/api:3
docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/api:3

# 3. utwórz cluster
aws ecs create-cluster --cluster-name prod

# 4. zarejestruj task definition (co uruchamiać)
aws ecs register-task-definition --family api \
  --requires-compatibilities FARGATE --network-mode awsvpc \
  --cpu 256 --memory 512 \
  --containerDefinitions '[{"name":"api",
    "image":"123456789012.dkr.ecr.us-east-1.amazonaws.com/api:3",
    "essential":true,"portMappings":[{"containerPort":8080}]}]'

# 5. uruchom taska (Fargate — bez serwerów)
aws ecs run-task --cluster prod --task api:1 --launch-type FARGATE \
  --network-configuration "awsvpcConfiguration={subnets=[subnet-0abc],
    securityGroups=[sg-0abc],assignPublicIp=ENABLED}"

# 6. zweryfikuj
aws ecs list-tasks --cluster prod
aws ecs describe-tasks --cluster prod --tasks <task-arn> \
  --query 'tasks[0].lastStatus'
# -> "RUNNING"
```
