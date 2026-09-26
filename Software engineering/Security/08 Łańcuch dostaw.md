# Łańcuch dostaw

Kod, który piszemy, to zwykle kilka procent kodu działającego na produkcji. Reszta to Django, DRF, Pillow, `requests`, sterowniki baz, ich zależności i zależności tych zależności, a do tego obraz Dockera, akcje GitHub i narzędzia w pipeline'ie. Każdy z tych elementów wykonuje się z pełnymi uprawnieniami aplikacji albo procesu budowania. Ten rozdział opisuje, jak ograniczyć ryzyko, które przychodzi z zewnątrz.

```text
pip install django-shop-utils
    │
    ├── Django, DRF, requests, Pillow ...           zależności bezpośrednie (requirements.in)
    │     └── urllib3, idna, certifi, ...           zależności przechodnie (nikt ich nie wybierał)
    ├── setup.py / hooki budowania                   kod wykonywany już przy instalacji
    └── CI: actions/checkout, obraz python:3.12      kod z dostępem do sekretów pipeline'u
```

## Ryzyka z cudzego kodu

<a id="term-supply-chain-attack"></a>[Atak na łańcuch dostaw](00%20Glossary%20Security.md#supply-chain-attack) (supply chain attack) to atak, który nie celuje w aplikację bezpośrednio, tylko w jej zależności, narzędzia albo proces budowania. Jedno przejęcie popularnej biblioteki daje dostęp do tysięcy aplikacji.

Rodzaje ryzyka, w tym <a id="term-typosquatting"></a>[typosquatting](00%20Glossary%20Security.md#typosquatting) i <a id="term-dependency-confusion"></a>[dependency confusion](00%20Glossary%20Security.md#dependency-confusion), opisane dokładniej pod tabelą:

| Ryzyko | Jak wygląda | Znany przykład |
|---|---|---|
| znana podatność w zależności | wersja biblioteki z opublikowanym CVE | podatności w Pillow, `urllib3`, samym Django |
| porzucony pakiet | brak łatek, brak opiekuna, nikt nie reaguje na zgłoszenia | wiele małych bibliotek Django bez wydań od lat |
| przejęte konto opiekuna | napastnik publikuje złośliwą wersję prawdziwego pakietu | `ctx` na PyPI (2022), `ua-parser-js` w npm (2021) |
| złośliwy nowy opiekun | przejęcie projektu przez socjotechnikę, powolne wprowadzanie backdoora | `xz-utils` (2024), `event-stream` w npm (2018) |
| typosquatting | pakiet o nazwie podobnej do popularnego | `reqeusts`, `python-dateutils`, `djanga` |
| dependency confusion | publiczny pakiet o nazwie wewnętrznego, z wyższą wersją | `torchtriton` w nocnych wydaniach PyTorch (2022) |
| przejęte narzędzie CI | złośliwa akcja albo skrypt w pipeline'ie | skrypt uploadera Codecov (2021), akcja `tj-actions/changed-files` (2025) |

Typosquatting wykorzystuje literówki przy instalacji. Złośliwy kod działa już podczas `pip install`, bo pakiety ze źródłami mogą wykonywać kod w czasie budowania.

Dependency confusion wykorzystuje konfigurację, w której `pip` szuka pakietu jednocześnie w wewnętrznym indeksie i w PyPI (`--extra-index-url`). Jeśli firma ma wewnętrzny pakiet `shop-common` w wersji 1.4, a napastnik opublikuje w PyPI `shop-common` 99.0, `pip` wybierze wyższą wersję z publicznego indeksu. Obroną jest jeden indeks, który pośredniczy w PyPI (np. Artifactory, devpi, AWS CodeArtifact) i ma pierwszeństwo dla nazw wewnętrznych, albo zarezerwowanie nazw wewnętrznych w PyPI.

Przy dodawaniu nowej zależności warto zadać kilka pytań:

- czy naprawdę jej potrzebujemy, czy to kilka linii kodu,
- czy nazwa jest dokładnie tą, o którą chodzi (skopiowana z oficjalnej dokumentacji, a nie wpisana z pamięci),
- czy projekt jest utrzymywany: ostatnie wydanie, reakcje na zgłoszenia, liczba opiekunów,
- ile zależności przechodnich dokłada,
- czy ma historię podatności i jak szybko je łatano.

## Skanowanie i przypinanie wersji

Ochrona przed znanymi podatnościami to <a id="term-sca"></a>[SCA](00%20Glossary%20Security.md#sca) (Software Composition Analysis): automatyczne porównywanie listy zależności z bazami podatności (PyPI Advisory Database, OSV, GitHub Advisory Database).

```bash
pip-audit -r requirements.txt               # sprawdza zależności z pliku
pip-audit --fix -r requirements.txt         # proponuje wersje z poprawką
```

W praktyce działają trzy warstwy:

- `pip-audit` w CI, które przerywa build przy podatności o wysokiej wadze,
- Dependabot albo Renovate, które otwierają pull requesty z aktualizacjami i informacjami o podatnościach,
- alerty GitHub Dependabot dla repozytorium.

Skanowanie działa tylko wtedy, gdy wiadomo dokładnie, co jest zainstalowane. Dlatego wersje się przypina. Plik wejściowy zawiera zależności bezpośrednie z zakresami, a plik zablokowany (lockfile) pełne drzewo z dokładnymi wersjami i hashami:

```text
# requirements.in: to, czego świadomie używamy
Django>=5.2,<5.3
djangorestframework>=3.15
Pillow
```

```bash
pip-compile --generate-hashes requirements.in -o requirements.txt    # albo: uv pip compile
pip install --require-hashes -r requirements.txt                    # w CI i w obrazie Dockera
```

```text
# requirements.txt (fragment wygenerowany)
django==5.2.6 \
    --hash=sha256:...
sqlparse==0.5.3 \
    --hash=sha256:...
    # via django
```

Hashe gwarantują, że instalowany jest dokładnie ten plik, który sprawdzono przy aktualizacji. Nawet jeśli ktoś podmieni pakiet w indeksie pod tą samą wersją, instalacja się nie powiedzie. Przypięte wersje nie oznaczają jednak braku aktualizacji. Aktualizuje się je regularnie przez pull requesty Dependabota, z pełnymi testami.

<a id="term-sbom"></a>[SBOM](00%20Glossary%20Security.md#sbom) (Software Bill of Materials) to spis wszystkich składników oprogramowania z wersjami, w formacie CycloneDX albo SPDX. Pozwala szybko odpowiedzieć na pytanie „czy któryś z naszych systemów używa podatnej wersji X?”, gdy pojawia się poważna podatność. Coraz częściej wymagają go klienci korporacyjni i regulacje, np. europejski Cyber Resilience Act.

```bash
cyclonedx-py requirements requirements.txt -o sbom.json
```

## Pipeline jako cel ataku

Pipeline CI/CD ma dostęp do najcenniejszych sekretów: kluczy do produkcji, tokenów publikacji i danych dostępowych do chmury. Przejęcie pipeline'u daje więcej niż przejęcie aplikacji.

Zasady dla GitHub Actions, które przenoszą się też na inne systemy CI:

```yaml
permissions:
  contents: read                              # minimalne uprawnienia tokenu GITHUB_TOKEN

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      # SHA przykładowe: pełny SHA wydania sprawdza się w repozytorium akcji
      - uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683   # przypięta do SHA, nie do tagu
      - uses: actions/setup-python@0b93645e9fea7318ecaed2b359559ac225c90a2b
        with:
          python-version: "3.12"
      - run: pip install --require-hashes -r requirements.txt
      - run: pip-audit -r requirements.txt
      - run: python manage.py check --deploy --fail-level WARNING
        env:
          DJANGO_SETTINGS_MODULE: shop.settings.production
```

- minimalne uprawnienia tokenu pipeline'u, domyślnie tylko odczyt,
- akcje zewnętrzne przypięte do pełnego SHA commita, a nie do taga, który można przesunąć (tak rozprzestrzenił się atak na `tj-actions/changed-files`),
- sekrety niedostępne dla pull requestów z forków. `pull_request_target` uruchamia się z sekretami, więc nie wolno w nim budować ani uruchamiać kodu z forka,
- OIDC do chmury zamiast stałych kluczy w sekretach: pipeline dostaje krótko żyjące dane dostępowe tylko dla określonego repozytorium i gałęzi,
- wdrożenia na produkcję tylko z chronionej gałęzi, po wymaganym review i przez osobne środowisko z zatwierdzeniem,
- podpisywanie artefaktów i obrazów (Sigstore, `cosign`), żeby wdrożenie mogło sprawdzić, że obraz pochodzi z naszego pipeline'u. Dla paczek w PyPI służy trusted publishing z atestacjami.

Ramy takie jak SLSA (Supply-chain Levels for Software Artifacts) porządkują te praktyki w poziomy dojrzałości.

## Wydania bezpieczeństwa Django

Django ma dojrzały proces obsługi podatności, a znajomość tego procesu jest częścią pracy z frameworkiem:

- podatności zgłasza się prywatnie na `security@djangoproject.com`, a nie w publicznym trackerze,
- zespół bezpieczeństwa przygotowuje poprawki dla wszystkich wspieranych wersji,
- około tydzień przed publikacją dystrybucje i duzi użytkownicy dostają wcześniejsze powiadomienie,
- poprawki ukazują się jednocześnie dla wszystkich wspieranych wersji, z opisem na blogu Django i na liście `django-announce`,
- wersje LTS (np. 4.2, 5.2) mają wsparcie bezpieczeństwa przez około trzy lata. Pozostałe wersje są wspierane krócej, do czasu wydania kolejnych.

Praktyka dla zespołu:

- korzystać z wersji wspieranej, najlepiej LTS w projektach o długim cyklu życia, i planować przejście na kolejną przed końcem wsparcia,
- zapisać się na `django-announce` albo śledzić wydania przez Dependabota,
- mieć proces szybkiego wdrażania wydań poprawkowych (np. 5.2.5 do 5.2.6): pełne testy, wdrożenie w ciągu dni, a nie miesięcy. Wydania poprawkowe Django nie wprowadzają zmian niekompatybilnych, więc ryzyko aktualizacji jest niskie,
- po każdym wydaniu bezpieczeństwa przeczytać opis i sprawdzić, czy projekt używa podatnej funkcji. Pomaga to ocenić pilność i dostarcza wiedzy, np. o podatnościach SQL injection w nazwach kolumn z rozdziału 02,
- to samo dotyczy DRF, Pillow i innych kluczowych zależności.

## Co zapamiętać

- Atak na łańcuch dostaw celuje w zależności, narzędzia i pipeline. Ryzyka to znane CVE, porzucone pakiety, przejęte konta, typosquatting, dependency confusion i przejęte narzędzia CI.
- Nowe zależności dodaje się świadomie: czy potrzebna, dokładna nazwa, utrzymanie, drzewo zależności.
- SCA (`pip-audit`, Dependabot, Renovate) w CI wykrywa znane podatności. Lockfile z hashami i `--require-hashes` gwarantuje, że instalowane jest dokładnie to, co sprawdzono.
- SBOM pozwala szybko sprawdzić, gdzie używana jest podatna wersja.
- Pipeline: minimalne uprawnienia tokenu, akcje przypięte do SHA, brak sekretów dla forków, OIDC zamiast kluczy, chronione wdrożenia i podpisywanie artefaktów.
- Django wydaje łatki dla wszystkich wspieranych wersji. Warto używać wersji LTS, śledzić `django-announce` i wdrażać wydania poprawkowe w ciągu dni.

## Pytania sprawdzające

### 35. Jakie ryzyka niosą zależności (podatne wersje, porzucone pakiety, typosquatting, przejęte konta opiekunów)?

<details>
<summary>Odpowiedź</summary>

Kod zależności działa z uprawnieniami aplikacji, a często już przy instalacji. Ryzyka to znane podatności w wersjach, porzucone pakiety bez łatek, przejęte konta opiekunów publikujące złośliwe wersje (`ctx`, `ua-parser-js`), złośliwi nowi opiekunowie (`xz-utils`, `event-stream`), typosquatting (pakiety z literówką w nazwie), dependency confusion (publiczny pakiet o nazwie wewnętrznego z wyższą wersją, jak `torchtriton`) i przejęte narzędzia CI. Nowe zależności dodaje się świadomie: potrzeba, dokładna nazwa, utrzymanie, drzewo zależności.

Zobacz: sekcja „Ryzyka z cudzego kodu”.

</details>

### 36. Jak skanować zależności i reagować na podatności (`pip-audit`, Dependabot, SBOM, przypinanie wersji i hashy)?

<details>
<summary>Odpowiedź</summary>

Przez SCA: `pip-audit` w CI przerywa build przy poważnej podatności, a Dependabot lub Renovate otwierają PR-y z aktualizacjami i alertami. Wersje przypina się w lockfile z pełnym drzewem i hashami (`pip-compile --generate-hashes` lub `uv`), a instaluje przez `--require-hashes`, więc podmieniony plik nie zostanie zainstalowany. Przypięte wersje aktualizuje się regularnie z testami. SBOM (CycloneDX, SPDX) pozwala szybko sprawdzić, czy gdziekolwiek jest podatna wersja, i jest coraz częściej wymagany.

Zobacz: sekcja „Skanowanie i przypinanie wersji”.

</details>

### 37. Jak zabezpieczyć CI/CD (sekrety w pipeline'ie, uprawnienia tokenów, pull requesty z forków, podpisywanie artefaktów)?

<details>
<summary>Odpowiedź</summary>

Pipeline ma najcenniejsze sekrety, więc potrzebuje: minimalnych uprawnień `GITHUB_TOKEN` (domyślnie odczyt), akcji przypiętych do SHA zamiast tagów (tagi można przesunąć, jak w `tj-actions/changed-files`), braku sekretów dla PR-ów z forków (ostrożnie z `pull_request_target`), OIDC do chmury zamiast stałych kluczy, wdrożeń tylko z chronionej gałęzi po review i z zatwierdzeniem środowiska oraz podpisywania artefaktów i obrazów (Sigstore, `cosign`, trusted publishing z atestacjami). SLSA porządkuje te praktyki w poziomy.

Zobacz: sekcja „Pipeline jako cel ataku”.

</details>

### 38. Jak śledzić wydania bezpieczeństwa Django i jak szybko wdrażać łatki?

<details>
<summary>Odpowiedź</summary>

Django przyjmuje zgłoszenia prywatnie (`security@djangoproject.com`), wcześniej powiadamia dystrybucje i publikuje łatki jednocześnie dla wszystkich wspieranych wersji, z opisem na blogu i na liście `django-announce`. Wersje LTS mają wsparcie przez około trzy lata. Zespół powinien używać wspieranej wersji (najlepiej LTS), subskrybować `django-announce` lub korzystać z Dependabota, wdrażać wydania poprawkowe w ciągu dni (nie łamią kompatybilności), czytać opis każdej podatności, żeby ocenić pilność, i robić to samo dla DRF, Pillow i innych kluczowych zależności.

Zobacz: sekcja „Wydania bezpieczeństwa Django”.

</details>
