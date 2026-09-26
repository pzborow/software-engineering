# Kryptografia dla programisty

Programista aplikacji nie projektuje algorytmów kryptograficznych, ale ciągle ich używa: przy hasłach, podpisanych linkach, webhookach, szyfrowaniu danych wrażliwych, tokenach i TLS. Najważniejsza umiejętność to wiedzieć, którego narzędzia użyć do jakiego celu, i nie wymyślać własnych. Ten rozdział porządkuje podstawowe pojęcia i pokazuje, co daje Django i biblioteka standardowa Pythona.

```text
potrzeba                                  narzędzie                        w Pythonie / Django
sprawdzić, czy dane się nie zmieniły      hash                             hashlib.sha256
przechować hasło                          funkcja do haseł                 PASSWORD_HASHERS (rozdział 04)
ukryć dane, a potem je odczytać           szyfrowanie                      cryptography: Fernet, AESGCM
potwierdzić, że dane pochodzą od nas      HMAC / podpis                    django.core.signing, hmac
losowy token, klucz, identyfikator        CSPRNG                           secrets
```

## Trzy różne cele

Te trzy operacje są często mylone, a mają zupełnie różne cele.

<a id="term-hash-function"></a>[Funkcja skrótu](00%20Glossary%20Security.md#hash-function) (hash) zamienia dane dowolnej długości w krótki odcisk o stałej długości. Jest jednokierunkowa: z odcisku nie da się odtworzyć danych. Ta sama treść zawsze daje ten sam odcisk, a najmniejsza zmiana daje zupełnie inny. Służy do sprawdzania integralności (suma kontrolna pliku), deduplikacji i jako element innych konstrukcji. Nie zapewnia poufności ani autentyczności: każdy może policzyć hash zmienionych danych.

<a id="term-encryption"></a>[Szyfrowanie](00%20Glossary%20Security.md#encryption) zamienia dane w szyfrogram, który da się odczytać tylko z kluczem. Zapewnia poufność. Szyfrowanie symetryczne (AES) używa jednego klucza do szyfrowania i odszyfrowania. Asymetryczne (RSA, krzywe eliptyczne) używa pary kluczy: publicznego do szyfrowania i prywatnego do odszyfrowania.

<a id="term-hmac"></a>[HMAC](00%20Glossary%20Security.md#hmac) (Hash-based Message Authentication Code) to odcisk liczony z danych i wspólnego sekretu. Tylko ktoś, kto zna sekret, może go poprawnie policzyć, więc HMAC potwierdza integralność i autentyczność między stronami, które dzielą klucz.

<a id="term-digital-signature"></a>[Podpis cyfrowy](00%20Glossary%20Security.md#digital-signature) działa podobnie, ale asymetrycznie: podpisuje się kluczem prywatnym, a weryfikuje publicznym. Każdy może sprawdzić podpis, ale złożyć go może tylko właściciel klucza prywatnego. Tak podpisywane są tokeny JWT w RS256, certyfikaty TLS i paczki oprogramowania.

| Operacja | Cel | Odwracalna | Wymaga klucza | Przykład w sklepie |
|---|---|---|---|---|
| hash | integralność, odcisk | nie | nie | suma kontrolna pliku z importu dostawcy |
| hash hasła | weryfikacja hasła | nie | nie (ale sól i koszt) | hasła klientów |
| szyfrowanie | poufność | tak, z kluczem | tak | numer rachunku do zwrotów w bazie |
| HMAC | integralność i autentyczność, wspólny klucz | nie | tak, wspólny | webhook od operatora płatności |
| podpis | integralność i autentyczność, klucz publiczny do weryfikacji | nie | tak, para kluczy | tokeny dla partnerów, weryfikowane ich kluczem publicznym |

Przykład weryfikacji webhooka HMAC-iem:

```python
import hashlib
import hmac

def valid_signature(body: bytes, signature_hex: str) -> bool:
    expected = hmac.new(settings.PAYMENT_WEBHOOK_SECRET.encode(), body, hashlib.sha256).hexdigest()
    return hmac.compare_digest(expected, signature_hex)       # porównanie w stałym czasie
```

Dwa szczegóły mają znaczenie. HMAC liczy się z surowego ciała żądania (`request.body`), a nie z danych po parsowaniu JSON-a, bo parsowanie zmienia kolejność i formatowanie. Porównanie przez `==` kończy się na pierwszym różnym znaku, więc czas odpowiedzi zdradza, ile znaków się zgadza. `hmac.compare_digest` porównuje w stałym czasie. Operatorzy płatności dodają też znacznik czasu do podpisywanej treści, a aplikacja odrzuca stare wiadomości, żeby nie dało się powtórzyć przechwyconego webhooka.

## Gotowe biblioteki

Kryptografia wymaga poprawności we wszystkich szczegółach, a błędu nie widać w testach funkcjonalnych: zaszyfrowane dane odszyfrowują się poprawnie, nawet jeśli szyfrowanie jest słabe. Dlatego obowiązuje zasada „nie pisz własnej kryptografii”. Nie chodzi tylko o algorytmy, ale też o składanie gotowych elementów w protokoły.

Typowe błędy przy „prostym” własnym szyfrowaniu:

- Base64 albo XOR zamiast szyfrowania. To kodowanie, a nie ochrona,
- AES w trybie ECB, w którym takie same bloki danych dają takie same bloki szyfrogramu, więc widać strukturę danych,
- szyfrowanie bez uwierzytelnienia (AES-CBC bez MAC). Napastnik może modyfikować szyfrogram i obserwować reakcję aplikacji,
- ponowne użycie nonce w AES-GCM z tym samym kluczem, co całkowicie łamie bezpieczeństwo,
- klucz wyprowadzony z hasła przez pojedynczy hash albo klucz zapisany w kodzie,
- porównywanie MAC-ów przez `==`.

Biblioteki, które rozwiązują te problemy za programistę:

```python
# cryptography.fernet: szyfrowanie symetryczne z uwierzytelnieniem, gotowe do użycia
from cryptography.fernet import Fernet, MultiFernet

fernet = MultiFernet([Fernet(k) for k in settings.FIELD_ENCRYPTION_KEYS])  # pierwszy klucz szyfruje

token = fernet.encrypt(iban.encode())           # zawiera znacznik czasu, IV i HMAC
iban = fernet.decrypt(token).decode()           # rzuca InvalidToken przy modyfikacji
```

```python
# django.core.signing: podpisane dane, np. link do rezygnacji z newslettera
from django.core import signing

token = signing.dumps({"customer": customer.pk}, salt="newsletter-unsubscribe")
data = signing.loads(token, salt="newsletter-unsubscribe", max_age=60 * 60 * 24 * 30)
```

`django.core.signing` używa HMAC z kluczem wyprowadzonym z <a id="term-secret-key"></a>[`SECRET_KEY`](00%20Glossary%20Security.md#secret-key), głównego sekretu projektu opisanego na końcu rozdziału. Dane są podpisane, ale nie zaszyfrowane: każdy może je odczytać, nikt nie może ich zmienić. Parametr `salt` oddziela zastosowania, więc token z linku newslettera nie zadziała w linku resetu czegoś innego. `max_age` ogranicza ważność.

| Potrzeba | Biblioteka |
|---|---|
| szyfrowanie pól w bazie | `cryptography` (Fernet, MultiFernet do rotacji kluczy) |
| podpisane linki i dane w ciasteczkach | `django.core.signing`, `TimestampSigner` |
| hasła | hashery Django |
| JWT | `PyJWT`, `djangorestframework-simplejwt` |
| niskopoziomowe prymitywy | `cryptography.hazmat` (AESGCM, Ed25519), tylko gdy naprawdę trzeba |
| TLS w żądaniach wychodzących | `requests` i `httpx` z domyślną weryfikacją certyfikatów |

Osobny przypadek to TLS. Najczęstszy błąd programisty to `requests.get(url, verify=False)` dodane, żeby „naprawić” problem z certyfikatem w środowisku testowym, które potem trafia na produkcję. Wyłącza to ochronę przed podsłuchem i podmianą odpowiedzi. Zamiast tego wskazuje się właściwy plik CA (`verify="/path/ca.pem"`).

## Losowość

Tokeny resetu hasła, klucze API, identyfikatory sesji i kody jednorazowe muszą być nieprzewidywalne. Moduł `random` w Pythonie używa generatora Mersenne Twister, który jest szybki i dobry do symulacji, ale przewidywalny. Po zaobserwowaniu 624 kolejnych 32-bitowych wartości da się odtworzyć jego stan i przewidzieć następne.

Do celów bezpieczeństwa służy <a id="term-csprng"></a>[CSPRNG](00%20Glossary%20Security.md#csprng) (cryptographically secure pseudo-random number generator), korzystający z entropii systemu operacyjnego. W Pythonie to moduł `secrets`:

```python
import secrets

# podatne: przewidywalny token
token = "".join(random.choice(string.ascii_letters) for _ in range(32))

# bezpieczne
token = secrets.token_urlsafe(32)          # 32 bajty losowości, zapis bezpieczny w URL
code = f"{secrets.randbelow(10**6):06d}"   # kod jednorazowy z 6 cyfr
secrets.compare_digest(a, b)               # porównanie w stałym czasie
```

Django korzysta z `secrets` w swoich mechanizmach: `get_random_string()` (np. przy generowaniu `SECRET_KEY` w nowym projekcie), sekret CSRF i klucze sesji. Tokeny resetu hasła nie są losowe, tylko wyliczane przez HMAC z danych użytkownika, znacznika czasu i `SECRET_KEY`. Dzięki temu nie trzeba ich przechowywać w bazie, a zmiana hasła automatycznie je unieważnia.

Tokeny zapisywane w bazie, np. klucze API dla partnerów, przechowuje się jak hasła: w bazie tylko hash, a pełny token pokazuje się użytkownikowi raz. Dla tokenów o wysokiej entropii wystarczy SHA-256, bo nie da się ich zgadnąć słownikowo.

## Klucz, od którego zależy wszystko

`SECRET_KEY` to główny sekret projektu Django. Nie służy do hashowania haseł, ale jest podstawą wielu podpisów:

- `django.core.signing` i wszystko, co z niego korzysta,
- tokeny resetu hasła,
- sesje w backendzie `signed_cookies` (cała sesja jest w podpisanym ciasteczku),
- magazyn wiadomości `CookieStorage` z `django.contrib.messages`,
- hash sesji powiązany z hasłem użytkownika (`get_session_auth_hash`),
- domyślnie klucz podpisu w `djangorestframework-simplejwt`.

Po wycieku `SECRET_KEY` napastnik może:

- wygenerować działający link resetu hasła dla dowolnego konta, czyli przejąć każde konto,
- podrobić dane sesji, jeśli używany jest backend `signed_cookies`,
- podrobić tokeny JWT, jeśli simplejwt używa domyślnego klucza,
- podrobić każdy podpisany link i dane z `signing`.

Rotacja `SECRET_KEY` bez przestoju jest możliwa od Django 4.1 dzięki `SECRET_KEY_FALLBACKS`:

```python
SECRET_KEY = env("DJANGO_SECRET_KEY")                     # nowy klucz: podpisuje
SECRET_KEY_FALLBACKS = env.list("DJANGO_SECRET_KEY_OLD")  # stare klucze: tylko weryfikacja
```

Kolejne kroki:

1. Wygeneruj nowy klucz (`get_random_secret_key()`), a stary przenieś do `SECRET_KEY_FALLBACKS`.
2. Wdróż. Nowe podpisy powstają nowym kluczem, a stare nadal są akceptowane, więc sesje i linki działają.
3. Po czasie dłuższym niż najdłuższa ważność podpisów (sesje, linki resetu) usuń stary klucz z `SECRET_KEY_FALLBACKS`.

Po wycieku kroki 2 i 3 skraca się do minimum. Lepiej wylogować wszystkich użytkowników, niż zostawić napastnikowi działający klucz.

## Co zapamiętać

- Hash daje odcisk bez klucza, szyfrowanie daje poufność z kluczem, HMAC daje autentyczność ze wspólnym kluczem, a podpis daje autentyczność weryfikowalną kluczem publicznym.
- HMAC webhooka liczy się z surowego ciała żądania i porównuje przez `hmac.compare_digest`, ze znacznikiem czasu przeciw powtórzeniom.
- Nie pisze się własnej kryptografii. Fernet i MultiFernet służą do szyfrowania pól, `django.core.signing` do podpisanych danych (podpisane, nie zaszyfrowane), gotowe biblioteki do JWT i nigdy `verify=False`.
- Do bezpieczeństwa służy `secrets`, a nie `random`. Tokeny przechowywane w bazie zapisuje się jako hash.
- `SECRET_KEY` podpisuje resety haseł, sesje w ciasteczkach, wiadomości i domyślnie JWT. Wyciek oznacza możliwość przejęcia kont.
- Rotacja bez przestoju przez `SECRET_KEY_FALLBACKS`: nowy klucz podpisuje, stare weryfikują przez ograniczony czas.

## Pytania sprawdzające

### 28. Czym różnią się hashowanie, szyfrowanie i podpisywanie? Kiedy użyć każdego z nich?

<details>
<summary>Odpowiedź</summary>

Hash to jednokierunkowy odcisk bez klucza: integralność, sumy kontrolne, deduplikacja. Nie daje poufności ani autentyczności. Szyfrowanie jest odwracalne z kluczem (symetryczne AES, asymetryczne RSA lub EC) i daje poufność, np. numer rachunku w bazie. HMAC to odcisk z danych i wspólnego sekretu: integralność i autentyczność między stronami dzielącymi klucz, np. webhook. Podpis cyfrowy składa się kluczem prywatnym, a weryfikuje publicznym, np. JWT RS256, certyfikaty, paczki. Hasła to osobny przypadek: funkcja do haseł z solą i kosztem.

Zobacz: sekcja „Trzy różne cele”.

</details>

### 29. Dlaczego nie pisze się własnej kryptografii i jakich bibliotek używać w Pythonie (`cryptography`, `secrets`, `django.core.signing`)?

<details>
<summary>Odpowiedź</summary>

Bo błędów nie widać w testach funkcjonalnych, a typowe pomyłki (Base64 lub XOR zamiast szyfrowania, AES-ECB, szyfrowanie bez uwierzytelnienia, ponowny nonce w GCM, klucz z pojedynczego hasha albo w kodzie, porównanie przez `==`) łamią ochronę. Do szyfrowania pól służy `cryptography` (Fernet, MultiFernet do rotacji), do podpisanych danych `django.core.signing` z `salt` i `max_age` (dane są podpisane, nie zaszyfrowane), do haseł hashery Django, do JWT `PyJWT` lub simplejwt, do losowości `secrets`. W żądaniach wychodzących nigdy `verify=False`.

Zobacz: sekcja „Gotowe biblioteki”.

</details>

### 30. Skąd brać bezpieczne losowe wartości (`secrets` a `random`) i jak Django generuje tokeny (reset hasła, CSRF)?

<details>
<summary>Odpowiedź</summary>

Z CSPRNG, czyli modułu `secrets` (`token_urlsafe`, `randbelow`, `compare_digest`), który korzysta z entropii systemu. `random` (Mersenne Twister) jest przewidywalny: po 624 wartościach da się odtworzyć jego stan. Django używa `secrets` w `get_random_string`, sekrecie CSRF i kluczach sesji. Tokeny resetu hasła są wyliczane HMAC-iem z danych użytkownika, czasu i `SECRET_KEY`, więc nie trzeba ich przechowywać, a zmiana hasła je unieważnia. Tokeny przechowywane w bazie (klucze API) zapisuje się jako hash.

Zobacz: sekcja „Losowość”.

</details>

### 31. Do czego służy `SECRET_KEY` w Django, co się stanie po jego wycieku i jak go rotować (`SECRET_KEY_FALLBACKS`)?

<details>
<summary>Odpowiedź</summary>

Podpisuje dane: `django.core.signing`, tokeny resetu hasła, sesje w backendzie `signed_cookies`, wiadomości w ciasteczkach, hash sesji powiązany z hasłem, a domyślnie także JWT w simplejwt. Nie hashuje haseł. Po wycieku napastnik może generować linki resetu dla dowolnego konta (przejęcie kont), podrabiać sesje w ciasteczkach, JWT i podpisane dane. Rotacja od Django 4.1: nowy klucz w `SECRET_KEY`, stary w `SECRET_KEY_FALLBACKS` (tylko weryfikacja), wdrożenie, a po upływie najdłuższej ważności podpisów usunięcie starego. Po wycieku ten czas skraca się do minimum.

Zobacz: sekcja „Klucz, od którego zależy wszystko”.

</details>
