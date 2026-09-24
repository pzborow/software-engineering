# SOLID Principles

Five object-oriented design principles, each shown as a violation next to
its fix. Companion to
[../Design patterns/](../Design%20patterns/) — patterns are reusable
*solutions*, SOLID principles are the *reasoning* for why a given design
is better than another.

## S — Single Responsibility Principle

**A class should have only one reason to change.** If a class mixes
unrelated responsibilities, a change to one forces a change (and a retest)
of code that has nothing to do with it.

```python
# Violation: Report both HOLDS data/formatting logic AND knows how to persist itself
class ReportBad:
    def __init__(self, data):
        self.data = data
    def generate(self):
        return f"Report: {self.data}"
    def save_to_file(self, filename):     # a reason to change unrelated to reporting logic
        with open(filename, "w") as f:
            f.write(self.generate())
# If storage moves from files to S3, this class changes for a reason that has
# nothing to do with what a "report" actually is.
```

```python
# Fix: split into two classes, each with exactly one reason to change
class Report:
    def __init__(self, data):
        self.data = data
    def generate(self):
        return f"Report: {self.data}"

class ReportSaver:
    def save(self, report, filename):
        with open(filename, "w") as f:
            f.write(report.generate())

report = Report("sales up 10%")
ReportSaver().save(report, "/tmp/report.txt")
print(open("/tmp/report.txt").read())
```

## O — Open/Closed Principle

**Software entities should be open for extension, but closed for
modification.** Adding a new case shouldn't require editing existing,
already-tested code.

```python
# Violation: adding a new shape means editing this function and re-testing all branches
def area_bad(shape):
    if shape["type"] == "circle":
        return 3.14159 * shape["radius"] ** 2
    elif shape["type"] == "square":
        return shape["side"] ** 2
    raise ValueError("unknown shape")

print(area_bad({"type": "circle", "radius": 2}))
```

```python
# Fix: polymorphism - new shapes are added, existing code is untouched
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Circle(Shape):
    def __init__(self, radius): self.radius = radius
    def area(self): return 3.14159 * self.radius ** 2

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side ** 2

class Triangle(Shape):   # NEW shape - zero changes to Circle, Square, or any calling code
    def __init__(self, base, height): self.base, self.height = base, height
    def area(self): return 0.5 * self.base * self.height

shapes = [Circle(2), Square(3), Triangle(4, 5)]
print([round(s.area(), 2) for s in shapes])
```

## L — Liskov Substitution Principle

**Subtypes must be substitutable for their base type without breaking the
caller's expectations.** If code that works correctly with the base class
breaks when handed a subclass instance instead, the subclass violates LSP
— even if it "is-a" the base type conceptually.

```python
class Rectangle:
    def __init__(self, w, h): self.w, self.h = w, h
    def set_width(self, w): self.w = w
    def set_height(self, h): self.h = h
    def area(self): return self.w * self.h

class SquareBad(Rectangle):        # mathematically a square IS a rectangle... but:
    def set_width(self, w): self.w = self.h = w    # setting width silently changes height too!
    def set_height(self, h): self.w = self.h = h

def resize_and_check(rect):
    rect.set_width(4)
    rect.set_height(5)
    return rect.area()   # any caller of Rectangle reasonably expects 4*5 = 20 here

print(resize_and_check(Rectangle(2, 2)))    # 20 - as expected
print(resize_and_check(SquareBad(2, 2)))    # 25 - SquareBad broke the caller's assumption!
```

**Fix**: don't force the inheritance relationship just because it sounds
right conceptually. `Square` and `Rectangle` can both implement a common
`Shape` interface (as in the OCP example above) without one inheriting
from the other's mutable-state assumptions.

## I — Interface Segregation Principle

**Clients shouldn't be forced to depend on methods they don't use.**
Prefer several small, focused interfaces over one large, general-purpose
one.

```python
from typing import Protocol

class WorkerBad(Protocol):     # one fat interface for every kind of "worker"
    def work(self): ...
    def eat(self): ...

class RobotBad:
    def work(self): print("working")
    def eat(self):
        raise NotImplementedError("robots don't eat!")   # forced to implement something nonsensical
```

```python
# Fix: split into focused, single-purpose interfaces
class Workable(Protocol):
    def work(self): ...
class Eatable(Protocol):
    def eat(self): ...

class Human:
    def work(self): print("working")
    def eat(self): print("eating")

class Robot:
    def work(self): print("working")   # only implements what it actually needs - no fake eat()

def make_it_work(w: Workable):
    w.work()

make_it_work(Robot())
make_it_work(Human())
```

## D — Dependency Inversion Principle

**Depend on abstractions, not concrete implementations.** High-level
modules (business logic) shouldn't import and instantiate low-level
modules (specific tools) directly — both should depend on an interface,
with the concrete choice injected from outside.

```python
class EmailSender:
    def send(self, msg): print(f"Email: {msg}")

class NotifierBad:                  # hardcodes exactly ONE concrete sender
    def __init__(self):
        self.sender = EmailSender()  # can never notify via SMS without editing this class
    def notify(self, msg):
        self.sender.send(msg)
```

```python
# Fix: depend on an abstraction, inject the concrete implementation
class MessageSender(Protocol):
    def send(self, msg): ...

class SMSSender:
    def send(self, msg): print(f"SMS: {msg}")

class Notifier:
    def __init__(self, sender: MessageSender):   # doesn't care WHICH sender, only the interface
        self.sender = sender
    def notify(self, msg):
        self.sender.send(msg)

Notifier(EmailSender()).notify("hello")
Notifier(SMSSender()).notify("hello")   # swap implementations with zero changes to Notifier
```
