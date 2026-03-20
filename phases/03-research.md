# Phase 3: Research

Investigate codebase and gather context.

## Process

1. **Select direction**
   - Codebase exploration
   - Web research
   - Technical investigation

2. **Research loop**
   - Investigate specific question
   - Present findings to user
   - "Record this?" → write to `research/{topic-slug}.md`
   - "Decision made?" → capture in `research/decisions.md`
   - "More research?" → repeat or checkpoint

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
