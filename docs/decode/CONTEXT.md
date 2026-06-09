# Communication Translation Layer

A skill that consumes a sender's content (text, transcript, recording, image), distills its meaning and intent, and re-encodes it to fit a recipient's comprehension profile, while preserving the original's spirit and adding nothing the sender did not state. A neutral, unbiased translation layer between sender and recipient.

## Language

**Comprehension Capacity**:
A recipient's ability to follow content at a given depth without scaffolding, scoped per domain. The dial the transformation turns. A three-level per-domain value (novice / working / fluent), floored at novice and raised only by explicit positive evidence. Not knowledge, not authorship.
_Avoid_: knowledge, competency, expertise (when what is meant is the ability to follow, not to recall or produce)

**Stakes**:
The cost of a transformation error on a given Run. Drives how aggressively content may be transformed and can override a high Comprehension Capacity downward (more scaffolding) but never the novice floor upward. The per-folder baseline is set at calibration; a single Run can raise above it (never below) when the content carries cost-signals (money, legal/contractual language, commitments, hard deadlines, high Affective Signal intensity). A run-time raise is scoped to that Run, never rewrites the profile, applies silently, and is disclosed with a terse inline note.

**Exposure**:
Evidence that a recipient has encountered material. The only thing the presence of a document in a folder proves.
_Avoid_: understanding, familiarity

**Domain**:
A bounded subject area within which Comprehension Capacity is calibrated. A recipient can be high-capacity in one domain and low in another.

**Folder Content**:
All material in the project folder the skill runs on, regardless of origin. Used for domain detection. Not valid for capacity estimation.

**Authored Material**:
Samples the recipient explicitly supplies at recipient-level setup as material they wrote themselves. The only valid source for register inference. Not extracted from Folder Content (the skill cannot reliably detect authorship). Note: this uses how the recipient *writes* as a proxy for the register they read comfortably. An accepted good-enough proxy until proven otherwise.
_Avoid_: folder content (when authorship matters)

**Baseline Profile**:
The recipient-stable tier of the profile, set once per person and reused across projects: register, role/purpose defaults, attention budget, reading level. Captured via **Quick Setup** (a single **Reading Role** choice that supplies preset defaults) or **Advanced Setup** (registers voice from **Authored Material** and stable preferences; recommended).

**Reading Role**:
The recipient's declared relationship to the material they are reading (scanning for decisions, acting on it, reviewing/approving, learning the area). A task-level, reversible posture, not a personality or learner type. It is the single thing **Quick Setup** asks, and it supplies the default register and attention budget. Distinct from a typology: it describes the job the reader is doing, not the kind of mind they have, and every value it sets is recoverable.
_Avoid_: type, profile type, communication style (when what is meant is the declared task posture, not a fixed trait)

**Recalibration**:
A change to a stored profile value after initial setup. **Comprehension Capacity** moves up only by explicit user action (the skill may prompt a raise when behavioral evidence accumulates, but never commits it silently); it never auto-lowers (run-time **Stakes** override supplies more scaffolding without rewriting the profile). Reversible Tier-1 values (**Reading Role**, register) are corrected by direct edit or correction-on-use. Capacity raises are folder-scoped and do not propagate across projects.

**Project Calibration**:
The project-scoped tier, set once per folder: the **Domains** present and the recipient's **Comprehension Capacity** within each, plus verification that the folder reflects understood material.

**Run**:
A single transformation of one piece of sender content. Detects the content's **Domain** and applies calibration silently when covered. When not covered, runs a tight structured fallback (no fixed question cap; the goal is to nail the domain fast, not to minimize questions): first confirm or correct the detected **Domain**, then ask **Comprehension Capacity** for it using the behavioral frame. Both answers fold into **Project Calibration** so the next run in that domain is silent. If the fallback is dismissed, it defaults to the skill's best-guess domain and the novice capacity floor.

**Proposition**:
A unit of meaning the seed carries forward. Every Proposition traces to one or more source spans. The skill is a translator, not a thought partner: it carries what is stated, it does not generate what is not.

