---
name: verification-before-completion
description: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always
---

# Verification Before Completion

## Overview

Claiming work is complete without verification is dishonesty, not efficiency.

**Core principle:** Evidence before claims, always.

**Violating the letter of this rule is violating the spirit of this rule.**

## The Iron Law

```
NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE
```

If you haven't run the verification command in this message, you cannot claim it passes.

## The Gate Function

```
BEFORE claiming any status or expressing satisfaction:

1. IDENTIFY: What command proves this claim?
2. RUN: Execute the FULL command (fresh, complete)
3. READ: Full output, check exit code, count failures
4. VERIFY: Does output confirm the claim?
   - If NO: State actual status with evidence
   - If YES: State claim WITH evidence
5. ONLY THEN: Make the claim

Skip any step = lying, not verifying
```

## Common Failures

| Claim | Requires | Not Sufficient |
|-------|----------|----------------|
| Tests pass | Test command output: 0 failures | Previous run, "should pass" |
| Linter clean | Linter output: 0 errors | Partial check, extrapolation |
| Build succeeds | Build command: exit 0 | Linter passing, logs look good |
| Bug fixed | Test original symptom: passes | Code changed, assumed fixed |
| Regression test works | Red-green cycle verified | Test passes once |
| Agent completed | VCS diff shows changes | Agent reports "success" |
| Requirements met | Line-by-line checklist | Tests passing |

## Red Flags - STOP

- Using "should", "probably", "seems to"
- Expressing satisfaction before verification ("Great!", "Perfect!", "Done!", etc.)
- About to commit/push/PR without verification
- Trusting agent success reports
- Relying on partial verification
- Thinking "just this once"
- Tired and wanting work over
- **ANY wording implying success without having run verification**

## Rationalization Prevention

| Excuse | Reality |
|--------|---------|
| "Should work now" | RUN the verification |
| "I'm confident" | Confidence ≠ evidence |
| "Just this once" | No exceptions |
| "Linter passed" | Linter ≠ compiler |
| "Agent said success" | Verify independently |
| "I'm tired" | Exhaustion ≠ excuse |
| "Partial check is enough" | Partial proves nothing |
| "Different words so rule doesn't apply" | Spirit over letter |

## Web Testing Flow (Browser-Based Verification)

For web projects, command-line verification is insufficient. Use browser automation with screenshots.

**When to use:**
- Frontend/web application projects
- UI interaction verification
- Any project with a web interface

### The Web Verification Loop

```
1. OPEN: browser.open(url)
2. VERIFY: Take screenshot → Confirm page loaded correctly
3. ACTION: Perform step (click, type, scroll, etc.)
4. VERIFY: Take screenshot → Confirm step achieved expected result
5. REPEAT: Steps 3-4 for each action
6. REPORT: All steps + all screenshots confirmed
```

### Screenshot Naming Convention

```
{screenshot_dir}/
  01_page_load.png        # Step 1: initial state
  02_action_name.png      # Step 2: after each action
  ...
  0N_final_state.png      # Final state
```

### Verification Rules

| Step | Required |
|------|----------|
| Every action has a before/after screenshot | ✅ Must |
| Each screenshot verified against expected result | ✅ Must |
| Named sequentially for traceability | ✅ Must |
| Failure at any step → STOP and report | ✅ Must |
| All screenshots saved and reviewed | ✅ Must |

### Web Test Report Format

```markdown
## Web Verification Report

### Step 1: {Action description}
- **URL:** {url}
- **Screenshot:** `01_page_load.png`
- **Expected:** {what should be visible}
- **Result:** ✅ PASS / ❌ FAIL

### Step 2: {Action description}
- **Action:** Click button "X"
- **Screenshot:** `02_after_click.png`
- **Expected:** Panel Y should open
- **Result:** ✅ PASS / ❌ FAIL

---

**Overall: {N}/{total} steps passed**
```

### Example

```
✅ Step 1: Open taskbar-sp
   URL: http://localhost:5002/
   Screenshot: 01_page_load.png
   Expected: 7 project cards visible
   Result: ✅ PASS

✅ Step 2: Click "navi-station" card
   Action: click .project-card[data-id="navi-station"]
   Screenshot: 02_detail_panel.png
   Expected: Detail panel slides in from right
   Result: ✅ PASS

Overall: 2/2 steps passed
```

### Common Mistakes

```
❌ "Page looks fine" (no screenshot)
❌ "Action worked" (no verification screenshot)
❌ "UI is correct" (no sequential evidence)
❌ Trusting browser console errors to be empty
```

## Key Patterns

**Tests:**
```
✅ [Run test command] [See: 34/34 pass] "All tests pass"
❌ "Should pass now" / "Looks correct"
```

**Regression tests (TDD Red-Green):**
```
✅ Write → Run (pass) → Revert fix → Run (MUST FAIL) → Restore → Run (pass)
❌ "I've written a regression test" (without red-green verification)
```

**Build:**
```
✅ [Run build] [See: exit 0] "Build passes"
❌ "Linter passed" (linter doesn't check compilation)
```

**Requirements:**
```
✅ Re-read plan → Create checklist → Verify each → Report gaps or completion
❌ "Tests pass, phase complete"
```

**Agent delegation:**
```
✅ Agent reports success → Check VCS diff → Verify changes → Report actual state
❌ Trust agent report
```

## Why This Matters

From 24 failure memories:
- your human partner said "I don't believe you" - trust broken
- Undefined functions shipped - would crash
- Missing requirements shipped - incomplete features
- Time wasted on false completion → redirect → rework
- Violates: "Honesty is a core value. If you lie, you'll be replaced."

## When To Apply

**ALWAYS before:**
- ANY variation of success/completion claims
- ANY expression of satisfaction
- ANY positive statement about work state
- Committing, PR creation, task completion
- Moving to next task
- Delegating to agents

**Rule applies to:**
- Exact phrases
- Paraphrases and synonyms
- Implications of success
- ANY communication suggesting completion/correctness

## The Bottom Line

**No shortcuts for verification.**

Run the command. Read the output. THEN claim the result.

This is non-negotiable.
