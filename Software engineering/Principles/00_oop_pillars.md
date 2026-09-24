# The Four Pillars of OOP

Encapsulation, Abstraction, Inheritance, Polymorphism — the foundational
OOP principles that SOLID ([01_solid.md](01_solid.md)) builds on top
of.

## Encapsulation

**Bundle data with the methods that operate on it, and control access to
that data** — so invariants (like "balance can't go negative from an
invalid deposit") are enforced in one place instead of trusted to every
caller.

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance     # leading underscore: "protected", by convention only
        self.__pin = "1234"          # leading double underscore: name-mangled (see below)

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("deposit must be positive")
        self._balance += amount      # the ONLY path that can change balance - validation guaranteed

    @property
    def balance(self):
        return self._balance         # read access without a way to write around deposit()

acc = BankAccount(100)
acc.deposit(50)
print(acc.balance)

try:
    acc.balance = 1_000_000   # no setter defined - can't bypass deposit()'s validation this way
except AttributeError as e:
    print("AttributeError:", e)
```

Output:

```text
150
AttributeError: can't set attribute 'balance'
```

**Python doesn't have true private attributes.** A single leading
underscore is purely a convention ("internal, don't touch"), and a double
leading underscore triggers **name mangling** — `__pin` inside `BankAccount`
actually becomes `_BankAccount__pin`, which makes accidental collisions
in subclasses less likely, but doesn't actually block access:

```python
print(acc.__dict__.keys())        # dict_keys(['_balance', '_BankAccount__pin'])
print(acc._BankAccount__pin)      # still reachable if you know the mangled name - "we're all adults here"
```

## Abstraction

**Expose *what* an object does through a simple interface, hide *how* it
does it.** Callers depend on the interface, never on the implementation
details behind it — which is also what makes those details free to change
later.

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, amount): ...    # the interface says WHAT ("you can pay"), not HOW

class CreditCardProcessor(PaymentProcessor):
    def pay(self, amount):
        print(f"Charging ${amount} to credit card (talks to card network internally)")

class PayPalProcessor(PaymentProcessor):
    def pay(self, amount):
        print(f"Charging ${amount} via PayPal (talks to PayPal API internally)")

def checkout(processor: PaymentProcessor, amount):
    processor.pay(amount)   # checkout() never needs to know HOW payment actually happens

checkout(CreditCardProcessor(), 50)
checkout(PayPalProcessor(), 50)
```

## Inheritance

**A class can reuse and extend the behavior of another class.** Use it for
genuine "is-a" relationships where the subclass really is a more specific
version of the parent — not just to avoid retyping a couple of methods
(see [../Design patterns/](../Design%20patterns/)'s note on "Composition over
Inheritance" in `02_other_principles.md` for the tradeoff).

```python
class Vehicle:
    def __init__(self, make, model):
        self.make, self.model = make, model
    def describe(self):
        return f"{self.make} {self.model}"

class ElectricVehicle(Vehicle):
    def __init__(self, make, model, battery_kwh):
        super().__init__(make, model)     # reuse the parent's init logic instead of repeating it
        self.battery_kwh = battery_kwh
    def describe(self):
        return f"{super().describe()} ({self.battery_kwh}kWh battery)"   # extend, not just replace

ev = ElectricVehicle("Tesla", "Model 3", 75)
print(ev.describe())
```

## Polymorphism

**The same call (`.speak()`, `.area()`, ...) produces different behavior
depending on the actual object it's called on**, so calling code can treat
a whole family of types uniformly.

```python
class Dog:
    def speak(self): return "Woof"
class Cat:
    def speak(self): return "Meow"
class Duck:
    def speak(self): return "Quack"

for animal in [Dog(), Cat(), Duck()]:
    print(animal.speak())
# note: none of these classes share a common base class at all - Python's duck typing means
# polymorphism here doesn't even require inheritance, unlike languages that need a shared interface
```

```python
# The more traditional (inheritance-based) version, for contrast:
class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Circle(Shape):
    def __init__(self, r): self.r = r
    def area(self): return 3.14159 * self.r ** 2

class Square(Shape):
    def __init__(self, s): self.s = s
    def area(self): return self.s ** 2

for shape in [Circle(2), Square(3)]:
    print(round(shape.area(), 2))   # same .area() call, correct behavior picked per actual type
```
