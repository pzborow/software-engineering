# Design Patterns in Python

The most well-known Gang-of-Four design patterns, grouped by the three
classic categories, each with a working Python implementation. One
file per category, converted from Jupyter notebooks; each code block is
followed by its output.

| Notebook | Patterns |
|---|---|
| [01_creational.md](01_creational.md) | Singleton, Factory Method, Abstract Factory, Builder, Prototype |
| [02_structural.md](02_structural.md) | Adapter, Decorator, Facade, Composite, Proxy |
| [03_behavioral.md](03_behavioral.md) | Strategy, Observer, Command, State, Template Method |

## The three categories, in one sentence each

- **Creational** — how objects get *created* (decoupling instantiation
  from usage).
- **Structural** — how objects and classes are *composed* into larger
  structures.
- **Behavioral** — how objects *communicate* and share responsibility.

## A running theme: not every GoF pattern is equally relevant in Python

Several classic patterns exist specifically to work around limitations of
statically-typed, class-heavy languages (Java, C++) — verbose interfaces,
no first-class functions, no duck typing. Each notebook calls out, where
relevant, the more idiomatic Python alternative:

- **Singleton** — a module is already a singleton (Python caches imports
  in `sys.modules`); you rarely need the `__new__`-override version.
- **Factory Method** — often just a plain function returning different
  classes; no factory *class* required.
- **Strategy** — a "strategy" is often just a function passed around,
  since Python doesn't need an interface/class to make something callable.
- **Builder** — keyword arguments with defaults or a `@dataclass` cover
  most cases that would need a full Builder in a language without them.

None of this means the pattern is "wrong" in Python — it means recognize
when the ceremony is solving a problem your language has already solved
for you, versus when the pattern's actual intent (decoupling, undo/redo,
uniform tree traversal, ...) still earns its complexity.

## How this relates to the rest of this project

- **This directory** — classic OOP design vocabulary, implemented in
  actual Python rather than pseudocode, with notes on where Python's own
  features already give you the pattern's benefit more directly.
