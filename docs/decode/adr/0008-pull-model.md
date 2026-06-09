# Pull model: Operator is the Recipient, push deferred

## Context

The skill has three actors: the Sender (produces the source, never present), the Recipient (the profile the transform adapts to), and the Operator (the person running the skill). ADRs 0001-0003 model a Recipient's comprehension capacity, register, and stakes without pinning down whether the Operator and the Recipient are the same person. Two deployment shapes follow, and they are different machines:

- **Pull (inbound).** The Recipient runs the skill on content they received, adapting it to their own profile. Operator = Recipient. The source is in the chat because they pasted it.
- **Push (outbound).** The Sender, or a proxy, runs the skill on their own content to fit a separate Recipient's profile, then delivers the transform to a Recipient who was never at the chat. Operator != Recipient.

This is not cosmetic. The escape-to-source simplification (the source is always one scroll away because the user supplied it) holds only in pull. In push, the Recipient receives only the transform and does not have the source unless it is deliberately delivered alongside, which re-introduces the travel-with-output machinery that simplification removed. Push also requires one person to configure another person's comprehension profile.

## Decision

**v1 is pull. Operator = Recipient = the single user at the chat, adapting inbound content to their own pre-calibrated profile.** This resolves the actor ambiguity in ADRs 0001-0003: the "recipient" whose profile is calibrated, the "user" who sets the stakes baseline, and the operator who confirms gated skill-originated content are all the same person.

Consequences of pull that the design relies on:
- **Escape-to-source is inherent**, because the consumer is the one who supplied the source.
- **The profile is self-calibrated**, no one models a third party's mind.
- The original vision still holds: the Sender shares however they naturally share (raw), and the Recipient de-burdens themselves on demand. The Sender never changes behavior.

**Push is deferred.** Transform-for-another-and-deliver re-opens source-delivery and the harder problem of modeling someone else's comprehension; it is a later, separately-scoped capability.

**Register proxy accepted.** In pull, "adapt to the recipient's register" means the register the user reads comfortably, proxied by their own Authored Material (how they write). Using how-they-write to stand for how-they-read-comfortably is an accepted good-enough proxy until proven otherwise.

## Consequences

- The skill is built as a single-user inbound transformer, not a sender-to-recipient delivery pipeline. Setup, calibration, stakes, and confirmation all address one person.
- Deferring push means the skill cannot be used by a sender to pre-adapt a message before sending it. Accepted for v1; pull proves the core translation-layer value without the source-delivery and third-party-modeling problems.
- If push is taken up later, escape-to-source and the role-specific ownership of stakes/calibration must be re-grilled, not assumed.
