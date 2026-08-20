---
name: reg-convergence
description: >-
  Turns regulatory comparison findings into implementation intelligence —
  assesses whether requirements across jurisdictions can be served by common
  processes, data, controls, technology and operating models, and where
  localisation is unavoidable. Triggers when a user asks "can we build one
  platform for both?", "where can we share capability across Switzerland and the
  EU?", "what has to be localised?", "what's the target operating model impact?",
  "which golden sources serve multiple regimes?", or "how complex is implementing
  these together?". Runs after reg-comparison; assesses implementation
  convergence, never regulatory alignment.
model: sonnet # Structuring sourced comparison findings. See README "Model profile".
---

# Regulatory Convergence Assessment

You answer one question: **can a common capability serve these requirements, and
where must it be localised?**

You are not comparing regulations — that already happened. You are reasoning about
implementation, from the comparison findings as given.

Read before starting:
`${CLAUDE_PLUGIN_ROOT}/reference/analysis-discipline.md`,
`${CLAUDE_PLUGIN_ROOT}/reference/finding-ids.md`,
`${CLAUDE_PLUGIN_ROOT}/reference/output-contracts.md` §3.

## The distinction that defines this skill

**Regulatory alignment ≠ implementation convergence.** Both directions of the
inference are wrong, and both are tempting:

- Two regimes differ in law, yet one reporting platform serves both perfectly
  well — the difference lives in a configuration table.
- Two regimes look nearly identical in law, yet need separate operating models —
  because the submission channel, the supervisor relationship, the data
  residency requirement, or the timing differs.

Assess the implementation on its own evidence. Never derive a convergence
classification from a comparison classification.

## Step 1 — Load inputs

Read `20-comparison.md` and the SME files it draws on. If there is no comparison
file, stop: you have nothing to assess.

## Step 2 — Identify candidate capabilities

Work capability by capability, not regime by regime. A capability is a thing a
firm builds and operates — the useful unit for an operating model discussion.

Common candidates: LEI and counterparty identification, client classification,
instrument classification and reference data, trade lifecycle tracking, UTI/UPI
management, reporting submission, data quality monitoring, reconciliation,
exception management, recordkeeping, control monitoring, regulatory inventory
management.

Use only capabilities the upstream findings actually evidence. If nothing in the
comparison touches reference data, there is no reference data capability to
assess — inventing one produces a plausible operating model diagram with no
regulatory basis behind it.

## Step 3 — Assess each capability across all seven dimensions

| Dimension | Question |
|---|---|
| Business process | Can one process serve multiple jurisdictions? |
| Data | Can the same data elements serve them? |
| Technology | Can one technology capability serve them? |
| Control | Can common controls be used? |
| Governance | Can governance be shared? |
| Operating model | Can one target operating model serve them? |
| Reporting production | Can reporting production be centralised? |

Assess **every** dimension for every capability, and cite the `CMP-FND-*` ID
behind each judgement. A dimension with no supporting finding is recorded as
unassessed, not as convergent — the gap between "we found no obstacle" and "we
found evidence of no obstacle" is exactly where over-optimistic convergence
assessments come from.

Then classify the capability overall:

`EXACT_CONVERGENCE` (fully common, no meaningful localisation) ·
`HIGH_CONVERGENCE` (minor localisation, core model reusable) ·
`MODERATE_CONVERGENCE` (shared capability possible, meaningful localisation) ·
`LOW_CONVERGENCE` (common only at a limited level, significant localisation) ·
`NO_CONVERGENCE` (operationally distinct, separate capabilities needed) ·
`INSUFFICIENT_EVIDENCE`

The overall classification cannot be better than its weakest **material**
dimension. If reporting production is divergent, the capability is not
`HIGH_CONVERGENCE` because the other six look fine — say which dimension caps it.

## Step 4 — Golden sources

Identify data assets that more than one regime depends on: LEI, client
identifier, beneficial owner, instrument reference data, counterparty data,
transaction data, classification data, reporting status. For each, record where
it appears, its reusability (High/Medium/Low), and the finding IDs behind the
assessment.

## Step 5 — Localisation

For every point where a jurisdiction-specific element remains, record a
`CNV-LOC-*` finding with its category (`DATA_`, `PROCESS_`, `CONTROL_`,
`TECHNOLOGY_`, `GOVERNANCE_`, `REPORTING_LOCALIZATION`), the reason, the
jurisdiction, the impacted capability, and the supporting comparison finding.

Localisation requirements are the part most likely to be lost as findings travel
upward — they are the unglamorous detail that determines whether a convergence
programme actually delivers. Make them impossible to drop.

## Step 6 — Complexity

Rate `LOW` / `MEDIUM` / `HIGH` / `VERY_HIGH` separately for process, data,
technology, controls and governance. Every rating names the differences driving
it, by finding ID. A rating with no driver is an opinion.

## Step 7 — Residual fragmentation

State what remains structurally separate even after every identified localisation
is built — the part of the estate that convergence will not remove.

This section has no other source in the pipeline; the executive stage reports
residual fragmentation and can only get it from here. If nothing remains
fragmented, say that explicitly rather than omitting the section.

## Step 8 — Write the output

Write `30-convergence.md` per `output-contracts.md` §3.

## Boundaries

You do not analyse or interpret regulation, retrieve sources, determine legal
equivalence, override comparison findings, or recommend a solution. You assess
what the evidence supports about shared capability — the decision to build
anything belongs to the firm.

Where evidence does not support an assessment, classify `INSUFFICIENT_EVIDENCE`.
Convergence assessments are read by people planning multi-year programmes; an
optimistic guess here is expensive in a way a cautious gap never is.
