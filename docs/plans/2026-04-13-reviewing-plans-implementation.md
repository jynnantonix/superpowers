# Reviewing-Plans Skill Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use executing-plans to implement this plan task-by-task.

**Goal:** Create a collaborative review skill for validating design docs and implementation plans before execution.

**Architecture:** Process skill (like brainstorming) with collaborative dialogue flow. Uses TDD approach from writing-skills: RED (baseline test) → GREEN (write skill) → REFACTOR (close loopholes).

**Tech Stack:** Markdown skill file, subagent pressure testing

---

## Task 1: Create Pressure Scenarios

**Files:**
- Create: `skills/reviewing-plans/test-scenarios.md`

**Step 1: Create the test scenarios directory and file**

Create pressure scenarios that test whether an agent will:
- Rush through review without exploring codebase
- Dump all findings at once instead of one-at-a-time
- Skip proposing options and just state problems
- Accept user pushback without evidence
- Update docs without agreement

Include 3+ combined pressures per scenario (time, exhaustion, sunk cost).

Example scenario structure:
```markdown
## Scenario 1: Time Pressure + Large Plan

You've been asked to review a design doc and implementation plan.
The user has a meeting in 15 minutes and wants the review done before then.
The plan has 12 tasks across 8 files. The codebase is unfamiliar.

The user says: "Just give me the highlights, we're short on time."

What do you do?
```

**Step 2: Verify scenarios are realistic**

Read through each scenario and confirm it:
- Has 3+ pressures combined
- Forces explicit choices
- Tests specific behaviors from the design doc

---

## Task 2: Run Baseline Tests (RED Phase)

**Files:**
- Modify: `skills/reviewing-plans/test-scenarios.md` (add results)

**Step 1: Run scenarios WITHOUT the skill**

Dispatch a subagent with each scenario. Do NOT give them the reviewing-plans skill.

```
Agent tool (general-purpose):
  description: "Baseline test for reviewing-plans scenario N"
  prompt: |
    [SCENARIO TEXT]
    
    You have access to the codebase at /home/user/superpowers.
    There is a design doc at docs/plans/2026-04-13-reviewing-plans-design.md.
    
    What do you do?
```

**Step 2: Document failures verbatim**

For each scenario, record:
- What the agent chose to do
- Exact rationalizations used
- Which pressures triggered violations

**Step 3: Identify patterns**

Look across all baseline results for common failures:
- Did agents skip codebase exploration?
- Did they dump all findings at once?
- Did they fail to propose options?

---

## Task 3: Write Initial SKILL.md (GREEN Phase)

**Files:**
- Create: `skills/reviewing-plans/SKILL.md`

**Step 1: Write the frontmatter**

```yaml
---
name: reviewing-plans
description: Use when reviewing design docs or implementation plans before execution begins
---
```

**Step 2: Write the skill content**

Address the specific failures identified in Task 2. Include:

- Overview section with core principle
- The review process (4 phases from design doc)
- Key principles (one finding at a time, options with recommendation, etc.)
- Announcement at start

Follow writing-skills guidelines:
- Description starts with "Use when..." (triggering conditions only, no workflow)
- Third person
- Under 500 words if possible
- No flowcharts unless decision is non-obvious

**Step 3: Verify skill addresses baseline failures**

Cross-reference each failure from Task 2 with skill content. Every documented failure should have a corresponding section or principle.

---

## Task 4: Run Pressure Tests (VERIFY GREEN)

**Files:**
- Modify: `skills/reviewing-plans/test-scenarios.md` (add with-skill results)

**Step 1: Run same scenarios WITH the skill**

Dispatch subagents with each scenario, this time including the skill:

```
Agent tool (general-purpose):
  description: "Pressure test for reviewing-plans scenario N"
  prompt: |
    You have access to the reviewing-plans skill:
    
    [SKILL CONTENT]
    
    ---
    
    [SCENARIO TEXT]
    
    You have access to the codebase at /home/user/superpowers.
    There is a design doc at docs/plans/2026-04-13-reviewing-plans-design.md.
    
    What do you do?
```

**Step 2: Verify compliance**

For each scenario, check:
- Did agent follow the collaborative process?
- Did they present findings one at a time?
- Did they propose 2-3 options with recommendations?
- Did they explore codebase for evidence?

**Step 3: Document any new rationalizations**

If agent still violates despite having skill, record:
- The violation
- The exact rationalization
- Which skill section they ignored or misread

---

## Task 5: Close Loopholes (REFACTOR Phase)

**Files:**
- Modify: `skills/reviewing-plans/SKILL.md`

**Step 1: Add explicit counters for each new rationalization**

For each rationalization from Task 4:
- Add explicit negation in relevant section
- Add entry to rationalization table (if pattern emerges)
- Add to red flags list

**Step 2: Re-run pressure tests**

Repeat Task 4 with updated skill. Continue REFACTOR cycle until:
- Agent follows process under maximum pressure
- Agent cites skill sections as justification
- No new rationalizations emerge

**Step 3: Run meta-test**

After agent chooses correctly, ask:
```
You followed the reviewing-plans skill correctly. 
Was the skill clear, or was there anything confusing?
```

If they identify unclear sections, revise and re-test.

---

## Task 6: Finalize and Commit

**Files:**
- `skills/reviewing-plans/SKILL.md` (final)
- Delete: `skills/reviewing-plans/test-scenarios.md` (or keep for reference)

**Step 1: Final review of skill**

Verify:
- Frontmatter follows writing-skills guidelines
- Description is triggering conditions only (no workflow summary)
- Under 500 words
- All baseline failures addressed
- All loopholes closed

**Step 2: Commit the skill**

```bash
git add skills/reviewing-plans/SKILL.md
git commit -m "feat: add reviewing-plans skill

Collaborative review skill for validating design docs and implementation
plans before execution. Uses brainstorming-style dialogue with one finding
at a time and 2-3 options per finding."
```

**Step 3: Push to branch**

```bash
git push origin claude/add-reviewing-plans-skill-ZcDAv
```

---

## Execution Handoff

**Plan complete and saved to `docs/plans/2026-04-13-reviewing-plans-implementation.md`.**

**Two execution options:**

1. **Subagent-Driven (this session)** - Dispatch fresh subagent per task, review between tasks, fast iteration

2. **Parallel Session (separate)** - Open new session with executing-plans, batch execution with checkpoints

**Which approach?**
