# Other Well-Known Design Principles and Acronyms

DRY, KISS, YAGNI, Law of Demeter, and Composition over Inheritance —
shown as violation vs fix, same style as [01_solid.md](01_solid.md).

## DRY — Don't Repeat Yourself

**Every piece of knowledge should have a single, unambiguous
representation in the system.** Duplicated logic means every future change
has to be found and applied in every copy — miss one, and behavior quietly
diverges.

```python
# Violation: the tax RATE is duplicated as a magic number in two places
def tax_bad_us(price): return price * 1.08
def tax_bad_eu(price): return price * 1.20
print(tax_bad_us(100), tax_bad_eu(100))
# if the US rate changes, whoever edits this has to remember BOTH functions exist
```

```python
# Fix: one source of truth for the rates
TAX_RATES = {"US": 0.08, "EU": 0.20}

def tax(price, country):
    return price * (1 + TAX_RATES[country])

print(tax(100, "US"), tax(100, "EU"))
```

**Caution — DRY is about knowledge, not text.** Two pieces of code that
happen to look similar today but represent different business rules (and
would naturally evolve independently) should usually stay separate.
Merging them "to avoid duplication" creates a false coupling that's often
worse than the duplication it removed.

## KISS — Keep It Simple, Stupid

**Prefer the simplest solution that correctly solves the problem.**
Unnecessary cleverness costs every future reader time, and is more likely
to hide a bug.

```python
def is_even_overcomplicated(n):
    return True if (n % 2 == 0 and not (n % 2 != 0)) else False   # says the same thing twice, badly

def is_even(n):
    return n % 2 == 0

print(is_even_overcomplicated(4), is_even(4))   # identical result, very different reading effort
```

## YAGNI — You Aren't Gonna Need It

**Don't build flexibility/abstraction for a requirement that doesn't exist
yet.** Speculative generality adds real cost today (more code to read,
test, and maintain) for a hypothetical benefit that may never arrive - and
if it does, you'll likely design the abstraction better once you actually
know the second use case, not before.

```python
from abc import ABC, abstractmethod

# Violation: a whole pluggable-strategy architecture built for a feature
# that has exactly ONE implementation and no concrete plan for a second
class DiscountStrategy(ABC):
    @abstractmethod
    def apply(self, price): ...

class NoDiscountStrategy(DiscountStrategy):
    def apply(self, price): return price

class PriceCalculatorBad:
    def __init__(self, strategy: DiscountStrategy = None):
        self.strategy = strategy or NoDiscountStrategy()
    def calculate(self, price):
        return self.strategy.apply(price)

print(PriceCalculatorBad().calculate(100))
```

```python
# Fix: write what today's requirement actually needs
def calculate_price(price):
    return price

print(calculate_price(100))
# When a second discount type is ACTUALLY needed, introduce the abstraction then -
# informed by two real cases instead of one imagined one.
```

## Law of Demeter ("don't talk to strangers")

**An object should only call methods on: itself, its own fields, objects
passed into its methods, or objects it creates.** Reaching through one
object to grab another and call a method on *that* couples your code to
the internal structure of something you don't own.

```python
class Engine:
    def start(self): print("engine started")

class Car:
    def __init__(self):
        self.engine = Engine()

class Driver:
    def __init__(self, car):
        self.car = car
    def start_car_bad(self):
        self.car.engine.start()   # reaches THROUGH car into its internal engine - a "train wreck" call

Driver(Car()).start_car_bad()   # works today, but Driver now depends on Car having an .engine at all
```

```python
# Fix: Car exposes its own method, hiding that an Engine exists inside at all
class CarGood:
    def __init__(self):
        self.engine = Engine()
    def start(self):
        self.engine.start()

class DriverGood:
    def __init__(self, car):
        self.car = car
    def start_car(self):
        self.car.start()   # Driver never needs to know Car even HAS an engine

DriverGood(CarGood()).start_car()
# if Car later switches to an ElectricMotor instead of an Engine, Driver's code is unaffected
```

## Composition over Inheritance

**Prefer building behavior by combining small, focused objects over
deep inheritance hierarchies.** Inheritance locks in a relationship at
class-definition time and only offers one axis of variation at a time;
composition lets you mix and swap behaviors at runtime.

```python
# Instead of: class MallardDuck(Duck), class RubberDuck(Duck) each hardcoding fly behavior
# (which explodes combinatorially once you add Quack/NoQuack, Swim/NoSwim, ...)
class FlyBehavior:
    def fly(self): return "flying"

class NoFly:
    def fly(self): return "can't fly"

class Duck:
    def __init__(self, fly_behavior):
        self.fly_behavior = fly_behavior   # behavior is composed in, not inherited
    def perform_fly(self):
        return self.fly_behavior.fly()

mallard = Duck(FlyBehavior())
rubber_duck = Duck(NoFly())
print(mallard.perform_fly(), rubber_duck.perform_fly())
# a duck's flying ability can even be swapped at runtime: mallard.fly_behavior = NoFly()
```
