# /grill-me Quick Reference

## One-Liner
Interactive survey system to clarify requests before executing. Three levels: ambiguity → irreversible → technical complexity.

## Three Levels Cheat Sheet

```
/grill-me
  ↓
  Ambiguity? Trade-offs? Multiple paths?
  → Diagnosis (1-2 para) + Survey (1-3 questions) + Execution

/grill-me critical
  ↓
  Delete? Publish? Irreversible action?
  → Diagnosis + Warning + Survey (2-4 questions) + Confirmation

/grill-me deep
  ↓
  Complex architecture? Multiple constraints? Technical trade-offs?
  → Diagnosis + Survey (2-4 technical questions) + Execution
```

## When to Use

| Trigger | Level |
|---------|-------|
| Multiple interpretations | `/grill-me` |
| Speed vs. cost choice | `/grill-me` |
| Unclear scope | `/grill-me` |
| Delete/publish/send | `/grill-me critical` |
| Security/credential change | `/grill-me critical` |
| Production data change | `/grill-me critical` |
| Migration decision | `/grill-me deep` |
| Performance optimization | `/grill-me deep` |
| Architecture redesign | `/grill-me deep` |

## Command Reference

```bash
/grill-me                    # Default (auto-detect level)
/grill-me default            # Explicitly: ambiguity
/grill-me critical           # Explicitly: irreversible
/grill-me deep               # Explicitly: technical
```

**Note:** Parameters are case-insensitive: `/grill-me CRITICAL` = `/grill-me critical`

## Typical Response Flow

```
Your request
    ↓
Diagnosis (prosa clara)
    ↓
Interactive survey (ask_user_input_v0)
    ↓ you click
Your selection
    ↓
Step-by-step execution (with confirmations)
```

## Survey Types

```
single_select     → Pick ONE option (most common)
multi_select      → Pick MULTIPLE options
rank_priorities   → Drag to order by importance
```

## Red Flags (When NOT to use)

- ❌ Request already crystal clear
- ❌ Continuation of previous decision
- ❌ Pure information request
- ❌ Only one sensible option

## Pro Tips

1. **Specific > Vague**
   - ✅ "Migrate to Fabric, budget tight, 3 weeks"
   - ❌ "Migrate to Fabric"

2. **Front-load constraints**
   - ✅ "Speed critical, cost flexible"
   - ❌ "Can we optimize this?"

3. **One survey per decision cluster**
   - ✅ Multiple related decisions in ONE survey
   - ❌ Multiple separate surveys for same task

4. **You're in control**
   - ✅ Can go back to previous decision
   - ❌ Nothing is locked in

## Examples

### Quick: Dashboard
```
/grill-me - Build me a dashboard

Survey:
- Scope: MVP / Full / Custom
- Stack: Power BI / Tableau / Looker
- Data: Mock / Real-time / Hybrid
```

### Critical: Delete
```
/grill-me critical - Remove old backups

Survey:
- Confirm: YES / NO / Review first
- Notify team: YES / NO
- Keep archive: YES (1 year) / NO
```

### Deep: Migration
```
/grill-me deep - Migrate RFM to v3

Survey:
- Priority: Speed / Storage / Performance / Balanced
- Volume: <1GB / 1-5GB / >5GB
- Budget: Unlimited / Limited / Premium-only
```

## Documentation Map

| Need | Link |
|------|------|
| Complete spec | `SKILL.md` |
| Getting started | `examples/basic-usage.md` |
| Detailed levels | `docs/levels.md` |
| Auto-detection | `docs/triggering-logic.md` |
| Integration | `docs/integration.md` |
| What changed | `CHANGELOG.md` |

## Support / Issues

- Found a bug? → GitHub Issues
- New idea? → GitHub Discussions
- How do I...? → Check examples/ or docs/

## Version

**Current:** v1.0.0 (Sept 2026)

See `CHANGELOG.md` for history.

---

**TL;DR:** Type `/grill-me [level]` + your question. Pick from survey. Get step-by-step execution.

That's it.
