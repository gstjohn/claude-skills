# Recipient modeling: folder for domain detection only, capacity from a tiered profile

## Context

The skill adapts a sender's message to a recipient's **comprehension capacity per domain** (the ability to follow content at a given depth without scaffolding). The tempting design is to scan the recipient's project folder and infer expertise from the material present. We rejected that as a capacity signal.

## Decision

**Folder content is consumed for domain detection only, never for capacity estimation.** A document's presence proves only *exposure*, and exposure is a weak and frequently *inverted* proxy for comprehension: dense reference material and AI output accumulate most in the folders of people reaching beyond their current understanding. Reading capacity from folder presence would under-scaffold exactly the novice it should protect, producing the soul-loss failure the skill exists to prevent.

Comprehension capacity instead comes from a **three-tier profile**:

1. **Recipient-stable (general setup, once per person):** register/voice, role and purpose defaults, attention budget, general reading level. Offered as **quick setup** (role preset defaults, fast) or **advanced setup** (recommended; registers voice and stable preferences).
2. **Project-scoped (per folder):** domains in play (from folder scan), capacity per domain, and an explicit verification that the folder reflects material the recipient actually understands rather than reference they are still working through.
3. **Per-run (each transformation):** detect the message's domain; if covered by Tier 2, apply silently; if outside coverage, fall back to conservative scaffolding and ask at most one lightweight question. Never silently assume uncalibrated capacity.

Register inference draws only from authored samples the recipient explicitly supplies at recipient-level setup, never from folder scavenging, because the skill cannot reliably distinguish authored material from AI output or third-party docs.

## Consequences

- A normal run asks the recipient nothing; questions fire only on out-of-domain content.
- Tier 1 values are transformation *variables* (a wrong register is recoverable), so quick setup defaulting them never threatens fidelity. Capacity is the one estimate whose error is irreversible, which is why it is never sourced from the folder.
- The skill needs a domain-coverage check at run time to decide between silent application and the conservative fallback.
