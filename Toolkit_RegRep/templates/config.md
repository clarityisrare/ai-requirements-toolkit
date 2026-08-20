# Run Configuration

Copy to `.reg-analysis/config.md` in your project. If absent, Mode 1 and today's
date apply.

```yaml
grounding_mode: 1        # 1 = hybrid | 2 = live-web | 3 = corpus-only
corpus_path: ./corpus    # used by modes 1 and 3
as_of_date: 2026-08-19   # the date the analysis speaks as of
```

| Mode | Behaviour | Use when |
|---|---|---|
| 1 | Corpus first, official web fallback, remainder tagged `[UNVERIFIED]` with a gap | Most work |
| 2 | Every citation retrieved live from official sources; no fallback to recollection | Currency matters most |
| 3 | Corpus only; anything outside it is a gap | Audit-sensitive, reproducible runs |

See `reference/grounding-modes.md` for the full specification.
