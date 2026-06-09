# Fidelity rules: the Seed, Invariants, and the grounding model

This is the heart of the skill. It defines what must be preserved, what may change, and the exact line between faithful translation and hallucination.

## Extract the Seed before transforming

Do not transform the input directly. First extract a **Seed**: a structured representation of the input's meaning. Every element of the Seed traces to one or more spans in the source. The transform works from the Seed, not from a fresh re-read of the input, and the drift check verifies the output against the Seed. The Seed is the meaning the skill must not lose.

The Seed records every Invariant below, each with its source span(s).

## Invariants: preserve on every transform

These are the soul of the message. Changing any of them is the telephone-game failure the skill exists to prevent.

- **Propositional content.** The claims the sender actually stated.
- **Illocutionary force.** Request vs. order vs. FYI. A question that functions as a directive stays a directive. "Can you get this to me by Thursday" is a deadline, not a yes/no question.
- **Epistemic stance.** Hedged stays hedged. Certain stays certain. Do not firm up a "maybe" or soften a "will."
- **Affective signal (existence and intensity).** That the message is escalated, urgent, or frustrated is signal the reader must receive. See "affect" below for how to convey it without putting words in the sender's mouth.
- **Salience hierarchy.** What the sender treated as mattering most must still read as mattering most, even if they buried it.
- **Meaning-bearing sequence.** Chronology, cause then effect, a built argument. When order encodes meaning, the order is an Invariant.
- **The unsaid.** Absences the sender left (a missing reason, deadline, rationale) stay absent. Do not fill them.
- **Precision.** How definite or vague the content is, on any axis. Never narrow the range the sender left open.

## Variables: free to change in service of the reader

- **Surface wording.**
- **Register.** Including the surface expression of affect (venom, profanity, rawness may be re-registered).
- **Length.**
- **Representation.** Prose, list, table, outline (subject to the modality scope in SKILL.md and the rules in output-format.md).
- **Ordering** that does not encode meaning. Held in service of salience: you may surface a buried lede, but you may not distort what ranks highest.

The stopping rule: you may move any Variable. You may not touch any Invariant. "Adapt for the reader" never licenses rewriting meaning.

## The three operations

Every piece of the output is produced by exactly one of these.

### 1. Render (always done, untagged)

Carry across what a stated sentence already encodes: its propositional content, force, stance, deadline, affect intensity. Reading the encoded meaning of a sentence is faithful translation, not inference. Rendered content is the sender's own meaning, so it travels **untagged** in the output body.

### 2. Bridging Inference (default off, tightly barred)

Insert a new middle proposition B across a gap between stated A and stated C, **only** when:
- A and C are both present in the input, and
- B is **required without question**: the unique, deductively forced connector, not a plausible or helpful one.

Test before inserting a bridge: "Is there any reading of A and C where B is false?" If yes, it is not a bridge. Leave the gap and flag it.

In practice bridges are rare. Most of the time, placing the sender's adjacent statements next to each other lets the reader infer the link themselves, which is correct: the skill should not assert a connector the sender left implicit. A bridge is for the case where the body genuinely cannot cohere without it. A permitted bridge is Skill-Originated Content: marked and gated (the logic test that proves necessity is the gate).

### 3. Gap-Filling (prohibited)

Populating an absence with world knowledge: a missing reason, cause, elaboration, or detail the sender did not supply. Forbidden even when the supplied content is factually correct or would be helpful. "Don't eat the cookies" carries forward with its reason blank. The skill never invents "because they are hot." The unsaid stays unsaid.

## Scaffolding: the one sanctioned use of world knowledge

Scaffolding is an explanation the skill adds to help a lower-capacity reader. It is admissible but quarantined:

- It may only **elaborate a term the sender invoked** (explain "matching rules" because the sender said "matching rules"), never explain into a blank the sender left.
- It is **marked** as the skill's aid, never blended into the sender's voice.
- It is **strippable** back to the bare Seed without loss.

How much scaffolding to add is set by the reader's comprehension capacity for the domain (see calibration.md). Novice: define terms, spell out implications the words encode. Fluent: keep the jargon, skip the basics.

## Affect: stated vs. read

The intensity of affect is an Invariant and must be conveyed. But how you convey it depends on whether the sender stated it or only expressed it.

- **Stated affect.** The sender wrote "I'm frustrated." This is Rendered seed. It travels untagged in the body, in the sender's voice.
- **Read affect.** The sender did not name a feeling, but the surface (caps, punctuation, profanity, word choice) carries it. Naming this is the skill's interpretation, not the sender's stated state. Convey it as an **attributed read, marked as Skill-Originated Content** ("the phrasing reads as frustrated"). Never assert it as fact ("the sender is frustrated").

Either way the intensity invariant is satisfied: the reader learns the message is escalated. The attribution just keeps the skill from putting an unstated internal state in the sender's mouth.

## What is off the table

"Intent reads" and "what the sender really meant" beyond what the words encode. That is thought-partnering, not translation. The skill carries what is stated. It does not generate what is not.
