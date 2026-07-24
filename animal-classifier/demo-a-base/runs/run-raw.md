# Run A — raw output (immutable)

Date: 2026-07-22. Verbatim output of the blind agent in `demo-a-base/` (Strategy + DI; species discovered only from the catalog). Pair with `run-input.md`.

---

1. It has fur, meows, and has retractable claws.
   → Cat
   — why: gate passes (has fur); Cat's classify holds (meows AND retractable claws).

2. It has fur, barks, and fetches a stick.
   → Dog
   — why: gate passes (has fur); Dog's classify holds (barks AND fetches).

3. It has feathers, wings, and a beak.
   → Out of scope
   — why: gate fails — affirmatively states a non-fur covering (feathers).

4. It has fur and four legs.
   → Unresolved
   — why: gate passes (has fur); no member's classify holds (neither Cat nor Dog criteria stated) — too thin to place.

5. It has fur, meows, and fetches a stick.
   → Unresolved
   — why: gate passes (has fur); Cat fails (meows but no retractable claws), Dog fails (fetches but no barks) — matches parts of two species, none fully.
