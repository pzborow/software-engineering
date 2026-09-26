# Podatności webowe

Przeglądarka to środowisko, w którym kod z wielu źródeł działa obok siebie: strona sklepu, skrypty analityczne, ramki partnerów, rozszerzenia. Większość podatności webowych polega na tym, że napastnik zmusza przeglądarkę ofiary do wykonania czegoś w kontekście sklepu: uruchomienia jego skryptu, wysłania żądania z jej ciasteczkami albo odczytania odpowiedzi. Osobną kategorią jest serwer, który sam wykonuje żądania w imieniu napastnika. Ten rozdział przechodzi przez sześć najważniejszych tematów i pokazuje, co z nich załatwia Django.

```text
podatność     kto wykonuje atak            co chroni Django                  co zostaje
XSS           przeglądarka ofiary          escapowanie szablonów             mark_safe, JS, API + innerHTML
CSRF          przeglądarka ofiary          token, Origin, SameSite           csrf_exempt, GET zmieniające stan
CORS          przeglądarka (konfiguracja)  nic, to pakiet django-cors-headers  zbyt szerokie reguły
SSRF          serwer sklepu                nic                               walidacja URL-i i sieci
clickjacking  przeglądarka ofiary          X-Frame-Options: DENY             wyjątki
nagłówki      przeglądarka                 SecurityMiddleware, check --deploy  HSTS, CSP, konfiguracja
```

## Cudzy skrypt na naszej stronie

