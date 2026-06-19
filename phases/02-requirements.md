# Phase 2: Requirements Gathering

Two passes: one open question, then a single batched round for the rest. Front-loading the requirements in one round costs fewer turns and gives the model a well-specified task to reason against.

## Process

1. Ask one open-ended problem question: what are we building or fixing, and why.
2. From the answer, identify the remaining unknowns across scope, success criteria, context (files, systems), and constraints.
3. Present those unknowns as one batched set using the AskUserQuestion tool (multi-question form), not one at a time. Pre-fill each question with the most likely option so the user can confirm fast.
4. Ask a targeted follow-up round only if an answer opens a material new unknown. Otherwise summarize.
5. Confirm the summary with the user.

Small tasks: the open question plus one short batch is usually enough.

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
- Revise → Ask another round
```

## State Update

```json
{
  "phase": "research",
  "requirement": { "summary": "...", "minimal": false }
}
```
