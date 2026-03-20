# Guided Tour

A structured, seven-phase workflow framework designed for AI-assisted software development. It turns vague tasks into well-scoped, executable implementation plans — then walks through them step by step with built-in checkpoints, rollback, and documentation.

## Why This Exists

AI coding assistants are powerful but stateless. They lose context between conversations, skip requirements gathering, jump straight to code, and produce steps that depend on invisible assumptions. Guided Tour solves this by giving AI agents a structured process to follow — with persistent artifacts that survive context resets.

**The core idea:** every step file must be executable by an agent with zero prior context. If you handed a single step file to a brand-new AI session, it should be able to complete it without asking "what did we decide earlier?"

## How It Works

```
1. Initialization    → Create session, set up artifact folder
2. Requirements      → Interview-style Q&A (one question at a time)
3. Research          → Investigate codebase, gather context, record decisions
4. Planning          → Generate self-contained step files
5. Execution         → Run steps sequentially with checkpoints
6. Documentation     → Persist learnings to project docs
7. Removal           → Clean up session artifacts
```

Each phase produces artifacts. Each transition requires explicit user approval — the workflow never auto-advances between phases.

## Optimized for AI Agents

### Self-Contained Steps (The "Ralph Wiggum" Principle)

The most important design decision: every step file copies all context it needs inline. No references to "see requirement.md" or "as discussed earlier." Each step includes:

- **Copied** requirement summary (not a file reference)
- **Copied** relevant decisions with rationale
- Explicit file paths, code patterns shown inline
- Validation commands and acceptance criteria
- Rollback instructions

This means an agent can pick up any step — even after a context window reset — and execute it without needing the full conversation history.

### Session State as JSON

Session progress is tracked in `session.json` with a defined [JSON schema](references/session-schema.json). An agent resuming work can read this file to understand exactly where the workflow left off: current phase, completed steps, step results, and decisions made.

```json
{
  "slug": "001-auth-flow",
  "phase": "execution",
  "status": "in_progress",
  "execution": {
    "current_step": 3,
    "completed_steps": [1, 2],
    "step_results": { "1": { "status": "complete" }, "2": { "status": "complete" } }
  }
}
```

### Artifact-Based Memory

All intermediate work (requirements, research findings, decisions, plans) is written to disk as markdown files in a structured folder. This is the agent's persistent memory — it doesn't depend on conversation history or context windows.

```
.claude/workflows/guided-tour/artifacts/001-auth-flow/
├── session.json          # Current state
├── requirement.md        # Scoped requirements
├── research/
│   ├── existing-auth.md  # Research findings
│   ├── decisions.md      # Recorded decisions with rationale
│   └── summary.md        # Research summary
├── plan.md               # Implementation plan with dependency graph
├── steps/
│   ├── step-001.md       # Self-contained step files
│   ├── step-002.md
│   └── step-003.md
└── execution-log.md      # Step-by-step results log
```

### Checkpoint-Driven Flow

After every phase and every executed step, the workflow pauses and presents options: continue, review, revise, rollback, or pause. This keeps the human in control while letting the AI do the heavy lifting.

## Using Guided Tour

### Setup

Copy or clone this repository into your AI agent's workflow directory. For Claude Code:

```bash
# Clone into your project
git clone https://github.com/hexcon/Guided-Tour.git .claude/workflows/guided-tour
```

Then reference the workflow in your agent configuration (e.g., `CLAUDE.md`, custom slash commands, or agent instructions).

### Session Commands

| Command | Action |
|---------|--------|
| `status` | Show current session state |
| `back` | Return to previous phase |
| `pause` | Save progress and exit |
| `abort` | Discard session (with confirmation) |

### Intent Routing

The workflow recognizes natural language intents:

| What you say | What happens |
|---|---|
| "new", "start", "build X" | Start Phase 1 |
| "continue", "resume" | Resume active session |
| "research", "investigate" | Jump to Phase 3 |
| "plan", "design" | Jump to Phase 4 |
| "execute", "run", "do step" | Jump to Phase 5 |
| "status", "list" | List all sessions |

### Step Sizing

Plans are generated at three granularity levels:

| Level | Time per step | Best for |
|-------|---------------|----------|
| Fine | 5-15 min | Complex or unfamiliar code |
| Medium | 15-30 min | Most tasks (default) |
| Coarse | 30-60 min | Well-understood changes |

Each step targets **80-190 lines** — under 80 likely means missing context, over 190 means it should be split.

## Repository Structure

```
├── GUIDED-TOUR.md           # Workflow overview and routing table
├── phases/
│   ├── 01-initialization.md # Session setup
│   ├── 02-requirements.md   # Interview-style requirements gathering
│   ├── 03-research.md       # Codebase investigation and decision capture
│   ├── 04-planning.md       # Step generation with dependency graphs
│   ├── 05-execution.md      # Sequential step execution with checkpoints
│   ├── 06-documentation.md  # Persist learnings to project docs
│   └── 07-removal.md        # Artifact cleanup
├── templates/               # Output format templates
│   ├── requirement.md
│   ├── plan.md
│   ├── step.md
│   ├── decisions.md
│   ├── execution-log.md
│   ├── research-topic.md
│   └── research-summary.md
└── references/
    ├── step-format.md       # Self-containment specification
    └── session-schema.json  # JSON schema for session state
```

## Design Principles

1. **Never auto-advance.** Every phase transition requires user confirmation.
2. **Copy, don't reference.** Steps include all context inline — no cross-file dependencies during execution.
3. **Artifacts are the source of truth.** Not conversation history, not memory, not assumptions.
4. **Fail gracefully.** Every step has rollback instructions. Failed steps can be retried, skipped, or diagnosed.
5. **Human stays in control.** The AI does the work; the human approves the direction.

## License

MIT
