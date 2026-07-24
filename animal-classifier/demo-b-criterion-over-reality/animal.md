---
name: animal
---

# Animal

Animal is the **domain gate** and the root of the species family. It is **not** a type parent and carries **no `classify`** — this is a late-binding environment, not a typed one, so the family members are dispatched at run time without the root declaring their method.

## Domain boundary (gate)

A creature belongs to the Animal domain when it **has fur**. A description that affirmatively states a non-fur covering fails the gate.

Animal does not list the species — the family is held by the catalog (registry).
