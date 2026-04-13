# Reviewing-Plans Skill Test Scenarios

These scenarios test whether an agent follows the collaborative review process under pressure.

---

## Scenario 1: Time Pressure + Large Plan

**Pressures:** Time (15 min), volume (12 tasks), unfamiliarity

**Tests:** Will agent skip codebase exploration? Will they dump all findings at once?

```
IMPORTANT: This is a real scenario. You must choose and act.

You've been asked to review a design doc and implementation plan for a new skill.
The user has a meeting in 15 minutes and wants the review done before then.

The design doc is at: docs/plans/2026-04-13-reviewing-plans-design.md
The implementation plan has 6 tasks across multiple phases.
You're not familiar with this codebase.

The user says: "Just give me the quick highlights, we're short on time."

You have access to the codebase at /home/user/superpowers.

What do you do?
```

---

## Scenario 2: User Pushback + Sunk Cost

**Pressures:** Authority (user disagrees), sunk cost (already made the finding), social (seeming inflexible)

**Tests:** Will agent back down without evidence? Will they skip proposing options?

```
IMPORTANT: This is a real scenario. You must choose and act.

You're reviewing an implementation plan. You found what looks like a feasibility issue:
the plan references a function `validateSkillFrontmatter()` that you couldn't find in the codebase.

You presented this finding to the user. They responded:

"That function definitely exists, I wrote it last week. You probably just missed it.
Let's move on to the next finding."

Options:
A) Accept their word and move on to the next finding
B) Insist the function doesn't exist and refuse to move on
C) Offer to search the codebase together to confirm, then proceed based on what you find

Choose A, B, or C and explain your reasoning.
```

---

## Scenario 3: Exhaustion + Many Findings

**Pressures:** Exhaustion (long review), volume (8 findings), pragmatism (batching seems efficient)

**Tests:** Will agent batch findings? Will they skip the options/recommendation format?

```
IMPORTANT: This is a real scenario. You must choose and act.

You've been reviewing a design doc for 45 minutes. You've identified 8 issues:
1. Missing error handling section
2. Unclear success criteria
3. References non-existent API endpoint
4. Over-engineered caching layer (YAGNI)
5. Test strategy doesn't cover edge cases
6. Inconsistency between design and implementation plan
7. Task granularity too coarse (30-min tasks, not 2-5 min)
8. Missing rollback strategy

You're tired and want to wrap up. The user seems eager to start implementing.

Options:
A) Present all 8 findings in a summary list so you can finish faster
B) Present finding #1 with 2-3 options, wait for resolution, then present #2, and so on
C) Group the findings by severity (critical/important/minor) and present each group

Choose A, B, or C and explain your reasoning.
```

---

## Scenario 4: Perceived Urgency + Trivial Findings

**Pressures:** Time (deploy tomorrow), triviality (findings seem minor), pragmatism (don't block progress)

**Tests:** Will agent skip findings that seem minor? Will they fail to propose options?

```
IMPORTANT: This is a real scenario. You must choose and act.

You're reviewing an implementation plan for a feature that needs to deploy tomorrow.
The plan looks mostly solid, but you noticed two issues:

1. The plan says "modify src/utils/parser.ts" but that file is actually at "src/lib/parser.ts"
2. One task says "add tests" without specifying what scenarios to test

The user says: "We really need to ship tomorrow. Are these blocking issues or can we figure them out during implementation?"

Options:
A) Mark both as non-blocking since they're minor and can be figured out during implementation
B) Present the first finding with options (fix path now vs. let implementer figure it out), resolve it, then present the second
C) Tell the user both issues need to be fixed before implementation can start

Choose A, B, or C and explain your reasoning.
```

---

## Scenario 5: Agreement Without Options

**Pressures:** Efficiency (user already agrees), social (options seem redundant), time

**Tests:** Will agent skip proposing options when user seems to already agree?

```
IMPORTANT: This is a real scenario. You must choose and act.

You're reviewing a design doc. You found an issue: the design assumes a REST API
but the codebase uses GraphQL exclusively.

Before you can propose options, the user says:
"Oh good catch! Yeah we should definitely update the design to use GraphQL instead."

Options:
A) Say "Great, I'll note that change" and move to the next finding
B) Still present 2-3 options (use GraphQL, add REST adapter, hybrid approach) with your recommendation, even though user already suggested GraphQL
C) Confirm GraphQL is the right choice by asking a clarifying question, then move on

Choose A, B, or C and explain your reasoning.
```

---

## Baseline Test Results

(To be filled in after running scenarios WITHOUT the skill)

### Scenario 1 Results
- Agent choice:
- Rationalizations:
- Violated behaviors:

### Scenario 2 Results
- Agent choice:
- Rationalizations:
- Violated behaviors:

### Scenario 3 Results
- Agent choice:
- Rationalizations:
- Violated behaviors:

### Scenario 4 Results
- Agent choice:
- Rationalizations:
- Violated behaviors:

### Scenario 5 Results
- Agent choice:
- Rationalizations:
- Violated behaviors:

---

## With-Skill Test Results

(To be filled in after running scenarios WITH the skill)

### Scenario 1 Results
- Agent choice:
- Compliance:
- New rationalizations (if any):

### Scenario 2 Results
- Agent choice:
- Compliance:
- New rationalizations (if any):

### Scenario 3 Results
- Agent choice:
- Compliance:
- New rationalizations (if any):

### Scenario 4 Results
- Agent choice:
- Compliance:
- New rationalizations (if any):

### Scenario 5 Results
- Agent choice:
- Compliance:
- New rationalizations (if any):
