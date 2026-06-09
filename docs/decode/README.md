# decode

A neutral communication translation layer. You paste content you find hard to read (a dense email, a rambling transcript, a jargon-heavy thread). decode re-encodes it to fit how you read, preserves the sender's meaning exactly, and adds nothing the sender did not say.

It is not a summarizer. A summary decides what to drop. decode drops nothing: it carries every claim, the force behind it, the emphasis, and the emotion, and changes only the packaging (wording, register, length, layout). The make-or-break promise is fidelity. No hallucination, no added information, no lost meaning. The anti-telephone guarantee.

## How it works, in one pass

1. Detect the subject domain and apply your calibrated reading level (or ask, if the domain is new).
2. Extract a Seed: a structured capture of the input's meaning, with every preserved element traced back to a span in the source.
3. Transform the Seed to fit you, moving only what is safe to move.
4. Back-translate the output and verify the Seed survived. If a piece will not survive, hand it back in the sender's own words rather than ship a distortion.
5. Present it: a clean body in the sender's voice, with anything the skill added pulled out into a numbered trailer (definitions, flagged gaps, attributed tone reads).

The full operating spec is in [SKILL.md](../../skills/decode/SKILL.md) and the [references/](../../skills/decode/references/) files. The design decisions and their rationale are in [adr/](adr/), the domain language is in [CONTEXT.md](CONTEXT.md), and the research base is in [research/](research/).

## Why it is built the way it is

decode makes several unusual design choices. Each one traces to evidence about how human communication and comprehension actually work. The evidence base was assembled through a multi-source, adversarially-verified research process; the load-bearing findings are below with their primary sources.

### It never asks you to pick a personality type or rate your level

The obvious design (a setup wizard that asks "are you a visual learner?" or "rate your expertise 1 to 5") is the one the evidence most clearly rejects.

- **Learning styles do not work.** Matching instruction to a learner's preferred modality (visual, auditory, kinesthetic) has no rigorous support. Pashler et al. found the experimental design needed to validate matching was "virtually absent" from the literature ([Psychological Science in the Public Interest, 2009](https://journals.sagepub.com/doi/full/10.1111/j.1539-6053.2009.01038.x)). A 2024 meta-analysis of 21 studies found the effect "too small and too infrequent to warrant widespread adoption" ([Frontiers in Psychology, 2024](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2024.1428732/full)), and a 2025 synthesis put matching-specific effects at a negligible d=0.04 ([Educational Psychology Review, 2025](https://link.springer.com/article/10.1007/s10648-025-10002-w)).
- **Personality typologies fail their own validity tests.** MBTI fails all three standard scientific theory criteria and shows no discrete type structure in score data; preferences are continuous, not categorical (Stein & Swan, [Social and Personality Psychology Compass, 2019](https://swanpsych.com/publications/SteinSwanMBTITheory_2019.pdf); Arnau et al., Personality and Individual Differences, 2003). The Hofstede VSM 2013 instrument has near-zero internal consistency for individualism and negative consistency for power distance ([Gerlach & Eriksson, Frontiers in Psychology, 2021](https://pmc.ncbi.nlm.nih.gov/articles/PMC8056018/)).

The common thread across all of these: taking continuous human variation and forcing it into discrete types produces tools that feel rigorous but predict nothing reliably. So decode calibrates on **behavior**, not type. Instead of "what kind of reader are you," it asks "what do you do with this material: explain it, act on it, or are you still working through it." A task posture, not a trait.

### It floors you at novice until you show otherwise

Self-assessment of one's own skill is poorly calibrated and biased upward, and the cognitive-style self-report literature has a known validity ceiling. For decode, the errors are asymmetric: over-estimating your comprehension strips scaffolding you needed (irreversible meaning loss, the exact failure the skill exists to prevent), while under-estimating it merely over-explains (annoying, recoverable). Because over-rating is the fatal direction and self-report biases that way, decode treats you as a novice in a domain until positive evidence says otherwise, and raises your level only when you explicitly act on accumulated evidence. It never raises you on a guess.

### It prepares your profile in advance instead of improvising per message

Tailoring a message to a specific audience is cognitively demanding and competes for working memory; under load (a complex topic, time pressure, a high-stakes thread), that tailoring degrades (Navarro, Macnamara, Glucksberg & Conway, Discourse Processes, 2020; with audience-design-under-load mechanisms also documented by Horton & Gerrig, Cognition, 2005). The implication is to do the audience-design work ahead of time and hold it, rather than expect it to happen in the moment. That is why decode persists a calibrated profile: the prepared model carries the load so you do not re-derive your own reading needs on every message.

### It never asks "did I get this right?"

Self-reported alignment is a weak proxy for actual shared understanding. Shared mental models predict team performance at a meaningful level (rho around 0.35; DeChurch & Mesmer-Magnus, [Journal of Applied Psychology, 2010](https://www.semanticscholar.org/paper/The-cognitive-underpinnings-of-effective-teamwork:-DeChurch-Mesmer-Magnus/f5bbfdf33d6fbbbd9f6614894c5151dcaa42623e)), but the companion measurement work found that questionnaire-based "do you feel aligned" operationalizations correlate near zero, and even slightly negative (rho = -0.05), with actual process. So decode never validates a register or a transform by asking whether it felt right. It validates on behavior (you trimmed the scaffolding, so raise the level) and on an independent back-translation check, not on a feeling of alignment.

### It makes the boundary between sender and skill visible

Because the one thing decode must never do is blur its own contribution into the sender's voice, every output keeps them in separate zones: the body is the sender's words, and anything the skill added (a definition, a flagged gap, a read on the sender's tone) is pulled into a numbered trailer and attributed. When the skill reads emotion from surface cues rather than a stated feeling, it says "the phrasing reads as frustrated," never "the sender is frustrated." When a piece of meaning will not survive a transform, the skill hands that span back in the sender's own words rather than ship a smooth distortion.

## What it does not do (v1)

- **No cross-modality generation.** It will not turn text into a diagram or an image. Those representations assert structure (layout, adjacency, visual detail) the source never specified, which is where meaning loss concentrates. Same-modality work only: reword, re-register, reorder, and prose-to-list or prose-to-table.
- **No outbound use.** v1 adapts content you received to your own profile (you are the reader). Using it to pre-adapt a message for someone else is a separate, harder problem (modeling another person's mind) and is deferred.
- **No summarizing, no advice, no "what they really meant."** It translates what was said. It does not generate what was not.

## A note on the evidence

The research base behind these choices is recorded in full, including the claims that did *not* survive verification, in [research/](research/). Several widely-cited communication findings were killed in adversarial review for overclaiming relative to their primary sources; they are preserved there so the same mistakes do not get repeated. Effect sizes and qualifiers in this README are stated as the primary sources report them. Where a finding is group-level (personality and cultural patterns), it is not used to type any individual, by design.
