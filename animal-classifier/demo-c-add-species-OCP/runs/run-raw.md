# Run C — raw output (immutable)

Date: 2026-07-22. Verbatim output of the blind agent in `demo-c-add-species-OCP/` (Strategy + DI; species discovered only from the catalog). Pair with `run-input.md`.

The point: a new species (Wolf) was added by writing `wolf.md` and registering it in `catalog.md` — nothing else changed. The classifier names no species, yet the agent found all three (Cat, Dog, Wolf) through the catalog and classified creature 6 as Wolf.

---

1. It has fur, meows, and has retractable claws.
   → Cat
   — why: gate passed (has fur); Cat's classify held (meows + retractable claws); Dog and Wolf did not hold — exactly one member.

2. It has fur, barks, and fetches a stick.
   → Dog
   — why: gate passed (has fur); Dog's classify held (barks + fetches); Cat and Wolf did not hold — exactly one member.

3. It has feathers, wings, and a beak.
   → Out of scope
   — why: gate failed — description affirmatively states a non-fur covering (feathers), contradicting the Animal gate criterion.

4. It has fur and four legs.
   → Unresolved
   — why: gate passed (has fur); no member's classify held (no meow/retractable claws, no bark/fetch, no wild+pack+hunt); description too thin to place.

5. It has fur, meows, and fetches a stick.
   → Unresolved
   — why: gate passed (has fur); Cat requires meows AND retractable claws (retractable claws absent); Dog requires barks AND fetches (barks absent); Wolf absent — no member holds, does not decide.

6. It has fur, lives in the forest, moves in a pack, and hunts.
   → Wolf
   — why: gate passed (has fur); Wolf's classify held (wild/forest + pack + hunts); Cat and Dog did not hold — exactly one member.
