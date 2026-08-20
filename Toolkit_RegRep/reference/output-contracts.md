# Output Contracts

Each stage writes one file, in one shape. Downstream stages parse these, so the
headings are fixed. Templates for each live in `templates/`.

Every file opens with YAML frontmatter. Machine-readable metadata at the top,
analysis below.

---

## 1. SME finding file — `10-sme-<domain>.md`

```markdown
---
stage: sme
agent: sme-emir
domain: EMIR
jurisdiction: European Union
as_of: 2026-08-19
grounding_mode: 1
regime_version: EMIR as amended by REFIT (Reg. (EU) 2019/834)
pending_changes: none identified
---

# SME Finding — EMIR

## Question Understanding
What was asked, in regulatory terms, and how it was scoped. Name explicitly
anything in the question this agent is *not* answering.

## Relevant Regulatory Provisions
Pinpoint list. Every entry carries a citation tag.

## Explicitly Supported Requirements
One block per requirement:

**EMIR-REQ-001** · `REPORTING_PARTY` · Evidence: STRONG
Statement of the requirement.
Source: EMIR Art. 9(1) [RETRIEVED 2026-08-19] <url>

## Supervisory Guidance
Tier 2 material bearing on the above, each tied to the REQ it qualifies.

## Operational Implications
Impacts on systems, processes, controls, governance, data. Facts only — no
evaluation of whether they can be shared with another jurisdiction.

## Interpretations
**EMIR-INT-001** · Evidence: MODERATE
The reasoning, and what it rests on. Explicitly flagged as interpretation.

## Ambiguities / Open Questions
**EMIR-AMB-001** — what is unclear and why the official material does not settle it.

## Implementation Risks
**EMIR-RSK-001** · what could go wrong, and which requirement it attaches to.

## Evidence Gaps
**EMIR-GAP-001** — what could not be established, and what would close it.

## Official Sources
Grouped by tier, each with citation tag and retrieval date.

## Agent Notes
Context useful downstream — including anything a comparison agent should be
careful about when pairing these findings.
```

---

## 2. Comparison file — `20-comparison.md`

The originating Copilot agent had no output format at all, despite three
downstream consumers. This is that contract.

```markdown
---
stage: comparison
domains: [EMIR, FMIA104]
jurisdictions: [European Union, Switzerland]
sme_inputs: [10-sme-emir.md, 10-sme-fmia-art-104.md]
as_of: 2026-08-19
---

# Comparison Findings

## Comparison Scope
Which domains were compared, on which question, and — importantly — what was
*not* compared and why.

## Findings Summary

| ID | Core type | EU side | Swiss side | Classification | Evidence |
|---|---|---|---|---|---|
| CMP-FND-001 | REPORTING_PARTY | EMIR-REQ-001 | FMIA104-REQ-002 | CONFIRMED_DIFFERENCE | STRONG |
| CMP-FND-002 | REPORTABLE_EVENT | EMIR-REQ-004 | {FMIA104-REQ-006, FMIA104-REQ-007} | PARTIAL_ALIGNMENT | MODERATE |

## Detailed Findings

**CMP-FND-001** · `REPORTING_PARTY` · CONFIRMED_DIFFERENCE · Evidence: STRONG

- **European Union** (`EMIR-REQ-001`): the position, in the SME's terms.
- **Switzerland** (`FMIA104-REQ-002`): the position, in the SME's terms.
- **Basis of classification**: why this classification and not an adjacent one.
- **What this does not say**: the limit of the finding.

## Concepts Without Counterparts
Each `NO_EXACT_EQUIVALENT`: the concept, the regime that has it, the regimes
searched, and what was checked before concluding there is no counterpart.

## Conflicts Requiring Review
Each `CONFLICT_REQUIRES_REVIEW`: both positions in full, the nature of the
incompatibility, and what a reviewer would need to resolve it. **Not resolved
here.**

## Evidence Gaps
`CMP-GAP-*`: comparisons that could not be made, and what was missing.

## Consistency Observations
Problems in the SME inputs themselves: inconsistent classification, interpretation
presented as fact, jurisdiction bleed, ambiguous sourcing. Described, not fixed.

## Convergence Escalation Flags
Findings worth a convergence assessment, with the trigger named — a shared
objective, a shared data dependency, a common control theme. **A flag is not a
convergence assessment.**
```

