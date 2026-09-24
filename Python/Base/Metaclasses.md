# Metaclasses

Domyślnie klasy są konstruowane przy użyciu type(). Proces tworzenia klasy można dostosować, przekazując argument słowa kluczowego metaclass w linii definicji klasy
```.python
class Meta(type):
    def __new__(mcs, name, bases, class_dict):
        class_obj = super().__new__(mcs, name, bases, class_dict)
		# Do something usefull here
        return class_obj

class MyClass(metaclass=Meta):
    pass

class MySubclass(MyClass):
    pass
```

[Dokumentacja](https://docs.python.org/3/reference/datamodel.html#metaclasses_)

[Przykład](https://www.pythontutorial.net/python-oop/python-metaclass-example/)