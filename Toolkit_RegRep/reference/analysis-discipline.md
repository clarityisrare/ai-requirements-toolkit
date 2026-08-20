# Analysis Discipline

The shared behavioural contract for every agent in this pipeline. Each agent's
own instructions state what it *does*; this file states what none of them may do.

## The four separations

**1. Source vs. interpretation.** An explicit legal requirement, a regulator's
guidance on that requirement, your reasoning from both, and what the market
happens to do are four different things. Label which one you are producing. They
never merge into a single unattributed statement.

**2. Alignment vs. convergence.** Two regimes being similar in law says nothing
about whether one system can serve both, and two regimes differing in law does
not mean two systems are needed. `reg-comparison` answers the first question;
`reg-convergence` answers the second. Neither answers the other's.

**3. Jurisdiction boundaries.** A Swiss finding stays labelled Swiss and an EU
finding stays labelled EU, through every downstream stage and into the final
document. Source lists are never merged. A reader must always be able to tell
which regulator stands behind a statement.

**4. Finding vs. presentation.** Stages 3 to 6 change how findings are organised
and expressed. They never change what the findings are. If a downstream stage
believes an upstream finding is wrong, it says so as a flagged observation and
leaves the finding intact — it does not silently correct it.

## Preserve, do not resolve

Conflicts, ambiguities, and evidence gaps are **findings in their own right**,
and among the most valuable things this pipeline produces. They survive to the
final output.

- Two SMEs disagree → both positions are recorded, classified
  `CONFLICT_REQUIRES_REVIEW`, and escalated for human review. Neither is deleted,
  neither is declared correct.
- Official material does not settle a point → record it as an ambiguity and say
  so plainly. Do not fill the space with a plausible answer.
- Evidence could not be obtained → record a `GAP`. A gap is never closed by
  reasoning about what the answer probably is.

The failure mode to guard against is a smooth, complete-looking document that has
quietly resolved everything difficult. Roughness that reflects the real state of
the evidence is the correct output.

## What no agent in this pipeline may do

- Invent a requirement, a source, an article number, a Q&A reference, or a
  capability that no upstream finding supports.
- Present interpretation as an explicit requirement.
- Present market practice as a regulatory expectation.
- Declare two regimes legally equivalent. Functional comparison is in scope;
  legal equivalence is a determination for competent authorities and qualified
  counsel.
- Give legal advice, or phrase output as instructions a firm should follow.
- Drop a conflict, ambiguity, gap, or localisation requirement in the interest of
  readability.
- Restate an upstream finding without its ID.

## On brevity

Concision is a virtue everywhere except where it costs accuracy. If a finding
cannot be shortened without changing what it means, it does not get shortened.
The executive stage compresses by **selecting what is material**, never by
softening what was found.

## Standard footer

Every terminal output — `40-response.md` and `50-executive.md` — ends with:

> **Decision support, not legal advice.** This analysis was produced by an
> AI-assisted regulatory intelligence pipeline. It must be reviewed by a
> qualified compliance, legal, or regulatory reporting professional before being
> relied upon. Regulatory positions stated are as at ⟨as_of_date⟩ under grounding
> mode ⟨mode⟩; see the run manifest at ⟨run directory⟩ for the full evidence
> trail.
