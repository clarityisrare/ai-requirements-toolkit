# Regulatory Reporting Skills

The pipeline stages, as [Claude skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills).
The six SME specialists are **subagents**, in [`../agents/`](../agents) — they
run in isolated context windows so no jurisdiction can see another's reasoning.

| # | Skill | When it fires |
|---|---|---|
| 1 | [`reg-orchestrator`](./reg-orchestrator) | Any Swiss/EU regulatory reporting question — classifies it, picks the agents, runs the pipeline |
| 2 | [`reg-comparison`](./reg-comparison) | Two or more SME analyses exist and need setting against each other |
| 3 | [`reg-convergence`](./reg-convergence) | "Can one platform serve both?" — implementation convergence and localisation |
| 4 | [`reg-output-quality`](./reg-output-quality) | Turn findings into a business answer, and run the quality gate |
| 5 | [`reg-executive-output`](./reg-executive-output) | Steering committee or management brief |

Start with `reg-orchestrator` for anything multi-regulation. A single-domain
question can go straight to its SME subagent.

Shared method lives in [`../reference/`](../reference) — the pipeline definition,
regulatory domain map, requirement taxonomy, finding-ID scheme, source
governance, grounding modes, confidence framework, analysis discipline and output
contracts. Skills reference it by `${CLAUDE_PLUGIN_ROOT}` rather than each
carrying a copy, so there is one version of the method, not nine.
