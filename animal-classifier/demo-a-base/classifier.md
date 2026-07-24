---
name: classifier
requires: [animal, catalog, out-of-scope, unresolved]
---

# Classifier — the Strategy context

Classifies a single creature description by applying a **family of Strategies** (one per species) drawn from the catalog. It never hardcodes the species; each species carries its own `classify`, resolved at run time (late binding).

## Rule of judgement (determinism)

Judge ONLY by the criteria in the skills. Real-world knowledge is **forbidden**: if a criterion diverges from reality, the criterion wins. Never invent, never "know better".

## Routing (one description)

1. Domain gate: if the description fails the Animal domain boundary (see `animal.md`) → **Out of scope**.
2. Otherwise ask the catalog for the species family and apply each member's `classify`:
   - exactly one member's `classify` holds → that species,
   - none, or more than one, and the description does not decide it → **Unresolved** (record the reason; do not guess).
3. Record the outcome. Exactly one outcome per description; nothing is dropped silently.

Adding a species = register it in the catalog and give it a `classify`; the context picks it up automatically. No context edit.
