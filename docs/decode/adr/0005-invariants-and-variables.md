# Invariants and variables: what the transform must preserve vs. what it may change

## Context

The transform adapts a sender's content to a recipient. To do that without a telephone-game failure, the skill needs an explicit line between what must survive unchanged (the meaning, the seed's soul) and what is free to change (the packaging the recipient sees). Without the line, "adapt for the recipient" has no stopping rule and drifts into rewriting the message.

## Decision

**Invariants, preserved on every transform:**

- **Propositional content**: the claims the sender stated.
- **Illocutionary force**: request vs. order vs. FYI; a question that functions as a directive stays a directive.
- **Epistemic stance**: hedged stays hedged, certain stays certain.
- **Affective signal (existence and intensity)**: that the message is escalated/urgent/frustrated, as signal.
- **Salience hierarchy**: what the sender treated as mattering most still reads as mattering most.
- **Meaning-bearing sequence**: chronology, cause→effect, a built argument; ordering that encodes meaning.
- **The unsaid**: absences the sender left (a missing reason, deadline, rationale) stay absent.

**Variables, free to change in service of the recipient:**

- **Surface form and wording.**
- **Register**: including the surface expression of affect (its venom or rawness may be re-registered).
- **Length.**
- **Representation**: text, list, table, etc. (subject to the modality-risk rules).
- **Ordering**: non-meaning-bearing sequence, held in service of the salience-hierarchy invariant; the skill may surface a buried lede but may not distort what ranks highest.

## Consequences

- Adaptation has a hard stopping rule: it may move any variable but may not touch an invariant. "Adapt for the recipient" can no longer drift into rewriting meaning.
- Affect and ordering each split across the line (intensity vs. expression; meaning-bearing vs. packaging), so the skill needs a per-element classifier for those two, not a blanket rule.
- The seed must record every invariant explicitly so the transform and the drift check (forthcoming ADR) have something concrete to preserve and verify against.
- This list is the preservation target the back-translation / drift check measures the output against.
