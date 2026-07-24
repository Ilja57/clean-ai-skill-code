# Clean AI Skill Code (CASC)

Bringing Clean Code, the Object Paradigm, SOLID and GOF back to AI skills.

## What this is

AI skills written as loose prose decay fast — Dirty AI Skill Code (DASC): fast to generate, fast to rot. The model fills the gaps with its own real-world knowledge and the output drifts. Clean AI Skill Code (CASC) brings the old, proven engineering discipline — Clean Code, the Object Paradigm, SOLID, GOF design patterns — to the way AI skills are written, and puts it in service of one goal: **determinism** (for the reasoning behind it, see the [Pattern Metamodel](https://gitlab.com/iljakraval/pattern-metamodel)). The AI judges only by the criteria written in the skills, and nothing else.

This is not tied to one project, one domain, or one toolchain. It is meant for anyone who writes AI skills and wants them to hold to the principles and patterns of Clean Code — to stay flexible, predictable and maintainable as they grow, the very reasons these principles earned their place in ordinary software in the first place.

## The principle catalog

**[`PRINCIPLE_CATALOG.md`](PRINCIPLE_CATALOG.md)** — the load-bearing document. It is organized in three layers:

- **Principles** — the load-bearing ideas (Object Paradigm, SOLID, DRY, …).
- **Rules** — normative rules that live under a principle (identity, encapsulation, clean terms, …).
- **Patterns** — reusable constructions (Facade, Mediator, Strategy, Dependency Injection, …).

The catalog is the single home of the full list; each item carries an **In the demo:** pointer to where it appears in the demo below.

## The demo

**[`animal-classifier/`](animal-classifier/)** — a toddler-simple domain (sort short creature descriptions into species) that demonstrates the catalog on a domain a child understands. Three isolated worlds show a clean base, the criterion winning over reality, and adding a species without touching existing code. Each run is kept as an immutable input/output pair.
