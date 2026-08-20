# Grounding Modes

How SME agents obtain the regulatory text they cite. This is the single biggest
determinant of output trustworthiness, so it is an explicit, recorded setting —
not an implicit behaviour.

Set it in `.reg-analysis/config.md` in your project:

```markdown
grounding_mode: 1        # 1 = hybrid (default) | 2 = live-web | 3 = corpus-only
corpus_path: ./corpus    # only used by modes 1 and 3
as_of_date: 2026-08-19   # the date the analysis speaks as of
```

If the file does not exist, **Mode 1** applies and today's date is used as
`as_of_date`. The mode in force is recorded in every run manifest and in the
footer of every terminal output — a reader must be able to tell how the citations
were obtained.

---

## Mode 1 — Hybrid (default, recommended)

Corpus first, web second, and everything else labelled.

1. Search `corpus_path` for the provision. If found, cite it as
   `[CORPUS]` with the local file and the article/paragraph.
2. If not in the corpus, fetch the official source (see `source-governance.md`
   for the domain allowlist) and cite it as `[RETRIEVED <date>]` with the URL.
3. If neither is available and the point still needs to be made, state it as an
   interpretation, tag it `[UNVERIFIED]`, and register a `GAP` finding.

Best for most work: deterministic and fast where the corpus covers the ground,
current where it does not, and honest about the remainder.

## Mode 2 — Live web

Every citation must be retrieved during the run. Nothing is cited from model
memory.

- Fetch from the official domains only (see `source-governance.md`).
- Every citation carries `[RETRIEVED <date>]` and a URL.
- If retrieval fails, do **not** fall back to recollection. Register a `GAP` and
  say the provision could not be retrieved.

Best when currency matters more than speed — a live rule change, a newly
published ESMA Q&A, a consultation in flight. Slower, network-dependent, and
subject to source-site availability.

## Mode 3 — Corpus only

Strictly offline. Only material in `corpus_path` may be cited.

- No web access, no fallback.
- Anything outside the corpus is a `GAP`, full stop — including provisions the
  model is confident it knows.
- The response header states the corpus contents and their retrieval dates so a
  reviewer can see exactly what the analysis had to work with.

Best for audit-sensitive and reproducible work: the same question against the
same corpus gives the same evidence base, and there is no dependency on an
external site's uptime or content changing under you.

---

## Citation tags — used identically in all three modes

| Tag | Meaning |
|---|---|
| `[CORPUS]` | Quoted from a local official text; include file and article |
| `[RETRIEVED <date>]` | Fetched from an official source during this run; include URL |
| `[SECONDARY]` | A non-official source (industry, vendor, law firm, consultancy); never used where an official source exists, and always named as secondary |
| `[UNVERIFIED]` | Asserted without a source that could be checked. Mode 1 only. Always accompanied by a `GAP` finding |

## What a mode never changes

The source hierarchy, the requirement that interpretation is labelled as
interpretation, and the prohibition on presenting market practice as regulation.
Those hold in every mode. See `source-governance.md`.
