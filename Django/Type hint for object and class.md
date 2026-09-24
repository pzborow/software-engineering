# Type hint for object and class

```python
class Animal:
    def __init__(self, *, name: str):
        self.name = name


class Cat(Animal):
    ...


class Dog(Animal):
    ...


def make_animal(animal_class: type[Animal], name: str) -> Animal:
    return animal_class(name=name)


animal = make_animal(Dog, "Kevin")
```

To działa dla Python 3.9. Dla starszych wersji trzeba zaimportować `from typing import Type`



[source](https://adamj.eu/tech/2021/05/16/python-type-hints-return-class-not-instance/)

```python
from typing import Type

class X:
    """some class"""

def foo_my_class(my_class: Type[X], bar: str) -> None:
    """ Operate on my_class """
```
[source](https://stackoverflow.com/questions/33387042/type-hinting-argument-of-type-class)