**Classifications** — exactly one per finding:
`CONFIRMED_ALIGNMENT` · `PARTIAL_ALIGNMENT` · `CONFIRMED_DIFFERENCE` ·
`INTERPRETED_DIFFERENCE` · `NO_EXACT_EQUIVALENT` · `INSUFFICIENT_EVIDENCE` ·
`CONFLICT_REQUIRES_REVIEW`

---

## 3. Convergence file — `30-convergence.md`

```markdown
---
stage: convergence
comparison_input: 20-comparison.md
jurisdictions: [European Union, Switzerland]
as_of: 2026-08-19
---

# Convergence Assessment

## Convergence Scope
What was assessed, from which comparison findings.

## Capability Assessments

**CNV-CAP-001 — Counterparty Identification (LEI)**

- Regulatory objective: what both regimes are trying to achieve here.
- Participating jurisdictions: EU, CH
- Supporting comparison findings: `CMP-FND-003`, `CMP-FND-004`
- Classification: `HIGH_CONVERGENCE`
- Dimension assessment:

| Dimension | Assessment | Basis |
|---|---|---|
| Business process | Convergent | `CMP-FND-003` |
| Data | Convergent | `CMP-FND-003` |
| Technology | Convergent | — |
| Control | Partially convergent | `CMP-FND-004` |
| Governance | Convergent | — |
| Operating model | Convergent | — |
| Reporting production | Divergent | `CMP-FND-005` |

- Rationale: evidence-based reasoning referencing the IDs above.
- Localisation required: `CNV-LOC-002`

## Golden Source Candidates

| Candidate | Appears in | Reusability | Basis |
|---|---|---|---|
| LEI | EMIR, FMIA104, MiFIR | High | `CMP-FND-003` |

## Localisation Requirements

**CNV-LOC-002** · `CONTROL_LOCALIZATION` · Switzerland
- Reason, impacted capability (`CNV-CAP-001`), supporting finding (`CMP-FND-004`).

## Implementation Complexity

| Area | Rating | Drivers |
|---|---|---|
| Process | MEDIUM | `CMP-FND-002` |
| Data | LOW | `CMP-FND-003` |
| Technology | MEDIUM | `CMP-FND-005` |
| Controls | HIGH | `CMP-FND-004`, `CMP-FND-006` |
| Governance | LOW | — |

## Residual Fragmentation
What cannot be converged even after localisation, and why. Named explicitly —
this is what the executive stage reports as residual fragmentation, and it has no
other source.

## Evidence Gaps
`CNV-GAP-*`: what could not be assessed.
```

**Convergence classifications:** `EXACT_CONVERGENCE` · `HIGH_CONVERGENCE` ·
`MODERATE_CONVERGENCE` · `LOW_CONVERGENCE` · `NO_CONVERGENCE` ·
`INSUFFICIENT_EVIDENCE`

**Localisation categories:** `DATA_LOCALIZATION` · `PROCESS_LOCALIZATION` ·
`CONTROL_LOCALIZATION` · `TECHNOLOGY_LOCALIZATION` · `GOVERNANCE_LOCALIZATION` ·
`REPORTING_LOCALIZATION`

**Complexity ratings:** `LOW` · `MEDIUM` · `HIGH` · `VERY_HIGH`

---

## 4. Business response — `40-response.md`

Structure is chosen by question type; see `skills/reg-output-quality/SKILL.md`.
Every variant ends with a Confidence Assessment, a Sources section split by
jurisdiction, a Traceability appendix, and the standard footer from
`analysis-discipline.md`.

## 5. Executive brief — `50-executive.md`

One page of substance, then appendices. See
`skills/reg-executive-output/SKILL.md`.
