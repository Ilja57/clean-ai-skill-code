# Animal Classifier — a tiny demo of Clean AI Skill Code

A toddler-simple domain — sort short creature descriptions into species — that shows the **Clean AI Skill Code** principles at work. It is the same deterministic distillation method used on real analytical requirements, here on a domain a child understands.

The one rule that makes it deterministic: **the AI judges only by the criteria written in the skills.** Real-world knowledge is forbidden — if a skill says a Cat has a purple head, then a purple-headed thing is a Cat, and a meowing one is not. Every creature ends in exactly one outcome: a species, Out of scope, or Unresolved.

## The three demos

Each demo is a **self-contained world** — a full copy, so one example never couples to another (a change in demo B can never reach demo A; this is the *Isolation* pattern, explained in the catalog). Together they show the same clean classifier from three angles: the clean base, the criterion overriding reality, and extension without touching existing code.

### `demo-a-base` — the clean base
The classifier with two species (Cat, Dog). The reference implementation; audited clean for SRP and determinism.

### `demo-b-criterion-over-reality` — the criterion wins over reality
Identical to the base except **Cat's `classify` says a Cat has a purple head**. Result: a furry, purple-headed thing is classified **Cat**, while a meowing, clawed "real" cat is **Unresolved**. The skill's criterion is the source of truth — not the model's world knowledge.

### `demo-c-add-species-OCP` — add a species, touch nothing else
Adds a third species, **Wolf**, to the base. The diff against the base is **two files** — the new `wolf.md` and one line in `catalog.md`; every existing skill is untouched, and the unchanged Classifier picks up Wolf automatically. Open for extension, closed for modification.

## How to run a demo

Point a fresh agent at one demo folder and have it read **only** that folder — blind, no outside files, no real-world knowledge:
- entry: `facade.md`; registry: `catalog.md`; creatures: `input.md`.

Each demo keeps its run under `runs/` as an **immutable pair**: `run-input.md` (the exact prompt) + `run-raw.md` (the verbatim output).

## The principles behind it

The principles, rules and patterns these demos put to work — and exactly where each one shows up — live in the catalog: [`../PRINCIPLE_CATALOG.md`](../PRINCIPLE_CATALOG.md). Every catalog item carries an **In the demo:** pointer back to the files here.
