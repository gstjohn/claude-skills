# Stakes: user owns the baseline, inference only raises it

## Context

Capacity valuation (ADR-0002) lets stakes override a high capacity setting downward, so a run needs a stakes value. Stakes do not behave like capacity. For capacity the safe default (novice) is also the common case, so flooring low is free. For stakes the safe default is high (less transformation, more fidelity), but flooring at high makes the skill never transform anything and therefore useless. Safety and utility pull opposite ways, so the floor cannot be a constant.

## Decision

**The user sets the stakes baseline at setup** (config default, with per-run override), expressing their own risk appetite. **Inference can only raise a run's stakes above that baseline, never lower it:** commitment language, figures, deadlines, named obligations, directives, and legal/financial/irreversible content bump the run toward high-stakes, and uncertainty resolves *higher*. **Only an explicit human signal can drop a run below the baseline,** because lowering stakes means a more aggressive transform (the soul-loss direction), which never happens automatically.

## Consequences

- Every automatic move the skill makes is toward more fidelity, never less. The human owns any move toward more aggressive transformation.
- High stakes pushes toward more scaffolding regardless of capacity, consistent with ADR-0002's override rule.
- The skill needs lightweight content classifiers for the raising signals; missing one under-protects, so they are tuned to over-detect.
