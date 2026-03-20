# Phase 1: Initialization

Create session folder and initialize state.

## Artifacts Location

Artifacts are stored in the **current project directory** (not the global workflow location):

`.claude/workflows/guided-tour/artifacts/`

If `.claude/` does not exist in the current working directory, create the full path:
`.claude/workflows/guided-tour/artifacts/`

## Process

1. **Determine session number**
   ```bash
   ls .claude/workflows/guided-tour/artifacts/ 2>/dev/null | grep -E '^[0-9]{3}-' | sort -r | head -1
   # Extract number, increment. No sessions → start at 001
   ```

2. **Generate slug** from user input: lowercase, hyphens, max 30 chars

3. **Create structure**
   ```
   .claude/workflows/guided-tour/artifacts/{NNN}-{slug}/
   ├── session.json
   ├── research/
   └── steps/
   ```

4. **Initialize session.json**
   ```json
   {
     "slug": "{NNN}-{slug}",
     "phase": "requirements",
     "status": "in_progress",
     "created": "{ISO timestamp}",
     "updated": "{ISO timestamp}"
   }
   ```

5. **Confirm** and transition to Phase 2

## Output

- Folder structure created under `.claude/workflows/guided-tour/artifacts/`
- session.json initialized
- Automatic transition to Phase 2
