# Phase 2: Requirements Gathering

Interview-style: ONE question at a time, wait for answer, adapt next question.

## Process

1. Start with open-ended problem question
2. Based on answer, drill down or move to next category (scope, success, context, constraints)
3. After 3-7 questions (2-3 for small tasks), summarize
4. Confirm accuracy

## Output

Write `requirement.md` using `templates/requirement.md`:
- Problem statement
- Scope (in/out)
- Success criteria
- Context (files, systems)
- Constraints
- Q&A transcript

## Checkpoint

```
## Requirement Summary

{2-3 sentence summary}

**Scope**: {in/out}
**Success**: {key criteria}

- Proceed to Research → Phase 3
- Skip research → Phase 4 (if well-understood task)
- Revise → Continue interview
```

## State Update

```json
{
  "phase": "research",
  "requirement": { "summary": "...", "minimal": false }
}
```
