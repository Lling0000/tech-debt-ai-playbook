# 00. Preface

This guide is not about choosing the "best" technology stack.

It is about building a stronger engineering instinct:

> Do not start with the stack.  
> Start with what can break, how you will detect it, and how you will roll back.

When beginners look at messy code or technical debt, they often think experienced engineers are better because they know more frameworks, languages, and tools.

Those things help, but the deeper difference is judgment.

Experienced engineers know:

- which simple-looking areas are actually risky
- which code works today but will be hard to change tomorrow
- which refactors look clean but can break old behavior
- which AI-generated changes look complete but ignore production risk
- which tests must exist before changing dangerous code

## A Small Story

Imagine you have an old login API.

The code is messy. AI reads it and says:

```text
This module mixes too many responsibilities.
I suggest splitting it into auth service, token service, and user service.
```

That sounds reasonable.

But if you follow it blindly, you may break hidden behavior:

- old mobile apps still depend on old response fields
- some users have no phone number, and the old logic still allows login
- failed login attempts trigger risk control
- another service assumes tokens expire in 7 days
- the customer support console calls the same API

AI may not know any of this.

A safer path is:

1. Record the current external behavior.
2. Add tests that lock down that behavior.
3. Identify the riskiest change points.
4. Run the new logic in shadow mode first.
5. Compare old and new outputs.
6. Gradually shift traffic only after the result is stable.

That is engineering judgment.

## The Main Loop

This playbook follows one loop:

```text
identify risk -> write tests -> make small changes -> shadow run -> canary release -> keep rollback
```

This loop matters more than any single framework.

At the same time, the more hidden knowledge you have about a stack, the better you can see its failure modes. That is how you give AI clear boundaries and make it execute your judgment instead of replacing it.

