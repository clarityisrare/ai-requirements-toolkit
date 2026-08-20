# The Regulatory Intelligence Pipeline

Six stages. Each stage has exactly one job and is forbidden from doing the next
stage's job. That separation is the whole point: it is what stops a formatting
layer from quietly inventing a legal conclusion.

```
                    reg-orchestrator          (routing, sequencing, completeness)
                            │
    ┌──────────┬──────────┼──────────┬──────────────┬──────────────┐
    ▼          ▼          ▼          ▼              ▼              ▼
sme-fmia-  sme-fmia-    sme-     sme-mifir-    sme-mifid2-     sme-finsa-
 art-39     art-104     emir     transaction-    client-         client-
                                   reporting   classification  segmentation
    └──────────┴──────────┬──────────┴──────────────┴──────────────┘
                            ▼
                    reg-comparison            (alignment / difference / conflict)
                            ▼
                    reg-convergence           (can one capability serve both?)
                            ▼
                 reg-output-quality           (business-consumable + QA + confidence)
                            ▼
                reg-executive-output          (decision-support for leadership)
```

## Why SMEs are subagents and the rest are skills

The six SME agents run as **subagents**, each in its own context window. This is
not a performance choice — it is a correctness control. An SME that cannot see
another jurisdiction's analysis cannot unconsciously import it, which is the
failure mode the whole architecture exists to prevent. It also lets all six run
**in parallel**.

The four downstream stages run as **skills** in the main context, reading the
artifacts the SMEs wrote to disk. They need to see everything upstream by
definition, so isolating them would only lose fidelity.

## The run directory

Every run writes to a dated directory under `.reg-analysis/` in the working
project. Nothing is passed agent-to-agent in memory; everything goes through
files. That is what makes a run auditable, resumable, and reviewable by a human
months later.

```
.reg-analysis/2026-08-19-1432-emir-vs-fmia104-scope/
  manifest.md            run metadata: request, mode, as-of date, stages run
  00-request.md          the question as classified by the orchestrator
  00-plan.md             routing decision + which stages will run and why
  10-sme-emir.md         SME finding files (one per SME engaged)
  10-sme-fmia-art-104.md
  20-comparison.md
  30-convergence.md
  40-response.md         the business-consumable answer
  50-executive.md        the executive brief (only if requested)
```

Stage number prefixes make the sequence obvious in a file listing and let a
reviewer see immediately which stages were skipped.

## Dependency rules

A stage must not run until its inputs exist. If they do not, stop and say so —
do not synthesise the missing input.

| Stage | Requires |
|---|---|
| `reg-comparison` | at least **two** SME finding files covering different regulatory domains |
| `reg-convergence` | a completed `20-comparison.md` |
| `reg-output-quality` | at least one SME finding file, plus any comparison/convergence files that were produced |
| `reg-executive-output` | a completed `40-response.md` |

A single-regulation question legitimately skips comparison and convergence. That
is not an incomplete run; record it in the manifest as `SKIPPED — single domain`.

## Execution economy

- Never engage an SME whose domain the question does not touch.
- Never run comparison for a single-domain question.
- Never run convergence unless the question concerns implementation, operating
  model, localisation, shared capability, or platform strategy.
- Never run the executive stage unless an executive audience was asked for.

Each unnecessary stage costs real money and adds a layer that can distort
findings. Restraint is a feature.

## Human accountability

Every artifact this pipeline produces is **decision support, not legal advice**.
The final call belongs to a qualified compliance, legal, or regulatory reporting
professional. Each terminal output carries that statement — see
`output-contracts.md`.
