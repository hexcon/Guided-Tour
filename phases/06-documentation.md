# Phase 6: Documentation

Persist learnings to project knowledge base.

## Process

1. **Select target**
   - Feature documentation - New features, enhancements
   - Concept documentation - Patterns, architecture, domain knowledge
   - Both
   - Skip → Phase 7

2. **Determine documentation location**
   - Ask user where project documentation should be written
   - Default suggestion: a `docs/` or `AI/analysis/` folder in the project root

3. **Gather sources**: requirement.md, research/, plan.md, execution-log.md

4. **Write documentation**
   - 80/20 rule: 20% of docs covering 80% of use cases
   - Present tense
   - No fluff

5. **Present for review**

## Feature Structure

```
{docs-path}/features/{name}/
├── README.md      # Overview, key files, usage
└── architecture.md # Design decisions (if complex)
```

## Concept Structure

Single file: `{docs-path}/concepts/{name}.md`
- Definition
- When it applies
- Key considerations
- Codebase examples

## Checkpoint

```
Documentation created at: {path}

- Review → Read documentation
- Edit → Modify
- Complete → Phase 7
- Skip cleanup → End workflow
```

## State Update

```json
{
  "phase": "removal",
  "documentation": { "type": "feature", "path": "{docs-path}/features/..." }
}
```
