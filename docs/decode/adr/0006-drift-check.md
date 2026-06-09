# Drift check: invariant-only back-translation, always on except provable identity

## Context

The invariant set (ADR-0005) and the grounding model (ADR-0004) are inert without a mechanism that verifies the invariants actually survived the transform. The skill needs an enforcement engine: the anti-telephone guarantee made operational. This is the deep-research adversarial-verify pattern pointed inward at the skill's own output.

Two design traps. First, a back-translation that compares the output to the raw input flags every *intended* change (register, order, length, affect-expression) as drift, drowning real loss in noise. Second, a back-translation produced by the same process that generated the output rubber-stamps its own work.

## Decision

The drift check re-derives meaning from the output and verifies it against the **Seed**, not the raw input, and it is **invariant-aware**:

1. **Independent re-read.** A fresh extraction derives a seed′ from the output, independent of the generator, so it cannot rubber-stamp.
2. **Strip the marked layer first.** Scaffolding and bridges are tagged Skill-Originated Content; the check removes them before re-extracting, because it is verifying the *sender's* seed survived, not grading the skill's additions.
3. **Compare on invariants only.** seed′ vs. Seed across the ADR-0005 invariants. Variable differences (register, ordering, length, affect-expression) are expected and ignored.
4. **Drift** = any invariant lost or distorted, OR any proposition in seed′ absent from the Seed (added meaning, the hallucination tripwire).

**On drift: bounded auto-repair, then hard escalation.** Regenerate the transform targeting the specific failed invariant and re-check, for a bounded number of attempts. If drift persists, block the silent output and surface to the operator which invariant will not survive, with escape-to-source. The skill never ships a known-drifted artifact.

**The check runs on every Run except a provable identity transform.** A triviality floor ("skip the check on a simple reformat") was rejected: deciding a change is trivial is itself a fallible meaning judgment, and its failure mode is the exact silent soul-loss the check exists to prevent, so it trades a cheap deterministic pass for a probabilistic irreversible failure, against the conservative-default spine of ADR-0002 and ADR-0003. The only safe skip is **provable non-transformation**: output structurally/semantically identical to input, which is a deterministic comparison with no meaning judgment in the path. Any actual change, however small (including same-modality reformatting, where a dropped sub-clause is the common failure), gets at least one pass.

The lever is the **intensity** of the check, never whether to check: one pass for low-stakes same-modality, multiple independent adversarial passes for high-stakes or cross-modality runs.

## Consequences

- Most runs carry the cost of at least one independent re-read. Accepted: the cost is cheap relative to the irreversible failure it prevents, and it is the skill's reason to exist.
- The check is where earlier moves earn their keep: it is what confirms affect-intensity survived after the venom was softened, and that salience survived after a reorder.
- The skill needs an extractor that can run in two independent modes (generate-the-seed, and re-derive-seed′-from-output) without shared state, and a comparison that operates strictly on the invariant set.
- Rigor scaling couples this ADR to the forthcoming modality-risk-tier decision.

## Amendment: escalation UX and visible rigor

The original decision specified *that* the skill escalates on persistent drift ("surface to the operator which invariant will not survive, with escape-to-source") but not *what the operator sees*. Three shapes were on the table:

1. **Pure refuse**: ship nothing, name the failed invariant, send the user to the source. Safest and leanest, but abandons the user exactly when the content was hard enough to need the skill.
2. **Ship-with-flag**: deliver the best attempt with a warning banner. Rejected: this is the silent-soul-loss failure mode the drift check exists to prevent. A transform that reads as finished gets trusted; the banner gets skimmed past.
3. **Failure-framed partial**: chosen.

**On persistent drift, the skill delivers a failure-framed partial.** It leads with one plain failure statement naming the invariant that won't survive (no closing restatement of it). It ships the portions that *passed* the drift check as normal transform. For the span where the invariant fails, it stops transforming and hands back the **sender's original words for that span inline**, labeled plainly. The artifact can never be mistaken for a clean transform, and the user gets raw text for exactly the piece that wouldn't translate. This is strictly more helpful than pure refuse (the faithful remainder still ships) without ever shipping a known-drifted artifact (the failed piece is raw source, not a smooth rewrite).

**Rigor is mostly invisible.** The pass count is internal machinery; broadcasting "verified in N passes" on every run is the same instinct as asking "did I get this right," and it trains the user to skim. Rigor becomes visible only at two edges that already change the output: the high-stakes inline note (which implicitly signals the heavier treatment) and an actual escalation (the failure-framed partial above). No persistent verification badge.
