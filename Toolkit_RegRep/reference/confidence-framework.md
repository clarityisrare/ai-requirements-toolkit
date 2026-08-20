# Confidence Framework

Confidence is assessed once, by `reg-output-quality`, and **inherited** by
`reg-executive-output`. It is never recomputed downstream — two different
confidence figures for the same finding destroys the credibility of both.

Upstream stages do not assign confidence. SMEs and `reg-comparison` assign
**evidence strength**, which is an input to confidence, not the same thing.

## Evidence strength (assigned by SMEs and reg-comparison)

| Value | Meaning |
|---|---|
| `STRONG` | Rests on Tier 1 or Tier 2 sources, cited pinpoint, with no material interpretation in the chain |
| `MODERATE` | Part explicit source, part interpretation; or the source is Tier 3/4; or the source is clear but its application to this fact pattern is not |
| `WEAK` | Chiefly interpretation, incomplete evidence, `[UNVERIFIED]` citations, or a `GAP` in the reasoning chain |

## Confidence dimensions (assigned by reg-output-quality)

Each takes `HIGH`, `MEDIUM`, or `LOW`, and each carries a one-line rationale.
Mark a dimension `N/A` when that stage did not run — do not score a stage that
produced nothing.

| Dimension | Question |
|---|---|
| **Regulatory confidence** | How well is the regulatory position supported by official sources? |
| **Comparison confidence** | How well supported are the alignment / difference conclusions? |
| **Convergence confidence** | How well supported are the convergence and localisation findings? |
| **Overall confidence** | How much weight can a decision maker put on this response? |

## Deriving each dimension

| Level | Criteria |
|---|---|
| `HIGH` | Predominantly `STRONG` evidence; no `CONFLICT_REQUIRES_REVIEW`; no `GAP` on a point material to the answer; grounding mode produced verifiable citations |
| `MEDIUM` | Meaningful interpretation in the chain, or `MODERATE` evidence on material points, or non-material gaps, or `[UNVERIFIED]` citations on secondary points |
| `LOW` | Material `GAP`s, an unresolved `CONFLICT_REQUIRES_REVIEW`, mostly `WEAK` evidence, or `INSUFFICIENT_EVIDENCE` on the central question |

## Deriving overall confidence — the rule

**Overall confidence is the lowest of the applicable dimensions.** No averaging,
no rounding up.

Departing upward from that floor is permitted in exactly one case, and must be
stated: the weak dimension is **immaterial to the question actually asked** — for
example, convergence confidence is `LOW` on a question whose answer does not
depend on convergence. Write the departure out:

> Overall: MEDIUM. Convergence confidence is LOW, but the question asked whether
> the transaction is reportable, which the regulatory finding (HIGH) answers
> without reference to the convergence assessment.

Never depart downward without saying which dimension drove it.

## Presentation

```markdown
## Confidence Assessment

| Dimension | Level | Rationale |
|---|---|---|
| Regulatory | HIGH | Both positions rest on Tier 1 text, cited pinpoint (`EMIR-REQ-001`, `FMIA104-REQ-002`) |
| Comparison | HIGH | The structural difference is visible in the legal text on both sides (`CMP-FND-001`) |
| Convergence | MEDIUM | Capability assessment rests partly on interpretation of operational implications (`CNV-CAP-002`) |
| **Overall** | **MEDIUM** | Floored by convergence confidence, which is material here because the question asked about a shared platform |
```

Always give the rationale. A confidence label with no reasoning is decoration.
