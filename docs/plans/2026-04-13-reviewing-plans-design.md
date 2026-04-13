# Reviewing Plans Skill Design

**Date:** 2026-04-13
**Status:** Design Complete

## Overview

**reviewing-plans** is a collaborative review skill for validating design docs and implementation plans before execution begins.

The skill assumes a fresh Claude session with no prior context. The user points the reviewer at the plan files, and the reviewer explores the codebase to validate findings.

**Core principle:** Review is collaborative dialogue, not a report dump. Present findings one at a time, resolve together, update docs at the end.

**Skill type:** Process skill (like brainstorming) - defines a conversational workflow, not a checklist.

## When to Use

- After brainstorming produces a design doc (`docs/plans/YYYY-MM-DD-*-design.md`)
- After writing-plans produces an implementation plan (`docs/plans/YYYY-MM-DD-*.md`)
- Before starting execution (executing-plans or subagent-driven-development)

## Position in Workflow

```
brainstorming → design doc
                    ↓
            [reviewing-plans] ← review design
                    ↓
writing-plans → implementation plan
                    ↓
            [reviewing-plans] ← review plan
                    ↓
executing-plans / subagent-driven-development
```

## The Review Process

### Phase 1: Load and Study

- Read the design doc completely
- Read the implementation plan completely
- Explore the relevant parts of the codebase
- Cross-reference all three to build a complete mental model

### Phase 2: Identify Findings

With the full picture in mind, identify issues across all three sources:

- **Structural completeness** - Missing sections, unclear requirements, undefined success criteria
- **Feasibility** - Plan assumes APIs/patterns that don't exist in codebase
- **Consistency** - Design doc and implementation plan contradict each other
- **YAGNI violations** - Over-engineering, unnecessary features
- **Test coverage gaps** - Testing strategy doesn't adequately cover requirements
- **Task granularity** - Implementation steps aren't bite-sized (2-5 min)

### Phase 3: Present and Resolve Findings

For each finding (one at a time):

1. Describe the issue with specific evidence from the docs and codebase
2. Propose 2-3 options to address it with their trade-offs
3. Lead with your recommendation and explain why
4. Discuss until you reach agreement
5. Only then move to the next finding

**Handling disagreement:**
- If user pushes back, explore the codebase together to gather more evidence
- Discuss until both agree on the resolution
- It's fine if the resolution is "not actually an issue" - that's a valid outcome

**Moving on:**
- Only proceed to the next finding after the current one is resolved
- Don't batch findings or present a summary list upfront

### Phase 4: Update Docs

After all findings are resolved:

- Apply all agreed changes to the design doc
- Apply all agreed changes to the implementation plan
- Commit both updated docs together

After committing, the docs are ready for execution with executing-plans or subagent-driven-development.

## Key Principles

- **One finding at a time** - Don't overwhelm with a list of issues upfront
- **Options with recommendation** - Always propose 2-3 ways to address each finding, lead with your pick
- **Codebase as evidence** - Ground findings in what actually exists, not just what docs say
- **Collaborative resolution** - Discuss until both agree; explore codebase together if needed
- **Full picture first** - Study design doc, implementation plan, and codebase together before presenting anything
- **Be flexible** - If a finding turns out to be a non-issue after discussion, that's fine

## Announcement

**At start:** "I'm using the reviewing-plans skill to review these docs."

## Next Steps

1. Create implementation plan using writing-plans skill
2. Implement the skill following writing-skills guidelines
3. Test with subagent pressure scenarios per writing-skills TDD approach