<a id="term-xss"></a>[XSS](00%20Glossary%20Security.md#xss) (cross-site scripting) to wstrzyknięcie skryptu, który wykona się w przeglądarce innego użytkownika w kontekście sklepu. Skrypt ma dostęp do wszystkiego, do czego ma dostęp strona: może czytać dane na ekranie, wykonywać żądania z sesją ofiary, zmieniać formularze i przekierowywać płatności.

Trzy odmiany:

| Odmiana | Skąd pochodzi skrypt | Przykład w sklepie |
|---|---|---|
| stored | zapisany w bazie, wyświetlany innym | recenzja produktu z `<script>` |
| reflected | parametr żądania odbity w odpowiedzi | `/search/?q=<script>…</script>` w „Wyniki dla: …” |
| DOM-based | skrypt na stronie wstawia dane do DOM bez serwera | `element.innerHTML = location.hash.slice(1)` |

Django chroni przed dwiema pierwszymi odmianami przez automatyczne escapowanie w szablonach. Każda zmienna `{{ … }}` jest zamieniana tak, że znaki `<`, `>`, `&`, `'` i `"` stają się encjami HTML:

```django
<p>{{ review.text }}</p>
{# review.text = "<script>steal()</script>" #}
{# wynik:       <p>&lt;script&gt;steal()&lt;/script&gt;</p> #}
```

Dzięki temu tekst użytkownika zawsze jest wyświetlany jako tekst, a nie interpretowany jako HTML.

## Gdzie escapowanie nie wystarcza

Escapowanie HTML chroni tylko w kontekście HTML, czyli między znacznikami i w atrybutach ujętych w cudzysłów. W innych miejscach nie wystarcza:

Jawne wyłączenie. `mark_safe`, filtr `|safe` i `{% autoescape off %}` mówią Django, że tekst jest już bezpiecznym HTML-em. Jeśli zawiera dane użytkownika, to jest XSS:

```python
# podatne: dane użytkownika w tekście oznaczonym jako bezpieczny
return mark_safe(f"<b>{product.name}</b> w promocji")

# bezpieczne: format_html escapuje argumenty, a mark_safe dotyczy tylko szablonu
return format_html("<b>{}</b> w promocji", product.name)
```

Kontekst JavaScript. Escapowanie HTML nie chroni wewnątrz `<script>`, bo tam obowiązują inne reguły. Do przekazywania danych do skryptu służy filtr `json_script`, który wstawia JSON w bezpiecznym znaczniku:

```django
{# podatne #}
<script>const cart = {{ cart_json|safe }};</script>

{# bezpieczne #}
{{ cart|json_script:"cart-data" }}
<script>const cart = JSON.parse(document.getElementById("cart-data").textContent);</script>
```

Kontekst URL. Escapowanie nie blokuje schematu `javascript:` w linkach. `<a href="{{ customer.website }}">` z wartością `javascript:alert(document.cookie)` wykona skrypt po kliknięciu. Adresy od użytkowników sprawdza się pod kątem schematu (`http`, `https`) przy zapisie, np. przez `URLValidator(schemes=["http", "https"])`.

Atrybuty bez cudzysłowów i style. `<div class={{ x }}>` pozwala dopisać nowy atrybut przez spację, np. `onmouseover=…`. Atrybuty zawsze ujmuje się w cudzysłów.

API i frontend. DRF zwraca JSON, więc szablony Django nie są w ogóle używane. Ochrona przed XSS przechodzi na frontend: React escapuje domyślnie, ale `dangerouslySetInnerHTML`, `v-html` w Vue i `element.innerHTML` wracają do problemu. Jeśli treść musi zawierać HTML (np. opis produktu z edytora), oczyszcza się ją biblioteką z listą dozwolonych znaczników: `nh3` po stronie serwera albo DOMPurify w przeglądarce.

Ostatnią linią obrony przed XSS jest Content Security Policy, opisana na końcu rozdziału.

## Żądanie wysłane w imieniu ofiary

<a id="term-csrf"></a>[CSRF](00%20Glossary%20Security.md#csrf) (cross-site request forgery) wykorzystuje to, że przeglądarka automatycznie dołącza ciasteczka do żądań. Strona napastnika zawiera ukryty formularz, który wysyła `POST /account/email/` do sklepu. Przeglądarka ofiary dołącza ciasteczko sesji, więc sklep widzi prawidłowo zalogowanego użytkownika i zmienia adres e-mail na adres napastnika.

```html
<!-- na stronie evil.example -->
<form action="https://shop.example/account/email/" method="post">
  <input type="hidden" name="email" value="attacker@evil.example">
</form>
<script>document.forms[0].submit()</script>
```

Django chroni przed CSRF przez `CsrfViewMiddleware`, włączone w każdym nowym projekcie. Warstwy ochrony:

- token CSRF: każdy formularz zawiera `{% csrf_token %}`, a żądania AJAX nagłówek `X-CSRFToken`. Middleware porównuje go z wartością w ciasteczku `csrftoken`. Strona napastnika nie zna tokenu, bo nie może odczytać ani strony sklepu, ani jego ciasteczek,
- sprawdzanie nagłówka `Origin` (i `Referer` przy HTTPS): żądanie z obcej domeny jest odrzucane, chyba że domena jest w `CSRF_TRUSTED_ORIGINS`,
- atrybut <a id="term-samesite"></a>[SameSite](00%20Glossary%20Security.md#samesite) ciasteczek: Django domyślnie ustawia `SameSite=Lax` dla ciasteczek sesji i CSRF, więc przeglądarka nie wysyła ich w żądaniach POST inicjowanych z innych domen.

Ochrona kończy się w trzech miejscach.

Metody bezpieczne, które zmieniają stan. Django nie sprawdza CSRF dla GET, HEAD, OPTIONS i TRACE, bo te metody nie powinny niczego zmieniać. Widok `GET /cart/clear/` albo `GET /newsletter/unsubscribe/` jest podatny, bo wystarczy obrazek `<img src="https://shop.example/cart/clear/">` na obcej stronie.

`@csrf_exempt`. Często dodawany „bo formularz nie działa”. Uzasadniony tylko wtedy, gdy żądanie jest uwierzytelniane inaczej niż ciasteczkiem, np. webhook od operatora płatności podpisany HMAC-iem (rozdział 06):

```python
@csrf_exempt                                  # brak ciasteczek: webhook przychodzi z serwera operatora
@require_POST
def payment_webhook(request):
    if not valid_signature(request.body, request.headers.get("X-Signature", "")):
        return HttpResponseForbidden()
    ...
```

API a CSRF. W DRF `SessionAuthentication` wymusza CSRF dla zalogowanych użytkowników, bo sesja jest w ciasteczku. `TokenAuthentication` i JWT w nagłówku `Authorization` nie są podatne na CSRF, bo przeglądarka nie dołącza tych nagłówków automatycznie. Jeśli jednak token JWT trzymany jest w ciasteczku, wraca problem CSRF i trzeba go rozwiązać.

## Współdzielenie zasobów między domenami

Przeglądarki stosują same-origin policy: skrypt ze strony `evil.example` może wysłać żądanie do `api.shop.example`, ale nie może odczytać odpowiedzi. <a id="term-cors"></a>[CORS](00%20Glossary%20Security.md#cors) (Cross-Origin Resource Sharing) to mechanizm, przez który serwer pozwala wybranym domenom odczytywać swoje odpowiedzi. Serwer wysyła nagłówek `Access-Control-Allow-Origin`, a dla żądań nietypowych przeglądarka najpierw pyta o zgodę żądaniem preflight `OPTIONS`.

Dwie rzeczy, które warto powiedzieć na rozmowie:

- CORS nie chroni serwera. To poluzowanie ochrony przeglądarki, a nie zabezpieczenie. Żądanie z `curl` albo z innego serwera nigdy nie jest ograniczane przez CORS,
- CORS nie zastępuje CSRF. Nawet bez nagłówków CORS przeglądarka wyśle formularz POST do obcej domeny. Nie pozwoli tylko odczytać odpowiedzi.

Django nie obsługuje CORS samo. Standardem jest pakiet `django-cors-headers`. Typowe błędy konfiguracji:

```python
# podatne: każda domena może czytać odpowiedzi z ciasteczkami zalogowanego użytkownika
CORS_ALLOW_ALL_ORIGINS = True
CORS_ALLOW_CREDENTIALS = True

# podatne: wyrażenie pasuje też do shop.example.evil.com i evilshop.example
CORS_ALLOWED_ORIGIN_REGEXES = [r"https://.*shop\.example.*"]

# bezpieczne: jawna lista, credentials tylko jeśli naprawdę potrzebne
CORS_ALLOWED_ORIGINS = ["https://shop.example", "https://admin.shop.example"]
CORS_ALLOW_CREDENTIALS = True
```

Przy `CORS_ALLOW_ALL_ORIGINS` i credentials pakiet odsyła w nagłówku domenę z żądania, więc każda strona może odczytać dane zalogowanego klienta. Specyfikacja zabrania `*` razem z credentials, ale odbijanie dowolnej domeny daje ten sam skutek. Uwagi wymaga też origin `null`, wysyłany m.in. przez ramki z atrybutem `sandbox`. Nie powinien trafiać na listę dozwolonych.

## Serwer jako pośrednik napastnika

<a id="term-ssrf"></a>[SSRF](00%20Glossary%20Security.md#ssrf) (server-side request forgery) to zmuszenie serwera do wykonania żądania pod adres wskazany przez napastnika. Serwer zwykle ma dostęp do miejsc niedostępnych z internetu: usług wewnętrznych, paneli administracyjnych, baz, a w chmurze do endpointu metadanych (`169.254.169.254`), który może zwrócić klucze dostępu do konta.

W sklepie SSRF grozi wszędzie, gdzie serwer pobiera coś spod adresu podanego przez użytkownika: import produktów z URL, podgląd linku, awatar z adresu, webhooki konfigurowane przez partnerów.

```python
# podatne: supplier_url = "http://169.254.169.254/latest/meta-data/iam/security-credentials/"
response = requests.get(supplier_url)
```

Django nie daje żadnej ochrony przed SSRF, bo to kod aplikacji wykonuje żądanie. Obrona ma kilka warstw:

```python
import ipaddress
import socket
from urllib.parse import urlparse

ALLOWED_SCHEMES = {"https"}
ALLOWED_PORTS = {443}


def resolve_public_ip(url: str) -> str:
    parts = urlparse(url)
    if parts.scheme not in ALLOWED_SCHEMES or (parts.port or 443) not in ALLOWED_PORTS:
        raise ValidationError("Niedozwolony adres")
    infos = socket.getaddrinfo(parts.hostname, parts.port or 443, proto=socket.IPPROTO_TCP)
    ips = {ipaddress.ip_address(info[4][0]) for info in infos}
    if any(ip.is_private or ip.is_loopback or ip.is_link_local or ip.is_reserved or ip.is_multicast
           for ip in ips):
        raise ValidationError("Adres wewnętrzny jest niedozwolony")
    return str(next(iter(ips)))
```

Zasady:

- lista dozwolonych domen, jeśli to możliwe (import tylko z domen zweryfikowanych dostawców), zamiast listy zabronionych,
- tylko `https` i standardowe porty,
- sprawdzenie adresu IP po rozwiązaniu nazwy, bo nazwa `internal.evil.example` może wskazywać na `10.0.0.5`,
- połączenie z już sprawdzonym adresem IP. Inaczej napastnik może podmienić odpowiedź DNS między sprawdzeniem a połączeniem (DNS rebinding),
- wyłączone przekierowania (`allow_redirects=False`) albo ponowna walidacja każdego przekierowania,
- timeout i limit rozmiaru odpowiedzi,
- warstwa sieciowa: wychodzący ruch serwera przez proxy z listą dozwolonych celów (np. Smokescreen), blokada adresów metadanych, w AWS IMDSv2 wymagający tokenu.

Walidacja w kodzie łatwo przepuszcza przypadki brzegowe (IPv6, zapisy dziesiętne adresów, przekierowania), więc ochrona na poziomie sieci jest najważniejszą warstwą.

## Nagłówki bezpieczeństwa

Przeglądarki mają mechanizmy ochronne, które serwer włącza nagłówkami odpowiedzi. Django ustawia część z nich przez `SecurityMiddleware` i `XFrameOptionsMiddleware`.

<a id="term-clickjacking"></a>[Clickjacking](00%20Glossary%20Security.md#clickjacking) polega na osadzeniu strony sklepu w niewidocznej ramce na stronie napastnika i skłonieniu ofiary do kliknięcia w przycisk, np. „Zamów” albo „Usuń konto”. Django domyślnie wysyła `X-Frame-Options: DENY`, więc strony nie da się osadzić w ramce. Wyjątki robi się dekoratorem `@xframe_options_sameorigin` albo `@xframe_options_exempt`, tylko dla widoków, które naprawdę muszą być osadzane.

<a id="term-hsts"></a>[HSTS](00%20Glossary%20Security.md#hsts) (HTTP Strict Transport Security) każe przeglądarce przez określony czas łączyć się z domeną wyłącznie przez HTTPS. Chroni przed atakiem, w którym napastnik w sieci Wi-Fi przechwytuje pierwsze żądanie HTTP i nie pozwala przejść na HTTPS.

<a id="term-csp"></a>[CSP](00%20Glossary%20Security.md#csp) (Content Security Policy) określa, skąd strona może ładować skrypty, style, obrazy i ramki. Dobrze ustawiona CSP blokuje wykonanie wstrzykniętego skryptu, nawet jeśli XSS się zdarzy, bo skrypty inline i z nieznanych domen nie są uruchamiane. Django 6.0 dodało wbudowaną obsługę CSP (ustawienie `SECURE_CSP`). We wcześniejszych wersjach używa się pakietu `django-csp`.

| Nagłówek | Ustawienie Django | Domyślnie | Zalecane |
|---|---|---|---|
| `Strict-Transport-Security` | `SECURE_HSTS_SECONDS`, `SECURE_HSTS_INCLUDE_SUBDOMAINS`, `SECURE_HSTS_PRELOAD` | wyłączony | rok, po sprawdzeniu, że wszystkie subdomeny działają na HTTPS |
| przekierowanie na HTTPS | `SECURE_SSL_REDIRECT` | wyłączone | włączone albo realizowane na proxy |
| `X-Frame-Options` | `X_FRAME_OPTIONS` | `DENY` | `DENY` |
| `X-Content-Type-Options` | `SECURE_CONTENT_TYPE_NOSNIFF` | `nosniff` | `nosniff` |
| `Referrer-Policy` | `SECURE_REFERRER_POLICY` | `same-origin` | `same-origin` albo `strict-origin-when-cross-origin` |
| `Cross-Origin-Opener-Policy` | `SECURE_CROSS_ORIGIN_OPENER_POLICY` | `same-origin` | `same-origin` |
| `Content-Security-Policy` | `SECURE_CSP` (Django 6.0) albo `django-csp` | brak | zaczynając od trybu `Report-Only` |

HSTS włącza się ostrożnie. Po ustawieniu długiego czasu i `preload` domeny nie da się łatwo wycofać z HTTPS. Dobrze zacząć od kilku minut, sprawdzić wszystkie subdomeny i dopiero potem wydłużać.

Polecenie `python manage.py check --deploy` sprawdza większość tych ustawień, a także `DEBUG`, `SECRET_KEY`, `ALLOWED_HOSTS` i flagi `Secure` ciasteczek. Warto uruchamiać je w pipeline'ie CI z ustawieniami produkcyjnymi.

## Co zapamiętać

- Django escapuje zmienne w szablonach, co chroni przed XSS stored i reflected w kontekście HTML.
- Escapowanie nie wystarcza przy `mark_safe` i `|safe`, w `<script>` (użyj `json_script`), w URL-ach (`javascript:`), w atrybutach bez cudzysłowów i we frontendzie z `innerHTML`.
- `CsrfViewMiddleware` chroni przez token, `Origin` i `SameSite=Lax`. Luki powstają przy GET zmieniającym stan i przy `@csrf_exempt` bez innego uwierzytelnienia.
- CORS nie chroni serwera ani nie zastępuje CSRF. Najczęstszy błąd to wszystkie domeny razem z credentials.
- Django nie chroni przed SSRF. Potrzebne są lista dozwolonych adresów, sprawdzenie IP po rozwiązaniu nazwy, połączenie z tym IP, brak przekierowań, limity i ochrona na poziomie sieci.
- `SecurityMiddleware` i `check --deploy` pokrywają większość nagłówków, ale HSTS i CSP trzeba włączyć i dostroić samemu.

## Pytania sprawdzające

### 11. Czym jest XSS (stored, reflected, DOM) i jak chroni przed nim automatyczne escapowanie w szablonach Django?

<details>
<summary>Odpowiedź</summary>

XSS to wstrzyknięcie skryptu, który wykona się w przeglądarce innego użytkownika w kontekście strony i ma dostęp do jej danych i sesji. Stored: skrypt zapisany w bazie (np. recenzja). Reflected: parametr żądania odbity w odpowiedzi. DOM-based: skrypt na stronie wstawia dane do DOM bez udziału serwera. Django escapuje każdą zmienną `{{ … }}`, zamieniając `<`, `>`, `&`, `'` i `"` na encje, więc tekst użytkownika jest wyświetlany jako tekst. To chroni przed stored i reflected w kontekście HTML.

Zobacz: sekcja „Cudzy skrypt na naszej stronie”.

</details>

### 12. Gdzie escapowanie Django nie wystarcza (`mark_safe`, `|safe`, dane w `<script>` i atrybutach, `json_script`, API zwracające HTML)?

<details>
<summary>Odpowiedź</summary>

Przy jawnym wyłączeniu (`mark_safe`, `|safe`, `autoescape off`) z danymi użytkownika. Wtedy zamiast f-stringa używa się `format_html`. W kontekście JavaScript, gdzie dane przekazuje się przez `json_script`. W URL-ach, gdzie `javascript:` przechodzi przez escapowanie, więc waliduje się schemat. W atrybutach bez cudzysłowów. W API z frontendem używającym `innerHTML`, `dangerouslySetInnerHTML` czy `v-html`, gdzie HTML oczyszcza się (`nh3`, DOMPurify). Ostatnią linią obrony jest CSP.

Zobacz: sekcja „Gdzie escapowanie nie wystarcza”.

</details>

### 13. Jak działa CSRF i jak działa ochrona Django (token, `CsrfViewMiddleware`, `SameSite`)? Kiedy `@csrf_exempt` jest uzasadnione, a kiedy to luka?

<details>
<summary>Odpowiedź</summary>

CSRF wykorzystuje automatyczne dołączanie ciasteczek: strona napastnika wysyła żądanie do sklepu z sesją ofiary. `CsrfViewMiddleware` porównuje token z formularza lub nagłówka `X-CSRFToken` z ciasteczkiem, sprawdza `Origin` i `Referer` względem `CSRF_TRUSTED_ORIGINS`, a Django ustawia `SameSite=Lax` dla ciasteczek sesji i CSRF. Luki to GET zmieniający stan (nie jest sprawdzany) i `@csrf_exempt`, uzasadnione tylko przy uwierzytelnieniu bez ciasteczek, np. webhook podpisany HMAC-iem. JWT w nagłówku nie jest podatny, ale JWT w ciasteczku już tak.

Zobacz: sekcja „Żądanie wysłane w imieniu ofiary”.

</details>

### 14. Czym jest CORS, czego nie chroni i jakie są typowe błędy konfiguracji `django-cors-headers` (`CORS_ALLOW_ALL_ORIGINS` z credentials)?

<details>
<summary>Odpowiedź</summary>

CORS to mechanizm, przez który serwer pozwala wybranym domenom odczytywać swoje odpowiedzi w przeglądarce, czyli poluzowanie same-origin policy. Nie chroni serwera (`curl` go nie respektuje) i nie zastępuje CSRF, bo formularz POST do obcej domeny i tak zostanie wysłany. Typowe błędy: `CORS_ALLOW_ALL_ORIGINS` z `CORS_ALLOW_CREDENTIALS`, gdzie pakiet odbija domenę z żądania, więc każda strona czyta dane zalogowanego klienta, zbyt luźne wyrażenia w `CORS_ALLOWED_ORIGIN_REGEXES` oraz origin `null` na liście. Poprawnie: jawna lista `CORS_ALLOWED_ORIGINS`.

Zobacz: sekcja „Współdzielenie zasobów między domenami”.

</details>

### 15. Czym jest SSRF i jak się przed nim bronić, skoro Django nie daje tu żadnej ochrony (webhooki, podgląd URL, import z adresu)?

<details>
<summary>Odpowiedź</summary>

SSRF to zmuszenie serwera do żądania pod adres napastnika, np. do usług wewnętrznych albo endpointu metadanych chmury z kluczami dostępu. Obrona: lista dozwolonych domen, tylko `https` i standardowe porty, sprawdzenie adresu IP po rozwiązaniu nazwy (prywatne, loopback, link-local, zarezerwowane), połączenie z już sprawdzonym IP przeciw DNS rebinding, brak przekierowań lub ich walidacja, timeout i limit rozmiaru. Najważniejsza jest warstwa sieciowa: proxy wychodzące z listą celów, blokada metadanych, IMDSv2.

Zobacz: sekcja „Serwer jako pośrednik napastnika”.

</details>

### 16. Jakie nagłówki bezpieczeństwa warto ustawić (HSTS, CSP, X-Frame-Options, Referrer-Policy) i co z tego daje `SecurityMiddleware` oraz `manage.py check --deploy`?

<details>
<summary>Odpowiedź</summary>

HSTS wymusza HTTPS (`SECURE_HSTS_SECONDS`, domyślnie wyłączony, włączany ostrożnie). CSP ogranicza źródła skryptów i jest ostatnią linią obrony przed XSS (`SECURE_CSP` od Django 6.0, wcześniej `django-csp`, start od `Report-Only`). `X-Frame-Options: DENY` chroni przed clickjackingiem (domyślnie w Django). Dalej `X-Content-Type-Options: nosniff`, `Referrer-Policy: same-origin` i `Cross-Origin-Opener-Policy`, domyślnie ustawiane przez `SecurityMiddleware`. `check --deploy` sprawdza te ustawienia oraz `DEBUG`, `SECRET_KEY`, `ALLOWED_HOSTS` i flagi ciasteczek. Warto uruchamiać je w CI.

Zobacz: sekcja „Nagłówki bezpieczeństwa”.

</details>
