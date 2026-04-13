---
name: reviewing-plans
description: Use when reviewing design docs or implementation plans before execution begins
---

# Reviewing Plans

Review design docs and implementation plans through collaborative dialogue before execution.

**Core principle:** One finding at a time, with options. Never summarize or batch.

**Announce at start:** "I'm using the reviewing-plans skill to review these docs."

## The Process

**Phase 1: Load and Study**

Read all three together before presenting anything:
- Design doc completely
- Implementation plan completely  
- Relevant parts of the codebase

Cross-reference to build a complete mental model.

**Phase 2: Identify Findings**

Look for:
- Structural completeness (missing sections, unclear requirements)
- Feasibility (plan assumes things that don't exist in codebase)
- Consistency (design and plan contradict each other)
- YAGNI violations (over-engineering, unnecessary features)
- Test coverage gaps
- Task granularity (steps should be 2-5 min, not 30 min)

**Phase 3: Present and Resolve**

For each finding (one at a time):
1. Describe the issue with evidence from docs and codebase
2. Propose 2-3 options with trade-offs
3. Lead with your recommendation and explain why
4. Discuss until agreement
5. Only then move to the next finding

**Phase 4: Update Docs**

After all findings resolved, apply agreed changes and commit.

## Key Principles

- **One finding at a time** - Never batch, never summarize, never "here are all 8 issues"
- **Always propose options** - Even if user already suggested a solution, present 2-3 options with your recommendation
- **Codebase as evidence** - If user pushes back, explore codebase together
- **Agreement before moving on** - Don't proceed to next finding until current one is resolved

## Red Flags

These thoughts mean you're rationalizing:

| Thought | Reality |
|---------|---------|
| "One-at-a-time would take forever" | It ensures each finding gets proper attention. Do it anyway. |
| "This is overkill / unnecessary ceremony" | The process exists for a reason. Follow it. |
| "User already decided, options are performative" | Options ensure we considered alternatives. Always present them. |
| "Being pragmatic" | "Pragmatic" often means skipping the process. Don't. |
| "Just give quick highlights" | Quick highlights = batching. One at a time. |
| "These are minor, let implementer figure it out" | Present each finding with options. Let user decide priority. |

## When Findings Aren't Issues

If discussion reveals a finding isn't actually a problem, that's fine. "Not an issue" is a valid resolution. The point is to discuss and agree, not to force changes.
