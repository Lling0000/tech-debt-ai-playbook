# 02. Hidden Stack Knowledge: How You Drive AI

## What Is Hidden Knowledge?

Explicit knowledge is easy to write in tutorials.

For example:

- how to create a React component
- how to write an Express route
- how to connect to a database
- how to call an API

Hidden knowledge is harder to explain, but it matters in production.

For example:

- what usually goes wrong in this framework
- which default settings are unsafe in production
- which patterns work with small data but fail with large data
- which elegant-looking abstractions are hard to debug
- which caches can return stale data
- which async flows can run twice
- which changes can break old clients

## Why Hidden Knowledge Helps You Drive AI

AI is good at generating code, but it does not know your production reality.

If you only say:

```text
Optimize this API.
```

AI may:

- change function structure
- extract services
- switch libraries
- change response shapes
- merge logic
- delete code it thinks is duplicated

These actions can look like improvements while breaking existing behavior.

If you have hidden knowledge, you can say:

```text
This API is used by old mobile apps and the support console.
Do not change response fields.
First list the externally observable behavior.
Add minimal regression tests.
Put the new implementation behind a feature flag.
Before release, compare old and new outputs in shadow mode.
```

Now AI is not making the judgment for you. It is executing your judgment.

## AI Drives You vs You Drive AI

AI drives you when:

- you do not know where the risks are
- AI gives a complete-looking plan
- you accept it because it sounds professional
- changes become larger and larger
- you ask AI to fix problems after they appear
- eventually you cannot explain why the system changed this way

You drive AI when:

- you define the goal and boundaries first
- you ask AI to expose its assumptions
- you ask AI to find risk points
- you ask AI to add tests
- you control the change size
- you verify results with tests, logs, and metrics

## Beginner-Friendly Prompts

When you want AI to change code, do not start with "refactor this".

Start with:

```text
Do not change code yet.
Read this module and list:
1. Its externally observable behavior.
2. Which behavior other modules may depend on.
3. The most likely regression points.
4. The tests we should add first.
5. Where a replacement needs fallback.
```

When you are ready for code changes, ask:

```text
Only modify this file.
Keep the external interface unchanged.
Add characterization tests first to lock current behavior.
Then make the smallest implementation change.
Do not add new dependencies.
Finally, explain the remaining regression risks.
```

When you are preparing a risky release, ask:

```text
Design a shadow mode plan.
Requirements:
1. The old logic still serves users.
2. The new logic only computes beside it.
3. Log differences between old and new outputs.
4. Use a feature flag.
5. Allow quick shutdown.
6. List the metrics we should monitor.
```

## Stack Knowledge Is Not For Showing Off

Knowing a stack is not about using more buzzwords.

It helps you know:

- where AI should not improvise
- which changes need tests
- which default solutions are not production-safe
- when to move in small steps
- when to keep the old logic as fallback

A better sentence is:

> Stack names are not that important.  
> Stack failure modes are very important.

