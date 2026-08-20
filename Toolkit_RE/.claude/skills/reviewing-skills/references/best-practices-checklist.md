# Reviewing-skills checklist

The baked half of the reviewer's hybrid criteria. `SKILL.md` Step 2 tries to refresh the
source docs live (WebFetch the URLs below); when the network is unavailable it falls back to
this file and notes the staleness in the report.

**last-synced:** 2026-07-29 — re-fetch the URLs and reconcile any new guidance when this is stale.

## Contents

- [Sources](#sources)
- [A. Agent Skills authoring](#a-agent-skills-authoring)
- [B. Model-specific prompting (conditional)](#b-model-specific-prompting-conditional)
- [C. General Claude prompting](#c-general-claude-prompting)
- [D. Reduce hallucinations](#d-reduce-hallucinations)
- [E. Increase output consistency](#e-increase-output-consistency)
- [F. Mitigate jailbreaks & prompt injection](#f-mitigate-jailbreaks--prompt-injection)
- [G. Reduce prompt leak](#g-reduce-prompt-leak)
- [H. Success criteria & evaluations](#h-success-criteria--evaluations)
- [R. Repo conventions](#r-repo-conventions)

## Sources

| Key | Doc | URL |
|---|---|---|
| A | **Agent Skills specification** (the open standard) | https://agentskills.io/specification |
| A | Agent & skill best practices | https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices |
| B | Prompting Claude Sonnet 5 | https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-sonnet-5 |
| B | Prompting Claude Opus 5 | https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5 |
| B | Prompting Claude Opus 4.8 | https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-4-8 |
| B | Prompting Claude Fable 5 (covers Mythos 5 too) | https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5 |
| C | Claude prompting best practices | https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices |
| D | Reduce hallucinations | https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/reduce-hallucinations |
| E | Increase output consistency | https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/increase-consistency |
| F | Mitigate jailbreaks | https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/mitigate-jailbreaks |
| G | Reduce prompt leak | https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/reduce-prompt-leak |
| H | Define success criteria & build evaluations | https://platform.claude.com/docs/en/test-and-evaluate/develop-tests |
| H | **Evaluating skill output quality** (the open standard) | https://agentskills.io/skill-creation/evaluating-skills |

**Precedence — the open standard is the base.** The Agent Skills specification defines what a
valid skill *is*; a conflict with it is a finding. Anthropic's and Claude Code's docs *extend* the
standard with platform guidance and extra frontmatter. Those extensions are permitted and often
useful, but they never override the spec, and a skill that leans on one is not portable to other
agents. Where a client **relaxes** a spec requirement, the spec's stricter form holds — Claude Code
lists `name` as optional and defaults it to the directory name, but `A1` still requires it. Where a
client adds a rule the spec does not have, that rule **narrows** the spec and is safe to apply — the
ban on `anthropic`/`claude` in a name is Anthropic-platform-only, so cite it as a platform note
rather than a spec violation.

Each item below is a pass criterion. Cite the criterion key (e.g. `A3`, `D1`) in findings. A few
items carry their evidence from a doc outside their own group; each of those names its source
inline, so a re-sync checks the page the item actually came from.

## A. Agent Skills authoring

- **A1 — name.** Required. 1–64 characters, lowercase letters, digits, and hyphens only; must not
  start or end with a hyphen, must not contain consecutive hyphens (`--`), and **must match the
  parent directory name** — a mismatch means other agents resolve the skill under a different name
  than it declares. No XML. Gerund preferred; noun phrase acceptable. *Platform note:* Anthropic
  reserves `anthropic` and `claude` in names, which the open standard does not — report that as a
  Claude Code constraint, not a spec violation.
- **A2 — description POV.** Third person ("Reviews…", not "Review…" or "I/you"). It is injected
  into the system prompt; mixed POV hurts discovery.
- **A3 — description content.** Required and non-empty. States both *what* the skill does and
  *when* to use it, with concrete trigger terms. 1–1024 chars. Not vague ("helps with X").
- **A4 — length.** SKILL.md body under ~500 lines **and** under ~5000 tokens; overflow pushed to
  reference files. The two bounds are independent — dense prose can clear the line count and still
  blow the token budget, which is what actually competes with conversation context.
- **A5 — progressive disclosure.** SKILL.md is an overview that references detail files; it does
  not inline everything.
- **A6 — references one level deep.** All reference files link directly from SKILL.md, not from
  each other (nested refs get partially read).
- **A7 — reference TOC.** Reference files >100 lines start with a table of contents.
- **A8 — degrees of freedom.** Specificity matches task fragility: mechanical/fragile steps are
  scripted or exact (low freedom); judgment steps left open (high freedom). Deterministic lookups
  are not left as vague prose.
- **A9 — examples.** Concrete input→output examples where output quality depends on style/shape.
- **A10 — consistent terminology.** One term per concept throughout.
- **A11 — no time-sensitive info.** No "before August 2025…"; use a versioned/"old patterns"
  framing instead, because a dated instruction goes quietly wrong rather than failing loudly. (A
  dated `last-synced` metadata line is acceptable.)
- **A12 — forward-slash paths.** No Windows backslashes, because backslash paths error on Unix
  systems.
- **A13 — one default, not a menu.** Do not offer many interchangeable options; give a default with
  an escape hatch, because a menu makes the model deliberate where it should act.
- **A14 — scripts solve, don't defer.** Bundled scripts handle their own errors; no unexplained
  "voodoo constants"; dependencies listed.
- **A15 — MCP tools fully qualified.** `Server:tool_name`. Without the server prefix the model may
  fail to locate the tool, especially with several MCP servers connected.
- **A16 — allowed-tools least privilege and form.** Only the tools the skill needs. The spec
  defines the value as a **space-separated string**; Claude Code also accepts a comma-separated
  string or a YAML list. A comma-separated or list value is a **Low** — it works here but is not
  the form the standard defines, so it may not port to another agent. Carve-out: when a value
  itself contains spaces (`Bash(git add *)`), space separation is ambiguous — prefer commas or a
  list there and say why, rather than splitting the value.
- **A17 — not over-prescriptive.** The skill doesn't enumerate behaviors a brief instruction
  would cover. Over-specification degrades newer models (Fable 5's docs are explicit that skills
  built for older models are "often too prescriptive" and can lower output quality) and violates
  `R1`. Prefer short steering + intent over exhaustive rule lists. Corroborated by the open
  standard's iteration guidance: when pass rates plateau while rules keep accumulating, the skill is
  over-constrained, and removing instructions is the move to try.
- **A18 — optional spec frontmatter used correctly.** `license` is a license name or the name of a
  bundled license file, kept short. `compatibility` is 1–500 chars and present **only** when the
  skill has real environment requirements (a required CLI, network access, an intended product) —
  most skills need none, and an empty-calorie `compatibility` line costs startup context for
  nothing. `metadata` is a flat map of string keys to string values, with names distinctive enough
  to avoid colliding with another author's keys.
- **A19 — directory layout.** Bundled files sit under the standard directories — `scripts/` for
  executable code, `references/` for documentation, `assets/` for templates and static resources —
  and are addressed by paths relative to the skill root. A reviewer looking for a skill's script in
  `scripts/` should find it there.
- **A20 — spec core vs. client extensions.** The spec's frontmatter is `name`, `description`,
  `license`, `compatibility`, `metadata`, and `allowed-tools`. Anything else — `model`, `effort`,
  `context`, `agent`, `background`, `hooks`, `paths`, `shell`, `disable-model-invocation`,
  `user-invocable`, `disallowed-tools`, `argument-hint`, `arguments` — is a Claude Code extension:
  permitted, but it does not carry to other agents. Flag one only when it is load-bearing and its
  purpose is undocumented, so a reader can tell deliberate use from a copied line. Do not flag a
  skill merely for using an extension.

## B. Model-specific prompting (conditional)

Apply the subset matching the skill's pinned or likely model (per its `model:` frontmatter). All
four current model-prompting docs share the items below; per-model specifics follow. If the pin
is a durable alias (`opus`, `sonnet`) or absent, treat the currently-released model in that family
as the target. Managed settings can override a model pin, so a skill that depends on quirks of
exactly one model is fragile. (`SKILL.md` Step 5 carries the rule for reporting this.)

**Shared across current models:**

- **B1 — verbosity.** No forced ceremony (mandatory summaries, interim status) unless it is
  load-bearing; current models self-calibrate length. (See also `A17`.)
- **B2 — effort/thinking not over-scaffolded.** Do not hand-roll what adaptive thinking and the
  effort parameter already do.
- **B3 — tool nudges.** If the skill relies on tool use with thinking off, it nudges explicitly.
- **B4 — coverage before filtering.** A skill that finds, reviews, or audits must not cap the
  *finding* stage with "only report high-severity", "be conservative", or "don't nitpick". Current
  models follow such a bar literally — they investigate just as deeply, then drop findings below
  it, so measured recall falls while the underlying ability is unchanged. Ask for coverage at the
  finding stage and filter in a separate step. (Stated for Sonnet 5, Opus 5, and Opus 4.8.)
- **B5 — progress-update scaffolding.** Current models narrate agentic work well unprompted.
  Scaffolding that forces interim status ("after every 3 tool calls, summarize progress") should be
  removed; describe the cadence and shape wanted instead, with positive examples. **Carve-out:** a
  workflow checklist the skill tells the model to copy into its reply and tick off is *not* a `B5`
  finding — the `A` authoring doc endorses that pattern by name for complex multi-step workflows.
  `B5` governs narration cadence, not task tracking.

**Sonnet 5:** literal instruction following (state scope — see `C8`); verbosity self-calibrates;
more agentic than its predecessor and reaches for tools and self-verification loops readily — with
thinking disabled it is *less* likely to reach for tools, so `B3` applies then.

**Opus 5:** self-verifies and self-corrects unprompted — explicit "verify/double-check" steps
cause over-verification, so a skill should only script verification that the model wouldn't do
itself (external validators, evals); delegates to subagents readily — cap or scope delegation if
the skill fans out; narration and written deliverables run long — calibrate length in the prompt
where it matters (effort controls thinking, not response length); **expands scope** — it may add
steps nobody asked for, so a narrow skill states its scope explicitly. With thinking disabled it
can emit tool calls as plain text or leak internal XML tags, and a rule telling it not to think
makes that leakage worse — remove such a rule rather than adding one.

**Opus 4.8:** favors reasoning over tool calls — nudge explicitly if the skill depends on tool
use; spawns **fewer subagents** by default — steer explicitly if the skill fans out; `xhigh`/`high`
effort suits agentic work.

**Fable 5 (and Mythos 5, which shares this doc):** brief steering beats enumerating behaviors
(`A17`); much longer turns on hard tasks —
if the skill assumes quick completion or blocks synchronously, reconsider; dispatches parallel
subagents readily; never instruct it to reproduce its reasoning (`C7`).

> **The verification rule inverts between Opus 5 and Fable 5.**
> On Opus 5, scripted "verify your work" steps cause over-verification and should be removed. On
> Fable 5 long runs, the opposite holds: self-verification should be made *explicit*, and separate
> fresh-context verifier subagents outperform self-critique. A skill pinned to one model can carry
> guidance that is wrong for the other.

## C. General Claude prompting

- **C1 — clear & direct.** Unambiguous, sequenced instructions.
- **C2 — multishot examples.** Present for style-dependent output (overlaps A9).
- **C3 — room to think.** Complex judgment steps allow step-by-step reasoning.
- **C4 — XML/structure.** Structure used where it aids parsing; not decorative.
- **C5 — role.** A role/persona is set where it improves consistency (optional, not required).
- **C6 — chaining.** Genuinely complex tasks are split into sequential sub-steps rather than one
  mega-instruction.
- **C7 — no reasoning-echo.** The skill never instructs the model to transcribe, echo, or explain
  its internal reasoning *as response text*. Beyond being noise, this trips the
  `reasoning_extraction` refusal on Fable 5 (and elevated fallbacks). If reasoning visibility is
  needed, read structured `thinking` blocks — do not ask the model to narrate them into output.
  (Sourced from the Fable 5 doc in group `B`, not from this group's doc.)
- **C8 — explicit scope.** Instructions meant to apply broadly state their scope ("every section,
  not just the first"). All current models follow instructions literally and won't silently
  generalize from one item to the rest.
- **C9 — tool use not over-prompted.** No blanket "default to using `X`" or "if in doubt, use `X`".
  Tools that undertriggered on older models trigger appropriately now, so a blanket default makes
  them *over*trigger. Scope the nudge to the case that needs it ("use `X` when it would sharpen
  your understanding of the problem"). This qualifies `B3` rather than contradicting it: nudge
  explicitly when thinking is off, do not nudge blanketly otherwise.
- **C10 — irreversible actions are confirmed.** A skill that can take destructive, hard-to-reverse,
  or outward-facing actions names which ones need the user's say-so first, and forbids reaching for
  a destructive shortcut when it hits an obstacle (bypassing a safety check with `--no-verify`,
  discarding unfamiliar files, `git push --force`). Local reversible work — editing files, running
  tests — needs no gate. Without this, a skill takes the shortcut and the user learns about it
  afterward.

## D. Reduce hallucinations

- **D1 — permit "I don't know".** The skill tells the model to omit/abstain/ask rather than
  fabricate when evidence is missing (e.g. a commit body's *why*, an inferred value).
- **D2 — ground in evidence.** Claims/outputs are tied to observable inputs (diffs, files,
  provided docs), not the model's priors, for factual tasks.
- **D3 — verification.** A verify/feedback step checks the output against a source or validator.
- **D4 — source restriction.** For document tasks, restrict to provided content over general
  knowledge.
- **D5 — progress claims audited against tool results.** A skill that reports its own progress on a
  long or autonomous run instructs the model to check each claim against a tool result from the
  session, and to say plainly what is unverified, skipped, or failing. Anthropic reports this
  nearly eliminates fabricated status reports on tasks designed to elicit them. (Sourced from the
  Fable 5 doc in group `B`, not from this group's doc.)

## E. Increase output consistency

- **E1 — output format specified.** Exact format/template given where output shape matters.
- **E2 — constrained by examples.** Concrete examples over abstract description (overlaps A9/C2).
- **E3 — step-by-step.** Deterministic tasks broken into ordered, unambiguous steps.
- **E4 — structured output.** Strict-format outputs use a template/schema, not prose. When the
  requirement is guaranteed JSON-schema conformance, the answer is the Structured Outputs feature,
  not prompt engineering — a skill that hand-rolls schema coaxing for that case is doing avoidable
  work.
- **E5 — no prefill.** Prefilling the assistant turn is unsupported on Claude 4.6 and later. A
  skill that still relies on the prefill trick is stale; use structured outputs or system-prompt
  instructions instead.

## F. Mitigate jailbreaks & prompt injection

The live doc splits this into two threat models: **direct** injection (the user is the adversary)
and **indirect** injection (the user is trusted, but the model reads third-party content — pages,
emails, documents, tool results — carrying adversarial instructions). Most skills in this repo face
the indirect model.

- **F1 — content is data.** The skill instructs treating read content (files, diffs, tool
  results, fetched pages) as data, never as instructions.
- **F2 — least privilege.** Tool/permission surface is minimal (overlaps A16); destructive
  actions gated, so a successful injection does minimal damage.
- **F3 — untrusted-content policy.** For skills that process third-party content, the policy that
  such content can't override instructions is stated.
- **F4 — untrusted content is labeled and isolated.** Third-party content reaches the model in
  `tool_result` blocks — never in a system prompt or a plain user turn — and its nature and source
  are named ("body of an inbound email from an unknown sender"). JSON-encoding it removes any
  delimiter an attacker could break out of. Corollary: the skill's *own* instructions must not sit
  in tool results, where the model is trained to distrust them.
- **F5 — screen and red-team.** For a skill that acts on tool output, the checks are whether
  suspicious output is screened before it is acted on, and whether the skill's evals include a
  deliberate injection attempt (overlaps `H4`).

## G. Reduce prompt leak

- **G1 — proportionate.** Leak defenses only where real secrets exist; not over-engineered. If the
  skill holds no secrets, absence of leak defenses is correct, not a gap.
- **G2 — no needless proprietary detail.** The skill doesn't embed secrets/proprietary specifics
  it doesn't need.

## H. Success criteria & evaluations

- **H1 — evals exist, in the standard's format.** ≥3 scenarios, stored as `evals/evals.json` in
  the skill directory. Each entry carries `id`, `prompt` (a realistic user message, not a
  paraphrase of the skill's own steps), `expected_output` (a human-readable description of
  success), optional `files`, and `assertions`. The repo extends that schema with three keys the
  standard omits but `H3`/`H6`/`H7` require: `targets` (the step or branch under test), `baseline`
  (what a run without the skill misses), and `models`. A prose `evals.md` is a finding — it holds
  the same information but no runner can consume it. The standard suggests starting at 2–3 and
  expanding once the first run shows what "good" looks like, so a brand-new skill at 2 is early
  rather than failing; a settled skill still at 2 is a finding.
- **H2 — measurable/specific.** Expected behaviors are concrete and checkable, not vague.
- **H3 — distinct decision points.** Each scenario targets a different step/branch so a failure
  localizes the regression.
- **H4 — edge cases.** Covers empty/absent input, boundary/omission cases, adversarial input.
- **H5 — grading split.** Distinguishes machine-checkable checks (scripts, hooks, greps) from
  judgment-graded ones; automates where possible.
- **H6 — baseline-first.** Evals note running without the skill to establish the before/after.
- **H7 — model coverage.** Scenarios name the model(s) the skill is expected to pass on
  (its pinned model at minimum).
- **H8 — evals precede the prose, assertions follow the first run.** The documented order is: find
  the gaps by running the task without a skill, write three scenarios against those gaps, measure
  the baseline, then write the minimum instructions that pass. A skill whose evals were clearly
  written after the fact is at risk of documenting imagined problems rather than real ones. The
  order *within* a scenario is the reverse of what that implies: `prompt` and `expected_output`
  come first, and `assertions` are added **after** the first run shows what the output actually
  looks like. Assertions invented before any run tend to be brittle or unverifiable, so do not
  fault a scenario set for reaching its assertions on the second pass.
- **H9 — criteria are SMART.** Specific, measurable, achievable, relevant. "Handles edge cases
  well" fails; a stated pass condition on a named input passes. Volume of cheap automated checks
  beats a handful of hand-graded ones (`H5`).
- **H10 — grader independence.** Where an LLM grades, it should not be the same instance that
  produced the output. Self-grading in the same run is not evidence. For comparing two versions of
  a skill, prefer a blind comparison — the judge scores both outputs without being told which
  version produced which.
- **H11 — clean-context runs.** Each eval run starts from a fresh context — a subagent, or a
  separate session — with no state left over from a previous run or from developing the skill. A
  run that inherits the authoring conversation is testing the conversation, not the `SKILL.md`.
- **H12 — cost recorded against benefit.** Runs capture token count and duration alongside the
  pass rate, and the skill's value is read as the *delta* against the baseline. Without the cost
  side, a skill that triples token usage for a two-point gain looks identical to one that is both
  better and cheaper.
- **H13 — assertion hygiene.** Assertions that pass in both the with-skill and without-skill runs
  are removed or replaced: the model already handles them, so they inflate the with-skill pass rate
  without measuring anything the skill contributes. Assertions that fail in both are investigated —
  the assertion is broken, the case is too hard, or it checks the wrong thing. The assertions worth
  keeping are the ones that pass with the skill and fail without it.
- **H14 — evidence-based PASS.** Grading records PASS or FAIL with evidence quoting or referencing
  the actual output, and gives no benefit of the doubt: a section titled "Summary" holding one
  vague sentence fails an assertion asking for a summary. An opinion without a quotation is not a
  grade.

## R. Repo conventions

Sources: `CLAUDE.md`.

- **R1 — simplicity first.** No speculative features/abstractions/config beyond what the skill's
  job requires.
- **R2 — surgical.** The skill's own *apply* edits touch only what a finding requires.
- **R3 — single source of truth / no drift.** The skill references authoritative repo docs rather
  than restating their rules; any restated rule is sourced and kept in sync. Unsourced restated
  rules are a drift finding.
- **R4 — ask when uncertain.** The skill surfaces ambiguity/tradeoffs rather than guessing
  silently.
- **R5 — naming convention.** Skill names use gerund form (verb-ing + object, e.g.
  `reviewing-skills`, `checking-dev-env`).
- **R6 — prose conventions.** Skill *body* prose (`SKILL.md` body, the prose fields of
  `evals/evals.json` or a legacy `evals.md`, `references/`)
  follows `references/writing-conventions.md`. Judge holistically; `R7`–`R10` below
  are the specific checks worth calling out by name. Two scope limits: the `name`/`description`
  frontmatter is **not** covered (that is `A1`/`A2`/`A3` — never reword a `description` for prose
  style, it drives discovery), and the doc has **no sentence-length rule** — do not invent one, see
  its § What is deliberately not here.
- **R7 — named actor.** Instructions use the active voice. Flag passive constructions where the
  actor is ambiguous ("is rejected" — by the skill, the model, or a hook?). Passive is fine where
  the agent genuinely doesn't matter.
- **R8 — notes vs. instructions.** Notes, blockquotes, and parentheticals carry information only.
  A normative rule hiding in an aside is a finding: it belongs in a numbered step.
- **R9 — guardrail consequences.** Every prohibition states its risk or result, so the model can
  weigh it against a conflicting instruction. A bare "never do X" is a finding.
- **R10 — closed sets & explicit referents.** No `etc.`/"and so on" terminating a list the model
  must act on (it invites invented members) — state the membership test instead. No bare `this` /
  `it` / `they` where two antecedents are plausible, because a pronoun with two plausible
  antecedents is a coin flip.
