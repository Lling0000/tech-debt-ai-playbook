# 01. Core Idea: The Stack Is Not a Religion

## The Short Version

"The stack is not that important" does not mean stack knowledge is useless.

It means we should not worship stack names.

A weak belief looks like this:

```text
If we move to a newer stack, the system will become good.
```

A stronger belief looks like this:

```text
A stack is a tool.
The system improves when you understand risk, verify changes, and keep a safe rollback path.
```

## A Common Beginner Mistake

When people see an old project, messy code, or technical debt, they often jump to:

- Should we change frameworks?
- Should we rewrite everything?
- Should we use microservices?
- Should we use Kubernetes?
- Should we ask AI to refactor the whole thing?

These questions are not always wrong, but they usually come too early.

Better first questions are:

- What is the most important business path?
- Which old behaviors must stay the same?
- Which areas have no tests?
- Which changes can affect real users?
- Can we roll back quickly?
- Do we have monitoring that can tell us when something is wrong?

## What Does "Break First" Mean?

"Break first" means the area most likely to fail.

It may be:

- a core function with no tests
- a shared helper used by many modules
- a complex state machine
- a database migration
- cache logic
- permission logic
- payment, order, inventory, or login flows
- places that depend on third-party services

If you do not know what can break first, you do not know what your tests should protect.

## What Does "Collapse First" Mean?

Some failures stay local.

Some failures spread.

For example:

- if login breaks, nobody can enter the system
- if permissions break, private data may leak
- if order status is wrong, payment, inventory, and shipping may all become wrong
- if a migration is wrong, old and new services may read incompatible data
- if a message queue retries incorrectly, users may be charged twice

These are load-bearing areas.

The first goal is not to make the code pretty. The first goal is to protect these areas.

## Test Driven Does Not Have To Be Rigid

For beginners, do not start by arguing about the strict definition of TDD.

Use this simpler rule:

> Before changing dangerous code, write tests that describe the behavior you do not want to break.

If you refactor a login API, tests should answer:

- Can a user log in with the correct password?
- What happens with the wrong password?
- What happens to frozen users?
- Can old users without phone numbers still log in?
- Did the token format or expiration time change?

These tests are not ceremony. They protect hidden behavior.

## What Is Shadow Mode?

Shadow mode means:

> The new implementation runs beside the old one, receives the same input, but does not affect real users yet.

For example, the old login logic still returns the real result.

The new login logic also computes a result, but only writes logs. You compare old and new outputs.

If the difference is small and the metrics are healthy, you can gradually shift traffic.

Benefits:

- the new logic sees real traffic early
- users are not affected by the new logic yet
- you can measure differences
- if something is wrong, you do not need an emergency rollback because the new logic has not taken over

## Summary

The stack is not a religion.

The core loop is:

```text
know the risk -> lock behavior with tests -> replace in small steps -> compare old and new -> release with rollback
```

If you think this way, AI becomes your tool.

If you only ask AI to "make the architecture more modern", AI may become your steering wheel.

