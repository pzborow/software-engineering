# Design Patterns — Structural

Structural patterns are about **how objects and classes are composed**
into larger structures, while keeping those structures flexible and
efficient.

## Adapter

**Intent**: convert the interface of a class into another interface
clients expect, letting incompatible interfaces work together. **Use
when**: you need to use an existing class but its interface doesn't match
what your code (or a third-party API) requires.

```python
class EuropeanPlug:
    def voltage(self):
        return 230

class USDevice:
    def __init__(self, plug):
        self.plug = plug
    def power_on(self):
        return f"Powering on with {self.plug.us_voltage()}V"  # expects .us_voltage(), not .voltage()

class EuropeanToUSAdapter:                 # translates one interface into the other
    def __init__(self, european_plug):
        self.european_plug = european_plug
    def us_voltage(self):
        return round(self.european_plug.voltage() * 0.52, 1)

device = USDevice(EuropeanToUSAdapter(EuropeanPlug()))
print(device.power_on())
```

## Decorator (structural pattern — not Python's `@decorator` syntax)

**Intent**: attach additional responsibilities to an object dynamically,
by wrapping it, as a flexible alternative to subclassing. **Use when** you
need to add behavior to individual objects at runtime, and combinations of
behaviors would explode into a subclass per combination.

This is a different thing from Python's `@decorator` syntax (see
the Python gotchas on decorators) even though they share a name and a similar
"wrap something to add behavior" idea — Python's `@` syntax decorates
*functions*, this GoF pattern wraps *objects*, one instance at a time,
chosen at runtime.

```python
class Coffee:
    def cost(self): return 5
    def description(self): return "Coffee"

class MilkDecorator:                 # wraps a Coffee-like object, adds to it, same interface
    def __init__(self, coffee):
        self.coffee = coffee
    def cost(self): return self.coffee.cost() + 1
    def description(self): return self.coffee.description() + " + Milk"

class SugarDecorator:
    def __init__(self, coffee):
        self.coffee = coffee
    def cost(self): return self.coffee.cost() + 0.5
    def description(self): return self.coffee.description() + " + Sugar"

order = SugarDecorator(MilkDecorator(Coffee()))   # stack decorators in any combination at runtime
print(order.description(), order.cost())
```

## Facade

**Intent**: provide a single, simplified interface to a complex subsystem
of classes. **Use when**: client code shouldn't need to know the internal
structure/ordering of a multi-step subsystem to use it correctly.

```python
class CPU:
    def freeze(self): print("CPU: freeze")
    def jump(self, pos): print(f"CPU: jump to {pos}")
    def execute(self): print("CPU: execute")

class Memory:
    def load(self, pos, data): print(f"Memory: load {data} at {pos}")

class HardDrive:
    def read(self, sector, size): return f"boot data({sector},{size})"

class ComputerFacade:            # hides the correct boot sequence behind one method
    def __init__(self):
        self.cpu = CPU()
        self.memory = Memory()
        self.hd = HardDrive()
    def start(self):
        self.cpu.freeze()
        self.memory.load(0, self.hd.read(0, 1024))
        self.cpu.jump(0)
        self.cpu.execute()

ComputerFacade().start()   # caller doesn't need to know CPU/Memory/HardDrive exist at all
```

## Composite

**Intent**: compose objects into tree structures and let clients treat
individual objects and compositions of objects **uniformly**. **Use
when**: you have a part-whole hierarchy (files/folders, UI widgets, org
charts) and want the same code to work on a single item or a whole subtree.

```python
class File:
    def __init__(self, name, size):
        self.name, self.size = name, size
    def total_size(self):
        return self.size
    def display(self, indent=0):
        print(" " * indent + f"- {self.name} ({self.size}kb)")

class Folder:
    def __init__(self, name):
        self.name = name
        self.children = []
    def add(self, child):
        self.children.append(child)
        return self
    def total_size(self):                          # same method name as File.total_size
        return sum(c.total_size() for c in self.children)  # works whether children are Files or Folders
    def display(self, indent=0):
        print(" " * indent + f"+ {self.name}/")
        for c in self.children:
            c.display(indent + 2)

root = Folder("root").add(File("a.txt", 10)).add(
    Folder("sub").add(File("b.txt", 20)).add(File("c.txt", 5))
)
root.display()
print("total size:", root.total_size())
```

## Proxy

**Intent**: provide a stand-in for another object to control access to it
(lazy loading, access control, logging, caching). **Use when**: creating
or accessing the real object is expensive or needs to be gated.

```python
class RealImage:
    def __init__(self, filename):
        self.filename = filename
        print(f"loading {filename} from disk (expensive)")
    def display(self):
        print(f"displaying {self.filename}")

class LazyImageProxy:                     # same .display() interface as RealImage
    def __init__(self, filename):
        self.filename = filename
        self._real_image = None
    def display(self):
        if self._real_image is None:
            self._real_image = RealImage(self.filename)  # only loaded on first actual use
        self._real_image.display()

img = LazyImageProxy("photo.png")
print("proxy created, nothing loaded yet")
img.display()   # loads here
img.display()   # no reload the second time - reuses the cached real object
```
