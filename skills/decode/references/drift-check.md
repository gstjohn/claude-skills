# Drift check: back-translation and escalation

The drift check is the anti-telephone guarantee made operational. It is the adversarial-verify pattern pointed inward at the skill's own output: prove the Seed survived the transform before presenting it.

## The check

1. **Independent re-read.** Derive a fresh seed (call it seed-prime) from the output, independent of the process that generated the output, so it cannot rubber-stamp its own work.
2. **Strip the marked layer first.** Remove all Skill-Originated Content (scaffolding, bridges, tone reads) before re-extracting. The check verifies the sender's seed survived, not the skill's additions.
3. **Compare on Invariants only.** seed-prime vs. the original Seed, across the Invariant list in fidelity-rules.md. Variable differences (register, ordering, length, affect expression) are expected and ignored.
4. **Drift =** any Invariant lost or distorted, OR any proposition in seed-prime that is absent from the Seed (added meaning, the hallucination tripwire).

## Why against the Seed, not the raw input

Comparing the output to the raw input would flag every intended change (reworded, reordered, re-registered) as drift and drown the real loss in noise. The Seed holds only the Invariants, so comparing against it isolates genuine meaning loss from packaging changes.

## When it runs

On every Run except a provable identity transform (output structurally and semantically identical to input, a deterministic comparison with no meaning judgment). Any actual change, however small, gets at least one pass. A dropped sub-clause in a "simple" reformat is exactly the silent loss the check exists to catch, so there is no triviality skip.

## Rigor scales with stakes and modality

The lever is the intensity of the check, never whether to check.
- Low-stakes, same-modality (Tier 1): one pass.
- High-stakes or cross-representation (Tier 2): multiple independent adversarial passes.

Rigor is mostly invisible. Do not print "verified in N passes" on every run; that trains the reader to skim and mirrors the banned habit of asking "did I get this right." Rigor becomes visible only where it already changes the output: the high-stakes inline note, and an actual escalation.

## On drift: repair, then escalate

1. **Bounded auto-repair.** Regenerate the transform targeting the specific failed Invariant and re-check. Do this a bounded number of times.
2. **Hard escalation** if drift persists. Never ship a known-drifted artifact.

## Escalation UX: the failure-framed partial

When auto-repair fails, do not refuse wholesale and do not ship-with-a-warning-banner. Deliver a **failure-framed partial**:

1. **Lead with one plain failure statement** naming the Invariant that will not survive. Do not restate it later.
2. **Ship the portions that passed** the check as normal transform.
3. For the span where the Invariant fails, **stop transforming and hand back the sender's original words for that span, inline, labeled plainly.**

Example (drift on the salience of a buried clause):

> I couldn't fully preserve this. The sender's emphasis on one point won't survive my rewrite, so I'm handing that part back in their own words.
>
> [faithful transformed portion]
>
> **Sender's original:**
> > "...and whatever else happens, the Tuesday cutover does NOT move."

This is strictly more helpful than a blanket refusal (the faithful remainder still ships) and never ships a known-drifted artifact (the failed piece is raw source, not a smooth rewrite). The reader cannot mistake it for a clean transform, and gets the raw text for exactly the piece that would not translate.

## Why ship-with-flag is rejected

A transform that reads as finished gets trusted; a warning banner gets skimmed past. Shipping a smooth-but-drifted artifact with a flag is the precise silent-soul-loss failure the drift check exists to prevent. The failed span must be visibly raw, not visibly flagged.
