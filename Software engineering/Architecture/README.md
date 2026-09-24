# Application Architecture Patterns

A level above [../Design patterns/](../Design%20patterns/) (class-level GoF
patterns) and [../Principles/](../Principles/) (rules for designing a
class) — these are patterns for structuring an entire application. Each
tutorial has a glossary, Python examples, a "Co zapamiętać" summary and
interview questions with hidden answers at the end of every chapter.

| Document | Covers |
|---|---|
| [Layered/](Layered/) | Architektura warstwowa na poziomie senior — tutorial po polsku: 9 rozdziałów, glosariusz, 28 pytań; warstwy we frameworkach, N+1, sinkhole, vertical slice, migracja |
| [Hexagonal/](Hexagonal/) | Ports & Adapters — tutorial po polsku: 8 rozdziałów, glosariusz, 40 pytań rekrutacyjnych; porównanie z Clean i Onion w rozdziale 06 |
| [Onion/](Onion/) | Onion Architecture — tutorial po polsku: 7 rozdziałów, glosariusz, 30 pytań rekrutacyjnych; porównanie z Hexagonal, Clean, N-tier i CQRS w rozdziale 06 |
| [Clean/](Clean/) | Clean Architecture — tutorial po polsku: 8 rozdziałów, glosariusz, 42 pytania rekrutacyjne; boundaries i presenter, zasady komponentów (REP…SAP), Humble Object, Screaming Architecture |
| [DDD/](DDD/) | DDD na poziomie senior — tutorial po polsku: 11 rozdziałów, glosariusz, 51 pytań; język, subdomeny, bounded contexts, mapa kontekstów, Event Storming, agregaty, legacy |
| [CQRS/](CQRS/) | CQRS na poziomie senior — tutorial po polsku: 10 rozdziałów, glosariusz, 45 pytań; projekcje, spójność ostateczna, outbox i inbox, event sourcing, sagi |

## Suggested reading order

Read in the order of the table: `Layered/` sets up the coupling problem,
`Hexagonal/` fixes it by inverting the dependency arrow, `Onion/` and
`Clean/` show the same idea with a more detailed inner structure,
`DDD/` gives you the strategy and vocabulary for what goes *inside* that
inverted core, and `CQRS/` is an orthogonal, optional decision about
splitting reads from writes that can be layered on top of any of the
above.

## Deliberately not covered here

**MVC/MVP/MVVM** are UI-presentation patterns (how a screen's view, state,
and input handling relate to each other) — a different axis from the
backend/domain-structuring concern the rest of this directory focuses on.
MVC appears only briefly in `Layered/` chapter 04, as the presentation
layer of web frameworks.

## The common thread

Hexagonal, onion and clean (together with the tactical side of DDD) are
the same move applied at different scope: **depend on an abstraction you
control, not a concrete detail you don't**. That is exactly the move that
`Layered/` is missing, and the same idea as the Dependency Inversion
Principle in [../Principles/01_solid.md](../Principles/01_solid.md),
just scaled from "one class" up to "an entire application." None of them
are free: each trades simplicity for testability and flexibility, so the
tradeoff and pitfalls chapters in each tutorial matter as much as the
pattern itself.
