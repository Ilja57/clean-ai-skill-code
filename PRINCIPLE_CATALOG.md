# Principles, Rules and Patterns for Writing Clean AI Skill Code

> For each item, the **In the demo:** line shows where you find it in the `animal-classifier` example and how it is demonstrated there.

## Principle: Object Paradigm (the BASE principle for defining any element)

The Object Paradigm describes the inherent relativity of the view on every arbitrary element of any system of any type anywhere: either we describe what the element offers to its clients = the external view of its services, or how that offering is realized inside = the internal view of the implementation. Talking about an element without the context of the external and internal view makes no sense and leads to logical errors. The context is often clear from circumstances, but omitting it is generally a source of logical errors.

**In the demo:** every skill has an external view = **Skill Entry** (the file name, e.g. `cat.md`) and an internal one = **Skill Text** (the body). Holds across all demos.

### Rule: Element Identity

Elements have, in the external view, their unambiguous identity: an algorithm is established for the primitive (yet verbally violable) assertion "this is this element and that is a different element". The sentences "these two elements are actually one element" and "this element is actually two elements" are contradictions and are forbidden.

**In the demo:** `cat.md` is one identity "Cat"; in `demo-b-criterion-over-reality` it has a different implementation (a purple head), but still **one identity** Cat — two versions of the criterion, one concept.

### Rule: Element Encapsulation

The client sees an element's services, not its implementation — this is a generalization of encapsulation from OOP. The client knows and uses the services in a given context, but the implementation ("how") is hidden. Without this consequence, SRP, DRY (and the other SOLID, GOF principles) could not be introduced without losing the logic that says: an internal refactoring of an element with better SRP or DRY etc. does not change the external view.
This rule also holds for Generalization, where the ancestor is used by the descendant through the external view (services) without knowing the ancestor's implementation.

**In the demo:** the `classifier` sees only a species' service `classify`, not how it does it inside. Generalization: `cat`/`dog` use the ancestor (the `animal` gate) only through the external view — they **do not restate** its criterion "has fur" (this was the subject of the fix in `out-of-scope.md` — it is an internal matter of the ancestor's implementation). In OOP this means the rule for the ancestor's implementation is not only "not public" but "not even protected" (violating the rule = a change in the ancestor leads to an often needless rework of all descendants).

### Rule: Client Anonymity

Client anonymity is in the definition of **both the service and the implementation**. External view: a service is by its definition an offer for **anyone** — and "anyone" is a synonym for an **anonymous party**. Internal view: the implementation **realizes that service for an anonymous party** — it does not know or take on a concrete client. If it knew the client, it would be an offer **for that client**, i.e. not for anyone, and that is no longer a service.

**In the demo:** `cat.md` offers `classify` to anyone; it does not know that `classifier` calls it. The surroundings (clients) can be refactored without touching it; the element knows nothing about the arrangement of clients or about who calls it.

### Consequences for AI Skills

An AI Skill also has an external and an internal view, and it is recommended to name them as follows:

- **External view of the AI Skill's services: "Skill Entry"** — identifies the Skill element and lets it be used (invoked).
- **Internal view: "Skill Text"** — the internal text of what is to be done.

### Implementation in the AI Skill environment

This logical OP construction can be introduced in several ways, for example: a Skill Entry is defined by a file + an H2 heading, and the Skill Text is the text after the heading up to the next H2 or the end of the file. This, however, did not prove itself for me, because there is a cleaner way to honor SRP.

### Recommendation

It is better to treat the Skill Entry (the external view of an AI Skill) as the file name (of type md) and the Skill Text (the internal view) as the internal text of that file.

Note: This labeling looks like a formality, but the logic of many Clean AI Skill Code principles is built on this external and internal view of an AI Skill.

**In the demo:** Skill Entry = the file name (`cat.md`, `classifier.md`), Skill Text = the file body — exactly per the Recommendation.

## Principle: "Use Clean Terms" (UCT)

The terms used must be so-called clean and non-colliding. It holds everywhere — for analysis (ANA), for Design, and for programming when naming elements — as well as in the AI Skill environment. The principle is also fundamental: without it there is no point working with the other principles and patterns at all, because the essential logic in the identity of elements is broken.

