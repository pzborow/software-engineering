# Design Patterns — Creational

Creational patterns are about **how objects get created** — decoupling
"what to instantiate" from the code that uses the object.

A running theme in this note: several classic GoF creational patterns
exist to work around limitations of statically-typed, class-heavy
languages (Java/C++). Python's first-class functions, modules-as-
singletons, and flexible constructors make some of them close to trivial
— worth calling out explicitly rather than cargo-culting the full pattern.

## Singleton

**Intent**: ensure a class has only one instance, with a single global
point of access to it. **Use when**: exactly one object must coordinate
actions across a system (a config object, a connection pool).

```python
# The classic GoF implementation: override __new__ to always return the same instance
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

a = Singleton()
b = Singleton()
print(a is b)  # True - same object, even though we called Singleton() twice
```

**The Pythonic alternative**: a module is already a singleton — Python
caches imported modules in `sys.modules`, so every `import config`
anywhere in a program gets the exact same module object. For most "one
shared instance" needs, a module-level object beats a `Singleton` class:
```python
# config.py
settings = {"debug": True}

# anywhere else
from config import settings   # always the same dict object, no class needed
```
Reach for the `__new__`-based version only when you need it to be a real
class (e.g. for inheritance, or `isinstance` checks).

## Factory Method

**Intent**: let a method decide which concrete class to instantiate,
instead of the caller hardcoding a constructor call. **Use when**: the
exact type to create depends on input/config and you want callers decoupled
from the concrete classes.

```python
class Dog:
    def speak(self): return "Woof"

class Cat:
    def speak(self): return "Meow"

def animal_factory(kind):     # in Python this is usually just a function - no factory CLASS needed
    return {"dog": Dog, "cat": Cat}[kind]()

print(animal_factory("dog").speak())
print(animal_factory("cat").speak())
```

Output:

```text
Woof
Meow
```

## Abstract Factory

**Intent**: create *families* of related objects without specifying their
concrete classes. **Use when**: you need to guarantee that objects created
together are compatible (e.g. all widgets match one UI theme).

```python
class LightButton:
    def render(self): return "[Light Button]"
class DarkButton:
    def render(self): return "[Dark Button]"
class LightCheckbox:
    def render(self): return "(Light Checkbox)"
class DarkCheckbox:
    def render(self): return "(Dark Checkbox)"

class LightThemeFactory:               # a "family" of matching widget factories
    def create_button(self): return LightButton()
    def create_checkbox(self): return LightCheckbox()

class DarkThemeFactory:
    def create_button(self): return DarkButton()
    def create_checkbox(self): return DarkCheckbox()

def render_ui(factory):    # this code never mentions Light/Dark by name - fully decoupled
    print(factory.create_button().render(), factory.create_checkbox().render())

render_ui(LightThemeFactory())
render_ui(DarkThemeFactory())
```

Output:

```text
[Light Button] (Light Checkbox)
[Dark Button] (Dark Checkbox)
```

## Builder

**Intent**: separate the construction of a complex object from its
representation, building it step by step. **Use when**: an object has many
optional parts/configuration steps and a single giant constructor call
would be unreadable.

```python
class Pizza:
    def __init__(self):
        self.toppings = []
        self.size = None
    def __repr__(self):
        return f"Pizza(size={self.size}, toppings={self.toppings})"

class PizzaBuilder:
    def __init__(self):
        self.pizza = Pizza()
    def set_size(self, size):
        self.pizza.size = size
        return self          # returning self enables fluent/chained calls
    def add_topping(self, topping):
        self.pizza.toppings.append(topping)
        return self
    def build(self):
        return self.pizza

pizza = PizzaBuilder().set_size("L").add_topping("cheese").add_topping("olives").build()
print(pizza)
```

**Note**: in Python, a lot of "Builder" use cases are handled just as well
by keyword arguments with defaults, or a `@dataclass` — reach for a real
Builder when construction genuinely needs multiple *steps* (validation
between steps, optional stages, a fluent API is a deliberate UX choice),
not just "a constructor with many parameters."

## Prototype

**Intent**: create new objects by copying an existing instance (a
"prototype") instead of instantiating from scratch. **Use when**
constructing an object is expensive, or you want a copy that starts
identical to a template and then diverges.

```python
import copy

class Sheep:
    def __init__(self, name, genes):
        self.name = name
        self.genes = genes
    def clone(self):
        return copy.deepcopy(self)   # Python's copy module makes this pattern nearly free

source = Sheep("source", ["gene1", "gene2"])
dolly = source.clone()
dolly.name = "Dolly"
dolly.genes.append("mutation")

print(source.genes)   # ['gene1', 'gene2'] - unaffected
print(dolly.genes)    # ['gene1', 'gene2', 'mutation'] - independent copy
# (deepcopy, not copy.copy - see the Python gotchas on mutability and shared references
# for why a shallow copy would have let dolly's mutation leak back into source)
```

Output:

```text
['gene1', 'gene2']
['gene1', 'gene2', 'mutation']
```
