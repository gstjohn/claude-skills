# Calibration: building the reader's profile

How the skill learns who it is translating for. The profile is the prepared audience model that spares the reader from re-deriving their own needs under load on every message.

## The spine principle

**Calibrate on evidence and behavior, never on self-rated type.** This governs every question the skill asks. Where over-statement is irreversible (comprehension capacity), elicit evidence or hold the novice floor. Where the error is recoverable (register, stakes, reading role), accept self-declaration because the next run corrects it.

Concretely, this rules out: personality typing, learner-style sorting, and any "rate your level 1 to 5" question. People over-rate their own competence, and over-rating capacity is the one error the skill cannot recover from. (See README for the evidence.)

## Lazy, just-in-time, persisted

No `/setup` ceremony. The profile is built inline as it is needed, then persisted.

- **First run with no profile:** trigger a minimal Quick Setup (one question).
- **First run in a new folder:** trigger Project Calibration.
- Each is asked once per scope, then reused.

All calibration questions are AskUserQuestion-style structured choices, not free-text interviews. Lower cognitive load, concrete anchors instead of self-generated ratings.

## Two tiers

### Tier 1: about the reader (asked once per person, persists in the config home)

Recipient-stable values reused across every project: register and voice, reading role defaults, attention budget, general reading level.

- **Quick Setup = one question: Reading Role.** The reader's declared relationship to material they read (scanning for decisions, acting on it, reviewing or approving, learning the area). A role preset supplies a default register and attention budget. This is a task posture, not a personality type, and every value it sets is recoverable. Everything not asked falls to the safe floor.
- **Advanced Setup (offered, never blocking; recommended).** Registers the reader's voice from Authored Material (two or three samples the reader attests they wrote themselves) and captures stable preferences. Register is inferred silently and corrected from an actual transform, never confirmed by asking "did I get this right." (Self-reported alignment is a near-zero proxy; see README.)

Authored Material is the only valid source for register inference. Never scavenge it from folder content; the skill cannot reliably tell authored text from AI output or third-party docs.

### Tier 2: about this folder (asked once per folder, persists folder-local)

- **Domains present**, detected from a folder scan and confirmed with the reader. Coarse granularity by default; split a domain only if it is lopsided.
- **Comprehension capacity per domain.** One behavioral question per domain: "I understand it well enough to explain it" / "...to act on it without lookup" / "still working through it." Asking what the reader does with the material, not how good they are, blunts over-rating. Novice is the no-claim default.
- **Stakes baseline.** "If this skill misreads something here, how bad is that?" Default high when skipped.

Make the tier boundary legible by labeling every prompt "about you (asked once)" vs. "about this folder." Never expose the word "tier."

## Folder content is for domain detection only

A document's presence in a folder proves only **exposure**, not comprehension. Exposure is a weak and often inverted proxy: dense reference material accumulates most in the folders of people reaching beyond their current understanding. Reading capacity from folder presence would under-scaffold exactly the novice it should protect. So folder content detects domains and never estimates capacity.

## The safe floor

Skip everything and you get **novice capacity + high stakes** = maximum scaffolding, most faithful output. Safe by construction. The reader earns lighter transforms by lowering stated stakes or raising stated capacity through evidence, never the reverse.

## Recalibration is asymmetric

- **Capacity rises only by explicit user action.** The skill may prompt a raise when behavioral evidence accumulates (the in-the-moment offer in run-protocol.md), but never commits it silently. Raises are folder-scoped and do not propagate to the person or to other folders, because folder-understood evidence is folder-specific.
- **Capacity never auto-lowers.** When a reader needs more help on a particular run, the run-time stakes raise supplies more scaffolding without rewriting the profile.
- **Reversible Tier 1 values** (reading role, register) are corrected by direct edit or correction-on-use.
- **`/recalibrate` is always available** for proactive adjustment.

## Stakes: user owns the baseline, inference only raises

Capacity floors low safely because novice is also the common case. Stakes cannot floor high (the skill would never transform anything and be useless) or low (unsafe). So the user sets the baseline expressing their own risk appetite, and inference can only raise a given run above it, never lower it. Only an explicit human signal drops a run below baseline, because lowering stakes means a more aggressive transform, which never happens automatically. Every automatic move the skill makes is toward more fidelity, never less.
