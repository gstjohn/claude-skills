---
name: decode
description: Faithfully re-encodes dense inbound content (email, transcript, message, document, image) to fit the reader's comprehension level, preserving meaning, force, and emphasis while adding nothing the sender did not say. Use when the user pastes a message, thread, transcript, or document they find dense, jargon-heavy, long, or hard to parse and wants it made readable without losing or inventing meaning. Triggers include "decode this", "what is this saying", "break this down", "make this readable", "translate this for me", "I can't parse this".
license: MIT
---

# decode

A neutral translation layer. The user pastes content they find hard to read; decode re-encodes it to fit how that user reads, preserving the sender's meaning exactly and adding nothing the sender did not state.

## The one rule that governs everything

Fidelity. No hallucination, no added information, no lost meaning (anti-telephone). Every other behavior in this skill exists to enforce that rule. When a choice trades readability against fidelity, fidelity wins. The reader is the person who pasted the content, so the original is always one scroll up; decode never has to reconstruct it, only translate it.

## The run loop

Every transformation runs this loop. Full detail in [reference/run-protocol.md](references/run-protocol.md).

1. **Ingest** the content the user pasted.
2. **Detect the Domain.** If the user's calibration covers it, apply silently. If not, run the structured fallback (confirm the domain, then ask comprehension capacity). See [reference/calibration.md](references/calibration.md).
3. **Extract the Seed.** Build a structured representation of the input's meaning before transforming anything. The Seed holds every Invariant, each traced to its source span. See [reference/fidelity-rules.md](references/fidelity-rules.md).
4. **Transform** the Seed to fit the reader's profile. Move only Variables; never touch an Invariant.
5. **Drift check.** Back-translate the output and verify the Seed survived. On unrepaired drift, escalate. See [reference/drift-check.md](references/drift-check.md).
6. **Present** in the Model 2 output format. See [reference/output-format.md](references/output-format.md).

## Hard rules (never break these)

- **Render, do not invent.** Carry across what a sentence already encodes (its claim, force, stance, deadline, affect). Never reach into world knowledge to fill an absence the sender left. A missing reason stays missing. Full grounding model in [reference/fidelity-rules.md](references/fidelity-rules.md).
- **Mark everything you add.** Anything the skill contributes (a definition, a forced bridge, a tone read) is tagged as the skill's, never blended into the sender's voice. The sender's words travel untagged because they are the sender's. See [reference/output-format.md](references/output-format.md).
- **Never assert an unstated internal state.** If the sender did not say they were frustrated, you do not say they are. You say the phrasing reads as frustrated, and you mark it as your read.
- **Never narrow what the sender left open.** Vague stays legibly vague. Flag the gap; do not resolve it.
- **Never ship a known-drifted artifact.** If the output cannot preserve an Invariant, hand that span back in the sender's own words and say so.

## Calibration

Lazy and just-in-time. There is no setup ceremony. The first run with no profile asks one question; the first run in a new folder calibrates the folder. Everything not asked falls to the safe floor: novice comprehension, high stakes, maximum scaffolding. Capacity rises only by explicit user action, never automatically. Full model in [reference/calibration.md](references/calibration.md).

## Scope

v1 handles text and same-modality reformatting (Tier 0 through Tier 2: reword, re-register, reorder, prose to list or table). Cross-modality generation (text to diagram or image) is Tier 3 and is deferred. If asked for a Tier 3 output, say it is out of scope rather than attempting it.

## When in doubt

Default conservative. More scaffolding, less transformation, the novice floor, high stakes. Over-explaining is annoying and recoverable. Under-explaining or inventing meaning is the failure this skill exists to prevent.
