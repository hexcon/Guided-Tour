# Plan Template

Output format for `artifacts/{session}/plan.md`.

---

# Implementation Plan

**Session**: {NNN}-{slug}
**Granularity**: {fine | medium | coarse}
**Total Steps**: {count}

## Overview

{2-3 sentences: what will be built, approach}

## Prerequisites

- [ ] {Must exist before starting}

## Steps

| # | Title | Dependencies | Scope |
|---|-------|--------------|-------|
| 001 | {Title} | - | {files} |
| 002 | {Title} | 001 | {files} |

## Dependency Graph

```
001 ─┬─► 002 ─► 004
     └─► 003 ─┘
```

## Rollback Strategy

{High-level: how to recover if implementation fails}
