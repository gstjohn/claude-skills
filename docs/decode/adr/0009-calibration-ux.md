# Calibration is lazy, evidence-based, and never a self-rated typology

## Context

Every upstream ADR assumes a calibrated profile exists but none specifies how it is captured. The naive design is an upfront wizard that asks the user to rate their level. The human-communication research (`docs/research/human-communication-differences*.md`) makes that design unsafe: self-rated style and level have no predictive validity and bias upward (the fatal direction for capacity), and discrete typologies (MBTI, DISC, VAK) fail psychometrics. The one finding that argues for any up-front work is that audience design degrades under cognitive load, so the model the human relies on should be prepared in advance, not improvised per message.

## Decision

**Calibrate on evidence and behavior, never on self-rated type.** Where over-statement is irreversible (Comprehension Capacity) the skill elicits evidence or holds the novice floor; where the error is recoverable (register, Stakes, Reading Role) self-declaration is accepted because the next run corrects it.

The mechanism and flow:

- **Lazy, just-in-time, persisted.** No `/setup` ceremony. First run with no Baseline Profile triggers a minimal inline Quick Setup (defaults to one question); first run in a new folder triggers Project Calibration. Each is asked once per scope, then persisted. The persisted profile is the prepared audience model that spares the human from re-deriving under load.
- **All calibration questions are AskUserQuestion-style structured choices**, not free-text interviews. Lower cognitive load, concrete anchors instead of self-generated ratings.
- **Quick Setup = one question: Reading Role.** A role preset supplies default register and attention budget. Everything not asked falls to a safe floor (capacity = novice, Stakes = high). Leanness is paid for by conservatism, not risk. Advanced Setup is offered, never blocking.
- **Project Calibration domains are detected and confirmed**, coarse granularity by default; the user splits a domain only if lopsided.
- **Capacity and the folder-understood check are one question per domain**, framed behaviorally ("I understand it well enough to explain it" / "...to act on it without lookup" / "still working through it"). Asking what the user *does* with the material, not how *good* they are, blunts over-rating; novice is the no-claim default. (See ADR-0002 amendment.)
- **Stakes baseline is Tier 2 (per folder)**, asked as "if this skill misreads something here, how bad is that?", default high when skipped.
- **Authored Material is the evidence channel for register** (Advanced/Tier 1, 2-3 attested samples). Register is inferred silently and corrected from an actual transform, never confirmed by asking "did I get this right?" (self-reported alignment is a near-zero proxy).
- **Tier 1 persists per-person (config home), Tier 2 persists folder-local.** The boundary is made legible by labeling every prompt "about you (asked once)" vs "about this folder," never by exposing the tier concept.
- **Recalibration is asymmetric.** Capacity rises only by explicit user action (the skill prompts on accumulated behavioral evidence, the human commits); it never auto-lowers (run-time Stakes override handles "needs more help now"). `/recalibrate` is always available. Raises are folder-scoped.

## Consequences

- Skipping all setup yields novice capacity + high stakes = maximum scaffolding, most faithful output. Safe by construction; the user earns lighter transforms by lowering stated stakes, not the reverse.
- The same domain is re-calibrated in each new folder. Deliberate: folder-understood evidence is folder-specific. Prompts acknowledge this so it does not read as the skill forgetting.
- Self-report cannot be fully removed from a one-user pull tool (no third party to verify against). This design minimizes it; the run-time backstops (Stakes override, drift check, escape-to-source) contain the residue.
