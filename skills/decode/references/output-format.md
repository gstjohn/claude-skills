# Output format: Model 2 (clean body, numbered skill trailer)

How a transformed Run renders. The governing principle: the body is the sender's voice, the trailer is the skill's voice, and they never compete for the same line.

## The format

1. **Optional stakes line.** If the Run raised stakes, one terse line at the very top: "Treated as high-stakes (...)." Otherwise omit.
2. **Body.** Pure sender seed, transformed to fit the reader. Reads as clean prose (or list/table per the chosen Representation). No skill voice woven in. Where the skill touched a spot, place a small numbered anchor (1, 2, 3...) inline.
3. **Numbered trailer.** Each anchor resolves to one entry. This is where every Skill-Originated Content item lives: definitions, attributed tone reads, flagged gaps.

The body never contains a word the sender did not say. Everything the skill contributes is in the trailer, attributed, and strippable.

## Worked example

Sender's raw message (sitting above in the chat):
> "look the dedupe thing is a mess, we CANNOT push badge scans to prod until Kyle blesses the matching rules, full stop. we're already behind. hold the import and do NOT let marketing pin us to a date. I'll deal with Kyle."

Output:

> Treated as high-stakes (hard blocker plus a commitment to withhold a date from marketing).
>
> Hold the badge-scan import.¹ It can't go to prod until Kyle approves the matching rules.² We're already behind.³ Don't let marketing commit to a date. The sender will handle Kyle directly.
>
> 1. Tone: the phrasing (caps, "full stop", "mess") reads as frustrated and escalated. This is the skill's read of the surface, not a stated feeling.
> 2. "matching rules" = the dedupe logic that decides which scanned records are the same person.
> 3. "already behind" = the sender did not say by how much.

Note what the body does not do: it does not editorialize ("this is firm"), it does not assert the sender's emotion, and it does not invent how far behind the project is. The imperative carries the directive force on its own; the rest is attributed in the trailer.

## What goes in the trailer

- **Definitions (scaffolding).** Elaborating a term the sender used. Deletable comprehension help.
- **Attributed tone reads.** Affect the skill read from surface signal, framed as the skill's read.
- **Flagged gaps.** Unfilled absences and unresolved precision. State what is missing; do not fill it. "The sender did not say by how much" / "no date given."
- **Bridges (rare).** A permitted Bridging Inference, when one was necessary. Most runs have none.

## Representation

The skill chooses the Representation; it does not offer a menu. Default to preserving the sender's own form. Restructure (prose to list, surface a buried lede) only when doing so makes the true salience hierarchy legible. A reader who wants a different form re-runs with that ask; it is not a prompt.

A target Representation is permitted only if it can carry every Invariant without forcing an assertion the Seed is silent on. Where a form forces a structural choice the Seed does not specify (table cells, outline hierarchy), use the most neutral arrangement, or mark the choice in the trailer and gate it.

## Escape-to-source

The source is in the chat because the user pasted it. Do not narrate its presence. No "source is above" reminder, no separate loss report. Transparency about what the skill did is the inline anchors and the trailer, nothing more. If drift cannot be repaired, say so in the chat (drift-check.md) rather than shipping silently.

## Marker hygiene

The numbered anchors must survive a plain-text copy (the user will paste the transform elsewhere). Use plain numerals, not color or styling alone. If superscript numerals are unavailable in the render target, use bracketed numerals [1], [2] instead. The point is that the boundary between sender and skill stays legible after copy-paste, not just on screen.
