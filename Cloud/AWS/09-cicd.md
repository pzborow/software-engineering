# CI/CD — CodeBuild & CodePipeline

**Opis**
**CodeBuild** = runner CI: "skompletuj, przetestuj, wyprodukuj artefakt". **CodePipeline** = taśma montażowa łącząca etapy: source → build → test → deploy, automatycznie przy każdym pushu.

**Kluczowe koncepty**
- **buildspec.yml** — przepis na build w CodeBuild: fazy install → build → test.
- **Pipeline** — uporządkowane etapy (source → build → deploy); każdy etap to serwis AWS.
- **Source** — skąd bierze się kod: GitHub, CodeCommit, S3.
- **Artifact** — wynik etapu (np. zip do deployu), przekazywany dalej.

**Key points**
- CodeBuild: build definiowany w `buildspec.yml` (fazy install → build → test).
- CodePipeline: uporządkowane etapy; każdy może to być CodeBuild, deploy do ECS, Lambda itd.
- Triggery z GitHuba, CodeCommitu albo ręcznie start; w pełni konfigurowalne.

`buildspec.yml` w repozytorium:
```yaml
version: 0.2
phases:
  install:
    runtime: python3.12
  build:
    commands:
      - pip install -r requirements.txt
      - pytest
  post_build:
    commands:
      - echo "gotowe do deployu"
artifacts:
  files:
    - "**/*"
```

**Example (AWS CLI)**
```bash
# projekt buildowy + start
aws codebuild create-project --name app-build \
  --source type=GITHUB,location=github.com/me/app,buildspec=buildspec.yml \
  --artifacts type=CODEPIPELINE
aws codebuild start-build --project-name app-build

# status + logi
aws codebuild list-builds --project-name app-build \
  --query 'builds[0].[buildId,buildStatus]'
aws codebuild tail-build-log --build-id <build-id>

# pipeline: uruchom i sprawdź stan etapów
aws codepipeline start-pipeline-execution --name app-pipeline
aws codepipeline get-pipeline-state --name app-pipeline \
  --query 'stageStates[*].[stageName,status]'
```

**Pełny flow** — od repozytorium do działającego pipeline'u:
```bash
# 1. w repozytorium masz buildspec.yml (patrz wyżej) i kod

# 2. utwórz projekt CodeBuild (source = GitHub, buildspec z repo)
aws codebuild create-project --name app-build \
  --source type=GITHUB,location=github.com/me/app,buildspec=buildspec.yml \
  --artifacts type=CODEPIPELINE
# -> arn:aws:codebuild:us-east-1:123456789012:project/app-build

# 3. utwórz pipeline: source (GitHub) -> build (CodeBuild) -> deploy
aws codepipeline create-pipeline --name app-pipeline \
  --pipeline '{"name":"app-pipeline",
    "stages":[
      {"name":"Source","actions":[{"name":"Source","actionTypeId":{"category":"Source","provider":"CodeStarSourceConnection"},
        "configuration":{"ConnectionArn":"arn:aws:codestar-connections:...","RepositoryName":"me/app"},
        "outputs":[{"name":"SourceArtifact"}]}]},
      {"name":"Build","actions":[{"name":"Build","actionTypeId":{"category":"Build","provider":"CodeBuild"},
        "configuration":{"ProjectName":"app-build"},
        "inputArtifacts":[{"name":"SourceArtifact"}]}]}
    ]}'

# 4. startuj pipeline (ręcznie albo automatycznie przy pushu)
aws codepipeline start-pipeline-execution --name app-pipeline

# 5. śledź stan etapów
aws codepipeline get-pipeline-state --name app-pipeline \
  --query 'stageStates[*].[stageName,status]'
# -> ["Source", "Succeeded"], ["Build", "InProgress"]

# 6. po zakończeniu — logi builda
aws codebuild list-builds --project-name app-build --query 'builds[0].buildId'
aws codebuild tail-build-log --build-id <build-id>
```
