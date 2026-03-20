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
3. Research → 4. Planning (checkpoint)
4. Planning → 5. Execution (checkpoint)
5. Execution → 6. Documentation (checkpoint) or skip to 7
6. Documentation → 7. Removal (checkpoint)
```

**Never auto-proceed between phases.** Summarize, confirm, allow revisiting.

## Artifacts Structure

Artifacts are always created in the **current project directory**, not in the global workflow location.

```
{project-root}/.claude/workflows/guided-tour/artifacts/{NNN}-{slug}/
├── session.json
├── requirement.md
├── research/
│   ├── {topic}.md
│   ├── decisions.md
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

## Files

- `phases/01-07` - Phase instructions
- `templates/` - Output formats
- `references/` - Step format specification, session schema
