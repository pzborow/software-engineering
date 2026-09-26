# Autoryzacja

Autoryzacja odpowiada na pytanie „czy wolno ci to zrobić?”. Jest najczęstszym źródłem poważnych podatności w API, bo frameworki pomagają w niej najmniej. Django i DRF sprawdzą, czy użytkownik jest zalogowany i czy ma uprawnienie do modelu, ale nie wiedzą, które zamówienia należą do którego klienta. Tę wiedzę ma tylko programista i musi ją zapisać w kodzie każdego widoku.

```text
żądanie ──► uwierzytelnienie ──► autoryzacja funkcji ──► autoryzacja obiektu ──► autoryzacja pól
            kim jesteś?          czy możesz wołać ten     czy to twoje            które pola możesz
                                 endpoint?                zamówienie?             zmienić i zobaczyć?
            Django, DRF          permission_classes       get_queryset,           serializer
                                                          has_object_permission
```

## Kim jesteś a co ci wolno

<a id="term-authentication"></a>[Uwierzytelnienie](00%20Glossary%20Security.md#authentication) ustala tożsamość: to jest klient o identyfikatorze 7. <a id="term-authorization"></a>[Authorization](00%20Glossary%20Security.md#authorization), czyli autoryzacja, decyduje, co ta tożsamość może zrobić: klient 7 może zobaczyć swoje zamówienia, ale nie zamówienia klienta 8.

W DRF łatwo je pomylić, bo obie konfiguruje się w tym samym miejscu:

```python
class OrderViewSet(ModelViewSet):
    queryset = Order.objects.all()
    serializer_class = OrderSerializer
    permission_classes = [IsAuthenticated]
```

`IsAuthenticated` sprawdza tylko uwierzytelnienie: czy żądanie ma poprawną sesję albo token. Każdy zalogowany klient dostaje wtedy pełen dostęp do wszystkich zamówień: listę, szczegóły, edycję i usuwanie. Taki widok przechodzi testy, w których klient pobiera własne zamówienie, i jest przy tym poważną podatnością.

Warto też pamiętać, że domyślna wartość `DEFAULT_PERMISSION_CLASSES` w DRF to `AllowAny`. Widok bez jawnie ustawionych uprawnień jest dostępny dla wszystkich, także niezalogowanych. Bezpieczniej ustawić globalnie bardziej restrykcyjną wartość i otwierać wyjątki świadomie:

```python
REST_FRAMEWORK = {
    "DEFAULT_PERMISSION_CLASSES": ["rest_framework.permissions.IsAuthenticated"],
}
```

To tylko punkt wyjścia. Właściwa autoryzacja zaczyna się na poziomie obiektów.

## Cudzy obiekt po identyfikatorze

<a id="term-bola"></a>[BOLA](00%20Glossary%20Security.md#bola) (Broken Object Level Authorization), znana też jako IDOR (Insecure Direct Object Reference), to brak sprawdzenia, czy użytkownik ma prawo do konkretnego obiektu. Wystarczy zmienić identyfikator w adresie: `GET /api/orders/1041/` zamiast `/api/orders/1040/`. To pierwsze miejsce na liście OWASP API Security Top 10.

W Django i DRF są dwa sposoby zapobiegania.

Filtrowanie querysetu. Widok od początku widzi tylko obiekty użytkownika. Cudzy obiekt daje 404, jakby nie istniał, więc nie zdradza nawet tego, że istnieje:

```python
class OrderViewSet(ModelViewSet):
    serializer_class = OrderSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        return Order.objects.filter(customer=self.request.user)

    def perform_create(self, serializer):
        serializer.save(customer=self.request.user)      # właściciel z sesji, a nie z żądania
```

Uprawnienie na poziomie obiektu. `has_object_permission` wywołuje DRF w `get_object()`, czyli przy szczegółach, edycji i usuwaniu:

```python
class IsOrderOwnerOrStaff(BasePermission):
    def has_object_permission(self, request, view, obj):
        return obj.customer_id == request.user.id or request.user.is_staff
```

| | Filtrowanie `get_queryset` | `has_object_permission` |
|---|---|---|
| Działa dla listy | tak | nie, DRF nie wywołuje go dla list |
| Odpowiedź dla cudzego obiektu | 404 | 403, czyli zdradza, że obiekt istnieje |
| Działa w akcjach własnych | tak, jeśli używają `get_queryset` | tylko jeśli wołają `get_object()` |
| Najlepsze do | reguły „widzę tylko swoje” | reguły zależne od stanu obiektu, np. edycja tylko przed wysyłką |

W praktyce stosuje się oba: `get_queryset` jako podstawę, a `has_object_permission` dla reguł dodatkowych.

Gdzie ochrona się kończy:

- akcje `@action` i widoki funkcyjne, które pobierają obiekt przez `Order.objects.get(pk=pk)` zamiast `self.get_object()`,
- zagnieżdżone adresy `/api/customers/8/orders/`: sprawdza się uprawnienie do zamówień, ale nie do klienta z adresu,
- identyfikatory w treści żądania, np. `{"shipping_address_id": 55}` przy tworzeniu zamówienia. Adres też trzeba sprawdzić: `Address.objects.get(pk=55, customer=request.user)`,
- UUID zamiast kolejnych liczb utrudnia zgadywanie, ale nie jest autoryzacją. Identyfikatory wyciekają w logach, linkach i odpowiedziach innych endpointów.

Test, który powinien mieć każdy endpoint z identyfikatorem:

```python
def test_customer_cannot_read_other_customers_order(api_client, customer, other_customer):
    order = OrderFactory(customer=other_customer)
    api_client.force_authenticate(customer)

    response = api_client.get(f"/api/orders/{order.pk}/")

    assert response.status_code == 404
```

## Modele uprawnień

Poza regułą „widzę tylko swoje” sklep ma role: klient, obsługa klienta, magazyn, administrator. Są dwa główne podejścia.

<a id="term-rbac"></a>[RBAC](00%20Glossary%20Security.md#rbac) (Role-Based Access Control): uprawnienia przypisuje się do ról, a role do użytkowników. Django ma to wbudowane: każdy model dostaje uprawnienia `add`, `change`, `delete` i `view`, grupy (`Group`) pełnią rolę ról, a `user.has_perm("shop.change_order")` sprawdza uprawnienie. W DRF klasa `DjangoModelPermissions` mapuje metody HTTP na te uprawnienia.

```python
class Meta:
    permissions = [
        ("refund_order", "Może zwracać płatności za zamówienia"),
        ("view_customer_pii", "Może widzieć pełne dane osobowe klientów"),
    ]

# widok
if not request.user.has_perm("shop.refund_order"):
    raise PermissionDenied
```

<a id="term-abac"></a>[ABAC](00%20Glossary%20Security.md#abac) (Attribute-Based Access Control): decyzja zależy od atrybutów użytkownika, obiektu i kontekstu. Na przykład „pracownik magazynu może zmienić status zamówienia tylko z własnego magazynu i tylko przed wysyłką” albo „zwrot powyżej 1000 zł wymaga roli kierownika”.

| | RBAC | ABAC |
|---|---|---|
| Decyzja zależy od | roli użytkownika | atrybutów użytkownika, obiektu, kontekstu |
| W Django | grupy, `has_perm`, `DjangoModelPermissions` | własne `has_object_permission`, `django-rules` |
| Uprawnienia do pojedynczych obiektów | nie | tak |
| Zaleta | proste, audytowalne, wbudowane | elastyczne, wyraża reguły biznesowe |
| Ryzyko | eksplozja ról („magazyn-kraków-bez-zwrotów”) | reguły rozsiane po kodzie, trudne do przeglądu |

Uprawnienia Django dotyczą całego modelu: `change_order` pozwala zmieniać wszystkie zamówienia. Uprawnienia do konkretnych obiektów dają biblioteki. `django-guardian` przechowuje je w bazie jako przypisania użytkownik–obiekt–uprawnienie. `django-rules` definiuje reguły jako funkcje w kodzie, co zwykle lepiej pasuje do ABAC:

```python
import rules

@rules.predicate
def is_same_warehouse(user, order):
    return order is not None and order.warehouse_id == user.profile.warehouse_id

@rules.predicate
def not_shipped(user, order):
    return order is not None and order.shipped_at is None

rules.add_perm("shop.change_order_status", rules.is_group_member("warehouse") & is_same_warehouse & not_shipped)
```

Reguły biznesowe autoryzacji najlepiej trzymać w jednym miejscu (moduł uprawnień, predykaty `rules`), a nie w każdym widoku osobno. Dzięki temu można je przeglądać i testować.

## Wiele firm w jednej bazie

Sklep rozwija się w platformę dla wielu sprzedawców: każdy ma swoje produkty, zamówienia i klientów, a wszyscy korzystają z jednej instalacji. To <a id="term-multitenancy"></a>[multitenancy](00%20Glossary%20Security.md#multitenancy), a najpoważniejszą podatnością jest wyciek danych między najemcami (tenantami).

Trzy modele izolacji:

| Model | Jak | Izolacja | Koszt |
|---|---|---|---|
| wspólne tabele z kolumną `tenant_id` | każdy model ma klucz obcy do najemcy | tylko w kodzie aplikacji | najniższy |
| schemat bazy na najemcę | PostgreSQL schemas, `django-tenants` | na poziomie bazy | średni, migracje dla każdego schematu |
| baza na najemcę | osobne bazy danych | pełna | najwyższy |

Przy wspólnych tabelach typowe rozwiązanie w Django to manager, który automatycznie filtruje po bieżącym najemcy:

```python
class TenantManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(tenant=get_current_tenant())   # np. z contextvars


class Product(models.Model):
    tenant = models.ForeignKey(Tenant, on_delete=models.CASCADE)
    ...
    objects = TenantManager()
    all_tenants = models.Manager()          # jawnie nazwany, do zadań administracyjnych
```

Miejsca, w których izolacja najczęściej przecieka:

- `Model.all_tenants`, `_base_manager` i relacje odwrotne, które nie przechodzą przez domyślny manager,
- surowy SQL i agregacje w raportach,
- panel admina i komendy zarządzania, gdzie nie ma bieżącego najemcy,
- zadania w tle (Celery), które nie przenoszą kontekstu najemcy z żądania,
- cache z kluczem bez identyfikatora najemcy, np. `cache.get(f"product:{sku}")`,
- indeksy wyszukiwarki, ścieżki plików w S3, eksporty,
- unikalność: `unique=True` na `sku` zamiast `UniqueConstraint(fields=["tenant", "sku"])` zdradza, że SKU istnieje u innego najemcy.

Dodatkową warstwą (defense in depth) jest Row Level Security w PostgreSQL: baza sama filtruje wiersze według zmiennej sesji ustawianej na początku żądania. Nawet błąd w kodzie aplikacji nie ujawni wtedy danych innego najemcy. Najważniejsze są jednak testy: każdy endpoint sprawdza się z użytkownikiem jednego najemcy i danymi drugiego.

## Pola, których nie wolno ustawić

<a id="term-mass-assignment"></a>[Mass assignment](00%20Glossary%20Security.md#mass-assignment) to sytuacja, w której aplikacja zapisuje do modelu wszystkie pola przesłane w żądaniu, także te, których użytkownik nie powinien zmieniać:

```python
# podatne
class CustomerSerializer(serializers.ModelSerializer):
    class Meta:
        model = Customer
        fields = "__all__"

# PATCH /api/me/  {"first_name": "Anna", "is_staff": true, "loyalty_discount": 50}
```

Klient może w ten sposób nadać sobie uprawnienia pracownika, zmienić rabat, cenę w zamówieniu, status płatności albo właściciela obiektu. OWASP API Security Top 10 łączy to z drugą stroną tego samego problemu, czyli nadmiarowymi danymi w odpowiedzi (serializer zwracający hash hasła, notatki wewnętrzne, dane innych klientów), jako Broken Object Property Level Authorization.

Jak unikać:

```python
class CustomerProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = Customer
        fields = ["id", "email", "first_name", "last_name", "phone", "loyalty_discount"]
        read_only_fields = ["id", "email", "loyalty_discount"]


class StaffCustomerSerializer(serializers.ModelSerializer):     # osobny serializer dla pracowników
    class Meta:
        model = Customer
        fields = ["id", "email", "first_name", "last_name", "phone", "loyalty_discount", "is_blocked"]
```

- jawna lista `fields` zamiast `"__all__"` i zamiast `exclude`. Przy `exclude` każde nowe pole modelu automatycznie staje się zapisywalne,
- `read_only_fields` dla pól wyliczanych i ustawianych przez system,
- osobne serializery dla różnych ról i operacji (tworzenie, edycja, podgląd),
- pola własności i stanu (`customer`, `status`, `price`) ustawiane w `perform_create` albo w logice domenowej, a nie z żądania,
- to samo w formularzach Django: `ModelForm` z jawną listą `fields`.

## Co zapamiętać

- Uwierzytelnienie ustala tożsamość, a autoryzacja decyduje o dostępie. `IsAuthenticated` to tylko uwierzytelnienie, a DRF domyślnie ma `AllowAny`.
- BOLA (IDOR) to najczęstsza luka w API. Chroni przed nią `get_queryset` filtrujący po właścicielu (404 dla cudzych), a reguły zależne od stanu obiektu obsługuje `has_object_permission`.
- Luki powstają w `@action`, zagnieżdżonych adresach i identyfikatorach w treści żądania. UUID nie jest autoryzacją, a każdy endpoint potrzebuje testu z cudzym obiektem.
- RBAC w Django to grupy i `has_perm` na poziomie modelu. Uprawnienia do obiektów i reguły ABAC dają `django-guardian` i `django-rules`.
- Multitenancy przecieka przez managery bazowe, surowy SQL, admina, zadania w tle, cache i unikalność. Row Level Security to dodatkowa warstwa.
- Mass assignment zapobiega jawna lista `fields`, `read_only_fields`, osobne serializery i pola własności ustawiane z sesji.

## Pytania sprawdzające

### 23. Czym różni się uwierzytelnienie od autoryzacji i dlaczego `IsAuthenticated` w DRF nie wystarcza?

<details>
<summary>Odpowiedź</summary>

Uwierzytelnienie ustala, kim jest użytkownik, a autoryzacja decyduje, co może zrobić. `IsAuthenticated` sprawdza tylko, czy żądanie ma poprawną sesję lub token, więc każdy zalogowany klient ma dostęp do wszystkich obiektów widoku: listy, szczegółów, edycji i usuwania cudzych zamówień. Dodatkowo domyślne `DEFAULT_PERMISSION_CLASSES` w DRF to `AllowAny`, więc bezpieczniej ustawić globalnie `IsAuthenticated` i dodać autoryzację na poziomie obiektów.

Zobacz: sekcja „Kim jesteś a co ci wolno”.

</details>

### 24. Czym jest IDOR (BOLA) i jak mu zapobiegać w Django i DRF (filtrowanie `get_queryset`, `has_object_permission`)?

<details>
<summary>Odpowiedź</summary>

To brak sprawdzenia, czy użytkownik ma prawo do konkretnego obiektu. Wystarczy zmienić identyfikator w adresie. Jest pierwsza na liście OWASP API Security Top 10. Zapobiega się przez `get_queryset` filtrujący po właścicielu (działa dla list i szczegółów, cudzy obiekt daje 404) oraz `has_object_permission` dla reguł zależnych od stanu (tylko przy `get_object()`, daje 403). Właściciela ustawia się w `perform_create` z sesji. Luki: `@action` i widoki pobierające obiekt bezpośrednio, zagnieżdżone adresy, identyfikatory w treści żądania i złudzenie, że UUID wystarczy. Każdy endpoint potrzebuje testu z cudzym obiektem.

Zobacz: sekcja „Cudzy obiekt po identyfikatorze”.

</details>

### 25. RBAC czy ABAC: jak modelować uprawnienia w Django (grupy, `has_perm`, `django-guardian`, `rules`)?

<details>
<summary>Odpowiedź</summary>

RBAC przypisuje uprawnienia do ról. W Django to grupy, uprawnienia modeli (`add`, `change`, `delete`, `view` i własne w `Meta.permissions`), `has_perm` i `DjangoModelPermissions`. Jest proste i audytowalne, ale działa dla całego modelu i grozi eksplozją ról. ABAC decyduje na podstawie atrybutów użytkownika, obiektu i kontekstu (np. ten sam magazyn i przed wysyłką). Realizuje się go przez `has_object_permission` albo predykaty `django-rules`. `django-guardian` daje uprawnienia do pojedynczych obiektów w bazie. Reguły warto trzymać w jednym module, żeby dało się je przeglądać i testować.

Zobacz: sekcja „Modele uprawnień”.

</details>

### 26. Jak zapewnić izolację danych w aplikacji wielodostępnej (multitenancy) i gdzie najczęściej przecieka?

<details>
<summary>Odpowiedź</summary>

Są trzy modele: wspólne tabele z `tenant_id` (izolacja tylko w kodzie, zwykle przez manager filtrujący po bieżącym najemcy), schemat na najemcę (`django-tenants`) i baza na najemcę. Przecieki pojawiają się w managerach bazowych i relacjach odwrotnych, surowym SQL i raportach, panelu admina i komendach, zadaniach Celery bez kontekstu najemcy, kluczach cache bez identyfikatora najemcy, indeksach wyszukiwania i ścieżkach plików oraz w unikalności bez najemcy. Dodatkową warstwą jest Row Level Security w PostgreSQL, a podstawą testy z danymi dwóch najemców.

Zobacz: sekcja „Wiele firm w jednej bazie”.

</details>

### 27. Czym jest mass assignment i jak uniknąć go w formularzach i serializerach (`fields = "__all__"`, `read_only_fields`)?

<details>
<summary>Odpowiedź</summary>

To zapis do modelu wszystkich pól z żądania, także takich jak `is_staff`, rabat, cena, status czy właściciel. Drugą stroną jest zwracanie nadmiarowych pól w odpowiedzi. OWASP łączy oba jako Broken Object Property Level Authorization. Unika się go przez jawną listę `fields` (nie `"__all__"` i nie `exclude`, bo nowe pola stają się zapisywalne), `read_only_fields`, osobne serializery dla ról i operacji oraz ustawianie pól własności i stanu w `perform_create` lub logice domenowej. W formularzach Django tak samo `ModelForm` z jawnym `fields`.

Zobacz: sekcja „Pola, których nie wolno ustawić”.

</details>
