# 03. Examples: Start Where Things Break

This chapter turns the ideas into simple examples.

## Example 1: Refactoring a Login API

### Scenario

You have an old login API with messy code.

AI suggests a cleaner service structure.

### What Can Break First

- old mobile apps depend on response fields
- frozen users, deleted users, or users without phone numbers may be handled incorrectly
- token expiration may change
- failed-login risk control may stop working
- the support console may still call the old API

### Unsafe Approach

```text
Ask AI to rewrite the login module and deploy it.
```

This is risky because you do not know all hidden rules in the old system.

### Safer Approach

1. Record the old API behavior.
2. Add tests for normal login, wrong password, frozen users, and old users.
3. Put the new logic behind a feature flag.
4. Run old and new logic together in shadow mode.
5. Compare outputs.
6. Release to a small percentage of traffic.
7. Keep a fast rollback path.

### Prompt AI Like This

```text
Do not refactor directly.
First list the externally observable behavior of the login API.
Then design characterization tests.
The new implementation must keep response fields compatible.
Give me a shadow mode integration point and the fields we should log for differences.
```

## Example 2: Changing an Order State Machine

### Scenario

Orders currently have these states:

```text
created -> paid -> shipped -> completed
created -> canceled
paid -> refunded
```

You want to add:

```text
paid -> preparing -> shipped
```

### What Can Break First

- old code assumes paid can only go to shipped or refunded
- reports do not know the preparing state
- support tools cannot display the new state
- scheduled jobs treat preparing as invalid
- old mobile apps have no text for it

### Unsafe Approach

```text
Only change the backend transition and database enum.
```

The backend may work while surrounding systems break.

### Safer Approach

1. Search every place that reads order status.
2. Add tests for state transitions.
3. Update reports, support tools, and scheduled jobs.
4. Enable the new state for internal orders first.
5. Expand after metrics are healthy.

### Prompt AI Like This

```text
Analyze the impact of adding a preparing order state.
Do not write code yet.
List all modules that may read order status, tests we need, and compatibility concerns.
```

## Example 3: Database Field Migration

### Scenario

You want to split `name` into:

```text
first_name
last_name
```

### What Can Break First

- old services still write `name`
- new services only read `first_name` and `last_name`
- historical data is not backfilled
- rollback becomes incompatible
- search, exports, and reports still depend on `name`

### Unsafe Approach

```text
Delete name and add first_name and last_name immediately.
```

Old code may fail right away.

### Safer Approach

Use three steps:

```text
expand -> backfill -> contract
```

Meaning:

1. expand: add new fields, keep the old field.
2. backfill: copy historical data into the new fields.
3. contract: remove the old field only after no service depends on it.

### Prompt AI Like This

```text
Design a rollback-safe database field migration.
Use expand, backfill, and contract.
Do not delete the old field until the migration is stable.
List tests and rollback steps for each phase.
```

## Example 4: Frontend Page Refactor

### Scenario

A page is messy. You want AI to split it into components.

### What Can Break First

- form default values change
- submit payload changes
- loading state disappears
- error messages change
- analytics events disappear
- permission-based buttons display incorrectly
- mobile layout breaks

### Unsafe Approach

```text
Ask AI to refactor the whole page using best practices.
```

### Safer Approach

1. List page behavior first.
2. Add interaction tests or screenshot checks.
3. Extract pure display components first.
4. Then extract form logic.
5. Finally extract requests and state management.
6. Run tests and preview after each step.

### Prompt AI Like This

```text
Only extract pure display components.
Do not change request logic or form submission logic.
Keep visible text, analytics fields, and permission checks unchanged.
List any user-visible behavior that may change.
```

## Summary

Good engineering is usually not:

```text
Make a big change and hope it works.
```

It is:

```text
Know what can break, protect it with tests, replace it in small steps, and release with visibility.
```