**Rendering** (always done, untagged):
Carrying across what a stated sentence already encodes, including its illocutionary force, epistemic stance, deadline, and affect. "Get this to me before Thursday" encodes a directive and a deadline; rendering preserves them because they are *in* the sentence. Reading encoded force is faithful translation, not inference. Distinguished from Gap-Filling and Bridging because nothing new is added.

**Bridging Inference** (default off, tightly barred):
Inserting a new middle proposition B across a gap between stated A and stated C. Admissible only when A and C are both in the input and B is **required without question** (the unique, deductively forced connector, not a plausible or helpful one). When a gap is not without-question, the skill leaves it as a gap and flags it rather than filling it. A permitted Bridging Inference is Skill-Originated Content: marked and gated (here the logic-test that proves necessity is the gate).

**Gap-Filling** (prohibited):
Populating an absence in the input with content from the AI's world knowledge: a missing reason, cause, elaboration, or detail the sender did not supply. Forbidden even when the supplied content is factually correct or would be helpful. "Don't eat the cookies" carries forward with its reason blank; the skill never invents "because they are hot." The unsaid stays unsaid; an absence in the input is preserved as an absence in the seed.
_Avoid_: inference (when what is meant is the prohibited reach into external knowledge, not input-licensed implicature)

**Skill-Originated Content**:
The narrow set of things the skill may add that the sender did not state: a permitted **Bridging Inference** and a scaffolding explanation. (Intent reads and "natural conclusions" are *not* in this set; the translator stance bars them.) Governed by two hard rules. (1) **Marked**: visibly tagged in the output as the skill's contribution, never blended into the sender's voice. (2) **Gated**: before it stands, it is either confirmed with the operator or validated by an explicit logic test against the input. The sender's preserved seed travels untagged because it is the sender's own; everything the skill adds travels tagged and pre-checked. This makes the boundary between original meaning and skill contribution visible in every output.

**Precision**:
How definite or vague the sender's content is, on any axis (action, timing, commitment). Part of epistemic stance and therefore an **Invariant**: the skill never narrows the range the sender left. It may make vagueness **legible** (the recipient clearly sees the content is tentative or unspecified) but never **resolved** (sharpened to a definite the sender did not state). When the recipient cannot act without a resolution the source does not provide, the skill flags the gap rather than guessing.
_Avoid_: clarity (when what is meant is resolving vagueness rather than making it legible)

**Salience Hierarchy**:
Which points in the content rank highest, what matters most. An **Invariant**: the recipient must end up understanding the same things to be most important as the sender did. Preserved even when the sender buried the critical point.

**Ordering**:
The sequence of content. A **Variable held in service of Salience Hierarchy**: the skill may resequence (including surfacing a buried lede) to make true salience legible to the recipient, but never in a way that distorts what ranks highest. Carve-out: when sequence itself encodes meaning (chronology, cause then effect, a built argument), that sequence is Rendered content and is therefore Invariant. Test: if resequencing changes what the recipient understands to be true or to matter, the order was meaning; otherwise it was packaging.

**Seed**:
The structured representation of the input's meaning, extracted before any transformation (extract-then-transform). Holds every **Invariant** (propositional content, force, stance, affect-intensity, salience, meaning-bearing sequence, the unsaid, precision) with each element traced to its source span(s). The transform works from the Seed, not a free re-read of the input; the **Drift Check** verifies the output against the Seed. The Seed is the soul the skill must not lose.

**Drift Check** (back-translation):
The verification that the **Seed** survived the transform. An independent re-read derives a seed′ from the output (independent of the generator, so it cannot rubber-stamp), the marked **Skill-Originated Content** is stripped first, and seed′ is compared to the Seed on **Invariants only** (Variable differences are expected and ignored). Drift = any invariant lost or distorted, or any proposition in seed′ absent from the Seed (added meaning). On drift: bounded auto-repair, then hard escalation to the operator (never ship a known-drifted artifact). Runs on every Run except a provable identity transform; rigor scales with **Stakes** and modality risk.

