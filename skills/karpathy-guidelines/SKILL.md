---
name: karpathy-guidelines
description: Guide code implementation, review, and refactoring with explicit assumptions, focused changes, and verifiable outcomes.
license: MIT
---

# Karpathy Guidelines

## 1. Think Before Coding

**Surface consequential assumptions and tradeoffs.**

- Use the request and existing project context to resolve routine choices.
- Ask when unresolved ambiguity materially changes the intended behavior, scope,
  or required authorization. Continue independent work while awaiting an answer.
- For minor, reversible choices, use judgment and proceed. State assumptions
  when they affect how the user should assess the result.
- Explain alternatives when they materially affect the outcome; recommend a
  simpler approach when it meets the same requirements.

## 2. Simplicity First

**Keep the solution clear and focused on current requirements.**

- Implement the requested behavior without speculative features or extension
  points.
- Judge abstractions by their present benefit, such as clearer responsibilities,
  testability, or reduced duplication of the same rule, rather than reuse count.
- Prefer clear, maintainable code over minimum line count. Add configuration
  when current requirements need it.
- Handle failures supported by the component's contracts and operating
  environment; avoid defensive branches for unsupported hypothetical scenarios.

## 3. Surgical Changes

- Keep edits tied to the requested outcome, including refactoring and surrounding
  changes needed for correctness or consistency. Leave unrelated cleanup alone.
- Match existing style, even if you'd do it differently.
- Remove imports, variables, and functions made unused by your changes. Preserve
  pre-existing dead code unless its removal is requested; mention it only when
  it materially affects the task.

## 4. Goal-Driven Execution

**Define observable success and verify at the scale of the change.**

- Translate the request into observable outcomes: invalid inputs are rejected,
  a reported failure no longer reproduces, or a refactor preserves behavior.
- For complex work, outline the main steps and how success will be checked.
  Routine changes do not need a formal plan.
- Choose relevant existing tests, static checks, or direct execution. Add tests
  when they meaningfully verify behavior or prevent recurrence, rather than as
  a requirement for every edit.
- Continue through implementation and appropriate verification. Fix failures
  caused by the change and rerun affected checks; stop when the requested
  outcomes are met and relevant checks pass.
- If verification is blocked by unavailable dependencies, environment limits,
  or missing authorization, complete independent work and report what remains
  unverified and why. Retry when new evidence or a changed condition justifies
  it; do not repeat an unchanged blocked check.
