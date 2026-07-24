---
name: unresolved
---

# Unresolved

A creature the classifier cannot decide with the given criteria — e.g., it fits the Animal boundary but matches no species, matches more than one species partially, or the description is too thin to place.

This is the **TO RESOLVE** outcome: the classifier does not guess — it records the question and hands it to a human. Not a weaker answer; it is what keeps the other outcomes trustworthy.

Carries: `description` (the input line) and `reason` (why undecidable).