**Representation**:
The form the output takes (prose, list, table, outline, diagram, image). A **Variable**, but a **constrained** one: a target Representation is permitted only if it can carry every **Invariant** in the **Seed** without forcing an assertion the Seed is silent on. Where a Representation forces a structural choice the Seed does not specify (diagram layout, table cells, outline hierarchy), the skill uses the most neutral, assertion-free arrangement, or marks the choice as **Skill-Originated Content** and gates it. The skill selects the Representation itself (no per-run menu); it defaults to preserving the sender's own form and only restructures when doing so makes true **Salience Hierarchy** legible. A different form is a one-line re-run, not a prompt.

**Modality Tier**:
The forced-invention risk of a transform, which sets **Drift Check** rigor and whether the transform is in scope. Tier 0: identity (no transform; drift check skipped). Tier 1: same modality, same Representation (text reworded/re-registered/reordered). Tier 2: same modality, cross Representation (prose to table/bullets/outline). Tier 3: cross modality (text to diagram/image, audio to visual), where the Representation itself makes assertions the Seed may not contain. **v1 scope is Tier 0-2; Tier 3 is deferred** as a separately-gated later capability.

**Operator**:
The person running the skill. In v1 (**pull**), the Operator is the **Recipient**: one user transforming inbound content to fit their own profile. The Operator self-calibrates the **Baseline Profile** and **Project Calibration**, owns the **Stakes** baseline, and confirms gated **Skill-Originated Content**. The **Sender** produces the source and is never present at the chat. The deferred **push** model (Operator transforms for a separate downstream Recipient) is out of v1 scope.
_Avoid_: user (when the Sender/Recipient distinction matters)

**Escape-to-Source**:
The recipient's ability to read the sender's original at any time. Not a feature the skill builds: the source is present in the chat because the user supplied it, never abstracted away. The user can read the original word by word, line by line, alongside the transform. The skill never narrates the source's presence (no "source is above" reminder); the source is simply there. Transparency about what the skill did is delivered as marked **Skill-Originated Content** and flagged unresolved gaps, not as a separate loss report. If drift cannot be repaired, the skill says so in the chat rather than shipping silently.

**Affective Signal**:
Emotion or attitude carried in sender content. Splits into two components the skill treats differently. The **existence and intensity** of the affect is an **Invariant** (preserved as signal: the recipient must learn the message is escalated, urgent, frustrated, etc.). The **surface expression** of the affect is a **Variable** (its venom, profanity, or rawness may be re-registered for the recipient). The skill never silently strips affect; "neutral" means it takes no side, not that it flattens force. **Stated vs. read affect:** when the sender explicitly states a feeling ("I'm frustrated"), it is Rendered seed and travels untagged in the body. When the affect is only expressed through surface signal (caps, punctuation, profanity, word choice), naming it is the skill's interpretation, not the sender's stated state, it is conveyed as an attributed read marked as **Skill-Originated Content** ("the phrasing reads as frustrated"), never asserted as fact ("the sender is frustrated"). The intensity invariant is still satisfied; the attribution just keeps the skill from putting an unstated internal state in the sender's mouth.
_Avoid_: tone (when what is meant is the preserved signal vs the adjustable surface)

## Relationships

- **Comprehension Capacity** is scoped to a **Domain**; it is not a single global value for a recipient
- **Exposure** is a weak, sometimes inverted, proxy for **Comprehension Capacity**
- **Folder Content** evidences **Domain** relevance; it does not evidence **Comprehension Capacity**
- **Authored Material** is the subset of **Folder Content** valid for register inference

## Flagged ambiguities

- "knowledge" / "competency" / "depth of knowledge" were used interchangeably. Resolved: the skill measures **Comprehension Capacity per Domain** (ability to follow), not domain knowledge (facts held) or authorship (ability to produce).
