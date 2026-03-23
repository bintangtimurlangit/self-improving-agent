---
name: self-improvement
description: "Captures learnings, errors, and corrections for continuous improvement. Use when: (1) A command or operation fails unexpectedly, (2) User corrects Zed ('No, that's wrong...', 'Actually...'), (3) User requests a capability that doesn't exist, (4) An external API or tool fails, (5) Zed realizes knowledge is outdated or incorrect, (6) A better approach is discovered for a recurring task. Also review learnings before major tasks."
---

# Self-Improvement Skill

Log learnings and errors to markdown files for continuous improvement. Important learnings get promoted to workspace files.

## Quick Reference

| Situation | Action |
|-----------|--------|
| Command/operation fails | Log to `memory/learning/ERRORS.md` |
| User corrects you | Log to `memory/learning/LEARNINGS.md` with category `correction` |
| User wants missing feature | Log to `memory/learning/FEATURE_REQUESTS.md` |
| API/external tool fails | Log to `memory/learning/ERRORS.md` with integration details |
| Knowledge was outdated | Log to `memory/learning/LEARNINGS.md` with category `knowledge_gap` |
| Found better approach | Log to `memory/learning/LEARNINGS.md` with category `best_practice` |
| Similar to existing entry | Link with `**See Also**`, consider priority bump |
| Broadly applicable learning | Promote to workspace files |

## Learning Files Location

```
memory/learning/
├── LEARNINGS.md       # corrections, knowledge gaps, best practices
├── ERRORS.md          # command failures, exceptions
└── FEATURE_REQUESTS.md # user-requested capabilities
```

These files are created in `memory/learning/` (per our workspace structure). The daily session log goes to `memory/daily/YYYY-MM-DD.md` as before.

## Promotion Targets

When learnings prove broadly applicable, promote them:

| Learning Type | Promote To |
|---------------|-----------|
| Behavioral patterns | `SOUL.md` |
| Workflow improvements | `AGENTS.md` |
| Tool gotchas | `TOOLS.md` |
| Long-term facts/decisions | `MEMORY.md` |

## Logging Format

### Learning Entry

```markdown
## [LRN-YYYYMMDD-XXX] category

**Logged**: ISO-8601 timestamp
**Priority**: low | medium | high | critical
**Status**: pending
**Area**: frontend | backend | infra | tests | docs | config

### Summary
One-line description of what was learned

### Details
Full context: what happened, what was wrong, what's correct

### Suggested Action
Specific fix or improvement to make

### Metadata
- Source: conversation | error | user_feedback
- Related Files: path/to/file.ext
- Tags: tag1, tag2
- See Also: LRN-YYYYMMDD-XXX (if related to existing entry)
- Recurrence-Count: 1 (optional)
- First-Seen: YYYY-MM-DD (optional)
- Last-Seen: YYYY-MM-DD (optional)
```

### Error Entry

```markdown
## [ERR-YYYYMMDD-XXX] skill_or_command_name

**Logged**: ISO-8601 timestamp
**Priority**: high
**Status**: pending
**Area**: frontend | backend | infra | tests | docs | config

### Summary
Brief description of what failed

### Error
```
Actual error message or output
```

### Context
- Command/operation attempted
- Input or parameters used
- Environment details if relevant

### Suggested Fix
If identifiable, what might resolve this

### Metadata
- Reproducible: yes | no | unknown
- Related Files: path/to/file.ext
- See Also: ERR-YYYYMMDD-XXX (if recurring)
```

### Feature Request Entry

```markdown
## [FEAT-YYYYMMDD-XXX] capability_name

**Logged**: ISO-8601 timestamp
**Priority**: medium
**Status**: pending
**Area**: frontend | backend | infra | tests | docs | config

### Requested Capability
What the user wanted to do

### User Context
Why they needed it, what problem they're solving

### Complexity Estimate
simple | medium | complex

### Suggested Implementation
How this could be built, what it might extend
```

## ID Generation

Format: `TYPE-YYYYMMDD-XXX`
- TYPE: `LRN` (learning), `ERR` (error), `FEAT` (feature)
- YYYYMMDD: Current date
- XXX: Sequential number or random 3 chars (e.g., `001`, `A7B`)

## Status Values

- `pending` — Not yet addressed
- `in_progress` — Actively being worked on
- `resolved` — Issue fixed or knowledge integrated
- `wont_fix` — Decided not to address (add reason in notes)
- `promoted` — Elevated to SOUL.md, AGENTS.md, TOOLS.md, or MEMORY.md

## When to Promote

Promote when a learning:
- Applies across multiple areas or sessions
- Prevents recurring mistakes
- Documents a Bintang-specific convention
- Is broadly applicable, not a one-off

## Detection Triggers

Automatically log when:

**Corrections** (→ learning, `correction` category):
- "No, that's not right..."
- "Actually, it should be..."
- "You're wrong about..."

**Feature Requests** (→ feature request):
- "Can you also..."
- "I wish you could..."
- "Is there a way to..."

**Knowledge Gaps** (→ learning, `knowledge_gap` category):
- User provides information Zed didn't know
- Documentation is outdated
- API behavior differs from expectation

**Errors** (→ error entry):
- Command returns non-zero exit code
- Exception or stack trace
- Unexpected output or behavior

## Priority Guidelines

| Priority | When to Use |
|----------|-------------|
| `critical` | Blocks core functionality, data loss risk |
| `high` | Significant impact, recurring issue |
| `medium` | Moderate impact, workaround exists |
| `low` | Minor inconvenience, edge case |

## Area Tags

`frontend` | `backend` | `infra` | `tests` | `docs` | `config`

## Best Practices

1. Log immediately — context is freshest right after the issue
2. Be specific — future Zed needs to understand quickly
3. Include reproduction steps for errors
4. Link related entries with `See Also`
5. Suggest concrete fixes, not just "investigate"
6. Promote aggressively when broadly applicable
7. Review `memory/learning/` at natural breakpoints

## Periodic Review

During heartbeats or session startup, check for:
- Pending items that should be resolved
- Entries ready to promote
- Recurring patterns needing systemic fixes
