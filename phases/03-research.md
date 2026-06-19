# Phase 3: Research

Investigate codebase and gather context.

Reason through trade-offs before recommending. Verify each claim against files you have actually opened; never assert how code behaves without reading it first.

## Process

1. **List the open questions.** Break research into specific, independent questions across codebase, web, and technical investigation. Name each one before you start so you can tell when they are answered.

2. **Scale the effort to the question.** A single fact needs one quick lookup. A comparison of two approaches needs a focused dig into each. An unfamiliar subsystem needs a broad sweep. Do not over-investigate a simple question.

3. **Fan independent questions out to subagents.** When two or more questions do not depend on each other, dispatch a subagent per question in one batch (parallel). Give each one a precise objective, the files or sources to check, and a required output shape. Each subagent explores in its own context and returns a distilled summary, so raw exploration never fills the main window. Read [../references/research-fanout.md](../references/research-fanout.md) for the dispatch contract.

4. **Research loop** (repeat until saturated):
   - Investigate the next question (directly, or collect subagent results)
   - Verify each claim against a file you actually opened. Never assert how code behaves without reading it.
   - Present findings to the user
   - "Record this?" → write to `research/{topic-slug}.md`
   - "Decision made?" → capture in `research/decisions.md`
   - **Saturation check:** if this round produced no new finding that changes a decision, stop. Otherwise continue with the questions still open.

   Exit when every listed question is answered or a round adds nothing that moves a decision. This is the saturation exit from Loop Discipline — do not keep searching for its own sake.

## Decision Capture

Use `templates/decisions.md` format:
```markdown
## Decision: {Title}
**Context**: {Why needed}
**Options**: A: {desc} | B: {desc}
**Chosen**: {Option}
**Rationale**: {Why}
```

## Output

- `research/{topic-slug}.md` per topic (use `templates/research-topic.md`)
- `research/decisions.md` (use `templates/decisions.md`)
- `research/summary.md` (use `templates/research-summary.md`)

## Checkpoint

```
## Research Summary

{Key findings}
Decisions: {count}

- Proceed to Planning → Phase 4
- More research → Continue
```

## State Update

```json
{
  "phase": "planning",
  "research": { "findings_count": 3, "decisions_count": 2, "last_topic": "..." }
}
```
