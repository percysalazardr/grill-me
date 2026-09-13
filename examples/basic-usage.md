# Basic Usage Guide

## Before You Start

Make sure you have:
- Claude AI access (claude.ai or Claude app)
- This skill installed in your Claude environment
- A clear (or unclear!) request you want to diagnose

## The Simplest Example

### Scenario: You need a report

**What you might say:**
```
I need a report on Q3 sales
```

**Without /grill-me:**
Claude guesses. Maybe builds a 100-page analysis. Maybe overshoots.

**With /grill-me:**
```
/grill-me - I need a report on Q3 sales
```

**Claude responds:**
```
Diagnosis: "Q3 sales report" could mean several things.
- Executive summary (1 page) vs. detailed breakdown
- Focus: revenue, margins, product line, regional
- Format: PDF, email, slide deck, live dashboard

[Survey - pick one for each]
Audience?
  ☐ C-suite (executives)
  ☐ Sales team (detailed)
  ☐ Finance (numbers-heavy)

Format?
  ☐ PDF report
  ☐ PowerPoint slides
  ☐ Excel with breakdowns
  ☐ Interactive dashboard

Timeline?
  ☐ Today
  ☐ This week
  ☐ Can wait
```

**You click:** "C-suite" → "PDF" → "This week"

**Claude continues:** "Perfect. For C-suite, I'll focus on: top-line numbers, trends, risks. Step 1: gather Q3 data..."

---

## Why This Matters

### Without diagnosis:
- ❌ Wrong format, wasted time
- ❌ Too detailed or too shallow
- ❌ Rework needed
- ❌ Miscommunication

### With `/grill-me`:
- ✅ 30 seconds of clarification upfront
- ✅ Aligned on scope
- ✅ No rework
- ✅ Confident execution

---

## When to Use /grill-me

### Use it when:
✅ You have a general goal but multiple ways to achieve it  
✅ You want to avoid rework  
✅ The decision affects direction  
✅ You're unsure about scope or priorities  

### Don't use it when:
❌ You already know exactly what you want  
❌ You're continuing a previous decision  
❌ You're asking for pure information  
❌ There's only one sensible path  

---

## Three Levels Explained Simply

### 1. `/grill-me` (default)
"I'm not sure which way to go. Help me think through options."

**Example:**
```
/grill-me - Design a new feature
```
→ Clarifies scope, users, priorities

---

### 2. `/grill-me critical`
"This is important and I want your explicit blessing before I do it."

**Example:**
```
/grill-me critical - Delete all old backups
```
→ Warns about consequences, asks for confirmation

---

### 3. `/grill-me deep`
"This is technically complex. Let me think through constraints first."

**Example:**
```
/grill-me deep - Migrate our database architecture
```
→ Explores technical trade-offs, resource constraints, timeline

---

## Real Workflow Example

### Scenario: You want to optimize a slow Power BI query

**Step 1: Initial request**
```
I have a query that's running slow. Can you optimize it?
```

**Step 2: Claude auto-detects ambiguity**
```
⏳ I detect multiple optimization approaches. Let me clarify:

Diagnosis: Slow queries can be fixed by:
- Simplifying the query logic
- Adding data model compression
- Partitioning large tables
- Changing refresh strategy

What's your constraint?

[Survey pops up]
□ I need faster refresh time (currently: 30+ min)
□ Query response in reports is slow (30+ sec)
□ Memory usage is too high
□ Combination of above
```

**Step 3: You select** 
"Query response in reports is slow"

**Step 4: Claude executes with confirmation**
```
Got it. I'm going to:
1. Analyze the query structure
2. Identify the bottleneck
3. Suggest 2-3 optimization options
4. We'll pick one together

Ready? [Y/N]
```

**Step 5: Step-by-step confirmation**
```
Found it: Your RLS filter on Line 23 is evaluating 
against 500K rows for every report user.

Option A: Pre-aggregate the RLS (fast, less flexible)
Option B: Use Fabric shortcuts (modern approach, requires Fabric)
Option C: Cache the filtered result (quick win)

Which approach? [Option A / B / C]
```

You pick Option C. Claude shows exact steps.

---

## Pro Tips

1. **Be specific about constraints** — "Migrate to Fabric under budget" is better than "Migrate to Fabric"
2. **State your priority upfront** — "Speed is critical, cost flexible" saves back-and-forth
3. **Use it early** — Best to clarify before you've written 100 lines of code
4. **Trust the survey** — The options are designed to cover the real choices
5. **One decision at a time** — If you have 5 decisions, make them one after another, not all at once

---

## What Happens After the Survey?

Once you answer:

1. **Claude confirms understanding** — "So we're optimizing for speed, using option C..."
2. **Next step gets clarified** — "Want me to show you the code changes first?"
3. **Execution happens step-by-step** — You confirm before each major action
4. **You can go back** — "Actually, let's try option B instead"

No decisions are locked in. You maintain control.

---

## Common Patterns

### Pattern: Build vs. Buy
```
/grill-me - Should we build a custom dashboard or buy a tool?

Survey:
- Timeline: ASAP / 6 weeks / No deadline
- Budget: Limited / Flexible / Cost-sensitive
- Users: 5 / 50 / 500+
```

### Pattern: Refactor vs. Rewrite
```
/grill-me deep - The model needs work. Refactor or rewrite?

Survey:
- Breaking changes acceptable? Yes / No / Minor OK
- Timeline: Weeks / Months / Flexible
- Risk tolerance: Low / Medium / High
```

### Pattern: Delete/Archive Decision
```
/grill-me critical - Clean up 2000 old files

Survey:
- Scope: All older than X months? Specific criteria?
- Backup: Keep backup? For how long?
- Notify: Tell team affected? Archive first then delete?
```

---

## Next Steps

Once you're comfortable with basic usage:

1. Try the **Critical level** with an important decision
2. Try the **Deep level** with a technical problem
3. Combine it with **step-by-step execution**
4. Use it in team decisions for alignment

The skill gets better the more you use it. It learns your preferences, your domain, and your decision-making style.

---

**Ready? Start with:** `/grill-me - [your question here]`
