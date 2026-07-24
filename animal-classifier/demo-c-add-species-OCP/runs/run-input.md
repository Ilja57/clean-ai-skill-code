# Run C — input (immutable)

Date: 2026-07-22. Blind run in the isolated world `demo-c-add-species-OCP/` (Strategy + DI). A fresh agent read only this folder, no real-world knowledge, and discovered the species **only from the catalog**. Pair with `run-raw.md`.

Demo C = "add a species (Open-Closed)". Copy of demo-a-base with a new species **Wolf** added. Diff vs demo-a-base (excluding runs): only `catalog.md` (Wolf registered) and `input.md` (test data) changed, and `wolf.md` is new — every existing skill is untouched.

DI-clean: `classifier.md` requires only `[animal, catalog, out-of-scope, unresolved]` — it names no species. This run proves it: the agent discovered all three species (Cat, Dog, Wolf) purely from the catalog, though the classifier lists none of them.

## Prompt given to the agent

You are the runtime for a small classification demo. Work ONLY from the skill files in this folder — read nothing else, and do NOT use real-world knowledge about animals.

Folder: D:\AAA-DEV\not_dev\casc\animal-classifier\demo-c-add-species-OCP\

Steps:
1. Read `catalog.md` — the registry. It lists the domain gate, the species family members and their skill files, the outcome skills, and the execution entry. Take the set of species ONLY from the catalog — do not assume which species exist.
2. Read `facade.md`, `classifier.md`, the gate `animal.md`, and the outcome skills (`out-of-scope.md`, `unresolved.md`).
3. Read EACH species skill the catalog registers as a family member.
4. Read `input.md` — the creatures to classify.
5. Classify EACH creature by applying the Classifier: first the Animal domain gate, then apply each registered family member's `classify`. Judge ONLY by the criteria in the skills. Real-world knowledge is forbidden. When undecidable, use Unresolved — do not guess.

Output: `<n>. <verbatim>` / `→ <Outcome>` / `— why: …`. Outcomes: a species registered in the catalog, Out of scope, or Unresolved.