**In the demo:** the terms are clean and non-colliding (Cat, Dog, Wolf, Out of scope, Unresolved). *Note — to be honest:* the **anti-examples** (a synonym / a homonym / a lying name) are **not yet planted**; UCT is honored in the demo but not demonstrated. Planned as a separate demo twist.

### Rule: do not use synonyms

Synonyms established in human speech lead, in system design, to collisions with identity — see the already mentioned contradictions in OP. The question "are Customer and Client the same thing in the system (= a synonym in human speech)" is a "contradictory" question about two elements or one. Therefore the use of "synonyms" is strictly forbidden (they are taken over from human speech, mostly through poor discipline or through team document production etc.). It can happen that two elements look like "synonyms" but are not.

**In the demo:** honored (one concept = one name); the anti-example (e.g. an input "hound" = Dog) is not shown in the demo — the logic of the rule is, I think, clear.

### Rule: do not use homonyms

Homonyms are words that can have several meanings and are also forbidden, because they are not unambiguous. For example the term Package. One must define the full and longer context of the term that rules out the homonym (Package in UML, in Java, etc.).

**In the demo:** honored; an anti-example (e.g. "Boxer") is likewise not shown.

### Rule: do not use lying names

It is forbidden to use a term with a different meaning, i.e. to swap names etc. (alias the rule "a Cat is a Cat and a Dog is a Dog"). This error occurs mainly in the programming realization, with the addendum "sure, we call that table Cat, but it's actually a Dog, though we all know it's a Cat even if it's named Dog, so there's no problem". It is a problem, and a big one. A few such swaps in the system are enough, in combinatorics, and no one can make sense of it. It usually arises after some breaking change that requires renaming elements on a wider scale.

The rule for the AI Skill environment during renaming and refactoring (= a change of the mental model): no workarounds regarding names, remove lying names as soon as possible, even if there are many. The AI itself will help with this cleanup.

**In the demo:** honored — `cat.md` is about a cat, `wolf.md` about a wolf (name = meaning). *Note:* the purple head in `demo-b` is **not** a lying name (the name Cat still means the concept Cat, only the criterion changes). The anti-example (a `cat.md` file describing a dog inside) is not yet planted.

## Principle: "Don't Repeat Yourself" (DRY)

Don't repeat yourself: the same thing is defined once in the system and used (re-used) from the other places. The principle rests on extracting an element and using it from various places — there are no copies and one refers to a single source.

It is closely related to OP (external × internal view): deploying re-use inside an element is a change of implementation, and therefore **does not change the external view** — the client does not see the implementation. Extracting a common part and re-wiring it to re-use can be done without impact on the view of the element's services.

The mentioned extraction process is also closely related to element identity: the examined parts, before extraction, have no identity, even though one logically talks about them "as if they were there". The elements are not there; they are just some "parts of the implementation" (e.g. of the Skill Text, etc.). An element gains identity only after "extraction" — it is then identified and starts offering services.

There is **clean and dirty re-use**. Dirty re-use drags into the element, along with the extracted part, also ballast (things that do not belong there), and thereby breaks SRP. Therefore DRY is not enough on its own — re-use must be led so that the extracted element holds a single responsibility "without ballast". DRY and SRP go together.

An essential rule for AI Skills: one concept or rule is defined in one skill, and the other skills call it or refer to it — they do not copy it. The skill environment is much more transparent and changes are targeted over identified elements — not scattered God-knows-where in whose implementation. For the functioning of AI as a machine this is essential.

**In the demo (within one world):** the gate criterion "has fur" lives **only** in `animal.md`; both `classifier` and `out-of-scope` **refer** to it, they do not copy it. The rule "judge only by criteria" has a single home (`classifier`). *(Across demos, on the contrary, Isolation applies — see below.)*

## Pattern: Isolation

