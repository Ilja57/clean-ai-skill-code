---
name: facade
requires: [catalog, classifier]
---

# Facade — classification service

The outward door: the single service an external request (the prompt) calls. It **only exposes and dispatches** — it decides nothing itself (hotel receptionist).

## Service

`classify(input) using a catalog` → for every creature in the input, one outcome.

## What it does

1. Load the catalog.
2. Hand each creature in the input to the Classifier.
3. Assemble the outcomes and return them.
