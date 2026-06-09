# Modality risk tiers: representation as a constrained variable, v1 scoped to Tier 0-2

## Context

Representation is a variable (ADR-0005), the skill may change prose to a list, text to a diagram. But the risk of a representation change is not uniform, and ADR-0006 already scales drift-check rigor by "modality risk" without defining it. The defining hazard is not the size of the change. It is that some target representations **force invention the Seed does not contain.**

A diagram must place boxes and draw arrows. Given only "sales, ops, and finance are involved," a diagram must arrange them (adjacent, hierarchical, or as a flow), none of which the input stated. The layout either omits a relationship (loss) or asserts one (gap-filling in visual form). An image commits to detail (color, setting, expression) the words never specified. The representation itself makes assertions, and the Seed may be silent on them.

## Decision

**Representation is a constrained variable: a target representation is permitted only if it can carry every Invariant in the Seed without forcing an assertion the Seed is silent on.** Where a representation forces a structural choice the Seed does not specify, the skill uses the most neutral, assertion-free arrangement (a flat list, not a hierarchy), or marks the choice as Skill-Originated Content and gates it.

Transforms are tiered by forced-invention risk, which sets drift-check rigor:

- **Tier 0: Identity.** No transform; drift check skipped (ADR-0006).
- **Tier 1: Same modality, same representation.** Reword, re-register, reorder text→text. One drift pass. No forced invention.
- **Tier 2: Same modality, cross representation.** Prose→table/bullets/outline. One-to-multi pass; watch structure-forced assertions (a table implies every cell is filled; an outline implies hierarchy).
- **Tier 3: Cross modality.** Text→diagram/image, audio→visual. Multi-pass drift check; the permission rule bites hardest here.

**v1 scope is Tier 0-2. Tier 3 is deferred** as a separately-gated later capability, because cross-modality is where soul-loss concentrates and where the marking/gating machinery gets its hardest workout. Proving the core on same-modality first de-risks the fidelity guarantee before taking on representations that assert structure on their own.

## Consequences

- The skill needs a check, before transforming, that the chosen representation can carry the Seed's invariants; an incapable representation is refused or downgraded, not attempted-and-patched.
- Deferring Tier 3 means the v1 skill cannot produce diagrams or images from text. Accepted: those are the highest-risk outputs and are not needed to prove the core translation-layer value.
- Tier classification is mechanical (modality and representation of input vs. output), not a meaning judgment, so unlike the rejected triviality floor it introduces no fallible-classifier failure surface.
