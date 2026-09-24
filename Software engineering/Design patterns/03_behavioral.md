# Design Patterns — Behavioral

Behavioral patterns are about **how objects communicate and distribute
responsibility** — algorithms, control flow, and interaction between
objects.

## Strategy

**Intent**: define a family of interchangeable algorithms and make them
swappable at runtime. **Use when**: you have several ways to do the same
job (sorting, pricing, validation) and want to pick one without an `if/elif`
chain scattered through the codebase.

```python
def bubble_sort(data): return sorted(data)  # stand-ins for real algorithm implementations
def quick_sort(data): return sorted(data)

class Sorter:
    def __init__(self, strategy):
        self.strategy = strategy    # in Python, a "strategy" is often just a function - no interface needed
    def sort(self, data):
        return self.strategy(data)

s = Sorter(quick_sort)
print(s.sort([3, 1, 2]))

s.strategy = bubble_sort   # swap the algorithm at runtime, no subclassing needed
print(s.sort([5, 4, 6]))
```

**Note**: in a language without first-class functions, Strategy requires a
family of classes each implementing one `execute()` method. In Python,
since functions are objects you can pass around, that ceremony often
collapses into "the strategy IS a function" — as shown above.

## Observer

**Intent**: define a one-to-many dependency so that when one object
changes state, all its dependents are notified automatically. **Use
when**: multiple parts of a system need to react to an event without being
tightly coupled to whatever triggers it (this is the core idea behind
pub/sub and most GUI event systems).

```python
class Subject:
    def __init__(self):
        self._observers = []
    def subscribe(self, observer):
        self._observers.append(observer)
    def notify(self, event):
        for obs in self._observers:
            obs(event)

def email_observer(event):
    print(f"sending email: {event}")
def log_observer(event):
    print(f"logging: {event}")

subject = Subject()
subject.subscribe(email_observer)
subject.subscribe(log_observer)
subject.notify("order placed")   # both observers react, Subject knows nothing about what they do
```

## Command

**Intent**: encapsulate a request (an action + its receiver + its
arguments) as an object, so it can be queued, logged, undone, or passed
around like any other value. **Use when**: you need undo/redo, a queue of
deferred actions, or to decouple "who triggers an action" from "how the
action is performed."

```python
class Light:
    def on(self): print("light on")
    def off(self): print("light off")

class OnCommand:                     # wraps "turn this light on" as an object
    def __init__(self, light):
        self.light = light
    def execute(self): self.light.on()
    def undo(self): self.light.off()

class RemoteControl:                 # never touches Light directly - only knows the Command interface
    def __init__(self):
        self.history = []
    def press(self, command):
        command.execute()
        self.history.append(command)
    def undo_last(self):
        if self.history:
            self.history.pop().undo()

light = Light()
remote = RemoteControl()
remote.press(OnCommand(light))
remote.undo_last()   # undo works generically, for ANY command that implements .undo()
```

## State

**Intent**: let an object alter its behavior when its internal state
changes, appearing to change class. **Use when**: an object's behavior
depends heavily on a mode/status, and an `if self.state == ...` ladder
spread across every method is becoming unmanageable.

```python
class DraftState:
    def publish(self, doc):
        print("moving to review")
        doc.state = ReviewState()     # transitions are handled by the state objects themselves

class ReviewState:
    def publish(self, doc):
        print("publishing!")
        doc.state = PublishedState()

class PublishedState:
    def publish(self, doc):
        print("already published")

class Document:
    def __init__(self):
        self.state = DraftState()     # Document delegates - it has no idea what "publish" actually does
    def publish(self):
        self.state.publish(self)

doc = Document()
doc.publish()   # draft -> review
doc.publish()   # review -> published
doc.publish()   # published -> no-op, same call every time
```

## Template Method

**Intent**: define the skeleton of an algorithm in a base class, deferring
specific steps to subclasses without letting them change the algorithm's
overall structure. **Use when**: several variants of a process share the
same overall steps but differ in one or two of them.

```python
from abc import ABC, abstractmethod

class DataProcessor(ABC):
    def process(self):            # THE template method - fixed skeleton, don't override this
        data = self.load()
        result = self.transform(data)
        self.save(result)

    def load(self):                # a step with a sensible default - override only if needed
        return [1, 2, 3]

    @abstractmethod
    def transform(self, data): ...  # the one step every subclass MUST provide

    def save(self, result):
        print(f"saved: {result}")

class DoubleProcessor(DataProcessor):
    def transform(self, data):
        return [x * 2 for x in data]

DoubleProcessor().process()   # runs load -> transform -> save, in that fixed order
```
