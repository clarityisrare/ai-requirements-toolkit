# Regulatory Reporting Intelligence Toolkit

A multi-agent pipeline for Swiss and EU regulatory reporting questions. Six
jurisdiction-isolated subject matter experts analyse their own regime and nothing
else; four downstream stages compare, assess convergence, quality-check and
communicate — without any of them being allowed to invent, resolve, or quietly
smooth over what the specialists found.

> 🤖 **Using Claude Code?** Install the whole toolkit as a **plugin**:
>
> ```
> /plugin marketplace add clarityisrare/ai-requirements-toolkit
> /plugin install reg-reporting-toolkit@ai-requirements-toolkit
> ```

> ⚠️ **Using Codex?** The five pipeline skills install the same way:
>
> ```
> /plugin marketplace add clarityisrare/ai-requirements-toolkit
> /plugin install reg-reporting-toolkit
> /reload-plugins
> ```
>
> **With two material limitations.** The first: a Codex plugin can package
> skills, MCP servers and app connectors — not subagents. The six SME agents in
> [`agents/`](./agents) therefore do not install, and the orchestrator has
> nothing to dispatch to: the SME analysis runs inline, in one shared context.
> That removes the jurisdiction isolation this design rests on, so findings from
> one regime can bleed into another. Everything downstream — the comparison,
> convergence, quality and executive stages — still works as written. On Codex,
> treat the SME layer as unisolated and check the jurisdiction attribution on
> every finding yourself.
>
> The second: Codex chooses a model per session, not per skill, so the per-stage
> model pinning described under
> [Model profile](#model-profile--which-model-runs-each-agent-claude-code) has no
> effect — set your session to the strongest model available for the whole run.
>
> Claude Code is the supported surface for the full architecture.

> Companion to [Clarity Is Rare](https://www.clarityisrare.com). Use freely, adapt
> to your context, and keep a human accountable for the final decision.

> 📌 **Before relying on any output, read
> [Scope, limits and disclaimer](#scope-limits-and-disclaimer).** This toolkit
> covers six Swiss and EU regimes and nothing else, produces decision support
> rather than advice, and comes with no warranty of any kind.

---

## The problem it solves

Ask a general-purpose assistant whether a swap is reportable under EMIR or FinfraG
and you get a fluent answer with no way to tell which parts are the legal text,
which are the regulator's guidance, which are the model's inference, and which
are simply wrong. Ask it to compare two regimes and it will find similarities,
because that is what "compare" invites — even where the regimes are structurally
different.

This toolkit makes those distinctions structural rather than aspirational:

- **Jurisdiction isolation.** Each SME runs in its own context window. The EMIR
  expert cannot see the FinfraG analysis, so it cannot unconsciously import it.
- **Pinpoint citation, tagged by origin.** Every requirement names its article
  and paragraph, tagged `[CORPUS]`, `[RETRIEVED <date>]`, `[SECONDARY]` or
  `[UNVERIFIED]`. You can always tell how a citation was obtained.
- **Stable finding IDs.** `EMIR-REQ-003`, `CMP-FND-007`, `CNV-LOC-002`. Every
  downstream statement names the upstream ID behind it. Anything unattributable
  is removed before delivery.
- **Conflicts and gaps survive.** Disagreements between regimes and holes in the
  evidence are findings, not defects to be tidied away. They reach the executive
  summary intact.
- **An audit trail on disk.** Every run writes a dated directory of artifacts a
  reviewer can walk months later.

## Covered regimes

| Agent | Regime |
|---|---|
| `sme-fmia-art-39` | FinfraG / FMIA Art. 39 — Swiss trading venue transaction reporting |
| `sme-fmia-art-104` | FinfraG / FMIA Art. 104 — Swiss derivatives reporting to a trade repository |
| `sme-emir` | EMIR + REFIT — EU derivatives reporting, clearing, risk mitigation |
| `sme-mifir-transaction-reporting` | MiFIR Art. 26, RTS 22/23/24 — EU transaction reporting |
| `sme-mifid2-client-classification` | MiFID II — EU client classification and investor protection |
| `sme-finsa-client-segmentation` | FinSA / FIDLEG Art. 4 — Swiss client segmentation and conduct duties |

**Counterpart pairs:** FMIA Art. 39 ↔ MiFIR Art. 26 · FMIA Art. 104 ↔ EMIR Art. 9 ·
FinSA Art. 4 ↔ MiFID II client classification. The last is structurally
asymmetric — three Swiss segments against four EU categories, on tests that
differ in kind — so a matching label on either side is a thing to check rather
than to accept. See
[`reference/regulatory-map.md`](./reference/regulatory-map.md).

Out of scope: **FinIA/FINIG**, **AMLA/GwG**, SFTR, CSDR, Dodd-Frank, UK
EMIR/MiFIR, APAC regimes, AnaCredit, MMSR, Basel/CRR, and the Swiss Banking Act.
The orchestrator names the gap rather than routing to the nearest-looking expert.
See [Scope, limits and disclaimer](#scope-limits-and-disclaimer).

## The pipeline

```
reg-orchestrator ──┬─ sme-fmia-art-39  ─┐
                   ├─ sme-fmia-art-104  │
                   ├─ sme-emir          ├─→ reg-comparison ─→ reg-convergence
                   ├─ sme-mifir-tr      │        ↓                  ↓
                   ├─ sme-mifid2-cc     │   reg-output-quality ─→ reg-executive-output
                   └─ sme-finsa-cs     ─┘
```

SMEs run **in parallel**; downstream stages run in sequence, each gated on its
inputs actually existing. Stages that are not needed are not run — a
single-regulation question runs one SME and the output stage.

See [`examples/worked-example.md`](./examples/worked-example.md) for a full run, and
[`examples/Example Reg Reporting.pdf`](./examples/Example%20Reg%20Reporting.pdf) for a
second, real end-to-end run captured as a PDF.

## Quick start

```
Compare the reporting obligation under EMIR and FinfraG Art. 104 for an OTC
interest rate swap between a Swiss bank and an EU non-financial counterparty
below the clearing threshold, and tell me whether one platform can serve both.
```

The orchestrator will ask for any decisive fact you left out, tell you which
agents it is about to run, and write everything to
`.reg-analysis/<date>-<slug>/`.

---

## Configuration

### Grounding mode — how citations are obtained

This is the single biggest determinant of how much the output is worth. Set it in
`.reg-analysis/config.md` (copy from [`templates/config.md`](./templates/config.md)):

```yaml
grounding_mode: 1        # 1 = hybrid | 2 = live-web | 3 = corpus-only
corpus_path: ./corpus
as_of_date: 2026-08-19
```

| Mode | Behaviour | Best for |
|---|---|---|
| **1 — Hybrid** *(default)* | Local corpus first, official web fallback, anything left tagged `[UNVERIFIED]` with an evidence gap | Most work. Fast and deterministic where the corpus covers the ground, current where it does not |
| **2 — Live web** | Every citation retrieved during the run from official domains; failed retrieval becomes a gap, never a recollection | When currency matters most — a live rule change, a new ESMA Q&A |
| **3 — Corpus only** | Strictly offline; anything outside the corpus is a gap, including things the model is confident it knows | Audit-sensitive, reproducible runs — same question, same corpus, same evidence base |

The mode in force is recorded in every run manifest and in the footer of every
output, so a reader can always tell how the citations were obtained. Full
specification in [`reference/grounding-modes.md`](./reference/grounding-modes.md);
corpus setup in [`corpus/README.md`](./corpus/README.md). An empty corpus is fine
— mode 1 degrades gracefully.

### Model profile — which model runs each agent (Claude Code)

The toolkit ships pinned to a **balanced** profile: Opus where a wrong answer is
expensive and subtle, Sonnet where the work is structuring already-sourced
material.

| Agent / stage | Model | Why |
|---|---|---|
| `sme-fmia-art-39` | `opus` | Regulatory analysis with low tolerance for a plausible-sounding error |
| `sme-fmia-art-104` | `opus` | " |
| `sme-emir` | `opus` | " |
| `sme-mifir-transaction-reporting` | `opus` | " |
| `sme-mifid2-client-classification` | `opus` | " |
| `sme-finsa-client-segmentation` | `opus` | " |
| `reg-orchestrator` | `opus` | Routing errors are cheap to make and expensive downstream — a misrouted question wastes the whole run |
| `reg-comparison` | `opus` | False equivalence is the costliest error in the pipeline, and the hardest to spot |
| `reg-convergence` | `sonnet` | Structured reasoning over comparison findings that are already sourced |
| `reg-output-quality` | `sonnet` | Organisation, attribution and checking against a checklist |
| `reg-executive-output` | `sonnet` | Selection and compression over findings that are already settled |

**To change it**, edit the `model:` line in the YAML frontmatter of the file:

- Skills — `skills/<skill-name>/SKILL.md`
- Subagents — `agents/<agent-name>.md`

Valid values are `opus`, `sonnet`, `haiku`, and `inherit` (use the session's
model). Delete the line entirely to make an agent model-agnostic.

Two alternative profiles:

- **Accuracy-first** — set every agent to `opus`. Highest cost; use when the
  output feeds a regulatory submission or a formal position.
- **Cost-optimised** — set everything to `sonnet` except `reg-comparison`.
  Cheapest; accepts more variance in the SME analysis, which is where errors are
  most expensive to inherit.

If you change models, change them at the agent level rather than switching the
session model — the profile is deliberately uneven, and flattening it removes the
protection where it matters most.

#### On Codex, none of the above applies

`model:` is a Claude Code extension. A Codex `SKILL.md` recognises only `name`
and `description`, and Codex selects the model **per session** rather than per
skill — so every value in the table above is inert there, and each stage runs on
whatever model the session happens to be set to.

That matters most for `reg-comparison`. The reason it is pinned to Opus — false
equivalence being the costliest error in the pipeline and the hardest to spot —
does not disappear on Codex; only the enforcement does. Together with the missing
subagents, a Codex run gives you neither jurisdiction isolation nor model
pinning, and nothing in the run will tell you so.

So if you run this on Codex, **set the session to your strongest available model
for the whole run**. You cannot spend capability only where it matters, so the
choice is to spend it everywhere or to get it nowhere.

---

## What is in the box

```
agents/       six SME subagents — isolated context, run in parallel
skills/       the six pipeline stages
reference/    the shared method: pipeline, domain map, taxonomy, finding IDs,
              source governance, grounding modes, confidence, output contracts
templates/    SME finding, executive brief, run manifest, config
checklists/   quality gates for each stage
corpus/       local official texts (modes 1 and 3)
examples/     two end-to-end worked runs (Markdown + PDF)
```

Skills reference the shared method by `${CLAUDE_PLUGIN_ROOT}` rather than each
carrying a copy, so there is one version of the method rather than nine drifting
ones.

## Extending the toolkit

**Adding an SME.** Copy an existing file in `agents/`, change the domain, scope,
domain code and sources, register it in
[`reference/regulatory-map.md`](./reference/regulatory-map.md), and add a routing
row to `skills/reg-orchestrator/SKILL.md`. Nothing else needs to change — the
comparison, convergence and output stages take whatever SME files they find.

Describe the regulator guidance in its domain **by issuer and subject, never by
document number** — "FINMA circulars on rules of conduct", not "FINMA Circular
2025/2". A category keeps working when an instrument is superseded and picks up
publications that did not exist when the file was written; a pinned number goes
silently wrong. Binding legal instruments keep their identifiers. See
[`reference/source-governance.md`](./reference/source-governance.md).

**Both sides of every counterpart pair are now covered.** The next additions
worth making are whole regimes rather than missing halves — SFTR and the UK
regimes (UK EMIR, UK MiFIR) are the ones users ask for most often, and each needs
its own SME plus a row in the domain map and the orchestrator's routing table.

## Scope, limits and disclaimer

**Read this before relying on anything this toolkit produces.**

### What it covers

Swiss and EU regimes only, across six domains: FMIA Art. 39, FMIA Art. 104,
EMIR, MiFIR transaction reporting, MiFID II client classification and conduct,
and FinSA client segmentation and conduct.

It covers cross-border questions between those two jurisdictions. It is not a
general-purpose regulatory tool and has no coverage of any other jurisdiction.

### What it does not cover

Not covered, and not to be inferred from anything the pipeline produces:

- **FinIA / FINIG** (Financial Institutions Act) — licensing, organisational and
  prudential requirements for portfolio managers, trustees, managers of
  collective assets, fund management companies and securities firms.
- **AMLA / GwG** (Anti-Money Laundering Act) and its ordinances — due diligence,
  identification of the beneficial owner for AML purposes, and reporting to MROS.
- SFTR, CSDR, Dodd-Frank / CFTC, UK EMIR, UK MiFIR, APAC reporting regimes,
  AnaCredit, MMSR, Basel / CRR reporting, and the Swiss Banking Act.

Onboarding, identification and client-lifecycle questions in particular often
engage FinIA and AMLA alongside FinSA. This toolkit answers only the part inside
its six domains and says so. **Silence from it is not evidence that nothing else
applies.**

### How to read the output

- **Decision support, not legal advice.** Every output carries that statement.
  The final call belongs to a qualified compliance, legal, or regulatory
  reporting professional.
- **Functional comparison only.** Legal equivalence is a determination for
  competent authorities. The pipeline compares what regimes require and refuses
  to declare them equivalent.
- **The output is only as good as the grounding.** In mode 1, check the
  `[UNVERIFIED]` tags before relying on anything. They are there so you can.
- **Regulation moves.** Every output states its as-of date and flags pending
  changes it knows about. Check the horizon items rather than trusting them.

### It may not be right for your question

This is an analytical aid, not a regulatory determination engine,
and it is least reliable exactly where questions are most detailed: narrow fact
patterns, edge cases, novel products and structures, cross-border arrangements,
national implementing measures, and anything turning on supervisory practice
rather than published text.

Treat every output as a **first draft for a qualified professional to check**,
never as an answer. Apply your own judgement and expertise to all of it, verify
every citation against the source, and confirm the position is current before
acting on it.

### No warranty and no liability

This toolkit is provided free and open source, **as is and without warranty of
any kind**, express or implied, including without limitation any warranty of
merchantability, fitness for a particular purpose, accuracy, completeness,
currency or non-infringement. See [LICENSE](./LICENSE).

Nothing it produces is legal, regulatory, compliance, tax or investment advice,
and use of it creates no advisory, professional or fiduciary relationship of any
kind. The authors and contributors are not acting as your adviser and accept
**no responsibility or liability whatsoever** for any loss, damage, regulatory
finding, penalty, cost or other consequence arising from use of, or reliance on,
this toolkit or its output — whether that output is accurate, inaccurate,
incomplete, or out of date.

**You are solely responsible** for verifying any output before relying on it and
for the decisions you take. Where a question carries real regulatory, financial
or legal consequence, obtain advice from a qualified professional in the relevant
jurisdiction.

## Provenance

Adapted from a ten-agent Microsoft Copilot Studio architecture. The stage
separation and the alignment-versus-convergence distinction are from the original
design. Added
here: jurisdiction isolation through subagents, real source retrieval with three
grounding modes, stable finding IDs and an end-to-end traceability contract, a
unified requirement taxonomy across regimes, an output contract for the
comparison stage (the original had none, despite three consumers), a deterministic
confidence rule, as-of dating, and the corrected FMIA ↔ EMIR / MiFIR counterpart
mapping.

## Licence

MIT — see [LICENSE](./LICENSE).