Deliberately against DRY: here, for example, the three demos are full copies, not sharing from a single source. The reason: they are independent worlds that are allowed to (indeed are meant to) diverge — demo-b is meant to have a different cat (a purple head); sharing would break that divergence, or a change made for B would break A. Coupling between the examples is undesirable. DRY holds within one world, Isolation across worlds — a different context, a different rule, it is not a contradiction.

In general the Isolation pattern can be deployed for other reasons too (e.g. bounded context in DDD, API versioning, fault isolation / bulkhead, multitenancy, separation of the domain and persistence models, test isolation, dependency vendoring).

SSOT is not abolished in doing so, it just moves up a level. Above the copies stands an oversight layer — in this demo the AI — which keeps a record of what is deliberately a copy between worlds and where divergence is desired, and checks it during changes. A single authoritative representation thus belongs to the knowledge about the relationships between the copies, not to the code itself.

**In the demo:** the folders `demo-a-base`, `demo-b-criterion-over-reality`, `demo-c-add-species-OCP` — each complete, without cross-references.

## Principle: "Single Responsibility" (SRP)

Every element has **one responsibility**; if it covers more, it is extracted. Don't make CatDogs — poke the Cat and the Dog falls over. There can even be an identity violation: the identity is CatDog, which from the OP standpoint = neither Cat nor Dog, even though one talks about them. A violation of SRP = a logical element scattered into the implementation across more places than where it belongs. A mishmash arises: the element then has to be looked up all over the place instead of in a single SSOT. It is an inconsistency of the external and internal view. For a system working with AI Skills (in the logic and in upholding semantic determinism) this is essential.
When SRP is honored, the logical rule of consistency of the external and internal view holds. A signal of good SRP is the common-sense sentence "if I change only X, then I change only X", which (paradoxically) need not hold when SRP is violated.

Recommendation: To track whether SRP is met or not, one must think through precisely the consequences of the relativity of the view on an element in the Object Paradigm: an element in the system is identified — and thus findable — only through the external view AND IN NO OTHER WAY. We must be consistent in this view of OP, even if in a given situation it may contradict common sense — that is precisely what happens when SRP is violated. When a CatDog is introduced, then in the system there de facto exists neither Cat nor Dog, even though one talks about them. In general, if SRP is violated, the software may contradict common sense. Consistently understood OP as a relative view (external and internal) on an element leads to a result different from what common sense dictates.

**In the demo:** `cat.md` holds only Cat's criteria; `classifier` only the routing; `catalog` only the registry; `animal` only the gate; `facade` only the door. Audited (SRP audit) **clean**.

## Pattern: "Open-Closed" (OCP)

The system is **extended by adding** a new element, not by rewriting existing ones: *open* for extension (add a new one), *closed* for modification of what already works (don't touch what's done). The fact that a new element must still be **consciously registered** is held by the separate Pattern *Enumeration in the catalog* — we don't mix that in here.

**Flexibility.** A new capability enters at **one place** — a new element — with **no intervention** into what already runs. You extend the system without reopening it.

**Transparency (against DASC).** Because the change is localized, it is also **auditable**: the diff is one deliberate point, not a spray of edits scattered across the system. This is the opposite of Dirty AI Skill Code, where a single addition drags illogical, needless edits into many places and no reviewer can tell what actually changed or why.

**Robustness.** The rule of thumb: *the more you cut into working code, the more bugs; the less you touch it, the fewer.* OCP keeps the working core **untouched**, so a new feature cannot break what already passed — the risk of the change is confined to the new element alone.

**"Just add" — the common-sense shape of change.** Under OCP a change **doesn't hurt**: it drops into the *"just add one more"* mechanism instead of forcing you to update several points across the system. This is exactly how a layman naturally describes what they want — *"I only want to add this one thing"* — not *"go update it in five places."* The working body of code only ever **grows**; it is never wounded — call this its **additive growth (non-invasive change)**.

**In the demo:** `demo-c-add-species-OCP` — adding a Wolf = a new `wolf.md` + **one line** in `catalog.md`; the diff against the blueprint = **2 files**, existing skills untouched, the `classifier` unchanged — it "does not know" about the added Wolf, yet processes it polymorphically.

## Pattern: Facade (hides the system from requests, like a hotel receptionist)

