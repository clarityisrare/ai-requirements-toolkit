# Source Governance

## Source hierarchy

Cite the highest available tier. Never cite a lower tier where a higher one
answers the question, and never blend tiers in a single statement without saying
which is which.

**Tier 1 — Binding legal text**
Swiss: FinfraG (FMIA), FinfraV (FMIO), FinfraV-FINMA (FMIO-FINMA), FinSA
(FIDLEG, SR 950.1), FinSO (FIDLEV, SR 950.11).
EU: EMIR, MiFIR, MiFID II, and Delegated/Implementing Regulations and Directives
(RTS 22/23/24, Del. Reg. 2017/565, Del. Dir. 2017/593, and equivalents).

**Tier 2 — Regulator guidance with supervisory weight**
FINMA Circulars, FINMA Guidance, FINMA FAQs, FINMA Supervisory Notices.
ESMA Guidelines, ESMA Q&As, ESMA Opinions, ESMA Validation Rules, ESMA Reporting
Instructions, ESMA Data Quality Framework, ESMA Supervisory Briefings.

**Tier 3 — Regulator material without binding force**
Consultation papers, final reports, discussion papers, draft standards, feedback
statements. Useful for direction of travel; never cited as a current obligation.

**Tier 4 — NCA and infrastructure material**
National competent authority guidance, and trading venue / trade repository /
reporting office specifications (SIX, BX, REGIS-TR, DTCC and equivalents). These
bind operationally but are not the legal source of the obligation — say which
role they are playing.

**Tier 5 — Secondary**
Law firm briefings, industry association papers, vendor documentation,
consultancy publications, market practice. Tagged `[SECONDARY]`. Never used where
Tiers 1–4 answer the question. Never treated as evidence of what the regulator
requires — only, at most, as evidence of what the market does.

## Official domains

Retrieval (Modes 1 and 2) is restricted to these:

| Domain | Covers |
|---|---|
| `fedlex.admin.ch` | Swiss federal legislation (FinfraG, FinfraV, FinSA, FinSO) |
| `finma.ch` | FINMA circulars, guidance, supervisory notices |
| `eur-lex.europa.eu` | EU legal texts and delegated acts |
| `esma.europa.eu` | ESMA guidelines, Q&As, RTS, validation rules |
| `six-group.com` | SIX reporting specifications (Tier 4) |
| NCA domains | e.g. `bafin.de`, `amf-france.org`, `fca.org.uk` (Tier 4) |

Anything else is `[SECONDARY]` by definition, whatever it claims about itself.

## Naming guidance sources

An agent describes the guidance in its domain by **issuer and subject**, never by
document number.

"FINMA circulars and guidance on rules of conduct under FinSA/FinSO" resolves to
whatever is in force at the as-of date. "FINMA Circular 2025/2" resolves to
whatever that number meant on the day the agent file was written, and goes
silently wrong when it is superseded — the worst kind of error, because the
citation still looks precise.

The same holds for ESMA material: name the category and the subject, and let
retrieval find the current instrument. A category also picks up publications that
did not exist when the agent was written, which a list of numbers never will.

This applies to regulator **guidance** — Tiers 2 to 4. Binding legal instruments
keep their identifiers: EMIR is Reg. (EU) 648/2012 and FinSA is SR 950.1, stably
and by universal convention, and amendments to them are tracked rather than
silent.

This governs how an agent's **scope** is written. It does not loosen **citation**:
a citation is always pinpoint and always names the document actually retrieved,
with its tag and date, per the format below.

## Citation format

Pinpoint, not general. A citation that does not identify the provision is not a
citation.

```
FinfraG Art. 104 para. 3 lit. a [CORPUS] corpus/ch/finfrag.md
EMIR Art. 9(1) [RETRIEVED 2026-08-19] https://eur-lex.europa.eu/eli/reg/2012/648/oj
ESMA Q&A on EMIR Reporting, TR Answer 51(b) [RETRIEVED 2026-08-19] <url>
FINMA Circular 2018/02 margin no. 24 [CORPUS] corpus/ch/finma-circ-2018-02.md
```

Do not cite "EMIR" or "MiFIR" alone as support for a requirement.

## Temporal governance

Regulation moves. Every SME output states the date the analysis speaks as of, and
flags anything in flight.

Each finding file header carries:

```
As at: 2026-08-19
Regime version: EMIR as amended by REFIT (Reg. (EU) 2019/834), reporting
                standards applicable from 29 April 2024
Pending changes: <known amendments, transition periods, or consultations that
                 could change this answer, with expected timing — or "none
                 identified">
```

Live examples to check rather than assume: the EMIR REFIT reporting standards,
the MiFIR Review (Reg. (EU) 2024/791) and its consolidated tape and reporting
changes, ongoing FinfraG revision work, and the EU Retail Investment Strategy for
MiFID II conduct obligations. Confirm the current position in the run's grounding
mode — do not restate this list as fact.

## Interpretation discipline

Four categories, never merged, always labelled:

1. **Explicit legal requirement** — the text says it.
2. **Regulator guidance** — a supervisor has said how the text is applied.
3. **Interpretation** — the SME's reasoning from the above. Always an `INT`
   finding, never a `REQ`.
4. **Market practice** — what firms do. Never evidence of what is required.

When official material does not settle the point, say so in those words:

> "This aspect is not clearly defined in [regime] or in official [regulator]
> materials. The position below is interpretation, not confirmed guidance."

Then register an `AMB` finding. An honest ambiguity is a useful output; a
confident guess is a liability.
