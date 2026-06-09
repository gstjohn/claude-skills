# Output format: Model 2 (clean body, numbered skill trailer)

How a transformed Run renders. Two governing principles:

1. **Voice separation.** The body is the sender's voice, the trailer is the skill's voice, and they never compete for the same line.
2. **Positive framing.** Say what the skill *is* doing to the text. Never narrate what it is not doing or did not need to do. If the skill judged something unnecessary, leave it out silently rather than reporting the omission.

## The format

1. **High-stakes line (only when raised).** If the Run raised stakes, one line at the top stating the action being taken: "This carries a hard deadline and a financial commitment, so I'm handling it at high stakes and keeping the transform conservative." On an ordinary-stakes run, say nothing about stakes. Never write "this is not high stakes" or "I'm not adjusting"; that narrates a non-action.
2. **Body.** Pure sender seed, transformed to fit the reader. Reads as clean prose (or list/table per the chosen Representation). No skill voice woven in. Where the skill touched a spot, place a small numbered anchor inline.
3. **Numbered trailer.** Each anchor resolves to one entry. This is where every Skill-Originated Content item lives: definitions, attributed tone reads, preserved-openness notes, bridges.

The body never contains a word the sender did not say. Everything the skill contributes is in the trailer, attributed, and strippable.

## Positive framing in practice

- **State actions, not omissions.** "I'm keeping 'already behind' as the sender left it, without a figure" (an action: preserving) is right. "The sender did not say by how much" (a deficiency report) is wrong.
- **Drop the immaterial silently.** If an absence does not affect what the reader needs, say nothing about it. Only surface a preserved-openness note when the reader would otherwise expect a resolution.
- **Provenance contrast is allowed**, because attributing is an action the skill is doing: "the sender gave the depth, not the name's origin" clarifies whose contribution is whose. That is different from reporting a deficiency.
- **No standing preamble.** Do not open with a "profile set for this run" summary. The transform shows what the skill did by doing it.

## Worked example

Sender's raw message (sitting above in the chat):
> "look the dedupe thing is a mess, we CANNOT push badge scans to prod until Kyle blesses the matching rules, full stop. we're already behind. hold the import and do NOT let marketing pin us to a date. I'll deal with Kyle."

Output:

> This carries a hard blocker and a commitment to withhold a date from marketing, so I'm handling it at high stakes and preserving the directives exactly.
>
> Hold the badge-scan import.¹ It can't go to prod until Kyle approves the matching rules.² We're already behind. Don't let marketing commit to a date. The sender will handle Kyle directly.
>
> 1. Tone: the phrasing (caps, "full stop", "mess") reads as frustrated and escalated. This is the skill's read of the surface, not a stated feeling.
> 2. "matching rules" = the dedupe logic that decides which scanned records are the same person.
>
> I'm keeping "already behind" as the sender left it, without a figure.

Note what the body does not do: it does not editorialize ("this is firm"), it does not assert the sender's emotion, and it does not invent how far behind the project is. The imperative carries the directive force on its own; the rest is attributed in the trailer.

## What goes in the trailer

- **Definitions (scaffolding).** Elaborating a term the sender used. Frame as the skill's addition with the reason: "the skill's definition; strip it and the sender's meaning is unchanged." Attribute provenance when the sender already glossed a term ("the sender's own gloss follows") versus when the skill supplied it.
- **Attributed tone reads.** Affect the skill read from surface signal, framed as the skill's read.
- **Preserved-openness notes (only when material).** When the skill is deliberately keeping something vague or open that the reader might expect resolved, state it as an action: "I'm keeping X open because the sender left it open." Omit when the openness does not matter to the reader.
- **Bridges (rare).** A permitted Bridging Inference, when one was necessary. Most runs have none.

## Representation

The skill chooses the Representation; it does not offer a menu. Default to preserving the sender's own form. Restructure (prose to list, surface a buried lede) only when doing so makes the true salience hierarchy legible. A reader who wants a different form re-runs with that ask; it is not a prompt.

A target Representation is permitted only if it can carry every Invariant without forcing an assertion the Seed is silent on. Where a form forces a structural choice the Seed does not specify (table cells, outline hierarchy), use the most neutral arrangement, or mark the choice in the trailer and gate it.

## Escape-to-source

The source is in the chat because the user pasted it. Do not narrate its presence. No "source is above" reminder, no separate loss report. Transparency about what the skill did is the inline anchors and the trailer, nothing more. If drift cannot be repaired, say so in the chat (drift-check.md) rather than shipping silently.

## Marker hygiene

The numbered anchors must survive a plain-text copy (the user will paste the transform elsewhere). Use plain numerals, not color or styling alone. If superscript numerals are unavailable in the render target, use bracketed numerals [1], [2] instead. The point is that the boundary between sender and skill stays legible after copy-paste, not just on screen.
