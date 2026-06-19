---
name: guided-tour
description: Seven-phase guided workflow for non-trivial code work — requirements, research, planning, step-by-step execution, documentation, cleanup. Use when starting a new feature, tackling a bug fix that needs investigation or design choices, or resuming a paused workflow session. Skip for trivial edits (typos, one-line fixes, mechanical renames). Triggers on intents like "new feature", "start", "build X", "fix bug Y", "continue", "resume", "plan", "execute", "status".
---

# Guided-Tour Workflow

Seven-phase workflow for research and implementation tasks.

## Intent Routing

| Intent | Patterns | Action |
|--------|----------|--------|
| New | "new", "start", "build X", no args + no active session | Phase 1 |
| Resume | "continue", "resume", no args + active session | Show status |
| Requirements | "requirements", "reqs" | Phase 2 |
| Research | "research", "investigate" | Phase 3 |
| Planning | "plan", "design", "steps" | Phase 4 |
| Execute | "execute", "run", "do step" | Phase 5 |
| Document | "document", "persist" | Phase 6 |
| Cleanup | "cleanup", "remove" | Phase 7 |
| Status | "status", "list" | List sessions |

## Session Detection

1. Scan `.claude/workflows/guided-tour/artifacts/` in the current project directory for existing sessions
2. Active sessions exist → "Resume or start new?"
3. No active sessions → Phase 1

## Phase Transitions

```
1. Initialization → 2. Requirements (auto)
2. Requirements → 3. Research (checkpoint) or skip to 4
3. Research → 4. Planning (checkpoint)        [inner loop: parallel investigate → record, until saturated]
4. Planning → 5. Execution (checkpoint)        [inner loop: draft → critique → revise, cap 2]
5. Execution → 6. Documentation (checkpoint) or skip to 7
                                               [inner loops: per-step verify, retry-with-diagnosis, final adversarial review]
6. Documentation → 7. Removal (checkpoint)
```

**Never auto-proceed between phases.** Summarize, confirm, allow revisiting.

The phase sequence is linear and human-gated. The work *inside* phases 3, 4, and 5 runs in loops — the agent investigates, verifies, and revises against a check until the check passes, then stops. See Loop Discipline.

## Loop Discipline

Phases 3-5 use iterative loops to raise quality. Every loop obeys three rules. Without them, loops either stop too early (one weak pass) or never stop (churn that burns tokens and degrades the output).

1. **Cap the iterations.** Each loop states a maximum (research effort scaled to complexity, plan critique 2 passes, per-step fixes 3 attempts, final review 2 rounds). Hitting the cap is the fallback exit, not the normal one.
2. **Exit on convergence.** Stop the moment the check passes or the critic finds no blocking gap. Do not run the full budget out of habit. Extra passes past convergence make the work worse, not better.
3. **Make "done" checkable.** Prefer a machine-checkable signal — tests pass, build exits clean, linter is silent, output matches a fixture — over the agent's own "looks done" judgment. When no automated check exists, name the explicit pass/fail criteria before the loop starts.

**Show evidence, not assertions.** A loop closes only when the agent has run the check and read its real output. "Should pass now" does not close a loop.

## Artifacts Structure

Artifacts are always created in the **current project directory**, not in the global skill location.

```
{project-root}/.claude/workflows/guided-tour/artifacts/{NNN}-{slug}/
├── session.json
├── requirement.md
├── research/
│   ├── {topic}.md
│   ├── decisions.md
│   ├── notes.md          # running discoveries during execution (folded into steps)
│   └── summary.md
├── plan.md
├── steps/
│   └── step-{NNN}.md
└── execution-log.md
```

## Session Commands

- "status" → Show current state
- "back" → Return to previous phase
- "pause" → Save and exit
- "abort" → Discard (with confirmation)

## When to Skip Guided-Tour

The user's global CLAUDE.md sets Guided-Tour as the default workflow for fixes and new features. Skip it (proceed directly without invoking phases) only when:

- The change is a single-line edit, typo, or obvious mechanical fix
- The user explicitly says "quick fix", "just do it", "no workflow", or similar
- The work is purely exploratory (reading, explaining, answering questions — no code change)

When in doubt, ask the user: *"This looks non-trivial — want me to run Guided-Tour, or handle it directly?"*

## Files

- `phases/01-07` — Phase instructions
- `templates/` — Output formats
- `references/` — Step format specification, session schema
