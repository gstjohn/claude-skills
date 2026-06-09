# Grounding model: translator, not thought partner

## Context

The skill must transform a sender's content for a recipient without hallucinating. The make-or-break constraint is fidelity: no added information the sender did not state. But the recipient branch (ADR-0001) has the skill *add scaffolding* for a low-capacity recipient, and scaffolding draws on the AI's world knowledge. Adaptation and anti-hallucination run straight into each other, so the line between them has to be exact.

The operative definition of hallucination for this skill: **the AI reaching into its own knowledge base to fill an absence in the input.** "Don't eat the cookies" supplies no reason; the forbidden move is supplying one ("because they are hot"), even when it is factually correct, because the real reason ("saving them for your brother") was never in the text. The skill is a translator, not a thought partner: it carries what is stated, it does not generate what is not.

## Decision

Three operations, with sharp boundaries:

1. **Render (always done, untagged).** Carry across what a stated sentence already encodes: its propositional content, illocutionary force, epistemic stance, deadline, and affect. The directive and deadline in "get this to me before Thursday" are *in* the sentence; preserving them is faithful translation, not inference. Affect splits here: its existence and intensity are rendered (invariant); its surface expression may be re-registered for the recipient (variable). Rendering is the sender's own meaning, so it travels untagged.

2. **Bridging Inference (default off, tightly barred).** Insert a new middle proposition B across a gap between stated A and stated C *only* when A and C are both in the input and B is required without question (the unique, deductively forced connector, not a plausible or helpful one). When a gap is not without-question, leave it as a gap and flag it rather than fill it. The unsaid stays unsaid.

3. **Gap-Filling (prohibited).** Populating any absence with world knowledge: a missing reason, cause, elaboration, or detail. Forbidden regardless of correctness or helpfulness.

**Scaffolding is admissible but quarantined.** It may only elaborate a term the sender invoked (explaining "canary" because the sender said "canary"), never explain into a sender-left blank. It is marked as the skill's aid, never blended into the sender's voice, and always strippable back to the bare seed. This is the one sanctioned use of the AI's world knowledge, sanctioned because it is walled off, anchored, and removable.

**Skill-originated content is marked and gated.** Anything the skill adds (a permitted Bridging Inference, scaffolding) is (1) visibly tagged as the skill's contribution and (2) gated before it stands, either confirmed with the operator running the skill or validated by an explicit logic test against the input. For a Bridging Inference the logic-test that proves necessity *is* the gate. The sender's rendered seed travels untagged; everything the skill adds travels tagged and pre-checked, so every output shows where the original ends and the skill begins.

## Consequences

- "Intent reads" and "natural conclusions" are off the table by default. The skill does not surface what the sender "really meant" beyond what the words encode; that would be thought-partnering.
- The marking-and-gating machinery governs a small surface (necessary bridges, scaffolding), not a broad inference layer, which keeps most runs silent and untagged.
- Gaps that genuinely impede the recipient are surfaced through the loss report and escape-to-source (see forthcoming ADR), never closed by invention.
- The skill needs a reliable test for "required without question" and a span-tracing mechanism so every rendered proposition and every bridge can point back to its source.
