---
name: catalog
---

# Catalog

Registry of the classification domain.

```json
{
  "domain": "Animal classification",
  "metaclasses": [
    { "stereotype": "Animal",       "skill": "animal.md", "role": "domain gate / family root" },
    { "stereotype": "Cat",          "skill": "cat.md" },
    { "stereotype": "Dog",          "skill": "dog.md" },
    { "stereotype": "Wolf",         "skill": "wolf.md" },
    { "stereotype": "Out of scope", "skill": "out-of-scope.md" },
    { "stereotype": "Unresolved",   "skill": "unresolved.md" }
  ],
  "relationships": [
    { "name": "species family", "pattern": "Strategy",
      "stereotypes": { "family": "Animal", "members": ["Cat", "Dog", "Wolf"] } }
  ],
  "execution": "facade.md"
}
```

The species family is **closed**: adding a member (a new species) means editing this catalog and writing its skill — no change to the gate, the other species, the Classifier, or the Facade.
