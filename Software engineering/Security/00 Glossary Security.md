# Glosariusz Security

## Spis haseł

- [Modelowanie zagrożeń](#threat-modeling)
- [STRIDE](#stride)
- [Defense in depth](#defense-in-depth)
- [Least privilege](#least-privilege)
- [Secure by default](#secure-by-default)
- [Powierzchnia ataku](#attack-surface)
- [Podatność](#vulnerability)
- [OWASP Top 10](#owasp-top-10)
- [SQL injection](#sql-injection)
- [Zapytanie parametryzowane](#parameterized-query)
- [Command injection](#command-injection)
- [Server-side template injection](#ssti)
- [Path traversal](#path-traversal)
- [NoSQL injection](#nosql-injection)
- [XSS](#xss)
- [CSRF](#csrf)
- [SameSite](#samesite)
- [CORS](#cors)
- [SSRF](#ssrf)
- [Clickjacking](#clickjacking)
- [HSTS](#hsts)
- [CSP](#csp)
- [Hash hasła](#password-hash)
- [Sól](#salt)
- [Credential stuffing](#credential-stuffing)
- [MFA](#mfa)
- [Sesja](#session)
- [JWT](#jwt)
- [Refresh token](#refresh-token)
- [OAuth2](#oauth2)
- [OpenID Connect](#oidc)
- [PKCE](#pkce)
- [Uwierzytelnienie](#authentication)
- [Autoryzacja](#authorization)
- [BOLA](#bola)
- [RBAC](#rbac)
- [ABAC](#abac)
- [Multitenancy](#multitenancy)
- [Mass assignment](#mass-assignment)
- [Funkcja skrótu](#hash-function)
- [Szyfrowanie](#encryption)
- [HMAC](#hmac)
- [Podpis cyfrowy](#digital-signature)
- [SECRET_KEY](#secret-key)
- [CSPRNG](#csprng)
- [Sekret](#secret)
- [Skanowanie sekretów](#secret-scanning)
- [Tryb debug](#debug-mode)
- [ALLOWED_HOSTS](#allowed-hosts)
- [Atak na łańcuch dostaw](#supply-chain-attack)
- [Typosquatting](#typosquatting)
- [Dependency confusion](#dependency-confusion)
- [SCA](#sca)
- [SBOM](#sbom)
- [Rate limiting](#rate-limiting)
- [Niebezpieczna deserializacja](#insecure-deserialization)
- [PII](#pii)
- [Minimalizacja danych](#data-minimization)
- [SAST](#sast)
- [DAST](#dast)
- [Reakcja na incydent](#incident-response)
- [Analiza po incydencie bez szukania winnych](#blameless-postmortem)

<a id="threat-modeling"></a>
## Modelowanie zagrożeń

Threat modeling: systematyczne ustalenie przed napisaniem kodu, co może pójść źle, przez cztery pytania: co budujemy, co może pójść źle, co z tym zrobimy, czy zrobiliśmy to dobrze.

Pierwsza wzmianka: [rozdział 01](01%20Podstawy.md#term-threat-modeling).

<a id="stride"></a>
## STRIDE

Lista kategorii zagrożeń: podszywanie się, modyfikacja danych, wypieranie się, ujawnienie informacji, odmowa usługi, podniesienie uprawnień.

Pierwsza wzmianka: [rozdział 01](01%20Podstawy.md#term-stride).

<a id="defense-in-depth"></a>
## Defense in depth

Obrona w głąb: wiele niezależnych warstw zabezpieczeń, z których każda zakłada, że poprzednia może zawieść.

Pierwsza wzmianka: [rozdział 01](01%20Podstawy.md#term-defense-in-depth).

<a id="least-privilege"></a>
## Least privilege

Zasada najmniejszych uprawnień: użytkownik, proces i token dostają tylko te uprawnienia, których potrzebują.

Pierwsza wzmianka: [rozdział 01](01%20Podstawy.md#term-least-privilege).

<a id="secure-by-default"></a>
## Secure by default

Bezpieczne ustawienia domyślne: najprostsza droga jest bezpieczna, a wyłączenie ochrony wymaga świadomej decyzji.

Pierwsza wzmianka: [rozdział 01](01%20Podstawy.md#term-secure-by-default).

<a id="attack-surface"></a>
## Powierzchnia ataku

Attack surface: suma miejsc, przez które napastnik może wprowadzić dane lub wywołać działanie systemu.

Pierwsza wzmianka: [rozdział 01](01%20Podstawy.md#term-attack-surface).

<a id="vulnerability"></a>
## Podatność

Vulnerability: błąd, który pozwala komuś osiągnąć coś, na co nie powinien mieć pozwolenia.

Pierwsza wzmianka: [rozdział 01](01%20Podstawy.md#term-vulnerability).

<a id="owasp-top-10"></a>
## OWASP Top 10

Lista najczęstszych kategorii ryzyka w aplikacjach webowych publikowana przez OWASP. Dla API istnieje osobna lista, OWASP API Security Top 10.

Pierwsza wzmianka: [rozdział 01](01%20Podstawy.md#term-owasp-top-10).

<a id="sql-injection"></a>
## SQL injection

Wstrzyknięcie fragmentu SQL przez dane użytkownika łączone z tekstem zapytania.

Pierwsza wzmianka: [rozdział 02](02%20Wstrzykiwanie.md#term-sql-injection).

<a id="parameterized-query"></a>
## Zapytanie parametryzowane

Zapytanie z symbolami zastępczymi, w którym wartości są przekazywane do bazy osobno od polecenia SQL.

Pierwsza wzmianka: [rozdział 02](02%20Wstrzykiwanie.md#term-parameterized-query).

<a id="command-injection"></a>
## Command injection

Wstrzyknięcie poleceń powłoki przez dane wstawione do polecenia systemowego.

Pierwsza wzmianka: [rozdział 02](02%20Wstrzykiwanie.md#term-command-injection).

<a id="ssti"></a>
## Server-side template injection

SSTI: kompilowanie danych użytkownika jako szablonu, co pozwala odczytać dane lub wykonać kod.

Pierwsza wzmianka: [rozdział 02](02%20Wstrzykiwanie.md#term-ssti).

<a id="path-traversal"></a>
## Path traversal

Wyjście poza dozwolony katalog przez sekwencje ../ w ścieżce pliku podanej przez użytkownika.

Pierwsza wzmianka: [rozdział 02](02%20Wstrzykiwanie.md#term-path-traversal).

<a id="nosql-injection"></a>
## NoSQL injection

Przemycenie operatora zapytania (np. $ne) zamiast wartości w zapytaniu do bazy dokumentowej.

Pierwsza wzmianka: [rozdział 02](02%20Wstrzykiwanie.md#term-nosql-injection).

<a id="xss"></a>
## XSS

Cross-site scripting: wstrzyknięcie skryptu wykonywanego w przeglądarce innego użytkownika w kontekście strony. Odmiany: stored, reflected, DOM-based.

Pierwsza wzmianka: [rozdział 03](03%20Podatno%C5%9Bci%20webowe.md#term-xss).

<a id="csrf"></a>
## CSRF

Cross-site request forgery: wysłanie przez obcą stronę żądania do aplikacji z ciasteczkami zalogowanej ofiary.

Pierwsza wzmianka: [rozdział 03](03%20Podatno%C5%9Bci%20webowe.md#term-csrf).

<a id="samesite"></a>
## SameSite

Atrybut ciasteczka, który ogranicza wysyłanie go w żądaniach inicjowanych z innych domen (Lax, Strict, None).

Pierwsza wzmianka: [rozdział 03](03%20Podatno%C5%9Bci%20webowe.md#term-samesite).

<a id="cors"></a>
## CORS

Cross-Origin Resource Sharing: mechanizm, przez który serwer pozwala wybranym domenom odczytywać swoje odpowiedzi w przeglądarce.

Pierwsza wzmianka: [rozdział 03](03%20Podatno%C5%9Bci%20webowe.md#term-cors).

<a id="ssrf"></a>
## SSRF

Server-side request forgery: zmuszenie serwera do wykonania żądania pod adres wskazany przez napastnika.

Pierwsza wzmianka: [rozdział 03](03%20Podatno%C5%9Bci%20webowe.md#term-ssrf).

<a id="clickjacking"></a>
## Clickjacking

Osadzenie strony w niewidocznej ramce i skłonienie ofiary do kliknięcia w jej elementy.

Pierwsza wzmianka: [rozdział 03](03%20Podatno%C5%9Bci%20webowe.md#term-clickjacking).

<a id="hsts"></a>
## HSTS

HTTP Strict Transport Security: nagłówek każący przeglądarce łączyć się z domeną wyłącznie przez HTTPS.

Pierwsza wzmianka: [rozdział 03](03%20Podatno%C5%9Bci%20webowe.md#term-hsts).

<a id="csp"></a>
## CSP

Content Security Policy: nagłówek określający, skąd strona może ładować skrypty i inne zasoby. Ostatnia linia obrony przed XSS.

Pierwsza wzmianka: [rozdział 03](03%20Podatno%C5%9Bci%20webowe.md#term-csp).

<a id="password-hash"></a>
## Hash hasła

Wynik jednokierunkowej funkcji do haseł (Argon2, scrypt, bcrypt, PBKDF2) z solą i wysokim kosztem obliczeniowym.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-password-hash).

<a id="salt"></a>
## Sól

Salt: losowa wartość unikalna dla każdego hasła, dzięki której te same hasła mają różne hashe.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-salt).

<a id="credential-stuffing"></a>
## Credential stuffing

Sprawdzanie par login i hasło wykradzionych z innych serwisów.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-credential-stuffing).

<a id="mfa"></a>
## MFA

Multi-factor authentication: uwierzytelnianie wymagające dodatkowego składnika poza hasłem (TOTP, klucz sprzętowy, passkey).

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-mfa).

<a id="session"></a>
## Sesja

Stan zalogowania przechowywany na serwerze i wskazywany losowym identyfikatorem w ciasteczku.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-session).

<a id="jwt"></a>
## JWT

JSON Web Token: podpisany token zawierający dane o użytkowniku, weryfikowany bez odpytywania bazy.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-jwt).

<a id="refresh-token"></a>
## Refresh token

Dłużej żyjący token służący tylko do uzyskania nowego, krótko żyjącego tokenu dostępu.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-refresh-token).

<a id="oauth2"></a>
## OAuth2

Protokół delegowania dostępu: aplikacja dostaje token do działania w imieniu użytkownika, bez poznania jego hasła.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-oauth2).

<a id="oidc"></a>
## OpenID Connect

OIDC: warstwa tożsamości na OAuth2, dodająca ID token i endpoint userinfo.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-oidc).

<a id="pkce"></a>
## PKCE

Proof Key for Code Exchange: ochrona przepływu authorization code w klientach bez sekretu przez code_verifier i code_challenge.

Pierwsza wzmianka: [rozdział 04](04%20Uwierzytelnianie.md#term-pkce).

<a id="authentication"></a>
## Uwierzytelnienie

Authentication: ustalenie tożsamości użytkownika.

Pierwsza wzmianka: [rozdział 05](05%20Autoryzacja.md#term-authentication).

<a id="authorization"></a>
## Autoryzacja

Authorization: decyzja, co zidentyfikowany użytkownik może zrobić.

Pierwsza wzmianka: [rozdział 05](05%20Autoryzacja.md#term-authorization).

<a id="bola"></a>
## BOLA

Broken Object Level Authorization (IDOR): brak sprawdzenia, czy użytkownik ma prawo do konkretnego obiektu.

Pierwsza wzmianka: [rozdział 05](05%20Autoryzacja.md#term-bola).

<a id="rbac"></a>
## RBAC

Role-Based Access Control: uprawnienia przypisane do ról, a role do użytkowników.

Pierwsza wzmianka: [rozdział 05](05%20Autoryzacja.md#term-rbac).

<a id="abac"></a>
## ABAC

Attribute-Based Access Control: decyzje oparte na atrybutach użytkownika, obiektu i kontekstu.

Pierwsza wzmianka: [rozdział 05](05%20Autoryzacja.md#term-abac).

<a id="multitenancy"></a>
## Multitenancy

Obsługa wielu klientów (najemców) w jednej instalacji, z izolacją ich danych.

Pierwsza wzmianka: [rozdział 05](05%20Autoryzacja.md#term-multitenancy).

<a id="mass-assignment"></a>
## Mass assignment

Zapis do modelu wszystkich pól z żądania, także tych, których użytkownik nie powinien zmieniać.

Pierwsza wzmianka: [rozdział 05](05%20Autoryzacja.md#term-mass-assignment).

<a id="hash-function"></a>
## Funkcja skrótu

Hash: jednokierunkowe przekształcenie danych w odcisk o stałej długości. Służy do integralności, nie daje poufności ani autentyczności.

Pierwsza wzmianka: [rozdział 06](06%20Kryptografia%20dla%20programisty.md#term-hash-function).

<a id="encryption"></a>
## Szyfrowanie

Odwracalne z kluczem przekształcenie danych, zapewniające poufność. Symetryczne (AES) lub asymetryczne (RSA, EC).

Pierwsza wzmianka: [rozdział 06](06%20Kryptografia%20dla%20programisty.md#term-encryption).

<a id="hmac"></a>
## HMAC

Hash-based Message Authentication Code: odcisk z danych i wspólnego sekretu, potwierdzający integralność i autentyczność.

Pierwsza wzmianka: [rozdział 06](06%20Kryptografia%20dla%20programisty.md#term-hmac).

<a id="digital-signature"></a>
## Podpis cyfrowy

Podpis składany kluczem prywatnym i weryfikowany kluczem publicznym.

Pierwsza wzmianka: [rozdział 06](06%20Kryptografia%20dla%20programisty.md#term-digital-signature).

<a id="secret-key"></a>
## SECRET_KEY

Główny sekret projektu Django, podstawa podpisów: resetów hasła, sesji w ciasteczkach, django.core.signing.

Pierwsza wzmianka: [rozdział 06](06%20Kryptografia%20dla%20programisty.md#term-secret-key).

<a id="csprng"></a>
## CSPRNG

Kryptograficznie bezpieczny generator liczb losowych. W Pythonie moduł secrets.

Pierwsza wzmianka: [rozdział 06](06%20Kryptografia%20dla%20programisty.md#term-csprng).

<a id="secret"></a>
## Sekret

Wartość, której ujawnienie daje dostęp do systemu lub danych: hasło, klucz API, klucz podpisu, token.

Pierwsza wzmianka: [rozdział 07](07%20Sekrety%20i%20konfiguracja.md#term-secret).

<a id="secret-scanning"></a>
## Skanowanie sekretów

Automatyczne wykrywanie sekretów w kodzie i commitach (GitHub secret scanning, gitleaks, detect-secrets).

Pierwsza wzmianka: [rozdział 07](07%20Sekrety%20i%20konfiguracja.md#term-secret-scanning).

<a id="debug-mode"></a>
## Tryb debug

Ustawienie DEBUG = True, przy którym Django pokazuje szczegółową stronę błędu z kodem, zmiennymi i ustawieniami.

Pierwsza wzmianka: [rozdział 07](07%20Sekrety%20i%20konfiguracja.md#term-debug-mode).

<a id="allowed-hosts"></a>
## ALLOWED_HOSTS

Lista domen, dla których Django obsługuje żądania. Chroni przed atakami przez nagłówek Host.

Pierwsza wzmianka: [rozdział 07](07%20Sekrety%20i%20konfiguracja.md#term-allowed-hosts).

<a id="supply-chain-attack"></a>
## Atak na łańcuch dostaw

Atak wymierzony w zależności, narzędzia lub proces budowania zamiast w samą aplikację.

Pierwsza wzmianka: [rozdział 08](08%20%C5%81a%C5%84cuch%20dostaw.md#term-supply-chain-attack).

<a id="typosquatting"></a>
## Typosquatting

Publikacja złośliwego pakietu o nazwie podobnej do popularnego, liczącej na literówkę.

Pierwsza wzmianka: [rozdział 08](08%20%C5%81a%C5%84cuch%20dostaw.md#term-typosquatting).

<a id="dependency-confusion"></a>
## Dependency confusion

Publikacja w publicznym indeksie pakietu o nazwie wewnętrznej z wyższą wersją, wybieranego zamiast wewnętrznego.

Pierwsza wzmianka: [rozdział 08](08%20%C5%81a%C5%84cuch%20dostaw.md#term-dependency-confusion).

<a id="sca"></a>
## SCA

Software Composition Analysis: automatyczne porównywanie zależności z bazami znanych podatności.

Pierwsza wzmianka: [rozdział 08](08%20%C5%81a%C5%84cuch%20dostaw.md#term-sca).

<a id="sbom"></a>
## SBOM

Software Bill of Materials: spis wszystkich składników oprogramowania z wersjami (CycloneDX, SPDX).

Pierwsza wzmianka: [rozdział 08](08%20%C5%81a%C5%84cuch%20dostaw.md#term-sbom).

<a id="rate-limiting"></a>
## Rate limiting

Ograniczenie liczby żądań w jednostce czasu dla adresu IP, użytkownika, tokenu lub operacji.

Pierwsza wzmianka: [rozdział 09](09%20API%20i%20dane.md#term-rate-limiting).

<a id="insecure-deserialization"></a>
## Niebezpieczna deserializacja

Odtwarzanie obiektów z niezaufanych danych formatem pozwalającym wykonać kod, np. pickle.

Pierwsza wzmianka: [rozdział 09](09%20API%20i%20dane.md#term-insecure-deserialization).

<a id="pii"></a>
## PII

Personally identifiable information: dane osobowe, czyli informacje o zidentyfikowanej lub możliwej do zidentyfikowania osobie.

Pierwsza wzmianka: [rozdział 09](09%20API%20i%20dane.md#term-pii).

<a id="data-minimization"></a>
## Minimalizacja danych

Zasada zbierania i przechowywania tylko tych danych, które są niezbędne.

Pierwsza wzmianka: [rozdział 09](09%20API%20i%20dane.md#term-data-minimization).

<a id="sast"></a>
## SAST

Static Application Security Testing: analiza kodu bez uruchamiania (bandit, semgrep, CodeQL).

Pierwsza wzmianka: [rozdział 10](10%20Proces.md#term-sast).

<a id="dast"></a>
## DAST

Dynamic Application Security Testing: testowanie działającej aplikacji z zewnątrz (OWASP ZAP, Burp).

Pierwsza wzmianka: [rozdział 10](10%20Proces.md#term-dast).

<a id="incident-response"></a>
## Reakcja na incydent

Zaplanowane postępowanie po wykryciu podatności lub naruszenia: przygotowanie, analiza, powstrzymanie, przywrócenie, wnioski.

Pierwsza wzmianka: [rozdział 10](10%20Proces.md#term-incident-response).

<a id="blameless-postmortem"></a>
## Analiza po incydencie bez szukania winnych

Blameless postmortem: szukanie przyczyn incydentu w systemie i procesie, zakończone konkretnymi działaniami.

Pierwsza wzmianka: [rozdział 10](10%20Proces.md#term-blameless-postmortem).
