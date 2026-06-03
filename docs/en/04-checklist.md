# 04. Beginner Checklist

Use this checklist before asking AI to change code, refactor a system, or handle technical debt.

## 1. Do Not Rush Into Code

Ask yourself:

- What is the goal of this change?
- Is it a bug fix, feature, performance improvement, or technical debt cleanup?
- Which behaviors must not change?
- Which users or systems may be affected?
- What is the worst case?

If you cannot explain the goal, do not ask AI to write code yet.

## 2. Find What Can Break First

Look at:

- core business flows
- code without tests
- shared code used by many modules
- database migrations
- permission logic
- cache logic
- async jobs
- third-party dependencies
- state machines

Ask AI:

```text
Do not change code yet.
Find the most likely regression points in this module and rank them by risk.
```

## 3. Add Tests First

Tests do not have to be perfect at the beginning.

Start with three types:

- happy path tests: normal user behavior succeeds
- error path tests: bad input, no permission, or missing data behaves correctly
- old behavior tests: existing behavior stays the same after refactor

Ask AI:

```text
Add characterization tests based on the current code.
The goal is to lock current external behavior, not to change the implementation.
```

## 4. Control AI's Change Scope

Do not only say:

```text
Optimize this.
```

Say:

```text
Only modify these files:
- ...

Requirements:
- keep the public API unchanged
- do not change response fields
- do not add new dependencies
- do not remove compatibility logic
- add tests before changing implementation
- explain remaining risks at the end
```

## 5. Prepare Shadow Replacement

For risky changes, ask:

- Can old and new logic run together?
- Can the new logic only log results without affecting users?
- Can we compare old and new outputs?
- Can we use a feature flag?
- Can we turn the new logic off quickly?

Ask AI:

```text
Design shadow mode for this change.
The old logic still serves users.
The new logic only computes and logs differences.
Give me the flag, log fields, metrics, and rollback path.
```

## 6. Check Before Release

Before release, ask:

- Did tests pass?
- Do we have monitoring?
- Do we have alerts?
- Do logs help us debug?
- Do we have a feature flag?
- Can we roll back?
- Can rollback cause data inconsistency?
- Who will notice the problem first?

## 7. A Minimal AI Prompt Template

You can copy this:

```text
I want to change this module, but I do not want to break old behavior.

Please do this in order:
1. Summarize the externally observable behavior.
2. List the most likely regression points.
3. Design the smallest useful test set.
4. Explain where shadow mode or fallback is needed.
5. Make the smallest change without changing the public API.
6. List release metrics and rollback steps.

Constraints:
- Do not add new dependencies unless you explain why first.
- Do not do a large refactor.
- Do not change response fields.
- Do not remove compatibility logic.
```

## Final Reminder

> AI can help you write code, but it cannot take responsibility for engineering judgment.

The more you understand what can break and how your stack fails, the better AI becomes as your execution power.

