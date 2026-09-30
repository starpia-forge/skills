---
name: luna-implement
description: Delegate code implementation and fixes to gpt-6-luna at max effort, with main-agent planning and verification. Use only for code changes; exclude document work, skill creation or editing, 2D/3D asset creation or editing, and analysis or planning alone.
---

# Luna Implement

Apply this workflow only to code implementation and fixes, including associated
tests and integration corrections. Do not use it for document work, skill
creation or editing, or 2D/3D asset creation or editing, even when those outputs
are produced through code or scripts. For mixed requests, apply this workflow
only to the code implementation portion.

Keep the user's selected main model responsible for design, planning, task
decomposition, and acceptance. Delegate implementation and corrective edits to
`gpt-6-luna` with `max` reasoning effort. For requests combining planning and
implementation, plan first and delegate when implementation begins. A plan-only
request does not authorize implementation.

The main agent inspects, runs, and verifies the work and revises the design;
workers make all code implementation edits, including small fixes, tests, and
integration corrections. Do not patch implementation files directly during
review or integration; delegate the required edits to a Luna/max worker.

This workflow is coordinated only by the main agent. If you are a delegated
implementation agent, complete your assigned task and report back without
spawning further agents or applying this workflow recursively.

## Delegate

- Define small, independently verifiable tasks with a goal, relevant context,
  allowed files or areas, dependencies, and acceptance criteria. Keep a small
  change as one task rather than splitting it artificially.
- Before delegation, resolve the design decisions needed for that task:
  responsibility boundaries, interfaces, data flow, expected behavior, and error
  handling where relevant. Include those decisions in the task brief, with detail
  proportional to the change; a goal alone is not an implementation plan.
- Spawn implementation agents with the actual tool settings `model:
  "gpt-6-luna"` and `reasoning_effort: "max"`, or their supported equivalents.
  Naming the model in the task prompt alone is insufficient. Where full-history
  forks prevent overrides, use a fresh or limited-context agent and supply the
  necessary design decisions and context explicitly.
- If delegation or the required model/effort is unavailable, report the blocker;
  do not silently substitute another model, effort, or main-agent implementation.
- Delegate independent tasks concurrently only when their edits will not
  conflict. Run dependent or overlapping changes sequentially and respect the
  environment's agent limits.
- Include the role boundary in every delegation and corrective brief: implement
  the supplied design without changing architecture, external behavior,
  interfaces, dependencies, or scope beyond that design. Local coding choices
  that preserve it, such as variable names and equivalent loop forms, belong to
  the worker. For an unresolved design decision or a necessary design change,
  pause the affected work and return evidence and options to the main agent.
  The main agent decides and supplies revised instructions before it resumes.
- Instruct each worker to preserve others' changes, avoid further delegation,
  run relevant checks, and return changed files, implementation results,
  validation evidence, and unresolved issues.

## Verify and retry

- Inspect the actual changes and verify behavior against the acceptance
  criteria. Use the worker's test and execution evidence where sufficient;
  perform additional checks to resolve gaps or concerns rather than repeating
  checks automatically. A completion claim alone is insufficient for acceptance.
  Verify combined behavior after tasks are integrated.
- The main agent decides whether visual inspection is needed based on the
  acceptance criteria, the change's visual risk, and available evidence.
  Changes affecting visible output do not automatically require visual
  inspection; skip it when code review and relevant checks sufficiently
  establish correctness. Use it when explicitly requested or when a material
  concern about appearance or interaction remains unresolved.
  When needed, the main agent directly inspects the running result or current
  screenshots for the relevant states and interactions. Workers may collect
  evidence, but the main agent owns visual reasoning and the verdict.
- Record **PASS** only when the required checks succeed. Record **FAIL** for
  observed defects, with the failed criterion, evidence, and concrete correction.
  Send corrective work back to a Luna/max worker and verify the result again.
- If required verification cannot run, report it as blocked and withhold PASS;
  do not treat missing evidence as an implementation defect requiring blind
  retries.
  A visual check judged unnecessary is not blocked verification and does not
  prevent PASS.
- Reassess the design and task boundaries when a failure repeats. Continue
  corrective work while it makes progress toward acceptance. If the revised
  approach still makes no progress, or an external blocker or required user
  decision prevents continuation, report the unresolved issue and what is needed
  to proceed. Respect any explicit user retry budget.

Report the final verdict and supporting checks concisely, including any blocked
verification or unresolved failures.
