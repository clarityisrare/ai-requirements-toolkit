# Mermaid syntax traps to check before returning a diagram

Use this list when `mermaid-cli` is not available to render the diagram (workflow
step 4). Each trap below renders as an error block on GitHub rather than a diagram,
and each one is silent — the source looks fine to read. Check the generated diagram
against every item, then state in your reply that you reviewed it against this list
rather than machine-verifying it.

## Every diagram type

- **Reserved words as node ids.** `end`, `graph`, `class`, `state`, `subgraph`,
  `style`, `click`, `direction` break parsing when used as a bare id. Rename the id
  (`endState`, `graphNode`) or give the node an explicit label.
- **Unescaped characters inside labels.** A label containing `(`, `)`, `[`, `]`,
  `{`, `}`, `<`, `>`, `"`, or `#` can close its own shape early. Wrap the label in
  double quotes (`A["Total (net)"]`) or replace the character with its `#35;`-style
  HTML entity.
- **A label that starts with `o` or `x`.** Written tight against an edge (`A---oB`),
  Mermaid reads the letter as a circle or cross edge ending. Add a space or quote
  the label.
- **Stray blank first line.** The diagram-type keyword must be on the first
  non-empty line; a leading comment before it is fine, other text is not.

## flowchart / graph

- **Diagram-type keyword present.** The source starts with `flowchart TD` (or `LR`)
  or `graph TD`. A direction alone (`TD`) is not valid.
- **Arrows are edge syntax, not state syntax.** Use `-->`, `---`, `-->|label|`. A
  colon-label (`A: text`) is state-diagram syntax and errors here.

## stateDiagram-v2

- **Header is exactly `stateDiagram-v2`.** The unversioned `stateDiagram` is the
  legacy parser and does not accept the same label syntax.
- **Transition labels use a colon, not a pipe.** Write `A --> B: Submit`. The
  flowchart form `A -->|Submit| B` errors in a state diagram.
- **Start and end are `[*]`.** Not `[ * ]`, not `start`.

## sequenceDiagram

- **Participants declared or first-used consistently.** A `participant X as Label`
  line fixes the display name; after that, refer to `X`, not `Label`.
- **`alt` / `else` / `opt` / `loop` blocks are closed with `end`.** An unclosed
  block consumes the rest of the diagram.
- **Message arrows are valid.** `->>`, `-->>`, `->`, `-->`. A flowchart `-->|x|`
  label form is not a sequence message.

## Quick self-check

If none of the above applies and the node/edge count matches what the user
described, the diagram is safe to return with a note that it was reviewed against
this checklist. When in doubt, paste the source into mermaid.live, which reports the
same parse errors `mermaid-cli` would.