An external interface that **hides the complexity** of the system and can be called from outside; it merely exposes and forwards, it decides nothing itself.

**In the demo:** `facade.md` — the single door that the prompt calls; delegates to `classifier`, decides nothing itself.

## Pattern: Mediator (Director, Orchestrator — like an airport control tower)

A central intermediary and **controlling algorithm**: elements do **not communicate directly**, everything goes through it, and it keeps them unaware of one another (against a web of relationships), and its overall algorithm is maintained more efficiently and more clearly. Other patterns may be used inside it (e.g. Strategy etc.).

**In the demo:** the `classifier` is that controlling algorithm — the species do not know each other, and it holds the arbitration "exactly one / more → Unresolved" and the ordering (gate first, then the family). For the actual classification of a single species it **calls Strategy** (the `classify` of the family members). Together this is the whole combination of this demo: **Facade → Mediator → Strategy** (+ the DI pattern, so that neither the Mediator nor the Strategy knows the concrete species and they stay at the ancestor level).

## Pattern: Strategy

The algorithm (behavior) is chosen **polymorphically**: each family member carries its own implementation of the same operation, and the superior code calls it **without knowing which one** — no `switch`/`if` by type, but an object decision. Because Strategy **does not know what it works with** (it receives the family from outside), it goes hand in hand with **DI** (who supplies it, and at the ancestor level) and **OCP** (a new member = add a new Strategy, rewrite nothing).

**In the demo:** each species (`cat.md`, `dog.md`, `wolf.md`) carries its own `classify` = one ConcreteStrategy; the `classifier` applies them uniformly, without knowing the concrete species (through late binding, and the family from `catalog`). Adding a species = a new Strategy, the `classifier` untouched — see `demo-c-add-species-OCP`, where **Wolf** joined Cat and Dog: its `wolf.md` strategy was added and registered in the `catalog`, with no changes anywhere else in the skills, and the Strategy algorithm processed it correctly.

## Pattern: Determinism (don't make things up → "TO RESOLVE")

Decide **only by the given criteria**; the real world is forbidden. What cannot be decided goes as **"TO RESOLVE"** to a human — not a guess. This is not a weaker answer; it upholds the credibility of the others. The structures are moreover presented in **JSON form for machine reading** — parse, don't infer.
This is semantic determinism. Its reliability depends on the domain precision of the definitions in the skills and also on the nature of the domain's concepts. If "foggy" or "hard-to-determine" concepts are chosen — ones that are so by their very nature (= "two analysts would argue over it and de facto both be right") — then the quality of determinism drops. For example, in the PMM AAF project (for those interested, see the [AAF pages](https://aaf-kraval-d9055e.gitlab.io/), in Czech), the concepts "Technological boundary condition" (= a very vague concept) versus "Technological requirement" (a strictly delimited definition based on several supporting skills such as "Analytical modeling versus Design" and others). In the demo these criteria are heavily simplified for the sake of illustration.

**Auditability and the human boundary (control).** Because every decision is made *only by the stated criteria* and emitted as **structured data**, it can be **checked** — not trusted on faith. This is the control surface: an auditor (a human, or another program) can verify *whether the rule was followed*, decision by decision, instead of judging fuzzy prose after the fact. Two mechanisms turn this into a boundary rather than a hope: **"TO RESOLVE"** hands anything undecidable to a human — the AI is forbidden to cross that line by guessing — and **"parse, don't infer"** keeps the machine reading facts, not inventing them. CASC does **not**, and does not claim to, contain a capable agent that actively games its environment (that is sandboxing and permissions — a different field); what it does is make the AI's decisions **legible and reviewable**, which shrinks the room for deviation to pass unnoticed.

**In the demo:** the rule in `classifier` ("judge only by criteria, real-world forbidden"); `unresolved` = TO RESOLVE. The sharpest proof is **`demo-b-criterion-over-reality`**: a purple-headed creature → Cat, a realistic meowing cat → Unresolved (the criterion won over reality). The registry `catalog.md` is structured **JSON** (it is parsed, not inferred); the species' criteria are prose (an accepted simplification of the demo as an illustration; in a real program all structures are written in JSON and a strict check for so-called "determinism holes" watches that nowhere does mere prose remain).

