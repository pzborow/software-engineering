# Uwierzytelnianie

Uwierzytelnianie odpowiada na pytanie „kim jesteś?”. W sklepie obejmuje rejestrację, logowanie, sesję przeglądarki, tokeny dla aplikacji mobilnej, logowanie przez Google i reset hasła. To obszar, w którym Django daje najwięcej gotowych, dobrych rozwiązań, a jednocześnie ten, w którym zespoły najczęściej tracą bezpieczeństwo, zastępując je własnymi pomysłami, zwłaszcza wokół tokenów.

```text
klient ──hasło──► logowanie ──► weryfikacja hasha ──► sesja (ciasteczko) albo token (JWT)
                     │                                          │
                     ├── limity prób, MFA                       └── każde kolejne żądanie
                     └── reset hasła przez e-mail                   niesie dowód tożsamości
```

## Przechowywanie haseł

Hasła nigdy nie są przechowywane wprost ani szyfrowane. Przechowuje się ich <a id="term-password-hash"></a>[hash hasła](00%20Glossary%20Security.md#password-hash), czyli wynik jednokierunkowej funkcji, zaprojektowanej specjalnie do haseł. Trzy cechy odróżniają ją od zwykłego hasha jak SHA-256:

- <a id="term-salt"></a>[sól](00%20Glossary%20Security.md#salt) (salt): losowa wartość unikalna dla każdego hasła, zapisana obok hasha. Te same hasła mają różne hashe, więc tablice tęczowe i porównywanie hashy między użytkownikami nie działają,
- koszt obliczeniowy: funkcja jest celowo wolna (tysiące iteracji, duże zużycie pamięci), żeby zgadywanie miliardów haseł na minutę było niemożliwe nawet po wycieku bazy,
- możliwość zwiększania kosztu z czasem, gdy sprzęt staje się szybszy.

Zalecane funkcje to Argon2id, scrypt, bcrypt i PBKDF2 z dużą liczbą iteracji. SHA-256, MD5 i SHA-1, nawet z solą, są za szybkie.

Django realizuje to przez `PASSWORD_HASHERS`. Pierwszy hasher na liście jest używany do nowych haseł, a pozostałe służą do weryfikacji starszych:

```python
# settings.py
PASSWORD_HASHERS = [
    "django.contrib.auth.hashers.Argon2PasswordHasher",       # wymaga pakietu argon2-cffi
    "django.contrib.auth.hashers.PBKDF2PasswordHasher",       # domyślny w Django
    "django.contrib.auth.hashers.PBKDF2SHA1PasswordHasher",
    "django.contrib.auth.hashers.ScryptPasswordHasher",
]

AUTH_PASSWORD_VALIDATORS = [
    {"NAME": "django.contrib.auth.password_validation.UserAttributeSimilarityValidator"},
    {"NAME": "django.contrib.auth.password_validation.MinimumLengthValidator", "OPTIONS": {"min_length": 12}},
    {"NAME": "django.contrib.auth.password_validation.CommonPasswordValidator"},
    {"NAME": "django.contrib.auth.password_validation.NumericPasswordValidator"},
]
```

Hash w bazie ma format `algorytm$parametry$sól$hash`, np. `pbkdf2_sha256$870000$Kx3...$Qm9...`. Dzięki temu Django wie, jak zweryfikować każde hasło.

Automatyczne przehashowanie: gdy użytkownik loguje się poprawnie, a jego hash powstał starszym algorytmem albo z mniejszą liczbą iteracji niż obecnie skonfigurowana, Django od razu zapisuje nowy hash. Po zmianie `PASSWORD_HASHERS` albo aktualizacji Django, która podnosi liczbę iteracji, hasła aktywnych użytkowników same się aktualizują.

Gdzie ochrona się kończy:

- import użytkowników ze starego systemu z hashami MD5. Django może je weryfikować przez `UnsaltedMD5PasswordHasher`, ale dopóki użytkownik się nie zaloguje, słaby hash zostaje w bazie. Lepiej opakować stary hash w silną funkcję od razu, a przy logowaniu zamienić na zwykły,
- ustawianie pola `password` bezpośrednio (`user.password = form.cleaned_data["password"]`) zamiast `user.set_password()`. Hasło trafia do bazy jawnym tekstem,
- własny hasher albo `hashlib.sha256(password)` w kodzie spoza Django.

## Zgadywanie haseł

Dwa najczęstsze ataki na logowanie to zgadywanie haseł jednego konta (brute force) i <a id="term-credential-stuffing"></a>[credential stuffing](00%20Glossary%20Security.md#credential-stuffing): sprawdzanie par e-mail i hasło wykradzionych z innych serwisów. Ludzie używają tych samych haseł w wielu miejscach, więc drugi atak jest dużo skuteczniejszy.

Samo Django nie ogranicza liczby prób logowania. Obrona wymaga kilku warstw:

- limit prób na konto i na adres IP. `django-axes` blokuje konto albo adres po określonej liczbie nieudanych prób. W API do endpointu logowania dodaje się throttling DRF,
- sprawdzanie haseł, które wyciekły. Przy rejestracji i zmianie hasła można odpytać bazę Have I Been Pwned w trybie k-anonimowości (wysyła się tylko pierwsze 5 znaków hasha SHA-1),
- CAPTCHA po kilku nieudanych próbach, a nie od razu,
- jednakowe odpowiedzi: „nieprawidłowy e-mail lub hasło”, bez zdradzania, czy konto istnieje. Django w `ModelBackend` wykonuje obliczenie hasha także dla nieistniejącego użytkownika, żeby czas odpowiedzi nie zdradzał, czy konto istnieje,
- powiadomienie użytkownika o logowaniu z nowego urządzenia.

Najskuteczniejszą obroną przed credential stuffing jest <a id="term-mfa"></a>[MFA](00%20Glossary%20Security.md#mfa) (multi-factor authentication): oprócz hasła wymagany jest drugi składnik, np. kod TOTP z aplikacji, klucz sprzętowy albo passkey (WebAuthn). Samo hasło z wycieku nie wystarczy wtedy do zalogowania. W Django MFA dodają `django-allauth` (TOTP, WebAuthn) albo `django-otp`. Warto je wymagać co najmniej dla kont pracowników z dostępem do panelu admina.

## Dowód tożsamości w kolejnych żądaniach

Po zalogowaniu każde kolejne żądanie musi nieść dowód tożsamości. Są dwa główne podejścia.

<a id="term-session"></a>[Sesja](00%20Glossary%20Security.md#session): serwer tworzy losowy identyfikator, zapisuje dane sesji u siebie (w bazie, cache albo podpisanym ciasteczku), a przeglądarka dostaje identyfikator w ciasteczku. To domyślny mechanizm Django (`django.contrib.sessions`).

<a id="term-jwt"></a>[JWT](00%20Glossary%20Security.md#jwt) (JSON Web Token): serwer wydaje podpisany token zawierający dane (identyfikator użytkownika, czas ważności). Każde żądanie niesie token, a serwer weryfikuje podpis bez odpytywania bazy. W DRF najczęściej przez `djangorestframework-simplejwt`.

| | Sesja Django | JWT |
|---|---|---|
| Gdzie są dane | na serwerze | w tokenie u klienta |
| Unieważnienie (wylogowanie, ban, zmiana hasła) | natychmiastowe: usunięcie sesji | trudne: token ważny do wygaśnięcia, potrzebna czarna lista |
| Skalowanie | wymaga wspólnego magazynu sesji | weryfikacja bez magazynu |
| Rozmiar | krótki identyfikator | setki bajtów w każdym żądaniu |
| Przechowywanie w przeglądarce | ciasteczko `HttpOnly` | ciasteczko albo pamięć JS (`localStorage` jest dostępny dla XSS) |
| Podatność na CSRF | tak, stąd ochrona CSRF | nie, jeśli w nagłówku `Authorization`, tak, jeśli w ciasteczku |
| Dobre dla | aplikacji webowej na jednej domenie | API dla aplikacji mobilnych, komunikacji między serwisami |

Częsty błąd to wybór JWT dla zwykłej aplikacji webowej „bo jest nowocześniejsze”. Traci się wtedy natychmiastowe wylogowanie, a zyskuje problem przechowywania tokenu w przeglądarce. Dla aplikacji webowej sesja Django jest zwykle lepszym wyborem. JWT ma sens dla aplikacji mobilnych, integracji i architektur z wieloma serwisami.

Jeśli JWT, to z krótko żyjącym tokenem dostępu i dłużej żyjącym <a id="term-refresh-token"></a>[refresh tokenem](00%20Glossary%20Security.md#refresh-token), służącym tylko do uzyskania nowego tokenu dostępu. Refresh token jest rotowany przy każdym użyciu, a stary trafia na czarną listę. Ponowne użycie starego refresh tokenu oznacza wyciek i powinno unieważnić całą rodzinę tokenów.

## Typowe błędy z JWT

JWT ma kilka znanych pułapek, o które często pytają na rozmowach:

- algorytm `none`: token z nagłówkiem `"alg": "none"` nie ma podpisu. Biblioteka, która ufa polu `alg` z tokenu, przyjmie dowolny token,
- pomylenie algorytmów: serwer używa RS256 (klucz publiczny do weryfikacji). Napastnik wysyła token z `"alg": "HS256"` podpisany kluczem publicznym jako sekretem HMAC. Biblioteka, która wybiera algorytm z tokenu, zweryfikuje go poprawnie,
- brak weryfikacji podpisu: `jwt.decode(token, options={"verify_signature": False})` użyte „tymczasowo”, żeby odczytać dane,
- brak sprawdzania `exp`, `aud` i `iss`: token wydany dla innej usługi albo przeterminowany jest akceptowany,
- wrażliwe dane w tokenie: payload JWT jest tylko zakodowany w Base64, a nie zaszyfrowany. Każdy może go odczytać,
- długi czas życia tokenu dostępu (dni albo tygodnie) i brak unieważniania,
- token w `localStorage`, skąd każdy skrypt XSS może go odczytać.

`djangorestframework-simplejwt` unika większości z nich:

```python
SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=5),     # domyślnie 5 minut
    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),
    "ROTATE_REFRESH_TOKENS": True,                     # domyślnie wyłączone
    "BLACKLIST_AFTER_ROTATION": True,                  # wymaga aplikacji token_blacklist
    "ALGORITHM": "HS256",                              # algorytm z konfiguracji, a nie z tokenu
    "SIGNING_KEY": env("JWT_SIGNING_KEY"),             # osobny klucz zamiast SECRET_KEY
    "AUDIENCE": "shop-api",
    "ISSUER": "https://shop.example",
}
INSTALLED_APPS += ["rest_framework_simplejwt.token_blacklist"]
```

Biblioteka weryfikuje podpis algorytmem z konfiguracji, odrzuca `none` i sprawdza `exp`. Domyślnie jednak nie rotuje refresh tokenów, a podpisuje tokeny kluczem `SECRET_KEY` projektu. Wyciek tego klucza pozwala wtedy fałszować tokeny, więc warto użyć osobnego klucza.

## Logowanie przez zewnętrznego dostawcę

<a id="term-oauth2"></a>[OAuth2](00%20Glossary%20Security.md#oauth2) to protokół delegowania dostępu: użytkownik pozwala aplikacji działać w swoim imieniu w innej usłudze, a aplikacja dostaje token dostępu, nie poznając hasła. OAuth2 sam w sobie nie mówi, kim jest użytkownik.

<a id="term-oidc"></a>[OpenID Connect](00%20Glossary%20Security.md#oidc) (OIDC) to warstwa tożsamości zbudowana na OAuth2. Dodaje ID token (JWT z danymi o użytkowniku, np. `sub` i `email`) i endpoint `userinfo`. „Zaloguj przez Google” to OIDC.

Który przepływ wybrać. Skrót <a id="term-pkce"></a>[PKCE](00%20Glossary%20Security.md#pkce) z tabeli jest wyjaśniony pod nią:

| Klient | Przepływ | Uwagi |
|---|---|---|
| aplikacja webowa z backendem (Django) | authorization code, z sekretem klienta, zalecane też z PKCE | tokeny zostają na serwerze |
| SPA (React w przeglądarce) | authorization code z PKCE, najlepiej przez backend (wzorzec BFF) | brak sekretu, tokeny najlepiej poza przeglądarką |
| aplikacja mobilna | authorization code z PKCE, przez przeglądarkę systemową | brak sekretu, własny schemat URL albo App Links |
| serwer do serwera, bez użytkownika | client credentials | sekret klienta albo klucz, wąskie uprawnienia (scope) |
| implicit, password grant | nie używać | wycofane w zaleceniach OAuth 2.0 Security BCP i OAuth 2.1 |

PKCE (Proof Key for Code Exchange, RFC 7636) chroni przepływ authorization code w klientach, które nie mogą bezpiecznie przechowywać sekretu. Klient generuje losowy `code_verifier`, wysyła jego hash (`code_challenge`) na początku przepływu, a przy wymianie kodu na token pokazuje oryginał. Napastnik, który przechwyci kod autoryzacyjny, nie zna `code_verifier`, więc nie wymieni kodu na token.

Dodatkowo parametr `state` chroni przed CSRF w przepływie OAuth, a `nonce` w OIDC przed ponownym użyciem ID tokenu. Obowiązkowa jest też dokładna weryfikacja `redirect_uri`, bez dopasowania prefiksem.

W Django gotowe rozwiązania to `django-allauth` (logowanie przez Google, Apple, GitHub i dowolnego dostawcę OIDC), `mozilla-django-oidc` (klient OIDC dla firmowego SSO) i `django-oauth-toolkit` (gdy sklep sam ma być serwerem autoryzacji dla partnerów). Implementowanie OAuth ręcznie jest źródłem wielu podatności. Biblioteki obsługują `state`, `nonce`, PKCE i weryfikację podpisu ID tokenu.

## Ciasteczka, reset hasła i wylogowanie

Ciasteczko sesji to klucz do konta, więc jego atrybuty mają znaczenie:

```python
SESSION_COOKIE_SECURE = True        # tylko przez HTTPS (domyślnie False)
SESSION_COOKIE_HTTPONLY = True      # niedostępne z JavaScript (domyślnie True)
SESSION_COOKIE_SAMESITE = "Lax"     # nie wysyłane w POST z obcych domen (domyślnie "Lax")
SESSION_COOKIE_AGE = 60 * 60 * 24 * 7
CSRF_COOKIE_SECURE = True
```

Django chroni przed session fixation: funkcja `login()` zmienia identyfikator sesji po zalogowaniu (`cycle_key`), więc identyfikator narzucony ofierze przed logowaniem przestaje działać. Po zmianie hasła wywołuje się `update_session_auth_hash(request, user)`. Obecna sesja zostaje, a pozostałe sesje użytkownika na innych urządzeniach przestają być ważne, bo sesja przechowuje hash oparty na haśle.

Reset hasła w Django (`PasswordResetView`) jest dobrze zaprojektowany:

- token jest podpisany HMAC-iem z `SECRET_KEY` i zawiera stan użytkownika, więc przestaje działać po zmianie hasła albo kolejnym zalogowaniu,
- ważność ogranicza `PASSWORD_RESET_TIMEOUT` (domyślnie 3 dni, warto skrócić),
- formularz nie zdradza, czy konto o podanym e-mailu istnieje.

Gdzie ochrona się kończy:

- link w e-mailu buduje się z nagłówka `Host` żądania. Bez poprawnego `ALLOWED_HOSTS` napastnik może wysłać żądanie resetu z `Host: evil.example` i ofiara dostanie prawdziwy e-mail ze sklepu z linkiem do domeny napastnika. Dlatego `ALLOWED_HOSTS` musi być ustawione, a w szablonie e-maila najlepiej używać stałej domeny,
- własna implementacja resetu z tokenem z `random.random()`, bez wygasania albo zapisanym w bazie jawnym tekstem,
- różne komunikaty dla istniejącego i nieistniejącego konta.

Wylogowanie przez `logout()` usuwa dane sesji po stronie serwera, więc skradzione ciasteczko przestaje działać. Przy JWT wylogowanie wymaga dodania refresh tokenu do czarnej listy. Token dostępu pozostaje ważny do wygaśnięcia, dlatego jest krótki.

## Co zapamiętać

- Hasła przechowuje się jako hash z solą i wysokim kosztem (Argon2, scrypt, PBKDF2). Django robi to przez `PASSWORD_HASHERS` i samo przehashowuje hasła przy logowaniu.
- `set_password()` zamiast zapisu do pola, walidatory długości i popularnych haseł, stare słabe hashe opakowane od razu.
- Django nie ogranicza prób logowania. Potrzebne są `django-axes` lub throttling, sprawdzanie wycieków, jednakowe odpowiedzi i MFA.
- Sesja daje natychmiastowe unieważnienie i ciasteczko `HttpOnly`. JWT pasuje do API i usług, ale wymaga krótkich tokenów, rotacji refresh tokenów i czarnej listy.
- Typowe błędy z JWT to `none`, pomylenie algorytmów, brak weryfikacji podpisu i `exp`, dane w payloadzie i `localStorage`.
- OIDC to tożsamość na OAuth2. Authorization code z PKCE dla SPA i mobile, client credentials dla serwerów, bez implicit i password grant, z użyciem gotowej biblioteki.
- Ciasteczka `Secure`, `HttpOnly`, `SameSite`. Reset hasła Django jest bezpieczny pod warunkiem poprawnego `ALLOWED_HOSTS`.

## Pytania sprawdzające

### 17. Jak poprawnie przechowywać hasła (hash, sól, koszt obliczeniowy)? Jak działa `PASSWORD_HASHERS` w Django i automatyczne przehashowanie przy logowaniu?

<details>
<summary>Odpowiedź</summary>

Jako hash funkcją do haseł (Argon2id, scrypt, bcrypt, PBKDF2 z dużą liczbą iteracji), z unikalną solą i wysokim, zwiększanym z czasem kosztem. Nigdy jawnie, szyfrowane ani szybkim hashem (SHA-256, MD5). W Django pierwszy hasher z `PASSWORD_HASHERS` tworzy nowe hashe, a pozostałe weryfikują starsze. Hash ma format `algorytm$parametry$sól$hash`. Przy poprawnym logowaniu, jeśli hash jest starszym algorytmem lub ma mniej iteracji, Django od razu zapisuje nowy. Pułapki to przypisanie do pola `password` zamiast `set_password()` i słabe hashe z importu.

Zobacz: sekcja „Przechowywanie haseł”.

</details>

### 18. Jak chronić logowanie przed zgadywaniem haseł i credential stuffing (limity, blokady, `django-axes`, MFA)?

<details>
<summary>Odpowiedź</summary>

Django samo nie ogranicza prób, więc potrzebne są limity na konto i adres IP (`django-axes`, throttling DRF na endpoincie logowania), sprawdzanie haseł z wycieków (Have I Been Pwned w trybie k-anonimowości), CAPTCHA po kilku próbach, jednakowe komunikaty i czas odpowiedzi (Django liczy hash także dla nieistniejącego użytkownika) oraz powiadomienia o nowych urządzeniach. Najskuteczniejsze przeciw credential stuffing jest MFA (TOTP, WebAuthn, passkeys przez `django-allauth` lub `django-otp`), co najmniej dla pracowników.

Zobacz: sekcja „Zgadywanie haseł”.

</details>

### 19. Sesje czy JWT: jakie są realne różnice w bezpieczeństwie, unieważnianiu i przechowywaniu po stronie klienta?

<details>
<summary>Odpowiedź</summary>

Sesja trzyma dane na serwerze, a klient ma tylko identyfikator w ciasteczku `HttpOnly`. Unieważnienie jest natychmiastowe, ale sesja wymaga wspólnego magazynu i ochrony CSRF. JWT zawiera dane i podpis, więc weryfikuje się go bez bazy, ale trudno go unieważnić przed wygaśnięciem. W `localStorage` jest dostępny dla XSS, a w ciasteczku wraca CSRF. Dla aplikacji webowej sesja Django jest zwykle lepsza. JWT pasuje do mobile, integracji i wielu serwisów, z krótkim tokenem dostępu, rotacją refresh tokenów i czarną listą.

Zobacz: sekcja „Dowód tożsamości w kolejnych żądaniach”.

</details>

### 20. Jakie są typowe błędy przy JWT (algorytm `none`, brak weryfikacji podpisu, długi czas życia, tokeny w `localStorage`) i jak unika ich `djangorestframework-simplejwt`?

<details>
<summary>Odpowiedź</summary>

Błędy to akceptowanie `alg: none`, pomylenie algorytmów (RS256 na HS256 z kluczem publicznym jako sekretem), wyłączona weryfikacja podpisu, brak sprawdzania `exp`, `aud` i `iss`, wrażliwe dane w niezaszyfrowanym payloadzie, długie tokeny dostępu bez unieważniania i przechowywanie w `localStorage`. simplejwt weryfikuje podpis algorytmem z konfiguracji (nie z tokenu), odrzuca `none`, sprawdza `exp` i ma domyślnie 5-minutowy token dostępu. Trzeba samemu włączyć `ROTATE_REFRESH_TOKENS`, `BLACKLIST_AFTER_ROTATION` z aplikacją `token_blacklist`, ustawić `AUDIENCE` i `ISSUER` oraz osobny klucz zamiast `SECRET_KEY`.

Zobacz: sekcja „Typowe błędy z JWT”.

</details>

### 21. Czym różnią się OAuth2 i OpenID Connect? Po co jest PKCE i który flow wybrać dla SPA, aplikacji mobilnej i komunikacji serwer–serwer?

<details>
<summary>Odpowiedź</summary>

OAuth2 deleguje dostęp (token dostępu do zasobów w imieniu użytkownika) i nie mówi, kim jest użytkownik. OIDC dodaje warstwę tożsamości: ID token (JWT) i `userinfo`. PKCE chroni authorization code w klientach bez sekretu: klient wysyła hash losowego `code_verifier`, a przy wymianie kodu pokazuje oryginał, więc przechwycony kod jest bezużyteczny. Dla SPA authorization code z PKCE, najlepiej przez BFF. Dla mobile authorization code z PKCE przez przeglądarkę systemową. Dla serwerów client credentials. Implicit i password grant są wycofane. W Django używa się `django-allauth`, `mozilla-django-oidc` lub `django-oauth-toolkit`, a nie własnej implementacji.

Zobacz: sekcja „Logowanie przez zewnętrznego dostawcę”.

</details>

### 22. Jak bezpiecznie obsługiwać ciasteczka sesji (`Secure`, `HttpOnly`, `SameSite`), reset hasła i wylogowanie w Django?

<details>
<summary>Odpowiedź</summary>

Ciasteczka: `SESSION_COOKIE_SECURE` i `CSRF_COOKIE_SECURE` na `True` (domyślnie `False`), `HttpOnly` (domyślnie włączone), `SameSite=Lax` (domyślnie). Django chroni przed session fixation (`login()` zmienia identyfikator), a `update_session_auth_hash` po zmianie hasła unieważnia sesje na innych urządzeniach. Reset hasła Django używa tokenu HMAC unieważnianego zmianą hasła lub logowaniem, z czasem ważności `PASSWORD_RESET_TIMEOUT`, i nie zdradza, czy konto istnieje. Wymaga poprawnego `ALLOWED_HOSTS`, bo link buduje się z nagłówka `Host`. `logout()` usuwa sesję na serwerze. Przy JWT refresh token trafia na czarną listę.

Zobacz: sekcja „Ciasteczka, reset hasła i wylogowanie”.

</details>
