# Comprehension capacity: conservative default, raised only by evidence

## Context

The transformation needs a value for the recipient's comprehension capacity per domain to decide how much scaffolding to keep. The errors are asymmetric: over-estimating capacity strips scaffolding the recipient needed (irreversible meaning loss, the failure the skill exists to prevent), while under-estimating it over-explains (annoying, recoverable). The naive design asks the recipient their level and trusts it, but people over-rate their own competence, and over-rating is the fatal direction.

## Decision

Comprehension capacity is a **three-level, per-domain dial: novice / working / fluent.** Binary cannot drive the expertise-reversal lever (it can't separate "define every term" from "skip the basics, keep the jargon"); continuous is false precision.

The dial is **floored at novice and raised only by explicit positive evidence,** in priority order: the project-level folder-understood confirmation, then optional self-declaration in advanced setup. **Self-declaration is a soft ceiling, not gospel.** When capacity has been raised high and the run is high-stakes, the risk tier pulls scaffolding back up: stakes override a high capacity setting downward, but nothing raises capacity above the floor without evidence.

## Consequences

- Absent any positive signal, a recipient is treated as a novice in that domain. Safe by construction.
- Capacity and stakes interact at run time; the skill needs a stakes signal for the override to operate (see ADR on stakes determination).
- A recipient who over-rates themselves is still protected on high-stakes runs and, on low-stakes runs, by the per-run loss report and escape-to-source.

## Amendment (ADR-0009)

The folder-understood confirmation and the capacity setting were originally two channels (confirmation as primary evidence, self-declaration as a secondary soft ceiling). The calibration UX collapses them into a **single behaviorally-anchored question per domain** ("I understand it well enough to explain it" / "...to act on it without lookup" / "still working through it"). The question is framed as folder-understood; its gradation sets the ceiling. Novice remains the no-claim default. Optional Advanced self-declaration persists as an additional explicit ceiling on top.
