---
stage: sme
agent: <sme-agent-name>
domain: <EMIR | MIFIR | MIFID2 | FMIA39 | FMIA104 | FINSA>
jurisdiction: <European Union | Switzerland>
as_of: <YYYY-MM-DD>
grounding_mode: <1 | 2 | 3>
regime_version: <regime and amendments analysed>
pending_changes: <known upcoming changes with timing, or "none identified">
---

# SME Finding — <Domain>

## Question Understanding

<The regulatory issue, scoped. State explicitly anything in the request this
agent is not answering and why.>

## Relevant Regulatory Provisions

- <Provision, pinpoint> [TAG] <source>

## Explicitly Supported Requirements

**<DOMAIN>-REQ-001** · `CORE_TYPE / QUALIFIER` · Evidence: STRONG
<The requirement.>
Source: <pinpoint citation> [TAG] <url or corpus path>

## Supervisory Guidance

**<DOMAIN>-REQ-001** is qualified by <guidance, pinpoint> [TAG]
<What the regulator has said about how the requirement applies.>

## Operational Implications

<Systems, processes, controls, governance, reporting architecture, data
management. Facts about this regime only — no assessment of shareability.>

## Interpretations

**<DOMAIN>-INT-001** · Evidence: MODERATE
<The reasoning, what it rests on, and why it is interpretation rather than an
explicit requirement.>

## Ambiguities / Open Questions

**<DOMAIN>-AMB-001**
<What is unclear, and why the official material does not settle it.>

## Implementation Risks

**<DOMAIN>-RSK-001** · attaches to `<DOMAIN>-REQ-00n`
<What can go wrong and why.>

## Evidence Gaps

**<DOMAIN>-GAP-001**
<What could not be established, and what would close it.>

## Official Sources

**Tier 1 — Legal text**
- <source> [TAG] <url> · retrieved <date>

**Tier 2 — Regulator guidance**
- <source> [TAG] <url> · retrieved <date>

**Tier 5 — Secondary** (only where no official source exists)
- <source> [SECONDARY] <url>

## Agent Notes

<Context for downstream stages — especially anything the comparison stage should
be careful about when pairing these findings.>
