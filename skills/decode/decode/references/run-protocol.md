# Run protocol: the per-transformation flow

A Run is a single transformation of one piece of sender content. This file specifies the flow end to end and the run-time decisions inside it.

## The loop

1. **Ingest.** Take the content the user pasted (text, transcript, document, image within scope).
2. **Detect the Domain.** Identify the subject area. Check it against the folder's calibration (calibration.md).
   - **Covered:** apply the stored comprehension capacity silently. Ask nothing.
   - **Not covered:** run the uncovered-domain fallback below.
3. **Determine Stakes for this Run.** Start from the folder baseline. Raise it if the content carries cost-signals (see "run-time stakes raise" below). Never lower it automatically.
4. **Extract the Seed** (fidelity-rules.md). Every Invariant, traced to its span.
5. **Transform** the Seed to fit the reader's capacity and register. Move Variables only.
6. **Drift check** (drift-check.md). Verify the Seed survived. Repair or escalate on drift.
7. **Present** in the Model 2 format (output-format.md).

## The uncovered-domain fallback

When the content's Domain is not covered by the folder's calibration, run a tight structured sequence. There is no fixed question cap; the goal is to nail the domain fast, not to minimize questions. Use AskUserQuestion-style structured choices, not free text.

1. **Confirm or correct the Domain.** Present the skill's best-guess domain pre-selected, with two or three alternates and an escape hatch. This catches mis-detection before it poisons the rest of the run.
2. **Ask comprehension capacity** for the confirmed domain, using the behavioral frame: "I understand it well enough to explain it" / "...to act on it without lookup" / "still working through it." Ask what the reader does with the material, never how good they are.

Both answers fold into the folder's Project Calibration so the next run in that domain is silent.

If the user dismisses the fallback: default to the skill's best-guess domain and the **novice capacity floor**. Safe by construction.

## Run-time stakes raise

Stakes default high and the user owns the per-folder baseline (calibration.md). A single Run can raise above the baseline, never below it.

Raise when the content carries cost-signals:
- Money or figures, legal or contractual language, named commitments or obligations.
- Hard deadlines, directives, irreversible actions.
- High affective-signal intensity (escalation, urgency).

When you raise:
- **Scope it to this Run only.** Never rewrite the stored profile.
- **Apply without asking** (raising means more scaffolding, the safe direction).
- **Disclose it in one line, framed as the action being taken:** "This carries a financial commitment and a hard deadline, so I'm handling it at high stakes and keeping the transform conservative." Only on a raise. On an ordinary-stakes run, say nothing about stakes; never state that stakes are ordinary or that no adjustment is happening (that narrates a non-action). No override widget; if the raise was wrong, the source is right there and a re-run costs nothing.

Uncertainty about stakes resolves higher, not lower.

## The capacity-raise offer

Capacity rises only by explicit user action, never automatically (calibration.md). The skill offers a raise in the moment, not on a long-horizon counter.

When the user corrects a Run for over-scaffolding in a domain (trims the explanations, says "too much detail here"), append a single offer at the **end** of that run's output, after the transform is delivered and never blocking it:

> You trimmed the explanations here. Raise your capacity in [domain] so I stop over-explaining?

- Commit only on an explicit yes.
- A yes writes the new capacity into the **folder's** calibration for that domain (not the person, not just this chat).
- A dismissal backs off: do not re-offer this session.

`/recalibrate` is always available for the user to adjust capacity proactively.

## What a normal run looks like

For a reader whose domain is calibrated, a Run asks nothing. Ingest, extract, transform, check, present. Questions fire only on uncovered domains, and the in-the-moment capacity offer fires only after a correction. The prepared profile is what spares the reader from being interrogated on every message.
