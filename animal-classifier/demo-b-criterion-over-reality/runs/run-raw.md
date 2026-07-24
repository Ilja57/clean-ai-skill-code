# Run B — raw output (immutable)

Date: 2026-07-22. Verbatim output of the blind agent in `demo-b-criterion-over-reality/` (Strategy + DI; species discovered only from the catalog). Pair with `run-input.md`.

The point: creature 6 (a furry, purple-headed thing) is classified **Cat** because the skill's criterion says so, while creature 1 (a meowing, retractable-clawed "real" cat) is **Unresolved**. The criterion wins over reality; real-world knowledge is forbidden.

---

1. It has fur, meows, and has retractable claws.
   → Unresolved
   — why: passes the Animal gate (has fur); no member's classify holds — Cat needs a purple head (absent), Dog needs both barks and fetches (absent). Undecidable, not a guess.

2. It has fur, barks, and fetches a stick.
   → Dog
   — why: passes the Animal gate (has fur); Dog's classify holds (barks AND fetches). Cat does not. Exactly one member.

3. It has feathers, wings, and a beak.
   → Out of scope
   — why: fails the Animal gate — affirmatively states a non-fur covering (feathers).

4. It has fur and four legs.
   → Unresolved
   — why: passes the Animal gate (has fur); no member's classify holds — no purple head (Cat), no barks/fetches (Dog). Description too thin to place.

5. It has fur, meows, and fetches a stick.
   → Unresolved
   — why: passes the Animal gate (has fur); Dog needs BOTH barks and fetches — only fetches, so it fails; Cat needs a purple head (absent). No member holds.

6. It has fur and a purple head.
   → Cat
   — why: passes the Animal gate (has fur); Cat's classify holds (purple head). Dog does not. Exactly one member.