## Pattern: Enumeration of descendants in the catalog (the enumeration is given by the system, not by the supertype)

The enumeration (the family) is provided **solely by the system = the catalog**, globally to all; neither the supertype nor anyone else holds it hardcoded. It is closely related to DI (the system **injects** the family). It relates to NCD — if descendants were enumerated in the supertype, everything would be intertwined, ancestor and descendants "in one bag", and changes would then be intertwined.

**In the demo:** the family of species lives only in `catalog.md` (`members`); the `classifier` **requests** it from there and **names no species** (`requires: [animal, catalog, out-of-scope, unresolved]`). Verified by a DI run (the agent discovered the species only from the catalog, including the Wolf). OK. *(Previously the `classifier` named `cat, dog` in `requires` = a collision with this pattern; fixed.)*

## Pattern: "Liskov Substitution" (LSP)

A family member is **substitutable into a given position** where "a family member" (a descendant of the given ancestor) is expected, without breaking the algorithm.

**In the demo:** the `classifier` is a verbal program — an OOP loop *"request the family of Animal descendants from `catalog` and for each member call `classify` (in skills untyped = late binding)"*. That loop works for **every** member the same way **precisely because they are substitutable into the position in the algorithm** (LSP). `demo-c` proves it live: the newly added **Wolf** (only in the catalog) was **substituted into the same loop without touching the other skills**. *(The demo does not show an adversarial test — an element that would violate the LSP substitution rule.)*

## Pattern: "Dependency Injection" (DI)

The high level depends on an **abstraction**, not on concretes; the concretes are **injected** (DI). Avoid the error of "misplaced concretization"; concretization does not belong at the level of "working only with the ancestor". The code then stays clean at the ancestor level, i.e. universal for every descendant thanks to LSP (which is injected).

**In the demo:** the `classifier` (the high level) depends only on the **catalog** (the registry/abstraction) + the gate + the outcomes — it **names no** concrete species; those **are injected via the catalog**. Finished by the `requires` fix (previously it named `cat, dog` = a binding to concretes, the error of misplaced concretization, against DI).

## Principle: No Circular Dependency

A circular dependency is forbidden — it relates to OP and SRP, it is needless coupling. Sometimes it follows from the nature of things, but don't create it needlessly.

**In the demo — examples that would be an error (and the demo does not do them):**
- if the supertype `animal` **enumerated** `cat, dog` → a cycle supertype ↔ descendants (which is why the catalog holds the enumeration),
- if `cat` **knew** `dog` (siblings) → a web, NCD violated,
- if the `classifier` **named** the species in `requires` → a binding context ↔ concretes (this **was** a defect, fixed — see DI / Enumeration in the catalog).

The demo is clean of these cycles.
An example of a necessary Circular Dependency (from practice, not from the demo): an Invoice has its N InvoiceLines — (a Composition to N, with a back-reference too). The relationship is bidirectional in Dependency: the Invoice controls its lines (OneToMany) and a line sees its Invoice (ManyToOne).

## Principle: "Interface Segregation" (ISP)

A client should not be forced to depend on an interface it does not use; rather many small interfaces than one fat one. An analogue of SRP for interfaces (alias for a set of external views of elements).

**In the demo:** **we don't have it, not needed** — the Strategy interface is the single method `classify`, there is nothing to segregate. It would show up only with **Breed** (`classify` + `classify_breed` as **separate** interfaces; a Cat would not carry breed). Not used in the demo.

---

## Trainings & webinars

These principles, taught live — for individuals who write AI skills and for teams that want them done right.

- **In the Czech or Slovak region?** → [Clean AI Skill Code — školení a webináře](https://www.objects.cz/clean-ai-skill-code-casc/) (in Czech)
- **Everywhere else?** → [Clean AI Skill Code — Workshop (English)](https://www.objects.cz/clean-ai-skill-code-casc-en/) — open to all countries; the dates are being scheduled and seats are limited, so join the waitlist there.
