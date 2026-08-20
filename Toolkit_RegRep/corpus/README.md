# Regulatory Corpus

Local copies of official regulatory texts. Grounding modes 1 and 3 cite from
here; mode 2 ignores it.

A corpus is what turns "the model says EMIR Art. 9 requires X" into "here is
EMIR Art. 9, and it requires X". It is the difference between a citation and a
recollection.

## Layout

```
corpus/
  ch/
    finfrag.md                  FinfraG / FMIA (SR 958.1)
    finfrav.md                  FinfraV / FMIO (SR 958.11)
    finfrav-finma.md            FinfraV-FINMA / FMIO-FINMA (SR 958.111)
    finma-circ-2018-02.md       Duty to report securities transactions
    finsa.md                    FinSA / FIDLEG (SR 950.1)
    finso.md                    FinSO / FIDLEV (SR 950.11)
    finma-circ-2025-02.md       Rules of conduct under FinSA/FinSO
  eu/
    emir.md                     Reg. (EU) 648/2012 consolidated
    emir-refit.md               Reg. (EU) 2019/834
    mifir.md                    Reg. (EU) 600/2014 consolidated
    mifid2.md                   Dir. 2014/65/EU
    rts-22.md                   Del. Reg. (EU) 2017/590
    rts-23.md                   Del. Reg. (EU) 2017/585
    del-reg-2017-565.md
    del-dir-2017-593.md
    esma-emir-qa.md
    esma-mifir-tr-guidelines.md
  venue/
    six-reporting-spec.md       Tier 4 — operationally binding, not the legal source
  SOURCES.md                    what was downloaded, from where, when
```

## Populating it

Download the consolidated version from the official source, convert to Markdown
keeping article and paragraph numbering intact, and record it in `SOURCES.md`.

| Source | Where |
|---|---|
| Swiss legislation | https://www.fedlex.admin.ch/ |
| FINMA circulars and guidance | https://www.finma.ch/ |
| EU legal texts | https://eur-lex.europa.eu/ |
| ESMA guidelines, Q&As, RTS | https://www.esma.europa.eu/ |

Two things matter more than completeness:

**Keep the numbering.** An SME cites "Art. 104 para. 3 lit. a". If the conversion
flattened the structure, the citation cannot be pinpointed and the corpus stops
being useful as evidence.

**Record the date.** Every file's entry in `SOURCES.md` carries the retrieval
date and the consolidation date of the text. A corpus with no dates cannot
support an as-of statement, and an undated regulatory analysis is not auditable.

## Keeping it current

Regulation moves; a stale corpus is worse than none, because it is confidently
wrong. Re-download when an amendment applies, and update `SOURCES.md`. In mode 1
the web fallback covers gaps, so an incomplete corpus degrades gracefully. In
mode 3 it does not — everything missing becomes an evidence gap, which is the
intended and honest behaviour.

## An empty corpus

Perfectly usable. Mode 1 falls back to the web for everything and tags what it
cannot verify. Start empty, add the texts you cite most, and the runs get faster
and more deterministic as you go.
