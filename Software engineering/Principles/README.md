# Design Principles and Acronyms

The most well-known software design principles — the acronyms you hear in
code reviews and interviews — each shown as a violation next to its fix,
with working Python. Converted from Jupyter notebooks; each code block is
followed by its output.

| Notebook | Covers |
|---|---|
| [00_oop_pillars.md](00_oop_pillars.md) | Encapsulation, Abstraction, Inheritance, Polymorphism — the foundation SOLID builds on |
| [01_solid.md](01_solid.md) | **S**ingle Responsibility, **O**pen/Closed, **L**iskov Substitution, **I**nterface Segregation, **D**ependency Inversion |
| [02_other_principles.md](02_other_principles.md) | DRY, KISS, YAGNI, Law of Demeter, Composition over Inheritance |

## How this relates to the rest of this project

- [../Design patterns/](../Design%20patterns/) — patterns are reusable
  *solutions* to recurring design problems.
- **This directory** — principles are the *reasoning* for why one design
  is better than another; a pattern is often just a principle applied
  concretely (e.g. Strategy is Open/Closed applied to swappable
  algorithms, Dependency Inversion is what makes a Proxy or Adapter
  pluggable in the first place).

## A word of caution

Every principle here can be over-applied. Splitting a class into five
single-purpose pieces that are never reused or tested independently isn't
SRP, it's indirection for its own sake; injecting an abstraction for a
dependency that will only ever have one implementation isn't DIP, it's
YAGNI violated in the name of a different acronym. Use these as a
checklist for *why something feels wrong*, not as a mandate to apply all
five SOLID letters to every class you write.
