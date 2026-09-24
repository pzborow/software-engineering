# Complex Type hinting, queryset and list, file, django model

### Objekty typu Django query set

```python
from typing import Union, List
from django.db.models import QuerySet
from my_app.models import MyModel

def somefunc(a_query_set: Union[QuerySet, List[MyModel]]):
    pass

# Wydaje się, że można i tak
def published_posts() -> 'QuerySet[BlogPost]':  # works fine!
    return BlogPost.objects.filter(
        is_published=True,
    )
```

### Object typu Django model

```python
from typing import Union, List
from django.db.models import QuerySet
from my_app.models import MyModel

def somefunc(my_model: MyModel):
    pass
```

[więcej](https://stackoverflow.com/questions/42397502/how-to-use-python-type-hints-with-django-queryset)
### Obiekty typu File

* Use  `IO`  to mean a file without specifying what kind
* Use  `TextIO`  or  `BinaryIO`  if you know the type

This defines the generic type `IO[AnyStr]` and aliases `TextIO` and `BinaryIO` for respectively `IO[str]` and `IO[bytes]`. These representing the types of I/O streams such as returned by open().

## Containters typing

### Iterable

```python
from collections.abc import Iterable
def find_from_osoby(self, q: Optional[str], osoba_ids: Optional[list[int]]) -> Iterable[Osoba]
    pass
```
Chyba najbardziej prawilna wersja, inne są oznaczone jako deprecated

## Generator yield

```python
from typing import ContextManager
@contextmanager
def session() -> ContextManager[Session]:
    yield Session(...)
```